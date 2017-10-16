.. index:: Core; Logging

Logging
-------

All PHP errors are logged into the ``log/tracy`` directory. This directory may contain the following files:

* :file:`error.log`: contains a list of exceptions, errors and notices  
* :file:`exception--<YYYY-MM-DD--HH-MM>--<hash>.html`: contains a single  HTML formatted exception trace  
* :file:`email-sent`: is used for snoozing email notifications and usually contains 'sent' text  

The path to this directory is configured in:

.. code-block:: php

    'tracy' => [
        'log' => __DIR__ . '/../../../log/tracy',
    ],  

