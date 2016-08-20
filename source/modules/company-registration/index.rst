.. index:: YawikCompanyRegistration

YawikCompanyRegistration
------------------------

If you want to offer the registration for companies, this module might be helpful. It offers a registration form with
additional fields. When a user registers, an user and an organization entity are created. This module requires the
"Oganizations" Module.


Installation
^^^^^^^^^^^^

.. code-block:: sh

    composer create-project cross-solution/yawik
    cd yawik
    composer require cross-solution/yawik-company-registration


This install the YawikCompanyModule into the `module` directory of your YAWIK installation. You can uninstall the module
via

.. code-block:: sh

    composer remove cross-solution/yawik-company-registration

This removes the directory `YawikCompanyModule` and all it content from your `module` directory of your YAWIK
installation.

.. note::

    Installing modules using composer should be seen as a feature preview. You have to set `"minimum-stability": "dev"`
    in your `composer.json` of your YAWIK installation to make this work.git pull
