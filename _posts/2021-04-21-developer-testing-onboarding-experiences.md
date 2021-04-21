---
layout: single
title: Developer testing some onboarding experiences
date: '2021-04-21T10:23:00.001-08:00'
author: frances
modified_time: '2021-04-21T10:23:00.001-08:00'

---


Recently while redesigning several developer onboarding tutorials, I was reminded just how key user testing is for developer experience -- and how liberating it is to remember I don't *have* to have all the answers about my user's minds. The power of observation beats wishful thinking about 'mind reading' any day! 

For background, my client recently overhauled both  their SDK and their web admin UI. I spent months on redesigning and rewriting the developer docs, and then it was finally time to work on the in-app onboarding tutorial and the docs quickstarts. 

The quickstarts underwent a fairly interesting (to me, at least) evolution.  When I consulted with the product manager, the UX designer, and our devrel folks, it seemed logical to rewrite the quickstart to reflect our app's new domain model. So my first draft had a table of contents that introduced concepts roughly according to:

1. Their place in the domain model hierarchy (starting with the base concept).
2.  Their order of importance in terms of what we were selling (i.e., first explain the feature we most want to sell).

And building on a previous tutorial, the quickstart was a mix of code snippets and UI instructions -- it didn't result in a functional demo app. It looked something like this: 


Then I went to user test, and oh boy -- my quickstart quickly turned upside down! In the end, I had something totally different:

1. Instead of progressive disclosure of concepts, I gave users a quick, working demo app to copy up front, then afterwards explained what was going on.
2. Instead of introducing our hoped-for sales feature first, I introduced the *easiest* feature first...because otherwise the users got stuck.

I was particularly pleased to watch one developer during user testing, who didn't both to run my sample app at all, but fully understood the quickstart's main points just from reading the code and looking at the sample command-line output I'd provided. 

I also formed some opinions on sample apps:

- They should start from a totally blank project. This gives the user confidence that there's no "hidden config magic" (to quote a tester) that will break when they try to integrate samples into their application.
- They should be well commented (obviously). 
- They should include some error logging, and if the SDK's native error messages aren't great, then manually include some error condition checking and nicer messages for common mistakes. (and let the SDK team know about DX improvements they could make).
- They should be as simple as possible. My sample app was purely a command-line toy that clearly signaled when it was faking SDK functionality (such as tracking user events), but it showed the most important calls in the SDKs and let the user see some metrics in the admin dashboard quickly.





I'd be curious to know what your opinions are on how lightweight or simple quickstart sample apps should be! 


<!--optim_quickstart_before_user_testing.png-->
<!--optim_quickstart_during_user_testing.png-->
<!--optim_quickstart_after_user_testing.png-->



