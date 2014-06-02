Installation
============

Requirements
------------

you need at least a webserver, a mongo database and PHP. We're developing using 
apache with mod_php5 enabled. If you don't have a local mongoDB availabe you can
try a provider like mongolab.com_ or mongosoup.de_.

.. _mongolab.com: https://mongolab.com/welcome/
.. _mongosoup.de: https://www.mongosoup.de/

* a Facebook, Xing or LinkedIn App
* php 5.3.*
* Zend Framework 2.2.*
* mongodb 2.4.*
* php5-mongo
* php5-intl
* php5-curl (only needed to install dependencies via composer)
* php5-xsl (only needed to install dependencies via composer)

Setup
-----

.. code-block:: sh

  git clone https://github.com/cross-solution/CrossApplicantManager
  cd CrossApplicantManager
  ./install.sh

this downloads composer_ and phing_ and installs missing dependencies and 
generates config files.

.. code-block:: sh

  cp build.properties.dist build.properties

The build.properties contains all configuration values. You currently need
at least one Social Network App. So take a look how to create an App with
Facebook_, Xing_ or LinkedIn_. Currently there is no way to create a Yawik
Account without a such an App.

.. _Facebook: https://developers.facebook.com/
.. _Xing: https://dev.xing.com/overview
.. _LinkedIn: https://developer.linkedin.com/

Adapt these values. Put you app IDs and your secret into the ``build.properties``.

.. code-block:: sh

  ;
  ; Facebook, Xing and Linkedin credentials. (module/Auth/config/module.auth.global.php.dist)
  ;

  facebook.enabled=false
  facebook.appid=
  facebook.secret=
  facebook.scope="email, user_about_me, user_birthday, user_hometown", "user_work_history", "user_education_history"

  xing.enabled=false
  xing.appid=
  xing.secret=
  xing.scope=

  linkedin.enabled=false
  linkedin.appid=
  linkedin.secret=
  linkedin.scope="r_fullprofile"

Ànd then run

.. code-block:: sh
  
  ./phing.phar

This will copy varios config *.dist files into the autoload directory. 

all build options can be listed by:

.. code-block:: sh

  $ ./phing.phar -l
  Buildfile: /home/cbleek/Zend/workspaces/DefaultWorkspace/CrossApplicantManager/build.xml
   [property] Loading /home/cbleek/Zend/workspaces/DefaultWorkspace/CrossApplicantManager/./build.properties
  Default target:
  -------------------------------------------------------------------------------
   install    reads build.properties and generates config files
  
  Main targets:
  -------------------------------------------------------------------------------
   clean      removes build, log, cache, tmp and vendor dir
   dist       create a distribution package
   docs       build api docs
   install    reads build.properties and generates config files
   phpdoc     build api docs
   translate  compiles all languages *.po files

  Subtargets:
  -------------------------------------------------------------------------------
   build
   compile-po-file
   generate-autoload-config
   prepare


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
