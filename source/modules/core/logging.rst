.. index:: Core; Logging

Logging
-------

all PHP errors are logged into log/yawik.log. This is configured in:

.. code-block:: php

  'log' => array(
        'Log/Core/Cam' => array(
            'writers' => array(
                 array(
                     'name' => 'stream',
                    'priority' => 1000,
                    'options' => array(
                         'stream' => __DIR__ .'/../../../log/yawik.log',
                    ),
                ),
            ),
        ),


