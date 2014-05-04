---
title: Open Metadata and Unified I/O
author: Marcus
layout: post
permalink: /unified-io/
categories:
  - Architecture
  - Python
  - Theory
---
> What does reading a file from disk have to do with receiving data from the internet? This post is about how all digital transactions relate to one another, what they all have in common and how that could be useful.

Without going into too much detail, a file is nothing more than a link to a physical address on disk. Under normal circumstances, you only ever need one link per address.

Just like you can create a link to a file, you can also create links to physical addresses. You do it all the time. Every time you hit download, under the hood data is first being written to your physical drive and then linked to via a file. The file is your handle to the data you are downloading.

Theoretically, you could remove files without ever affecting the data they point to. In fact, that is exactly what happens all the time.

When you remove a file, you aren&#8217;t actually removing the data. The file is for you and the OS to keep tabs on what happens on that spinning disk (or SSD) you keep within your computer. If you could keep track of it yourself, there would be no need for files.

Your OS talks to your files to, among other things, find out how much disk space is available on disk. It is quite simply everything that isn&#8217;t being linked to via files.

Once the &#8220;reference count&#8221; of any physical address reaches zero &#8211; meaning no files are currently pointing to it &#8211; it is said to be &#8220;free&#8221;. Consider it automatic garbage collection.

An interesting side-effect of this phenomena is disk recovery.

You might have accidentally removed files at some point and then used a file-recovery program like [Recuva][1] to get it back.

How did it do that?

Well, turns out that other than the physical data being referenced via files, the data also has a visible &#8220;Start here&#8221; and &#8220;End here&#8221; location. Recuva would look for such clues, encapsulate the data in-between and provide you the option to make a new link pointing to that address.

Neat, right?

In fact, what goes on is a little bit more magical. See, a file cannot only contain a starting point of where your data begins. Nor just a start and end.

You might have at some point resorted to de-fragmenting your disk. Maybe you found it slow and read that this was the way to go.

What you were doing (or telling your computer to do) was moving chunks of physical data closer to their immediate neighbours, so as to avoid hiccups in their retrieval.

But what does that mean? Well, as I said a few seconds ago, a file has more than a start and end to where data exists. For large files, say 10gb, it is very unlikely that you will have 10gb of empty space laid out consecutively within your hard-drive. (Unless your drive is a virgin, lucky you)

A more likely scenario is that you will have a some space here and some there and so what happens is that the file is spread out across the empty gaps.

A file, being a link to that data, then needs to keep tabs on each of these empty spaces that are now occupied by your big file. And thus rather than a single start and end, it ends up with several starts and several ends depending on how sparse the available space was at the time the file got written.

But so what does this have to do with unifying transactions?

The concept of fetching an address from a file and following the address stretches further.

Google Docs access. If you&#8217;ve got [Google Drive][2] installed on your computer you might have noticed how you got files that resembles those in your online Google Drive account. You can double click them and they bring you to your account via your web-browser. Almost like a regular text-file opening in Notepad or Sublime Text.

The illusion is almost complete. There&#8217;s just one more thing.

If you open that same file in Notepad, you&#8217;ll see something interesting. Inside, there is an address. An address to your online Google Docs document.

Wait, what?

What really happens when you double-click that file is that Google Drive (the software installed on your computer) is launching your web-browser using the link stored inside of that file.

Theoretically, you could remove that file, without it having any affect on your online Google Docs document. However, Google Drive (the software) is manually keeping tabs on what happens to the file stored in your local Google Drive folder.

So that, when you go ahead and remove that simple link that clearly doesn&#8217;t contain the actual document but rather a link to your online document, Google Drive (the software) would send a signal to Google Drive (the service) and tell it to mirror the action.

Whatever happens outside of that folder however is a different story. If you were to move it outside of the Google Drive folder and *then* remove it, nothing would be mirrored online and thus your online copy would remain untainted.

So essentially, a Google Drive file contains a link to a physical address on disk. At the end of that address, there is an address to Google Drive (the service) and at the end of that address lies your document.

# Technically

> In Python, these are the suggested concepts to be used within [Open Metadata][3], the file-based database, as follows.

Goal: To find a unified way to communicate with files. Reading and writing from a plain-text document should involve the same steps as those involved in reading and writing to a more complicated, server-side document.

In both of the cases above, the **formula** can be broken down into three steps.

1.  Get address to physical location on disk
2.  Post-process data at given address
3.  Return formatted data

In the case of a **plain-text** file, the procedure goes as follows:

1.  The .txt file is inputted
2.  The address is resolved, returning the raw data (possibly corrupt)
3.  The data is post-processed (cast to a string) and returned

In the case of a **key/value** store, .json, the procedure goes like this:

1.  The .json file is inputted
2.  The address is resolved
3.  The data is post-processed (run through json.loads) and returned

And in the case of a **Google Docs** document:

1.  The .gdoc file is inputted
2.  The address is resolved
3.  The data is post-processed (see below) and returned

The post-processing in the case of .gdoc is a little more involved.

Like mentioned earlier, the .gdoc file contains a link to an online document, so before we can return the content of it, we must first establish a connection with Google Drive. It&#8217;d ask to authenticate the user who is requesting said data and from there we could proceed with the download.

In each of the three cases, the same three steps are taken. The varying nature of each format is neatly encapsulated within the given extension (&#8220;.txt&#8221;, &#8220;.json&#8221; or &#8220;.gdoc&#8221;)

So how about writing?

Whenever you&#8217;ve got something to write, you would hand it over to an appropriate writer, such as open() with the &#8220;w&#8221; flag passed.

But what about writing to Google Docs? Since we&#8217;ve already established that the Google Drive files isn&#8217;t your actual documents, just links, writing to them would make little sense and you would simply write to the link which, when double-clicked would end up sending you to some other document (if your lucky).

Pre-processing. If we tell our program to write &#8220;Hello World&#8221; to this the given .gdoc file, we would first have to resolve that address, login and send a request to Google.

The formula could be broken down into three steps.

1.  Retrieve
2.  Pre-process
3.  Write to disk

In the case of a plain-text document, the process could go as follows:

1.  Retrieve data, &#8220;Hello World&#8221;
2.  Pre-process, run it through str(data)
3.  Write to disk

In the case of a Google Drive document:

1.  Retrieve data, &#8220;Hello World&#8221;
2.  Pre-process, (see below)
3.  Write to disk

Here, the steps to write to Google Drive remain ambitious and the steps are identical except download now uploads. It still needs to authenticate and it still needs data in a certain format (string).

In conclusion, to attain a bi-directional and unified approach of reading and writing data from any source, be it local or remote, you need:

*   **A)** The Data
*   **B)** To Process
*   **C)** To Output

 [1]: http://www.piriform.com/recuva
 [2]: http://drive.google.com
 [3]: https://github.com/mottosso/openmetadata