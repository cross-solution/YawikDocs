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


