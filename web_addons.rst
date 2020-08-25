OMERO.web extensions to view data
=================================

OMERO.web is a flexible Django-based Web platform offering extension points.
Those extensions are not installed by default when deploying OMERO.
They require some additional setup steps.


All the Web extensions can be installed using ``pip``. Check each app for configuration details.

:doc:`figure_guide:index`
~~~~~~~~~~~~~~~~~~~~~~~~~

OMERO.figure is a popular tool for creating figures from Images in OMERO. Image metadata can be used to facilitate figure creation.

:doc:`fpbioimage_guide:index`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OMERO.FPBioimage is a volumetric visualization tool. It is a wrapper around `FPBioimage <https://fpb.ceb.cam.ac.uk/>`__.

:doc:`iviewer_guide:index`
~~~~~~~~~~~~~~~~~~~~~~~~~~

OMERO.iviewe is a 2D viewer which can open and browse multi-t, multi-z and multi-channel images and allows to draw and edit Regions of Interest (ROIs) and perform some rudimentary image analysis. It also offers the ability to view several images at the same time and synchronize the view.

:doc:`parade_guide:index`
~~~~~~~~~~~~~~~~~~~~~~~~~

OMERO.parade is a data mining tool.

.. toctree::
   :maxdepth: 2
   :hidden:

   figure/docs/index
   fpbioimage/docs/index
   iviewer/docs/index
   parade/docs/index
