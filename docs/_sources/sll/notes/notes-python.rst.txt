:date: 2016-09-06
:modified: 2019-09-09

===================
Python Notes
===================

**GIL** [1]_ [2]_ [3]_ [4]_
    The Global Interpreter Lock is a mutex that protects access to objects
    thus allowing only a single thread in the Python interpreter to execute
    at any given time. The lock is needed because the memory management in
    CPython is not thread-safe (mostly due to the reference counting
    mechanism for garbage collection). This prevents multithreaded Python
    programs from fully utilizing multiprocessor hardware. To achieve true parallelism with CPython, one must turn to the multiprocessing module
    to utilize multiprocessor CPUs.

**GC and COW** [5]_ [6]_ [7]_
    Copy on Write can allow forked subprocesses to share more memory and
    reduce overall memory footprint of a multiprocess application. However,
    due to the reference counting employed by CPython's garbage collection,
    accessing an object is effectively a modification triggering duplication
    into the child process. There is now the ability in CPython 3.7 to
    "freeze" objects making POSIX fork() calls more copy-on-write friendly,
    but it is not without caveats. [8]_ [9]_ [10]_

**list comprehension**
    Syntactic sugar for defining lists; commonly used to create lists based
    on another iterable such as applying checks to each member of another
    iterable to create a subset of elements which all satisfy a given
    condition.

**generator function**
    A function that yields computed values and behaves as an iterator; a use
    case would be to defer the code execution of the generator until it is
    iterated through, or to conserve memory by simply yielding the values
    rather than storing them.

**generators vs comprehensions**
    |link_generator_vs_comprehension| - The comprehension will create the
    entire list in memory first, while the generator will calculate individual
    items on the fly (also allowing it to handle infinite sequences).
    Typically speaking, you’ll want to use a generator if you are only
    iterating over the results a single time, or if you need to save storage
    space, or if you are writing coroutines. If you are iterating multiple
    times over the same data, you want to use a comprehension since the result
    is stored.

**decorators**
    A decorator is simply a function (well normally a function, but
    technically a callable object) that takes at least a function as an
    argument, but can also take additional parameters, and returns a
    replacement function. This allows it to wrap the argument function and
    modify the input and/or output of the ‘wrapped’ function.

**pseudo-private name mangling**
    Private name mangling: When an identifier that textually occurs in a
    class definition begins with two or more underscore characters and does
    not end in two or more underscores, it is considered a private name of
    that class. Private names are transformed to a longer form before code is
    generated for them. The transformation inserts the class name in front of
    the name, with leading underscores removed, and a single underscore
    inserted in front of the class name. For example, the identifier __spam
    occurring in a class named Ham will be transformed to _Ham__spam. This
    transformation is independent of the syntactical context in which the
    identifier is used. If the transformed name is extremely long (longer
    than 255 characters), implementation defined truncation may happen. If
    the class name consists only of underscores, no transformation is done.

**metaclasses**:
    *   |link_metaclass_primer|
    *   |link_understanding_metaclasses|

**single-quotes vs double-quotes**:
    The difference is that using one allows you to include the other
    un-escaped.

namedtuple
multiprocessing
logging
queues
lambda
gevent, twisted, tornado
pickle for mp

collections
itertools
functools

database getting hammered, what do you do?
cache responses just make sure you have cache invalidation on updates

after you cache, then what if response times are still low?
load balance your application with multiple instances
use something like gevent for async request processing

after load balancing and clustering, code bottlenecks and performance profiling

import exception order
old/new style class differences
class level attribute overrides
variables as references to objects
Scopes and closures
mutability vs immutability (with function parameters)


multiprocessing
- cannot use pickle because its so slow
- can use shared memory, but then the process would need to inherit it
- can use process pool if you can preallocate all the shared memory
- don't continuously start processes or you will slow down from overhead
- can use ctypes to efficiently share data between processes
- cannot share memory (without posix lib) after process has started
- can use something like sockets or redis to share data between processes


References
----------------------

.. [1] `GIL <https://wiki.python.org/moin/GlobalInterpreterLock>`_

.. [2] `What is the Python GIL? <https://realpython.com/python-gil/>`_

.. [3] `Global Interpreter Lock <https://en.wikipedia.org/wiki/Global_interpreter_lock>`_

.. [4] `Has the GIL been slain? <https://hackernoon.com/has-the-python-gil-been-slain-9440d28fa93d>`_

.. [5] `Python vs Copy on Write <https://llvllatrix.wordpress.com/2016/02/19/python-vs-copy-on-write/>`_

.. [6] `Garbage collection in Python <https://rushter.com/blog/python-garbage-collector/>`_

.. [7] `Python Memory Management <https://realpython.com/python-memory-management/>`_

.. [8] `Dismissing Python Garbage Collection at Instagram <https://instagram-engineering.com/dismissing-python-garbage-collection-at-instagram-4dca40b29172>`_

.. [9] `Copy-on-write friendly Python garbage collection <https://instagram-engineering.com/copy-on-write-friendly-python-garbage-collection-ad6ed5233ddf?gi=4a5d30d9247a>`_

.. [10] `Reference counting and garbage collection in Python <https://alex.dzyoba.com/blog/arc-vs-gc/>`_


.. |link_generator_vs_comprehension| raw:: html

    <a href="https://stackoverflow.com/questions/47789/generator-expressions-vs-list-comprehension" rel="external noopener noreferrer">Generator vs Comprehension</a>

.. |link_metaclass_primer| raw:: html

    <a href="https://jakevdp.github.io/blog/2012/12/01/a-primer-on-python-metaclasses/" rel="external noopener noreferrer">A Primer on Python Metaclasses</a>

.. |link_understanding_metaclasses| raw:: html

    <a href="https://blog.ionelmc.ro/2015/02/09/understanding-python-metaclasses/" rel="external noopener noreferrer">Understanding Python Metaclasses</a>
