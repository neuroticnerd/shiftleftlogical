
Python
======

Unfortunately, there still exists somewhat of a schism between the Python 2
and Python 3 camps, but the fact of the matter is that Python 2 will only be
officially supported still for a finite amount of time before Python 3 will
become the de-facto standard. In my opinion, if given a choice, always learn
things the Python 3 way. In quite a few cases, writing clean Python 3 code is
inherently backward-compatible with the latest Python 2 (v2.7.12 at time of
writing), or if it isn’t, takes very little effort to make it
backward-compatible. I strongly feel it is far better to write code for the
current and future with a few tweaks to be compatible with the old, than to
write for the old and try to make it future-compatible.


|link_learnpython|
    Pretty awesome site really, I wish I had known about
    this when I was learning to write code or picking up Python

|link_thinkpython|
    Starts with the basics of programming before delving
    further into Python; ultimately has loads of information about the language

|link_httlacspy3| (|link_thinkcs_old|)
    Learn programming concepts and paradigms using Python 3

|link_pycourse|
    Teaches python as well as enough in-depth coverage that
    it serves well as an introduction to programming

|link_pyhardway|
    Great information for learning Python; the power and
    flexibility it gives makes writing scripts or small programs simply trivial

|link_pyawesome|
    Curated list of great Python libraries and frameworks
    to investigate and utilize in your own projects

|link_py4fun|
    Collection of python algorithm exercises

|link_pynlp|
    Who doesn’t find NLP interesting?

|link_intro_py|
    I haven't personally gone through this one specifically,
    but all of the other MIT OCW content I have looked through thus far has
    been extremely solid

|link_nonprog_guide|


.. |link_learnpython| raw:: html

    <a href="https://www.learnpython.org/" rel="external noopener noreferrer">Learn Python</a>

.. |link_thinkpython| raw:: html

    <a href="http://greenteapress.com/wp/think-python-2e/" rel="external noopener noreferrer">Think Python</a>

.. |link_httlacspy3| raw:: html

    <a href="http://openbookproject.net/thinkcs/python/english3e/" rel="external noopener noreferrer">How to Think Like a Computer Scientist: Python 3</a>

.. |link_thinkcs_old| raw:: html

    <a href="http://www.greenteapress.com/thinkpython/thinkCSpy/" rel="external noopener noreferrer">previous official edition</a>

.. |link_pycourse| raw:: html

    <a href="http://www.python-course.eu/course.php" rel="external noopener noreferrer">python course</a>

.. |link_pyhardway| raw:: html

    <a href="https://learnpythonthehardway.org/book/" rel="external noopener noreferrer">Learn Python the Hard Way</a>

.. |link_pyawesome| raw:: html

    <a href="https://github.com/vinta/awesome-python" rel="external noopener noreferrer">Awesome Python</a>

.. |link_py4fun| raw:: html

    <a href="http://www.openbookproject.net/py4fun/" rel="external noopener noreferrer">Python 4 Fun</a>

.. |link_pynlp| raw:: html

    <a href="http://www.nltk.org/book/" rel="external noopener noreferrer">Natural Language Processing with Python</a>

.. |link_intro_py| raw:: html

    <a href="https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-189-a-gentle-introduction-to-programming-using-python-january-iap-2011/" rel="external noopener noreferrer">A Gentle Introduction to Programming Using Python (MIT OCW)</a>

.. |link_nonprog_guide| raw:: html

    <a href="https://wiki.python.org/moin/BeginnersGuide/NonProgrammers" rel="external noopener noreferrer">Non-programmers Guide to Python Programming</a>


Things to Note
--------------

Some resources may not be completely up-to-date, so keep these things in mind:

*   You should almost always use the new style string format
    (``'{0}'.format(...)``) method over interpolation (``'%s %s' % (str1, str2)``)

*   Try to use the standard library ``logging`` module over the ``print(...)`` function

*   If you have to resort to the ``print(...)`` function, always use it as a function
    (e.g. don’t use the old syntax of ``print ‘here is text’`` use
    ``print(‘here is text’)``)

I’m also working on a guide for dealing with Python development environment setups in Windows; it’s a little trickier than it should be since many Python-related tools and modules were written with Unix platforms as a priority.
