---
title: Working in Context pt. 0
author: Marcus
layout: post
permalink: /working-in-context-pt-0/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/01/cygwin-vs-cmd-for-windows.html
categories:
  - Theory
---
Why use <a href="http://cygwin.com/" target="_blank">Cygwin</a> when windows already has a built-in terminal?

### Background 

Having an application know under which context to operate is essential to providing a truly immersive experience for the user. Whenever an action is being performed the action should happen within the context that the user is working under. Take publishing for instance. The user may be publishing an variant multiple times under the same session. It makes little sense for him to specify which asset is being published each time, the surrounding should be able to provide such information. The only information relevant for the user to specify is what has been changed since the last publish. Saving is another example. Whenever the user saves a working file, they should only have one place to go and there should be no mistake as to where that place is. This helps the user with encapsulating parts of his work that relate to a certain building-block of the film. It can also be extended to providing sandboxed areas under each shot or variant** **for whenever the user feels the need to experiment.

### Approaches 

So how can we inform the application of the context? Two ways, you can either start the application and then tell it about the context, or you can tell the parent of the application, the operating system, about the context and boot up the application under that context. The application can then ask the os for information it does not already know. It also allows us to have multiple applications share the same context. Say for instance you wish to work on **shot 23**. You set it once, and boot up Maya, Mari and Nuke to work on various aspects of the shot simultaneously. Since the context exists outside the scope of each application, each application may ask the higher source for information and may modify that source collectively, effectively staying synchronized with each other and may even allow a level of communication between them.

I chose to support the latter of the two approaches.

### Implementation 

How do we inform the os of the context? One word, &#8220;environment variables&#8221;. The os has a common area for storing both temporary and persistent metadata. The metadata may be altered either globally to affect everything always, or per instance of say a terminal.

A terminal, such as the built in Cmd.exe is booted up within this context (read &#8220;set of environment variables&#8221;) and stores a copy of it internally. Whenever we make any change to the context, only this instance knows about it. That means that once we boot up Maya from within this terminal, Maya will also know about it, but the next terminal you boot up will not. (unless you boot it up from within this terminal). This lets us encapsulate modifications to the higher source (the os) whilst still allowing us to keep multiple applications living under the same encapsulation (namespace).

### Reasoning

Cmd.exe has it&#8217;s drawbacks however, which is why I chose Cygwin. The main reasons being:

**Cross-platform**  
Considering the pipeline should work across any platform, it makes sense to conform windows to an otherwise working standard, rather than the other way around. Additionally, knowledge gained from using cygwin translates transparently to other operating systems such as Linux and OSX as they both have access to **bash**, making any future transition effortless. Additionally, many studios have already adopted Linux for their productions. Using Cygwin thus would allow us to benefit from an existing knowledge pool whilst also facilitating the transition between studios for artists.

**Built-in apps**   
Cygwin, like linux, allow for the use of editors within the terminal, mainly Text Editors. That allows you to quickly modify files that don&#8217;t need the feature-richness of an external app.

In addition to:

**Command line scripting**  
Custom commands can be made by both user and administrator to allow for easy access to common data such as project and current shot being worked on.

**Per-project environment variables**  
Users can run a bash-script, setting an environment variable PROJECT to correspond to under which project is currently being worked on. PROJECT can then delegate paths relevant to this project, such as which bash-script is being used to launch the correct version of applications such as Maya.

The latter ones are possible using Cmd.exe as well and preferring one over the other however is a matter of style.

### Headaches

One of the thing about Cygwin that separates it from being native is that it uses its own directory scheme. C:\ does not exist and is instead kept under a directory like /cygdrive/c/. This may seem silly at first but I&#8217;m guessing their reasoning is the same as mine. Facing the choice between either conforming all of linux functionality to work under windows paths, or altering windows to work with all of linux, I&#8217;m guessing it was the right thing to do.