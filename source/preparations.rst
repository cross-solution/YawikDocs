Preparations
============

YAWIK needs PHP >=7.2 for execution and the described extensions from the :ref:`requirements<requirements>`.

For the installation via Composer (this is the easiest way at the moment) npm is needed. The Nodes Package Manager 
executes grunt tasks at the end of the installation which copy images, convert LESS to CSS and compress JS. 

Data is stored in a MongoDB. The easiest way is to install a MongoDB locally. If this is not possible, you can use 
a MongoDB provider like `mlab.com`_ or google_.

Apache or nginx can be used as webserver. For testing you can use the PHP buildin server. 

And of course you need composer. 

In the different Linux distributions there are dirverse differences. So you have to proceed differently until an 
installation via composer works.

.. _mlab.com: https://mlab.com/
.. _google: https://console.cloud.google.com/launcher?q=mongodb


.. toctree::
   :maxdepth: 2

   preparations/ubuntu18.04
   preparations/ubuntu16.04    
   preparations/debian10
   preparations/debian8



Install mongo Database
^^^^^^^^^^^^^^^^^^^^^^

YAWIK runs with mongo 2.4. So you can use the mongod version, which is shipped with your distribution. However, you
should use a later version. Otherwise you have to `enable the text search`_, which is disabled in 2.4 by default.
In 2.6 and above the text search is enabled by default.

.. _enable the text search: https://docs.mongodb.com/v2.4/tutorial/enable-text-search/

You can install e.g. mongo 3.2 by: (Our demo is running 2.6, development is done with 3.x)


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
