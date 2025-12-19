---
"title": "Implementing docs-hinting best practices for LLMs using Claude Code"
---

Recently I implementing an LLM best practice for a docs site I wrote for my client Sensible using Claude Code.
It's an [llms.txt](https://llmstxt.org/) file at the root of a docs GitHub repo that shows the file structure of the docs and provides a brief description for each, to help LLMs interprete the docs site.

It was my first time using Claude Code, and I found it mind blowing to witness an LLM edit *local files* on *my* laptop. I'm now fired up about other docs-automation coding projects, and I've already made my first few commits on a project I'll probably blog about soon!

To return to `llms.txt` --  I'd heard that Claude Code could easily go off the rails without proper guidance, and I see it's true! Even with such a simple task there were many ways I had to guide it back out of dead-ends and oversights. The descriptions it generated in llms.txt needed some light hand editing too.

 I also then used the llms.txt to implement another best practice (adding descriptions to the frontmatter of our MD topics, a long-neglected task). I'll figure out how to automate updating llms.txt and keep the descriptions in sync using Claude Code and GitHub actions later. 
