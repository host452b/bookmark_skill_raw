Archives 
                        
                    
                    
                        

                            Categories 
                        
                    
                    

                        Blogroll 
                    
                

                
                
                
            

            

    
        
            

            

            

Since early February, I've been trying various interventions on a 163M-parameter GPT-2-style model that I
[trained from scratch on my local RTX 3090](/2025/12/llm-from-scratch-28-training-a-base-model-from-scratch),
using code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

My original model got a loss of 3.944 on my test set, while the original GPT-2
weights got 3.500 on the same dataset.  I wanted to see if I could close that gap,
and had a list of potential changes to the
training setup, and to the model itself.  Which of them would help?

I found a list of solid-looking interventions, and in [my last post](/2026/04/llm-from-scratch-32i-interventions-what-is-in-the-noise)
I came to the conclusion that the improvements in loss I had seen with all of them -- with
two possible exceptions -- seemed unlikely to be in the noise.  What would happen
if I tried to put them into a new model?

            
                

                    [[ Read more ]](/2026/04/llm-from-scratch-32j-interventions-trying-to-train-a-better-model-in-the-cloud#id_fold)
                
            

        

        
            
        

    
        
            

            

            

Towards the end of last year, I
[trained a 163M-parameter GPT-2-style model from scratch on my local RTX 3090](/2025/12/llm-from-scratch-28-training-a-base-model-from-scratch),
using code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

The result was a pretty decent little model, but it wasn't as good as the original
GPT-2-small, despite having more parameters (because it wasn't using weight-tying).
Specifically: on a particular test set, my model gave a loss of 3.944 -- quite a lot
more than the original GPT-2's 3.500 on the same dataset.

I wanted to see whether I could train a model on my own hardware (or on something that
didn't cost too much to rent in the cloud) that got closer to the original model's
performance.  So over the last few months, I've done a bunch of further training runs, each one testing
a specific intervention -- a stand-alone change that I expected to change the loss, either
for better or for worse.  Specifically:

- I trained [a baseline model](/2026/02/llm-from-scratch-32a-interventions-baseline-model) on
an 8x A100 40 GiB per GPU machine on Lambda (which
was better than my original locally-trained model, I believe due to the larger batch size
that the larger machine made possible).

- I tried [adding gradient clipping](/2026/02/llm-from-scratch-32b-interventions-gradient-clipping)
to see if that would help by limiting the effects of loss spikes.

- I tried [removing dropout](/2026/02/llm-from-scratch-32c-interventions-removing-dropout), given
that these days people tend not to use it (because we're doing single-epoch training runs).

- I tried [adding bias to the attention weight matrices](/2026/02/llm-from-scratch-32d-interventions-adding-attention-bias) --
something that was popular back in the GPT-2 era, and was used by the original weights, but which my code did not use.

- Instead of just using the learning rate of 0.0004 that was used in the code from
the book, I looked into what values people use these days, and learned how
to [schedule it over the course of the training run](/2026/03/llm-from-scratch-32e-interventions-learning-rate).

- Similarly, I learned more about [weight decay](/2026/03/llm-from-scratch-32f-interventions-weight-decay) and
tried some alternative values.

- Then I tried making my model more like the original GPT-2 one by introducing
[weight tying](/2026/03/llm-from-scratch-32g-interventions-weight-tying) to
see if that would help.

- Finally, I decided to try [training in "full-fat" float32](/2026/04/llm-from-scratch-32h-interventions-full-fat-float32)
instead of using PyTorch's AMP and TF32 matrix multiplication performance
enhancements.

At the end of all of that, I had this table showing the effect of each intervention
in terms of loss on the test set.  They're sorted from least-effective to most-effective,
and you can see the baseline in there too:

  
  Test set loss
  Improvement vs baseline

  8xa100m40-weight-tying
  3.874
  -0.182

  8xa100m40-weight-decay-cerebras
  3.867
  -0.175

  8xa100m40-baseline
  3.692
  -

  8xa100m80-no-amp
  3.679
  0.013

  8xa100m40-gradient-clipping
  3.678
  0.014

  8xa100m40-qkv-bias
  3.669
  0.023

  8xa100m40-weight-decay-gpt2
  3.643
  0.049

  8xa100m40-remove-dropout
  3.641
  0.051

  8xa100m40-schedule-learning-rate
  3.602
  0.09

Winners and losers are reasonably clear:

- Weight tying and the number for weight decay I derived from a paper by
Cerebras Research (probably without understanding it properly) were negatives.

- Full-fat float32, gradient clipping,  attention biases, the GPT-2 weight decay
parameter, removing dropout, and scheduling (and updating) the learning rate
were positives.

So, for an optimal train, we'd just use the effective interventions, right?
Well, not quite.

Full-fat float32 I decided wasn't worth the effort, as it meant that the
train took more than twice as long, and (because it required a larger machine), cost
more than three times as much.

The others did look like solid changes, but there was one concern.  The effect of
each intervention is actually pretty small.  For example, gradient clipping reduced
the loss by 0.014, from 3.692 to 3.678.  That's a 0.3% improvement.  Even the best
intervention, scheduling the learning rate, only improved things by 2%.

Could it be that some or all of these improvements were not real, but just a result
of the random nature of training deep neural networks?  Could the differences just
be in the noise?  They seemed small enough for that to be possible.

I've trained seven more models over the last few days to try to get a feel as to how
big an effect noise has for this kind of training run.  The results appear to show
that variations in the initial weights matter quite a lot, but randomness in the
training loop (given the same initial weights) actually has a fairly minimal impact.
That surprised me a bit!

Let's go through the details.

            
                

                    [[ Read more ]](/2026/04/llm-from-scratch-32i-interventions-what-is-in-the-noise#id_fold)
                
            

        

        
            
        

    
        
            

            

            

This is the last of the interventions I'm trying out to see if I can improve the
test loss for a from-scratch GPT-2 small base model, trained on code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

Back when I did my first training run for a base model, [on my local RTX 3090](/2025/12/llm-from-scratch-28-training-a-base-model-from-scratch),
I used two optimisations:

The first of those boosted training speed from 12,599 tokens per second to 15,402
in my test harness, while AMP on its own boosted it to 19,921 tps (and also allowed me
to increase the batch size from 5 to 6).  Doing both appeared to hit some kind of
diminishing returns -- it maxed out at 19,997 tps, only a little better than AMP on its
own.

But intuitively, you'd expect that might come at a cost.  While I'm sure the PyTorch
developers have solid understanding of where switching to 16-bit will have a minimal
impact on training quality, it seems too good to be true that it would have no impact
at all.

Let's see what happens if we switch both of these optimisations off!

            
                

                    [[ Read more ]](/2026/04/llm-from-scratch-32h-interventions-full-fat-float32#id_fold)
                
            

        

        
            
        

    
        
            

            

            

I've been trying to get an 8x A100 instance on Lambda Labs to do a training run for my
[LLM from scratch series](/llm-from-scratch), but they're really busy at the moment,
and it's rare to see anything.

Thanks to the wonders of agentic coding, I spent an hour today getting something up
and running to help, which I've called [lambda-manager](https://github.com/gpjt/lambda-manager).
It has three commands:

- `list-instance-types`, which prints which kinds of instances are available.

- `list-instance-type-descriptions`, which prints out all of the possible instance types (available or not)
with both their "friendly" names -- what you'd see on the website -- and the
instance type names that the API uses.

- `launch-when-available`, which polls the API until it sees a specified type of
instance, at which point it starts one and sends a Telegram message.

Let's see if that helps -- though it's been running for six hours now, with no luck...

            

        

        
            
        

    
        
            

            

            

In
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)",
he writes that weight tying, while it reduces the parameter count of a model,
in his experience makes it worse.  As such, apparently people don't use it in modern LLMs.  Intuitively, that makes
sense -- I'll explain why in this post.

But as I'm trying various [interventions](/2026/02/llm-from-scratch-32a-interventions-baseline-model) to see
if I can get my model -- based on Raschka's code, but trained for a fraction of the time that the original GPT-2 model was -- to perform as well as the original
in terms of the loss it gets on a test set, I thought it would be worth
seeing if it really is a negative for this particular tiny model of 163M parameters.

After all, the original weights use weight tying, and I did find that [QKV bias](/2026/02/llm-from-scratch-32d-interventions-adding-attention-bias)
appeared to help -- and that's
another old-school technique that they used, which has since dropped out of fashion.  Might
this one help too?

Worth a try!  Let's give it a go.

            
                

                    [[ Read more ]](/2026/03/llm-from-scratch-32g-interventions-weight-tying#id_fold)
                
            

        

        
            
        

    
        
            

            

            

I'm still working on improving the test loss for a from-scratch GPT-2 small base model, trained on code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

In my training code, I have this code to create the optimiser:

`    optimizer = torch.optim.AdamW(
        model.parameters(),
        lr=0.0004, weight_decay=0.1
    )
`

In my [last post](/2026/03/llm-from-scratch-32e-interventions-learning-rate) I looked
into the learning rate, the `lr` parameter in that code, and found a value for that,
plus some extra code to schedule it -- that is, to vary it over time -- which gave better training results.

This time I want to go into the weight decay.  What is it, what is it for, and is
0.1 really the best value?

            
                

                    [[ Read more ]](/2026/03/llm-from-scratch-32f-interventions-weight-decay#id_fold)
                
            

        

        
            
        

    
        
            

            

            

I'm still working on improving the test loss for a from-scratch GPT-2 small base model, trained on code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

In my training code, I have this code to create the optimiser:

`    optimizer = torch.optim.AdamW(
        model.parameters(),
        lr=0.0004, weight_decay=0.1
    )
`

The values in there -- `0.0004` for the learning rate, and `0.1` for the weight
decay -- were just copied from the tiny training run that we do in section 5.2 of
the book.

What do those values actually mean, and are those really the right values for them?

I felt I had a good handle on the learning rate, at least -- it's one of the first
things you learn when you start looking at machine learning of any kind -- but how would
you go about working out what the correct value for it was?
On top of that, when
I was reading [the Chinchilla paper](https://arxiv.org/abs/2203.15556) a while back,
I noticed they repeatedly referred to a "cosine cycle" for the learning rate, which didn't
fit into anything I'd learned about before.

The weight decay was pretty much an unknown for me -- I know it is a parameter
controlling the behaviour of the optimiser, but I don't know how it does that.

In this post I want to look into the learning rate, and these mysterious cosines;
I'll write a follow-up about the weight decay later.

            
                

                    [[ Read more ]](/2026/03/llm-from-scratch-32e-interventions-learning-rate#id_fold)
                
            

        

        
            
        

    
        
            

            

            

I'm still seeing what I can do to improve the test loss for a from-scratch GPT-2 small base model, trained on code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".
This is the third intervention I'm trying: adding bias to the attention weight matrices.

In the code from the book, we have this:

`class MultiHeadAttention(nn.Module):

    def __init__(
        self,
        d_in, d_out,
        context_length,
        dropout,
        num_heads,
        qkv_bias=False
    ):
        ...

        self.W_query = nn.Linear(d_in, d_out, bias=qkv_bias)
        self.W_key = nn.Linear(d_in, d_out, bias=qkv_bias)
        self.W_value = nn.Linear(d_in, d_out, bias=qkv_bias)

        ...

    def forward(self, x):
        ...

        keys = self.W_key(x)
        queries = self.W_query(x)
        values = self.W_value(x)
`

So: we initialise the weights Wq, Wk and Wv as linear layers rather than
simple matrices of weights, and have a parameter `qkv_bias` to say whether or not we should
add bias to those.  In all of our trains so far we've set that to `False`.

Why do we have this parameter, and where did it come from?

            
                

                    [[ Read more ]](/2026/02/llm-from-scratch-32d-interventions-adding-attention-bias#id_fold)
                
            

        

        
            
        

    
        
            

            

            

This is the second in my series of attempts to improve the loss on my test dataset
-- interventions, as I'm calling them --
for a from-scratch GPT-2 small base model, trained on code based on
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

Last time around I saw [what gradient clipping can do](/2026/02/llm-from-scratch-32b-interventions-gradient-clipping) --
it improved loss over [the baseline](/2026/02/llm-from-scratch-32a-interventions-baseline-model)
by 0.014, bringing it down from 3.692 to 3.678.  Not much, but it's something!

This time, I wanted to see what happened if we trained without dropout.  Would removing it make
the test loss worse, or better?

            
                

                    [[ Read more ]](/2026/02/llm-from-scratch-32c-interventions-removing-dropout#id_fold)
                
            

        

        
            
        

    
        
            

            

            

I'm still working on training the best GPT-2 small sized base model that I can
with a number of FLOPs roughly equal to two days on my own machine -- my "extra credit"
exercise after having worked through
[Sebastian Raschka](https://sebastianraschka.com/)'s book
"[Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch)".

In the [last post](/2026/02/llm-from-scratch-32a-interventions-baseline-model) I trained
a baseline model -- one with the same architecture and almost the same training code as in
the minimal training run in the book, just modified to run using DDP on an 8x A100 40 GiB/GPU
machine in the cloud.
There are a bunch of "interventions" I want to try to see if they'll make it better,
as measured by the loss they get on a test set.  I'll do a post for each intervention,
and this is the first: gradient clipping.

            
                

                    [[ Read more ]](/2026/02/llm-from-scratch-32b-interventions-gradient-clipping#id_fold)