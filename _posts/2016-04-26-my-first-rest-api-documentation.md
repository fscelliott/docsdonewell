---
layout: single
title: My first REST API documentation
date: '2016-04-26T07:52:00.000-07:00'
author: frances
tags: 
modified_time: '2016-04-26T07:52:36.274-07:00'


---

I've documented low-level hardware APIs, but never REST APIs -- I learned a ton working in Swagger for a Watson service API. Looking back, it breaks down into two parts:

Learning about REST APIs
Llearning about the Watson service.

## **Learning about REST APIs:**

**doc tutorials**
For an introduction to fundamental API concepts and terminology, I found **Tom Johnson's [tutorial on documenting APIs](http://idratherbewriting.com/docapis_course_overview/) ** invaluable-- he even had a [post](http://idratherbewriting.com/pubapis_swagger/) on Swagger specifically! (Tom's a prominent blogger in tech communications; in fact, I read his blog really intensively about 5 years ago when I decided to go into tech writing!)  He helped me talk intelligently about endpoints, resources, query strings, etc.

**building swaggger**
Getting a **local swagger build** up and running was a task and a half due to the build structure (which has since been simplified, thankfully!). I leaned heavily on colleagues, but I was eventually able to get the build running on my Linux virtual machine -- though not, strangely, on my local Windows machine.  I must have spent _days_ on this, yikes! But I wrote or updated 3 process docs on the subject, so hopefully the next person will have less pain.

**modifying source code**
Adding annotations into the source java files using @API annotations was not too difficult. But I ran into some bugs, and for the first time, [posted and got answers about bugs on a developer forum](https://groups.google.com/forum/?fromgroups#!topic/swagger-swaggersocket/Xq7jCJS7WRc).

**REST fundamentals**
Learning to play around with the API forced me to learn some REST fundamentals too--when can I enter something in a parameter, versus typing a query string in the request URL? What syntax to use to  get parameter fields into the URL query strings? How can I discover whether parameter field takes JSON or some other syntax? (answer--I think--is that there's not discoverable method; that's why you need the docs!) 

## **Learning about the Watson service**

My understanding of the resources I'm interacting with evolved quite substantially, though examining the source files for schemas and instance data, playing with the API, and most importantly, talking to the developers. I won't go into the details since the service isn't public yet, but I learned a great deal about type systems and entity/relationship modeling schemas. 