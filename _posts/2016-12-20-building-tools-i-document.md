---
layout: single
title: Building the tools I document
date: '2016-12-20T08:59:00.002-08:00'
author: frances
tags: 
modified_time: '2017-03-10T15:07:31.160-08:00'


---

I've come a long way as a self-taught developer. My software dev team is 
shorthanded at the moment, and the lead architect pinged me recently and said 
something along the lines of, "I know it's not in your job description, but 
you seem to pick up on stuff pretty quickly; want to make some deployment 
tools for us? If so, read up on ansible and the python jinja2 library." 

And guess what? I'm getting it done! He gave the specs for what the tool 
should do*, I worked independently for the most part, occasionally checking in 
to make sure I was interpreting his specs correctly, read up on ansible, 
kubernetes, a few python modules (jinja2, argparse, and configparser), learned 
a lot about linux (our deployment environment), a few features of yaml 
and...two weeks later I have a working script that is intended to be used 
by our devops team in production. The experience was such a contrast to my 
early Python days, when error messages were mysterious and frustrating. Now, I mostly have an instinct for what's wrong and can quickly debug. 

So at the moment, I don't have to ask, "when will the tool be ready to 
document, and what will it do?" Because I'm writing it. Which is a good thing, 
because the tool I'm coding will probably form about 30% of the documentation 
in the install/config guide I'm writing for our product. 




*In its current form, the tool takes some yaml specs for kubernetes 
deployments, injects some configuration values into them using jinja2 (such as 
dynamic IPs for kubernetes services), copies those deployment specs to remote 
hosts using ansible, and deploys them via kubernetes' kubectl command-line 
interface. 