Modules
=======

we use module system of the ZF2_. Modules are configured in their ``config`` directory. 
You can use multiple configuration files by using the \Core\ModuleManager\ModuleConfigLoader utility.
This way you can split up your configuration in smaller chunks (e.g. put all your configuration about routings into a 
``router.config.php`` and about templating into a ``template.congig.php``), which are easier to find, read and maintain.

.. _ZF2: http://framework.zend.com/manual/2.0/en/modules/zend.module-manager.intro.html

Modules can simply be enabled by adding their names to an array in `config/config.php`_.

.. _config/config.php: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/notifications.phtml

.. code-block:: php
   :linenos:

   <?php
   $modules = array(
         'DoctrineModule', 
         'DoctrineMongoODMModule', 
         'Core',
         'Auth',
         'Cv',
         'Applications',
         'Jobs',
         'Organizations',
         'Settings',
         'Pdf',
         'Geo',
         'FormularValidation',
    );

   ...
   ?>

Directory Structure of a module

+----------+-------------------------------------+---------------------------------+
|directory |description                          |example                          |
+==========+=====================================+=================================+
|language  | contains gettext language files     | .. image:: images/module.png    |
+----------+-------------------------------------+                                 |
|public    | place for images, css or javascript |                                 |
+----------+-------------------------------------+                                 |
|config    | place for configuration files       |                                 |
+----------+-------------------------------------+                                 |
|test      | place for unit tests                |                                 |
+----------+-------------------------------------+                                 |
|src       | Controllers, Models etc.            |                                 |
+----------+-------------------------------------+                                 |
|view      | view scripts                        |                                 |
+----------+-------------------------------------+---------------------------------+


A module can implement the following Features:

* Dashboard Widgets
* Configuration formulars
* Command line tools


currently the following modules exists:

.. toctree::
   :maxdepth: 2

   modules/core/index
   modules/auth/index
   modules/cv/index
   modules/applications/index
   modules/jobs/index
   modules/pdf/index
   modules/geo/index

