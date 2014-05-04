---
title: Building PyZMQ for Python 2.7 MSC v.1600
author: Marcus
layout: post
permalink: /building-pyzmq-for-python-2-7-msc-v-1600/
mytory_md_path:
  - 
categories:
  - Uncategorized
---
> This post is about compiling pyzmq for Windows using Python 2.7 compiled with MSC v.1600 (VS2010) 

The official version of Python 2.7 found at [the python website][1] is compiled with MSC v.1500 (which is Visual Studio 2008). Maya and others however ship with Python compiled with MSC v.1600 (Visual Studio 2010).

This doesn&#8217;t matter most of the time, unless you use C-extension modules such as PyZMQ and PyQt compiled with versions of Visual Studio other than the one Python came compiled with.

<pre>Download PyZMQ for Python 2.7 MSC v.1600 <a href="https://dl.dropbox.com/s/0nmyk43mrod0mza/pyzmq-14.0.1_msc1600.rar">here</a>
Compiled with
 - Windows 7 x64
 - Visual Studio 2010
 - <a href="http://www.python.org/ftp/python/2.7.5/python-2.7.5.amd64.msi">Python 2.7.5_x64
</a> - <a href="https://pypi.python.org/packages/source/p/pyzmq/pyzmq-14.0.1.zipt">pyzmq-14.0.1.zip</a></pre>

The MSI installer of PyZMQ come with a Python extension for Python 2.7, but since this is compiled with MSC v.1500, the same as the official Python distribution as python.org, means Maya's Python, which is on the MSC v.1600 side of the fence, will have trouble working with it.

`# WindowsError: [Error 126] The specified module could not be found #`

Some digging reveals that when Python attempts to import the extention module `libzmq.pyd` it errors due to a missing [MSVCP90.dll][2] which is part of Microsoft Visual C++ 2008 Redistributable Package. It's one way of telling whether the extension you are trying to load is compiled with a version different than the one your Python distribution comes with.

# Compilation Process

Compiling PyZMQ should be as easy as

`>>> python setup.py configure`  
`>>> python setup.py install`

As can be seen [here][3]

However since we're using mayapy.exe rather than the standard python.org binary, we'll have to dance a little to make this work.

With help from the PyQt4 compilation instructions [Compiling PyQt4 for Maya 2014 document][4], I figured out that the pyzmq build process required two environment variables set.

*   INCLUDE
*   LIB

`INCLUDE` must contain the Python headers and `LIB` its library, both of which are necessary for compiling the bindings, just like with PyQt.

`set INCLUDE=c:\Program Files\Autodesk\Maya2014\include\python27`  
`set LIB=c:\Program Files\Autodesk\Maya2014\lib`

The PyZMQ `setup.py`, which is included with the distribution, is using distutils which looks for these environment variables upon launch.

So now, we can successfully run.

`>>> python setup.py configure`  
`>>> python setup.py install`

And the bindings will appear in your `Maya2014\Python\Lib\site-packages` directory. For conveinence, I've supplied a link to the compiled bindings at the top of this post.

Enjoy and thanks for reading.

Marcus

 [1]: http://python.org
 [2]: http://pcsupport.about.com/od/findbyerrormessage/a/msvcp90-dll-not-found-missing-error.htm
 [3]: https://github.com/zeromq/pyzmq/wiki/Building-and-Installing-PyZMQ
 [4]: https://dl.dropbox.com/s/0nmyk43mrod0mza/pyzmq-14.0.1_msc1600.rar