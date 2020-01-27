Add-ons for OMERO
=================

OMERO is a flexible platform offering various extension points e.g. Django based Web application or
Command Line Interface plugins. Those extensions are not installed by default when deploying OMERO.
They require some additional setup steps.

**Web extensions**
------------------

All the Web extensions can be installed using ``pip``. Check each app for configuration details.

:doc:`figure/docs/index`
~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: figure/docs/index.rst
    :start-line: 3
    :end-before: Contents

:doc:`fpbioimage/docs/index`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: fpbioimage/docs/index.rst
    :start-line: 3
    :end-before: Contents

:doc:`iviewer/docs/index`
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: iviewer/docs/index.rst
    :start-line: 3
    :end-before: Contents

:doc:`parade/docs/index`
~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: parade/docs/index.rst
    :start-line: 3
    :end-before: Contents

**CLI extensions**
------------------


.. toctree::
    :maxdepth: 1
    :hidden:

    figure/docs/index
    fpbioimage/docs/index
    iviewer/docs/index
    parade/docs/index
