---
layout: single
title: AI tools for writing developer documentation
date: '2022-01-18T00:00:00.000Z'
author: frances
modified_time: '2023-03-09T00:00:00.000Z'

---

Recently I investigated a few AI-powered tools for writing developer documentation. Of course, part of my investigation was prompted by existential ~~dread~~ curiosity -- will AI replace documentarians?  My initial answer is no; we still need humans to write high-quality developer docs, but tools like GPT will absolutely change how we write. And I think that's a good thing! I'm encouraged by early research on AI's transformative role, such as those that found that ["separate studies of both writers and programmers find 50% increases in productivity with AI, and higher performance and satisfaction"](https://twitter.com/emollick/status/1631397931604488194).

Anyway, two tools that I recently investigated are:

- **Copilot labs** (powered by Codex, branched from GPT). I've see encouraging chatter about Copilot's ability to generate code from prompts among engineers on Slack, so I thought I'd try out it's "Explain code" capabilities. After all, a large part of my job is reading and explaining code! Could Copilot help me or do it better than me?
- **Theneo** -- a new developer portal tool that says it uses AI to generate Stripe-like docs.
- an old favorite (TODO) -- errata.ai

Let's dive in!



Copilot review 
----

**Getting access**

There were a couple of things here: 

- I didn't realize that the "explain" feature is part of Copilot *Labs* not Copilot itself.  I signed up for Copilot, then installed *both* in VS Code from the Visual Studio marketplace, and made sure that I'd authorized Github in VS Code  by previously installing the [GitHub Pull Requests and Issues](https://code.visualstudio.com/docs/sourcecontrol/github) extension.

- I also didn't want to expose any code from private codebases. So in the interest of security, in Github I (regretfully) removed any of the sharing/suggestion features for Copilot: 

  ![copilot settings](/assets/images/copilot_1.png)

**Experience**

**Bottom line**



Theneo review
---

**Getting access**



**Experience**

at a quick glance, some thoughts (as in 'would I personally use this for my clients'?):

1. when they said 'stripe like docs' I thought they were promising the "three panel" format stripe offers with full code samples (like this: https://stripe.com/docs/checkout/quickstart) but I was disappointed that doesn't seem the case
2. ok so historically, tech writers have been burned by vendor-lockin with crappy "techcomm tools". Personally that makes me very wary of anything that won't let me control/sync my content directly in GitHub as well as whatever interface the tool offers. (ie tool must play well with 'docs as code'). I can't tell how much Theneo supports this -- they have no docs, and CI deployment tab isn't enabled so I can't go play
3. not super impressed with the auto-generated descriptions. I'd still need a thinking human writing the docs, and I can't tell how smart the assistant is -- would it auto-generate reuse strategies for all params with the same description for example?

​        -> it does get me thinking that there are plenty of AI-automatable tasks potentially to be done here with human review, but I'm not sure that theneo has identified those most valuable areas.

1. bottom line, personally, I wouldn't use it until I was sure of the docs-as-code capabilities and until I saw some robust documentation abt theneo.





