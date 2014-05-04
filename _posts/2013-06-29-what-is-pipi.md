---
title: What is Pipi
author: Marcus
layout: post
permalink: /what-is-pipi/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/06/what-is-pipi.html
categories:
  - Theory
---
It has taken me a long time to define Pipi. As I made my way from studio to studio over the course of the past five years, each one had this &#8220;something&#8221; about it that made work a much more pleasant experience. Turning these, usually repetitive and cumbersome tasks, into welcome distractions.

These studios all displayed patterns of the &#8220;earlyvangelist&#8221;. The characteristics are as follows; the earlyvangelist:

1.  Has a problem
2.  Is aware of having a problem
3.  Has been actively looking for a solution
4.  Has put together a solution out of piece parts
5.  Has or can acquire a budget

I remember this one artist of a mid-sized house here in the UK who told me he had suggested to management that he wanted to build better tools that could help reduce the rate of mistakes and boost productivity of their crew, but the benefits was unseen by management and so never allowed him to proceed.

Management is not to blame, however. It is difficult to visualise the abstract benefits of what you do not know. It reminds me of a famous quote by Henry Ford. &#8221;If I had asked people what they wanted, they would have said faster horses.&#8221;  Although <a href="http://blogs.hbr.org/cs/2011/08/henry_ford_never_said_the_fast.html" target="_blank">fake</a>, its message holds true. It is a trait of human nature to try and improve on what we have by mere optimisation rather than stepping outside of that box and into unfamiliar territory. The territory of <a href="http://en.wikipedia.org/wiki/Innovation" target="_blank">innovation</a>.

Developing tools is expensive. Both in terms of money and time. There is an inevitable period of trial-and-error when breaking new ground. But what you get out of this process is invaluable. Not only will it accelerate your rate of delivery, it will enhance it, make it stronger and more accurate. The rate of mistakes will drop significantly and the happiness-factor of your workforce will increase.

As I have spent the past year refining this idea and the solutions that came with it, the smoke has cleared and my vision is slightly less blurry. I would now like to give you an overview of some of my conclusions thus far.

### What is Pipi?

Pipi is a Digital Content Creation (DCC) framework for the film, commercial and games industries.

### Why Pipi?

Digital content creation is rapidly getting more and more divided into areas of special expertise and along the way we have forgotten to keep the pieces in sync. Pipi aims to solve exactly that.

### How does it work?

Pipi is a <a href="http://en.wikipedia.org/wiki/Software_framework" target="_blank">framework</a>. It provides you with an essential set of tools along with a foundation upon which to build your own tools that fit into your studio&#8217;s unique way of working. It then integrates with the major existing applications, such as Maya and Nuke, and frameworks delivered by third-party developers, such as Shotgun and FTrack, to help take the hassle out of fast-paced production development.

### Tools?

Pipi ships with six essential tools that serve as pivot-points for your work and own custom tools development. These tools, in order of relevance, are **Launcher**, **Inspector**, **Creator**, **Library**, **Publisher **and **Handler**

I will now go over the supplied set of tools in more detail.

# Launcher

<img class="alignnone" alt="" src="http://3.bp.blogspot.com/-iDR8PatfDiw/Uc6lSh0Nw4I/AAAAAAAAAk8/GmINWcw5gFA/s1196/launcher_ux_creatorinterop_withtransparency_0000_Just-opened.png" width="1196" height="616" />

Main entry-point for artists. This is what is booted up at the dawn of each day as artists begin their work. It supplies artists with an overview of each project and its content along with the ability to manage projects from a higher-level point of view;  creating sequences, editing assets, removing shots is all performed via the Launcher.

# Inspector

<img class="alignnone" alt="" src="http://4.bp.blogspot.com/-u2NiX7u1abE/Uc6lSPGj-uI/AAAAAAAAAkw/LDHUsqVPLHo/s808/inspector_v002.png" width="650" height="808" />  
Each job, each asset and each shot come bundled with data. This &#8220;data about data&#8221; is referred to as <a href="https://en.wikipedia.org/wiki/Metadata" target="_blank">metadata</a>, and shots et. al. are in turn known as <a href="http://en.wikipedia.org/wiki/Entity" target="_blank">entities</a>.  
As the number of entities grow, metadata helps to keep things organized. To give an example, it can be used to keep track of frame-ranges in a shot, comments in playblasts or artist-supplied descriptions for assets. The Inspector then provides the means to visualise this data.  
In addition to visualising data, the Inspector also provides the means to monitor what is referred to as &#8220;events&#8221;. Events are recorded throughout the use of Pipi. Any time an artist comments on a shot, publishes his/her work or playblasts a shot in preparation for dailies, the recorded event can be monitored by other artists. This helps artists working on the same asset or shot stay in sync with each other and makes it easy to stay up to date on the overall progress for each chunk of work.

# Creator

<img class="alignnone" alt="" src="http://4.bp.blogspot.com/-rKFQoGC8_ZM/Uc6lSHJwwqI/AAAAAAAAAk0/Xe2MJ4yuCBw/s892/creator_mockup_2_v001.png" width="892" height="730" />  
As you start a new job, the Launcher provides the means of adding the necessary sequences, shots, assets and variants into that job. It is in the Creator where you append or remove metadata such as camera information, storyboards, references, audio or video et al. The metadata can then be accessed by artists, other Pipi tools or your custom tools.

Creator is most commonly accessed via the Launcher. Whenever an entity is edited, Creator will appear.

# Publisher

<img class="alignnone" alt="" src="http://4.bp.blogspot.com/-RPrP0pDGbQo/Uc6lTOhOBWI/AAAAAAAAAlM/ItljpPLrUj8/s652/publisher_ux_001_v001.png" width="575" height="652" />  
I mentioned that in a studio, work is divided into chunks and that each chunk is delegated to specialists. These specialists communicate with each other by &#8220;publishing&#8221; their finished material onto a central database. Other specialists can then access this material knowing that it conforms to a fixed set of studio rules. Background props, for instance, may have to conform to a certain polygon-count, character setups may have to provide a certain set of controls familiar to animators and so on.  
The Publisher then acts as the funnel through which each shared chunk of work is passed before it reaches the public space. The publisher will perform sanity-checks (e.g. &#8220;is the geometry visible?&#8221;) on your work to ensure it conforms to the already published work, in addition to help artists meet the required guidelines.

# Library

<img class="alignnone" alt="" src="http://4.bp.blogspot.com/-2ya6JBq6GSY/Uc6lS176GKI/AAAAAAAAAlE/WnT0FsauG0M/s871/library_ux_1_v001.png" width="871" height="696" />  
Once an artist has published his/her work, it can be found in the Library. The Library provides a birds-eye view of each published entity of each job within a studio. It allows artists not only to load animations, point-caches and assets, but also to perform an at-a-glance inspection of metadata, relations between it and other entities, their history and preview the data directly in the Library. This makes the process of finding what you are looking effortless for any artist.

# Handler

<img class="alignnone" alt="" src="http://4.bp.blogspot.com/-M5Mc1NjRsDs/Uc6mZ1y_fPI/AAAAAAAAAlk/O-vzwRQR3KA/s547/handler_design01_v002.png" width="424" height="547" />  
The Handler is the only application-specific tool so far. It deals with the specifics of how an application deals with assets, such as rigs or point-caches. To aid in explaining I&#8217;ll use Maya as case-in-point. In Maya, once an asset such as a rig has been loaded, it provides the user with a few options. Such as whether the asset should be imported or referenced, which version to load and the ability to up- or downgrade assets. Things which makes a difference only within the specific domain in which the artist is working at the time.

I mentioned that it is application-specific. This means that for each application to make use of it, it has to be provided with an implementation. This is due to the alternating ways applications deal with assets. In Nuke, an asset is an image-sequence loaded via its internal nodes known as &#8220;Read&#8221;. Maya can also load image-sequences, but does so via different means. The Handler then provides a high-level abstraction from these technicalities that can be manipulated via it&#8217;s user interface so that the artist only has to focus on the &#8220;what&#8221; and not the &#8220;how&#8221;.

> ..focus on the &#8220;what&#8221; and not the &#8220;how&#8221;

Initially, the Handler will be provided for Maya. Other applications will be supported at a rate fitted for their popularity.

With these tools at hand, an additional set of tools are being developed. Such as a relational viewer to display relationships between the entities within a studio, a rigging framework including &#8220;weightshift&#8221; and an animation library utilities for storing poses and reusable segments of animation.

Hope you enjoyed and thanks for your attention.