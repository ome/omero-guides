# omero-guides

[![Documentation Status](https://readthedocs.org/projects/omero-guides/badge/?version=latest)](https://omero-guides.readthedocs.io/)

The documentation is deployed at [OMERO guides](https://omero-guides.readthedocs.io)

This a Sphinx based documentation. 
If you are unfamiliar with Sphinx, we recommend that you first read 
[Getting Started with Sphinx](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html).


This repository is the overarching repository for the various ome guide repositories.

How to build locally
--------------------

We recommend to install the dependencies in a virtual environment.

* Create an environment e.g. a [Conda](https://docs.conda.io/en/latest/) and activate it.
* Clone this repository.
* Go into the directory ``omero-guides``.
* Install the required dependencies:

  ``$ pip install -r requirements.txt``

Initializes the submodule.

* Run:

  ``$ git submodule update``

* Fetch the contents of the submodule:

  ``$ git submodule update --recursive --remote``

You should now ready to build the documentation, by running ``make html``.
The generated ``html`` files should now be available under ``_build``.
