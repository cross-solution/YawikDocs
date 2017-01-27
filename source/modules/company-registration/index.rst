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

This removes the directory `YawikCompanyRegistration` and all it content from your `module` directory of your YAWIK
installation.

Configuration
^^^^^^^^^^^^^

The registration form contains by default the fields:

* gender
* name
* email
* organizationName
* postalCode
* city
* street
* houseNumber
* phone

You can configure the registration form. Copy the `RegistrationFormOptions.config.local.php.dist`_ into your `autoload`
directory and adjust the values.

.. _RegistrationFormOptions.config.local.php.dist: https://github.com/cross-solution/YawikCompanyRegistration/blob/develop/config/RegistrationFormOptions.config.local.php.dist


