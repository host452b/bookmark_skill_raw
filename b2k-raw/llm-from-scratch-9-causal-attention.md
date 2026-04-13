Archives 
                        
                    
                    
                        

                            Categories 
                        
                    
                    

                        Blogroll 
                    
                

                
                
                
            

            

    

    

    

My trek through [Sebastian Raschka](https://sebastianraschka.com/)'s
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)"
continues...
[Self-attention was a hard nut to crack](/2025/03/llm-from-scratch-8-trainable-self-attention),
but now things feel
a bit smoother -- fingers crossed that lasts!
So, for today: a quick dive into causal attention, the next part of chapter 3.

Causal attention sounds complicated, but it
just means that when we're looking at a word, we don't pay any attention to the words
that come later.  That's pretty natural -- after all, when we're
reading something, we don't need to look at words later on to understand what
the word we're reading now means (unless the text is *really* badly written).

It's
"causal" in the sense of causality -- something can't have an effect on something that came before
it, just like causes can't some after effects in reality.  One big plus about
getting that is that I finally now understand why I was using a class called
`AutoModelForCausalLM` for my earlier [experiments in fine-tuning LLMs](/fine-tuning).

Let's take a look at how it's done.

    
        
        

The book takes this is in two steps -- firstly, the way that's easy to understand,
and then an optimised version -- I'll do the same here.

First, a quick recap from last time: how self-attention works out context
vectors from inputs.  The inputs are in X, and we have the
query weights matrix Wq, the key weights matrix Wk, and the
value weights matrix Wv.

- Firstly, we project the inputs into the query, key and value spaces:

Q=XWq

K=XWk

V=XWv

- Next, we work out our attention scores as the dot product of the inputs in
query space with the transpose of the inputs in key space.

Ω=QKT

- Then we normalise them to attention weights by dividing by the square root of the
number of dimensions in key space, and applying softmax row-wise.

A=softmax(Ωc, axis=1)

- Finally, we multiply that by the inputs in value space to get context vectors.

C=AV

So let's think about how to stop tokens from knowing about stuff in the future.
Imagine that the attention weights matrix A looks like this:

  Token
  ω("The")
  ω("fat")
  ω("cat")
  ω("sat")
  ω("on")
  ω("the")
  ω("mat")

  The
  0.2642
  0.1312
  0.2057
  0.1074
  0.0972
  0.0972
  0.0972

  fat
  0.1202
  0.2674
  0.2189
  0.0984
  0.0984
  0.0984
  0.0984

  cat
  0.1419
  0.1733
  0.2117
  0.1568
  0.1051
  0.0951
  0.1162

  sat
  0.0933
  0.0844
  0.1974
  0.2294
  0.1139
  0.1031
  0.1786

  on
  0.0854
  0.0944
  0.1274
  0.1556
  0.2321
  0.1152
  0.1900

  the
  0.1006
  0.1006
  0.1006
  0.1006
  0.1112
  0.2735
  0.2130

  mat
  0.0833
  0.0833
  0.1018
  0.1854
  0.1678
  0.1518
  0.2265

The rows are the tokens and the columns for each one are its attention weights for
each token in the input, including itself.  We want the first "The" to only have a
weight for itself, "fat" to have weights for the first "The" and itself, and so on.

What if we zero out every number above the diagonal that
runs top left to bottom right, like this:

  Token
  ω("The")
  ω("fat")
  ω("cat")
  ω("sat")
  ω("on")
  ω("the")
  ω("mat")

  The
  0.2642
  0
  0
  0
  0
  0
  0

  fat
  0.1202
  0.2674
  0
  0
  0
  0
  0

  cat
  0.1419
  0.1733
  0.2117
  0
  0
  0
  0

  sat
  0.0933
  0.0844
  0.1974
  0.2294
  0
  0
  0

  on
  0.0854
  0.0944
  0.1274
  0.1556
  0.2321
  0
  0

  the
  0.1006
  0.1006
  0.1006
  0.1006
  0.1112
  0.2735
  0

  mat
  0.0833
  0.0833
  0.1018
  0.1854
  0.1678
  0.1518
  0.2265

That's easy enough to do, and Raschka shows how to do it in PyTorch by creating
a matrix the same size as A, with 1s on and below that diagonal and 0s above
(using `torch.tril`, a helper designed for exactly this kind of thing) and then
using an element-wise multiplication to use it to mask out A.

He then points out that the rows don't sum up to 1 any more; he doesn't say why
that's important -- though it is a constraint that's been applied to attention
weights throughout -- but intuitively it does make sense.

We're going to be multiplying
value-space projections of the inputs by these weights, and then adding them up
to get context vectors.
If we used the weights above when doing that, the context vector
for the first "The" would be just 0.2642 times its own value-space projection,
while the one for "mat" would be seven vectors multiplied by a set of weights that
added up to one.

Assuming that the value-space vectors are roughly the same size,
that would make the context vector for the first token *much* smaller than the one
for the last.  So without re-normalising these
weights, we would wind up with a set of context vectors where the ones for later
words were artificially inflated.  Not ideal.

So, Raschka shows how to fix this easily -- we use PyTorch to
generate an m×1 matrix containing the sums of all of the rows, and then use
a broadcast division to divide every item in every row by that row's sum.  The
sums are all ≤1, so this basically scales them up so that the rows all add
up to 1 again.  For example, in the first row 0.2642 is divided by itself to
become 1, and in the second row, with a sum of 0.3876, the values
become 0.1202÷0.3876=0.31011 and 0.2674÷0.3876=0.6899, which sum
to 1, and so on.

Once that's done, we can just use this new attention weights matrix -- let's call
it A′ -- and:

C=A′V

...gives us a set of context vectors where each token only pays attention to
tokens that came before it, plus itself.

Now, that method is easy to understand, but it has that ugly thing where
we normalise using softmax, then we mask, but then we have to do another normalisation
step to patch up the mess.  So the second solution Raschka shows is smarter:

Firstly, we mask off the attention scores rather than the attention weights -- that
is, where in the earlier solution we were operating on A, the result of step 3 above,
now we start off with Ω, the result of step 2.

The next step is to use masking slightly differently.  In the first example, he
used this to create a mask:

`mask_simple = torch.tril(torch.ones(context_length, context_length))
`

`torch.tril` is "triangle lower" -- that is, it sets everything *below* and including
the top-left
to bottom-right diagonal to the provided value.  Everything above is set to zero.
That meant that when we multiplied A by it element-wise, all of the top-right
part was zeroed out.

This time around, he uses:

`mask = torch.triu(torch.ones(context_length, context_length), diagonal=1)
`

There are two important differences; `torch.triu` is "triangle upper", as you probably
guessed, but we also have that `diagonal=1` kwarg.  Now, pretty clearly, the goal
is to produce the inverse of the original mask, and for the parts of the matrix that
aren't on the diagonal, just

`mask = torch.triu(torch.ones(context_length, context_length))
`

...would achieve that.  But both `tril` and `triu` include the diagonal by default,
so we'd be masking it out if that was all we did.  The `diagonal=1` is there in Raschka's
code to say "shift the boundary up by one"
so that it isn't included.  (Likewise, `diagonal=-1`
would shift it downwards -- not useful in this case, but I'm sure it is at other times.)

So, `mask` is the inverse of `mask_simple` -- it has 1s in the locations where we
want to drop values, as opposed to the locations where we want to keep them.

Next, we use the `masked_fill` method on Ω (which is called `attn_scores` in
the code) -- that just uses our `mask`
(coerced to a `bool`, which makes logical sense) to replace the masked values with
negative infinity:

`masked = attn_scores.masked_fill(mask.bool(), -torch.inf)
`

...and then we can just do the original one-time normalisation -- divide by the
square root of the key dimensions and run it through row-wise softmax, and we're done!
No extra normalisation step required.

I was wondering why we replaced with negative infinity here rather than zero,  but
a little experimentation with softmax showed that zeros in the input to the function
do not map to zero in the output -- my gloss of it as "boosting the big values,
deboosting the small ones, and making sure everything adds up to one" was not right,
because it would suggest that zero remains zero.

For example:

`In [1]: import torch

In [2]: import torch.nn.functional as F

In [3]: x = torch.tensor([1.0, 2.0, 3.0, 0.0, 0.0])

In [4]: softmax_result = F.softmax(x, dim=0)

In [5]: print(softmax_result)
tensor([0.0844, 0.2295, 0.6239, 0.0311, 0.0311])
`

You can see that the zeros have become 0.0311s.  I feel that getting a solid
intuitive understanding of how softmax works would be one of the side quests I'm
trying to avoid when working through this book (though I note that it uses items
in the list as powers, eg. ex, and taking something to the zeroth power is 1, so
that gives a hint).  But either way, it makes some kind of sense that if anything is
going to turn into zero after being run through softmax (especially with that exponent)
it's going to be minus infinity.

Anyway: replace the attention scores that we want to throw away with minus infinity
with a masking operation, then do our normal normalisation, and we have causal
attention!

That was actually quite a lot more than I planned to write on this bit, as it's
only a few pages in the book, and was much easier to understand than the last section.

But there's one thing that the book doesn't go into -- something that I had to do
a bit of extra research about.  As a long-time techie, the fact that we're doing
all of the work to calculate all of the attention scores and then throwing almost
half of them away pained me.  And then, when we do the second multiplication to
work out the context vectors, almost half of the multiplications will be by zero
-- so, more wasted work.

How could it be that this core algorithm for LLMs would be wasting pretty much half
of the CPU (or more likely, GPU) cycles?

The answer, of course, is that in practice, people don't use exactly this algorithm.
What we're doing in this
book is going through a textbook example, and a simple linear factor in (in)efficiency
isn't an enormous deal.  Real-world implementations might use specialised CUDA kernels
that have "triangular" matrix multiplication that just skips the masked-out
parts of our matrices automatically, or would use adjusted versions of self-attention
that -- while they're performing the same (or pretty much the same) underlying
maths, will work in a completely different way --
[FlashAttention](https://github.com/Dao-AILab/flash-attention) came up several times
when I was looking into this.

So I think that will have to go onto the ever-growing pile of things I can
look into once I'm done with the book :-)  For now, I'm done with causal attention,
and the next post will be looking into dropout -- another simple concept, I think
-- and also how we can do batching, when processing a single input already requires
us to use matrices.  Should be fun!

See you next time, and -- as always, comments, corrections,
or questions are very welcome.

[Here's a link to the next post in this series](/2025/03/llm-from-scratch-10-dropout).