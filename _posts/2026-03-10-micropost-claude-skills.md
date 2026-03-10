---
title: Micropost on building AI doc toolchains with Claude skills
---

I've been building out some powerful AI-assisted docs toolchain infrastructure recently. Some random observations:

- Claude's plugins are amazing! Especially the official `/skill-creator` and `/code-simplifier` plugins. I need to check out superpowers next.
- You know how the term "task switching" is in our workplace lexicon? I want to add "pace switching" too. It's the feeling of working with AI on something blazingly fast, and then abruptly slowing down to carefully check and correct its work. It's like stumbling off a moving walkway sometimes.
- LLM coding agents are SUCH a loss leader right now -- like a $200/month subscription could use up to $2,000 in compute. Designing my AI toolchains to minimize token use seems pretty critical, and I'm already finding ways I can steer LLMs in that direction. Like, hey, agent, go use the `llms.txt` to search the docs, and then fetch the MD raw files. Don't just use our sensible-docs MCP server for docs search!
