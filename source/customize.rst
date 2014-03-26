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
you can create a module ``MyModule``. Put it into the directory ``vendor/extern/MyModule`` and modify your layout.phtml.

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


CSS
---

YAWIK comes with bootstrap. Glyphicons are replaced by awesome fonts. The css for the complete application 
is currently build with lessc. 




