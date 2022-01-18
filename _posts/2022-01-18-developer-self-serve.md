---
layout: single
title: Launching developer self-serve walkthroughs
date: '2022-01-18T00:00:00.000Z'
author: frances
modified_time: '2022-01-18T00:00:00.000Z'

---






Recently my client Sensible launched their developer self-serve experience. It’s exciting to be a part of it, because self-serve for enterprise-grade PDF data extraction is fairly groundbreaking (I know of no other startups out there doing it, in fact). 

My self-serve goal is to get users to their first meaningful data extraction in minutes. So, I’m debuting debuting a series of interactive walkthroughs that greet you in your dashboard when you sign up for a free [self-serve account](https://app.sensible.so/register/):

![image](/assets/images/sensi_walkthroughs.png)

This is a big improvement over our former empty dashboard, which linked to a longer [getting started guide](https://docs.sensible.so/docs/quickstart) I wrote.

Here’re some of the guiding principles I used to create these walkthroughs:

Interactive
====
A fun aspect of these walkthroughs is their inherent interactivity.  They’re formatted as PDFs, and their text is both the instructions, and the data to extract. You view them in the Sensible UI, and then you extract what you view. Meta, right?

![image](/assets/images/sensi_interactive.png)


Industry agnostic
====
I tried to keep the walkthrough fun and grounded in the real world, but since Sensible offers a cross-industry toolkit, I avoided focusing on any particular industry. So for example, when you learn about rows, you get to extract some food data from a table. I chose fresh fruit as a popular snack when I made up the data, though that’s probably wishful thinking about healthy eating habits!

![image](/assets/images/sensi_table.png)


I must have been hungry when I wrote these walkthroughs. To learn about checkbox extraction, you work with options from a bed and breakfast menu:

![image](/assets/images/sensi_checkbox.png)

Keep it short
====

I had a strict rule: keep each walkthrough to just one page. But I also wanted to showcase the breadth of extraction methods. That meant I had to show, not tell. So I carefully chose extraction steps that build in complexity, from rows to tables; from checkboxes to regions. There’s also an intentional misstep! (sometimes highlighting common errors is the quickest way to showcase concepts).  If you do get stuck there's a [cheat sheet](docs.sensible.com/cheat) with solutions and links to explanations.


Easy to start from scratch
===

While you can build on Sensible's [broad library](https://github.com/sensible-hq/sensible-configuration-library) of queries for common document forms, I want to empower you to quickly write queries from scratch for a brand-new form. So my walkthroughs guide you to modify existing queries, then challenge you with a blank slate. With your knowledge from previous walkthroughs, you might be surprised how easy it is to tackle a sales quote form you’ve never seen before and grab information like the document date and the grand total.

![image](/assets/images/sensi_scratch.png) 


Feedback welcome
====

These walkthroughs underwent many iterations before their present form, and now I look forward to user testing them. We welcome feedback -- submit your comments or suggestions to support@sensible.so. 


