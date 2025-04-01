---
layout: single
title: 'Comparison: AI-generated developer docs vs blogs'
date: '2025-04-01T00:00:00.000Z'
author: frances
modified_time: '2025-02-25T00:00:00.000Z'
---

I'm sure that generating developer documents with the assistance of LLMs is in my near future. Doc platforms like  [theneo](https://www.theneo.io/) already advertise the capacity to generate API docs for you with LLMs. (Note to self: I've got to test out theneo soon!)

I've been experimenting lately with prompting LLMs to:

1. update my documentation   
2. generate technical blog posts based on my documentation.

Spoiler alert: at the moment, I've been more successful with #2 than #1. I'll dive into it briefly:

## Chat GPT unreliably updated my developer docs

I've been unimpressed by Chat's ability to maintain rigorous accuracy and keep its grabby little hands off the parts of the document I DON'T want it to update. Overall, I have an impression of having to correct the work of some hasty intern who didn't actually test if the steps they listed are accurate. As soon as they gave me back a response and I spotted some glaring errors, I knew I'd have to double check each step by actually performing the documented actions myself. In that case, frankly I'd rather author the steps myself than search for gotchas authored by the 'unreliable intern.'

Here's how my experiment went:

- Goal: update a [Zapier tutorial](https://docs.sensible.so/docs/zapier-tutorial-2) for my client Sensible to use a new file action as its trigger.

- Experiment: I iterated on prompts, getting stricter and stricter. My last attempt was:

  ```
  Rewrite the following text exactly as-is but with the following technical change:
  
  - Zap 1 now uses Google Drive's New File in Folder trigger instead of gmail's New Attachment.
  
   Rewrite without any stylistic changes—only update it for technical accuracy where necessary. Be careful not to delete anything you don't need to delete.
  
  ```

- Result: Chat failed for my purposes:

  - It removed unrelated paragraphs wholesale from the update (for example, it removed a **General limitations** section)
  - It removed helpful tips that I'd included mixed in with the UI instructions.
  - It failed to catch all necessary updates (for example, retaining a mention of email triggers in the introduction, which it should have updated to Google Drive)
  - It failed to give me confidence that UI terms were accurate. For example, I reference a property displayed in Zapier as **File (exists but not shown)**, which Chat changed to **File**. Now I have to open Zapier and click through workflows to determine if Zapier's UI changed, or if Chat has changed my style, or if there's a differently named UI element I'm not aware of. I wouldn't trust Chat not to hallucinate an answer to these questions.


That said, I'm sure that with the right LLM, the right docs as context, and the right prompts, I'll succeed soon at updating docs using LLMs. 

## Claude 3.5 generated a plausible blog post

 On the other hand, I was much more impressed by LLM-assisted blog posts. I found that I could just **barely** squeeze in enough documentation as context for my prompt before Claude choked on input token limits, at least with my free account.

I gave Claude a two-part prompt:

```
# prompt 1:
You're a developer advocate for Sensible. I'll be asking you to write a technical blog post in a minute. First, here's some background information about Sensible to get you up to speed.

# prompt 2:
I want you to write a blog post about our agentic LLM-based workflows for extracting data from documents.  These rely on the source_ids parameter. Here are some documents for reference  some key points to touch are: - in combination with the Conditional method, this lets you execute agentic LLM 'bot' style workflows - this lets you tackle extracting data from documents that might previously have been impossible (e.g., documents were too long, LLM prompts were too complex to author) - position the new feature as an addition to our existing LLM document data extraction features and briefly mention some of them
```

I gave it [four of my key documentation topics](https://github.com/fscelliott/docsdonewell/tree/master/assets/prompts/llms_1/key_topics) as the context for the first prompt, and [abbreviated docs](https://github.com/fscelliott/docsdonewell/tree/master/assets/prompts/llms_1/blog_post_source_ids) on the feature itself for the second prompt.

It did fairly well!

Here's an excerpt:

````
# Unlock Advanced Document Processing with Agentic LLM Workflows in SenseML

At Sensible, we're constantly enhancing our document processing capabilities to help developers tackle increasingly complex extraction challenges. Today, we're excited to highlight one of our most powerful features: agentic LLM workflows through chained prompts using the `source_ids` parameter.

## The Problem: Complex Documents Require Sophisticated Extraction

Document processing isn't always straightforward. Many documents present challenges like:

- Lengthy multi-page content where LLMs struggle with context windows
- Complex data relationships requiring multi-step reasoning
- Variable document formats that need conditional processing logic
- Nested or hierarchical data structures

Traditional extraction approaches often fall short with these documents, requiring developers to build custom workarounds or resort to manual processing.

## Enter Agentic LLM Workflows with Chained Prompts

Sensible's `source_ids` parameter unlocks a new paradigm in document processing by enabling you to:

1. **Chain LLM prompts sequentially** - Extract data with one prompt, then apply further prompts to that extracted data
2. **Create targeted extractions** - Narrow the context for your prompts to specific parts of a document
3. **Transform and refine data** - Reformat or analyze previously extracted fields with subsequent prompts
4. **Execute conditional workflows** - When combined with our Conditional method, create dynamic extraction paths based on document contents

This approach mirrors the way human experts process complex documents - by breaking down the task into manageable steps, focusing attention on relevant sections, and making decisions based on previously discovered information.

## How It Works: The Power of `source_ids`

Let's look at how this works in practice with the Query Group method:

```json
{
  "method": {
    "id": "queryGroup",
    "queries": [
      {
        "id": "_transactions",
        "description": "Extract all transactions with date, merchant, description, and amount"
      }
    ]
  }
},
{
  "method": {
    "id": "queryGroup",
    "source_ids": ["_transactions"],
    "queries": [
      {
        "id": "freq_merchant",
        "description": "What is the most frequent merchant?"
      },
      {
        "id": "max_transaction_amount",
        "description": "What is the maximum transaction amount?"
      }
    ]
  }
}
```

In this example:

1. First, we extract a transaction table from the document
2. Then, we analyze that extracted data to find the most frequent merchant and maximum transaction amount

By targeting the second set of queries specifically at the `_transactions` field, we get more accurate results and simplify the LLM's task.

// continued...
````



Now, I'm aware my interpretation of these results is biased: I'm a documentarian first and foremost, so I hold my docs to a higher standard than I do feature-release blog post announcements. That said, for work-a-day technical blog posts,  Claude seems like a reasonable tool.

