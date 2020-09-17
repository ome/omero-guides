OMERO walkthrough example
=========================

In this document, we go through a common workflow that a scientist wishing to use OMERO might follow:

 * Import data using the Desktop client.
 * View images using the OMERO.iviewer plugin.
 * Analyze images using a 3rd party tool, e.g. Fiji.
 * Generate a figure using OMERO.figure.



Import
------

:doc:`upload_guide:import-desktop-client`

In the first part, we first show how to import data by yourself and for yourself into OMERO using various import strategies. This will be mainly done using the OMERO.insight desktop client.

Second part of this import section will show how to import data for another user, using OMERO.insight. The user importing the data needs to have some `admin or restricted-admin <https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html>`__ privileges.

The import for another user requires that the user doing the import has specific privileges. We will use the user importer1, this could be, for example, a facility manager.

View
----

:doc:`iviewer_guide:iviewer_viewing`

We introduce OMERO.iviewer, a 2D viewer which can open and browse multi-t, multi-z and multi-channel images and allows to draw and edit Regions of Interest. It also offers the ability to view several images at the same time and synchronize the view.

Inspect intensities, draw and evaluate ROIs
-------------------------------------------

:doc:`iviewer_guide:iviewer_rois`

@e cover the ability of OMERO.iviewer to work with ROIs, to draw, edit, annotate and evaluate ROIs in the images is shown. In this way, a simple image analysis can be achieved, such as getting the intensity measurements inside the pixels of the ROIs and sizes of the ROIs, such as areas for polygons and lengths for lines and polylines.

Analyze
-------

:doc:`fiji_guide:manual_analysis`

The following workflows should work both with ImageJ and Fiji, after these have been correctly set up with the OMERO plugin for Fiji/ImageJ.

Present or publish data
-----------------------

:doc:`figure_guide:omero_figure`
