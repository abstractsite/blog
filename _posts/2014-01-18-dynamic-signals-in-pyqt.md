---
title: Dynamic Signals in PyQt
author: Marcus
layout: post
permalink: /dynamic-signals-in-pyqt/
categories:
  - Uncategorized
---
> This post is about devising your own Signals and Slots mechanism to work with PyQt in a more dynamic fashion.

The legendary [Signals and Slots][1] in Qt are not so difficult to understand, and once you understand it not so difficult to implement.

Here is the class we will be talking about in this post.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">class Signal:
    def __init__(self):
        self.__subscribers = []
      
    def emit(self, *args, **kwargs):
        for subs in self.__subscribers:
            subs(*args, **kwargs)

    def connect(self, func):
        self.__subscribers.append(func)  
      
    def disconnect(self, func):  
        try:  
            self.__subscribers.remove(func)  
        except ValueError:  
            print('Warning: function %s not removed '
                  'from signal %s'%(func,self))

</pre>

### Why

Lets back up a minute and think about why you would want to implement them yourself.

[PyQt*.QtCore.pyqtSignal()][2], the factory method you use to create signals in your custom classes, comes with a few limitations.

pyqtSignal:

1.  Only works with [class attributes][3]
2.  Cannot be used in an already instantiated class
3.  Must be pre-specified with any data-types you wish to emit
4.  Produces a signal which does not support keyword arguments and
5.  Produces a signal which cannot be modified after instantiation

None of these conform to the way Python normally works. Lets go through each one a little bit further.

### 1. Only works with class attributes

Signals are not class attributes. PyQt\*.QtCore..pyqtSignal() is merely a vessel for a future instance variable containing a PyQt\*.QtCore.pyqtBoundSignal instance. When you instantiate your class, pyqtSignal goes to work and injects itself as an instance variable and adds itself to the [QMetaObject][4] of the class.

> QMetaObject? It comes with useful methods such as .className(), superClass(), methodCount() which returns the name of the class, its superclasses and number of methods respectively.
> 
> In C++ these are probably very useful, however a Python programmer might not be very impressed. It&#8217;s something we&#8217;ve had access to all along via any instances&#8217; \_\_class\_\_, \_\_bases\_\_ and \_\_dict\_\_attributes.

### 2. Cannot be used in an already instantiated class

Now here&#8217;s the kicker.

If you&#8217;re doing any sort of base- or abstract class work with Qt widgets, you&#8217;ll quickly realise that [you can&#8217;t inherit signals][5].

Other than that, if try and bypass inheritance and have a builder spit out widgets for you, you&#8217;ll also notice how [Dependency Injection][6] isn&#8217;t going to work with signals. They have to be created as class attributes and they can only be created using pyqtSignal(). Please correct me if I&#8217;m wrong.

### 3. Must be pre-specified with any data-types you wish to emit

In other languages, this is referred to as [static typing][7]. Python however doesn&#8217;t do any of that.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># Note, these are pseudo-coded, as pyqtSignal will 
# normally have to be run via a class' class attribute.
signal = pyqtSignal(int, str)
signal.emit(my_number, my_string)
signal.emit(my_string, my_number)
# TypeError
signal.emit(not_enough_args)
# TypeError
</pre>

### 4. Does not support keyword arguments

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">TypeError: emit() takes no keyword arguments
</pre>

Keyword arguments are quite useful as a means of self-documenting code.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">signal.emit(5)
</pre>

Could instead be written as:

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">signal.emit(velocity=5)
</pre>

Not only does it increase readability, it can also be used to enforce signals and slots to carry an identical argument signature.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">def callback(name, address):
	print("Name=%s and address=%s" % (name, address))


signal = Signal()
signal.connect(callback)

# Mistake the first argument for a tuple.
signal.emit(names=('marcus', 'ottosson'), address='earth')
# TypeError: callback() got an unexpected keyword argument 'names'

# When actually, its a single string value.
signal.emit(name='marcus ottosson', address='earth')
# Name=marcus ottosson and address=earth

# Of course, non-keyword arguments works too.
signal.emit('marcus ottosson', 'earth')
</pre>

### 5. Cannot be modified after instantiation

As a Python object, you would expect the ability to monkey-patch, but pyqtSignals are special enough to not let you do any of that.

I&#8217;ll provide an example of monkey-patching for you below.

# Grand opening

Let&#8217;s turn that frown upside-down, mock-up a feature list and provide an example. How&#8217;s this for a feature list of Signal?

1.  Pure Python object
2.  Dynamic instantiation
3.  No type-checking
4.  Support for keyword arguments
5.  Monkey-patch support

All of which are already expected from Python objects in general.

### Full Example

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># Lets start by constructing our test-subject
    # These could be any class, including QObjects 
    # or any of its subclasses.
    Homosapien = type('Homosapien', (), {})

    # And then introduce two of them to the world.
    boy = Homosapien()
    girl = Homosapien()

    # Next, we inject a brand new signal
    boy.s = Signal()

    # We monkey-patch signal to tell you
    # when it is being connected to.
    def connect(self, f):
        print("Boy just got a new connection")
        Signal.connect(self, f)

    boy.s.connect = lambda f: connect(boy.s, f)

    # Inject method to be called upon
    # when our injected signal emits.
    def state_fact(message):
        print("Boy &lt;%s&gt; Girl = True" % message)
    
    girl.c = state_fact

    # Make the connection..
    boy.s.connect(girl.c)
    
    # ..and then emit. 
    # With key-worded argument, just cus' we can.
    boy.s.emit(message='loves')

</pre>

Which prints

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># Boy just got a new connection
    # Boy &lt;loves&gt; Girl = True
</pre>

# Understanding Signals and Slots

The Qt signals and slots are based on a programming pattern known as the [Observer pattern][8].

Our implementations is fairly straightforward so there are some things that we haven&#8217;t covered, mainly related to how it works with threading.

> You&#8217;ll notice that if you try and send a signal from another thread, the recieving thread \*might\* crash on you. And therein lies the beauty of multi-threaded operations, or operations that share resources and try and access them simultaneously.
> 
> This includes any use of QThread and the Python threading module.

Another issue noticed during testing is use of [QObject.sender()][9]

In a nutshell, QObject.sender() returns the caller from the receiving end.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">def callback(self, message):
	# Used within a class, callback is triggered 
	# via a signal. Works with both pyqtSignal 
	# and our own implementation.
	source_of_signal = self.sender()
</pre>

Quite useful when a slot is receiving multiple signals and needs a way to distinguish them. 

> The API reference warns about its breach in modularity for object-oriented programs and I generally tend to avoid it.

I&#8217;m not familiar enough with the details to give you a full overview, but when using our implementation over the one given by pyqtSignal(), sender retrieves the first in a chain of signals.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># Here, QObject.sender() called within obj3.listen
    # will return obj1, and not obj2. Even though obj2
    # obj2 was the last one to emit the signal.
    obj1.signal.connect(obj2.emit)
    obj2.signal.connect(obj3.listen)
    obj1.signal.emit()
    # With pyqtSignal, it would instead have retrieved obj2.
</pre>

# The exciting part

The observer pattern is great for GUI programming.

Actually, let me rephrase that. The observer pattern is great.

### Example 1 &#8211; The all-seeing eye

If you&#8217;ve ever made use of the fact that imported modules are accessible from any other imported module within the same running instance of Python (e.g. [the Django settings][10]), you&#8217;ve most likely already been to town with all sorts of perfectly legal global-variable use.

Signals are the crack to this methodology.

[<img src="http://abstractfactory.io/blog/wp-content/uploads/2014/01/signalsandslots_img11.png" alt="signalsandslots_img1" width="490" height="280" class="alignnone size-full wp-image-546" />][11]

Here the common module *shared.py* is imported by two or more modules.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># main.py
from PyQt5.QtWidgets import *
from PyQt5.QtCore import *

import shared
import logic


class Window(QWidget):
	def __init__(self, parent=None):
		super(Window, self).__init__(parent)

	def showEvent(self, event):
		shared.shown_signal.emit()
		super(Window, self).showEvent(event)


if __name__ == '__main__':
	import sys
	app = QApplication(sys.argv)

	win = Window()
	win.show()

	sys.exit(app.exec_())
</pre>

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># logic.py
import shared


def show_event():
	# I will be triggered whenever a 
	# listening widget is being shown.
	print("I'm being shown")

# Connection
shared.shown_signal.connect(show_event)
</pre>

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title=""># shared.py
# (using our Signal class from at the very top)
shown_signal = Signal()
</pre>

### Example 2 &#8211; Observe attribute changes

It can sometimes be useful to monitor an attribute of a class.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">class Listener(object):
	def __init__(self):
		self.container = Container()
		self.container.value_changed.connect(self.value_changed_event)

	def value_changed_event(self, previous, current):
		print("%r says: Value was changed from %s to %s" % 
		     (self.__class__.__name__, previous, current))


class Container(object):
	def __init__(self):
		self.__value = None

		# This is our signal. We emit this
		# whenever `value` changes.
		self.value_changed = core.Signal()

	@property
	def value(self):
		return self.__value

	@value.setter
	def value(self, value):
		self.value_changed.emit(previous=self.__value, 
					current=value)
		self.__value = value


if __name__ == '__main__':
	list = Listener()
        
	# Try an modify the container from within the
	# listener, and listener will be notified of 
	# the change and respond!

	list.container.value = 5
	# 'Listening' says: Value was changed from None to 5

	list.container.value = 6
	# 'Listening' says: Value was changed from 5 to 6

</pre>

# Benefits

To avoid repeating the internet on the many benefits of the Observer pattern, I&#8217;ll instead point you towards some existing resources about it and other patterns.

[Design Patterns][12]  
Is an excellent summary and reference of many very useful patterns.

[Head First Design Patterns][13]  
Provides a more gentle and explanatory view of many of the same patterns.

# Summary

As we have seen, pyqtSignal is incredibly useful, but can sometimes fall short in complex situations.

Rolling our own solutions however has the disadvantage of no longer standing on the shoulders of giants as we take responsibility for features we might not know we were relying upon until they were no longer there, e.g. thread-safety.

# Discussion

Although they compete for the same spot in your code, they are not necessarily mutually exclusive. Perhaps a better approach is to have them compensate for each others weaknesses and use them where they are best suited.

For instance, QThreads may use pyqtSignal and your widget baseclasses and builders may use Signal.

I&#8217;ve started a discussion on [Stack Overflow][14] about it. Not many inputs yet, but perhaps by the time you read this, there will be.

# Before I go..

..there is one more thing I have to point out. 

Although the use of signals derived from pyqtSignal and signals created directly using our Signal class are identical in every scenario I have yet encountered (they do share the same [interface][15], after all) there is one thing worth pointing out that baffled me at first.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">class Window(QWidget):
	same_signal = pyqtSignal()
	def __init__(self, parent=None):
		super(Window, self).__init__(parent)
		self.same_signal = Signal()
</pre>

It may seem as though simply replacing pyqtSignal() with Signal() in this case should work, but like mentioned earlier pyqtSignal() actually waves its wand here and instantiates a PyQt*.QtCore.pyqtBoundSignal object when the class is instantiated.

This means that the class attribute you assigned to has magically become an instance attribute.

The effect of this is that if you have multiple instance of the class, they will all contain their own signals that do not interfere with each others emitting.

Our implementation does not perform such magic and thus a class attribute remains a class attribute.

Unfortunately, this also means that if you assign a Signal as a class attribute, each of its instantiated objects will contain the same subscribers and will emit whenever any other object emits.

The solution is to create them as instance attributes. As they should have been from the start.

Thanks for reading!

 [1]: http://qt-project.org/doc/qt-5/signalsandslots.html
 [2]: http://pyqt.sourceforge.net/Docs/PyQt5/signals_slots.html#PyQt5.QtCore.pyqtSignal
 [3]: http://docs.python.org/2/tutorial/classes.html
 [4]: http://qt-project.org/doc/qt-5/qmetaobject.html
 [5]: http://trevorius.com/scrapbook/python/pyqt-multiple-inheritance/#respond
 [6]: http://stackoverflow.com/questions/130794/what-is-dependency-injection
 [7]: http://www.sitepoint.com/typing-versus-dynamic-typing/
 [8]: http://en.wikipedia.org/wiki/Observer_pattern
 [9]: http://qt-project.org/doc/qt-5/qobject.html#sender
 [10]: https://docs.djangoproject.com/en/dev/topics/settings/#using-settings-in-python-code
 [11]: http://abstractfactory.io/blog/wp-content/uploads/2014/01/signalsandslots_img11.png
 [12]: http://www.amazon.co.uk/Design-patterns-elements-reusable-object-oriented/dp/0201633612
 [13]: http://www.amazon.co.uk/Head-First-Design-Patterns-Freeman/dp/0596007124/ref=sr_1_1?s=books&#038;ie=UTF8&#038;qid=1390044302&#038;sr=1-1&#038;keywords=head+first+design+patterns
 [14]: http://stackoverflow.com/questions/21101500/custom-pyqtsignal-implementation
 [15]: http://pyqt.sourceforge.net/Docs/PyQt5/signals_slots.html#defining-new-signals-with-pyqtsignal