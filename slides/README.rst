The ``Dockerfile`` included therein allows you to build the slides.

To build the image:

.. code-block:: bash

   $ docker build -t slides .

You can call the image whatever you wish, e.g., "slidezlab":

.. code-block:: bash

   $ docker build -t slidezlab .


There are probably various ways you can go about to build the slides. A few will be given here.

In most cases, you'll want to mount the host directories where the source rst files are, and where
the built html files end up.

Mounting the source rst files will allow you to make changes outside the container, meanwhile
building the slides inside the container with the most recent changes you made to the rst files,
outside the container.

Mounting the build directory where the html files are generated will allow you to view and preserve
the html files, even if the container and image are destroyed.

One way to build the slides could be:


.. code-block:: bash

   $ docker run --rm -v $PWD/build:/usr/src/slides/build slidezlab

The ``--rm`` flag will destroy the container after executing the default command ``make slides``,
which is specifiied in the ``Dockerfile``.

Let's say you made some modifications to ``source/index.rst``, so you can mount it so that these
changes are taken into consideration.

.. code-block:: bash

   $ docker run --rm -v $PWD/./:/usr/src/slides slidezlab


A different approach would be to have a bash session, and run ``make slides`` in that session:

.. code-block:: bash

   $ docker run --rm -it -v $PWD/./:/usr/src/slides slidezlab /bin/bash
   root@c7a0ae9bd220:/usr/src/slides# make slides

Once done, you can then exit the container, which will be destroyed automatically again because of
the ``--rm`` flag.

.. code-block:: bash

   $ root@c7a0ae9bd220:/usr/src/slides# exit

The newly generated slides should be under ``build/slides/``. You can open the slides, and view
them in a browser:

.. code-block:: bash

   $ open build/slides/index.html
