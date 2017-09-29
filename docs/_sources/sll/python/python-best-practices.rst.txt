=========================
Code Style Guidelines
=========================

A lot of good information can also be found at the Hitchhikers Guide to
Python [10]_.


PEP 8
----------

For Python,
`PEP 8 <https://www.python.org/dev/peps/pep-0008>`_ [1]_ is the de-facto guide
for code style (a formatted and easier-to-read version can be found at
`pep8.org <http://pep8.org/>`_). It is a well-defined and
respected list of guidelines for code style that I recommend following whenever
possible. Certain projects may have legacy code, a lack of time to refactor old
code, or other reasons to deviate from PEP 8. In situations where possible,
new code being added should conform to PEP 8, and any ongoing deviations agreed
upon by the code contributors should be documented. In addition to documenting
alterations, they should be supported by configuration for your linting tools
(such as a ``setup.cfg`` file -- see the Flake 8 section below) that can be
shared amongst contributors.


The Zen of Python
----------------------

`The Zen of Python <https://www.python.org/dev/peps/pep-0020/>`_ [2]_
(officially known as
`PEP 20 <https://www.python.org/dev/peps/pep-0020/>`_
) is a short manifesto of sorts which embodies many of the core principles of
design and style which make writing and reading Python such a pleasant
experience. If you haven't already, it is recommended required reading!


Flake8
-----------------

The tool `Flake8 <http://flake8.pycqa.org/en/latest/>`_ [3]_ is an excellent
open source command line wrapper around multiple useful tools. Flake8 combines
PEP 8 style checking (``pycodestyle`` [4]_ package), ``pyflakes`` [5]_ checking
for code errors (it does not import so its safe to use on modules with
side-effects/monkeypatching), and McCabe complexity analysis (``mccabe`` [6]_).
Even if it is not feasible or desired to directly enforce any guidelines, I
encourage everyone to utilize Flake8 to sanitize existing files they are
working in and check new code being committed.

These tools support configuration via the ``setup.cfg`` file in the package
root. This means that if there any package-specific variations in
configuration, or things like deviations from PEP 8 you wish to support, they
can be reflected in ``setup.cfg``, which can be committed to source control and
stored in the package module itself for everyone to use.

At the time of writing, please note that Flake8 only uses the first config file
it finds, it is not hierarchical in transversing anscestor directories.
Hierarchical overriding of configuration is a requested feature that may be
implemented in a future version, but is not currently available.


Python 2 vs Python 3
----------------------

Code should be written for Python 3 wherever possible, but there may be
certain instances (AWS Lambda for example) where it will not be supported or
there is an existing codebase where circumstances make refactoring an
infeasible task. In these cases, I would recommend writing code as close as
possible to Python 3 compatibility, with the remaining gap closed by using
python-future [7]_ or (if necessary) six [8]_. There is also a handy cheat
sheet [9]_ detailing some ways of being able to keep code compatible simply
by how you write it.


Documentation
----------------------

(coming soon: gist = use docstrings + sphinx)
Logging

(coming soon: gist = always use logging module don't use print)
Resources and Links

(many of these can be found above, but there are a few additional ones as well)


Footnotes
----------------------

.. [1] `PEP 8 <https://www.python.org/dev/peps/pep-0008>`_
    is the de-facto Python coding style guide.

.. [2] `The Zen of Python <https://www.python.org/dev/peps/pep-0020/>`_
    is a short manifesto of Python principles.

.. [3] `Flake8 <http://flake8.pycqa.org/en/latest/>`_
    is a command line utility for checking code style.

.. [4] `pycodestyle <https://pycodestyle.readthedocs.io/en/latest/>`_
    (used to be called pep8 package)

.. [5] `pyflakes <https://github.com/PyCQA/pyflakes>`_

.. [6] `mccabe <https://github.com/pycqa/mccabe>`_

.. [7] `python-future <https://pypi.python.org/pypi/future>`_

.. [8] `six <https://pypi.python.org/pypi/six>`_

.. [9] `Python 2-3 Compatible Code Cheat Sheet <http://python-future.org/compatible_idioms.html>`_

.. [10] `The Hitchhiker's Guide to Python <http://docs.python-guide.org/en/latest/>`_
    has all sorts of information!
