Add-ons for OMERO
=================

OMERO is a flexible platform offering various extension points e.g. Django based Web application or
Command Line Interface plugins. Those extensions are not installed by default when deploying OMERO.
They require some additional setup steps.

Web extensions
--------------
All the Web extensions can be installed using ``pip``.

- :doc:`figure/docs/index` is a popular tool for creating figures from Images in OMERO. Image metadata can be used to facilitate figure creation.

- :doc:`fpbioimage/docs/index` is a volumetric visualization tool.

- :doc:`iviewer/docs/index` is a 2D image viewer allowing to visualize 5D images, draw ROIs and add annotation. It also offers a multi-view mode.

- :doc:`parade/docs/index` is a data mining tool.

.. toctree::
    :maxdepth: 1
    :hidden:

    figure/docs/index
    fpbioimage/docs/index
    iviewer/docs/index
    parade/docs/index
