============
FAQ: General
============


File Upload does not work?
--------------------------

when trying to upload a file, the status wheel turns forever. Uploaded file is not stored.

This happens, if a javascript error occurse. You can only debug such a problem by using firebug_ or comparable developer
tools.
The MimeType of uploaded files is checked by default using the libmagic. Please make sure that:

 * the fileinfo extention exists. On FreeBSD, this extension has to be installed. On Linux, this extention is normally included by default. Check it by:  ``php -m | grep fileinfo``
 * Make sure, your Webserver can access ``/usr/share/misc/magic*``. These files are referenced by YAWIK/vendor/zendframework/zend-validator/src/File/MimeType.php
 * make sure the access is not restricted by an open_basedir setting

.. _firebug: https://addons.mozilla.org/en-US/firefox/addon/firebug/


File Upload shows "An unknown error occured" on large files
-----------------------------------------------------------

When the upload seems to work, but at the end, it shows an "An unknown error occured", and in the
``log/error.log`` appears a line like

    "ERR POST Content-Length of 16414047 bytes exceeds the limit of 8388608 bytes (errno 2)"

you should check that you set all required configuration values.

 * The allowed max size must be set in the yawik configurations
   .e.g. for attachments in an application the option 'attachmentsMaxSize' in the file ``config/autoload/applications.forms.global.php``
   must be set appropriatly.
 * The php.ini value of 'upload_max_size' must also be set accordingly. Either in the php.ini or (for apache) via 'php_admin_value'
 * Do not forget the 'post_max_size' php.ini option.

