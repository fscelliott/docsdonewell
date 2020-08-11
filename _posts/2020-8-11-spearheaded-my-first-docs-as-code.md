---
layout: single
title: Spearheaded my first docs as code
date: '2020-08-11T09:55:00.001-08:00'
author: frances
tags:
- docs-as-code
modified_time: '2020-08-11T13:13:14.240-08:00'
 
---

I can finally say that I've led a [docs as code](https://www.writethedocs.org/guide/docs-as-code/) initiative! It took buy-in from the engineering manager, technical elbow-grease, and a helpful DevOps lead, but after a 3-months effort, I've got the infrastructure in place and the developers educated. Now we'll see what fruit my efforts bear.

The full story is that my current client uses ReadMe to publish their docs. ReadMe has many nice features, but their WYSIWYG online markdown editor has made the same tradeoffs between contributor ease versus administrative power that many wikis have made. Administrative capabilities for writers, like finding and replacing across pages are...lacking, in many cases. As Anne Gentle at [Just Write Click](https://justwriteclick.com/) once put it in a conversation with me, it "makes the easier things easier, and the harder things harder." It boiled down to this: since the client has 9 SDKs, it's getting harder and harder to maintain the growing docs if we can't find and replace across duplicate content. 

So, with the engineering manager's support, I decided to try to adapt an [open-source tool](https://github.com/flowcommerce/readme-sync/) I found for syncing GitHub Markdown to ReadMe. The tool, readme-sync, uses ReadMe's API to sync markdown to the ReadMe published platform. My challenge was to adapt the tool for our use case, including integrating it into a Travis build so that the tool would automatically kick off a sync every time someone committed a change to the GitHub markdown docs.

At first, I thought up a complicated Travis build that would accomodate our 9 SDKs, and with the help of a friendly DevOps engineer, we got it done. However, we then realized that adopting the tool for all 9 SDKs would be overwhelming, given that I'd discovered some minor limitations and authoring annoyances that could be cleaned up in further iterations. I was new to Travis, but largely on my own, I was able to retool Travis to sync just our docs for the microservice deployment of the SDK, as a pilot project. I got an engineering contractors' help in migrating the docs from ReadMe flavor to Github flavored Markdown, got the tool up and running with some testing, and presented at an engineering Community of Practice meeting. Now, I'll be policing (ah-hem! "conducting change management") the developers to ensure tool adoption. Next time we have a hack week, I'd also like to work on improvements to the tool (like: previewing docs changes in a staging environment, automatically updating the 'modify date' on articles, handling image links and relative links more smoothly, etc). I'm excited to see where it will all head! 
