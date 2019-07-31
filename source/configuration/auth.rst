Authentication
==============

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
