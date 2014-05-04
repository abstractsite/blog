---
title: Notes on.. A Facebook Wall for Production
author: Marcus
layout: post
permalink: /notes-on-a-facebook-wall-for-production/
categories:
  - Notes On
---
> Considering how such a feature of tracking ones history could be useful in a production environment.

Of course, it wouldn&#8217;t look anything like a the Facebook wall, it would be closer related to a dependency graph interface such as Nuke or Houdini, but the benefits would remain the same.

# Features

*   See where you started (that day, that year, from the beginning)
*   See what you have done
*   See what has been done by what you have done (node graph)

E.g. Trigger a playblast from Maya  
Nodes = (user) -> [maya] -> [send to queue] -> [playblast] -> [relocate] -> [notify user]  
1. The middle section could be bundled-up into a compound node for easier illustration.  
2. The compound could be exploded to expose inner workings.

# Why

*   Overview of what you do
*   Management (cancel/inspect) what you do
*   Build custom compounds

# Behavior

*   Actions completed are greyed out/hidden
*   Actions in progress are colored/outlined
*   Actions in the future are editable

# History

1.  User starts working
2.  User launches Maya
3.  User saves work (compound)
4.  User saves work (compound)
5.  User saves work (compound)
6.  User commits playblast (compound)
7.  User returns to old version
8.  &#8230;

# Relationships

*   From User
*   Current playblast operation is connected
*   Current caching operation is connected
*   Users workstation can be spotted
*   Users deskbuddies can be spotted

The user has metadata, such as phone number  
The playblast has options and metadata, such as framerange and ETA  
The caching has it too  
&#8230;