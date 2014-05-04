---
title: Pipi Object Model pt. 3
author: Marcus
layout: post
permalink: /pipi-object-model-pt-3/
mytory_md_path:
  - 
categories:
  - Uncategorized
---
> In part 2, we further defined our pipeline, its intent and what is required to successfully implement it. Lets have a look at how tracking fits in with all of this. 

# Tracking

In electronics, tracking refers to

> The maintenance of a constant difference in frequency between two or more connected circuits or components. &#8211; Google &#8220;Definition of tracking&#8221; 

But for our intents and purposes, we may refer to it as the way in which `data` is inferred by other `data`.

Lets take an example.

Bob outputs an `obj` to John who turns it into an `mb` and sends it forward.

To the recipient of Johns output, there is only an `mb` &#8211; the `obj` is nowhere in sight, yet the `obj` had a significant impact on the creation of `mb`.

Here, tracking means to maintain a `link` between `obj` and `mb` so that the recipient of Johns output may later refer back to it.

# Why Tracking?

Yes, why bother. The `obj` is done, `mb` is what the cool kids are all talking about these days. However, consider this.

You are looking at the output of Mary, the compositor. Mary has produced a sequence of images for review and in the review there is you and there is Mary.

> &#8220;I want the plane to come in from the left&#8221; &#8211; you say. 

It is not in Mary&#8217;s responsibilities to alter neither animation nor camera so the request must be passed up-stream to whomever is responsible and capable of processing this change.

# Responding to Change

In [part 2][1], we touched briefly on how to deal with change. We said that in order for change to enter into a graph, a `node` must be capable of outputting partially finished information, before it is finished.

[Lean Manufacturing][2] was first coined by John Krafcik in 1988 and later translated into something called [Lean Software Development][3]

In it, there are two principles applicable to our situation.

*   Decide as late as possible
*   Deliver as fast as possible

To us, this means that whoever is responsible for making that plane come in from the left has not yet *decided* on a side from which the plane is to come in. The `data` sent was *partial* and is still being computed.

Thus the decision is made as late as possible, ideally after Mary has had a chance to show her work to you so that you may comment and suggest change beyond her responsibilities.

![Decide Late][4]

# Proceduralism

To decide late implies that changes may alter `data` as it is being processed and if there is any methodology in our industry that facilitates for this it is that of proceduralism.

Proceduralism involves working with a description of steps, rather than actually performing them. It means to have the output of each step be generated rather than created which may involve delegating such processes to an external medium, such as our computers.

Lets take an example.

No doubt the first thing that runs through your mind at this point is that of [Houdini][5] and its capabilities in regards to procedural generation of `data`. (If it isn&#8217;t, I envy you. You&#8217;ve got some rather delightful experiences ahead of you).

![Proceduralism][6]

In this example, Bob outputs a tetrahedron to John who rotates it 45° and sends it along to Mary who colours it red.

What all three of them have in common is how they have each *described* the steps necessary to achieve their processing. Houdini then is the one who actually performs the processing and *creates* the output.

If there is anything for us to absorb from this example it is that Bob may alter his output after John and Mary have finished processing **without either John or Mary having to re-visit any of their work.**

This is a key factor in our design and governs the majority of choices made for the Pipi Object Model and in fact those of Pipi itself.

# Output = Description

When `data` is described rather than created, we facilitate change.

But how can we apply these same practices to something as abstract and perhaps difficult to grasp as that of the result of another artist?

By now, we have established that to a pipeline in terms of a graph there are two things for us to work towards.

*   Partial outputs
*   Contracts

When output is partial, we can transmit it quickly and when both the transmitter and recipient have both agreed to on what data they will each receive &#8211; i.e. have signed a contract &#8211; the transmission can happen repeatedly without either party having to look for differences across inputs.

Lets transform the [illustration from part 1][7] into something a little more suited to our conversation.

![Pipeline Conversion][8]

There. Now we can clearly see the that each `node` is connected via a `link` and that in some cases, one `node` has multiple inputs. The plot thickens.

# Limits of Proceduralism

The notion of a describing a set of steps for the computer to process is great, but is it applicable to everything?

Can we alter the output of Bob without involving John or Mary? Yes. But can we have the output of a Storyboard department alter its output, and have that change trickle down-stream without influencing any other `node`?

# The Wolfram Computational Engine

When you ask [Siri][9] a question, your question is translated into text. The text is then sent to one or more processes, one of which may be the Wolfram Computational Engine [&#91;1&#93;][10], [&#91;2&#93;][11].

It may be possible to one day have a change in `storyboarding` trickle down-stream, and witness its repercussions interactively &#8211; just as we are with the Tetrahedron outputted by Bob, rotated by John and coloured by Mary.

Until then, lets locate our limits so that we may work within them.

# Within Limitations

![Reasonable Bounds][12]

Here is my claim.

Each `node` within this red rectangle may be condensed into a set of descriptions &#8211; just like those illustrated in Houdini above.

You may not believe me, and I don&#8217;t blame you. What goes in and what comes out of each `node` within this illustration varies greatly between one studio and the next.

In many cases, there are no contracts. In others, there are no partial outputs.

# Why are development studios different?

You may find it odd that even though talent in our industry never stays in one place for very long, best practices and a general approach to any given task may not be even partially the same across development studios.

This may have something to do with the speed at which technology shifts today. The process employed to produce the latest blockbuster is legacy as soon as the movie hits the theatres.

At this rate, how could we ever expect consistency?

# Within Reasonable Bounds

It may be possible one day for full consistency to be achieved between productions; but just as render-times has hovered around 8 hours per frame for the past 12 years [&#91;1&#93;][13] despite the colossal increase in computing power, so too may requirements be added to any achievable consistency.

Until then, lets locate our bounds so that we may work within them.

Stay tuned for part 4, thanks and see you in a bit.

xoxo,  
Marcus

 [1]: http://www.abstractfactory.io/blog/pipi-object-model-pt-2/
 [2]: http://en.wikipedia.org/wiki/Lean_manufacturing
 [3]: http://en.wikipedia.org/wiki/Lean_software_development
 [4]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/stuart_townsend_digital_painting_wip_by_melusaaste-d6aaswj.jpg
 [5]: http://www.sidefx.com/
 [6]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/proceduralism_1.png
 [7]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/3d_production_pipeline1.jpg
 [8]: https://dl.dropbox.com/s/1h5sn4o9mwhndbh/3d_production_pipeline_conversion_2.png
 [9]: https://www.apple.com/uk/ios/siri/
 [10]: https://www.wolframalpha.com/
 [11]: http://www.youtube.com/watch?v=_P9HqHVPeik
 [12]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/reasonable_bounds.png
 [13]: http://youtu.be/MA_tpeyas4o