---
title: Pipi Object Model pt. 1
author: Marcus
layout: post
permalink: /pipi-object-model-pt-1/
mytory_md_path:
  - https://dl.dropboxusercontent.com/u/779859/Abstract%20Factory/blog/pipi%20object%20model/part%201.txt
categories:
  - Uncategorized
---
> This series of posts is about the current object model employed in Pipi. What it is, does and works. How it came to be, why it is needed need it and what life would be like without it. 

Lets start with a target.

<pre>Output may be altered up-stream and sent down-stream with little or no effort.</pre>

This is the main goal of Pipi as a whole, where the object model plays a substantial part. We will break down and further refine this goal as we go along, but for now, let&#8217;s move on and define what I mean with &#8220;object model&#8221;.

Quoting from Steve McConnell in his book [Code Complete 2nd edition][1]

> #### 2.1 The Importance of Metaphors
> 
> Important developments often arise out of analogies. By comparing a topic you understand poorly to something similar you understand better, you can come up with insights that result in a better understanding of the less-familiar topic. This use of metaphor is called “modeling.” 

Thus, an *object model* is a *collection of metaphors*

# Working in construction

Lets give an example. Lets say you are a construction worker and working with bricks is what you know best.

With a `brick`, you can establish higher-level objects such as a `stack of bricks`, a `wall`, a `room` and a `house`.

These objects form the **object model** in which you operate, each object being derived from something other than bricks themselves (e.g. a `wall`) to help us deal with a large amount of smaller objects (e.g. `bricks`).

With metaphors such as these, someone who knows very little about construction (me) can walk up to you and say &#8220;build me a house&#8221; without having to get into excruciating details about how to do so &#8211; like the fact that a `room` needs `walls` which in turn needs many `stack of bricks` which needs `bricks`.

In fact, the use of `brick` in this scenario is a mere implementation detail. It matters very little to me whether you use `bricks` or `planks` or `adamantium`. I asked for a `house` and what matters to me is that it is located close to where I work, is warm and feels cosy. Only then do you get my money.

# 1 and 0

In computing, our only bricks are the 1 and the 0 and unless you are autistic these numbers won&#8217;t mean much to you. So in order to get the level where I can come to you and say &#8220;build me a digital asset management pipeline&#8221; we&#8217;ll first have to apply a few metaphors to these numbers.

In this series of posts, I&#8217;ll be taking you through some of the steps I&#8217;ve gone through in finding these objects, why some metaphors have been used in favour of others and what lies ahead.

But first, lets establish some common ground.

# What is a Pipeline

Jono Gibbs of Dreamworks, in his [SIGGRAPH University][2] course, defined it as

> A [framework][3] for how you want to work. 

And Mike Stein of MPC, from the same course, explained it as

> A set of software tools and technologies that enables artists to perform a large number of tasks consistently, efficiently and repeatably. 

[Wiki][4] defines a pipeline as being

> A set of data processing elements connected in series, where the output of one element is the input of the next. 

Of course, Wikipedias definition is not in regards to a digital asset management pipeline; however I&#8217;d like to think of our digital asset management pipeline as being derived from it.

Lets see if we can&#8217;t re-format this last one into more familiar terms.

A pipeline is

> A set of artists connected in series, where the output of one is the input of the next. 

Now we may start to see some resemblance.

The [Directed Acyclic Graph][5] (DAG for short) is one flavour of such processing model. There, a connection is referred to as an `edge` and each processing element called `vertex`.

We will get back to this model in part 2. Let&#8217;s move on and have a quick look at how a traditional pipeline as it exists today.

# The traditional pipeline

![alt text][6]  
Credit: http://zealotcrazytalk.blogspot.com/  
James A. Beane (c)

# Understanding our understanding

As humans, our understanding is limited.

Our brains prefer reusing knowledge it has already established when encountering new knowledge and rightly so. Much in our existence have similarities and behave similarly. In many cases identically. In science, this process is called [Neural Reuse][7]

According to this *theory* (it is, after all, reversely engineered science), our brains can absorb vast amounts of &#8220;new&#8221; information instantly by mere connection to previously existing information.

Take this example.

My new brand of `Dumbars` is just like `Snickers`. There. You just applied all of your knowledge about `Snickers`, and all knowledge already connected to it, and connected it to the newly established space in your brain for `Dumbars`. You now know as much about it as you already knew about `Snickers`, yet less than 5 seconds ago you had never heard of `Dumbars`.

The important thing to take away from this example is &#8211; I could&#8217;ve replaced `Snickers` with anything and it would&#8217;ve changed your entire spectrum of knowledge about `Dumbars`.

This way of modeling new information is called *prototype-based modeling* and was first introduced in the 70s by Douglas Hofstadter and his book [Gödel, Escher, Bach: An Eternal Golden Braid][8].

Put simply, it is how our brains work.

# Origin of Metaphors

The great thing about this ability is that our brain doesn&#8217;t seem to care about where you connect existing information.

> &#8220;But I, being poor, have only my dreams. I have spread my dreams under your feet. Tread softly because you tread on my dreams.&#8221; &#8211; Equilibrium, 2002 

Dreams aren&#8217;t capable of being spread anywhere, yet you may refer to them as being spread underneath ones feet in order to aid in the recipients understanding of how you feel.

Besides being a useful tool to communicate feelings, which are abstract in nature, the same holds true in computers, where what we operate on is also abstract.

# Finding a commonality

While metaphors allow complex and new information to be absorbed quickly, an even more powerful tool our ability to apply seemingly different information in a similar fashion, without having to dedicate any room in our mind for each chunk individually.

> A further aspect of consistency is the use of familiar patterns and standard platform idioms. When you buy a new car, you don’t have to relearn how to drive. The concept of using brake and accelerator pedals, a steering wheel, and a gear stick (be it manual or automatic) is universal the world over. &#8211; Martin Reddy, API Design for C++, 2.4 

This is helpful as it allows us to only remember a minimal amount of new information.

Looking at the illustration above, what similarities are shared across each step?

For instance, we know that:  
1. Data arrives  
2. Data transforms  
3. Data travels

# Data &#8211; Arrives, transforms, travels

Referring back to the wikipedia definition of a pipeline, this fits rather well. `data` arrives at one artist, is transformed in some way and then travels on.

Lets have a look at what that something may be.

You are a modeler in Studio Dumbars and have just received artwork, or `data` of a hero character. You translate this `data` into a 3d model and send it back out.

The `data` has undergone change. From a higher-level perspective, `data` remains the same. It is still the same hero character, yet various properties have now changed.

In the next part, we&#8217;ll have a closer look at the Directed Acyclic Graph, how `data` may  
flow within it and look at how we can exploit the features of our brain, specifically the use of metaphors, to try and understand it all.

Stay tuned, thanks and see you in a bit.

Marcus

Links  
- [Directed Acyclic Graph][5]  
- [Software Framework][3]  
- [Object Design][9]  
- [Responsibility-driven design][10]  
- [Gödel, Escher, Bach: An Eternal Golden Braid][8]  
- [Neural Reuse][7]  
- [Building A Company-Wide Framework For Your Art Pipelines][11]  
- [SIGGRAPH University][2]  
- [Domain Knowledge][12]  
- [Pipeline Computing][4]  
- [Universal Design Pattern][13]  
- [Code Complete 2nd edition][1]

 [1]: http://www.amazon.co.uk/Code-Complete-Practical-Handbook-Construction/dp/0735619670
 [2]: http://youtu.be/MA_tpeyas4o
 [3]: http://en.wikipedia.org/wiki/Software_framework
 [4]: http://en.wikipedia.org/wiki/Pipeline_(computing)
 [5]: http://en.wikipedia.org/wiki/Directed_acyclic_graph
 [6]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/3d_production_pipeline1.jpg
 [7]: http://www.ncbi.nlm.nih.gov/pubmed/20964882
 [8]: http://en.wikipedia.org/wiki/G%C3%B6del,_Escher,_Bach
 [9]: http://www.amazon.com/Object-Design-Roles-Responsibilities-Collaborations/dp/0201379430
 [10]: http://en.wikipedia.org/wiki/Responsibility-driven_design
 [11]: http://christianakesson.com/2012/218
 [12]: http://en.wikipedia.org/wiki/Domain_knowledge
 [13]: http://steve-yegge.blogspot.co.uk/2008/10/universal-design-pattern.html