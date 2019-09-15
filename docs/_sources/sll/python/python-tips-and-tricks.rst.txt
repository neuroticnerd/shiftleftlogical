==============================
Python Tips and Tricks (WIP)
==============================


Create ``virtualenv`` Without Internet
-------------------------------------------------------------------------------

To create the virtualenv without it choking, you will first need to
pre-download the wheels of at least pip, setuptools, and wheel packages, then
you can use the following:

.. code-block:: bash

    virtualenv --python=<python-to-use> --no-download --extra-search-dir=/path/to/preinstall/wheels ENV_NAME

Now to install local packages you can:

.. code-block:: bash

    pip install --no-index --find-links=/path/to/pre-downloaded/packages <package-to-install>
    # --or--
    pip install --no-index --find-links=/path/to/pre-downloaded/packages -r requirements.txt

I’ve used these myself for a Raspberry Pi that didn’t have an internet connection yet.


``defaultdict`` with ``functools.partial`` for arguments
-------------------------------------------------------------------------------

You can create a ``defaultdict`` instance which will create objects with a
specific structure (``OrderedDict`` is a great use-case) by using
``functools.partial`` to initialize the object since ``defaultdict`` will
construct it without any arguments:

.. code-block:: python

    def get_defaultdict_schema():
        return OrderedDict([
            ('stuff', None),
            ('things', defaultdict(functools.partial(OrderedDict, [
                ('one_fish', None),
                ('two_fish', None),
                ('red_fish', None),
                ('blue_fish', False),
                ('enabled', True),
            ]))),
            ('enabled', True),
        ])

    def get_nested_defaultdict_schema():
        return defaultdict(functools.partial(OrderedDict, [
            ('stuff', None),
            ('things', defaultdict(functools.partial(OrderedDict, [
                ('one_fish', None),
                ('two_fish', None),
                ('red_fish', None),
                ('blue_fish', False),
                ('enabled', True),
            ]))),
            ('enabled', True),
        ]))


Code Profiling
-------------------------------------------------------------------------------

You can use the ``cProfile`` module in Python to perform code profiling, then
print out the information after your code has run:

.. code-block:: python

    import cProfile
    import pstats
    profiler = cProfile.Profile()
    profiler.enable()
    log.warning('PROFILING IS ENABLED!')

    # DO STUFF YOU WANT TO PROFILE HERE

    profiler.disable()
    sortby = 'tottime'
    stats_stream = io.StringIO()
    stats = pstats.Stats(
        profiler, stream=stats_stream
    ).sort_stats(sortby)
    stats.print_stats()
    stats_lines = stats_stream.getvalue().split('\n')
    log.info('\n'.join(itertools.chain.from_iterable([
        ['\n'], [stats_lines[0]], stats_lines[4:25]
    ])))
