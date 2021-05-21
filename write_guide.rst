How to write a guide
====================

The OMERO guide is hosted on `readthedocs <https://readthedocs.org/>`_. 
This section describes on to create a new guide.

To create a new guide:
  - Create a new repository on GitHub using the `template guide <https://github.com/ome/guide-template>`_.
  - Add the new repository as a new project on `readthedocs <https://readthedocs.org/>`_.
  - Add the new repository as a subproject of `omero-guides <https://readthedocs.org/projects/omero-guides/>`_ using an alias e.g. omero-guide-figure has been added as figure,
  - Add the new repository to the `omero-guides repository <https://github.com/ome/omero-guides>`_ as a submodule using the same alias.
  - Insert the guide into one of the existing files or in a new file it is a new section.
  - If you intend that the new repository contains a ``binder`` folder to generate an environment for analysis, create two new YAML workflow files from the templates `binder_badge.yml <https://github.com/ome/.github/blob/master/workflow-templates/binder_badge.yml>`_ and `repo2docker.yml <https://github.com/ome/.github/blob/master/workflow-templates/repo2docker.yml>`_  , then place these new files to ``.github/workflows``.
