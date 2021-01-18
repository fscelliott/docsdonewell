---
layout: single
title: Lookback on DX Onboarding teardown
date: '2020-12-16T09:55:00.001-08:00'
author: frances
modified_time: '2020-12-16T13:13:14.240-08:00'


---

When I take on a new client, I like to take advantage of my fresh eyes to walk through the onboarding steps a developer takes to get to Hello World and/or first meaningful call.  I also like to walkthrough an initial impression of the docs.


I did the same when I took Optimizely on as a client back in March 2020. (Hello - I started just as covid-19 hit the USA! I still remember a coworker in San Francisco cancelling an afternoon meeting because "we're about to go into lockdown." It got real, real fast.)

As we wrap up 2020, (whew, whom amongst us is not glad to see its tail end?) I'd like to look back at my teardowns as a measure of my impact on the dev docs. 

Here are the teardowns:

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQOG4mNWEJE-SiDPcxYJzK1SRhte8RaOnF8d_ZuxHH6da0JGCyE9AyrkzG04qtOWEsoQDi6QWCeSxHd/embed?start=false&loop=false&delayms=5000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vT0yeU_IJPUrYDH0BVVpQZYrCaK791BIjaNe5eZz-HQf4cddy7Oq_nuwPJjq_QldIwEINrd3TndGCJU/embed?start=false&loop=false&delayms=5000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


So, what did I get done from the challenges I uncovered in these teardowns? 

Plenty! Some stuff was outside of my control; some stuff got reprioritized with shifting business goals, but here are some highlights:

### Welcome page
The welcome page was a wall 'o text. I added an [architectural diagram](https://docs.developers.optimizely.com/full-stack/docs/welcome) I took from marketing, and authored my own, more technical diagram to add to our [implementation checklist](https://docs.developers.optimizely.com/full-stack/docs/implementation-checklist).

### Too much detail, too soon
The docs dived too early into detailed technical explanations, mixed with introductory how-to topics. I improved the progressive disclosure of the docs by exiling a lot of those long explanations into a "concepts" section (after winnowing out unnecessary explanations), and added warnings when the topics were [advanced](https://docs.developers.optimizely.com/full-stack/docs/how-bucketing-works).

I noticed that while the ranking of most popular pages stayed unchanged (which makes sense, since they *are* important), some of the very-visited but too-advanced conceptual pages decreased their rank after my efforts..which was exactly what I was going for!

![image](/assets/images/optim-metrics.png)


### Too many dev resource links in Optimizely's global nav
This one required me to put on my cross-team hat and talk to marketing. Ultimately I removed a page that was quite prominent -- optimizely.com/developer-docs -- which overlapped with another page, /developers, and which didn't really contain docs -- just links to docs!  Ultimizely it 'smelled' like a marketing page, and Adam Duvander [points out](https://everydeveloper.com/evaluate-documentation-like-a-developer/), developers will quickly abandon such a page. Down it went, in favor of a direct link to the docs!   


### Non-onboarding improvements to the user journey

But as usual, the biggest improvements for the docs turned out to be things that only came from months of being embedded and discovering needs through conversations. For example, since we were pivoting to a developer audience, I upped the emphasis on code by writing:
- code implementation sections in all the major how-to articles
- *working* code examples in key quickstarts
- a quickstart code example that could actually be run in codepen without an SDK install 

There were lots of other docs improvments, but I'm most proud of aiding in a domain-model overhaul of the SDKs and online app; since I made an effort to get in on design conversations early in the process, I was able to reconcile some inconsistencies between the app vs SDK, and advocate for the developer persona to change some API signatures I saw as less than ideal. Ultimately the info architecture of the docs got a total overhaul in a 100+ hr effort. In this messy visual, I highlight how much the info architecture changed:
![image](/assets/images/optim-before-after.png)








