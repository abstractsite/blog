---
title: Separating Data From the Information About It
author: Marcus
layout: post
permalink: /separating-data-from-the-information-about-it/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/01/separating-data-from-information-about.html
categories:
  - Theory
---
In any collection that includes a binary chunk of data and its related metadata, it can be convenient to store each in separate locations, such as having files in a hierarchical format on a server and metadata in a database table.

This way, you have two independent sources of information that relate to one anther.  You could store information in the table that you wouldn&#8217;t as easily be able to store in the file itself. Especially when dealing with multiple file-types that share a common usage. 

The problem is how to know which piece of the database table refers to which file. This is called **referential integrity**. Either each cell keeps a record of which data it represents, or each data contains reference to which cell its data is stored. &#8220;**integrity**&#8221; thus refers to how strong this link is.

This link is rather important. Lets take an example.

On your server, you have a file. A maya scene file representing a Character Rig. This rig has properties, such as who made it, when and how it was made. In addition, this rig exists in more than a vacuum. As a buildingblock, it has been built out of other buildingblocks such as models and perhaps even other rigs. The rig contains links to other rigs and thus maintains it&#8217;s own referential integrity. More on that later.

Then, in your database table, at position A5-C5, you have stored its **creator** and **date** at which it was created and a **reference** to its location on disk.

<span> __________A_____________B_________________C________________</span>  
<span>|5 |  Marcus      | 2012-04   | c:\path\charactersetup.ma   |</span>  
<span>|&#8211;|&#8212;&#8212;&#8212;&#8212;&#8211;|&#8212;&#8212;&#8212;&#8211;|&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;|</span>

Pretty cool huh? This way, I could look up the path to my binary data in this table and retrieve information about it not commonly stored by default file systems. Anything could be put in this table!

### Synchronization

Now imagine what would happen if we were to move **charactersetup.ma** to c:\anotherpath\charactersetup.ma. The link would be broken and the metadata would no longer know what binary file it relates to.

We&#8217;ve got a couple of options in this case. We could:  
1. **Prevent files from being moved**  
2. **Adjust cell when moving file**  
3. **Automate cell-modification when moving the file**

**Prevention**  
This is the easiest approach. Simply ensure that files don&#8217;t need to be moved and enforce that fact either by setting files and directories to be read-only. In many cases, this is sufficient.  
** **  
**Manual Intervention**  
Whenever you move a file, simply update the cell. You could have either a web-based software for managing your database, making the editing not so bad. When moving more than one file on a regular basis however can make this process rather tedious. That&#8217;s when automation can help.** **

**Automation**  
Whenever you move a file, simply signal the database to follow. This requires some work. If you are on windows, you know how to move files via Windows Explorer. You could set up a callback from Explorer to your database, letting it know whenever a relevant file is being moved and act accordingly.

A more common approach however is to only allow files to be modified by your own tools. That is, instead of teaching Windows Explorer to your Database, let your Database and your Modification Tools speak the same language to begin with.

Having all of your tools under the same roof has it&#8217;s advantages. For instance, a callback from Windows Explorer could not send information about why the change was made. Something that could be critical in a collaborative environment. On the other hand, it could help prevent files from being moved by artists who don&#8217;t have write-access to certain files. Something you would get for free due to the tight integration with the current user and his permissions.

<div>
  <b>Synchronize utilizing existing tools or roll your own?</b>
</div>

If a user is allowed to use common tools such as Windows Explorer to **move** files, should they also be allowed to **rename** files this way? How about **modifying **the properties for a file from executable to non-executable? Integrating an existing tool has the drawback that you might end up muddling the interface to your toolchain. The user needs to know what is supposed to be possible and what is not, he needs to know the constraints of the system and only work within them.

By integrating a common, yet comprehensive and existing toolset into your application, you need to ensure that all bases are covered by either clearly stating what is allowed up front or informing the user whenever an unsupported action is taking place. As you might suspect, this requires you to have a comprehensive understanding of what the Explorer is able to do in the first place and ensure that whatever it is able to do is handled appropriately. <div>
</div>

<div>
  <b>Windows Explorer Feature List</b>
</div>

<div>
  Create<b> </b>
</div>

<div>
  Read (incl. their properties)
</div>

<div>
  Update (move, rename)
</div>

<div>
  Delete
</div>

Another way of ensuring that your data and metadata are synchronized is to only allow file modification through the use of custom tools. This means that for whatever feature you wish to enable, you must explicitly build it. This makes the support for it rather fool-proof in that you give yourself the ability to only enable features which are easily supported. It does however mean that the more features you require, the more code you must write and the more code you write, the more room there is for bugs to creep in.

### Is there another way?

<div>
  This brings me to the climax of this post. Keeping your data synchronized with your metadata is always a headache and there will always be times where there is a mismatch, either due to errors in your program or human-error.
</div>

<div>
</div>

<div>
  Let me show you the way I chose to approach it in the Asset Library.
</div>

<div>
</div>

<div>
  What do we have? Our assets all have additonal information about them, such as change-logs and relations to other assets in the project, but most importantly, it contains information about how it should get treated. An Asset has no files, it is merely a container for various types of character setups, textures, shaders etc. Which means we could not rely on file format to tell us how to handle it, we must give it an identity through other means. Thus, we have <b>binary data</b> inside of <b>groups </b>along with its corresponding <b>metadata</b> and we would like to keep them synchronized.
</div>

<div>
</div>

<div>
  <b>Extrapolation</b>
</div>

<div>
  In windows, you can attach additional information to a file such as dimension, frame-rate, comments and even thumbnails. This is used by a few file formats to make browsing media a more immersive experience in apps such as Explorer. It is however to the best of my knowledge limited to only a few types of metadata on only a few types of file formats. Unless, as far as I know, you go more deeply in which case things seems less stable. In addition, this would require reading and writing entire files when modifying metadata which is a big deal in most scenarios but an especially big deal when modifying large pointcaches of several hundreds of gigabytes. Not sure how this works on folders.
</div>

<div>
</div>

<div>
  <b>Integration</b>
</div>

<div>
  What would be nice is if we could somehow store the metadata directly in the binary file. Maya files for example may be stored in an ASCII format, thus allowing us to extrapolate it with additional information inside the file in the form of comments. Nuke also allows for this. However, some formats do not and thus doing it this way would limit us to only extrapolate certain file formats and not others. Additionally, the same fate is suffered with that of Extrapolation in that large files need to be read and written whenever a change occurs. This also wouldn&#8217;t be that easy with folders.
</div>

<div>
</div>

<div>
  <b>Bundling</b>
</div>

<div>
  Another way is to keep them separate in terms of files, but store them together somehow. This would allow us to benefit from a database approach whilst not having to worry too much about synchronizing them since they will always be together. 
</div>

<div>
</div>

<div>
  How can we bundle them? Well, we want them to always be together and thus separating them should involve an obvious and difficult process of an either manual or tool-based intervention. How about storing metadata in a <b>.txt </b>file along with <b>charactersetup.ma</b> binary file in an uncompressed archive of sorts. Such as <b>.zip</b>. This would allow assets to be passed around easily without running the risk of it loosing its metadata and suffer the performance issues whenever reading or writing to compressed archives. Reading and writing to them is quite easy as most operating systems allow for zip archives to be treated as regular folders, with the addition of them having a different icon. Which in our case is a good thing as it enlightens the fact that you are within a bundle that should not be dissolved.
</div>

<div>
</div>

<div>
  In addition, it would allow us to give the archives custom file extensions, such as <b>.asset </b>for archives of type Asset.
</div>

<div>
</div>

<div>
  This allows us to store <b>Any</b> metadata <b>independently</b> from the type of binary data or group in addition to the tight coupling between the two. It does however require us to read and write potentially large files whenever a change occurs. It also requires us to deal with that of nested archives.
</div>

<div>
</div>

<div>
  o PuffAdder
</div>

<div>
      o texture
</div>

<div>
      o character_setup
</div>

<div>
      o simulation_setup
</div>

<div>
</div>

<div>
  <b>PuffAdder</b> is a group with <b>metadata</b>, and <b>character_setup</b> is binary data with additional metadata<b></b>, which means we end up with a bundle of bundles. Ultimately, we would end up with the entire data-set being a large bundle of bundles of bundles..
</div>

<div>
</div>

<div>
  o MyProject.project
</div>

<div>
      o MyDatabase.database
</div>

<div>
          o MyAsset.asset
</div>

<div>
              o MyVariant1.variant
</div>

<div>
              o MyVariant2.variant
</div>

<div>
</div>

<div>
  How about we turn the situation around. Instead of relying on file telling us what type of data we are dealing with, how about letting the <b>folder</b> have a type? If the folder is a type, that means it&#8217;s content is the data just as the ones and zeros are the data of a binary file (read &#8220;container&#8221;). It would mean metadata and binary data could live as equals under the same roof, being accessed in a common fashion, without causing performance penalties when accessing either of them separately.
</div>

<div>
</div>

<div>
  A folder could have dots in its name, essentially enabling them to have an extension just like files. However, as a matter of preference, adding dots to folders clutters their representation in an explorer as they would be more difficult to distinguish from files other than by looking at their icon. Of course, the library could strip the name during their display if one wanted to go that route without the visual clutter.
</div>

<div>
</div>

<div>
  Thus, the asset library expects its library of assets to be formatted as follows:
</div>

<div>
  - Each folder has a metadata file
</div>

<div>
  - Each folder may specify a type other than the default via its metadata
</div>

<div>
  - Each folder may have additional folders
</div>

<div>
</div>

<div>
  o MyProject
</div>

<div>
      &#8211; metadata
</div>

<div>
      o MyDatabase
</div>

<div>
          &#8211; metadata
</div>

<div>
          o MyAsset
</div>

<div>
              &#8211; metadata
</div>

<div>
              o MyVariant1
</div>

<div>
                  &#8211; metadata
</div>

<div>
                  &#8211; binary data
</div>

<div>
              o MyVariant2
</div>

<div>
                  &#8211; metadata
</div>

                &#8211; binary data

Having an additional file per folder clutters their interface, and thus we set the metadata to be &#8220;hidden&#8221;  
  <div>
  o MyProject
</div>

<div>
      o MyDatabase
</div>

<div>
          o MyAsset
</div>

<div>
              o MyVariant1
</div>

<div>
                  &#8211; binary data
</div>

<div>
              o MyVariant2
</div>

                &#8211; binary data

<div>
   Now we have a hierarchy of files, each folder knows what type it is without cluttering its interface.
</div>

<div>
</div>

<div>
  How do I deal with keeping binary data and metadata toghether? The only accesspoint to the file system is through custom tools which only allow certain features to be performed. Artists use the library and the library is only allowed to read files. Supervisors use an Editor which may edit files and may expose more information about the system.
</div>

<div>
</div>

<div>
  Some topics were left out of this post. Such as reading and writing metadata, type of metadata that may be stored and how to store it.
</div>