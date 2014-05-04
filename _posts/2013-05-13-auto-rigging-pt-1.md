---
title: Auto Rigging pt. 1
author: Marcus
layout: post
permalink: /auto-rigging-pt-1/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/05/auto-rigging-pt-1.html
categories:
  - Theory
---
A somewhat overloaded term. What does it actually mean to &#8220;autorig&#8221; something? Firstly, let&#8217;s look at why one would consider autorigging for their project.

### Why?

<div>
  Lets have a look at a simple task, such as setting up forward kinematics controls for an arm.
</div>

<div>
</div>

<div>
</div>

<div>
  The video is sped up 5x and takes about two minutes to play out. Its quite the task! Also, note that after the joints have been drawn, no <b>new</b> information is added. The joints contain both position, orientation and hierarchical information which is all that is required for the subject to behave as expected. Everything past that point is implementation detail, technicalities, that can be automated. Also note that the drawing is the least time consuming process.</p> <p>
    I think this will suffice as motivation for automation.
  </p>
  
  <h3>
    What else? 
  </h3>
  
  <p>
    Well, a human usually has two of these along with legs, each side being identical to the other in any meaningful regard. That means that the additional time it takes to also set up the other side is of equal length to the one we just set up, meaning that what you do you&#8217;ll have to do four times to cover each limb of a character.
  </p>
  
  <p>
    Put simply, rigging is a repetative task. The very many things you do for each setup are densly similar to tasks you just did or have done previously. How about a bullet list of some of the main things that automation can help you with?
  </p>
</div>

#### Symmetry

This is a big one. We can cut out job in half if one side simply followed the other. Even if your characters suffers from asymmetry, such as zombies, chances are that **features** are still to be repeated to the other side.

#### Common features

Many things have been done before and works. Automation could keep you from reinventing the wheel more than once

#### Time well spent

Time spent repeating is time wasted and nothing hinders creativity more than that of wasted time. You&#8217;ll spend half the time performing repetative tasks and the other half thinking of ways around those tasks. Not having to worry about things already solved will allow you to focus on moving forward and make things better and faster. <div>
  <h3>
    Ok, let&#8217;s get crackin&#8217;
  </h3>
  
  <div>
  </div>
  
  <p>
    Hold on there. Even though the end result is to have an intutive control rig for the animator, the way to get there is often different with each artist. Before deciding whether to automate something, it is important to understand exactly what it is you wish to automate and such information is best taken from experience. If you&#8217;re thinking &#8220;I dislike rigging and want to automate it in order to get it out of my way&#8221; you&#8217;re reading the wrong post. Once you know what to do, you must also understand it. Remember, you can&#8217;t design what you don&#8217;t understand.
  </p>
  
  <p>
    Lets have a look at another video, this time the video has been sped up only two times, is half as long and  contains twice as many features on four times as many limbs as the previous video.
  </p>
</div>

### What happened there?

<div>
</div>

<div>
  As you can see, the result of this video is the same as the previous video, and more, in less time. What is missing from this video are things that have been automated based on the initial drawing of the joints along with their naming schemes. Remember, anything beyond that point is implementation detail and is repetative with each setup. Once you know how to setup forward kinematics, the same rules apply for each and every forward kinematic enabled setup you do and the same goes for inverse kinematics, twisting, bending, stretching, pinning, space switching and so on.
</div>

<div>
</div>

<div>
  Currently working on this tool, the next incarnation will do more without requiring any more work from the user. Thats the beauty of automation.
</div>