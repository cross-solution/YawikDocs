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


If you want to customize the layout, you can do so by writing a plugin. Create a directory "MyPlugin" and map all :ref:`templates <templates>` 
to your own views scripts.

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







