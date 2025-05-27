---
layout: single
title: Video walkthrough: AI-assisted developer advocate blogging
date: '2025-05-20T00:00:00.000-08:00'
author: frances

modified_time: '2025-05-20T00:00:00.000-08:00'
---

Here's a short video tour of how I've configured Claude with style guides and a knowledge base to automate some of my more formulaic developer advocate tutorials. This setup is aimed to help my client [Sensible](https://sensible-website.webflow.io/) meet a goal of publishing six AI-assisted blog posts this quarter.


<iframe width="560" height="315" src="https://www.youtube.com/embed/5I0nG5c2Bc0?vq=720 frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Here's a recent example of a blog post published using this set up:

[How to extract data from CMS 1500 forms with Sensible](http://sensible.so/blog/how-to-extract-data-from-cms-1500-forms-with-sensible)


I should note that even with a fairly successful prompt like this one, there's still a substantial editorial process. For example, for this blog post, I made the following manual edits:

- Corrected some inaccurately generated inline code comments (code hallucination is still a thing even with a prebuilt example config!)
- Added lots of inline comments to the code examples
- Corrected a misstatement about the purpose of a feature ('fingerprints are for classifying document types!' well, no, they're for classifying document *subtypes*)
- Inserted a bunch of screenshots
- Added in a bunch of prerequiste setup steps that Claude missed even though those steps were in the prompt context (signup for an account; clone cms-1500 support to your account)
- Slimmed down verbose fluff and nixed some marketing hyperbole ('this is the perfect method for...')
- Modified the example PDF to provide a better example for a complex feature (sections)
- Rewrote a heavily hallucinated conclusion ('signup for a free account for $100/month!')