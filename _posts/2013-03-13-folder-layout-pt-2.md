---
title: Folder Layout pt. 2
author: Marcus
layout: post
permalink: /folder-layout-pt-2/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/03/folder-layout-pt-2.html
categories:
  - Theory
---
### Keeping your socks in your boots

It may be very beneficial to ensure that all data related to any other data are kept together. Like sequences can contain shots, a shot may contain more than simply the users working directories, such as its description, length, padding, camera information, frame rate, media such as video-references for animators or audio for lipsync. <div>
</div>

<div>
  Tools already exist for this purpose. Some examples I already mentioned in the previous post but I&#8217;ll repeat them here for completeness. 
</div>

<div>
</div>

<div>
  <a href="http://www.shotgunsoftware.com/products/" target="_blank">Shotgun</a>, <a href="http://www.ftrack.com/" target="_blank">FTrack</a>, <a href="http://www.southpawtech.com/" target="_blank">Tactic</a>. 
</div>

<div>
</div>

<div>
  I really recommend checking those out, they&#8217;ve got videos showing some fundamental functionality and they are used today by hundreds of studios. I&#8217;ll refer to these tools as Offline Asset Management, or OFAM for short. They provide two major concepts rolled into one &#8211; tracking assets and shots along with assigning tasks and maintaining schedules of projects. The tracking part enable users to associate data that would otherwise be difficult to associate via a simple hierarchy of files and folders, along with the ability to add links other than simple hierarchical ones, such as their relationships to users or even other data in the database. They do this by separating the binary data from its related information.
</div>

<div>
</div>

<table align="center" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <a href="http://4.bp.blogspot.com/-3jlnDscUxqQ/UToNL8qidpI/AAAAAAAAAi4/UWDiQ_5pqnQ/s1600/separate_binaryandmetadata.jpg" imageanchor="1"><img border="0" src="http://4.bp.blogspot.com/-3jlnDscUxqQ/UToNL8qidpI/AAAAAAAAAi4/UWDiQ_5pqnQ/s1600/separate_binaryandmetadata.jpg" /></a>
    </td>
  </tr>
  
  <tr>
    <td>
      Separating binary data from related information
    </td>
  </tr>
</table>

<div>
</div>

<div>
  The caveat of this approach however is that it is external to the files they augment. Augmenting data, aka Metadata, is stored separately from their associated assets, shots and sequences in a database table such as SQL.
</div>

<div>
</div>

<div>
  This means that whenever a change happens on one side, the other side needs to get updated somehow. This introduces the concept of syncing and is generally handled like this &#8211; a change in Maya, say a publish of a character, will trigger an event (referred to as a callback) which performs the corresponding action on the server. Data generally only travels in this one direction as any change in any of an objects metadata, such as shot description, has no relevance within, in this case, Maya (or does it? I&#8217;ll dive into this more later!). For example, a new asset is created from Maya. Maya triggers a callback and the equivalent asset is created within the OFAM.
</div>

<div>
</div>

<table align="center" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <a href="http://4.bp.blogspot.com/-YupbBKnxmX0/UTnmD70boCI/AAAAAAAAAhY/PFdskHO4NCs/s1600/duplicate_actions.jpg" imageanchor="1"><img border="0" src="http://4.bp.blogspot.com/-YupbBKnxmX0/UTnmD70boCI/AAAAAAAAAhY/PFdskHO4NCs/s1600/duplicate_actions.jpg" /></a>
    </td>
  </tr>
  
  <tr>
    <td>
      Psuedo-code of mirrored command
    </td>
  </tr>
</table>

<div>
</div>

<div>
  Some data will remain unique on either end, such as the binary scene file, while other data, such as camera information, will overlap and cause duplicity.
</div>

<div>
</div>

<div>
</div>

<table align="center" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <a href="http://2.bp.blogspot.com/-Dex6zSOcE6Y/UTnj_-YB_VI/AAAAAAAAAhQ/EZsjrklMUKs/s1600/complementing_data.jpg" imageanchor="1"><img border="0" src="http://2.bp.blogspot.com/-Dex6zSOcE6Y/UTnj_-YB_VI/AAAAAAAAAhQ/EZsjrklMUKs/s1600/complementing_data.jpg" /></a>
    </td>
  </tr>
  
  <tr>
    <td>
      Overlapping data means duplicated data
    </td>
  </tr>
</table>

<div>
</div>

<div>
  In order to store the camera information of a shot, the shot itself and all of its related hierarchy must exist within the database, if only to host that information, so that users have a way to associate it and to search for it. However the hierarchy must also exist to host the binary files.
</div>

<div>
</div>

<div>
  While the overlap is very small in terms of megabytes on disk, we aren&#8217;t concerned with disk space issues. What matters is the information they represent and our ability to efficiently find it.
</div>

<div>
</div>

<div>
  The overlap applies to both shots, sequences and assets and also any media associated. Some media are only accessible via the OFAM, such as a reference material, thumbnails, playblasts etc., but must yet be stored in binary form somewhere on disk. This means that you end up having an additional hierarchy of binary files, besides the original binary files themselves.
</div>

<div>
</div>

<table align="center" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <a href="http://1.bp.blogspot.com/-VANv3WkqKHY/UTnnudPkUaI/AAAAAAAAAhg/2KLcJEiFi8U/s1600/complementing_data_superfluous.jpg" imageanchor="1"><img border="0" src="http://1.bp.blogspot.com/-VANv3WkqKHY/UTnnudPkUaI/AAAAAAAAAhg/2KLcJEiFi8U/s1600/complementing_data_superfluous.jpg" /></a>
    </td>
  </tr>
  
  <tr>
    <td>
      Superfluous complementing data
    </td>
  </tr>
</table>

<div>
</div>