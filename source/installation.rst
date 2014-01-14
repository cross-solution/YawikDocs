Installation
============

Requirements
------------

* php 5.3.*
* Zend Framework 2.1.*
* mongodb 2.4.*

Setup
-----

.. code-block:: sh

  git clone https://github.com/cross-solution/CrossApplicantManager
  cd CrossApplicantManager
  composer.phar install


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