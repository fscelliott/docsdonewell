---
layout: single
title: Baby steps toward a Bayes classifer
date: '2015-06-03T13:22:00.004-07:00'
author: frances
tags: 
modified_time: '2015-06-03T13:28:07.463-07:00'
thumbnail: http://1.bp.blogspot.com/-axKHwWTHYIc/VW9hK6jBBgI/AAAAAAAANVw/8RC890mKqVY/s72-c/bayes%2BUI.png
blogger_id: tag:blogger.com,1999:blog-2779361939324367100.post-4336054696840512857
blogger_orig_url: http://elliottworklife.blogspot.com/2015/06/a-baby-bayes-classifer.html
---

Actually, the blog title is a misnomer--I started trying to code up a naive 
Bayes classifer while studying[ chapter 6](http://www.nltk.org/book/ch06.html) 
of the Python NLTK book, but I didn't get very far before I switched over to a 
tutorial on the scikit-learn [random forest 
classifer](https://www.kaggle.com/c/word2vec-nlp-tutorial/details/part-1-for-beginners-bag-of-words), 
because it aimed at building something instead of demonstrating little 
building blocks. 

I haven't gotten far, but at this point I can create a feature set from a 
cleaned-up 'bag of words' using scikit-learn. 
<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" height="149" 
src="http://1.bp.blogspot.com/-axKHwWTHYIc/VW9hK6jBBgI/AAAAAAAANVw/8RC890mKqVY/s320/bayes%2BUI.png" 
width="320" 
/>](http://1.bp.blogspot.com/-axKHwWTHYIc/VW9hK6jBBgI/AAAAAAAANVw/8RC890mKqVY/s1600/bayes%2BUI.png) 


Next up: training the random forest! (I love the terminology involved, by the 
way. "training the random forest" sounds like a nonsense poem). 