---
layout: single
title: My wishlist for LLM-powered authoring tools for SDK and API documentation
date: '2023-10-25T00:00:00.000Z'
author: frances
modified_time: '2023-10-25T00:00:00.000Z'
---

I'm currently writing some SDK docs from scratch, and it got me thinking about my wishlist for LLM-powered doc-authoring tools for SDKs and APIs. Ignoring questions of current feasibility and in no particular order, I'd love to see:

## Rewrite SDK docs in other languages

Rewriting SDK docs for another language is often a tedious chore. I generally author and polish docs in one language, then I author a separate set for the next language. Usually the new set involves only minor tweaks compared to the first language, but they're not the sort of tweaks that a quick set of regex search and replace operations will reliably take care of. As a side note, an alternate approach is to write just one doc set with multiple tabbed code examples, but that breaks down pretty quickly in my experience.

But what if an LLM could do the work for me? Maybe I could set one language as my 'primary docs', and specify my target languages to auto-generate. The LLM could create a Github PR to update each target language any time I update my primary docs. I foresee LLM challenges for languages with very different syntaxes -- even Node versus React, for example. But I think there are many languages for which it's currently feasible!

## Language-agnostic tool to auto-generate openapi spec from codebases

Sometimes I go into a codebase completely blind about the API I need to document. In those cases, I've used existing tools that generate openapi specs from codebases. Generally the output is a skeleton that I then use to hand-write the API docs.**

But existing API spec auto-gen tools are kinda painful to install and run when you're a documentarian who doesn't work habitually in one language or codebase. It would be so cool if there were a LLM-powered language-agnostic tool that didn't require me to install a development environment, but just let me point it to the entire codebase and have it automatically identify the API-related portions and generate the REST API spec(s). Bonus points for autopopulating the `description` parameters from code comments. If there are no code comments, at this point I'd rather have empty `descriptions`; in my experience auto-generated LLM content for `descriptions` tend to be poor quality.

** Why do I generally hand-write and maintain the openapi specs that power API docs? It's a constraint I wish I wasn't working within. While I've heard it bandied about as a best practice to source an openapi spec from the code or source at least some of the code, such as types, from the openapi spec, I don't see that happen a ton in the wild. What most often happens is that if someone cares enough to hire me to write the API docs, then I'm hand-maintaining the openapi spec so that I can have fine-grained control over the `description` properties. For example: a customer versions their API a lot, so I write templates for the specs and source the versioned `description`'s in config files.


## Tool to auto-generate SDK docs from codebases

This wish item is pretty similar to the previous tool wish item. Notice that I say "from the codebase" though, not "from an openapi spec."  A quality SDK will often combine or otherwise automate tricky API endpoints, so a 1:1 correspondence between an API and SDK often isn't the best user experience.

## Github action to notify me when SDK/API docs need updates

I'd love auto-generated PRs that suggest changes to my Github-sourced docs based on committed changes to the codebases. Bonus points for traceability: easily accessible pointers to what changed in the codebases that necessitate the doc changes.

## Auto-update internal links

Links maintenance can be a big, manual process. Off the top of my head:

- If I change a page slug, give me suggestions for updating existing links. And give me configurable options for recognizing internal link syntax. For example, when I work in the Readme platform, I often use the internal syntax `[link title](doc:slug)`.
- If I delete a page, let me know about broken links.
- If I create a new page and the LLM recognizes that it's related to existing topics, ask me if I want to link to any of the existing topics. This one is probably very difficult to do well with current LLMs, because there are so many nuances about feature relationships. For example, when a new feature renders another less desireable, but not exactly obsolete, the relationship can be very hard to recognize without deep knowledge of the product.
