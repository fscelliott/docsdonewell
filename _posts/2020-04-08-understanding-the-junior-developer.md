---
layout: single
title: Understanding the junior developer
date: '2020-04-08T09:55:00.001-08:00'
author: frances
tags:
- techcomm
- api
modified_time: '2020-04-08T13:13:14.240-08:00'
 
---




So first off a personal update -- last year, I got laid off the day I returned from maternity leave! Within a half hour of returning to my desk! Whew boy! It was a blessing in disguise in some ways, because 1) I'd been thinking for some time I could be more effective in a consulting role and 2) as part of my severance package, I got to attend a General Assembly coding bootcamp.

I ended up auditing the bootcamp because wow, it demands a ton of sacrifice with the end goal of getting a developer job. In contrast, I am happy to do a bit of scripting on the side, work with developers, and improve their experiences. Nonetheless, I worked through all the lectures, did a few homework assignments, and got a lot out of it. Not the least of which is that I validated my existing coding skills, gained deeper insight into the "junior developer" persona, and reaffirmed my conviction that tailoring your developer experience and docs to junior developers is a **Good Thing**.

There are a couple of big takeaways I'd like to share:

### Everyone is a junior developer

Well, no, not actually ... but every developer has to learn new concepts.  And yes, of course, as you gain experience as a developer, "totally new" concepts get rarer and rarer. Still, there's a lot of learning:

Some developers must learn a breakneck pace (think of all the Javascript frameworks coming out all the time! Those front-end folks have to sprint just to stay in place). Others face big disruptions to their coding world only occasionally (your Enterprise Java programmer with a 20 year career in monolithic app development who now lives in a brave new world of microservices, CI/CD, devops, oh my!)

I felt I experienced this disruption myself as part of the coding bootcamp. Up till then, my background was in writing Python scripts, and in documenting big Java applications in a analytics microservices context. I knew about RedHat, Docker, Kubernetes, Spark, Lucene, Cassandra, etc.

Now, I was learning about a whole new world: the ecosystems, the mindset, the business of ....  JavaScript.  Like probably many people outside the JavaScript world, I was fooled by the "script" part of the name -- especially since I'd only used JavaScript myself to write macros in an XML docs tool.  Now I realize it's [epic battle](https://www.javaworld.com/article/2886368/java-vs-nodejs-an-epic-battle-for-developer-mindshare.html) between Java and JavaScript. And while I haven't fallen in love (Python, you still have my heart), I had lots of "oh, that's neat!" moments. I also recognized that my learning curve was not dissimilar to that of experienced -- but JavaScript-naïve -- developers. 

Which brings me to my main point:

### We should all design for the junior developer

 Creating experiences with a junior developer in mind forces you to discard your comfy assumption that everyone's drunk your product Kool-aid. If you assume you're writing for someone who's technically savvy and can learn quickly, but who knows nothing about your world, you're positioning yourself to vastly decrease your developer onboarding friction. And if you assume that your "junior developer" is super impatient because they have, like, 10 other things on the docket to learn about, then you'll learn to answer up front the question: "why should I care? Why should I do this work?" 

It's a fine line to tread, assuming not too much about technical knowledge, but also not coming across as condescending or silly (like, at the level of "open a terminal by taking the following steps..."). Still, I think it's actually quite achievable. For example, it's quite low effort to provide high-level context for coding instructions. Even something as simple as "Clone this repository and open a terminal at the local directory location" is a direction that often gets left out in GitHub readmes...but it really shouldn't be left out.  And it never hurts to link to frameworks' getting started guides, even if you don't want to provide the details yourself. At the very least, no one is likely to roll their eyes at it, and it helps your reader understand what level of granularity your instructions will provide. 

When I look for inspiration, I think the [React newbie tutorials](https://reactjs.org/tutorial/tutorial.html) do an outstanding job of introducing junior developers to React, helping them understand why they should care, and explicitly stating their audience. I also really love (who doesn't) the [Stripe developer onboarding](https://dashboard.stripe.com/register ) experience.  

Ultimately, I think I came away from the coding bootcamp more confident that I *am* a junior developer. And while I'd never make the classic UX mistake of thinking I am the user, still -- my confusions, my pain points in learning about a product-- these are things that other developers likely share.

### Postscript: Fun with Javascript!

I'll end on another personal note. The coding bootcamp turned out to be quite serendipitous, because I took on contracting work that immediately benefited from my new knowledge. I'd just learned about Express, and now here I was, entering a pull request to change the authentication method for an Express server. I'd just learned about React, and now here I was, wading into a web UI to change some text. It's always nice when you can put what you've learned to immediate use. 









