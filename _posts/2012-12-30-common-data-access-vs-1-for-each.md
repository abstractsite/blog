---
title: Common Data Access vs 1-for-each
author: Marcus
layout: post
permalink: /common-data-access-vs-1-for-each/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2012/12/benefits-of-storing-all-data-access-in.html
dsq_thread_id:
  - 2659507605
categories:
  - Theory
---
## 

Benefits of storing all data access in a **.data** member method rather than one method per type of data.

Initially, I chose to store data in member variables and access them through specific means such as 
<pre>>>> self.name<br />'marcus'<br />>>> self.icon<br />&lt;QPixmap instance at 0x00000..&#038;gt<br /></pre>

 I recently found myself in a situation where the number of data access routes I have in one of my primary classes grew into quite a mess. Inbetween state-getters, such as **self.is_hidden() **and essential getters such as **self.name() **were composited classes, each with their own getters, and god knows how many accessors I&#8217;ve inherited from the underlying Qt class.

Qt has a rather neat way of solving this problem. Instead of accessing variables classifiable as being &#8220;data&#8221; through specific methods or properties of a class, the class holds a much broader method called simply &#8220;data&#8221;. The data method takes two inputs, **column** and **role**. The **column** parameter is only applicable with the Model/View architecture of Qt, such as when using Tree- or ItemView. It passes the column of the TreeView that data is requested for. Lets assume our tree only has one column for now.

o root  
|&#8211;o child1  
|&#8211;o child2

That means the **column** parameter will always be ****. The role is the more interesting one. It specifies an **enum** for which **type** of data is requested. Say I wish to know your name. I could simply do 
<pre>>>> you.name()<br />'nicholas'<br /></pre>

With the **.data() **access however, I can instead do 
<pre>>>> you.data(role='name')<br />>>> 'nicholas'<br />>>> me.data(role='icon')<br />&lt;QPixmap instance at 0x00000..&#038;gt<br /></pre>

Cool huh? Actually, it might seem rather dirty at first since **you.name() **is clearly much more to the point. 

This really starts to shine when you&#8217;ve got plenty of things you might want to ask your object for. It might have a name, an adress, a car and perhaps an additional long list of various types of data, each with it&#8217;s own accessor method. This can muddy down the interface for a class. A <a href="http://doc.qt.digia.com/4.7/qabstractitemmodel.html" target="_blank">QAbstractItemModel</a> for instance has 14 different roles associated, such as DisplayRole, DecorationRole and EditRole. Each of the roles may provide unique types of data. DisplayRole for instance values for use in Tree- and Item-Models, whilst EditRole returns an editor of depending on which type of data is to be edited.

Using strings as role keys probably isn&#8217;t a great of an idea though, which is why Qt uses identifiers instead. 
<pre>>>> qtitem.data(role=Qt.DisplayRole)<br />>>> 'nicholas'<br />>>> me.data(role=Qt.DecorationRole)<br />&lt;QPixmap instance at 0x00000..><br /></pre>

Each identifier returns a integer corresponding to the role.

Now, how can you know when the use of a **data** accessor is the better alternative to direct access? How many accessors are too many? The approach seems rather un-OOP in that you both lack the dot-syntax to access data and you lose the ability to encapsulate common data, **name** and **adress** might go under **personal_information** for instance.