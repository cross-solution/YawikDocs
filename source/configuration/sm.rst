Example: Setting up Facebook_, Xing_ or LinkedIn_ Login
=======================================================

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
