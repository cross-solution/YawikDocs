Debian 8
========

If like to run YAWIK in an `LXC container`_ on proxmox_. If we do so, we prefere debian 8, because it ships with php5.6.
So we do not have to downgrade to php5.6. On the other hand it comes with `sysv`_. However, installing YAWIK on Debian 8
you have to install the following packages.

.. code-block:: sh

  apt-get install php5-mongodb libapache2-mod-php5 php5-curl php5-xsl php5-gd \
                   php5-intl php5-common php5-cli php5-json php5 apache2 curl npm uglifyjs

``npm`` and ``uglifyjs`` are needed to install assets (boostrap, jquery, select2 ...). You're only need those packages,
if you want to install YAWIK git ``cdgit``


.. _LXC container: http://download.proxmox.com/images/system/
.. _proxmox: https://www.proxmox.com/de/
.. _sysv: https://forum.proxmox.com/threads/debian-8-6-lxc-template-with-systemd-feature-request.30212/
