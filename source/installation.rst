Installation
============

you need at least a webserver, a mongo database and PHP. We're developing using
apache with mod_php5 enabled. But you can use ngix, too. If you don't have a local mongoDB available you can try a
provider like `mlab.com`_ or google_.

.. _mlab.com: https://mlab.com/
.. _google: https://console.cloud.google.com/launcher?q=mongodb

Requirements
------------

* php >= 5.6.* (PHP7 is currently not supported)
* Zend Framework 2.5.* (we're currently `updating to ZF3`_, ZF2 Support will be dropped in 0.29+)
* mongodb >= 2.4.* (you should use >= 2.6 ... see below)
* php5-mongo
* php5-intl
* php5-curl (only needed to install dependencies via composer)
* php5-xsl (only needed to install dependencies via composer)
* php5-openssl (only needed to install dependencies via composer)
* php5-mbstring (only needed, if the PDF module is used)

YAWIK should run on any OS, which supports the above software components. In real life, we've seen YAWIK running on
Linux Ubuntu, Debian, FreeBSD and OSX. It's possible to run YAWIK on AWS.

.. _updating to ZF3: https://github.com/cross-solution/YAWIK/projects/3

On FreeBSD, make sure, the php fileinfo extention is available. Fileinfo extention is needed by validating file uploads.

The YAWIK development is done on Ubuntu Linux. It is tested on Precise 12.04 and Trusty 14.04, Xenial 16.04 and Debian 8.

.. _get_mongo:

Install mongo Database
^^^^^^^^^^^^^^^^^^^^^^

YAWIK runs with mongo 2.4. So you can use the mongod version, which is shipped with your distribution. However, you
should use a later version. Otherwise you have to `enable the text search`_, which is disabled in 2.4 by default.
In 2.6 and above the text search is enabled by default.

.. _enable the text search: https://docs.mongodb.com/v2.4/tutorial/enable-text-search/

You can install e.g. mongo 3.2 by: (Our demo is running 2.6, development is done with 3.0 and 3.2)


https://docs.mongodb.com/manual/administration/install-on-linux/

We've installed mongo the following way:

.. code-block:: sh

 sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
 echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
 sudo apt-get update
 sudo apt-get install -y mongodb-org

If your linux comes with systemd, you can start your mongod with ``service mongo start``. If you need an init script,
because your linux comes with `sysv`_, you can fetch it from mongodb github repository

.. code-block:: sh

    cd /etc/init.d/
    curl https://raw.githubusercontent.com/mongodb/mongo/master/debian/init.d > mongod
    chmod +x mongod
    update-rc.d mongod defaults

Start your mongod with ``/etc/init.d/mongod start``

Install YAWIK on Debian 8
^^^^^^^^^^^^^^^^^^^^^^^^^

If like to run YAWIK in an `LXC container`_ on proxmox_. If we do so, we prefere debian 8, because it ships with php5.6.
So we do not have to downgrade to php5.6. On the other hand it comes with `sysv`_. However, installing YAWIK on Debian 8
you have to install the following packages.

.. code-block:: sh

  apt-get install php5-mongo libapache2-mod-php5 php5-curl php5-xsl \
                   php5-intl php5-common php5-cli php5-json php5 apache2 curl npm uglifyjs

``npm`` and ``uglifyjs`` are needed to install assets (boostrap, jquery, select2 ...). You're only need those packages,
if you want to install YAWIK git ``cdgit``


.. _LXC container: http://download.proxmox.com/images/system/
.. _proxmox: https://www.proxmox.com/de/
.. _sysv: https://forum.proxmox.com/threads/debian-8-6-lxc-template-with-systemd-feature-request.30212/

Install YAWIK on Ubuntu 16.04
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We assume, you have a running mongod. Otherwise check :ref:`getting a mongo db<get_mongo>`

YAWIK should run on all operating systems, which support PHP (currently php 5.5 and php 5.6). Due to the changed in the
php extentions for mongo (php-mongo and php-mongodb) YAWIK currently does not support php7. We'll wait for
doctrine-mongodb-odm_ until they fully support PHP7. This means, you have to downgrade php on Ubuntu Xenial 16.04. Add
the ondrej/php repository to your apt source lists.


.. code-block:: sh

 LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
 aptitude update
 aptitude install php5.6-mongo php5.6-curl php5.6-xsl php5.6-intl php5.6-common php5.6-cli php5.6-json curl

.. _doctrine-mongodb-odm: http://doctrine-orm.readthedocs.io/projects/doctrine-mongodb-odm/en/latest/#


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

By pointing your browser to the ``YAWIK-x.y.z/public`` directory, an installation page appears. You'll be asked to
enter a mongodb connection string, a username, a password and an email address.

.. note::

    YAWIK will run in production mode by default. So if you make modifications to the config autoload files you
    have to remove the ``cache/module-classmap-cache.module_map.php`` and ``cache/module-config-cache.production.php``.


Using Apache
^^^^^^^^^^^^

If you want to use Apache, you probably need root access to the machine you've installed
YAWIK on. In addition you need to enable the rewrite module of apache.

.. code-block:: sh

  sudo a2enmod rewrite && sudo service apache2 reload

Then you have to make sure that the DocumentRoot of apache is pointing to ``YAWIK/public``
and apache is allowed to Access the YAWIK directory.

A VirtualHost section might look like.

.. code-block:: sh

   <VirtualHost *:80>
        ServerName yawik.example.com
        DocumentRoot /var/www/YAWIK/public
        AddDefaultCharset utf-8

        # set an env to disable caching.
        #SetEnv APPLICATION_ENV "development"

        <Directory /var/www/YAWIK/public>
             DirectoryIndex index.php
             Options Indexes FollowSymLinks MultiViews
             AllowOverride All
             # for apache >=2.4
             Require all granted

             # for apache <= 2.2
             # Allow from all
        </Directory>
    </VirtualHost>

Place this in a file called ``yawik.example.com.conf`` in ``/etc/apache2/conf`` and execute

.. code-block:: sh

  sudo a2ensite yawik.example.com.conf && sudo service apache2 reload


now you should be able to login into your YAWIK by pointing a browser to

http://${YAWIK_HOST}

.. note::

    Be sure you either export the variables YAWIK_HOST and YAWIK_HOME or replace them with the actual values in the
    apache config file.

    Also your Webserver should not be able to access your build.properties. You can safely remove this file
    after you've run the installation is done.

Using Nginx
^^^^^^^^^^^

A configuration file for Nginx looks like this

.. code-block:: sh

  server {
       listen         80;

        server_name my.yawik.host;

        root /your-location/YAWIK/public;
        index index.html index.htm index.php;
        charset utf-8;

        location / {
            try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
            fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_pass unix:/run/php/php5.6-fpm.sock;
            fastcgi_param   APPLICATION_ENV  production;
            include /etc/nginx/fastcgi_params;
        }
  }


.. todo::

    We need more details on setup nginx here.
    - Where to put the server config
    - What commands to run.

Yawik can be downloaded at https://sourceforge.net/projects/yawik/files/

Setup for Developers
^^^^^^^^^^^^^^^^^^^^

if you want to modify the YAWIK code, you should clone the repository from Github. 
The repository does not contain any dependency. You have to import all dependencies by 
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
from the modules configuration directory to the autoload directory and removing the ".dist" part.

.. note::

    To disable the caching of the config autoload files you need to set an environment variable called
    ``APPLICATION_ENV`` to the value "development"

    If you use apache, you can do this in your virtual section config with
    ``SetEnv APPLICATION_ENV="development"``



Setup using composer
^^^^^^^^^^^^^^^^^^^^

you can install yawik using composer

.. code-block:: sh

  composer create-project cross-solution/yawik:dev-develop

This will clone the latest version from the develop branch, download all needed dependencies.

.. code-block:: sh

    cd yawik
    php -S localhost:8000 index.php

Point your browser to localhost:8000 and start using yawik




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

At the end ``*.local.php`` files are processed.:

Modules are coming with there own ``config`` directory. Configuration files of
modules can be named ``*.config.php``. This allows you to split configurations
into sections. E.g. a router.config.php file should contain an associative
array defining routing specific things.

If the enviroment is set to ``production``, all configurations are cached in
``cahe/module-classmap-cache.module_map.php``. There is currently no way to invalidate the
cache. You have to remove this file, if you alter files in ``config/autoload``.


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
            "keys"    => array ( "key" => "", "secret" => "" ),
        ),
        "Github" => array(
            "enabled" => true,
            'keys'    => array ( "id" => "", 'secret' => ""),
            "scope"   => ''
        ),
        "Google" => array(
             "enabled" => true,
             'keys'    => array ( "id" => 'xxxxxxxxxxxx-xxxxxxxxxxxxxxxxxxxxxxxx.apps.googleusercontent.com', 'secret' => ''),
             "scope"   => 'https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email',
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