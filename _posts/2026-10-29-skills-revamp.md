---
title: "Building deterministic testing harness for AI-generated docs"
---

LLMs don't write quality developer docs without a ton of deterministic guardrails *and* human near the loop or human in the loop. That's what I hear from those neck-deep in inventing AI doc gen best practices, and I agree. I've already introduced deterministic tests into my AI doc gen workflows to a certain extent, but after reading [Docs as Test](https://www.docsastests.com/), I'm getting a lot more granular and systematic:

### Embedded test
It was a revelatory thought at the time that now seems perfectly obvious: I'm  introducing deterministic, in-line tests embedded as HTML comments into my docs so a test runner can verify before the docs even come to my review. My doc gen workflows generate the tests before they even author new docs content, then embed them into the generated docs.

For example, for a new troubleshooting table I generated, I also generated a test fixture for every row in the table, which I set up to run monthly.

I get back a nice HTML report on every GitHub Action run:
 <img width="477" height="545" alt="image" src="https://github.com/user-attachments/assets/69d8af08-90e5-4e9b-878b-f3e8a9236cb8" />

Under the hood, the HTML comments direct the test runner that powers the report:
<img width="536" height="511" alt="image" src="https://github.com/user-attachments/assets/167da416-99ac-4d67-a4db-2da30faaf563" />

This will, in time, lead to a grand vision of 'self-healing' docs -- a term I can already tell will be abused, but at its finest, has a ton of infrastructure behind it.

### Eval-driven docs workflows
- I'm auditing and parsing the logs of my doc-gen workflows so I can deterministically pass/fail workflows that skip steps and start to build more sophisticated evals for workflows (to date, my eval-writing has been limited pretty much to "does the built-in MCP server our docs platform provided with us  serviceable  search results?") I especially want to add in *ablation* evals so that when LLMs models uplift their capacities, my skills auto-trim themselves so they don't actively drag down the new models. I've already witnessed that Opus 5.5 markedly improved my doc gen output from Opus 4.5, without any rewrites to my skills; now I need to find out if my skills are actually hindering Opus 5.5 with bloated content. I hear lots of anti-skill talk out there, and while I'm not abandoning them, I do want to push everything I can into hooks, scripts, etc.

 
I feel late to the "docs as test" and eval-driven party...but actually I'm pretty sure I'm *just* behind the cutting-edge documentarian practitioners whose mad-scientist vibes I adore. That's a place I like to be; I keep an eye on the pioneers for a couple months, hear out their lessons learned in real time on Slack, and then start implementing myself. For example, a few months back, I started hearing from people in the WTD Slack #ai channel that they were experimenting with front-matter metadata to guide agents' doc writing processes. I'm hearing more and more good feedback from that approach, so I'm gonna start focusing on what I'm calling 'docs ops' metadata in my topics.



