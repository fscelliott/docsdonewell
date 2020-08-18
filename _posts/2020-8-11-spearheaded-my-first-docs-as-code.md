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

In case you're not familiar with docs as code, here are some of the salient points I considered before setting this up:


Pros: 

- familiar pull request & merge process for the engineering team
- docs live closer to code
- tech writer & engineers can more easily collaborate
- access to build checking tools through travis, etc, for example, for broken links

Cons:

- can be fragile (my client previously has a deprecated, custom "docs as code" site that often broke, and the people who built it left, so no one wanted to touch it)
- often lose some of the advanced tech comm authoring tools & requirements
- If you're not working in a microservices code base, your docs publishing toolchain might be part of a bloated build process


The full story is that my current client uses [ReadMe](https://readme.com/) to publish their docs. ReadMe has many nice features, but their WYSIWYG online markdown editor has made the same tradeoffs between contributor ease versus administrative power that many wikis have made. In other words, community contribution is easy, but administrative capabilities for writers, like finding and replacing across pages are...lacking, in many cases. As Anne Gentle at [Just Write Click](https://justwriteclick.com/) once put it in a conversation with me, it "makes the easier things easier, and the harder things harder." It boiled down to this: since the client has 9 SDKs, it's getting harder and harder to maintain the growing docs if we can't find and replace across duplicate content.

I found that for my own purposes, I could often get admin tasks done quickly by using a Node-based, [open-source readme-sync tool](https://github.com/flowcommerce/readme-sync/) tool for roundtripping GitHub markdown to ReadMe. The tool uses ReadMe's API to sync markdown to the ReadMe published platform. It was worth it for one-off, large-scale change management of the docs, but it was a pain, because I had to export the files from ReadMe, then manipulate the directories and filenames from the ReadMe export in order to the tool to work.

So, with the engineering manager's support, I decided to try to adapt the readme-sync tool for a more DevOps approach that engineers could also use. My challenge was to adapt the tool for our use case, including integrating it into a Travis build so that the tool would automatically kick off a sync every time someone committed a change to the GitHub markdown docs.

At first, I thought up a complicated Travis build that would accommodate our 9 SDKs, and with the help of a friendly DevOps engineer, we got it done. However, we then realized that adopting the tool for all 9 SDKs would be overwhelming, given that I'd discovered some minor limitations and authoring annoyances that could be cleaned up in further iterations. I was new to Travis, but largely on my own, I was able to retool Travis to sync just our docs for the microservice deployment of the SDK, as a pilot project. I got an engineering contractors' help in migrating the docs from ReadMe-flavored to Github-flavored markdown, got the tool up and running with some testing, and presented at an engineering Community of Practice meeting.

Now, I'll be policing the developers (ah-hem! that is, "conducting change management") to ensure they adopt the new toolchain. Next time we have a hack week, I'd also like to work on improvements to the tool (like: previewing docs changes in a staging environment, automatically updating the "modify date" on articles, handling image links and relative links more smoothly, etc). I'm excited to see where it will all head!
