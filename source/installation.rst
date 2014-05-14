Installation
============

Requirements
------------

you need at least a webserver, a mongo database and PHP. We're developing using 
apache with mod_php5 enabled. If you don't have a local mongoDB availabe you can
try a provider like mongolab.com_ or mongosoup.de_.

.. _mongolab.com: https://mongolab.com/welcome/
.. _mongosoup.de: https://www.mongosoup.de/

* php 5.3.*
* Zend Framework 2.2.*
* mongodb 2.4.*
* php5-mongo
* php5-intl

Setup
-----

.. code-block:: sh

  git clone https://github.com/cross-solution/CrossApplicantManager
  cd CrossApplicantManager
  make install

this will download composer_ for installing missing libraries and and phing_ for generating the config files

.. code-block:: sh

  cp build.properties.dist build.properties

The build.properties contains all configuration values. Adapt these values and run

.. code-block:: sh
  
  ./phing -D overwrite=1

This will copy varios config *.dist files into the autoload directory.  

.. _composer: https://getcomposer.org/
.. _phing: http://www.phing.info/

Configuration
-------------

Configuration files are located in ``config/autoload``. Config files are 
returning an assoziative array. All arrays are merged, so the order how 
the configuration files are processed might be relevant.

Files with names ending in ``*.global.php`` are process first. As a second
files ending in ``*.{env}.php``. {env} can have at least the values ``production``, 
and ``development``. 
If the environment variable ``APPLICATION_ENV`` is set, and if files named 
``*. development.php`` exist, then these configurations are processed.

At the and ``*.local.php`` files are processed.

Modules are coming with there own ``config`` directory. Configuration files of
modules can be named ``*.config.php``. This allows you to split configurations
into sections. E.g. a router.config.php file sould contain an assoziative
array defining routing specific things.


Database
^^^^^^^^

create a ``config/autoload/core.db.mongodb.local.php`` to define the database. 

.. code-block:: php
   :linenos:

   <?php
   return array(
     'database' => array(
        'connection' => 'localhost:27017',
     ),
   );
   ?>

Apache
^^^^^^

point the DocumentRoot of your Webserver to the ``public`` directory.

.. code-block:: sh

  <VirtualHost *:80>
        ServerName YOUR.HOSTNAME
        DocumentRoot /YOUR/DIRECTORY/public
  
        <Directory /YOUR/DIRECTORY/public>
                DirectoryIndex index.php
                AllowOverride All
                Order allow,deny
                Allow from all
        </Directory>
  </VirtualHost>

.. note::

  you should ``SetEnv APPLICANTION_ENV development`` in your VirtualHost section,
  if you plan do develop.

Authentication
^^^^^^^^^^^^^^

to enable login via Facebook, Xing, Linkedin or any other hybridauth_ adapter simply create a ``config/autoload/module.auth.local.php``

.. _hybridauth: http://hybridauth.sourceforge.net/

.. code-block:: php
   :linenos:

   <?php
   return array(
	'hybridauth' => array(
        "Facebook" => array (
            "enabled" => true,
            "keys"    => array ( "id" => "", "secret" => "" ),
            "scope"       => 'email, user_about_me, user_birthday, user_hometown, user_website',
        ),
        "LinkedIn" => array (
            "enabled" => true,
            "keys"    => array ( "key" => "", "secret" => "" ),
        ),
        "XING" => array (
            "enabled" => true,
            // This is a hack due to bad design of Hybridauth
            // There's no simpler way to include "additional-providers"
            "wrapper" => array ( 
                'class' => 'Hybrid_Providers_XING',
                'path' => __FILE__,
            ),
            "keys"    => array ( "key" => "", "secret" => "" ),
        ),
   );
   ?>

Debugging
^^^^^^^^^

you can enable the debugging Mode by setting the enviroment variable 
``APPLICATION_ENV=development``. This will enable increase the debug 
level, enable error messages on the screen.
