How to write a guide
====================

The OMERO guide is hosted on `readthedocs <https://readthedocs.org/>`_. 
This section describes on to create a new guide.

To create a new guide:
  - create a new repository on GitHub using the `template guide <https://github.com/ome/guide-template>`_
  - enable travis to it is automatically built when commits are pushed
  - add the new repository as a new project on `readthedocs <https://readthedocs.org/>`_
  - add the new repository as a subproject of `omero-guides <https://readthedocs.org/projects/omero-guides/>`_ using an alias e.g. omero-guide-figure has been added as figure
  - add it to the this repository as a submodule using the same alias.
  - insert the guide into one of the existing files or in a new file it is a new section.
