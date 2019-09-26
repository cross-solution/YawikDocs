Install mongo Database
======================

https://docs.mongodb.com/manual/installation/
YAWIK runs with mongo 2.4. So you can use the mongod version, which is shipped with your distribution. However, you
should use a later version. Otherwise you have to `enable the text search`_, which is disabled in 2.4 by default.
In 2.6 and above the text search is enabled by default.

.. _enable the text search: https://docs.mongodb.com/v2.4/tutorial/enable-text-search/

You can install e.g. mongo 3.2 by: (Our demo is running 3.2, development is done with 4.x)


https://docs.mongodb.com/manual/administration/install-on-linux/

We've installed mongo the following way:

.. code-block:: sh

 sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
 echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
 sudo apt-get update
 sudo apt-get install -y mongodb-org

If your linux comes with systemd, you can start your mongod with ``service mongo start``. If you need an init script,
because your linux comes with `sysv`_, you can fetch it from mongodb github repository

.. code-block:: sh

    cd /etc/init.d/
    curl https://raw.githubusercontent.com/mongodb/mongo/master/debian/init.d > mongod
    chmod +x mongod
    update-rc.d mongod defaults

Start your mongod with ``/etc/init.d/mongod start``


.. _sysv: https://forum.proxmox.com/threads/debian-8-6-lxc-template-with-systemd-feature-request.30212/
