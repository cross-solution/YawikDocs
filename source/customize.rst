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
or if you don't want to touch any code from git at all, simply put a file named eg. ``config/autoload/MyModule.module.php``
in your autoload directory. Files named *.module.* are read to include additional Modules.

.. code-block:: sh

  <?php
  return array("YawikDemoSkin");

This will add the module dynamically.

If modules contain data like images, javasript or css, which should be directly accessable by the Webserver, these data
should be placed into a directory named ``public``. To make this directory accessible to the Webserver place a symbolic
link into the ``YAWIK/public`` directory, pointing to the modules public directory.

.. code-block:: sh

  cd YAWIK/public
  ln -s ../modules/YawikDemoSkin/public YawikDemoSkin

It is a good practice to name the link with the modules name. This way, you can reference objects of the module by
using the ModulesName within the URL.

Example: The YawikDemoSkin references its css in the layout.phtml_

.. code-block:: php

  $this->headLink()->prependStylesheet($this->basePath() . '/YawikDemoSkin/YawikDemoSkin.css');


Next thing you propably want is to change the name of the Module. Search and replace all "YawikDemoSkin" with "MyModule"
in the sources and rename the Directory "YawikDemoSkin" into "MyModule". Do not forget to change the name in your
"autoload/MyModule.module.php" file.

Now you have a module which you can use as a starting point for modifications.


.. _layout.phtml: https://github.com/cbleek/YawikDemoSkin/blob/master/view/layout.phtml
.. _YawikDemoSkin: https://github.com/cbleek/YawikDemoSkin

customize your Skin by mapping more :ref:`templates <templates>` to your own views scripts.

If you want a completely own customized startpage, add a 'startpage' to your viewmap. It will be automatically picked,
when you enter the name of the domain and have no session. But be aware, there is no login-box, unless you integrate
it yourself.


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
|Editor_         | Editor element                                                                                          |
+----------------+---------------------------------------------------------------------------------------------------------+
|FileUpload_     | FileUpload Form element                                                                                 |
+----------------+---------------------------------------------------------------------------------------------------------+
|InfoCheckbox_   | InfoCheckbox Form element. Adds a Link like to the description Text.                                    |
+----------------+---------------------------------------------------------------------------------------------------------+
|Location_       | autocomplete a location and adds additional Geo data, see: :ref:`Geo Module <geo>`                      |
+----------------+---------------------------------------------------------------------------------------------------------+
|Phone_          | adds Validation for a phone number                                                                      |
+----------------+---------------------------------------------------------------------------------------------------------+
|Rating_         | Star rating Element                                                                                     |
+----------------+---------------------------------------------------------------------------------------------------------+
|SpinnerSubmit_  | a spinner icon is added during form validation. While sending data, the submit button is inactivated    |
+----------------+---------------------------------------------------------------------------------------------------------+


.. _Editor: https://github.com/cross-solution/YAWIK/blob/develop/module/Geo/src/Geo/Form/Editor.php
.. _FileUpload: https://github.com/cross-solution/YAWIK/blob/develop/module/Geo/src/Geo/Form/FileUpload.php
.. _InfoCheckbox: https://github.com/cross-solution/YAWIK/blob/develop/module/Geo/src/Geo/Form/InfoCheckbox.php
.. _Location: https://github.com/cross-solution/YAWIK/blob/develop/module/Geo/src/Geo/Form/GeoText.php
.. _Phone: https://github.com/cross-solution/YAWIK/blob/develop/module/Geo/src/Geo/Form/Phone.php
.. _Rating: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/Form/Element/Rating.php
.. _SpinnerSubmit: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/Form/Element/SpinnerSubmit.php


View Helper Scripts
-------------------

+----------------+---------------------------------------------------------------------------------------------------------+
|Name            |description                                                                                              |
+================+=========================================================================================================+
|Alert_          | displays notification like error or success                                                             |
+----------------+---------------------------------------------------------------------------------------------------------+
|Services_       | can access Services.                                                                                    |
+----------------+---------------------------------------------------------------------------------------------------------+


.. _Alert: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/View/Helper/Alert.php
.. _Services: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Core/View/Helper/Services.php