---
title: What is Pipi.. to the technical artist?
author: Marcus
layout: post
permalink: /what-is-pipi-to-the-technical-artist/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/07/what-is-pipi-to-technical-artist.html
categories:
  - Pipeline
---
<div>
  <a href="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/logo_nils.png"><img alt="" src="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/logo_nils.png" border="0" /></a>
</div>

<div>
</div>

#### <a href="http://tech-artists.org/forum/showthread.php?4065-Pipi-The-Visual-Effects-Pipeline" target="_blank">originally posted on tech-artists.org</a>

### Beating the bush

Ok, I think it&#8217;s safe to say that what we&#8217;re developing is already being developed in several places on this planet and is something that many of you may already familiar with. What we have done is recognize that not everyone has this luxury, especially the little guy. Our goal then is to make the most elegant and beautifully designed solution we possibly can and then make it available to all.

### $$$

We love cg. We work with it every day. And whether Pipi is to be distributed for free, as open-source software or in some other way sold will depend greatly on the feedback given here. Our primary objective is for Pipi to grow to be as beautiful as possible so that it may be useful enough for one, ten, or thousands of users. If the way to get there is giving it away for free or selling it on a per-user basis, that&#8217;s what we&#8217;re here to figure out. The way we do get there is up to you, me, and all of us together. Starting now.

### Our mantra is..

..**enable artists**. This means building a foundation upon simple ideas. Simple enough so that when a tool fails, you know what to do. Too many times have I experience situations in which the tool, blindly trusted upon, fails &#8211; leaving the user helpless and in need of technical support. To truly enable, the user must be given a choice.

### Our design is..

..beautiful. We believe frustration degrades productivity. And one of the ways frustration is born is through the way in which we interact with our tools. That is why user experience and its technical implementation bear equal importance to us.

<pre>We build <em>from</em> the user experience, not towards it.</pre>

### Where we are

We would like to think of Pipi as Process Management, rather than Task Management. This is where Pipi fits in compared to existing Task Management Suites, such as Shotgun and FTrack.

<img class="aligncenter" alt="" src="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/20130717_taskmanagement_vs_processmanagement.png" width="476" height="510" />

&nbsp;

### Development

We love agile development methodologies and the lean startup method and recognize that no process is a linear as this. Thats one of the reasons why we&#8217;re here. Our initial goal is for Pipi to become useful to 1 studio, reasonably small yet know what they want and how to go about doing it manually. We are on the lookout for one that is interested and fits the role of the earlyvangelist.

<img class="aligncenter" alt="" src="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/earlyvangelist.png" width="300" height="225" />

<div>
</div>

From there, development will orbit around what is most urgent to them. We will then branch outwards into a closed-beta. A cycle which we&#8217;ll repeat for each of the main development areas &#8211; foundation, usability, tools &#8211; until we then move on to the next area of application &#8211; Pre-production, Animation, Post-production &#8211; covering aspects from Animation, VFX and Games as separate beasts.

> I&#8217;ve tried to illustrate this process.

<img class="aligncenter" alt="" src="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/20130718_development_roadmap2.png" width="890" height="1010" />

### 

### Benefits, not features

We&#8217;ve broken down the most basic usage of a pipeline to a set of 6 set of tools. Those are Dashboard, Editor, Library, Publisher, Inspector and Manager.

> Dashboard

This is what each user of Pipi will be most familiar with. It serves as an entry point for each artist at the start of each new day. It is where the user specifies what to work with and in what application. The Dashboard then sets up the environment and runs the application.

> Editor

When creating in-development assets or shots, the Editor is where metadata is entered.

> Library

For browsing available assets

> Publisher

For creating an inactive (aka published) asset

> Inspector

For exploring metadata and events

> Manager

For loading and modifying instances of assets from within a DCC application, such as Maya.

From here, we will move on to more complex benefits, catering to extensibility and debugging followed by in-the-dirt tools used by artists in specific disciplines, such as utilities for the animator or setup artist.

> Illustration here

<img class="aligncenter" alt="" src="https://dl.dropboxusercontent.com/u/779859/tech-artists.org/20130718_feature_roadmap3.png" width="3660" height="1570" />

&nbsp;

I&#8217;ll hold off showing you actual designs and prototypes until next time. TMI! TMI my friend! <img src='http://abstractfactory.io/blog/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' /> 

Let me know what you think!

Best,  
Marcus

# FAQ

**Wait, who the hell are you?**  
My name is Marcus Ottosson. I&#8217;ve been making beautiful cg since 2008, time spent at over 10 vfx studios across Europe ranging from commercials to feature film to idents to triple-A game cinematics.

**The video on <a href="http://pipi.io/" target="_blank">your website</a> doesn&#8217;t contain all of the information I need**  
It doesn&#8217;t. But we hope it provides you with enough of an introduction to understand our initial goals.

**Isn&#8217;t this basically Shotgun?**  
No. Shotgun connects people. Pipi connects the software that people uses.

**Python, python, python**  
Yes. We develop with Python and Qt.

**I&#8217;m using software [X]. Will it be supported?**  
Where there&#8217;s a will there&#8217;s a way. We&#8217;ve been successfully prototyping with Maya and Nuke and aim to cover all of the packages that you use. Let us know what is important to you and we&#8217;ll move it higher on our checklist.

**What about a database?**  
Yes, who needs &#8216;em. Pipi runs under the Unix philosophy &#8220;Everything is a file&#8221;. That, coupled with a technique similar to the localised metadata storage used by OS X (.DS_Store), help keep the guts of Pipi simple and logical with very small learning curve.

**How about version control?**  
I&#8217;ll have to rely on you to light the way in this regard as I have no experience with Perforce or other any off-the-shelf solution to binary media revision control, nor have I heard or seen of any DCC house (besides in games) that make use of it.

**Will we have to reformat our folder structure to work with Pipi?**  
No. Our mantra is &#8220;Enable Artists&#8221;, rather than &#8220;Enforce Artists&#8221;. Pipi wraps any existing layout you might have (given it is logical) and provides a unified way of accessing content through code rather than static filepaths.

**I need more information**  
Just ask.