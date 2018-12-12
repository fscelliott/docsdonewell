---
layout: single
title: From zero to editing an android app in 4 hours
date: '2015-02-09T07:01:00.000-08:00'
author: frances
tags: 
modified_time: '2015-06-08T10:29:32.478-07:00'



---

Whoohoo! I spent a fun afternoon...learning how to edit an Android app! 

 It all started when a coworker mentioned how nice it'd be if we had a mobile 
app to display our internal techcomm conference schedule. I remembered someone 
who'd left had developed such an app in 2011, and thought, "I know nothing 
about Android app development. Sounds like a fun excuse to learn something!" 

And 4 hours later, I'd figured out how to get the original app developer's 
source code, edit it, build it, and install the revised app it on my phone. 
Yay! 

<a name='more'></a> 

It's fun looking back on my googling thought process, going from absolute zero 
knowledge of Android app development: 


1. what the heck's an .apk file? 
1. how do I get the source code from the .apk file? 
('decompile...unpackage...what's the term?') 
1. ok, I nominally have some source code now from 
http://www.decompileandroid.com/. 
1. ...but is that source code valid? Guess I'll try to install a development 
environment, import the code, and see if it builds to find out. 
1. OK, I got Android Studio up and running after the usual Java SDK version 
headache....but it looks like this source code doesn't jive at all with their 
expected project directory structure and file extensions.  
(http://developer.android.com/training/basics/firstapp/index.html ) 
1. Could this app have been developed in Eclipse? No, I don't think so... 
1. Floundering 
1. All right, let's back up. This app is nothing but a bunch of HTML pages. So 
let's google "How to make an HTML android app" 
1. Oh! Phonegap! I recognize that name from the source code. This app musta 
been developed with Phonegap. 
1. OK, let's download Phonegap and see if we can import and build the source 
code 
1. Hmmrphh, I'm getting sick of all these installs...is there anything easier? 
1. Holey moley!  According to this blog I can build PhoneGap apps online: 
http://www.tricedesigns.com/2013/05/16/phonegap-android-studio/ 
1. OK...let's make some changes to the source HTML files, upload them to Adobe 
PhoneGap Builder (https://build.phonegap.com), put the resulting .apk file on 
my phone and.... 
1. YAY! My changes show up in the updated app! 
The upshot is, I still don't know anything about the Android SDK, but I 
definitely feel I've honed my coding information-hunting skills. 

Here's a screenshot of one of the templates I created, so that future 
colleagues can easily rev the app on a yearly basis and fill in conference 
information for that year:

![phone app](/assets/images/phone_app_2.png)