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


.. _layout.phtml: https://github.com/yawik/DemoSkin/blob/master/view/layout.phtml
.. _YawikDemoSkin: https://github.com/yawik/DemoSkin

customize your Skin by mapping more :ref:`templates <templates>` to your own views scripts.

If you want a completely own customized startpage, add a 'startpage' to your viewmap. It will be automatically picked,
when you enter the name of the domain and have no session. But be aware, there is no login-box, unless you integrate
it yourself.


CSS
---

YAWIK comes with bootstrap. Glyphicons are replaced by awesome fonts. The sources_ for for the main CSS
is currently build with lessc.
Bootstrap and awesome font sources are symlinked to the ``vendor`` directory.
CSS files are build by grunt tasks. You can compile the main CSS file by:

.. code-block:: sh

  $ ./node_modules/.bin/grunt less:core
  Running "less:core" (less) task
  >> 1 stylesheet created.

Our YawikDemoSkin_ can be seen as an example, how to modify the CSS. The Skin needs a different height
for the fixed footer. This is achieved by creating a new less file, which can import our
``module/Core/public/less/yawik-core.less``. You can overwrite all less variables.

.. code-block:: sh

  @import "yawik/yawik-core.less";
  @footer-height:                     39px;


.. _sources: https://github.com/cross-solution/YAWIK/tree/master/module/Core/public/less



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
|Location        | autocomplete a location and adds additional Geo data, see: :ref:`Once Click Apply <one-click-apply>`    |
+----------------+---------------------------------------------------------------------------------------------------------+
|Phone_          | adds Validation for a phone number                                                                      |
+----------------+---------------------------------------------------------------------------------------------------------+
|Rating_         | Star rating Element                                                                                     |
+----------------+---------------------------------------------------------------------------------------------------------+
|SpinnerSubmit_  | a spinner icon is added during form validation. While sending data, the submit button is inactivated    |
+----------------+---------------------------------------------------------------------------------------------------------+


.. _Editor: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/Editor.php
.. _FileUpload: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/FileUpload.php
.. _InfoCheckbox: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/InfoCheckbox.php
.. _Phone: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/Phone.php
.. _Rating: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/Rating.php
.. _SpinnerSubmit: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/Form/Element/SpinnerSubmit.php

View Helper Scripts
-------------------

=================== ======================================================================================================
 Name                description
=================== ======================================================================================================
 Alert_              displays notification like error or success
 Services_           can access Services within view view scripts
 jobUrl_             displays the link to a job posting.
 applyUrl_           displays the link to an application form of a job posting.
 applyButton_        displays application buttons. see: :ref:`Geo Module <geo>`
 languageSwitcher_   renders a language switcher select box. see: :ref:`Language Switcher <language-switcher>`
=================== ======================================================================================================


.. _Alert: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/View/Helper/Alert.php
.. _Services: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/View/Helper/Services.php
.. _jobUrl: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/src/View/Helper/JobUrl.php
.. _applyUrl: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/src/View/Helper/ApplyUrl.php
.. _applyButton: https://github.com/cross-solution/YAWIK/blob/master/module/Jobs/src/View/Helper/ApplyButton.php
.. _languageSwitcher: https://github.com/cross-solution/YAWIK/blob/master/module/Core/src/View/Helper/LanguageSwitcher.php