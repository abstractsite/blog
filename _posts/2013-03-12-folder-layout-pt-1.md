---
title: Folder Layout pt. 1
author: Marcus
layout: post
permalink: /folder-layout-pt-1/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/03/folder-layout-pt-1.html
categories:
  - Theory
---
<div>
  In a perfect world, the user will never have to know that there ever was a hierarchy of files on some disk. What matters is the data and it&#8217;s level of discoverability.
</div>

<div>
</div>

<div>
  Technically though, files and folders are still the most efficient way of storing heavy data on disk and so for a tool to successfully hide the details of that implementation, great care must be taken when considering their layout. A cg production generally consists of thousands or hundreds of thousands of files, some of which are tightly related, such as sequences of images, and others which relationship is less obvious, such as which animation is using which character setups.
</div>

<div>
</div>

<div>
  That is why it is important to consider exactly what files will exist within this hierarchy and exactly how they relate to one another. Lets dive in with some examples.
</div>

<div>
</div>

<div>
  Sequences may contain shots, shots may be worked on by one or more users and on those shots users may work in one or more applications.
</div>

<div>
</div>

<div>
</div>

<table align="center" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <a href="http://1.bp.blogspot.com/-BU6-1AQqMLw/UTnNnjPaHAI/AAAAAAAAAgU/RpxQ7HPqrEY/s1600/hierarchy.jpg" imageanchor="1"><img border="0" src="http://1.bp.blogspot.com/-BU6-1AQqMLw/UTnNnjPaHAI/AAAAAAAAAgU/RpxQ7HPqrEY/s1600/hierarchy.jpg" /></a>
    </td>
  </tr>
  
  <tr>
    <td>
      Balance readability with duplicity
    </td>
  </tr>
</table>

<div>
</div>

<div>
</div>

<div>
   You may find it odd to couple sequence and shot, that seem quite obviously interconnected, with that of user and application, but later I&#8217;ll head into more details why they can come in handy in parts of the tool that deals with a users sandboxes and working spaces. The ideal layout is the one that produces the most appealing balance between readability and duplicity. In this layout, besides the logical benefits of picturing it in ones mind, practical considerations occur such as removing one shot will results in the users working directory to be deleted as well, which is what the user would come to expect.
</div>

<div>
</div>

<div>
  Consider to following hierarchy.
</div>

<div>
</div>

<div>
</div>

<div>
  <a href="http://3.bp.blogspot.com/-fYAK-KljGBE/UTnTlrPuSOI/AAAAAAAAAgs/eOg_oOD8lLM/s1600/hierarchy_userfirst.jpg" imageanchor="1"><img border="0" src="http://3.bp.blogspot.com/-fYAK-KljGBE/UTnTlrPuSOI/AAAAAAAAAgs/eOg_oOD8lLM/s1600/hierarchy_userfirst.jpg" /></a>
</div>

<div>
</div>

<div>
  In this layout, user is the host of sequences. A project is bound to have more than one user and since shots cannot exist without a sequence, and a film is nothing without shots, it is safe to say that at least one sequence will also exist and thus each sequence would get duplicated underneath each user.
</div>

<div>
</div>

<div>
  <a href="http://2.bp.blogspot.com/-4W01oY0a4H0/UTnVEu0j-KI/AAAAAAAAAg4/DVhTeqR_yys/s1600/hierarchy_userfirst_superflous.jpg" imageanchor="1"><img border="0" src="http://2.bp.blogspot.com/-4W01oY0a4H0/UTnVEu0j-KI/AAAAAAAAAg4/DVhTeqR_yys/s1600/hierarchy_userfirst_superflous.jpg" /></a>
</div>

<div>
</div>

<div>
  As you can see, &#8220;sequence 1&#8243; is repeated once for each user which may or may not be desirable. Each shot within each sequence is also duplicated, producing an exponential multitude of duplicates, thus violating our rule of balancing readability with duplicity. A potential benefit of this layout is that finding the associated sequences to a user is as easy as looking at the users folder root. However, minor filtering requirements like these there have other, better, alternatives that doesn&#8217;t depend on their physical layout on disk.
</div>

<div>
</div>

<div>
  If you look at the first hierarchy, it also produces duplicates. Underneath each shot is a folder for each user working on the shot. If a user has worked on more than one shot, that folder would have a duplicate under each one. This is where one needs to decide on which approach is better suited for which task, as there will most often exist a trade-off between.
</div>

<div>
</div>

<div>
  In summary, the hierarchical layout of files can exist in any order. Ideally the more general classes of types, such as shots and sequences, come first, followed by the more specific ones, such as images and pointcaches.
</div>

<div>
</div>