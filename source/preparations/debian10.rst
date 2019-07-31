Debian 10
=========

Debian 10 comes with PHP7.3 by default. 

.. code-block:: sh

  sudo apt install php-mongodb libapache2-mod-php php-curl php-gd php-intl php-json php-dom curl gzip git php composer npm

This installs everything to install YAWIK via composer.

.. note:: ``npm`` is only needed because at the end of the installation a few grunt tasks copy images, generate CSS and 
  compress JS. It's a good idea not to install it the apt, but via https://github.com/nodesource/distributions




