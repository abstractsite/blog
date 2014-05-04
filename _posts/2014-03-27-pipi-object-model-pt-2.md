---
title: Pipi Object Model pt. 2
author: Marcus
layout: post
permalink: /pipi-object-model-pt-2/
mytory_md_path:
  - 
categories:
  - Uncategorized
---
> In part 1 we uncovered some of the features of our neural nature and how these may be used to our advantage in absorbing and understanding new information. In this part, we&#8217;ll make use of these tools to try and understand how thinking about a pipeline as a graph can be helpful. 

# Data

You&#8217;ll remember from [part 1][1] our notion of `data`

Well, `data` is at the heart of digital asset management. Without it, there would be nothing to manage.

So, lets establish some common ground on what exactly `data` is.

# The location data

<pre class="brush: plain; title: ; notranslate" title="">/server/project/sequence/shot/instance/cache/data.abc</pre>

What I have bestowed upon you is indeed the location of data. This particular set of data resides on a server somewhere and consists of the `cache` for `instance` of `shot` of `sequence` of `project`.

# Data Hierarchy

That&#8217;s right. Data in our domain is all about hierarchies. Files *within* a hierarchy to be more precise and all of our tools for producing film, games and tv and web content and so on deal with files. So for now, lets determine that a `file` = `data` = `file`

Referring back to our notion of a pipeline, where `data` travels, transforms and arrives; what we are really saying is that a `file` travels, transforms and arrives.

# A Hero&#8217;s Journey

But where does the `file` go, and what exactly is its transformation?

Lets refer yet again back to [part 1][1] where our modeler, Bob, transformed *artwork* into a *3d model* and sent it back out.

What really happened was that Bob was given a `jpeg` and produced an `obj`.

# Data Transformation

Now lets assume Bob is a strictly by the book; we may then refer to Bobs input as a *pre-condition* and his output as *post-condition*.

For Bob to perform his service, the incoming `file` will have to be served in accordance with a previously agreed-to contract &#8211; in this case, the input will have to arrive in the form of a `jpeg`. In return, Bob has agreed to output his `file` as an `obj`.

If the `file` isn&#8217;t delivered to Bob in the form of a `jpeg` then Bob will be unable to guarantee the delivery of `obj`; if at all.

This notion is referred to as [Design by contract][2] and is the same methodology applied to the design of an [API][3] and indeed, whether directly or indirectly, universal across pipeline design in all industries.

# Data Tracking

Now that Bob has produced an output, we may locate his output with that of a `path` and a `path` may come in multiple flavours.

<pre class="brush: plain; title: ; notranslate" title="">/server/project01/hero/bobs_model.obj</pre>

Bob is a Maya artist and as such the transformation took place within this application.

<pre class="brush: plain; title: ; notranslate" title="">|Hero|L_arm_GRP|L_elbow_PLY</pre>

Additionally, the task given to Bob is located within an Asana project.

<pre class="brush: plain; title: ; notranslate" title="">https://app.asana.com/0/846062819581/1050536261774</pre>

# Conflict

But wait.. Didn&#8217;t we just declare that all `data` = `file` = `data`?

If the previous locations are indeed locations to data, we will have to expand on our understanding of what `data` really means. Let&#8217;s start by establishing some common ground on what is exactly that we need our pipeline to do.

# Common Ground

You&#8217;ll recall from [part 1][1] that we defined our goal for Pipi as<div class=sidenote>Output may be altered up-stream and sent down-stream with little or no effort.</div> 

But what does that mean, really?

Imagine Bob.

Bob finished and delivered his output a while ago and it is now being transformed by another artist.

During transformation, it occurs to the recipient that:

> &#8220;We need change&#8221;

![Data Upstream][4]

`data` was never designed to be passed up-stream. Bob signed a contract clearly stating that he would receive `jpeg` and output `obj`. The recipient artist on the other hand receives `obj` and outputs something else.

What is it exactly that Bob will receive? Does anyone know?

# Acyclic Failure

In [part 1][1], I briefly touched upon the model of a graph, more specifically a Directed Acyclic Graph and that it may be helpful to us in thinking about a pipeline.<div class=sidenote>The DAG refers to a processing element as a \`vertex\` and a connection as an \`edge\`. These keywords already occupy space in our brains relating to 3d geometry so I will instead be refer to these by the more familiar terms \`node\` and \`link\` respectively.</div> 

It would seem as though this is where this model falls apart.

The DAG is designed so that each `node` must finish its computation prior to outputting any new information &#8211; so how can information flow from one artist to the next if at any point in time that information may reverse direction?

In an ideal world, Bob would instantly output no more and no less that what is required from him but unfortunately for Bob we live in the real world, which is messy, and in our messy real world we must expect the unexpected. We must plan for change.

# Responding to Change

What we have just witnessed is called the *waterfall model*.

![Waterfall model][5]

You may notice its correlation to the terms I&#8217;ve been using so far &#8211; `flow`, `up-stream` and `down-stream` and indeed that is no coincidence.

The waterfall model was designed for an ideal world &#8211; but as just discussed, our world is far from ideal.

# The Ideal Graph

How do you design a graph capable of passing data up-stream?

The answer is, you don&#8217;t.

In February of 2001, a group of 17 developers got together to form [The Agile Manifesto][6]. In this manifesto there were four values, one of which is of particular interest to us.

*   **Responding to change** over Following a plan

# An Agile Graph

Let&#8217;s have a look at how we can re-shape our thinking about a graph for production with the agile manifesto in mind.

Lets define a `branch` as a sequence of `nodes`. In order for change to find its place within a graph, we must reduce the time taken to get from input to output in any `branch` of our graph; in short, less latency means more room for change.

Traditionally (i.e. in the waterfall-model), the output of each `branch` must be completed prior to being sent back out. In a digital asset management pipeline however this may not be the most efficient way to go.

Consider Bobs recipient, John.

John is dependent on the output of Bob and John has signed a contract specifying that he will receive an `obj` and output an `mb`.

In a waterfall-enabled environment, John would not be receiving any information until the output of Bob is final.

But as we know, *final* is but a mirage.

What we would like to have happen, is for Bob to output *partially finished* information while *still processing*, so that John could begin his processing as soon as possible.<div class=sidenote>We want \*partially finished\* information while \*still processing\*</div> 

# The Holy Grail

> [Working with a pipeline is like] rebuilding a plane mid-flight &#8211; Steve Lavietes of Imageworks from SIGGRAPH University 2013 

This is where pipelines get their name for being colossal, ever-changing and hard-to-manage. This is where pipelines, and their architects, are truly put to the test.

In the the next part, we&#8217;ll dissect this last statement further and see how and if a pipeline really is all that colossal.

Stay tuned, thanks and see you in a bit.

Marcus

Links  
- [part 1][1]  
- [Directed Acyclic Graph][7]  
- [Waterfall model][5]  
- [Data Upstream][4]  
- [Pipeline illustration][8]  
- [API][3]  
- [Design by contract][2]  
- [URL UML][9]  
- [Uniform Resource Locator][10]  
- [Object Aggregation][11]  
- [The Agile Manifesto][6]

 [1]: http://www.abstractfactory.io/blog/pipi-object-model-pt-1/
 [2]: http://en.wikipedia.org/wiki/Design_by_contract
 [3]: http://en.wikipedia.org/wiki/Application_programming_interface
 [4]: https://dl.dropbox.com/s/hmp7t97fm82okwn/data_up-stream.png
 [5]: http://upload.wikimedia.org/wikipedia/commons/thumb/e/e2/Waterfall_model.svg/350px-Waterfall_model.svg.png
 [6]: http://agilemanifesto.org/
 [7]: http://en.wikipedia.org/wiki/Directed_acyclic_graph
 [8]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/3d_production_pipeline1.jpg
 [9]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/02/url-class1.png
 [10]: http://en.wikipedia.org/wiki/Uniform_resource_locator
 [11]: http://www.abstractfactory.io/blog/wp-content/uploads/2014/03/20140302_objectAggregation.png