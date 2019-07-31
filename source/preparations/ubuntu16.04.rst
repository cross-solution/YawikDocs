Ubuntu 16.04
============

We assume, you have a running mongod. Otherwise check :ref:`getting a mongo db<get_mongo>`

YAWIK should run on all operating systems, which support PHP >=7.2. You have to install php7.2 on ubuntu16.04


.. code-block:: sh
   	
  LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
  aptitude update
  aptitude install php5.6-mongodb php5.6-gd php5.6-curl php5.6-xsl php5.6-intl php5.6-common php5.6-cli php5.6-json curl php-mbstring

 aptitude install unzip npm

