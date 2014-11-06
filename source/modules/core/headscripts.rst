:Author: Mathias Gelhausen <gelhausen@cross-solution.de>

.. index:: Core; Headscripts

Headscripts
^^^^^^^^^^^

To inject script tags (with and without source) to the head section of the rendered output, YAWIK makes use of
the Headscript_ view helper of Zend Framework.

.. _Headscript: http://framework.zend.com/manual/2.3/en/modules/zend.view.helpers.head-script.html


Inject scripts from a view script
=================================

To inject a script tag from a view script:

.. code-block:: php

    <!-- append a file -->
    <?php $this->headscript()->appendFile($this->basePath('path/to/script.js')) ?>

    <!-- prepend a file -->
    <?php $this->headscript()->appendFile($this->basePath('path/to/script.js')) ?>

    <!-- or use another method of Zend Frameworks' helper. -->


Inject scripts via module.config.php
====================================

It is possible to inject head script tags using the module.config.php.

.. code-block:: php

    // inside module.config.php

    return array(
        //...

        'view_helper_config' => array(
            // ...
            'headscript' => array(
                // append a script for all routes. (ommitting base path, it is added automatically)
                'path/to/script.js',

                // append a script for a special route name (or child routes)
                // note: you need to wrap script path in an array due to ZFs' config merging.
                'routename' => array('path/to/script.js'),

                // to prepend a script, you need to pass arguments to the headscript helper:
                'routename' => array(array(Headscript::FILE, 'path/to/script.js', 'PREPEND')),
            ),
        ),
        // ...

    );


.. note::
    The scripts from module.config.php are not included, if you use the default Headscript helper in your layout.
    You need to retrieve the ConfigHeadscript service from the view plugin manager, as its factory injects the
    scripts.

.. code-block:: php

    <?php echo $this->configHeadscript() ?>

