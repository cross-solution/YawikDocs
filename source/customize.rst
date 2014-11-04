.. _customize:

Customize
^^^^^^^^^

You can activate/deactivate Modules in config/config.php

.. code-block:: sh

   $modules = array(
         'DoctrineModule', 
         'DoctrineMongoODMModule', 
         'Core', 
         'Auth', 
         'Cv', 
         'Applications', 
         'Jobs', 
         'Settings', 
         'Pdf',
    );


If you want to customize the layout, you can do so by writing a plugin. The easiest way is to clone 
the YawikDemoSkin_ into your ``modules`` directory.

.. code-block:: sh
 
 cd modules
 git clone https://github.com/cbleek/YawikDemoSkin

To activate the plugin you can either simply add ``'YawikDemoSkin'`` to your modules array in ``config/config.php``, 
or if you don't want to touch any code from git at all, add an ENV variable e.g. ``APPLICATION_HOST`` to your 
VirtualHost section. In addition create a file ``config/autoload/yawik.module.php``

.. code-block:: sh

  if ((!array_key_exists('APPLICATION_HOST', $_SERVER) || $_SERVER['APPLICATION_HOST'] != "yawik") && !$allModules) {
     return array();
  }
  return array("YawikDemoSkin");

This will add the module dynamically. 

.. _YawikDemoSkin: https://github.com/cbleek/YawikDemoSkin

customize your Skin by mapping more :ref:`templates <templates>` to your own views scripts. 


CSS
---

YAWIK comes with bootstrap. Glyphicons are replaced by awesome fonts. The sources_ for for the main CSS
is currently build with lessc_. 
Bootstrap and awesome font sources are symlinked to the ``vendor`` directory`.
The global CSS file is build with make-css.sh_

you can install lessc on ubuntu by

.. code-block:: sh

  sudo apt-get install npm
  sudo npm install -g less

Our YawikDemoSkin_ can be seen as an example, how to modify the CSS. The Skin needs a different height
for the fixed footer. This is achieved by creating a new less file, which can import our
``yawik/yawik.less`` (a symlink is pointing to it). You can overwrite all less variables.

.. code-block:: sh

  @import "yawik/yawik.less";
  @footer-height:                     39px;

Your customized CSS can be compiled with lessc like:

.. code-block:: sh

 lessc YawikDemoSkin.less ../public/YawikDemoSkin.css


.. _lessc: http://lesscss.org/#using-less
.. _sources: https://github.com/cross-solution/YAWIK/tree/master/less
.. _make-css.sh: https://github.com/cross-solution/YAWIK/blob/master/less/make-css.sh


Formular Fields
---------------

+----------------+---------------------------------------------------------------------------------------------------------+
|Name            |description                                                                                              |
+================+=========================================================================================================+
|Rating_         | Star rating Element                                                                                     |
+----------------+---------------------------------------------------------------------------------------------------------+
|SpinnerSubmit_  | a spinner icon is added during form validation. While sending data, the submit button is inactivated    |
+----------------+---------------------------------------------------------------------------------------------------------+

.. _Rating: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/Form/Element/Rating.php
.. _SpinnerSubmit: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/Form/Element/SpinnerSubmit.php


View Helper Scripts
-------------------

+----------------+---------------------------------------------------------------------------------------------------------+
|Name            |description                                                                                              |
+================+=========================================================================================================+
|Alert_          | displays notification like error or success                                                             |
+----------------+---------------------------------------------------------------------------------------------------------+
|Services_       | can access Services                                                                                     |
+----------------+---------------------------------------------------------------------------------------------------------+


.. _Alert: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/View/Helper/Alert.php
.. _Services: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/View/Helper/Services.php