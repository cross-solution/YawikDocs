.. _requirements:

Requirements
------------

* php >= php 7.2
* Zend Framework 3
* mongodb >= 3.*
* php-mongodb >= 1.5
* php-intl
* php-gd
* php-curl (only needed to install dependencies via composer)
* php-dom (only needed to install dependencies via composer)
* php-openssl (only needed to install dependencies via composer)
* php-mbstring (only needed, if the PDF module is used)

YAWIK should run on any OS, which supports the above software components. In real life, we've seen YAWIK running on
Linux Ubuntu, Debian, FreeBSD and OSX. It's possible to run YAWIK on AWS.

On FreeBSD, make sure, the php fileinfo extention is available. Fileinfo extention is needed by validating file uploads.

The YAWIK development happens under mainly Ubuntu.

.. _get_mongo: