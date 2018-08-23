---
layout: single
title: Specifications as a taxonomy of product features
date: '2015-04-09T06:55:00.001-07:00'
author: frances
tags: 
modified_time: '2015-05-20T07:37:16.477-07:00'
blogger_id: tag:blogger.com,1999:blog-2779361939324367100.post-135870255598584184
blogger_orig_url: http://elliottworklife.blogspot.com/2015/04/specifications-as-taxonomy-of-product.html
---

I've been working hard  recently to gather specs for a new hardware product 
I'm documenting. Combing through competitor docs to compare organization, 
hierarchy, and wording gave me lots of fodder for my [Excel-based 
taxonomy](https://www.blogger.com/blogger.g?blogID=2779361939324367100#editor/target=post;postID=7747089384162209679;onPublishedMenu=allposts;onClosedMenu=allposts;postNum=5;src=postname), 
increased my conceptual understanding, and springboarded my first draft for a 
hardware help table of contents. 

When I think about it, a specs doc is really a beautiful thing. It tries to 
encapsulate a body of knowledge about a device and its industry in an 
organized and concise fashion. In some ways it directly mirrors portions of my 
taxonomy--just reformatted. And in fact, when [Schema.org 
2.0](http://blog.schema.org/) recently released, I browsed around the release, 
and my ideas about the similarities of taxonomies and specifications were 
reinforced. For example, check out the [automotive 
ontology](http://sdo-property-value-and-cars.appspot.com/Vehicle) proposed 
extension to Schema.org -- all those properties of vehicles look a lot like 
(both internal and external) specifications categories to me! 




Since I'm currently implementing my taxonomy in DITA as a means of vocabulary 
control and consistency, I have to consider how to source the specs and share 
them with other parts of the help. Increasingly I'm coming to the opinion that 
in in single-sourced documentation, specs should be used as the single source 
of truth. Well, actually, I have a more complicated opinion than that. 
Certainly in terms of actual numbers, it's the single source of truth, i.e. in 
DITA speak, it's the source for all conrefs. But for more 'functional' or 
'definition-like' specs who act more like a controlled vocabulary and whose 
impact ripples through the entire help, perhaps the source of truth should be 
just that--a controlled vocabulary in the form of a keydefs definitions 
document or 'library of conrefs.' Time will tell if my strategy works! 