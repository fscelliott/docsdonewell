---
layout: single
title: Video walkthrough - AI-assisted developer advocate blogging
date: '2025-05-20T00:00:00.000-08:00'
author: frances

modified_time: '2025-05-20T00:00:00.000-08:00'
---

Here's a short video tour of how I've configured Claude with style guides and a knowledge base to automate some of my more formulaic developer advocate tutorials for my client [Sensible](https://www.sensible.so/). It's quite off-the-cuff and informal, so don't go looking for production polish in this one!


<iframe width="560" height="315" src="https://www.youtube.com/embed/5I0nG5c2Bc0?vq=720" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<!--<iframe width="560" height="315" src="https://www.youtube.com/embed/X0vXnEuP-aU?si=oA7oas3Tzw-e0ZOG&hd=1" title="Quick walkthrough Claude project" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>-->



Here's a recent example of a blog post published using this setup:

[How to extract data from CMS 1500 forms with Sensible](https://www.sensible.so/blog/how-to-extract-data-from-cms-1500-forms-with-sensible)

And for comparison's sake, here's an example of a similar blog post I wrote without AI assistance:

[How to extract from rent rolls with LLMs and Sensible](https://www.sensible.so/blog/how-to-extract-data-from-rent-rolls-with-llms-and-sensible)


I should note that even with a fairly successful prompt like this one, there's still a substantial editorial process. For example, for this blog post, I made the following manual edits:

- Corrected some inaccurately generated inline code comments (code hallucination is still a thing even with a prebuilt example config!)
- Added lots of inline comments to the code examples
- Corrected a misstatement about the purpose of a feature ('fingerprints are for classifying document types!' Well, no, they're for classifying document *subtypes*)
- Inserted a bunch of screenshots
- Added in a bunch of prerequisite setup steps that Claude missed, even though those steps were in the prompt context (sign up for an account; clone cms-1500 support to your account)
- Slimmed down verbose fluff and nixed some marketing hyperbole ('this is the perfect method for...')
- Modified the example PDF to provide a better example for a complex feature (the sections method)
- Rewrote a heavily hallucinated conclusion ('signup for a free account for $100/month!')


Even with this editorial process, Claude still roughly halved the time I'd normally spend on a post like this. I expect it to save me even more time in the future, since I spent a lot of that time on reusable Claude project configuration.

<!-- test loom
<iframe width="560" height="315" src="https://www.youtube.com/embed/Z-RBcErFeoc?si=HkXuGbPzBvZGkVVS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe> -->

<!-- higher quality smaller screen OBS

<iframe width="560" height="315" src="https://www.youtube.com/embed/VysEwKkgw20?si=_OISSAGDb-rRyl4Z" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe> -->
