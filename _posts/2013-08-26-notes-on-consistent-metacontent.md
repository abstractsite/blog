---
title: Notes on.. Consistent Metacontent
author: Marcus
layout: post
permalink: /notes-on-consistent-metacontent/
categories:
  - Notes On
---
> This article touches upon generalising the term metadata and metacontent so as to be useful in everyday life.

**What does meta[[1][1]] mean?**  
1. From [Wiktionary][2] *&#8220;Pertaining to a level above or beyond.&#8221;*

**What is Content?**  
1. A collection of data.

> Metacontent is a collection of data about data or a collection of data.

**What is Data?**  
1. From [Wikipedia][3] *&#8220;Values of qualitative or quantitative variables, belonging to a set of items.&#8221;*

**What is the difference between metacontent and metadata?**  
Metadata refers to data about data or content, whilst metacontent refers to content about data or content.

E.g. Your **age** is metadata whilst a **picture of you** is metacontent.

Note: Both data and content are fuzzy, there are no absolutes. Your age could also be interpreted as content as it includes two or more numbers, each of which has a shape, history and meaning.

### Store

How do you store metacontent? For this, there is the Open Metadata specification.

### Rules

Introducing a specification, Open Metadata, governed by the following set of rules, based on [Towards a Theory of Meta-content][4] by R.V.Guha

<pre>1. The representation, manipulation and storage of meta-content should not be 
tied to that of the content it describes.

2. The metacontent language should be very expressive. This means that is 
should support referencing (cross-channel, user, time etc.) as well as many 
types of data formats,  including text, images, video, key/value pairs etc.

3. The authoring and publication of meta-content should be separable from its
consumption.

4. The metacontent language should have reflective abilities. It should be 
possible, from within the language, to view metacontent itself as content 
and thus be combined into hierarchies.

5. It should be possible to aggregate two or more channels into a single 
channel or into a channel of channels.</pre>

### Implementation

Metadata/content is stored as files underneath parent folder.

<pre>/parent/__channel1__.txt/text.txt
/parent/__channel2__.jpg/some_image.jpg</pre>

This allows for any type of format to be stored, thus fulfilling both **requirement nr 1 and 2**. The alternative to this would be to store metadata within an existing file-format, such as Autodesk Maya&#8217;s .ma ASCII file. Thus limiting what you can store (ASCII only) and also its consistency with other formats (other file-formats may not be text-based, but binary).

Reading and writing of metacontent is separated via the API and more so via the user interfaces that build upon them. Similar to how Acrobat comes with a more limited version called Reader, separating the authoring process from the consumption process. This covers **requirement nr 3**.

E.g. we could store a picture of you under:

<pre>/you/__images__.jpg/picture_of_you.jpg</pre>

\_\_images\_\_.jpg is a folder. The double underscores signifying that a set of data is contained within, this is referred to as a channel or stream of data. We could then nest another set of images within this channel, fulfilling **requirement nr. 4:**

<pre>/you/__images__.jpg/__moreimages__.jpg/another_picture_of_you.jpg</pre>

Within text-based channels it is possible to refer to neighbouring channels via the reference operator (@), thus fulfilling another aspect of **requirement nr 4.**

Utilising the reference operator, a separate channel may be constructed that only references other channels, and thus provides a composite channel. Useful when providing an additional overview channel to a very large amount of metadata. Thus fulfilling **requirement nr 5.**

Additionally, all metadata could be stored under a hidden *.metacontent* folder, thus alleviating the need to deal with the hidden-property of files when reading/writing.

<pre>/folder/.metacontent/__referenceImages__.jpg/image1.jpg
/folder/.metacontent/__referenceImages__.jpg/image2.jpg
/folder/.metacontent/__documentation__.txt/1_intro.txt
/folder/.metacontent/__documentation__.txt/2_high-level-overview.txt
/folder/.metacontent/__documentation__.txt/3_api-documentation
/folder/.metacontent/__properties__.json/properties.json</pre>

### Type

The file-format contained within any given channel is singularly defined by the channel&#8217;s extension.

<pre>/folder/.metacontent/__imagechannel__.jpg/all.jpg
/folder/.metacontent/__imagechannel__.jpg/images.jpg
/folder/.metacontent/__imagechannel__.jpg/are.jpg
/folder/.metacontent/__imagechannel__.jpg/jpeg.jpg</pre>

### Cons

What are the disadvantages to this approach when compared with databases?

1.  Performance. Data must be accessed via file-system mechanisms which aren&#8217;t as fast as say a database query.
2.  Large hierarchies that must be maintained.

### Pros

What are the advantages to this approach, compared to databases?

1.  No separation of data means no synchronization and no duplication or data.
2.  Consistency. All formats and types kept together.
3.  Logical. The file-system maps well to how we perceive the world around us. (The ball is in the box, the box is in the room, etc.)

<pre>References
<a href="http://downlode.org/Etext/MCF/towards_a_theory_of_metacontent.html">http://downlode.org/Etext/MCF/towards_a_theory_of_metacontent.html</a>
<a href="http://www.w3.org/RDF/">http://www.w3.org/RDF/</a>
<a href="http://en.wikipedia.org/wiki/Data">http://en.wikipedia.org/wiki/Data</a>
<a href="http://en.wiktionary.org/wiki/meta-">http://en.wiktionary.org/wiki/meta-</a></pre>

 [1]: http://en.wikipedia.org/wiki/Meta
 [2]: http://en.wiktionary.org/wiki/meta-
 [3]: http://en.wikipedia.org/wiki/Data
 [4]: http://downlode.org/Etext/MCF/towards_a_theory_of_metacontent.html