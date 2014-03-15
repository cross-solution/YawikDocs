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


.. _templates:

Layout
^^^^^^


+---------+-------------------------+---------------------------------------------------+
|Module   |Name                     |Description                                        |
+=========+=========================+===================================================+
|Core     |`layout/layout`_         |general layout                                     |
+---------+-------------------------+---------------------------------------------------+
|Core     |`main-navigation`_       |can be used as view script for the main navigation |
+---------+-------------------------+---------------------------------------------------+
|Core     |`pagination-control`_    |defines the pagination of listings                 |
+---------+-------------------------+---------------------------------------------------+
|Core     |`form/core/buttons`_     |defines default buttons of formulars               |
+---------+-------------------------+---------------------------------------------------+
|Core     |`form/core/privacy`_     |defines privacy policy                             |
+---------+-------------------------+---------------------------------------------------+
|Auth     |`form/auth/my-profile`_  |users profile                                      |
+---------+-------------------------+---------------------------------------------------+
|Auth     |`auth/index/login-info`_ |Login Box                                          |
+---------+-------------------------+---------------------------------------------------+

.. _layout/layout: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/layout/layout.phtml
.. _main-navigation: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/partial/main-navigation.phtml
.. _pagination-control: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/partial/pagination-control.phtml
.. _form/core/buttons: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/form/buttons.phtml
.. _form/core/privacy: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Core/view/form/privacy.phtml
.. _form/auth/my-profile: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Auth/view/form/my-profile.phtml
.. _auth/index/login-info: https://github.com/cross-solution/CrossApplicantManager/blob/master/module/Auth/view/auth/index/login-info.phtml

Mail Templates
^^^^^^^^^^^^^^
+--------+---------------------------+-------------------------------+
| Module | Name                      | Description                   |
+========+===========================+===============================+
|Auth    | first-login               | informs about the first login |
+--------+---------------------------+-------------------------------+

Services
^^^^^^^^

+---------+-----------------------+-----------------------------+
| Module  | Name                  | Description                 |   
+=========+=======================+=============================+
|Core     | Log/Core/Cam          | Logging service             |
+---------+-----------------------+-----------------------------+
|Auth     | HybridAuthAdapter     | Login via Social Networks   |
+---------+-----------------------+-----------------------------+
|Auth     | AuthenticationService | Authentication Service      |
+---------+-----------------------+-----------------------------+