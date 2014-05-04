---
title: '&#8220;Everything is a file&#8221;'
author: Marcus
layout: post
permalink: /everything-is-a-file/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/07/everything-is-file.html
categories:
  - Theory
---
One of the defining factors about UNIX operating systems is it&#8217;s use of files for everything<sup>[1]</sup>. Documents are files, images are files, but also processes and hardware such as the running session of Maya and your keyboard.

### Universal Namespace

Accessing an image on Linux can be done by traversing to the directory in which that image resides and then read or write to it. Accessing a process can also be done by traversing to the directory in which the process resides and then reading or writing to it.

<pre>/home/image.png
/proc/photoshop</pre>

Now, clearly your brand new floppy disk drive is not a file. It&#8217;s a collection of components physically soldered together in some factory. What Unix provides however is a unified mechanism for accessing the hardware in your PC and the documents on file-system. Lets look at an example.Reading from a text document involves launching Notepad and giving it the file you wish to read. Writing to it involves much the same process, only this time Notepad is giving the filesystem something. Accessing the contents of your Shadows of Darkness Disk 6 involves in much the same way handing the file over to the appropriate reading mechanism and overwriting in turn means giving your Full Throttle Disk 54 to the writing mechanism of your original diskette.

<pre>Makes sense? Of course it does. Lets move on.</pre>

### What about Pipi?

Pipi likes this way of handling data. In addition to every asset that you create being a file, so is its users and running processes. So is its metadata and so are its events. This ensures that we can completely bundle components together without worrying about handles to external entities such as database entries or memory addresses. Moving an asset to another project? No problem, anything related to that asset is safely stored within its own hierarchy of files and folders.

> &#8220;Pipi likes this way of handling data&#8221;

### The Unix &#8220;Everything is a File&#8221; isn&#8217;t great with metadata

This is true. In Linux, the floppy disk is a mere file and a file-system only allows so much metadata to be appended to it. The date at which it was modified, its author and perhaps even a tag if you&#8217;re lucky. This forces developers to use an alternative approach for its data about data, such as XMP information in photographs, which strays from the universality of everything in fact being files.

### In Pipi &#8220;If it isn&#8217;t a File, it&#8217;s a Folder&#8221;

Pipi solves this by adding another dimension to files;* parents*. By storing something abstract, such as a user or process, as a folder instead of a file, we can append files, or even more folders, within. These files may represent XMP information, images or settings for that particular piece of data.

Folders are treated as files. They have a name, and extension and basic metadata such as dates and original author. In a file, content is a stream of bytes whereas in folders it is the files that it contains and Pipi accesses these folders as though they were files, treating their contained files as standard binary data.

# Advantages

Using folders for files has several advantages, the main one being uniformity and ease of use allowing less of a learning curve for developers and a lower rate of error. Another benefit is the modularity it provides. Logical entities can easily be compartmentalized and transferred without any loss of related information.

# Disadvantages

While folders provide a common logical interface, they do come at a price. Traditionally, the metadata of files are stored in separate database structures, such as MongoDB. This separates the binary and metadata information of entities to where they can both perform at their best. Accessing hundreds of thousands of properties via the database model is many times faster than that of accessing it via individual files on disk.

# Conclusion

While performance is an important factor in any activity, the encapsulation and uniformity provided by this approach is hard to overlook. When one thinks performance, we usually think about one of three things; it is either responsive, sluggish or a long-running process. It is therefore important to consider the environment in which your application runs and whether or not the plausible numbers in a high-activity situation require you to jump through hoops or whether you can direct your focus towards simplicity and stability instead.

In the case of Pipi, the domain for which within creative studios of a 1-100/ppl crew, activity peaks at three times during the day; in the morning (when artists all load up their scenes), during lunch (when long-running processes such as renders or pointcaching are set off) and at 6 pm (when everyone either saves their work or sets of an even longer running process for execution during the night). Since digital content is quite heavy on the file-size front, the master bottleneck in all three of these scenarios is the read/write performance of the server and in the case of a 100 people crew, a low amount of file accesses might hover around 1 read/sec (giving the crew a gentle amount of 2 min from sitting down to start working), a vanilla amount around 3 reads/sec and in busy situations around 50 reads/sec.

Mind you these numbers are mere expectations at this point and via the power given by the ease and usability of this approach, unexpected ways of accessing this data is bound to be discovered and in cases where file access does reach into the hundreds of thousands per second, the user will simply have to wait a few milliseconds before he or she can continue working.

<pre><strong>References</strong>
<a href="http://ph7spot.com/musings/in-unix-everything-is-a-file">http://ph7spot.com/musings/in-unix-everything-is-a-file</a>
<a href="http://en.wikipedia.org/wiki/Everything_is_a_file">http://en.wikipedia.org/wiki/Everything_is_a_file</a>
<a href="http://www.faqs.org/docs/artu/">http://www.faqs.org/docs/artu/</a></pre>