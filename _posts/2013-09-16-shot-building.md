---
title: Shot Building
author: Marcus
layout: post
permalink: /shot-building/
categories:
  - Architecture
  - Pipeline
  - Theory
---
> Closing in on the end of yet another production in one of my freelance gigs, it dawned upon me the importance and relevance of being able to procedurally build shots as you go.
> 
> <span style="line-height: 1.714285714; font-size: 1rem;">Here are a few reasons.</span>

<span style="line-height: 1.714285714; font-size: 1rem;">As you start putting things together and getting ready for final renders, you traditionally end up with a master scene of sorts. As scene in which all of the work for that shot resides.</span>

From here, you integrate all of the separate pieces that make up that shot.

> &#8220;Change?&#8221;

Okay, you boot up the master scene, make the change and the scene just got a bit more complicated.

> &#8220;Another change?&#8221;

..you see where this is going. That scene is about to end up the same way they all do. In a mess. No one will be able to work with it except you and you won&#8217;t want to. You want the director to stop making changes because &#8211; lets face it &#8211; this shot it about to burst.

<pre>The more work you put in, the longer it takes to perform the work.</pre>

Say hello to Shot Building.

What is that? Fundamentally, it means you never work with a full scene directly but rather work on parts of it in isolation.

For example &#8211; in the vast environment of a metropolitan city, you are tasked with replacing one of the windows with a cracked version.

The building was created in isolation, so you boot up the asset. It&#8217;s relatively low-res and so you work on it in real-time. Perhaps it has several levels of detail.

Once you&#8217;re finished, you pop it back out under a new version.

Now you load your master scene and replace the window with your new version.

No!

Fact is. You don&#8217;t have to do anything. You&#8217;re done. Finished. In fact, there is no &#8220;master scene&#8221;

What? Surely it&#8217;s impossible to tell if your isolated part works with the rest of the scene unless its there with you. What about at least previewing what you&#8217;ve done?

Well..

Traditionally, once you hit render, everything in your scene is packaged up and sent to the renderer, e.g. Arnold.

But what if instead you could package up your scene and, as the data travels travels from Softimage to Arnold some additional data could tag along. Such as the rest of the city.

&#8220;But then..&#8221;

Your scene remains light and your render looks like it would if you were to have everything in your scene &#8211; making it your window into the final result.

The thing to realize is &#8211; adjustments are the ultimate time-consumer. On top of that, the majority of adjustments are small. Isolated. And thus, being forced into grappling with things that are to remain unchanged, you not only invite frustration into your life, you also risk altering what already works. You may even break it.

&#8220;So. What&#8217;s the catch?&#8221;

The caveat is, you get a lot of separate assets that need to be dealt with. Rather than having your master suite all loaded and managed internally within your DCC, using your special recipe for naming and sorting that only you could decipher, you&#8217;d have to rely on other means for management.

Say hello to Asset Management. (The topic of another talk)

What else do you get?

A scene may not be comprised of just the latest versions. What about an approval cycle? What about when an update is made that isn&#8217;t immediately reviewed, what if it&#8217;s faulty?

You&#8217;d want to allow automatic renders and scenes built by lighters and shading artists the flexibility of choice &#8211; whether they want to work with approved material or at the cutting-edge.

With proper asset management, it&#8217;d be possible for your coordinator to approve work from [Shotgun][1] and have it reflected in builds right away. How cool is that?

Now, not only have you sped up the working process of each artist but you&#8217;ve in fact abstracted away the software from the completed work.

If work is published into a common format regardless of software, such as [Alembic][2], you could build the same shot in Houdini, Maya, Softimage.. it doesn&#8217;t matter. What matters is the data that your artists produce and their relation to each other.

 [1]: http://www.shotgunsoftware.com/
 [2]: http://www.alembic.io/