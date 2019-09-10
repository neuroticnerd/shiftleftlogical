:date: 2019-09-09
:modified: 2019-09-09

================
Bash Notes
================

*NOTE: most of this is likely to be relevant to other shells as well, but it
is only tested or intended for Bash use.*


Find largest files when there is insufficient disk space
-------------------------------------------------------------------------------

A little caveat of some coreutils like ``sort`` is that they may write to
a temp file behind the scenes to do their work. Normally this would be fine,
but if you have a system that has run out of disk space, it can make it
difficult to find large files taking up space. To find the largest files
you can use the ``du`` command, then ``sort`` its output before using ``head``
to limit the number of results:

.. code-block:: bash

    sudo du -ka / | sort -n -r -S 10000000 | head -n 100
