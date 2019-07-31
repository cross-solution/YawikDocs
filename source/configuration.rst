Configuration
=============

Configuration files are located in :file:`config/autoload`. Config files are
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
:file:`cache/module-classmap-cache.module_map.php` and :file:`cache/module-config-cache.production.php`.
There is currently no way to invalidate the cache. You have to remove these
files, if you modify files in file:`config/autoload`.

.. toctree::
   :maxdepth: 2
   
   configuration/auth
   configuration/sm

Authentication
--------------

to enable login via Facebook, Xing, LinkedIn or any other hybridauth_ adapter simply copy the module.auth.local.php.dist_
file to :file:`config/autoload/module.auth.local.php` and adjust your keys and secrets.

.. _hybridauth: http://hybridauth.sourceforge.net/
.. _module.auth.local.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/config/module.auth.global.php.dist

.. code-block:: php
   :linenos:

       <?php
       return array(
            "Facebook" => array (
                "enabled" => false,
                "keys"    => array ( "id" => "your-consumer-key", "secret" => "your-consumer-secret" ),
                "scope"   => "email, user_about_me, user_birthday, user_hometown, user_work_history, user_education_history",// optional
                "display" => "popup"
            ),
            "LinkedIn" => array (
                "enabled" => true,
                "keys"    => array ( "id" => "your-consumer-key", "secret" => "your-consumer-secret" ),
                "scope"   => "r_fullprofile, r_emailaddress"
            ),
            "XING" => array(
                "enabled" => true,
                'keys'    => array ( "key" => 'your-consumer-key', 'secret' => 'your-consumer-secret'),
                "scope"   => ''
            ),
            "Github" => array(
                "enabled" => true,
                'keys'    => array ( "id" => 'your-consumer-key', 'secret' => 'your-consumer-secret'),
                "scope"   => ''
            ),
            "Google" => array(
                 "enabled" => true,
                 'keys'    => array ( "id" => 'your-consumer-key', 'secret' => 'your-consumer-secret'),
                 "scope"   => 'https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email',

        ),
       );
       ?>

The configuration structure was simply taken from the hybridauth library. So the "enabled" field means enabled for the hybridauth library. It 
does not mean "enabled" for login. To enable a social network for login you have to ad the lowercased key to `enableLogins` array. You have to
copy the auth.options.global.php.dist_ to :file:`config/autoload/auth.options.global.php` and adjust your values.

.. _auth.options.global.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/config/auth.options.global.php.dist


.. code-block:: php
   :linenos:

	$options = array(
		/*
		* default email address, which is used in FROM headers of system mails like "new registration",
		* "forgot password",..
		*/
		'fromEmail' => 'email@example.com',
	
		/*
		* default name address, which is used in FROM headers of system mails like "new registration",
		* "forgot password",..
		*/
		'fromName' => 'YAWIK Website',
	
		/*
		* Subject of your registration Mail
		*/
		'mailSubjectRegistration' => 'your registration',
	
		/*
		 * enable social networks for login and registration. The names must match the keys used in
		 * in the 'hybridauth' section of you module.auth.global.php file
		 */
		 'enableLogins' => ['linkedin','github','xing','google','facebook'],
	
		/*
		 * if true, users are allowed to register.
		 */
		 'enableRegistration' => true,

		/*
		 * if true, users can reset their password.
		 */
		 'enableResetPassword' => true,
	);



Mail
----

To configure an SMTP Server, copy `MailServiceOptions.config.local.php`_ to your ``config/autoload``
directory and adjust the values.

Setting the senders address
^^^^^^^^^^^^^^^^^^^^^^^^^^^

copy the `auth.options.global.php`_ into your ``config/autoload`` and set the fromEmail value.

.. _auth.options.global.php: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/config/auth.options.global.php.dist
.. _MailServiceOptions.config.local.php: https://github.com/cross-solution/YAWIK/blob/develop/module/Core/config/MailServiceOptions.config.local.php.dist

Setting Mail Texts
^^^^^^^^^^^^^^^^^^

The mail texts are defined by the following templats. You can overwrite the mails by mapping the following keys

.. code-block:: php
   :linenos:

            'mail/header' => __DIR__ . '/../view/mail/header.phtml',
            'mail/footer' => __DIR__ . '/../view/mail/footer.phtml',
            'mail/footer.en' => __DIR__ . '/../view/mail/footer.en.phtml',
            'mail/forgotPassword' =>  __DIR__ . '/../view/mail/forgot-password.phtml',
            'mail/register' =>  __DIR__ . '/../view/mail/register.phtml',
            'mail/job-created' => __DIR__ . '/../view/mails/job-created.phtml',
            'mail/job-pending' => __DIR__ . '/../view/mails/job-pending.phtml',
            'mail/job-accepted' => __DIR__ . '/../view/mails/job-accepted.phtml',
            'mail/job-rejected' => __DIR__ . '/../view/mails/job-rejected.phtml',
            'auth/mail/new-registration' => __DIR__ . '/../view/mail/new-registration.phtml',
            'auth/mail/user-confirmed' => __DIR__ . '/../view/mail/user-confirmed.phtml',
            'jobs-by-mail/form/subscribe/form' => __DIR__ . '/../view/jobs-by-mail/form.phtml',
            'jobs-by-mail/mail/jobs' => __DIR__ . '/../view/mail/jobs.phtml',
            'jobs-by-mail/mail/confirmation' => __DIR__ . '/../view/mail/confirmation.phtml',




The mail texts can be translated by adding the languages to the mapping keys. The Logic is coded in:
https://github.com/cross-solution/YAWIK/blob/develop/module/Core/src/Core/Mail/HTMLTemplateMessage.php#L246

.. code-block:: php
   :linenos:

                'mail/job-created.fr' => __DIR__ . '/../view/mails/job-created.fr.phtml',
                'mail/job-pending.fr' => __DIR__ . '/../view/mails/job-pending.fr.phtml',
                'mail/job-accepted.fr' => __DIR__ . '/../view/mails/job-accepted.fr.phtml',
                'mail/job-rejected.fr' => __DIR__ . '/../view/mails/job-rejected.fr.phtml',





Jobs
----

.. code-block:: php
   :linenos:

	$options = array(
	
		/**
		* If not set, the email address of the default user is used
		* @see Jobs\Options\ModulesOptionFactory
		*/
		'multipostingApprovalMail' => '',
	
		/**
		* If a target Uri is set, a rest Request is sent to this target in case
		* a job posting was accepted.
		*/
		'multipostingTargetUri' => '',
	
		/**
		* default Logo, if a company has no logo.
		*/
		'default_logo' => '/Jobs/images/yawik-small.jpg',
	
		/**
		* Maximum size in bytes of a company Logo
		*/
		'companyLogoMaxSize' => 100000,
		
		/**
		* Allowed Mime-Types for company Logos
		*/
		'companyLogoMimeType' => array("image")
	);
	
	### do not edit below ###
	
	return array('jobs_options' => $options);



Setting channels
^^^^^^^^^^^^^^^^

Currently prices and channels are hard coded. The operator of YAWIK is responsible for
publishing a jobposting to n ordered channel.

.. code-block:: php
   :linenos:

	$channel['yawik'] = array(
                'label' => 'YAWIK',
                'prices' => [ 'base' => 99, 'list' => 99, 'min'  => 99, ],
                'headline' => /*@translate*/ 'publish your job on yawik.org for free',
                'description' => /*@translate*/ 'publish the job for 30 days on %s',
                'linktext' => /*@translate*/ 'yawik.org',
                'route' => 'lang/content',
                'publishDuration' => 60,
                'params' => array(
                    'view' => 'jobs-publish-on-yawik'
                )
            );
	
	$channel['jobsintown'] = array(
                'label' => 'Jobsintown',
                'prices' => [ 'base' => 650, 'list' => 698, 'min'  => 499, ],
                'headline' => '30 Tage, incl. Karrierenetzwerk',
                'description' => 'publish the job for 30 days on %s',
                'linktext' => 'www.jobsintown.de',
                'logo' => '/Jobs/images/channels/jobsintown.png',
                'route' => 'lang/content',
                'publishDuration' => 30,
                'params' => array(
                    'view' => 'jobs-publish-on-jobsintown'
                )
            );
	
	$channel['fazjob'] = array(
                'label' => 'FAZjob.NET',
                'prices' => [ 'base' => 1095, 'list' => 1095, 'min'  => 1095, ],
                'headline' => '30 Tage auf dem Karriereportal der FAZ',
                'description' => 'publish the job for 30 days on %s',
                'linktext' => 'FAZjob.net',
                'logo' => '/Jobs/images/channels/fazjob_net.png',
                'route' => 'lang/content',
                'publishDuration' => 60,
                'params' => array(
                    'view' => 'jobs-publish-on-fazjob-net'
                )
            );
	
	$channel['homepage'] = array(
                'label' => /*@translate*/ 'Your Homepage',
                'prices' => [ 'base' => 0, 'list' => 0, 'min'  => 0, ],
                'headline' => /*@translate*/ 'enable integration of this job on your Homepage',
                'description' => /*@translate*/ 'enable %s of this job on your Homepage',
                'linktext' => /*@translate*/ 'integration',
                'route' => 'lang/content',
                'params' => array(
                    'view' => 'jobs-publish-on-homepage'
                )
            );
	
	return array('multiposting'=> array('channels' => $channel));




Sitename
--------




Apache
------

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

MongoDB
-------



Debugging
---------

You can enable the debugging mode by setting the following configuration:

.. code-block:: php

    'tracy' => [
        'mode' => false
    ]

This will enable displaying of error messages on the screen and disables sending of email error notifications to the
recipients specified in the following configuration:

.. code-block:: php

    'tracy' => [
        'email' => 'first.recipient@domain.tld, second.recipient@domain.tld'
    ],

The complete debugging configuration with default values consists of:

.. code-block:: php

    'tracy' => [
        'mode' => true, // toggles the production/development mode (true = production, false = development, null = autodetect, IP address(es) csv/array)
        'bar' => false, // toggles the diagnostics bar (a small bar placed in the bottom right corner of a browser displaying system info such a memory usage, elapsed time, ...)
        'strict' => true, // sets the error level strictness (bool = cause immediate death, int = matched against error severity)
        'log' => __DIR__ . '/../../../log/tracy', // sets the path to a log directory (this directory keeps error.log, snoozing mailsent file & html exception trace files)
        'email' => null, // sets the recipient(s) of email error notifications in the production mode (multiple recipients are separated with a comma or presented as an array)
        'email_snooze' => 900 // sets the interval for sending email error notifications in seconds
    ], 

Debugging Mails
^^^^^^^^^^^^^^^

To send all mails to one or more specific mail addresses, regardless of the original recipients in To:, Cc: and Bcc: headers, you can set the configuration:

.. code-block:: php

    'mails' => array(
        'develop' => array(
                /* 
                 * Every mail send from the system will be send ONLY to this address(es),
                 * regardless of the original set recipient(s) (including CC and BCC).
                 * Use comma to separate addresses. 
                 * Use an empty string (or comment out) to disable.
                 */
                'override_recipient' => '',

        ),
    ),

If you put this configuration in an autoloaded config file which name ends in `.development.php`, it will be loaded only, when the environment variable 
`APPLICATION_ENV` is set to "development". This allows for quick enabling and disabling without the need to modify configuration files.

 