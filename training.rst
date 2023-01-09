Prepare a training on OMERO
===========================

This chapter describes a setup of a training OMERO.server at 
your institution. Further, it gives an overview of the other training
resources as well as hints for trainers about how to present OMERO during a training session.

Resources
---------

- Community contributions and setups: `Github issue <https://github.com/ome/omero-guides/issues/107>`_.

- `Useful scripts <https://github.com/ome/training-scripts>`_ for setting up the training server.


Setup of scripts and OMERO.cli environment
------------------------------------------

- Clone the `training-scripts <https://github.com/ome/training-scripts>`_ repository::

    $ git clone https://github.com/ome/training-scripts.git

- Set up a OMERO.cli as specified under `CLI installation <https://docs.openmicroscopy.org/omero/latest/users/cli/installation.html>`_. Typically, this environment will be used on your local machine. Alternatively, you can use the OMERO.cli environment of the server you installed as specified below.

Spin up a training server
-------------------------

System requirements for an OMERO.server are specified in the `documentation <https://omero.readthedocs.io/en/stable/sysadmins/system-requirements.html>`_. All  training servers used by the OME Team run in VMs with CentOS 7.

We recommend to use the Ansible management software and use the provided Ansible playbook to install the OMERO.server for training, as this gives you the exact blueprint of the server setup used during trainings run by the OME Team.

You can use the exact `training ansible playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml>`_ used by the OME Team for their training server. Alternatively, you might take the approach suggested in POINT TO INSTALL, where a very simple playbook is suggested first and the more complex steps are added and explained gradually.

You also have the option to follow the server installation steps in the `sysadmin documentation <https://omero.readthedocs.io/en/stable/sysadmins/unix/server-installation.html>`_. In this case, you will have to install `Apps for OMERO.web <https://www.openmicroscopy.org/omero/apps/>`_ in separate, post installation steps. We recommend to install all apps listed on the webpage except OMERO.gallery and OMERO.mapr. 

In case any other installation method was used than `training ansible playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml>`_, you have to also set up the server configuration according to the `configuration block in the playbook <https://github.com/ome/prod-playbooks/blob/master/omero/training-server/playbook.yml#L47>`_.

Set up groups and users
-----------------------

Prepare groups and users as listed in the `provided template sheet <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/create_groups_users_setup>`_. Assuming you have the `template sheet <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/create_groups_users_setup>`_ in the same directory as the script `create_groups_users.sh <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/create_groups_users.sh>`_, you can run::

    $ SUDOER=trainer bash create_groups_users.sh

which will create 50 users in your database.
The users are members of four main OMERO.groups, which cover
the group permissions allowed in OMERO. The ``Read-annotate`` group ``Lab 1`` is the main group used in the trainings,
which contains most of the data.

Rename users to have first and last names of real people (the list of famous scientist names is used) running `the renaming script <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/rename_users.py>`_.

Import images
-------------

`Import data in-place <https://omero-guides.readthedocs.io/en/latest/upload/docs/import-cli.html#in-place-import-using-the-cli>`_ for all users using `import bash script <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/in_place_import_as.sh>`_ and the `publicly available data provided <https://downloads.openmicroscopy.org/images/>`_ or use your own data or `data downloaded from IDR <https://idr.openmicroscopy.org/about/download.html>`_. Shell into the machine where you have installed your OMERO.server (necessary for in-place import) and, assuming that you have for example your data in a folder `my-folder` which is visible from that machine::

    $ IMPORTTYPE=normal NUMBER=15 FOLDER=/path/to/my-folder bash in_place_import_as.sh

will in-place import the images from `my-folder` into a new Dataset named `my-folder` for user-1 through user-15.

To achieve a better reproducibility of your imports, you can use a `bulk file <https://omero-guides.readthedocs.io/en/latest/upload/docs/import-cli.html#bulk-import-using-the-cli>`_ pointing to a list of paths of the image files. Assuming you have for example the bulk file `idr0021-experimentA-bulk.yml <https://github.com/IDR/idr0021-lawo-pericentriolarmaterial/blob/master/experimentA/idr0021-experimentA-bulk.yml>`_ located on the filesystem you are working on, together with the corresponding `idr0021-experimentA-filePaths.tsv <https://github.com/IDR/idr0021-lawo-pericentriolarmaterial/blob/master/experimentA/idr0021-experimentA-filePaths.tsv>`_ file and the images as specified in the `idr0021-experimentA-filePaths.tsv <https://github.com/IDR/idr0021-lawo-pericentriolarmaterial/blob/master/experimentA/idr0021-experimentA-filePaths.tsv>`_ which you have edited accordingly, you can import::

    $ OMEUSER=trainer NUMBER=2 BULKFILE=/path/to/idr0021-experimentA-bulk.yml bash in_place_import_as.sh

to import the images for trainer-1 and trainer-2.

The `script <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/in_place_import_as.sh>`_ assumes by default `in-place imports <https://omero-guides.readthedocs.io/en/latest/upload/docs/import-cli.html#in-place-import-using-the-cli>`_. You can adjust it for "classsical", non-in-place import by deleting the ``--transfer=ln_s`` from the script lines or, if using the `bulk file <https://omero-guides.readthedocs.io/en/latest/upload/docs/import-cli.html#bulk-import-using-the-cli>`_ workflow, comment out the ``transfer`` line from the bulk file.

Image data can also be populated by a `Python script <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/idr_copy_plate.py>`_ which copies images as pixeldata (i.e. not the original images) from `IDR <http://idr.openmicroscopy.org/>`_ by default. You can adjust the `appropriate line <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/idr_copy_plate.py#L80>`_ to copy from other OMERO.servers. Note that the script is only creating `images of single T and Z <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/idr_copy_plate.py#L36>`_, and thus reducing the original images dimensions in case these are multi-z or T images::

    $ python idr_copy_plate.py trainer-1 --server $YOUR_SERVER_ADDRESS $PASSWORD $PLATE_ID

will copy the Plate with $PLATE_ID from IDR as trainer-1 into your server.


Import metadata
---------------

Import metadata from a CSV via `OMERO.web <https://omero-guides.readthedocs.io/en/latest/upload/docs/metadata-ui.html>`_ or `Command Line Interface <https://omero-guides.readthedocs.io/en/latest/upload/docs/metadata.html>`_.

Annotate images using training-scripts:

- `Copy Key-Value pairs <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/idr_get_map_annotations.py>`_ from IDR or other OMERO server. The command below will copy MapAnnotations from IDR to your server between images inside Projects with IDs 1 (in IDR) and 2 (in your server). The Project in your server is owned and the action is executed by `trainer-1`.::

    $ python idr_get_map_annotation.py trainer-1 $PASSWORD Project:1 Project:2 --server $YOUR_SERVER_ADDRESS

- `Add new Key-Value pairs <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/key_value_pairs.py>`_. The command below will add Key-Value pairs defined inside the script randomly to the images inside Datasets with name ``big-dataset`` for all 50 users in your server. The $PASSWORD for all the users must be the same.::

    $ python key_value_pairs.py $PASSWORD big-dataset --server $YOUR_SERVER_ADDRESS

- `Calibrate images <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/calibrate_images.py>`_. The command below will calibrate all the images within Dataset named ``western-blots`` to `0.33 micrometers per pixel <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/calibrate_images.py#L72>`_ for all 50 users in your server. The $PASSWORD for all the users must be the same.::

    $ python calibrate_images.py $PASSWORD western-blots --server $YOUR_SERVER_ADDRESS

- `Add timestamps <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/set_timestamps.py>`_. The command below will set timestamps on the timelapse images within Dataset named `timestamps` with `delta T of 300 seconds <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/set_timestamps.py#L71>`_ for all 50 users in your server. The $PASSWORD for all the users must be the same.::

    $ python set_timestamps.py $PASSWORD timestamp --server $YOUR_SERVER_ADDRESS

- `Propagate tags and ratings to all users <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/copy_tags_ratings.py>`_. Supposing that the ``trainer-1`` has a Dataset ``to-tag`` with Tags and Ratings on the images in the Dataset. Further, each user, such as ``user-1``, ``user-2`` has the same-named Dataset with equivalent images in it, but with no Tags and Ratings (a typical situation after a fresh import of images). The command below will link the Tags of ``trainer-1`` which are linked to the images in the ``to-tag`` Dataset to the corresponding images in the ``to-tag`` Datasets of the users. The links between the Tags and the Images will belong to each user. Also, the Ratings which are on the Images of the ``to-tag`` Dataset of ``trainer-1`` will be re-created for the corresponding Images of the users and will belong to those users.::

    $ python copy_tags_ratings.py to-tag $PASSWORD --server $YOUR_SERVER_ADDRESS

Add analytical metadata
-----------------------

Create an analysis results table using a script run from a 3rd party tool.
For example, you can run the `segmentation script <https://github.com/ome/omero-guide-fiji/blob/master/scripts/groovy/idr0021.groovy>`_ in the `scripting editor of Fiji <https://omero-guides.readthedocs.io/en/latest/fiji/docs/threshold_scripting.html>`_ on a Project in OMERO
containing Datasets with Images which creates an OMERO.table and a CSV file
with results and attaches these to that Project in OMERO.

These analytical results can be used to `showcase OMERO.parade <https://omero-guides.readthedocs.io/en/latest/parade/docs/omero_parade.html>`_.

Cleanup scripts
---------------

It might be of great advantage to be able to clean up in batches, but still selectively, metadata added to the images on your training server.

- `Delete ROIs <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/delete_ROIs.py>`_ on all Images inside Datasets of specified name for all users on the server who have such Datasets. In the example below, the Dataset's name is ``with-rois``. The $PASSWORD is the password of the user deleting the ROIs. The deleting user is ``trainer-1`` by default.::

    $ python delete_ROIs.py --datasetname with-rois --server $YOUR_SERVER_ADDRESS $PASSWORD

- `Delete Annotations <https://github.com/ome/training-scripts/blob/master/maintenance/scripts/delete_annotations.py>`_ on all Images inside Datasets of specified name for all users on the server who have such Datasets. In the example below, the Dataset's name is ``western-blots`` and the deleted annotation type is ``FileAnnotation``. All other annotation types such as ``TagAnnotation`` etc. will be preserved. The $PASSWORD is the password of the user deleting the ROIs. The deleting user is ``trainer-1`` by default.::

    $ python delete_annotations.py --anntype file  --namespace none --server $YOUR_SERVER_ADDRESS $PASSWORD western-blots