---
title: What does a Pipeline actually do?
author: Marcus
layout: post
permalink: /what-does-a-pipeline-actually-do/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/01/what-does-pipeline-actually-do.html
categories:
  - Theory
---
During the development of my approach to a pipeline, I found myself digging deeper into what it actually is I&#8217;m trying to do. Turns out the word Pipeline is heavily overloaded and may be broken down into two parts; <span>Workflow</span> and <span>Organization.</span>

Workflow deals with simplifying tasks, such as how to get this 200 pound gorilla on screen before the deadline, and Organization deals with how data travels between artists during production, such as how the character setup artists deals with updating the gorilla model.

*Simplifying Organization*

Organization may be broken down further into two additional parts; <span>Production Management</span> and <span>Asset Management</span>. Managing Production is the art of keeping your artists in sync with the needs of production. It involves handing them the information they need in order to do their jobs, such as tasks, feedback and a deadline. It is in control of how **<u>social</u>** data flows between artists and production.

There are several products on the market today that deals with this aspect of the pipeline exclusively, namely <a href="http://www.shotgunsoftware.com/products/" target="_blank">Shotgun</a>, <a href="http://www.ftrack.com/" target="_blank">FTrack </a>and <a href="http://www.southpawtech.com/" target="_blank">Tactic</a>

*Requirements*  
*  
*What is required by a Production Management system is rather similar across industries and have a large foothold in history as to how it should be approached. Asset Management however has not.

Asset Management is the art of directing how **<u>binary</u> **data flows between artists, such as how the gorilla model will get from the modeler to the rigger. Note the difference between this and what is going on in the workflow domain. Workflow governs **how artists perform actions **whereas Organization is **what the actions actually do**. Lets take an example

A modeler has finished his first iteration of the gorilla model and wishes to share it with the rigger. The modeler hits &#8220;Publish&#8221; and writes down a comment. When finished, the rigger opens up the Library and Loads the model.

This is all fine and dandy, but what is actually going on under the hood? What does &#8220;sharing&#8221; mean in terms of 1s and 0s? What the modeler did was part of the workflow and what actually happened is organizational. As you might suspect, the line I&#8217;m drawing between workflow and organization if close to that of Interface versus Implementation. The interface is very similar across various cg studios, artists will always require a way of sharing their work with others, but the implementation however might not be. Sharing might happen using git commits via a central server in Malaysia or it may happen via exchanging floppy disk in the kitchen during lunch.

To sum up, here is the pipeline hierarchy of responsibility

<span>/pipeline</span>  
             <span>/organization</span>  
                                <span>/production management</span>  
                                <span>/asset management</span>  
            <span>/workflow</span>  
                            <span>/tools</span>  
                            <span>/best practices</span>

I&#8217;ll touch on workflow more once I&#8217;ve started implementing it. Now onto how I approached the interface and implementation of an Asset Management system. Pipi is the name. It &#8220;*acts as a bridge between artists in order to aid collaboration*&#8220;

<div>
  <a href="http://1.bp.blogspot.com/-EUvDcxW9fA0/UQL7gw0HQzI/AAAAAAAAAeY/JVC-yK2nURw/s1600/pipi_overview.png" imageanchor="1"><img border="0" height="100" src="http://1.bp.blogspot.com/-EUvDcxW9fA0/UQL7gw0HQzI/AAAAAAAAAeY/JVC-yK2nURw/s320/pipi_overview.png" width="320" /></a>
</div>

Note that there is a subtle difference between simplifying &#8220;collaboration&#8221; and simplifying &#8220;organization&#8221;. Organization helps Collaboration, not the other way around, and the duties of any pipeline should be to simplify organization, and as such, aid in collaboration. Asset management is one of the components of a pipeline that

The duties of Pipi can be broken down into two major components. It..  
    &#8211; ..manages files and folders  
    &#8211; ..presents relevant information

And it does so via a set of custom-built tools.

I will now go over each of those in more detail.

### Managing files

To help users manage files, a separation between \`working\` and \`published\` files are introduced.

Let&#8217;s use the example of The Ladybug. The Ladybug is a hypotetical 10 second animation produced by 10 people in a matter of 10 months. Once the script has been written and the crew picked out, the first order of business is to start creating material.

#### Working

<pre>    "Hey Bob, can you start working on the ladybug model?"</pre>

Upon this request, the artist enters a working mode. He opens up the designated software for the Ladybug project, Maya, and starts saving files to his private user directory located under the asset. (more on what an asset is later) 
<pre>    /studio/assets/LadyBug/bob/bobs_ladybugmodel_v001.mb</pre>

As time goes, Bob will start gathering quite a large amount of files. That&#8217;s fine, Bob is currently working within his own sandboxed area and as long as Bob doesn&#8217;t have any problems with it, neither does anyone else.

Once Bob reaches v120, he decides to share his work with his co-workers. After all, Vicky has been expecting it for her Character Setup of the Ladybug.

#### Publishing

Bob commits his work to the central repository of files, where anyone can access it. By using tools provided by Pipi, Pipi will ensure that the file lands in a common area with a common name syntax. It will also tag it some extra information such as who it is from, when it was committed and any comments that the author has provided.

*This is referred to as Publishing*

Any artist who wishes to share his or her work must first **Publish **the material they wish to share. This ensures that all material in the common area align with each other in terms of the various conditions they must fulfill. 
<pre>    Error: Could not publish. Reason: Normals Locked!<br /></pre>

Uh uh. Seems Bob is having some trouble with his publish. It seems that before Bob may submit his work to the common area, he must first make sure that the normals on his models are unlocked. By fulfilling this criteria  Bob will ensure that his work live up to the standards of every other model in the common area.

*This critera is referred to as a Post-Condition*

All models in the common area are guaranteed to live up to a set of post-conditions just like this one. The same applies assets of any species.

#### What is an Asset?

A film may be considered to be divided up into a set of Sequences and Shots, and each shot may contain one or more Assets.

*An Asset is a building-block of a film*

It represents an entity, such as a character or a piece of furniture, along with information about that entity, such as its name, description, author and so on. All of it encapsulated into a unified whole, called an Asset.

Assets are at the very heart of Pipi. In fact: A shot can only consist of Assets

This means that before an animator, for instance, can make use of your beautifully sculpted model, it must first go through the rigorous set of tests and fulfill each of the post-conditions set for its species.

This enables artists to know what to expect when loading new material from Pipi and helps keep things neat.