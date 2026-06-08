Deep Dive into Prompt Engineering Techniques


1. Zero-shot Prompting

. Involves presenting a task to the Al without any prior examples or context
. The Al must rely solely on its pre-trained knowledge and understanding to
generate a response

> Zero-shot Prompt: Example
List potential business strategies for a startup in
the sustainable fashion industry aiming to expand
globally within the next five years


2. One-shot Prompting
- Given single example or scenario to help guide its response to a new and similar task


Purpose

. Helps the Al understand the context or expected response format through one
example, making it adaptable to similar requests with minimal input

3. Multi-shot or Few-shot Prompting
Overview

. Provides the Al with several examples to form a better understanding of the task
before responding to a new Prompt


4. Role Prompting
Overview

. Involves assigning a specific character or role for the Al to assume while
generating responses

> As a financial advisor with a decade of experience in the
stock market, provide a beginner's guide to investing in
stocks for a young professional


5. Tabular Format Prompting
Tabular Format Prompting

Overview

. Structures the Prompt to elicit responses in a tabular format
. Useful for organizing data, comparing items, or summarizing information in a
clear and accessible way


> . Data Points: Company Name, Quarter, Revenue, Expenses, and Net Profit
. Purpose: Compare financial performance side-by-side and prepare for strategic planning

Create a table comparing the quarterly financial performance of Company A and Company B.
Use columns for Quarter, Revenue, Expenses, and Net Profit, and rows for each quarter of the
fiscal year



6. Ask Before Answering Prompting

Encourages the Al to ask clarifying questions before providing an answer
. Designed to ensure that the Al fully understands the user's query or the context of
the conversation before responding

> Ask Before Answering Prompt: Example
Before diagnosing the problem, ask the user
to describe any sounds or lights observed
when trying to turn on the computer, recent
software or hardware changes, and if the
issue occurred after these changes



7. Fill in the Blank Prompting


. Al completes a sentence or data point, making it engage more actively with
the content

. Turning the tables, where the Al is put in a position to guess or calculate the
missing information


> should use

Identify the correct protocol to fill in the blank:
"For secure remote login, a system administrator
_____(SSH/Telnet)."


8. Perspective Prompting
Overview

. Involves asking the Al to consider a situation from a specific viewpoint, or narrate
a scenario from a particular perspective, such as first-person, second-person, or
third-person


> Create requirement document from the perspective of User and Admin


9. Chain of Thought Prompting
Overview

. Guides the Al to follow a logical progression of ideas or steps before arriving at a
conclusion, helping clarify the reasoning process behind its decisions


10. Generated Knowledge Prompting


. Involves directing the Al to produce or infer new information based on its training
and current input, going beyond mere retrieval of learned data

> Given current industry trends and our
company's sustainability goals, generate
innovative strategies that could reduce our
carbon footprint by 30% over the next five years

# How to design prompts

01. Clarity and Precision
. Overview: Ensuring that Prompts are clear to
avoid misinterpretations and streamline the Al's
response processes

. Example:

❌ "Analyze client data,"
✅ "Analyze the client data from Q3 2021, focusing on revenue and customer acquisition metrics."


02. Contextual Relevance

. Overview: Embedding necessary context within the
Prompt to enhance Al's ability to understand and
address queries more effectively
. Example:
❌ "Improve our process"
✅ "Suggest improvements for our software
development lifecycle based on Agile
methodologies."



03. Use of Modifiers

. Overview: Modifiers to be used in a Prompt to specify
the response's tone, style, or format, tailoring outputs
. Example:
❌ "Draft a report on IT security"
✅ "Draft a comprehensive, client-ready report on emerging IT security threats and mitigation strategies."



04. Goal Orientation


. Overview: Aligning Prompts with specific goals helps
in directing Al's outputs
. Example:
"Review project success,"
"Evaluate the success of the XYZ project in
terms of time, budget, and scope alignment,
and prepare a presentation for the client."


Where to deploy prompt design strategies


Market Analysis and Research

. Application: Use Prompts designed with
specific modifiers
. Example: 'Conduct a comparative analysis of the
latest Al tools in the market and their adoption
rates within the healthcare sector; present findings
in a slide deck with executive summary and
detailed charts.'



# Best Practices in Prompt Engineering



## Specifying Output Format

Structured Output

Code Output

Text Output

. Concise Text: Ideal for FAQs, quick
answers, or summaries where brevity
and directness are paramount

Example Prompt for a quick FAQ:
"Provide a concise explanation of
blockchain technology suitable for a
business executive summary."

Dialogue Format:

. Interactive Dialogue: Creating scripts or
conversational Al that mimics human
interaction

Example Prompt: "Write a dialog between
a customer and a service agent where
the customer is inquiring about an
account upgrade."



01

Incorporating 'Information on
What to Do'

Discuss the method to construct
Prompts that not only seek
information but also guide the Al in
providing directions or strategies
relevant to the task at hand




02

How to be Specific and
Descriptive to Get Closer Results

Explore Techniques for crafting
detailed and precise Prompts to
minimize ambiguity and maximize
the relevance and accuracy of Al
responses




# Best Practices for Crafting Actionable Prompts

Explicit Action
Commands
01. Explicit Action Commands

Directly state the action you expect the Al to assist with,
making the Prompts directive rather than exploratory
Example

X Describe the process of encrypting a file,'
'Explain how to encrypt a file using AES encryption.'


02. Scenario-based Prompts

Embed the Al's directive within a specific scenario to
contextualize the action and increase relevance

Example

'A client has reported a breach in their data security.
List the immediate steps they should take to mitigate
the breach.'



Use of
Imperatives
03. Use of Imperatives

Employ imperative language to make commands clear
and to the point, which helps in generating concise and
precise responses

Example

'Identify the errors in the following code snippet and
provide corrections.'



04. Break Down Complex Tasks

For complex tasks, break down the action into smaller,
manageable steps that the Al can explain sequentially

Example

'You're planning a product launch. First, outline the market
research needed. Next, describe how to analyze the
research data, followed by strategies for marketing based
on the data.'




05. Include Decision Points
Structure the Prompt to not only provide actions but also to
evaluate choices or decision points

Example

'Assess whether to use machine learning or traditional
algorithms for this data set. Provide reasons for your choice
and outline steps to implement the selected method.'





Real-world Application Examples

Business Strategy Development

Craft Prompts that direct business
leaders on how to proceed with
strategic planning sessions, including:

· SWOT analysis
. Market positioning
· Competitive analysis




Software Development

Craft Prompts that direct development
teams on next steps based on current
project status, such as:

· Debugging strategies
. Code refactoring priorities
. New feature development based on
user feedback



How to be Specific and Descriptive to Get Closer Results




01

Define the Context Clearly


'Tell me about stock markets.'

'Provide a detailed analysis of the current
trends in the U.S. stock market focusing
on technology stocks post-2020.'

02

Use Precise Language


---
'Design a responsive HTML website with
a homepage, about page, and contact
form, using Bootstrap for styling.'

---



03

Include Relevant Details

04

Specify the Desired Format

05

Ask for Examples



Technical Documentation

Specifically ask for
. Code snippets
. Parameter descriptions
. Sample output

Makes the manuals more practical
and helpful


