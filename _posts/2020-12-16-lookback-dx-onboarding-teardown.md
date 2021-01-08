---
layout: single
title: Lookback on DX Onboarding teardown
date: '2020-12-16T09:55:00.001-08:00'
author: frances
modified_time: '2020-12-16T13:13:14.240-08:00'


---

When I take on a new client, I like to take advantage of my fresh eyes to walk through the onboarding steps a developer takes to get to Hello World and/or first meaningful call.  I also like to walkthrough an initial impression of the docs.


I did the same when I took Optimizely on as a client back in March 2020. (Hello - I started just as covid-19 hit the USA! I still remember a coworker in San Francisco cancelling an afternoon meeting because "we're about to go into lockdown." It got real, real fast.)

As we wrap up 2020 (whew, whom amongst us is not glad to see its tail end?), I'd like to look back at my teardowns as a measure of my impact on the dev docs. 

Here are the teardowns:

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQOG4mNWEJE-SiDPcxYJzK1SRhte8RaOnF8d_ZuxHH6da0JGCyE9AyrkzG04qtOWEsoQDi6QWCeSxHd/embed?start=false&loop=false&delayms=5000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vT0yeU_IJPUrYDH0BVVpQZYrCaK791BIjaNe5eZz-HQf4cddy7Oq_nuwPJjq_QldIwEINrd3TndGCJU/embed?start=false&loop=false&delayms=5000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


So, what did I get done from the challenges I uncovered in these teardowns? 

Plenty! Some stuff was outside of my control; some stuff got reprioritized with shifting business goals, but here are some highlights:

### Welcome page
The welcome page was a wall 'o text. I added an [architectural diagram](https://docs.developers.optimizely.com/full-stack/docs/welcome) I took from marketing, and authored my own, more technial diagram to add to our implementation checklist.
![image](/assets/images/optim_diagram.png)

### Too much detail, too soon
The docs dived too early into detailed technical explanations, mixed with introductory how-to topics. I improved the progressive disclosure of the docs by exiling a lot of those long explanations into a "concepts" section (after winnowing out unnecessary explanations), and added warnings when the topics were advanced:
![image](/assets/images/progressive_disclosure.png)


### Too many dev resource links in Optimizely's global nav
This one required me to put on my cross-team hat and talk to marketing. Ultimately I removed a page that was quite prominent -- optimizely.com\developer-docs -- which overlapped with another page, \developers, and which didn't really contain docs -- just links to docs!   

### Non-onboarding improvments to the user journey

But as usual, the biggest improvements for the docs turned out to be things that only came from months of being embedded and discovering needs through conversations. Stuff like: 


- Added an SDK compatibility matrix, since the SDK versioning had recently been decoupled across languages, leading to potential confusion without a single source of truth
- Since we were pivoting to a developer audience, I upped the emphasis on code with:
   - code implementation sections in all the major how-to articles
   - *working* code examples in key quickstarts
   - writing a quickstart code example that could actually be run in codepen without an SDK install 
   - implemented docs as code for Microservice/Rest API docs
   - totally reorganized topics + overhauling SDK references for new domain model encompassing UI/UX overhaul and SDK overhaul (lisit hrs here?) 

The table of contents got completely revamped -- here I highlight some of the sections that were completely changed:
![image](/assets/images/optim-before-after.png)

What impact did all this have? Well, I'd say it's acknowledged that it can be hard to bring analytics to docs, but I got good feedback on the changes! And in terms of metrics, 
my efforts were certainly guided by some basic page view rankings. Naturally, I priortized my efforts on the most popular pages. And I noticed that while the ranking of most popular pages stayed unchanged (which makes sense, since they are important), some of the very-visited but too-advanced conceptual pages decreased their rank after my efforts..which was exactly what I was going for!



![image](/assets/images/optim-metrics.png)








