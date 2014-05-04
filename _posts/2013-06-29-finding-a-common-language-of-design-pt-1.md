---
title: Finding a Common Language of Design pt. 1
author: Marcus
layout: post
permalink: /finding-a-common-language-of-design-pt-1/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/06/finding-common-language-of-design-pt-1.html
categories:
  - Theory
---
It dawned upon me quite early that to design several interconnected parts of software, they would have to share a common language in terms of how they looked and behaved. Luckily, the default look and feel of an application developed under any operating system using <a href="http://qt-project.org/" target="_blank">Qt</a> is identical to other applications built under the same operating system. It mimics the window frame, the drag and resize facilities, closing and minimizing behaviours and also, colors and sound. In fact, developing with Qt provides promise of <a href="http://en.wikipedia.org/wiki/Write_once,_run_anywhere" target="_blank">&#8220;write once, run everywhere&#8221;</a>, or WORE, meaning that whatever you write will not only work on any platform, but also mimic the look and feel of that platform, while still performing as you designed.

&#8220;But then..&#8221; I hear you say, &#8220;..why not use that to your advantage when developing Pipi?&#8221;. It&#8217;s a fair question.

Pipi does not adhere to this flexibility of mimicking its host. This is due to the fact that Pipi is a cross-platform framework. It will be run on a variety of platforms (Windows, Linux and Mac) and thus the behaviour of its host platform will vary but its users, however, won&#8217;t. Users will come and go and their environments may change, the very platform they work on may change for each project they enroll which is why it is so important to maintain a &#8220;beacon of light&#8221; and provide a consistent and streamlined UI that any artist can access and use without the slightest doubt of anything being different. Regardless of which platform the artist is working under.

This does not mean, however, that the practices put in place by these hosts are ignored. Throughout the evolution of software, users have come to expect many things from their interaction with computers and it is your responsibility to maintain these expectations if you decide to stray from the path. There is a saying which says that the greatest design is that which behaves just as users expect. This applies to any interaction design, not least so webpages. If you have ever found yourself entering an unfamiliar website with a goal in mind, only to come out of that site with goal achieved 5 minutes later not remembering exactly how you did it but that in fact you did, you have experienced a rare and well-designed site and should take note of its whereabouts and learn from its design. This has happened to me only a few times and sadly, their successfull design makes them the most easily forgettable websites out there. They provide no friction, no moment of wonder or scratching of the head and thus no time to commit this flawless design to memory.

As you might suspect, if you are designing for a fashion site or any other market promoting content rather than functionality, this may not be the best route. For design that evolves around ease-of-use however, focus and simplicity (to borrow from the mantra of Steve Jobs) is key.