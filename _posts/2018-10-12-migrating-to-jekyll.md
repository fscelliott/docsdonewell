---
layout: single
title: Migrated my site to Jekyll
date: '2018-10-12T09:55:00.001-08:00'
author: frances
tags:
- technical learning
modified_time: '2018-10-12T09:55:00.001-08:00'


---



I finally, finally, completed a task that's long been on my backburner: migrating my site to Jekyll! 

I've been interested in Jekyll for quite a while. For example, see [Wait, there are alternatives to DITA for small companies?](https://www.franceselliott.com/2015/03/24/wait-there-are-alternatives-to-dita-for.html)

Here's how I did it, for my own future reference:

This tutorial was very helpful to me as a jumping off point: [Building a static website with Jekyll and GitHub Pages](https://programminghistorian.org/en/lessons/building-static-sites-with-jekyll-github-pages)

Next,  I went with the minimal mistakes theme because it seems widely used and has nice [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/). I chose to use the theme remotely -- we'll see how that plays out in terms of updates.

 Some future wishes for the site:

- Integrate Travis CI so I can easily view build errors (my initial quick effort failed, I think it's because I build on a Windows machine as specified by my gemfile, but Travis builds in Linux.)
- Integrate html-proofer at some point to make sure that website never has broken links or images