Installation
============

Requirements
------------

you need at least a webserver, a mongo database and PHP. We're developing using apache with mod_php5 enabled.

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

this will download the composer_, check dependencies and install missing libraries.

.. _composer: https://getcomposer.org/

Configuration
-------------

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

you can enable the debugging Mode by setting the enviroment variable APPLICATION_ENV=develop. This will enable increase the debug level, enable error messages on the screen.
