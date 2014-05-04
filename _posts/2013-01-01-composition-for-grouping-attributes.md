---
title: Composition for Grouping Attributes
author: Marcus
layout: post
permalink: /composition-for-grouping-attributes/
blogger_blog:
  - marcusottosson.blogspot.com
blogger_author:
  - Marcus Ottosson
blogger_permalink:
  - /2013/01/composition-for-grouping-attributes.html
categories:
  - Theory
---
In my <a href="http://marcusottosson.blogspot.com/2012/12/benefits-of-storing-all-data-access-in.html" target="_blank">previous post,</a> I briefly mentioned that I stored instance attributes together with composed instances whose attributes I could fetch via **instance.composited_instance.attr**

Is composition good for this sort of thing?

In books, you might find composition to be used for grouping functionality by letting smaller objects form larger objects via nested encapsulation. E.g. instead of storing **name,** **home_number** and **work_number** under **Person**, you could instead choose to store **home_number** and **work_number** under a **Contact** object that is then stored under **Person**.

o Person  
    o .name   
    o .contact  
        o .home_number  
        o .work_number** **

So whats the benefit of doing this? Well, besides the benefits of <a href="http://en.wikipedia.org/wiki/Object_composition" target="_blank">composition in general</a>, you get to stow away accessors that might not be directly related to the overall operation of the object into less obvious paths, thus encouraging the use of parts of the functionality over others. The directly available accessors is intuitively more comfortable to use than to go 6 level deep for a simple operation. 
<pre>>>> you.name() # This<br />"marcus" <br />>>> you.personaldetails.contactdetails.publicinformation.name() # vs. this<br />"marcus"<br />>>> # Which do you prefer?<br /></pre>

<a href="http://www.gadgetreview.com/wp-content/uploads/2012/02/TiVoSlide-C00240-Keyboard-Remote-Control-in-Black_thumb.jpg" imageanchor="1"><img border="0" height="151" src="http://www.gadgetreview.com/wp-content/uploads/2012/02/TiVoSlide-C00240-Keyboard-Remote-Control-in-Black_thumb.jpg" width="200" /></a>The neat thing about the latter is once you start gathering functionality that relates to the bigger picture of the parent object, but aren&#8217;t really necessary for everyday use. Remember, the idea is to make the interface as simple, yet as complete, as possible.

<pre>>>> you.countries_visited()<br />['france', 'russia', 'usa', 'finland', 'sweden']<br />>>> you.history.travel.countries_visited()<br />['france', 'russia', 'usa', 'finland', 'sweden']<br /></pre>

Storing that level of detailed functionality directly into the parent object can easily obfuscate it&#8217;s interface. That&#8217;s why it can be beneficial to stow them away somewhere where, when accessed, the user knows he&#8217;s dealing with less common functionality.

<a href="http://joshlinkner.com/images/2012/05/SAN.jpg" imageanchor="1"><img border="0" height="147" src="http://joshlinkner.com/images/2012/05/SAN.jpg" width="200" /></a>An alternative to composing accessors is to collect external sets of functionality. Rather than storing all functionality inside an object and it&#8217;s composed objects, you can choose to store it in separated functions, either in the same file or in different modules or packages.

<pre>>>> you.nearby_cinemas()<br />['canary wharf cineon 1.5km', 'north greenwich odeon 0.4km']<br />>>> externalmodule.position.nearby_cinemas(you)<br />['canary wharf cineon 1.5km', 'north greenwich odeon 0.4km']</pre>

As you can see,** you** is no longer responsible for processing this command. Rather, an exernal module takes care of the necessary steps in order to produce the result. This can lead to deep and thorough functionality whilst still providing a simple interface for **you**. The user now has to think about what tool is right for the job as opposed to figuring out how to use one tool for everything.