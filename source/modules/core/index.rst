.. index:: Core

Core
----

provides core functionality

* Logging
* Sending Mails
* Formular handling
* Pagination
* Error Handling
* Configuration Handling
* PDF Handling
* Attachment handling
* ACL for Attachments
* general Layout

Logging
^^^^^^^

all PHP errors are logged into log/cam.log. This is configured in:

.. code-block:: php

  'log' => array(
        'Log/Core/Cam' => array(
            'writers' => array(
                 array(
                     'name' => 'stream',
                    'priority' => 1000,
                    'options' => array(
                         'stream' => __DIR__ .'/../../../log/cam.log',
                    ),
                ),
            ),
        ),


Layout
^^^^^^


+---------+-------------------------+----------------------------+
|Module   |Name                     |Description                 |
+=========+=========================+============================+
|Core     |`layout/layout`_         |general layout              |
+---------+-------------------------+----------------------------+
|Auth     |`form/auth/my-profile`_  |users profile               |
+---------+-------------------------+----------------------------+
|Auth     |`auth/index/login-info`_ |Login Box                   |
+---------+-------------------------+----------------------------+

.. _layout/layout: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/layout/layout.phtml
.. _form/auth/my-profile: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Auth/view/form/my-profile.phtml
.. _auth/index/login-info: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Auth/view/auth/index/login-info.phtml

