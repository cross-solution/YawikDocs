Installation
============

Requirements
------------

you need at least a webserver, a mongo database and PHP. We're developing using 
apache with mod_php5 enabled. If you don't have a local mongoDB available you can
try a provider like mongolab.com_ or mongosoup.de_.

.. _mongolab.com: https://mongolab.com/welcome/
.. _mongosoup.de: https://www.mongosoup.de/

* php >= 5.5.*
* Zend Framework 2.5.*
* mongodb >= 2.4.*
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

http://docs.mongodb.org/manual/tutorial/install-mongodb-enterprise-on-ubuntu/

YAWIK runs with mongo 2.4 (which comes by default with ubuntu 14.04). If you want to use a later version
(which is recommended), you can install e.g. mongo 2.6 by:

.. code-block:: sh

 sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
 echo "deb http://repo.mongodb.com/apt/ubuntu "$(lsb_release -sc)"/mongodb-enterprise/2.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-enterprise-2.6.list
 sudo apt-get update
 sudo apt-get install -y mongodb-enterprise



Setup
-----


Get the latest YAWIK Package from Sourceforge_. Packages are build as ZIP or TGZ archive. 
They extract into a subdirectory YAWIK-x.y.z. If you preserve the permissions, the directories
``cache`` and ``log`` should be writable after extraction.

``tar`` preserves permissions with the ``p``-Option. So unpack a TGZ with ``tar -xzpf YAWIK-y.x.z.tgz``.
``unzip`` preserves the permissions by default (at least on ubuntu 14.4). So unpack a ZIP archive with
``unzip YAWIK-x.y.z.zip``

.. _Sourceforge: https://sourceforge.net/projects/yawik/

.. figure:: images/install-step-2.png
    :scale: 20%
    :align: right

.. figure:: images/install-step-1.png
    :scale: 20%
    :align: right

By pointing your browser to the ``YAWIK/public`` directory, an installation page appears. You'll be asked to
enter a mongodb connection string, a username, a password and an email address.

.. note::

    YAWIK will run in production mode by default. So if you make modifications to the config autoload files you
    have to remove the ``cache/module-classmap-cache.module_map.php`` and ``cache/module-config-cache.production.php``.


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
             Require all granted   // for apache >= 2.4
             //Allow from all      // for apache <= 2.2
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

if you want to modify the YAWIK code, you should clone the repository from Github. 
The repository does not contain any dependency. You can import all dependencies by 
executing the ``ìnstall.sh`` script located in the YAWIK root. This scripts imports 
all external libraries via composer. In addition, it creates the directories ``log``, 
``cache`` ùnd  ``config/autoload`` and set the directory permissions to a+w. 

.. code-block:: sh

  git clone https://github.com/cross-solution/YAWIK
  cd YAWIK
  ./install.sh


After the execution you are ready to point your browser to the ``public`` directory.
You'll get the install wizard and after entering the initial user, the database
connection and an email address you are ready to use YAWIK.

At this point your ```config/autoload`` directory contains only one file 
``yawik.config.global.php`` containing the database connection string. The initial user
is created with the ``àdmin`` role in the database.

.. code-block:: sh

    $ ls YAWIK/config/autoload
    yawik.config.global.php

All other configurations are currently done manually by copying the ```*.dist`` files
from the modules configuration directory to the autoload directory. 

Example: Setting up Facebook_, Xing_ or LinkedIn_ Login
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: sh

    YAWIK$ cp module/Auth/config/module.auth.global.php.dist config/autoload/module.auth.global.php

  
All placeholders in the configuration files which match '%%.*%%' are deprecated. They are relics of
the build.properties area. Since 0.20 an intall wizard is available which introduces an initial
user with the ``admin`` role. 



.. code-block:: sh

    ....
    "keys"    => array ( "id" => "%%facebook.appid%%", "secret" => "%%facebook.secret%%" ),    
    ....

Note: you need a Facebook, Xing or LinkedIn App, if you want to integrate the social
networks . So take a look how to create an App with Facebook_, Xing_ or LinkedIn_. 

.. _Facebook: https://developers.facebook.com/
.. _Xing: https://dev.xing.com/overview
.. _LinkedIn: https://developer.linkedin.com/

Copy the *.dist files from the modules/*/config dir into the config/autoload directory. Don't forget
to remove the "*.dist" suffix. Addjust the values and remove the cache/modules-* files.


.. _composer: https://getcomposer.org/
.. _phing: http://www.phing.info/

Configuration
-------------

Configuration files are located in ``config/autoload``. Config files are 
returning an associative array. All arrays are merged, so the order how
the configuration files are processed is relevant.

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


Apache
^^^^^^

point the DocumentRoot of your Webserver to the ``public`` directory.

.. code-block:: sh

  <VirtualHost *:80>
        ServerName YOUR.HOSTNAME
        DocumentRoot /YOUR/DIRECTORY/YAWIK/public
  
        <Directory /YOUR/DIRECTORY/YAWIK/public>
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

to enable login via Facebook, Xing, LinkedIn or any other hybridauth_ adapter simply copy the module.auth.local.php.dist_
file to ``config/autoload/module.auth.local.php`` and adjust your keys and secrets.

.. _hybridauth: http://hybridauth.sourceforge.net/
.. _module.auth.local.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/config/module.auth.global.php.dist

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