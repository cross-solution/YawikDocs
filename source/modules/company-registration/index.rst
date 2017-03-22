.. index:: CompanyRegistration

CompanyRegistration
-------------------

.. sidebar:: CompanyRegistration

   =======================  ==========================================
   ``Repository``            `yawik/CompanyRegistration`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

.. |coverage| raw:: html

	<a href='https://coveralls.io/github/yawik/CompanyRegistration?branch=develop'><img src='https://coveralls.io/repos/github/yawik/CompanyRegistration/badge.svg?branch=develop' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/CompanyRegistration"><img src="https://travis-ci.org/yawik/CompanyRegistration.svg?branch=master"></a>

If you want to offer the registration for companies, this module might be helpful. It offers a registration form with
additional fields. When a user registers, an user and an organization entity are created. This module requires the
"Oganizations" Module.


Installation
^^^^^^^^^^^^

to install the `yawik/CompanyRegistration`_ Module into a running YAWIK, change into the `YAWIK/modules` directory and clone
the yawik/CompanyRegistration repository.

.. code-block:: sh

 git clone https://github.com/yawik/CompanyRegistration

To activate the module create a php file named ``WhateverYouWant.module.php`` in your config autoload directory containing:

.. code-block:: php

 <?php
 return ['CompanyRegistration'];

.. _yawik/CompanyRegistration: https://github.com/yawik/CompanyRegistration


Another possibility to install YAWIK modules is using composer.

.. code-block:: sh

    composer create-project cross-solution/yawik
    cd yawik
    composer require cross-solution/yawik-company-registration


This install the CompanyModule into the `module` directory of your YAWIK installation. You can uninstall the module
via

.. code-block:: sh

    composer remove cross-solution/yawik-company-registration

This removes the directory `CompanyRegistration` and all it content from your `module` directory of your YAWIK
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

.. _RegistrationFormOptions.config.local.php.dist: https://github.com/yawik/CompanyRegistration/blob/develop/config/RegistrationFormOptions.config.local.php.dist


