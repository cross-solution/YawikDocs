Installation
============

Requirements
------------

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

this will download the composer.phar, check dependencies and install missing libraries.

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



Authentication
^^^^^^^^^^^^^^

to enable login via Facebook, Xing, Linkedin or any other hybridauth adapter simply create a ``config/autoload/module.auth.local.php``

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