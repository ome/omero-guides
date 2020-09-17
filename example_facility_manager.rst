OMERO walkthrough for facility managers
=======================================

In this document, we go through a common workflow that an imaging facility manager who facilitates OMERO usage for others might follow:

 * Create and manage Groups and Users.
 * Import data for others.
 * Import large or heterogeneous data for others.
 * Manage data for others.
 * Set up OMERO for publication of data.
 * Get users started.


Administrate Groups and Users
-----------------------------

Click on the link below to get to the full content of this chapter. The excerpts of the chapter are highlighted below the link.

:doc:`introduction_guide:group-user-management`


This section will show how to manage groups and users using the graphical interface in OMERO.web and the command-line interface. Most of the following tasks below can only be done by users with some administrator privileges. 


Import for others using the Desktop application
-----------------------------------------------

Click on the link below to get to the full content of this chapter. The excerpts of the chapter are highlighted below the link.

:doc:`upload_guide:import-desktop-client`


This import section will show how to import data for another user, using OMERO.insight. The user importing the data needs to have some `admin or restricted-admin <https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html>`__ privileges.

The import for another user requires that the user doing the import has specific privileges. We will use the user importer1, this could be, for example, a facility manager.


Import large data using Command Line Interface
----------------------------------------------

Click on the link below to get to the full content of this chapter. The excerpts of the chapter are highlighted below the link.

:doc:`upload_guide:import-cli`


This chapter shows how to import data for another user, using Command Line Interface (CLI).

The user importing the data needs to have some `admin or restricted-admin <https://docs.openmicroscopy.org/latest/omero/sysadmins/restricted-admins.html>`__ privileges.


Manage data for others
----------------------

Click on the link below to get to the full content of this chapter. The excerpts of the chapter are highlighted below the link.

:doc:`introduction_guide:data-management`

In this document, we introduce the basic concepts of data management, such as browsing, navigating to others’ data, and changing the display of the images in OMERO. The example here uses OMERO.web, but majority of the features described here are also present in OMERO.insight.


Set up OMERO for publication of data
------------------------------------

Click on the link below to get to the full content of this chapter. The excerpts of the chapter are highlighted below the link.

:doc:`introduction_guide:data-publication`

Users can publish Image data to the world using OMERO. Here we describe some steps to facilitate that. The steps are to be done by an administrator or restricted administrator in OMERO.

Get users started
-----------------

Here we describe how to get users started. This is a walkthrough for a facility manager in charge of introducing new users to OMERO.

Step-by-Step
------------

#. Create the new user in OMERO and add them to the appropriate group(s) in OMERO. Consult the user and group creation sections of :doc:`introduction_guide:group-user-management`. In case your OMERO.server is set up for synchronization of logins with your institutional login system (LDAP), look for ``Managing LDAP Users`` in :doc:`introduction_guide:group-user-management`.

#. Explain to the user the basics of Group and User system in OMERO, drawing their attention to the importance of logging into the correct group when importing data. The user sets then their ``default group`` in OMERO correctly, as explained in :doc:`introduction_guide:group-user-management`, or you do it for the user.

#. Point the new user to the section explaining how to install and import data into OMERO using a Desktop client :doc:`upload_guide:import-desktop-client`.

#. Point the new user to the basic workflow example :doc:`example`. This will give them hints about the basic steps usually done when working with OMERO and how to go through them.

#. Explain to the user the data management and annotation possibilities in OMERO, as highlighted in :doc:`introduction_guide:data-management` and :doc:`introduction_guide:annotate`. 

#. Consult with the user the analysis possibilities when using 3rd party tools with OMERO, as listed in :doc:`external_tools`.

#. Mention :doc:`figure_guide:index`. This will help to raise the usage of OMERO in your institution.
