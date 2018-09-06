---
layout: single
title: My first REST API documentation
date: '2016-04-26T07:52:00.000-07:00'
author: frances
tags: 
modified_time: '2016-04-26T07:52:36.274-07:00'


---

<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin: 0in;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">I've documented low-level hardware APIs, but never REST APIs -- I 
learned a ton working in Swagger for a Watson service API.<div 
style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 3.75pt;"> 
<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 
3.75pt;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">Looking back, it breaks down into two parts:<o:p></o:p> 
<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 
3.75pt;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">Learning about APIs, and learning about the Watson 
service.<o:p></o:p><div style="background: white; line-height: 13.5pt; 
margin-bottom: .0001pt; margin-bottom: 0in; margin-left: 0in; margin-right: 
0in; margin-top: 3.75pt;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;"> 
<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 
3.75pt;">**<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">Learning about REST APIs:**<span style="color: #222222; 
font-family: &quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; 
mso-bidi-font-family: Helvetica;"><o:p></o:p><div style="background: white; 
line-height: 13.5pt; margin-bottom: .0001pt; margin-bottom: 0in; margin-left: 
0in; margin-right: 0in; margin-top: 3.75pt;"><strong><span style="color: 
#222222; font-family: &quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; 
mso-bidi-font-family: Helvetica;"> 
</strong><div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><!--[if 
!supportLists]--><span style="color: #222222; font-family: Symbol; font-size: 
10.0pt; mso-bidi-font-family: Symbol; mso-bidi-font-size: 9.0pt; 
mso-fareast-font-family: Symbol;">·<span style="font-family: 'Times New 
Roman'; font-size: 7pt; font-stretch: normal; line-height: normal;">        
<!--[endif]-->**<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">doc tutorials - **<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">For an introduction to fundamental API concepts and terminology, I 
found<span class="apple-converted-space"> **Tom Johnson's**<span 
class="apple-converted-space">** ****<span style="color: #1970b0;">[tutorial 
on documenting APIs](http://idratherbewriting.com/docapis_course_overview/) 
**invaluable-- he even had a<span class="apple-converted-space"> [<span 
style="color: #1970b0;">post 
](http://idratherbewriting.com/pubapis_swagger/)on Swagger specifically! 
(Tom's a prominent blogger in tech communications; in fact, I read his blog 
really intensively about 5 years ago when I decided to go into tech writing!) 
He helped me talk intelligently about endpoints, resources, query strings, 
etc.<o:p></o:p><div class="MsoNormal" style="background: white; line-height: 
13.5pt; margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: 
auto; mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: 
-.25in;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;"> 
<div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><!--[if 
!supportLists]--><span style="color: #222222; font-family: Symbol; font-size: 
10.0pt; mso-bidi-font-family: Symbol; mso-bidi-font-size: 9.0pt; 
mso-fareast-font-family: Symbol;">·<span style="font-family: 'Times New 
Roman'; font-size: 7pt; font-stretch: normal; line-height: normal;">        
<!--[endif]-->**<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">building swaggger - **<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">Getting a<span class="apple-converted-space"> **local swagger 
build**<span class="apple-converted-space"> up and running was a task and a 
half due to the build structure (which has since been simplified, 
thankfully!). I leaned heavily on colleagues, but I was eventually able to get 
the build running on my Linux virtual machine -- though not, strangely, only 
my local Windows machine.  I must have spent<span 
class="apple-converted-space"> <em>days</em><span 
class="apple-converted-space"> on this, yikes! But I wrote or updated 3 
process docs on the subject, so hopefully the next person will have less 
pain.<o:p></o:p><div class="MsoNormal" style="background: white; line-height: 
13.5pt; margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: 
auto; mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: 
-.25in;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;"> 
<div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><!--[if 
!supportLists]--><span style="color: #222222; font-family: Symbol; font-size: 
10.0pt; mso-bidi-font-family: Symbol; mso-bidi-font-size: 9.0pt; 
mso-fareast-font-family: Symbol;">·<span style="font-family: 'Times New 
Roman'; font-size: 7pt; font-stretch: normal; line-height: normal;">        
<!--[endif]-->**<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">modifying source code - **<span style="color: #222222; 
font-family: &quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; 
mso-bidi-font-family: Helvetica;">Adding annotations into the source java 
files using @API annotations was not too difficult. But I ran into some bugs, 
and for the first time,<span class="apple-converted-space">** ****posted and 
got answers about bugs on a developer forum**([<span style="color: 
#1970b0;">https://groups.google.com/forum/?fromgroups#!topic/swagger-swaggersocket/Xq7jCJS7WRc](https://groups.google.com/forum/?fromgroups#!topic/swagger-swaggersocket/Xq7jCJS7WRc), 
[<span style="color: 
#1970b0;">https://groups.google.com/forum/?fromgroups#!topic/swagger-swaggersocket/ZCg4UZYYn08](https://groups.google.com/forum/?fromgroups#!topic/swagger-swaggersocket/ZCg4UZYYn08) 
).<o:p></o:p><div class="MsoNormal" style="background: white; line-height: 
13.5pt; margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: 
auto; mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: 
-.25in;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;"> 
<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 3.75pt;"> 
      <div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><!--[if 
!supportLists]--><span style="color: #222222; font-family: Symbol; font-size: 
10.0pt; mso-bidi-font-family: Symbol; mso-bidi-font-size: 9.0pt; 
mso-fareast-font-family: Symbol;">·<span style="font-family: 'Times New 
Roman'; font-size: 7pt; font-stretch: normal; line-height: normal;">        
<!--[endif]-->**<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">REST fundamentals - **<span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">Learning to play around with the API forced me to learn some<span 
class="apple-converted-space"> REST fundamentals<span 
class="apple-converted-space"> too--when can I enter something in a parameter, 
versus typing a query string in the request URL? What syntax to use to  get 
parameter fields into the URL query strings? How can I discover whether a 
parameter field takes JSON or some other syntax? (answer--I think--is that 
there's not discoverable method; that's why you need the docs!)<div 
class="MsoNormal" style="background: white; line-height: 13.5pt; margin-left: 
0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"> 
<div style="background: white; line-height: 13.5pt; margin-bottom: .0001pt; 
margin-bottom: 0in; margin-left: 0in; margin-right: 0in; margin-top: 
3.75pt;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;">**Learning about the Watson service**<div style="background: 
white; line-height: 13.5pt; margin-bottom: .0001pt; margin-bottom: 0in; 
margin-left: 0in; margin-right: 0in; margin-top: 3.75pt;"><span style="color: 
#222222; font-family: &quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; 
mso-bidi-font-family: Helvetica;">My understanding of the resources I'm 
interacting with evolved quite substantially, though examining the source 
files for schemas and instance data, playing with the API, and most 
importantly, talking to the developers. I won't go into the details since the 
service isn't public yet, but I learned a great deal about type systems and 
entity/relationship modeling schemas.<div class="MsoNormal" style="background: 
white; line-height: 13.5pt; margin-left: 0in; mso-list: l0 level1 lfo1; 
mso-margin-bottom-alt: auto; mso-margin-top-alt: auto; tab-stops: list .5in; 
text-indent: -.25in;"><span style="color: #222222; font-family: 
&quot;Helvetica&quot;,sans-serif; font-size: 9.0pt; mso-bidi-font-family: 
Helvetica;"> 
<div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><span 
style="color: #222222; font-family: &quot;Helvetica&quot;,sans-serif; 
font-size: 9.0pt; mso-bidi-font-family: Helvetica;"> 
<div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><span 
style="color: #222222; font-family: &quot;Helvetica&quot;,sans-serif; 
font-size: 9.0pt; mso-bidi-font-family: Helvetica;"> 
<div class="MsoNormal" style="background: white; line-height: 13.5pt; 
margin-left: 0in; mso-list: l0 level1 lfo1; mso-margin-bottom-alt: auto; 
mso-margin-top-alt: auto; tab-stops: list .5in; text-indent: -.25in;"><span 
style="color: #222222; font-family: &quot;Helvetica&quot;,sans-serif; 
font-size: 9.0pt; mso-bidi-font-family: Helvetica;">**L** 