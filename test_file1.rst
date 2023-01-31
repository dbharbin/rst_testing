. _getting_started:

Getting started
###############
The instructions mentioned on this page is a one time setup (per workspace).

1. Install repo
***************
Note that here you don’t install a huge SDK, it’s simply a Python script that
you download and put in your ``$PATH``, that’s it. Exactly how to “install”
repo, can be found at the Google `repo`_ pages, so follow those instructions
before continuing.

2. Getting the source code
**************************
Now we will check out code for the TRS. This step is light weight and only check
out code necessary to build TRS. There are two flavors right now, either you
checkout the one tracking lastest on all gits or you'll checkout a certain
release (the difference is in the ``repo init`` line, as highlighted).

For latest, do this
===================

.. code-block:: bash
   :emphasize-lines: 3

    $ mkdir trs-workspace
    $ cd trs-workspace
    $ repo init -u https://gitlab.com/Linaro/trusted-reference-stack/trs-manifest.git -m default.xml
    $ repo sync -j3

For a specific release, do this
===============================

.. code-block:: bash
   :emphasize-lines: 3

    $ mkdir trs-workspace
    $ cd trs-workspace
    $ repo init -u https://gitlab.com/Linaro/trusted-reference-stack/trs-manifest.git -m default.xml -b <release-tag>
    $ repo sync -j3

.. _prerequisites:

3. Installing prerequisites
***************************
TRS depends on a couple of packages that needs to be present on the host system.
These are installed as distro packages and using Python pip.

Host packages
=============
.. tabs::

    .. tab:: Ubuntu / Debian

        **Host / apt packages**

        This will require your **sudo** password, from the root of the
        workspace:

        .. code-block:: bash

            $ cd <workspace root>
            $ make apt-prereqs

        This will install the following packages:

        .. literalinclude:: ../../scripts/apt-packages.txt
            :language: text


    .. tab:: Arch Linux

        .. warning::
            Just boiler plate, no complete instructions. Only Ubuntu versions
            tested so far.

        Install the necessary packages using pacman.

        ..
          [NEEDS_TO_BE_FIXED] - Add correct pre-req packages

        .. code-block:: bash

            $ sudo pacman -Syy
            $ sudo pacman -S git

    .. tab:: Fedora

        .. warning::
            Just boiler plate, no complete instructions. Only Ubuntu versions
            tested so far.

        Install the necessary packages using dnf.

        ..
          [NEEDS_TO_BE_FIXED] - Add correct pre-req packages

        .. code-block:: bash

            $ sudo dnf update
            $ sudo dnf install git
            
Python packages
===============

By default all python packages will be installed at ``<workspace
root>/.pyvenv`` using a virtual Python enviroment. The benefits by doing
so is that if we delete the ``.pyvenv`` folder, there will be no traces
left of the Python packages needed for TRS. It can eventually also avoid
clashing with tools needing other versions of some Python packages.

.. code-block:: bash

    $ cd <workspace root>
    $ make python-prereqs

4. Building
***********
