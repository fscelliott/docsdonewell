---
layout: single
title: 'Comparison: AI-generated developer docs vs blogs'
date: '2025-04-01T00:00:00.000Z'
author: frances
modified_time: '2025-02-25T00:00:00.000Z'
---

I'm already using LLMs in my docs writing process in an ad-hoc way, and I strongly suspect that LLMs will be a core, structured part of my docs writing tools in the near future. Doc platforms like [theneo](https://www.theneo.io/) already advertise AI-generated API docs. (Note to self: I've got to test out theneo soon!)

To test the waters with my client [Sensible](https://www.sensible.so/), I've lately been prompting LLMs to:

1. update my documentation   
2. generate technical blog posts based on my documentation.

Spoiler alert: at the moment, I've been more successful with #2 than #1. I'll dive into it briefly:

## 1. Chat GPT unreliably updated my developer docs; Claude did well

### Chat GPT-4 Turbo

I've been unimpressed by Chat's ability to maintain rigorous accuracy and keep its grabby little hands off the parts of the document I DON'T want it to update. Overall, I feel like I'm editing the work of a hasty intern. As soon as I spotted glaring errors in the LLM's response, I knew I'd have to double check each step by actually performing the documented actions myself. Frankly I'd rather author the steps myself than search for an unreliable narrator's gotchas.

Here's how my experiment went:

- Goal: update a [Zapier tutorial](https://docs.sensible.so/docs/zapier-tutorial-2) for my client Sensible to use a new file action as its trigger.

- Experiment: I iterated on prompts, getting stricter and stricter. My last attempt was:

  ```
  Rewrite the following text exactly as-is but with the following technical change:
  
  - Zap 1 now uses Google Drive's New File in Folder trigger instead of Gmail's New Attachment.
  
   Rewrite without any stylistic changes: only update it for technical accuracy where necessary. Be careful not to delete or change anything you don't absolutely need to delete.
  
  ```

- Result: Chat failed for my purposes:

  - It removed unrelated paragraphs wholesale from the update. For example, it removed a **General limitations** section.
  - It removed helpful tips, stripping down the steps to UI point-and-click interactions.
  - It failed to catch all necessary updates. For example, it retained a mention of email triggers in the introduction, which it should have updated to Google Drive.
  - It failed to give me confidence that UI terms were accurate. For example, I reference a property displayed in Zapier as **File (exists but not shown)**, which Chat changed to **File**. Based on prior experience, I didn't trust Chat to give me an accurate answer if questioned about the change. So then I had to open Zapier and click through workflows to determine if Zapier's UI changed, or if Chat has changed my style, or if there was a differently named UI element not yet on my radar.


### Claude 3.5

I gave the same restrictive prompt to Claude, and it did much better. Its changes were strictly necessary, except for a few small proofreader-type changes that improved the formatting of a Markdown header and bulleted list. I came away with a greater sense of trust and believed I could plausibly use the results in my workflow.


## 2. Claude generated a decent blog post

Based on some chatter I followed in the DevRel Collective Slack community, I didn't bother testing blog-post generation with Chat. I went straight to Claude 3.5, and the results were adequate.

I don't yet have a paid account for Claude, which means I can't persist context across prompts with their Projects features. However, I found that I could just **barely** squeeze in enough documentation as context for my one-off prompt before Claude choked on input token limits.

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

The post's content seemed bascially sound, though its structure was a bit list-happy. All my comments represented manageble improvements:

![image](https://github.com/user-attachments/assets/27890192-d46c-4535-aa74-f3ae19c81b96)


So all in all, I'll be using AIs for writing blog posts in the near future, while taking a more cautious exploratory approach with AIs and docs. Now, I'm aware I'm biased: I'm a documentarian first and foremost, so I hold my docs to a higher standard of accuracy than I do feature-release blog post announcements. That said, I'm fairly confident my results also mimick others' experience. LLMs are better at writing generalized content and can still fall down in situations where rigorous, detailed accuracy is important.

Next up, I'll post about my efforts to systematize writing AI-assisted blog posts using a paid Claude account.

