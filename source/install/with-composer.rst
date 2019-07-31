Installation with composer
^^^^^^^^^^^^^^^^^^^^^^^^^^

A YAWIK instance can be build with composer.

.. code-block:: sh

    composer create-project yawik/standard path/to/yawik

This will install YAWIK with all development dependencies. You can add additional modules with

.. code-block:: sh

    cd path/to/yawik
    composer require [modulename]

For a list of available modules, check https://packagist.org/?type=yawik-module

If you do not want to have all development dependencies on your production server, you need to copy all files
except the ``vendor`` directory and all directories under ``public``  from ``path/to/yawik`` to a new
directory. In this directory you then run

.. code-block:: sh

    composer install --no-dev

Alternatively you can create a new yawik project and copy the files ``config/modules.config.php`` and ``composer.lock`` from
``path/to/yawik``. Then run the ``composer install``

.. code-block:: sh

    composer create-project --no-dev path/to/yawik-production
    cd path/to/yawik-production
    cp path/to/yawik/config/modules.config.php ./config
    cp path/to/yawik/composer.lock path/to/yawik/composer.json .
    composer install --no-dev

Finally you need to transfer the ``path/to/yawik-production`` to your webserver.
For configuring apache to server YAWIK, please look in the section below.
Document root must be the ``public`` directory.
