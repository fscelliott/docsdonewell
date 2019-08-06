---
layout: single
title: End-to-end development of Swagger API docs, including Dockerization
date: '2017-06-16T07:39:00.001-07:00'
author: frances
tags: 
modified_time: '2018-01-03T08:01:18.544-08:00'


---

I've known how to edit API docs in swagger for about a year or so, but as a 
solo writer recently I took taught myself the end-to-end process. Since I 
don't know any other information developers who've done the process end-to-end at my company, I taught myself the technology and occasionally asked my devs for help.

Here's what I did, working on and off over the course of a few 
months: 

-researched pros and cons of swagger annotations in the java spec itself or in 
a separate spec file. Went with the latter, even though at first I felt this 
violated single source of truth principles. (the build process was so 
precarious and difficult for in-java annotations that it wasn't worth my time) 

-read the java code in order to author the yaml spec by hand. [API handyman](https://apihandyman.io/writing-openapi-swagger-specification-tutorial-part-1-introduction/) 
came to my rescue here. 

-Installed swagger-editor to get instant feedback on my edits. 

-Created a web app to publish my docs using Tomcat.  Made some use of a [popular tutorial](https://idratherbewriting.com/learnapidoc/pubapis_swagger.html).

-Got feedback that I actually needed to publish my docs using Websphere 
Liberty Profile instead of Tomcat.  Created a WLP web app using an [IBM tutorial](https://developer.ibm.com/wasdev/blog/2016/02/17/exposing-liberty-rest-apis-swagger/). 
In theory this would have been easy, but the most difficult part was finding 
the right version of WLP to install on Eclipse marketplace; the versioning 
conventions just seemed really confusing to me. 

-Got told I needed to put my web app in Docker. Fortunately, there were a 
couple other Dockerized web apps in our team I could use as an example, plus 
the [Docker intro videos](https://training.docker.com/introduction-to-docker) are really good. I successfully 
Dockerized my WLP app, and handed it off to a developer. 

YAY! 