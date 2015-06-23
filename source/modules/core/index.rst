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
   mails
   options





provides core functionality

* Sending Mails
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


.. note::

    the following table is generated automatically.
    Descriptions are marked from the view scripts files mit ``{{rtd: ...}}``

+----------------------------------------+----------------------------------------+----------------------------------------+
|Module                                  |Name                                    |Description                             |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`layout/layout`_                        |General layout. Includes the HTML Header|
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`error/404`_                            |File not found error page               |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`error/403`_                            |Forbidden error page                    |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`error/index`_                          |Internal Server Error Page (500)        |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`main-navigation`_                      |Renders a horizontal navigation with    |
|                                        |                                        |drop downs                              |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`pagination-control`_                   |Renders paginations                     |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`core/loading-popup`_                   |Renders a simple loading box while ajax |
|                                        |                                        |requests are proceeded                  |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`core/notifications`_                   |Renders default notification boxes.     |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`form/core/buttons`_                    |Renders default 'save' and 'abort'      |
|                                        |                                        |buttons                                 |
+----------------------------------------+----------------------------------------+----------------------------------------+
|not found (form/core/privacy)           |WRONG CONFIGURATION                     |                                        |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`core/form/permissions-fieldset`_       |Renders the group permission fieldset   |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`core/form/permissions-collection`_     |Renders the group form                  |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Core                                    |`core/form/container-view`_             |Renders horizontal summary form         |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`form/auth/contact.form`_               |Renders the contact form within the     |
|                                        |                                        |application form and the personal       |
|                                        |                                        |profile.                                |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`form/auth/contact.view`_               |renders the contact information within  |
|                                        |                                        |the application form and the personal   |
|                                        |                                        |profile.                                |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`auth/form/user-info-container`_        |Renders horizontal form for the contact |
|                                        |                                        |and the user photo                      |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`auth/form/userselect`_                 |Renders form for adding Users to a Group|
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`auth/form/social-profiles-fieldset`_   |Renders the fieldset for adding Social  |
|                                        |                                        |Profiles to an Application              |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`auth/form/social-profiles-button`_     |Renders the selection boxes for adding  |
|                                        |                                        |social profiles to an application       |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Auth                                    |`auth/sidebar/groups-menu`_             |file exists                             |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Applications                            |`applications/error/not-found`_         |Error Page for an Application form which|
|                                        |                                        |references a non-existing job           |
+----------------------------------------+----------------------------------------+----------------------------------------+
|not found (layout/apply)                |WRONG CONFIGURATION                     |                                        |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Applications                            |`applications/sidebar/manage`_          |currently not used                      |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Applications                            |`applications/mail/forward`_            |Renders the email for forwarding an     |
|                                        |                                        |application                             |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Applications                            |`applications/detail/pdf`_              |Renders a application as a simple HTML, |
|                                        |                                        |used in the PDF generation and the      |
|                                        |                                        |forward mail                            |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Applications                            |`applications/index/disclaimer`_        |Display the privacy policy disclaimer   |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs/sidebar/index`_                   |Renders paginations                     |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs/form/list-filter`_                |Renders the search formular for jobs    |
|                                        |                                        |used by recruiters                      |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs/form/apply-identifier`_           |currently not used. Generates an        |
|                                        |                                        |reference number for jobs               |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs-publish-on-yawik`_                |displays short info about publishing on |
|                                        |                                        |YAWIK                                   |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs-publish-on-jobsintown`_           |displays short info about publishing on |
|                                        |                                        |Jobsintown.de                           |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs-publish-on-homepage`_             |displays short info about publishing on |
|                                        |                                        |the own homepage                        |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`jobs-terms-and-conditions`_            |display the terms and conditions, when  |
|                                        |                                        |publishing a job opening                |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Jobs                                    |`mail/jobCreatedMail`_                  |Mail is sent to the owner of yawik. The |
|                                        |                                        |mail contains a link to an approval     |
|                                        |                                        |page, where the owner can accept or     |
|                                        |                                        |decline the job opening                 |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Pdf                                     |`pdf/application/details/button`_       |Renders the download as PDF Button, in  |
|                                        |                                        |the Applications Module                 |
+----------------------------------------+----------------------------------------+----------------------------------------+
|Geo                                     |`geo/form/GeoText`_                     |Renders the autocompletion for locations|
+----------------------------------------+----------------------------------------+----------------------------------------+
|Organizations                           |`organizations/index/edit`_             |Renders the formular for editing        |
|                                        |                                        |organizations                           |
+----------------------------------------+----------------------------------------+----------------------------------------+
|not found (piwik)                       |WRONG CONFIGURATION                     |                                        |
+----------------------------------------+----------------------------------------+----------------------------------------+

.. _zend-developer-tools/toolbar/doctrine-odm: https://github.com/cross-solution/YAWIK/blob/master/vendor/doctrine/doctrine-mongo-odm-module/view/zend-developer-tools/toolbar/doctrine-odm.phtml
.. _layout/layout: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/layout/layout.phtml
.. _error/404: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/error/404.phtml
.. _error/403: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/error/403.phtml
.. _error/index: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/error/index.phtml
.. _main-navigation: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/main-navigation.phtml
.. _pagination-control: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/pagination-control.phtml
.. _core/loading-popup: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/loading-popup.phtml
.. _core/notifications: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/notifications.phtml
.. _form/core/buttons: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/buttons.phtml
.. _core/form/permissions-fieldset: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/permissions-fieldset.phtml
.. _core/form/permissions-collection: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/permissions-collection.phtml
.. _core/form/container-view: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/form/container.view.phtml
.. _form/auth/contact.form: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/contact.form.phtml
.. _form/auth/contact.view: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/contact.view.phtml
.. _auth/form/user-info-container: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/user-info-container.phtml
.. _auth/form/userselect: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/userselect.phtml
.. _auth/form/social-profiles-fieldset: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/social-profiles-fieldset.phtml
.. _auth/form/social-profiles-button: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/form/social-profiles-button.phtml
.. _auth/sidebar/groups-menu: https://github.com/cross-solution/YAWIK/blob/master/module/Auth/view/sidebar/groups-menu.phtml
.. _applications/error/not-found: https://github.com/cross-solution/YAWIK/blob/master/module/Applications/view/error/not-found.phtml
.. _applications/sidebar/manage: https://github.com/cross-solution/YAWIK/blob/master/module/Applications/view/sidebar/manage.phtml
.. _applications/mail/forward: https://github.com/cross-solution/YAWIK/blob/master/module/Applications/view/mail/forward.phtml
.. _applications/detail/pdf: https://github.com/cross-solution/YAWIK/blob/master/module/Applications/view/applications/manage/detail.pdf.phtml
.. _applications/index/disclaimer: https://github.com/cross-solution/YAWIK/blob/master/module/Applications/view/applications/index/disclaimer.phtml
.. _jobs/sidebar/index: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/sidebar/index.phtml
.. _jobs/form/list-filter: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/form/list-filter.phtml
.. _jobs/form/apply-identifier: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/form/apply-identifier.phtml
.. _jobs-publish-on-yawik: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/modals/yawik.phtml
.. _jobs-publish-on-jobsintown: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/modals/jobsintown.phtml
.. _jobs-publish-on-homepage: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/modals/homepage.phtml
.. _jobs-terms-and-conditions: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/jobs/index/terms.phtml
.. _mail/jobCreatedMail: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/view/mails/jobCreatedMail.phtml
.. _pdf/application/details/button: https://github.com/cross-solution/YAWIK/blob/master/module/Pdf/view/applicationDetailsButton.phtml
.. _geo/form/GeoText: https://github.com/cross-solution/YAWIK/blob/master/module/Geo/view/form/geotext.phtml
.. _organizations/index/edit: https://github.com/cross-solution/YAWIK/blob/master/module/Organizations/view/organizations/index/form.phtml


Mail Templates
^^^^^^^^^^^^^^
+--------+---------------------------+---------------------------------------------------------------------------------+
| Module | Name                      | Description                                                                     |
+========+===========================+=================================================================================+
|Auth    | register_                 | sends a confirmation link to the user, after registration                       |
+--------+---------------------------+---------------------------------------------------------------------------------+
|Auth    | forgot-password_          | sends a confirmation link to the user, after using the forgot password feature  |
+--------+---------------------------+---------------------------------------------------------------------------------+
|Auth    | first-external-login_     | sends the user login data, after the user wa created by an external application |
+--------+---------------------------+---------------------------------------------------------------------------------+
|Auth    | first-socialmedia-login_  | sends the user a welcom mail after the first login via a social network         |
+--------+---------------------------+---------------------------------------------------------------------------------+

.. _forgot-password: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/forgot-password.phtml
.. _register: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/register.phtml
.. _first-socialmedia-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-socialmedia-login.phtml
.. _first-external-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-external-login.phtml


Services
^^^^^^^^

+---------+-----------------------+-----------------------------+
| Module  | Name                  | Description                 |   
+=========+=======================+=============================+
|Core     | Core/Log              | Logging service             |
+---------+-----------------------+-----------------------------+
|Auth     | HybridAuthAdapter     | Login via Social Networks   |
+---------+-----------------------+-----------------------------+
|Auth     | AuthenticationService | Authentication Service      |
+---------+-----------------------+-----------------------------+

Notifications
^^^^^^^^^^^^^

Every notification or message, no matter how it will be displayed or returned, runs through an unified API.
This API is implemented in the Controller-Plugin 'notification'.
Notifications are session-persistent, that implies, they will pop up either on the current site, or on a following site.
So unless you are sure of it, make no references to a current page, because the notification may pop up on a different page.

The common use is:

.. code-block:: php

    $this->notification('any text');
    $this->notification()->success('any text');
    $this->notification()->error('any text');
    $this->notification()->info('any text');

To display notifications on a html-page, insert somewhere in the script or layout.
In the standard-layout this partial is already included.

.. code-block:: php

    echo $this->partial('core/notifications');

If you have an ajax-request and expect back a JSON,
the JSON-response should include information about notifications.
You have to trigger an event with the whole response as data.

.. code-block:: javascript

    $.post(url, param, function(data) {
        $(this).trigger('ajax.ready', {'data': data});
    })