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


If you want to customize the layout, you can do so by writing a plugin. Create a directory "MyPlugin" and map :ref:`templates <templates>` 
to your own views scripts. If you want e.g. add an additional javascrip for click tracking (Piwik, Google Analytics or whatever) without touching the sources, 
you can create a module ``MyModule``. Name it Module.php and put it into the directory ``module/MyModule`` and modify your layout.phtml.

.. code-block:: sh

  <?php
     
  namespace MyModule;
  
  class Module
  {
    public function getConfig()
    {
       return array('view_manager' => array(
                      'template_map' => array(
                        'layout/layout' => __DIR__ . '/layout.phtml',
                                             ),
                                           ),  
                                         );    
    }
  }
 
 

copy ``module/Core/view/layout/layout.phtml`` into your modules directory and start to customize your layout. 

.. note::

   If the name of your module stats with "Cam", you can put it outside of the
   repository into the ``vendor/extern`` directory`.


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

.. _lessc: http://lesscss.org/#using-less
.. _sources: https://github.com/cross-solution/CrossApplicantManager/tree/master/less
.. _make-css.sh: https://github.com/cross-solution/CrossApplicantManager/blob/master/less/make-css.sh

