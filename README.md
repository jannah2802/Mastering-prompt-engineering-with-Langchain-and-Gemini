# Mastering-prompt-engineering-with-Langchain-and-Gemini

Welcome everyone—and thanks for joining this demonstration on Mastering Prompt Engineering with LangChain and Gemini.

When we build generative AI applications, we quickly discover something important:
the real power of a large language model like Gemini doesn’t come from what it knows—
it comes from how we ask.

That’s where prompt engineering comes in.

Prompt engineering allows us to shape our inputs so that the model produces responses that are not just correct, but reliable, controllable, and context-aware. In this demo, I’ll walk you through five core prompting techniques, starting from the simplest and moving toward more advanced, chat-oriented approaches—each one giving us a greater level of control over the model’s behavior.

So let’s get started.

## Environment Setup
We begin by setting up our environment.
This project is intentionally lightweight. It relies on just a few key dependencies:

LangChain
LangChain Google Gemini
python-dotenv

By keeping only what we need, the project stays fast to set up, easy to understand, and simple to deploy.

## Exploring the Prompt Engineering Script
Next, let’s look at the main prompt engineering Python file.
We start by importing the essential libraries:

The OS module, which allows us to access environment variables
The dotenv package, which lets us securely load our Gemini API key from a .env file

We then import ChatGoogleGenerativeAI from LangChain’s Gemini connector.
This is what allows our application to communicate directly with the Gemini model.
Alongside that, we import PromptTemplate and ChatPromptTemplate, which we’ll use to construct structured and repeatable prompts.
Once the environment variables are loaded, we retrieve the Gemini API key and initialize our language model using the Gemini 2.5 Flash model.
This single LLM instance becomes the core engine behind every prompting technique you’ll see in this demo.

##1. Zero‑Shot Prompting
Let’s start with the simplest technique: zero-shot prompting.
Zero-shot prompting gives the model no examples and no constraints. It’s our baseline.
Inside the zero-shot prompting function, we define a very simple template with just one variable: the topic.
The instruction is straightforward: “Explain the topic in simple language.”
Here, Gemini relies entirely on its internal knowledge.
A key step is calling the .format() method—this safely injects the user’s input into the template and produces the final instruction string. That string is then sent to the model using llm.invoke().
Zero-shot prompting is fast and great for general questions, but it offers the least control over tone, structure, and depth.

##2. Few‑Shot (Structured) Prompting
Next, we move on to few-shot prompting.
While few-shot often refers to providing examples, here we demonstrate a structural few-shot approach—where the format itself guides the model.
This prompt explicitly defines:

The role
The goal
And the expected style

We instruct the model to provide a clear explanation using the tone, structure, and depth of a scientific explanation. We also label sections clearly—such as Topic and Explanation.
This additional structure sends a strong signal to the LLM about what we expect. Compared to zero-shot prompting, the improvement in clarity and consistency is immediately noticeable.

##3. Iterative Prompting (Chain‑of‑Thought)
For more complex tasks, we use iterative prompting, also known as the chain-of-thought technique.
Instead of asking one large question, we break the reasoning into smaller steps—essentially encouraging the model to think step by step.
This demo uses a two-stage chain:

First, we ask Gemini to produce a brief explanation of the topic.
Then, we take that output and feed it into a second prompt that expands or refines it further.

This approach significantly improves logical flow and depth, especially for complex or abstract topics. It’s a cornerstone of advanced prompt engineering.


##4. High‑Quality Prompting
Next, we introduce high-quality prompting, where we combine several best practices into a single, highly controlled template.
This prompt asks the user for:

A topic
A target audience
And a desired tone

The template enforces:

A clear role: “You are an expert instructor”
Explicit constraints
Step-by-step instructions on how the response should be delivered

Multiple variables are passed into the .format() method, resulting in an answer that dynamically adjusts its complexity, tone, and style based on user input. This shows just how powerful structured prompting can be.

##5. Chat‑Oriented Prompting
Finally, we explore chat-based prompting using ChatPromptTemplate.
This is how modern conversational AI systems manage personas and roles.
We define:

A system message that establishes a permanent persona
A user message containing the current question
And optionally, an assistant pre-fill, which injects an immediate constraint on how the model should respond

Using fromMessages(), we generate a structured list of messages in the exact format that Gemini’s chat model expects.
We even print this message structure so you can clearly see what the model receives—ensuring predictable, in-character responses every time.

##Bringing It All Together: main.py
Now let’s look at how everything comes together in main.py.
This file acts as the interactive control center of the application.
When the program starts, it displays a menu with five options:

Zero-shot prompting
Few-shot prompting
Iterative prompting
High-quality prompting
Chat prompting

There’s also an option to exit.
The script runs in a loop, waiting for the user to choose a technique. When a selection is made, the corresponding function executes—allowing users to explore each prompting style one at a time in a guided, hands-on workflow.
If the user chooses to exit, the application prints a closing message and terminates cleanly.

##Conclusion
And that brings us to the end of this demonstration.
You’ve now seen how prompt engineering evolves—from simple instructions to highly structured, conversational control—using LangChain and Gemini.
Thank you for watching.
We’ll continue with the remaining concepts and enhancements in the next demonstration.