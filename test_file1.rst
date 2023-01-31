.. _getting_started:

Getting started
###############
The instructions mentioned on this page is a one time setup (per workspace). Two installation/setup methods are provided below. First is the manual option.  This is for those who may want to integrate into their native development evnironment.  The second option is to install in docker. This will mean having Docker available on your development system.

.. _docker_installation:
Docker Install
##############

This repo has been developed to aid developers in quickly setting up an initial TRS development environment. Leveraging this repo, with just a few steps you can have a trs-development environment running in a docker container. The benefits of using a container for your development environment include quickly reproducing your environment in the event of distaster recovery or development environment corruption, speed of setup, all devs in a similar environment, can be customized/extended to meet your needs, usable across different host platforms, and more.  

Tested Environments
*******************
The instructions/scripts in this section have been verified against Ubuntu 20.04 desktop machine and a share server environment also based on Ubuntu 20.04

Pre-requisits
*************
- Assure that Docker has been installed on your Host development machine
.. code-block:: bash
    ~/dev$: docker --version;
    Docker version 20.10.19, build d85ef84;

.. note::
   These instructions assume the user name is "dev"

Installation instructions
*************************
1. Clone the TRS repository (Host)
==================================

.. code-block:: bash
    $ cd ~
    $ mkdir trs-repo
    $ cd trs-repo
    $ git clone https://gitlab.com/Linaro/trusted-reference-stack/trs.git
    $ cd trs
    $ git status
    On branch main
    Your branch is up to date with 'origin/main'.
    
    nothing to commit, working tree clean

2. Set up dev directory and clone the repo (Host)
=================================================

.. code-block:: bash
    $ cd ~
    $ mkdir trs-build
    $ cd trs-build

3. Copy the Dockerfile and scripts to the dev directory (Host)
==============================================================

.. code-block:: bash
    $ cd ~/trs-build
    $ cp ~/trs-repo/trs/scripts/docker-scripts/* .

4. Build Docker Image (Host)
============================
The instructions below creates a Dockerfile the named "trs" 

.. code-block:: bash
    $ cd ~/trs-build
    $ ls
    Dockerfile  run-trs.sh  trs-install.sh

    $ docker build -t trs .

The above defaults to a UID/GID of 1000/1000; typical of an Ubuntu Desktop.

If the host has a different UID/GID and it's desired for the container to have the same, used the following command:

.. code-block:: bash
    $ cd ~/trs-build
    $ ls
    Dockerfile  run-trs.sh  trs-install.sh

    $ docker build --build-arg USER_UID=$(id -u) --build-arg USER_GID=$(id -g) -t trs .

This will kick off a build of a new Docker image which will take a few minutes.

..note::
    During a docker build, it's not uncommon to see warnings such as the following that can be ignored:
    ``WARNING: apt does not have a stable CLI interface. Use with caution in scripts.``

5. Check for valid Docker images
================================
Assuming you had no other images, you should see soemthing similar to the following after completion of the docker build:

.. code-block:: bash
    $ docker images
    REPOSITORY   TAG       IMAGE ID         CREATED            SIZE
    trs          latest    2a10a95eacd2   10 seconds ago   336MB
    ubuntu       22.04     a8780b506fa4   4 weeks ago      77.8MB

6. Download and sync the TRS source using Repo tool

.. code-block:: bash
    $ cd ~
    $ mkdir trs_reference_repo
    $ cd trs_reference_repo
    $ repo init -u https://gitlab.com/Linaro/trusted-reference-stack/trs-manifest.git -m default.xml
    $ repo sync 

The location above is important as this is a shared folder between the Host and the Container. If the user chooses to change this location, the scripts/Dockerfile must be updated to align.

7. 


.. code-block:: bash
dev@2d0b8419dac3:~/trs-workspace$ history
    1  ls
    2  ls -l build/
    3  ls ..
    4  cd ../yocto_cache/
    5  ls
    6  ls sstate-cache/
    7  ls
    8  ls downloads/
    9  ls
   10  cd ..
   11  ls
   12  ls trs-reference-repo/
   13  pwd
   14  ls
   15  cd trs-workspace/
   16  ls
   17  ./trs-install.sh -h -r
   18  history
   dev@2d0b8419dac3:~/trs-workspace$ 


