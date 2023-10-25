---
layout: single
title: Wishlist for LLM-powered tools for SDK and API documentation
date: '2023-10-25T00:00:00.000Z'
author: frances
modified_time: '2023-10-25T00:00:00.000Z'
---

I'm writing some SDK docs from scratch, and it got me thinking about LLM-powered doc tools I'd love to see for SDKs and APIs. In no particular order:

## Language-agnostic tool to auto-generate openapi spec from codebases

I know there are tools that can generate openapi specs from codebases -- I've used some of them myself. And while I've heard it mentioned as a best practice to source an openapi spec from the code or source the code (types) from the openapi spec, I don't see that happen a ton in the wild. What most often happens is that if someone cares enough to hire me as an API docs writer, then I'm hand-maintaining the openapi spec so that I can have fine-grained control over the `description` properties -- the docs, in other words. For example: my client versions their API a lot, so I write templates for the specs and source the versioned descriptions in config files.

Given that situation, auto-generation tools are still useful to give me a skeleton spec to start from. But existing auto-gen tools are kinda a pain to install and run when you're a documentarian who doesn't work in one language or codebase; it seems as if each language has it own tool. It would be so cool if there were a LLM-powered language-agnostic tool that didn't require me to install a development environment, but just let me point it to the entire codebase and have it automatically identify the API-related portions and generated the REST API spec(s). Bonus points for traceability, like adding comments to the spec indicating which file and line(s) the LLM got an endpoint or parameter from. Additional bonus points for pulling in code comments as parameter and endpoint descriptions. I'm not sure about actually auto-generating descriptions though -- in my experience they tend to be poor quality, and then I've got to delete and edit them and it's more trouble than it's worth.



## Tool to auto-generate SDK docs from codebases

This wish item is pretty similar to the previous tool wish item. Notice that I say 'from the codebase' though, not 'from an openapi spec'.  A quality SDK will often combine or otherwise automate tricky API endpoints, so a 1:1 correspondence between an API and SDK often isn't the best user experience.

## Github action to notify me when SDK/API docs need updates

I'd love auto-generated PRs that suggest changes to my Github-sourced docs based on committed changes to the codebases. And again, bonus points for traceability -- show me what changed in the codebases that necessitate the changes.

## Rewrite SDK docs in other languages

A very tedious aspect of writing SDK docs is that you generally author docs in one language, then when that language looks good, you go and author a separate set for the next language, with only minor tweaks. (An alternate approach is one doc set with multiple tabbed code examples, but that breaks down pretty quickly in my epxerience.) In the past I've taken the approach of authoring the docs in the SDK's most important language, then farm out the other languages to engineers to write based on my example.

But what if an LLM could do the work for me? Maybe I could point the tool to one language's doc set as my 'primary docs', and specify my target languages to auto-generate. Then it could create a Github PR to update each target language any time I update my primary docs.
