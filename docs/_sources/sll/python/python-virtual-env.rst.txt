=======================
Utilizing virtualenv
=======================

Different projects, applications, or scripts may require different versions of
Python (e.g. 2.6 vs 2.7 vs 3.X) and can have different sets of dependencies.
Virtual environments are a great way of creating isolated spaces for
compartmentalizing specific Python versions and/or sets of package dependencies
for separate projects and applications.

This additionally prevents the global Python installs from becoming polluted
with a plethora of packages and incompatibilities between applications which
may require different versions of the same dependency that may lead to
conflicts or difficult-to-debug errors. It also avoids typical permissions
errors when managing global packages and makes removing a set of application
dependencies as simple as deleting the virtualenv directory.

*NOTE: While the prerequisites recommend the latest Python 2 and Python 3
installs, if there is a situation where you need a very specific version of
Python, as long as that version is installed and you know the path to the
Python executable then you can create a virtual environment for that version.*


Prerequisites
------------------------

*   First things first, make sure that you have the
    `latest version of Python 2 or Python 3 <https://www.python.org/downloads/>`_
    downloaded and installed (or just skip the manual download
    by installing via the appropriate package manager for your OS)

*   Next you'll need to make sure that
    `pip is installed <https://pip.pypa.io/en/stable/installing/>`_
    (it comes automatically with Python 2 >= 2.7.9 and Python 3 >= 3.4)

*   Ensure that pip and setuptools are updated: pip install -U pip setuptools


Setup
------------------------

Next we'll need to install the virtual environment packages:

.. code-block:: bash

    pip install -U virtualenvwrapper virtualenv

WINDOWS: if you are doing this on a windows box you will instead need to
install virtualenvwrapper-win and follow the
`directions here <https://github.com/davidmarble/virtualenvwrapper-win/>`_
(good luck!):

.. code-block:: bash

    pip install -U virtualenvwrapper-win virtualenv

While virtualenv can be used by itself, it is far easier to use the wrapper
package which makes creating, managing, and activating virtual environments a
far more pleasant experience.


Configuration
------------------------

WINDOWS: again, if you are doing this on a windows box, you should refer to
`these directions <https://github.com/davidmarble/virtualenvwrapper-win/>`_
since virtualenvwrapper, and hence this whole section, is only for
Bourne-compatible shells (have fun!)

Now that everything is installed, we need to configure our environment to
actually utilize it. The following needs to be added somewhere in your
``~/.bash_profile`` or your shell equivalent file:

.. code-block:: bash

    #######################################################
    ### virtualenv setup and shortcuts
    export PIP_REQUIRE_VIRTUALENV=true
    export WORKON_HOME="~/.envs"
    if [ -f /usr/local/bin/virtualenvwrapper.sh ]; then
      source /usr/local/bin/virtualenvwrapper.sh;
    fi
    alias mkvenv="mkvirtualenv"
    alias mkvenv3="mkvirtualenv -p python3"
    alias rmvenv="rmvirtualenv"
    alias lsvenv="lsvirtualenv"

Broken down, the export PIP_REQUIRE_VIRTUALENV=true actually prevents Python
packages from being installed globally unless a specific flag is passed to pip
to force it install anyway. What this does is it reminds you if you forget to
activate a virtual env, and prevents packages from being installed globally
unless you specifically go out of your way to do so.

The ``export WORKON_HOME="~/.envs"`` tells virtualenvwrapper the location where
you want it to create all of your virtual environments (this should NOT be
within a git repository as the env should NOT be committed with code). Modify
this export as needed for wherever you want it to use as the location.

The if statement is actually the most important part of the additions since it
is what actually initializes the wrapper whenever you start a shell session so
it can do its job. Without the wrapper script getting sourced, it will not work
correctly!

The remainder of the additions are aliases which I like to use, however they
are not strictly required if you do not wish to add them.


Managing envs
---------------

Basic usage for creating a virtual env is::

    mkvirtualenv <env-name>

For example::

    mkvirtualenv example

Or using the alias::

    mkvenv example

You can similarly list or remove environments using the aliases::

    lsvenv
    rmvenv example


Creating a Python 3 env
--------------------------

The alias from above can be used to quickly create a virtual env with the
system install version of Python 3::

    mkvenv3 example_env

Or using just virtualenvwrapper without the alias::

    mkvirtualenv -p python3 example_env


Using specific Python versions
----------------------------------

To use a specific version of Python in a virtual env, you need to explicitly
tell it which one via the -p flag:

.. code-block:: bash

    mkvirtualenv -p path/to/specific/version/of/python
    mkvenv -p path/to/specific/version/of/python

Activating/deactivating an env
-------------------------------------

When creating a virtual env, it will automatically be activated, however, to
activate an env that is not currently active, you use the workon command::

    workon example_env

Activating a virtual env gives you access to the installed packages in the env
and the normal Python executable found on the command line should be the
executable for the version of Python specified when the env was created (the
default Python install on the system if none was specified).
Deactivating an env

Leaving an env is also very simple::

    deactivate
