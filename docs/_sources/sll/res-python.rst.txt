======
Python
======


.. toctree::
    :maxdepth: 1

    python/python-why
    python/python-resources
    python/python-best-practices
    python/python-virtual-env
    python/python-tips-and-tricks
    python/python-mongodb


There are already other places where advanced Python material can be found,
so this is not meant as a comprehensive compendium or tutorial. This is simply
intended to catalog some of the more useful things I have encountered in my
own journey.

Python 3 is slowly becoming the standard version of the language, but for a
number of reasons, not everyone has been able to fully make the switch.
In my opinion, if given a choice, always learn things the Python 3 way. In
quite a few cases, writing clean Python 3 code is inherently
backward-compatible with the latest Python 2.7.X, or if it isn’t, takes very
little effort to make it backward-compatible. I strongly feel it is far better
to write code for the current and future with a few tweaks to be compatible
with the old, than to write for the old and try to make it future-compatible.

Some resources may not be completely up-to-date, so keep these things in mind:

*   You should almost always use the new style string format
    (``'{0}'.format(...)``) method over interpolation (``'%s %s' % (str1, str2)``)

*   Always try to use the standard library ``logging`` module over the ``print(...)`` function

*   If you have to resort to the ``print(...)`` function, always use it as a function
    (e.g. don’t use the old syntax of ``print ‘here is text’`` use
    ``print(‘here is text’)``)
