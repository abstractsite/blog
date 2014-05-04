---
title: Folder Layout pt. 3
author: Marcus
layout: post
permalink: /folder-layout-pt-3/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/05/folder-layout-pt-3.html
categories:
  - Theory
---
### A Better Way

<div>
  Wouldn&#8217;t it be great if we could avoid separating any data at all? If all data could live happily under the same roof?
</div>

<div>
</div>

<div>
  The end goal is to simplify data <b>navigation</b>. You want to be able to locate what you need as quickly as possible. As we have seen, some data may be logically paired with other data and so a hierarchical approach may seem like a good idea. Other data however provide a less rigid constraint towards its source, such as a user and his shots, and may perhaps be better suited for tagging and filtering. A user working on a shot deals with the shot &#8220;entity&#8221;, various rigs and output pointcaches supporting assets such as audio, images, notes, feedback and so on. The user does not care whether some data are stored in one location and some are not, the user only wishes to quickly retrieve the data he needs at the time he needs it whilst still being able to work on the physical files his chose application. We would like to find one unified way in which all of this is possible.
</div>

<div>
</div>

<div>
  A closer look at the previous example reveals some more superfluous use of structure.
</div>

<div>
</div>

<div>
  <a href="http://4.bp.blogspot.com/-B5RXOmRFLp0/UTn6hMh5Q_I/AAAAAAAAAiE/s00tUAno1uE/s1600/layering_data.jpg" imageanchor="1"><img border="0" src="http://4.bp.blogspot.com/-B5RXOmRFLp0/UTn6hMh5Q_I/AAAAAAAAAiE/s00tUAno1uE/s1600/layering_data.jpg" /></a>
</div>

<div>
</div>

<div>
  Some data within a cg production however have no binary data, and yet contain metadata as well as other pieces of data. Consider an asset such as the Simulation Setup for a Ladybug. The rig has no binary information related to it, it is &#8220;abstract&#8221;, yet it contains versions in which binary information are stored. Each version in turn has metadata, such as date of creation, author and changelog and so on.
</div>

<div>
</div>

<div>
</div>

<div>
</div>

<div>
  At the root, we have an item referred to as <span>Studio</span><span>. The studio contains everything related to a studio as a whole. This includes jobs, users, settings, running processes and so on.</span>
</div>

<div>
  <span><br /></span>
</div>

<div>
  <span>Each item hosts information relevant to its type. </span><span>Job</span><span> holds data relevant to a single job. This includes all sequences and shots, assets, users working on this job and related metadata such as who the client is, when the job is due, media such as storyboards, reference images and videos.</span>
</div>

<div>
  <span><br /></span>
</div>

<div>
  Moving forward, we have the <span>Asset</span><span> which contains everything related to a single asset, such as a Character. This includes models, textures, rigs, shaders and associated data and relationships to other data.</span>
</div>

<div>
  <span><br /></span>
</div>

<div>
</div>

<div>
  <span>Certain types of objects are designed to host certain other types of objects.</span>
</div>

<div>
</div>

<div>
  <a href="http://2.bp.blogspot.com/-fWsRKIqKfEg/URFpkomzIpI/AAAAAAAAAfA/u_d-HJTxuTY/s1600/effectivehierarchytraversal_hierarchyexample02.PNG" imageanchor="1"><img border="0" src="http://2.bp.blogspot.com/-fWsRKIqKfEg/URFpkomzIpI/AAAAAAAAAfA/u_d-HJTxuTY/s1600/effectivehierarchytraversal_hierarchyexample02.PNG" /></a>
</div>

<div>
  <span>In this example, the job <b>beast</b> is host of the items <b>work</b> and <b>published</b>. From a users perspective, when mining a job for resources, be it assets or which shot to get on working with next, this is all that is required at this level. On disk however, <b>beast</b> may host a multitude of items other than its resources.</span>
</div>

<div>
  <span><br /></span>
</div>

<div>
  <a href="http://3.bp.blogspot.com/--wmw4AVZL0Q/URFqKvYTYqI/AAAAAAAAAfI/NaVm5j3d7O4/s1600/effectivehierarchytraversal_hierarchyexample03.PNG" imageanchor="1"><img border="0" src="http://3.bp.blogspot.com/--wmw4AVZL0Q/URFqKvYTYqI/AAAAAAAAAfI/NaVm5j3d7O4/s1600/effectivehierarchytraversal_hierarchyexample03.PNG" /></a>
</div>

<div>
  The items <b>appdata</b> and <b>userdata</b> host application-specific data and users home directories respectively. Note the extensions. These are rather ugly too look at and would be better represented by icons other than the default windows explorer ones. Certain names also contain reserved keywords. In this case, <b>__properties__</b> host generic metadata about <b>beast</b> and <b>__settings__.ini</b> contains user editable data, as hinted towards via the .ini extension.
</div>

<div>
</div>

<div>
</div>

<div>
  The various types required to make up a studio and all of its resources can grow quite large, that&#8217;s why it is important to structure it in an as manageable form as possible.
</div>

<div>
</div>

<div>
  Firstly, lets look at some of the assumptions we can make about the users of Pipi.
</div>

<div>
</div>

<div>
  The target goal is to facilitate the creation of CG images and as such the major components can be broken down into <span>Sequences </span>and <span>Shots</span>, each shot capable of having one of more <span>Assets</span>.
</div>

<div>
</div>

<div>
  Assets include elements such as Characters, Props, Vehicles, Set Dressing objects etc. Each Asset may contain additional elements per department. I&#8217;ll bring in Bob and the Ladybug project from the previous post to aid in the explanation.
</div>

<div>
</div>

<div>
  Bob works in modeling on the hero character <b>Ladybug</b>. <b>Ladybug</b> has got several models associated with it, such as the <span>body</span>, the<span> face</span>, character-specific props such as <span>clothing</span>, a <span>wristwatch</span> and so on. Whatever model Bob eventually finishes, since Bob is in the <b>Modeling Department</b>, his published material will go under the department category <b>Modeling</b>.
</div>

<div>
</div>

<div>
  When Bob works on the body model in Maya, Bob saves his scene every now and then. Generally, Bob will only share material with other departments once he is happy with his results and so application files, such as scene versions, are stored separately from those happy results. This helps keep the database clean and minimal, whilst still allowing Bob to make as many revisions to his scene-files as he needs. This results in the following hierarchy.
</div>

<div>
</div>

<div>
  <a href="http://4.bp.blogspot.com/-mfa9g7GCqRc/UTnK-1PGT9I/AAAAAAAAAf8/oyyQA_WSigY/s1600/work_vs_publish.jpg" imageanchor="1"><img border="0" src="http://4.bp.blogspot.com/-mfa9g7GCqRc/UTnK-1PGT9I/AAAAAAAAAf8/oyyQA_WSigY/s1600/work_vs_publish.jpg" /></a>
</div>