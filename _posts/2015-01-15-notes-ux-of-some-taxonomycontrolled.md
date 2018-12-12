---
layout: single
title: Notes on the UX of some taxonomy/controlled vocabulary software
date: '2015-01-15T13:24:00.002-08:00'
author: frances
tags: 
modified_time: '2015-02-03T10:29:30.758-08:00'


---

I'm taking Simmons College School of Library and Information Science's online 
Taxonomy and Controlled Vocabularies course at the moment, and thought I'd 
post some notes and first impressions I had as a beginner of the software 
we're trying out in the class. 


<a name='more'></a> 



## Interaction design notes for Synaptica 
--Biggest question: 
     why can't you easily enter and edit terms in a hierarchical view that 
also displays non-hierarchical term relationships? (as in the "Hierarchical 
Report with Additional Relationship Types" report view )?  Is there a 
philosophical difference frqom back-of-the-book indexing software, or is it 
just cumbersome interaction design? (my guess is the latter, since other 
taxonomy software seems to allow this. In particular, it's pretty clunky in 
the Item Summary to cycle through 'add (term)-add relationship--edit 
relationship.) 

 This questions comes from having studied SKY indexing software a little bit, 
where it's really easy to enter term relationships in 1 big window where all 
terms are displayed. I find sorting through individual term panes rather 
painful in comparison. 


--Feature question: what flavor of regular expression supported? I always wish 
UIs would specify this instead of using the vague "wildcard" label. for 
example, Ultraedit lets you choose between Ultredit and UNIX style regex. From 
some digging and experimenting, I eventually found that they meant SQL-style 
wildcards, where the percent sign (%) matches zero or more characters, and 
underscore (_) a single character. so you can match a term like 
"Afforestation" with A_%tion ...but that doesn't seem very powerful :/ 


--there seem to be too many easily visible search options ('smart', 'exact', 
etc), when I bet that people normally default to 1 search flavor. 

-visual style: dropdowns, such as those in the Current Relationship Window, 
should have a dropdown indicator 

-I shouldn't get a prompt every time I want to change a relationship. instead, 
I should have an Undo function, through either a button or Ctrl Z 

--In a term edit form, I managed to close without saving edits. That form 
should auto save periodically, AND when you close the window.  save button 
should be grayed out when no new changes 

-if I try add a prexisting term, I shouldn't get an error message, instead, I 
should get a link to that existing term. This circles back to the idea that 
the multiple tabs could be merged into 1 big UI.... 

-The dropdown category labeled Relationship should be much closer to the 
"add/edit relationship" button; I missed it at first. 

REPORTING 
--in the option to alphabetically browse, I totally missed the "select 
letter/number" instruction.  Seems it'd be clearer if the browse window 
populated by default with a long-scrolling window showing the alphabetical 
arrangement, with a permanent A-Z navigation element across the top 


-shouldn't I be able to save my report options as a 'bookmark' or 'saved 
report" so I can regenerate the report easily? (be even nicer if I could 
populate the "Reports" tab menu with saved report bookmarks" also I'd change 
the button 'save report" to 'export report" so I could disambiguate between 
saved presets vs. an output like a pdf 

-shouldn't there be a 'quick report' option with a bunch of presets and the 
opportunity to change the most-used options, and then expand to include 
advanced options, so you don't have to scroll and click through 2 pages to 
generate a report? 


TOP-LEVEL NAVIGATION 

Failing merging the top-level tabs into 1 UI, at the very least clicking a top 
level tab such as Add or Reports should display a dropdown with navigation 
elements. For example, the Reports tab should dropdown (Alph, Hier, etc) 




## Interaction design notes for Poolparty Semantic Suite 
 
yaaay! This is a much slicker interaction design (I bet it was developed more 
recently than Synaptica): 

-easy to add terms in a hierarchical view. especially cool that you can 
drag n drop terms to create relationships 

-search bar is always present and makes some useful assumptions (you're 
searching w/in the current thesaurus, clicking the suggested auto-complete 
term from the search bar takes you straight to editing the term) 

-Tree hierarchy is a little difficult to read with white-on-color scheme and 
small font. 


Overall, seems great for its purpose (linked data). I do wonder if it gets 
messy trying to manage poly hierarchies. 