.. index:: Core

Core
----

.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/core/chart/image_png"/>
    <br/>translation state of Core module.
    </div>


Contents: 

.. toctree:: 
   :maxdepth: 1

   forms
   navigation
   notifications
   logging
   headscripts





provides core functionality

* Sending Mails
* Formular handling
* Navigation
* Pagination
* Error Handling
* Configuration Handling
* PDF Handling
* Attachment handling
* ACL for Attachments
* general Layout

.. _templates:

Layout
^^^^^^

+---------+---------------------------------+---------------------------------------------------+
|Module   |Name                             |Description                                        |
+=========+=================================+===================================================+
|Core     |`layout/layout`_                 |general layout                                     |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`core/index/index`_              |homepage for guests                                |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`core/notifications`_            |notifications                                      |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`main-navigation`_               |can be used as view script for the main navigation |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`pagination-control`_            |defines the pagination of listings                 |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`form/core/buttons`_             |defines default buttons of formulars               |
+---------+---------------------------------+---------------------------------------------------+
|Core     |`form/core/privacy`_             |defines privacy policy                             |
+---------+---------------------------------+---------------------------------------------------+
|Auth     |`form/auth/contact.form`_        |the users profile form                             |
+---------+---------------------------------+---------------------------------------------------+
|Auth     |`form/auth/contact.view`_        |the users profile view                             |
+---------+---------------------------------+---------------------------------------------------+
|Auth     |`auth/index/login-info`_         |Login Box                                          |
+---------+---------------------------------+---------------------------------------------------+
|Auth     |`auth/manage/password`_          |change password page                               |
+---------+---------------------------------+---------------------------------------------------+

.. _layout/layout: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/layout/layout.phtml
.. _core/index/index: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/auth/index/index.phtml
.. _core/notifications: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/notifications.phtml
.. _index/index: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/index/index.phtml
.. _main-navigation: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/main-navigation.phtml
.. _pagination-control: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/pagination-control.phtml
.. _form/core/buttons: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/buttons.phtml
.. _form/core/privacy: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/privacy.phtml
.. _form/auth/contact.form: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/contact.form.phtml
.. _form/auth/contact.view: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/contact.view.phtml
.. _auth/index/login-info: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/auth/index/login-info.phtml
.. _auth/manage/password: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/auth/manage/password.phtml

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
