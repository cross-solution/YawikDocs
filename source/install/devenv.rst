Install for Developers
======================

if you want to modify the YAWIK code, you should clone the repository from Github. 
The repository does not contain any dependency. You have to import all dependencies by 
executing the ``ìnstall.sh`` script located in the YAWIK root. This scripts imports 
all external libraries via composer. In addition, it creates the directories ``log``, 
``cache`` ùnd  ``config/autoload`` and set the directory permissions to a+w. 

.. code-block:: sh

  git clone https://github.com/cross-solution/YAWIK
  cd YAWIK
  ./install.sh


After the execution you are ready to point your browser to the ``public`` directory.
You'll get the install wizard and after entering the initial user, the database
connection and an email address you are ready to use YAWIK.

At this point your ```config/autoload`` directory contains only one file 
``yawik.config.global.php`` containing the database connection string. The initial user
is created with the ``àdmin`` role in the database.

.. code-block:: sh

    $ ls YAWIK/config/autoload
    yawik.config.global.php

All other configurations are currently done manually by copying the ```*.dist`` files
from the modules configuration directory to the autoload directory and removing the ".dist" part.

.. note::

    To disable the caching of the config autoload files you need to set an environment variable called
    ``APPLICATION_ENV`` to the value "development"

    If you use apache, you can do this in your virtual section config with
    ``SetEnv APPLICATION_ENV="development"``
