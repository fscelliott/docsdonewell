---
layout: single
title: Studying machine learning through Coursera
date: '2016-05-04T08:51:00.000-07:00'
author: frances
tags: 
modified_time: '2016-05-17T11:08:22.909-07:00'


---

Since I document tech that involves machine learning and natural language 
processing, I've been meaning for a while to take [Coursera's Machine 
Learning](https://www.coursera.org/learn/machine-learning/) course. And I have 
a bit of bandwidth at work now, so that's what I'm doing. 

It's great! I'll admit, I was doubtful if I'd understand anything since 
(shameful secret!) I never took calculus in high school; I opted for AP stats 
instead. At the time I was totally focused on studying classical music -- it 
never occurred to me I might wish one day I had. 

Fortunately, the instructor is really, really good at going slow and 
reassuringly pointing out when we don't actually have to understand the 
calculus or stats he's talking about.  He's also really good a giving us an 
intuitive understanding of the purpose of a formula. So, while I don't 
understand how to calculate a partial derivative for gradient descent, I *do* 
understand how taking the tangent of a curve gets us to take a step in the 
direction of steepest descent. 

It also helps to have a spouse with a PhD in math; when the instructor 
mentioned the "line search" strategy for choosing step size but didn't go into 
details, my husband sketched out a 2-D representation that made intuitive 
sense to me. 

I thought doing the homework would force me to understand the calculus/stats 
the teacher said we didn't need to understand...but it turns out that's not 
the case. Instead, so far it's more about learning the ins and outs of matrix 
math and of Octave, the programming language we're using. I'll admit, I'd be 
pretty lost without StackOverflow and the course wiki. That said, when I see 
students posting the same questions I had, it reassures me that I'm
on the right track. 

This course got me thinking about how being totally unintimidated and getting 
by with "sorta understanding" is a valuable tech writer skill. Back in my 
student days, I wanted to master everything from the get-go. But teaching 
myself coding and learning about technology on the job taught me to grab at 
the overview first, and fill in the confusing bits as I 
go. It's like my ability to read a book or a bunch of online info really 
quickly and connect the big-picture points first (something my 
engineering-trained spouse would never do).  That's not an approach that works 
for every field, but it sure works for a tech writer! 

Another thing this course got me thinking about was how I love to learn. 
Again, back in my student days, there was so much to learn that I easily 
prioritized my strengths over less interesting material. Sure, math was OK, 
but there were plenty of more compelling subjects to study.  But as adults, we 
have less chance to learn new stuff (again, another reason I like being a tech 
writer -- I get to study!), and I find myself revisiting math with fresh 
appreciation. Maybe math is not my main talent, but who cares? I'm learning, 
and I love how my brain feels when that happens. 

## Update 
In the end, I did the homework and implemented gradient descent for linear 
regression and for logistic regression in Octave (with much online help). 
After that, I mostly audited the course and took notes. Some highlights I took 
away (probably I've mis-stated a bunch of stuff; I'd have to rewatch the 
videos to get it exactly right): 

1. Neural networks let you compute truth tables for logic operations like AND, 
OR, XNOR, bv varying the weights (thetas) of your inputs and then running the 
sigmoid function on the sum of the weighted inputs. In each hidden layer, you 
learn a new theta through forward propagation, i.e. through reapplying the 
sigmoid function(???) 
1. Support vector machines are similar to logistic regression, with the 
addition of kernels (landmarks to which you measure the similarity, or 
distance, of your examples). In cost optimization, you compute the 'vector 
inner product'  (just a Pythagorean measure of length) between theta and 
training example, and try to maximize that distance, p, in order to get large 
margins between the examples and the decision boundary 
1. Unsupervised learning using k-means clustering was conceptually a lot 
simpler than I expected. You randomly initialize some k number of cluster (c) 
centroids (mu)  from your training set, compute the distances of the training 
points to the centroids, and classify them into clusters based on how far they 
are. Then you take the means of the distances in each cluster, place the 
centroids at those means, and recalculate the distances in order to come up 
with new clusters, then retake the means..etc. 