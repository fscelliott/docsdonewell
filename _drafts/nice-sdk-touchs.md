---
layout: single
title: Nice SDK touches
date: '2020-12-04T09:55:00.001-08:00'
author: frances
tags:
- dx
modified_time: '2020-12-04T13:13:14.240-08:00'


---

In the course of writing dev docs for a collection of an SDK in 9 languages (and one REST API) over the last few months, I've gotten to see (and contribute to)  a domain-model overhaul, and also witnessed smaller incremental improvements.
[Lorna Jane's recent blog post](https://lornajane.net/posts/2020/making-sdks-a-value-added-experience) helped me clarify some of the ways in which the SDKs I work with measure up in terms of DX:

### JWT helper functions

(TO DO: add some stuff here..shew as talking about generating and sending the JWT with the call which I didn't QUITE understand...I need an example...)

### Helpers

Something I've noticed is that in our static languages (Java, Swift, etc), we add defined data structures so you can quickly get JSON representations is a nice perk. Actually, it didn't occur to me that you'd write an SDK in a static language WITHOUT providing such data strucutres, but of course.. you could.. and your developers would scowl.

What do I mean? Say your SDK makes 'decisions' and you want to represent them as JSON:
"decision_made": "yes",
"date_decision_made": "2020-12-04T09:55:00.001-08:00",
"decision_outcome": "yes-to-the-dress"

In a dynamic language like python, you could just gobble up the JSON.
In a static langauge, you need to define the type of each JSON field.



### Save repetition

Lorna Jane talks about baking often-repeated tasks into your API. The flip side of that is avoiding repeated calls (or passing repeated parameters) if you can. We used to pass a userID to Each. And. Every. One of our SDK calls. With our domain model overhaul, now you set the user context once, then make one key call against it, and the rest of what you need, you can get from whatever that call returned. 

### Consistent vs idiomatic ???


