Ubuntu 18.04
============

Installation of PHP7.2 and apache2. Ubuntu 18.04 comes with php7.2.3 and ext-mongodb 1.3.4. You'll need at least ext-mongodb ^1.5.0. You'll have to build it
from PECL by yourself or use the great ondrej repos. 

.. code-block:: sh
      
    sudo apt install software-properties-common
    add-apt-repository ppa:ondrej/php

install npm version 10. It's needed to run grunt tasks at the end of the installation.

.. code-block:: sh

    apt install curl
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
    sudo apt-get install -y nodejs

If you want to run php7.2

.. code-block:: sh
    
    apt install php-mongodb php7.2 php7.2-curl php7.2-xsl php7.2-intl php7.2-common php7.2-cli php7.2-json php7.2-gd curl libapache2-mod-php7.2 \
        php7.2-cli apache2 php7.2-xml php7.2-mbstring composer unzip git

With php7.3 we've noticed an issue which leads to crashes in the apache module. At least in LXC containers.