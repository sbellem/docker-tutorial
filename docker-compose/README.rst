jupyter & postgres with docker-compose
======================================

.. code-block:: bash

   $ docker-compose build
   $ docker-compose up

To access the notebook, open another shell:

.. code-block:: bash
 
   $ docker-compose ps notebook
          Name                        Command               State            Ports
   -------------------------------------------------------------------------------------------
   dockercompose_notebook_1   /bin/sh -c ipython noteboo ...   Up      0.0.0.0:32768->8888/tcp

Notice what the port mapping is for the port ``8888``. In the example above it is ``32768``.

For the example above, the notebook could be accessed in a browser at ``<host_ip>:32768``, where
``<host_ip>`` is dependant on how you are running docker. If you run docker natively, (e.g. on
Ubuntu), then ``<host_ip>`` will simply be ``localhost``. If you run docker using boot2docker
(e.g. on Mac OS X), then you can run the command ``boot2docker ip`` in a shell to find out the
``<host_ip>``.
