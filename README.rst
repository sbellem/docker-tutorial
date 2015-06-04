Learning Docker
===============

A very basic and simple introduction to `Docker`_, initially prepared for
`PyData Berlin 2015 <http://pydata.org/berlin2015/>`_. It must be emphasized
that the tutorial was designed for people with ideally no prior exposure to
`Docker`_. However, it is not ruled out that more advanced material may be
added in the near future.

This repository contains:

* the `slides`_ used for the tutorial, at the conference
* different `dockerfiles`_ to build docker images -- most notably, to run the
  ipython/jupyter notebook
* jupyter `notebooks`_ that can be used to test that the docker container(s)
  are running as expected
* a simple `docker-compose`_ example, in which a containerized jupyter
  notebook is linked to a containerized postgres database


.. _docker: https://www.docker.com/
.. _slides: https://github.com/sbellem/docker-tutorial/tree/master/slides
.. _dockerfiles: https://github.com/sbellem/docker-tutorial/tree/master/dockerfiles
.. _notebooks: https://github.com/sbellem/docker-tutorial/tree/master/notebooks
.. _docker-compose: https://github.com/sbellem/docker-tutorial/tree/master/docker-compose
