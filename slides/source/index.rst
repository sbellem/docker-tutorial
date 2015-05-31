
.. Learning Docker slides file, created by
   hieroglyph-quickstart on Tue May 26 01:31:39 2015.


Learning Docker
===============

**PyData Berlin 2015**

*Sylvain Bellemare*

`@sbellem <https://twitter.com/sbellem>`_


Thanks
======

.. rst-class:: build

* Valentin & Philipp
* PyData Berlin
* PyData community
* To you, the audience, for attending this tutorial


``whoami``
==========

.. rst-class:: build

* Live in the `ultimate multiverse <http://en.wikipedia.org/wiki/Mathematical_universe_hypothesis>`_ 
* Bachelor in Computer Science, with "minor+" in Physics
* Undergraduate research assistantship:
   * Computational High Energy Physics (FeynArts)
   * AI, NLP: Automatic Text Summarization
* python, django, elasticsearch, rabbitmq, saltstack, etc


Goal of this tutorial
=====================

.. rst-class:: build

* learning to use docker

Tutorial approach
=================

.. rst-class:: build

* "`Feynman's babylonian mathematics <https://www.youtube.com/watch?v=YaUlqXRPMmY>`_"


Rough Outline
=============

.. rst-class:: build

* Docker Installation
* Docker Hub
* Docker Images
* Docker Containers

.. nextslide::
        
.. rst-class:: build

* Linking Containers
* Managing Data in Containers
* Docker Compose


What is Docker?
===============

.. rst-class:: quote

   *"Docker is an open platform for developers and sysadmins
   to build, ship, and run distributed applications."*

   -- https://www.docker.com/whatisdocker/


Installation
============

Follow the instructions, for your OS, at:

* https://docs.docker.com/installation/#installation

.. note:: before anything, let's just make sure everyone is set and has docker installed


Check the installation
======================

.. rst-class:: build

* .. code-block:: bash

   $ docker version

* .. code-block:: bash

   $ docker help


Docker Hub
==========

.. rst-class:: build

* Hosts public docker images
* Automated image builds and work-flow tools such as build triggers and web hooks
* Integration with GitHub and BitBucket

.. note:: useful to look at dockerfiles, how they're written, to extend images, etc

Register to Docker Hub
======================

.. rst-class:: build

* via the web at https://hub.docker.com/account/signup/
* via the command line:

   .. code-block:: bash

    $ docker login

* Login, via the web or via the command line, or both


``docker images``
=================
.. rst-class:: build

* https://docs.docker.com/terms/image/
* .. code-block:: bash
 
   $ docker images --help

   Usage: docker images [OPTIONS] [REPOSITORY]

   List images
   
   # Run it! And see the options!

.. nextslide::

.. rst-class:: build

* let's try it ...

* .. code-block:: bash
 
   $ docker images
   # hmmm ... maybe nothing ...


``images`` option: ``--all``
============================
.. rst-class:: build

* .. code-block:: bash

   -a, --all=false
      Show all images (default hides intermediate images)

* .. code-block:: bash
 
   $ docker images --all
   # hmmm ... maybe still nothing ...


``docker search``
=================

.. rst-class:: build

* .. code-block:: bash

   $ docker search --help
   
   Usage: docker search [OPTIONS] TERM

   Search the Docker Hub for images

   # Run it! And see the options!


simple ``search`` examples
==========================

.. rst-class:: build

* .. code-block:: bash

   $ docker search busybox

* .. code-block:: bash

   $ docker search ubuntu

* .. code-block:: bash

   $ docker search python


``search`` option: ``--stars``
==============================

.. rst-class:: build

* .. code-block:: bash

   -s, --stars=0        Only displays with at least x stars

* .. code-block:: bash

   $ docker search --stars=15 python


``search`` option: ``--no-trunc``
=================================

.. rst-class:: build

* .. code-block:: bash

   --no-trunc=false     Don't truncate output

* .. code-block:: bash

   $ docker search --no-trunc --stars=15 python


``search`` option: ``--automated``
==================================

.. rst-class:: build

* .. code-block:: bash

   --automated=false    Only show automated builds

* .. code-block:: bash

   $ docker search --automated --stars=15 python


"official" images
=================
.. rst-class:: build

* *"The Docker Official Repositories are a curated set of Docker repositories that are promoted on Docker Hub."*
* doc: https://docs.docker.com/docker-hub/official_repos/
* github: https://github.com/docker-library/official-images


``docker pull``
===============

.. rst-class:: build

* .. code-block:: bash

   $ docker pull --help

   Usage: docker pull [OPTIONS] NAME[:TAG|@DIGEST]

   Pull an image or a repository from the registry

   # Run it! And see the options!


simple ``pull`` example
=======================

.. rst-class:: build

* .. code-block:: bash

   $ docker pull busybox

* .. code-block:: bash

   $ docker images

* .. code-block:: bash

   $ docker images --all


``pull`` option: ``--all-tags``
===============================

.. rst-class:: build
   
* .. code-block:: bash
  
   -a, --all-tags=false    Download all tagged images in the repository

* .. code-block:: bash

   $ docker pull --all-tags busybox

* .. code-block:: bash

   $ docker images

* .. code-block:: bash

   $ docker images --all


``docker rmi``
==============

.. rst-class:: build

* .. code-block:: bash

   $ docker rmi --help

   Usage: docker rmi [OPTIONS] IMAGE [IMAGE...]

   Remove one or more images

   # Run it! And see the options!


``docker rmi`` example
======================

.. rst-class:: build

* let's just list images first ...
* .. code-block:: bash

   $ docker images
   REPOSITORY  TAG            IMAGE ID       CREATED       VIRTUAL SIZE
   busybox     ubuntu-14.04   32e97f5f5d6b   5 weeks ago   5.609 MB
   busybox     ubuntu-12.04   faf804f0e07b   5 weeks ago   5.455 MB
   # ...


.. nextslide::
.. rst-class:: build

* let's remove ``busybox:ubuntu-12.04`` ...
* .. code-block:: bash

   $ docker rmi faf804f0e07b
   Untagged: busybox:ubuntu-12.04
   Deleted: faf804f0e07b2936e84c9fe4ca7c60a6246cc669cf2ff70969f14a9eab6efb48
   Deleted: 7171b530b3c69f9cbc2b9893bbad8b726230515cb0c0886721ae7e5c1cee6df3


.. nextslide::
.. rst-class:: build

* let's list images again ...
* .. code-block:: bash

   $ docker images
   REPOSITORY  TAG                  IMAGE ID       CREATED        VIRTUAL SIZE
   busybox     ubuntu-14.04         32e97f5f5d6b   5 weeks ago    5.609 MB
   # busybox:ubuntu-12.04 is gone ... 
   busybox     buildroot-2014.02    8c2e06607696   5 weeks ago    2.433 MB
   # ...


``images`` option: ``--quiet``
==============================
.. rst-class:: build

* .. code-block:: bash

   -q, --quiet=false    Only show numeric IDs

* .. code-block:: bash
 
   $ docker images --quiet


clean up trick
==============

.. rst-class:: build

* use case: we wish to delete all images (credit: `John Willis <https://twitter.com/botchagalupe>`_)
   .. @botchagalupe)

* .. code-block:: bash

   $ docker images --quiet

* .. code-block:: bash

   $ docker rmi $(docker images --quiet)

* .. code-block:: bash

   $ docker images



Pulling some Docker images
==========================

.. rst-class:: build

* .. code-block:: bash

   $ docker pull ubuntu
   $ docker pull jupyter/notebook
   $ docker pull postgres
   $ docker pull elasticsearch
   $ docker pull sequenceiq/spark
   $ docker pull tutum/mongodb

``docker ps``
=============

.. rst-class:: build

* .. code-block:: bash

   $ docker ps --help

   Usage: docker ps [OPTIONS]

   List containers

   # Run it! And see the options!


``docker run``
==============

.. rst-class:: build
 
* .. code-block:: bash
   
   $ docker run --help

   Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

   Run a command in a new container

   # Run it! And see the multiple options!


.. nextslide::

* .. code-block:: bash

   $ docker run jupyter/notebook

* .. code-block:: bash
   
   $ docker ps

* .. code-block:: bash

   $ docker ps -a


``run`` option:  ``--interactive``
==================================

.. rst-class:: build

* .. code-block:: bash

   -i, --interactive=false    Keep STDIN open even if not attached

* .. code-block:: bash

   $ docker run --interactive jupyter/notebook

* .. code-block:: bash
   
   ls
   python --version
   ipython
   # ...
   exit

.. nextslide::

.. rst-class:: build

* .. code-block:: bash

   $ docker ps

* .. code-block:: bash

   $ docker ps -a
   CONTAINER ID   IMAGE             COMMAND        CREATED           STATUS      PORTS    NAMES
   5161cebd44e8   jupyter/notebook  "/bin/bash"    15 minutes ago    Exited (0)           abc

``docker rm``
=============

.. rst-class:: build

* .. code-block:: bash

   $ docker rm --help

   Usage: docker rm [OPTIONS] CONTAINER [CONTAINER...]

   Remove one or more containers

   # Run it! And see the options!

.. nextslide::

.. rst-class:: build

* .. code-block:: bash

   $ docker rm 5161cebd44e8


``run`` option:  ``--tty``
==========================

.. rst-class:: build

* .. code-block:: bash

   -t, --tty=false            Allocate a pseudo-TTY

* .. code-block:: bash

   $ docker run --tty jupyter/notebook

* no stdin!


``docker run -i -t``
====================
 
.. rst-class:: build

* .. code-block:: bash

   $ docker run -i -t jupyter/notebook
   root@48ac97aa16cd:/tmp#


``run`` option:  ``--rm``
=========================

.. rst-class:: build

* .. code-block:: bash

   --rm=false        Automatically remove the container when it exits

* .. code-block:: bash

   $ docker run --rm -it jupyter/notebook
   root@48ac97aa16cd:/tmp#


``run`` option:  ``--name``
===========================

.. rst-class:: build

* .. code-block:: bash

   --name=                    Assign a name to the container

* .. code-block:: bash

   $ docker run --name=nb jupyter/notebook

* .. code-block:: bash
   
   $ docker ps -a

* .. code-block:: bash
   
   $ docker rm nb

``docker run`` a command
========================

.. rst-class:: build

* .. code-block:: bash

   $ docker run -t --name=nb jupyter/notebook ipython


``Dockerfile``
==============

We can build an image from a ``Dockerfile``

.. nextslide::

Let's write one, for the notebook, FROM ``ubuntu``


``docker history``
==================

.. rst-class:: build

* .. code-block:: bash
  
   $ docker history --help

   Usage: docker history [OPTIONS] IMAGE

   Show the history of an image


Different Ways of Dockerizing the Notebook
==========================================

.. rst-class:: build

* ``FROM ubuntu`` ...
* ``FROM python`` ...
* ``FROM jupyter/notebook`` ... 
* ``FROM continuumio/anaconda`` ...


.. note:: ``FROM ubuntu`` write everything
   * ``FROM python`` ... write the rest ...
   * ``FROM ipython/ipython`` ... write missing stuff
   * ``FROM ipython/notebook`` ... just run it
   * ``FROM jupyter/notebook`` ... run it with command "ipython notebook ..."
   * ``FROM continuumio/anaconda`` ... add to Dockerfile




Viewing the logs for a container
================================

.. code-block:: bash
   
   $ docker logs container


Dockerizing elasticsearch
=========================
.. code-block:: bash

   $ docker run --name es -d -P elasticsearch 
 
Interacting with elasticsearch via our Notebook
===============================================
.. code-block:: bash
 
   $ docker run --name es-nb -d -P -v \
   $PWD/notebooks:/notebooks anaconda-notebook

Detached mode
=============

.. code-block:: bash

   $ -d, --detach=false         Run container in background and print container ID

Port mapping
============

.. code-block:: bash
 
   -P, --publish-all=false    Publish all exposed ports to random ports
   -p, --publish=[]           Publish a container's port(s) to the host


Volume mapping
==============

.. code-block:: bash

   -v, --volume=[]            Bind mount a volume

Docker Volumes
==============

* Image with VOLUME

.. note:: show difference between Dockerfile with VOLUME and one without, commit container with
   one python notebook in a volume and another outside volume, and see how new image only preserved
   the one outside the volume ...


Clean up tricks
===============

.. rst-class:: build

* Stop all running containers 
* Delete all remaining (exited) containers


Stop all running containers
===========================

.. rst-class:: build

* .. code-block:: bash
   
   $ docker stop $(docker ps -q)


Delete all stopped containers
=============================

.. rst-class:: build

* .. code-block:: bash
   
   $ docker rm $(docker ps -aq)


Dockerizing Postgres
====================

.. rst-class:: build

* .. code-block:: bash

   $ docker run --name pg -d -P postgres

Linking Postgres to our Notebook
================================
 

Clean Up Tips
=============
https://twitter.com/jpetazzo/status/347431091415703552

remove old containers:

.. code-block:: bash

   $ docker ps -a | grep 'weeks ago' \
   | awk '{print $1}' | xargs docker rm

remove untagged images:

.. code-block:: bash

   $ docker images | grep '^<none>' \
   | awk '{print $3}' | xargs docker rmi


References
==========

* docs: https://docs.docker.com/
* layers: https://docs.docker.com/terms/layer/
* OS X: https://coderwall.com/p/w-zk9w/increase-boot2docker-space-allocation-in-osx
