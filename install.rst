Install an OMERO server
=======================

This chapter describes an installation of an OMERO.server and the most important post-installation steps, such as additional apps installation and LDAP configuration. The installation of the server on a local machine is not recommended, except for testing or development purposes. The workflow is aimed at system administrators intending to familiarize themselves with an OMERO installation.

Description
-----------

We will show here:


-  Where to find the OMERO.server requirements.

-  How to install OMERO.server quickly using a simple Ansible playbook example.

-  How to install OMERO.server very quickly using a provided Docker image.

-  How to configure OMERO.server to work with LDAP, both using Ansible or using manual configuration.

-  How to install applications such as OMERO.figure for OMERO.web.

Resources
---------

- Webpage  `Start with OMERO at your Institution <https://www.openmicroscopy.org/omero/institution/getting-started.html>`_
- `Ansible <https://www.ansible.com/>`_
- `Ansible documentation <https://docs.ansible.com/ansible_community.html>`_
- `Example <https://github.com/ome/omero-deployment-examples>`_ and `production <https://github.com/ome/prod-playbooks>`_ ansible playbooks.
- `OMERO installation workshop presentation <https://downloads.openmicroscopy.org/presentations/2020/Dundee/Workshops/OME2020-OMERO-Installation/#/>`_
- `Manual installation documentation <https://omero.readthedocs.io/en/stable/sysadmins/unix/server-centos7-ice36.html>`_.
- `System requirements <https://omero.readthedocs.io/en/stable/sysadmins/system-requirements.html>`_
- `List of Apps for OMERO.web and Command line plugins <https://www.openmicroscopy.org/omero/apps/>`_

Install a server
----------------

System requirements for an OMERO.server are specified in the `documentation <https://omero.readthedocs.io/en/stable/sysadmins/system-requirements.html>`_.
The workflows below were tested on CentOS 7 only.

Ansible
-------

For OMERO installation, we recommend to use the Ansible software suite which enables infrastructure as a code.

Install ansible (at the time of writing, the ansible-core version was 2.11.12, python version was 3.6.8). Other versions might work too, but are not routinely tested.::

    $ pip install ansible

Clone the repository for the one-node example::

    $ git clone https://github.com/ome/ansible-example-omero-onenode.git
    $ cd ansible-example-omero-onenode	

Install the requirements::

    $ ansible-galaxy install -r requirements.yml

Edit the file ``hosts.yml`` in the same directory and replace the YOUR-HOST-NAME variable with a name of your machine you prepared in the step above to install OMERO on, e.g. ``foo.example.com`` or ``localhost``)::

    all:
      hosts:
        YOUR-HOST-NAME 

Edit the ``playbook.yml`` file to change the OMERO root password (by default ``ChangeMe``). Then use this playbook to install PostgreSQL, OMERO.server and OMERO.web on one node::

    $ ansible-playbook --become -i hosts.yml playbook.yml

Start OMERO.insight or a Command Line Interface (CLI) and log in to ``YOUR-HOST-NAME`` with the username ``root`` and the password you have set in the ``playbook.yml`` above.

Go to ``https://YOUR-HOST-NAME:4080/webclient/`` in your browser and log in to OMERO.web with the same credentials used above for OMERO.insight. In case you are on the same machine where you installed your OMERO, go to `http://localhost:4080/webclient/ <http://localhost:4080/webclient/>`_ to access your OMERO.web locally.

Docker
------

Even quicker option than ansible is docker, but you have to be comfortable working with containers. The docker workflow below is written for local installation of OMERO only for convenience, but bear in mind that you will have to install OMERO on a remote server when going into production.

Assuming that Docker is installed, clone the deployment examples repository (if not already cloned)::

    $ git clone https://github.com/ome/omero-deployment-examples.git
    $ cd omero-deployment-examples
    $ git clone https://github.com/ome/docker-example-omero.git
    $ cd docker-example-omero

Pull the latest versions of the containers and start them::

    $ docker-compose pull
    $ docker-compose up -d
    $ docker-compose logs -f

Start OMERO.insight or a Command Line Interface (CLI) and log in to ``localhost`` as ``root`` with password ``omero``.

Go to `http://localhost:4080/webclient/ <http://localhost:4080/webclient/>`_ in your browser and log in to OMERO.web as ``root`` with password ``omero``.



Manual installation
-------------------

You also have the option to follow the manual server installation steps - see link in Resources section above. This way is harder then using Ansible or Docker, but you will understand the
server installation in-depth after this.


Configure LDAP
--------------

LDAP is an open standard for querying and modifying directory services that is commonly used for authentication, authorization and accounting (AAA). OMERO.server supports the use of an LDAP server to query (but not modify) AAA information for the purposes of automatic user creation.

This allows OMERO users to be automatically created and placed in groups according to your existing institution policies.



Install the apps
----------------

In order to give your users full OMERO experience, you might want to install apps after you successful OMERO.server and OMERO.web install above. Many user-facing features are released only as applications for OMERO.web, such as full image viewer and OMERO.figure.

1. Install the apps using Ansible: If you used Ansible to install your OMERO.server, we recommend to add the apps installation lines to your Ansible playbook. First, add the `block <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L23>`_ defining the ``omero_python_addons`` to your ``ome.omero_server`` role. These addons are necessary for OMERO.figure exports. Further, add the block which `defines the packages <https://github.com/ome/prod-playbooks/blob/929a4c4fefcffa3b8cebe65047aa32ddbfe0c5b7/omero/training-server/playbook.yml#L453>`_ to your ``ome.omero_web`` role. Furhter, `set the versions of Apps <https://github.com/ome/prod-playbooks/blob/929a4c4fefcffa3b8cebe65047aa32ddbfe0c5b7/omero/training-server/playbook.yml#L444>`_ to be installed - you do not have to use the ``override`` logic for that, just define your variables in a ``vars`` block at the end of your playbook such as::
    
    vars:
      omero_figure_release:"5.1.0"
      omero_fpbioimage_release:...
      ...    
    
`Configure <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L63>`_ the OMERO.iviewer to be the default viewer when the user double-clicks onto a thumbnail in OMERO.web and `set the namespace <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L65>`_ of the MapAnnotations to be considered by OMERO.mapr. Then, `enable the Open With feature <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L74>`_ for your installed Apps and add the `centre pane links <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L90>`_ for the user to be able to start OMERO.parade from OMERO.web. Lastly, add the `block defining the top links for OMERO.figure and OMERO.mapr <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L94>`_. In another block in your playbook, in a separate `task <https://github.com/ome/ansible-example-omero-addons/blob/cf8aa023c30c89c127d7be7ee96ed8ba94813dcb/playbook.yml#L120>`_ define the job of downloading the necassary script for OMERO.figure which exports the Figures as pdf. Then rerun the command::

    $ ansible-playbook --become -i hosts.yml playbook.yml

2. If you installed the OMERO.server manually, you can also install Apps manually according to LINK to APPS list in the website. But please note that if you used Ansible to install your server, it is not advisable to start making manual installs on top of this, as the next re-run of the Ansible playbook might invalidate the manual changes made.

Configure your server
---------------------

Depending on the environment and purpose of your server, you will need to configure your OMERO.server. If you for example intend to run a training on OMERO using your OMERO.server, you can add to the `omero_server_config_set block <https://github.com/ome/prod-playbooks/blob/929a4c4fefcffa3b8cebe65047aa32ddbfe0c5b7/omero/training-server/playbook.yml#L473>`_ the `four parameters <https://github.com/ome/prod-playbooks/blob/929a4c4fefcffa3b8cebe65047aa32ddbfe0c5b7/omero/training-server/playbook.yml#L479>`_ - the ``omero.db.poolsize`` and the 3 ``omero.jvmcfg...`` parameters.