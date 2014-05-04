---
title: Working in Context pt. 2
author: Marcus
layout: post
permalink: /working-in-context-pt-2/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/01/working-in-context-pt-2.html
categories:
  - Theory
---
So how would you let your application know about the context? Well, there are a few ways. The most convenient way might be to try and find a common ground of communication between you and the application. A place where both you and the application could read and write to

### Environment Variables

In most operating systems there is the concept of <a href="http://en.wikipedia.org/wiki/Environment_variable" target="_blank">environment variables</a>. A common-ground for all applications on your computer, most of which will only read from it but some who also writes to it. You can think of it as a file on disk that everything accesses whenever the user stores a setting or an application requests one. In programming terms, it can be thought of as a <a href="http://en.wikipedia.org/wiki/Singleton_pattern" target="_blank">singleton </a>or <a href="http://en.wikipedia.org/wiki/Global_variable" target="_blank">global variable</a>.

So how does one access the environment? Well, it depends on your point of entry.

From the command line in Windows 7, you can go 
<pre>>>> set // Print all environment variables<br />PROCESSOR_LEVEL=6<br />PROCESSOR_REVISION=3a09<br />ProgramData=C:\ProgramData<br />ProgramFiles=C:\Program Files<br />ProgramFiles(x86)=C:\Program Files (x86)<br />...<br /><br />>>> set windir // Print a single variable<br />windir=C:\Windows<br /><br />>>> set myVariable=MyValue // Create a new variable and print it<br />>>> set myVariable<br />myVariable=MyValue<br /></pre>

And on Both Mac and Linux\Ubuntu using bash, you can go 
<pre>>>> env // Print all environment variables<br />XDG_CURRENT_DESKTOP=Unity<br />LESSCLOSE=/usr/bin/lesspipe %s %s<br />LC_TIME=en_GB.UTF-8<br />COLORTERM=gnome-terminal<br />XAUTHORITY=/home/marcus/.Xauthority<br />LC_NAME=en_GB.UTF-8<br />_=/usr/bin/env<br />...<br /><br />>>> printenv XDG_CURRENT_DESKTOP // Print a single variable<br />Unity<br /><br />>>> export myVariable=MyValue // Create a new variable and print it<br />>>> printenv myVariable<br />MyValue<br /></pre>

We, however, are mainly interested in accessing it via Python 
<pre>>>> import os<br />>>> for key, value in os.environ.iteritems():<br />>>>     print "%s=%s" % (key, value) // Print all environment variables<br />XDG_CURRENT_DESKTOP=Unity<br />LESSCLOSE=/usr/bin/lesspipe %s %s<br />LC_TIME=en_GB.UTF-8<br />COLORTERM=gnome-terminal<br />XAUTHORITY=/home/marcus/.Xauthority<br />LC_NAME=en_GB.UTF-8<br />_=/usr/bin/env<br />...<br /><br />>>> os.environ['MyVariable'] = MyValue // Create a new variable and print it<br />>>> print os.environ['MyVariable']<br />MyValue<br /></pre>

One variable you might already be familiar with is PATH. Which is, according to wiki.. *&#8220;..a list of directory paths. When the user types a command without providing the full path, this list is checked if it contains a path that leads to the command.&#8221;* You usually store executables that you would like to run from a command line of sorts.

Another useful and common one is the PYTHONPATH. This is a variable which python looks for when determining which paths to use when searching for modules during import.

So, cmd.exe uses PATH to determine what executables are available and python uses PYTHONPATH. How about we make our own dependency? Couldn&#8217;t we specify a CurrentProject variable that our library could use to determine which project we are in, in addition to Maya, Nuke, or any other program that might like to know about it? In this sense, CurrentProject is a global variable, accessible by everything that is run as a child of the OS.

Global is usually not the answer, however, but there is one thing that helps us with compartmentalization. Any time you open an application that needs the environment in any way, the environment is **copied** in to the running process. This means that modifying the environment from inside a child process is merely modifying it&#8217;s own copy of the environment. It&#8217;s own duplicate. You can think of this as a child process *inheriting* from its parent process.

This can be both a blessing and a curse. In some cases, it would be great to modify a variable and have all applications know about it so that they can update accordingly. But there are better ways around that. For instance, whenever a change occurs, a signal could be emitted to dependent processes to update accordingly. That way, not only can you control the flow of updates, but it also helps in keeping things tidy.

### What&#8217;s next

So, we&#8217;d like to modify our environment to store information about the context and then have Maya et al. make use of it. How do we go about doing this?

#### The terminal

Via the terminal, you can read the file system, create and edit files, folders. You can also modify the environment. This, in addition to the fact that the terminal contains a full copy of all environment variables, means that we can edit the environment inside the terminal and then start an application from it. This would make the terminal a child of the OS, and the application a child of the terminal. The OS would maintain it&#8217;s own original of the environment, the terminal would contain a modified version and then this modified version would get passed along to Maya (which, in turn, would then make another duplicate of this environment). In fact, we could launch several processes via the terminal and each one would get the same modified copy of the environment from the parent, our terminal.

o Windows  
    o Terminal  
        o <span>Maya</span>  
        o <span>Nuke</span>  
        o <span>Mari</span>

Each level of this hierarchy is an opportunity to modify the environment, which means that we could separate modifications into groups related to the context in which it is getting modified. For example, the operating system could assign variables related to the overall operation of every application, independent of the user. The terminal then lets the user add to that via custom commands, such as setting the current project. Maya would then have a final copy with all of the information that it needs to operate.

But wait, there&#8217;s more! In addition to these three levels of updating our environment, it can in fact happen at a few more levels.

o Boot  
    o Windows  
        o Login (per user)  
            o Launch Terminal (per terminal)  
                o Custom Commands  
                    o Per Project  
                        o Per Asset  
                            o <span>Maya</span>  
                            o <span>Nuke</span>  
                            o <span>Mari</span>

As you can see, we can assign each of these level a responsibility and have a very dynamic way of interacting with our applications. Letting them know exactly what is going on with very little effort.

In the next part, I&#8217;ll go through implementation and some of the problems I encountered along this path. Such as how to work around the fact that a process cannot edit it&#8217;s parent environment.