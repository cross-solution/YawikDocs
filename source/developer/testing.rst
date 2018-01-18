Behat
=====

Behat tests are executing scenarios within a browser. Do do so, you need a running YAWIK Installation, the virtual
framebuffer ``xvfb`` and the selenium.

The framebuffer can be installed via ``apt-get install xvfb``. Once installed it can be started by

.. code-block:: sh

    /sbin/start-stop-daemon --start --quiet --pidfile /tmp/xvfb_99.pid --make-pidfile --background
        --exec /usr/bin/Xvfb -- :99 -ac -screen 0 1680x1050x16


The "browser" is started via.


.. code-block:: sh

  java -jar /home/cbleek/Projects/YAWIK/vendor/se/selenium-server-standalone/bin/selenium-server-standalone.jar \
        -Dwebdriver.chrome.driver=/usr/chromedriver


The tests itself are started.

.. code-block:: sh

    APPLICATION_ENV=development ./vendor/bin/behat --strict \
        --no-interaction -vvv -f progress  --tags="@javascript && ~@todo && ~@skip-travis"

