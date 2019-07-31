Runtime
=======

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
``cache/module-classmap-cache.module_map.php``. There is currently no way to invalidate the
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
