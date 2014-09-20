Installation
============

Requirements
------------

you need at least a webserver, a mongo database and PHP. We're developing using 
apache with mod_php5 enabled. If you don't have a local mongoDB available you can
try a provider like mongolab.com_ or mongosoup.de_.

.. _mongolab.com: https://mongolab.com/welcome/
.. _mongosoup.de: https://www.mongosoup.de/

* php 5.3.*
* Zend Framework 2.2.*
* mongodb 2.4.*
* php5-mongo
* php5-intl
* php5-curl (only needed to install dependencies via composer)
* php5-xsl (only needed to install dependencies via composer)
* php5-openssl (only needed to install dependencies via composer)
* php5-mbstring (only needed, if the PDF module is used)

The YAWIK development is done on Ubuntu Linux. It is tested on Precise 12.04 and Trusty
14.04. There you can install the required apache, php and mongodb via:

.. code-block:: sh

  aptitude install mongodb-server php5-mongo libapache2-mod-php5 php5-curl php5-xsl \
                   php5-intl php5-common php5-cli php5-json php5 apache2 curl

YAWIK should run on all operating systems, which support PHP. 

More information about installation of Mongo:

http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/


Setup
-----

get the latest YAWIK Package. Packages are build as ZIP or TGZ archive. We publish 
them on Sourceforge_. They extract into a subdirectory YAWIK-x.y.z. If you preserve the
permissions, the directories ``cache`` and ``log`` should be writable after extraction.

.. _Sourceforge: https://sourceforge.net/projects/yawik/

Go into the ``YAWIK`` directory and edit the ``build.properties`` file. There you can 
set database resources and an initial Account to login into your YAWIK. The Webserver
only needs read access to the ``YAWIK/public`` and write access to the ``YAWIK/public``
and ``YAWIK/cache`` directory.

next step is to run ``./install.sh``

This will download phing_ , executes ``./phing.phar generate-autoload-config`` 
which takes the configuration option of your ``build.properties`` and generates
various configuration files located in config/autoload.

Trusty comes with php5.5 and therefore you can simply fire up YAWIK by

.. code-block:: sh

  cd public
  php -S localhost:8080     # make sure, the port is not already in use

after that you should are able to access YAWIK on your local machine by pointing your
browser to:

http://localhost:8080

If you want to use Apache, you probably need root access to the machine you've installed
YAWIK on. In addition you need to enable the rewrite module of apache.

.. code-block:: sh

  sudo a2enmod rewrite && sudo /etc/init.d/apache2 reload

Then you have to make sure that the DocumentRoot of apache is pointing to ``YAWIK/public``
and apache is allowed to Access the YAWIK directory.

A VirtualHost section might look like.

.. code-block:: sh

   <VirtualHost *:80>
        ServerName example.com/
        DocumentRoot ${YAWIK_HOME}/public
        AddDefaultCharset utf-8

        SetEnv APPLICATION_ENV "development"             // you can set

        <Directory ${YAWIK_HOME}/public>
             DirectoryIndex index.php
             Options Indexes FollowSymLinks MultiViews
             AllowOverride All
             Require all granted
        </Directory>
    </VirtualHost>



now you should be able to login into your YAWIK by pointing a browser to

http://example.com/

.. note::

    make sure your Webserver cannot access your build.properties. You can safely remove this file
    after you've run the installation is done.


Yawik can be downloaded at https://sourceforge.net/projects/yawik/files/

Setup for Developers
^^^^^^^^^^^^^^^^^^^^

if you want to modify the YAWIK code, you have to clone the sources from Github. 

Unpack the sources in the DocumentRoot. You'll find the sources in the YAWIK directory. 

.. code-block:: sh

  git clone https://github.com/cross-solution/CrossApplicantManager
  cd CrossApplicantManager
  cp build.properties.dist build.properties

The build.properties contains all configuration values in one file. It simplifies the
setup of a development environment. Here you can define an initial user account, a
database resource or integrate social networks. The values itself are copied to various
configuration files, which are placed into ``config/autoload`` by running
``./phing generate-autoload-config``. That means, you have to execute ``./phing generate-autoload-config``
to make changes available to the application.

Note: you need a Facebook, Xing or LinkedIn App, if you want to integrate the social
networks . So take a look how to create an App with Facebook_, Xing_ or LinkedIn_. 

.. _Facebook: https://developers.facebook.com/
.. _Xing: https://dev.xing.com/overview
.. _LinkedIn: https://developer.linkedin.com/

Adapt these values. Put your app IDs and your secret into the ``build.properties``.

Finally run the ``install.sh`` script. This downloads composer_ and phing_ and 
installs missing dependencies and generates config files.

.. code-block:: sh

  ./install.sh

.. code-block:: sh

  ;
  ; Facebook, Xing and LinkedIn credentials. (module/Auth/config/module.auth.global.php.dist)
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

This will extract the key/value pairs from the ``build.properties``, replaces them in the
``modules/<Module>/config/*.php.dist`` files and copies the result into the ``config/autoload`` directory.

all build options can be listed by:

.. code-block:: sh

  cbleek@xenon:~/Projects/YAWIK$ ./phing.phar -l
  Buildfile: /home/cbleek/Projects/YAWIK/build.xml
   [property] Loading /home/cbleek/Projects/YAWIK/./build.properties
  Default target:
  -------------------------------------------------------------------------------
   install        reads build.properties and generates config files

  Main targets:
  -------------------------------------------------------------------------------
   build          build tgz and zip packages
   clean          removes build, log, cache, tmp, components and vendor dir
   deploy-builds  publish TGZ and ZIP packages via rsync
   deploy-docs    publish API docs via rsync
   docs           build api docs
   install        reads build.properties and generates config files
   phpdoc         build api docs using phpdoc
   translate      compiles all languages *.po files

  Subtargets:
  -------------------------------------------------------------------------------
   compile-po-file
   generate-autoload-config
   prepare
   symlinks


.. _composer: https://getcomposer.org/
.. _phing: http://www.phing.info/

Configuration
-------------

Configuration files are located in ``config/autoload``. Config files are 
returning an associative array. All arrays are merged, so the order how
the configuration files are processed might be relevant.

Files with names ending in ``*.global.php`` are process first. As a second
files ending in ``*.{env}.php``. {env} can have at least the values ``production``, 
and ``development``. 
If the environment variable ``APPLICATION_ENV`` is set, and if files named 
``*. development.php`` exist, then these configurations are processed. If no environment
variable ist set, ``production`` is assumed.

At the end ``*.local.php`` files are processed.

Modules are coming with there own ``config`` directory. Configuration files of
modules can be named ``*.config.php``. This allows you to split configurations
into sections. E.g. a router.config.php file should contain an associative
array defining routing specific things.

If the enviroment is set to ``production``, all configurations are cached in
``cahe/module-classmap-cache.module_map.php``. There is currently no way to invalidate the
cache. You have to remove this file, if you alter files in ``config/autoload``.


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

  you should ``SetEnv APPLICATION_ENV development`` in your VirtualHost section,
  if you plan do develop.

Authentication
^^^^^^^^^^^^^^

to enable login via Facebook, Xing, LinkedIn or any other hybridauth_ adapter simply create a ``config/autoload/module.auth.local.php``

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

you can enable the debugging Mode by setting the environment variable
``APPLICATION_ENV=development``. This will increase the debug
level, enable error messages on the screen and disables sending of mails to the
recipients, stored in the database. You can overwrite the the all recipients (To, CC, Bcc)
by setting ``mail.develop.override_recipient=<your mail address>``