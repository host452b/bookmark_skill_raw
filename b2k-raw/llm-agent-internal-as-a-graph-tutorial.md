*Ever wondered how AI agents actually work behind the scenes? This guide breaks down how agent systems are built as simple graphs - explained in the most beginner-friendly way possible!*

*Note: This is a super-friendly, step-by-step version of the [official PocketFlow Agent documentation](https://the-pocket.github.io/PocketFlow/design_pattern/agent.html). We've expanded all the concepts with examples and simplified explanations to make them easier to understand.*

Have you been hearing about "LLM agents" everywhere but feel lost in all the technical jargon? You're not alone! While companies are racing to build increasingly complex AI agents like GitHub Copilot, PerplexityAI, and AutoGPT, most explanations make them sound like rocket science.

**Good news: they're not.** In this beginner-friendly guide, you'll learn:- 

The surprisingly simple concept behind all AI agents
- 

How agents actually make decisions (in plain English!)
- 

How to build your own simple agent with just a few lines of code
- 

Why most frameworks overcomplicate what's actually happening

*Check out my YouTube Video on this topic:*

In this tutorial, we'll use **[PocketFlow](https://github.com/The-Pocket/PocketFlow)**[ ](https://github.com/The-Pocket/PocketFlow)- a tiny 100-line framework that strips away all the complexity to show you how agents really work under the hood. Unlike other frameworks that hide the important details, PocketFlow lets you see the entire system at once.

Most agent frameworks hide what's really happening behind complex abstractions that look impressive but confuse beginners. [PocketFlow](https://github.com/the-pocket/PocketFlow) takes a different approach - it's just **[100 lines of code](https://github.com/The-Pocket/PocketFlow/blob/main/pocketflow/__init__.py)** that lets you see exactly how agents work!

Benefits for beginners:- 

**Crystal clear**: No mysterious black boxes or complex abstractions
- 

**See everything**: The entire framework fits in one readable file
- 

**Learn fundamentals**: Perfect for understanding how agents really operate
- 

**No baggage**: No massive dependencies or vendor lock-in

Instead of trying to understand a gigantic framework with thousands of files, PocketFlow gives you the fundamentals so you can build your own understanding from the ground up.

Imagine our agent system like a kitchen:- 

**[Nodes](https://the-pocket.github.io/PocketFlow/core_abstraction/node.html)** are like different cooking stations (chopping station, cooking station, plating station)
- 

**[Flow](https://the-pocket.github.io/PocketFlow/core_abstraction/flow.html)** is like the recipe that tells you which station to go to next
- 

**[Shared store](https://the-pocket.github.io/PocketFlow/core_abstraction/communication.html)** is like the big countertop where everyone can see and use the ingredients

In our kitchen (agent system):- 

Each station (Node) has three simple jobs:

**Prep**: Grab what you need from the countertop (like getting ingredients)
- 

**Exec**: Do your special job (like cooking the ingredients)
- 

**Post**: Put your results back on the countertop and tell everyone where to go next (like serving the dish and deciding what to make next)
- 

The recipe (Flow) just tells you which station to visit based on decisions:

"If the vegetables are chopped, go to the cooking station"
- 

"If the meal is cooked, go to the plating station"

Let's see how this works with our research helper!

An LLM (Large Language Model) agent is basically a smart assistant (like ChatGPT but with the ability to take actions) that can:- 

Think about what to do next
- 

Choose from a menu of actions
- 

Actually do something in the real world
- 

See what happened
- 

Think again...

Think of it like having a personal assistant managing your tasks:- 

They review your inbox and calendar to understand the situation
- 

They decide what needs attention first (reply to urgent email? schedule a meeting?)
- 

They take action (draft a response, book a conference room)
- 

They observe the result (did someone reply? was the room available?)
- 

They plan the next task based on what happened

Here's the mind-blowing truth about agents that frameworks overcomplicate:

That's it! Every agent is just a graph with:- 

A **decision node** that branches to different actions
- 

**Action nodes** that do specific tasks
- 

A **finish node** that ends the process
- 

**Edges** that connect everything together
- 

**Loops** that bring execution back to the decision node

No complex math, no mysterious algorithms - just nodes and arrows! Everything else is just details. If you dig deeper, you’ll uncover these hidden graphs in overcomplicated frameworks:

Let’s see how the graph actually works with a simple example.

Imagine we want to build an AI assistant that can search the web and answer questions - similar to tools like Perplexity AI, but much simpler. We want our agent to be able to:- 

Read a question from a user
- 

Decide if it needs to search for information
- 

Look things up on the web if needed
- 

Provide an answer once it has enough information

Let's break down our agent into individual "stations" that each handle one specific job. Think of these stations like workers on an assembly line - each with their own specific task.

Here's a simple diagram of our research agent:

In this diagram:- 

**DecideAction** is our "thinking station" where the agent decides what to do next
- 

**SearchWeb** is our "research station" where the agent looks up information
- 

**AnswerQuestion** is our "response station" where the agent creates the final answer

Imagine you asked our agent: "Who won the 2023 Super Bowl?"

Here's what would happen step-by-step:- 

**DecideAction station**:

LOOKS AT: Your question and what we know so far (nothing yet)
- 

THINKS: "I don't know who won the 2023 Super Bowl, I need to search"
- 

DECIDES: Search for "2023 Super Bowl winner"
- 

PASSES TO: SearchWeb station
- 

**SearchWeb station**:

LOOKS AT: The search query "2023 Super Bowl winner"
- 

DOES: Searches the internet (imagine it finds "The Kansas City Chiefs won")
- 

SAVES: The search results to our shared countertop
- 

PASSES TO: Back to DecideAction station
- 

**DecideAction station (second time)**:

LOOKS AT: Your question and what we know now (search results)
- 

THINKS: "Great, now I know the Chiefs won the 2023 Super Bowl"
- 

DECIDES: We have enough info to answer
- 

PASSES TO: AnswerQuestion station
- 

**AnswerQuestion station**:

LOOKS AT: Your question and all our research
- 

DOES: Creates a friendly answer using all the information
- 

SAVES: The final answer
- 

FINISHES: The task is complete!

This is exactly what our code will do - just expressed in programming language.

Let's build each of these stations one by one and then connect them together!

The **DecideAction** node is like the "brain" of our agent. Its job is simple:- 

Look at the question and any information we've gathered so far
- 

Decide whether we need to search for more information or if we can answer now

Let's build it step by step:```
`class DecideAction(Node):
    def prep(self, shared):
        # Think of "shared" as a big notebook that everyone can read and write in
        # It's where we store everything our agent knows

        # Look for any previous research we've done (if we haven't searched yet, just note that)
        context = shared.get("context", "No previous search")

        # Get the question we're trying to answer
        question = shared["question"]

        # Return both pieces of information for the next step
        return question, context`
```

First, we created a `prep` method that gathers information. Think of `prep` like a chef gathering ingredients before cooking. All it does is look at what we already know (our "context") and what question we're trying to answer.

Now, let's build the "thinking" part:```
`    def exec(self, inputs):
        # This is where the magic happens - the LLM "thinks" about what to do
        question, context = inputs

        # We ask the LLM to decide what to do next with this prompt:
        prompt = f"""
### CONTEXT
You are a research assistant that can search the web.
Question: {question}
Previous Research: {context}

### ACTION SPACE
[1] search
  Description: Look up more information on the web
  Parameters:
    - query (str): What to search for

[2] answer
  Description: Answer the question with current knowledge
  Parameters:
    - answer (str): Final answer to the question

## NEXT ACTION
Decide the next action based on the context and available actions.
Return your response in this format:

```yaml
thinking: |
    &lt;your step-by-step reasoning process&gt;
action: search OR answer
reason: &lt;why you chose this action&gt;
search_query: &lt;specific search query if action is search&gt;
```"""

        # Call the LLM to make a decision
        response = call_llm(prompt)

        # Pull out just the organized information part from the LLM's answer
        # (This is like finding just the recipe part of a cooking video)
        yaml_str = response.split("```yaml")[1].split("```")[0].strip()
        decision = yaml.safe_load(yaml_str)  # Convert the text into a format our program can use

        return decision`
```

The `exec` method is where the actual "thinking" happens. Think of it like the chef cooking the ingredients. Here, we:- 

Create a prompt that explains the current situation to the LLM
- 

Ask the LLM to decide whether to search or answer
- 

Parse the response to get a clear decision

Finally, let's save the decision and tell the flow what to do next:```
`    def post(self, shared, prep_res, exec_res):
        # If the LLM decided to search, save the search query
        if exec_res["action"] == "search":
            shared["search_query"] = exec_res["search_query"]

        # Return which action to take - this tells our flow where to go next!
        return exec_res["action"]  # Will be either "search" or "answer"`
```

The `post` method is where we save results and decide what happens next. Think of it like the chef serving the food and deciding what dish to prepare next. We save the search query if needed, and then return either "search" or "answer" to tell our flow which node to visit next.

The **SearchWeb** node is our "researcher." Its only job is to:- 

Take a search query
- 

Look it up (in this simple example, we'll fake the results)
- 

Save what it finds
- 

Tell the agent to decide what to do with this new information

Let's build it:```
`class SearchWeb(Node):
    def prep(self, shared):
        # Simply get the search query we saved earlier
        return shared["search_query"]`
```

The `prep` method here just grabs the search query that was saved by the DecideAction node.```
`    def exec(self, search_query):
        # This is where we'd connect to Google to search the internet
        # Set up our connection to Google
        search_client = GoogleSearchAPI(api_key="GOOGLE_API_KEY")

        # Set search parameters
        search_params = {
            "query": search_query,
            "num_results": 3,
            "language": "en"
        }

        # Make the API request to Google
        results = search_client.search(search_params)

        # Format the results into readable text
        formatted_results = f"Results for: {search_query}\n"

        # Process each search result
        for result in results:
            # Extract the title and snippet from each result
            formatted_results += f"- {result.title}: {result.snippet}\n"

        return formatted_results`
```

The `exec` method connects to a search API, sends the query, and formats the results. In a real implementation, you would need to sign up for a search API service like Google Custom Search API and get your own API key.```
`    def post(self, shared, prep_res, exec_res):
        # Store the search results in our shared whiteboard
        previous = shared.get("context", "")
        shared["context"] = previous + "\n\nSEARCH: " + shared["search_query"] + "\nRESULTS: " + exec_res

        # Always go back to the decision node after searching
        return "decide"`
```

The `post` method saves our search results by adding them to our shared context. Then it returns "decide" to tell our flow to go back to the DecideAction node so it can think about what to do with this new information.

The **AnswerQuestion** node is our "responder." Its job is simply to:- 

Take all the information we've gathered
- 

Create a friendly, helpful answer
- 

Save that answer for the user

Let's build it:```
`class AnswerQuestion(Node):
    def prep(self, shared):
        # Get both the original question and all the research we've done
        return shared["question"], shared.get("context", "")`
```

The `prep` method gathers both the original question and all the research we've collected.```
`    def exec(self, inputs):
        question, context = inputs
        # Ask the LLM to create a helpful answer based on our research
        prompt = f"""
### CONTEXT
Based on the following information, answer the question.
Question: {question}
Research: {context}

## YOUR ANSWER:
Provide a comprehensive answer using the research results.
"""
        return call_llm(prompt)`
```

The `exec` method asks the LLM to create a helpful answer based on our research.```
`    def post(self, shared, prep_res, exec_res):
        # Save the answer in our shared whiteboard
        shared["answer"] = exec_res

        # We're done! No need to continue the flow.
        return "done"`
```

The `post` method saves the final answer and returns "done" to indicate that our flow is complete.

Now for the fun part - we need to connect all our nodes together to create a working agent!```
`# First, create instances of each node
decide = DecideAction()
search = SearchWeb()
answer = AnswerQuestion()

# Now connect them together - this is where the magic happens!
# Each connection defines where to go based on the action returned by post()

# If DecideAction returns "search", go to SearchWeb
decide - "search" &gt;&gt; search

# If DecideAction returns "answer", go to AnswerQuestion
decide - "answer" &gt;&gt; answer

# After SearchWeb completes, go back to DecideAction
search - "decide" &gt;&gt; decide

# Create our flow, starting with the DecideAction node
flow = Flow(start=decide)`
```

That's it! We've connected our nodes into a complete flow that can:- 

Start by deciding what to do
- 

Search for information if needed
- 

Loop back to decide if we need more information
- 

Answer the question when we're ready

Think of it like a flowchart where each box is a node, and the arrows show where to go next based on decisions made along the way.

Now let's see our agent in action:```
`# Create a shared whiteboard with just a question
shared = {"question": "What is the capital of France?"}

# Run our flow!
flow.run(shared)

# Print the final answer
print(shared["answer"])`
```

Here's what happens when our agent runs:

First, our agent thinks about the question:```
`thinking: |
  The question is asking about the capital of France. I don't have any prior search results to work with.
  To answer this question accurately, I should search for information about France's capital.
action: search
reason: I need to look up information about the capital of France
search_query: capital of France`
```

Our agent decides it doesn't know enough yet, so it needs to search for information.

The SearchWeb node now searches for "capital of France" and gets these results:```
`Results for: capital of France
- The capital of France is Paris
- Paris is known as the City of Light`
```

It saves these results to our shared context.

Our agent looks at the question again, but now it has some search results:```
`thinking: |
  Now I have search results that clearly state "The capital of France is Paris".
  This directly answers the question, so I can provide a final answer.
action: answer
reason: I now have the information needed to answer the question`
```

This time, our agent decides it has enough information to answer!

Finally, the AnswerQuestion node generates a helpful response:```
`The capital of France is Paris, which is also known as the City of Light.`
```

And we're done! Our agent has successfully:- 

Realized it needed to search for information
- 

Performed a search
- 

Decided it had enough information
- 

Generated a helpful answer

If you’re technically inclined and want to read or experiment with the complete code for this tutorial, you can find it [here](https://github.com/The-Pocket/PocketFlow/tree/main/cookbook/pocketflow-agent)!

You can also see how this same loop-and-branch pattern appears in larger frameworks by checking out these snippets:

Now you know the secret - LLM agents are just **loops with branches**:- 

**Think** about the current state
- 

**Branch** by choosing one action from multiple options
- 

**Do** the chosen action
- 

**Get results** from that action
- 

**Loop back** to think again

The "thinking" happens in the prompt (what we ask the LLM), the "branching" is when the agent chooses between available tools, and the "doing" happens when we call external functions. Everything else is just plumbing!

Next time you see a complex agent framework with thousands of lines of code, remember this simple pattern and ask yourself: "Where are the decision branches and loops in this system?"

Armed with this knowledge, you'll be able to understand any agent system, no matter how complex it may seem on the surface.

*Want to learn more about building simple agents? Check out [PocketFlow on GitHub](https://github.com/the-pocket/PocketFlow)!*