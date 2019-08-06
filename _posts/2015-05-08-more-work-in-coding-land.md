---
layout: single
title: More work in coding land
date: '2015-05-08T09:03:00.002-07:00'
author: frances
tags: 
modified_time: '2015-06-08T09:30:22.213-07:00'



---

A lot happening in work-land recently; hard to keep up with blogging! Some 
brief updates on the coding front: 


## I can call myself a help developer 
'Cause I wrote Python code to build our help system that actually made it into 
the product's driver build, yay! 

This was a really empowering moment for me, because it meant we got our help 
built when I wanted it built, rather being totally dependent on someone else's 
schedule. 

The background is, our help system is a mix of a really old tool chain and a 
really new tool chain--so new, that I'm one of the first people to work with 
both at once. 

Normally, we ask our software developers to integrate our help into the 
driver. But because we had a totally new scenario with our toolchains, I put 
some thought into the integration and realized--hey, might as well turn this 
analysis into code. I wrote up a script that worked on my local computer 
(pulled in help systems from both old and new toolchains, decompiled them, and 
recombined them, essentially), handed it off to a software developer, he made 
a few changes*... 

and BOOM! Our help system now builds in the driver! 

*don't want to minimize his work. It only looks like a few lines of changes, 
but for example, he spent 3 hours hunting down a suuuuuper old .exe that lived 
deep in our version control system! 


## Someone else is calling me a code architect!  
Even though I consider myself a hacker.
There's a couple other writers on my floor who also code, and one of them 
invited me to collaborate on a project recently.  It went great--he handled 
most of it, I handled all the file I/O portions, and we ended up with a tool 
that diffs CHMS using daisydiff as an engine. 

Which is a Game. Changer. for our department as far as I'm concerned. The lack 
of a reliable diff tool has been one of the biggest thorns in our collective 
sides for....for ever! (The fact that we're still working with CHMs is another 
thorn in our sides, but we're finally migrating to DITA, and I'm already 
scheming how to adapt this diff tool to DITA as well) We're super proud: 


![zauis diff tool ui](/assets/images/zauis_blurred.png)

and the output of the tool (a diffed CHM) looks like this:

 ![diffed chm](/assets/images/diffed_3.png)

Based on that successful collaboration, my coworker asked me and another 
writer to coauthor a more ambitious tool with a plugin architecture for tests 
that check compliance for our department's style guide and DITA checklists. 

And...he asked me to write out the skeleton code for the whole package, 
because I have the most Python experience of any of us. 


Yikes! I think of myself as a hacker, not an architect. 
But so far it's gone really well; we brainstormed the architecture together 
one day, then I wrote out the pseudocode, then I finally learned about some 
Python package best practices at [Structuring Your Project--The Hitchhiker's 
Guide to Python](http://docs.python-guide.org/en/latest/writing/structure/) , 
and now I have working code that runs 1 test successfully, and which is 
hopefully easy for the other writers to plug into. 

<!--Here's a snap shot of the 1st working code---all authored by me at this point, 
but soon to include others' contributions, hopefully! It's HEAVILY commented, 
because my cowriters are new to Python. Also I didn't exactly pay attention to 
commenting best practices; I'm a little embarrassed, but mostly proud: 

https://www.dropbox.com/sh/ftvfg2z733was5r/AABHjSz8GvV6H3eth1-7W0Wia?dl=0 -->