Modules
=======

we use module system of the ZF2_. Modules are configured in their ``config`` directory. You can use multiple configuration files. All config files are imported. Their containing assoziativ array is merged. So you can put all your configuration about routings into a 
``router.config.php`` and about templating into a ``template.congig.php``

.. _ZF2: http://framework.zend.com/manual/2.0/en/modules/zend.module-manager.intro.html

Modules can simply be enabled by adding their names to an array in ``config/config.php``.

.. code-block:: php
   :linenos:

   <?php
   $modules = array(
         'Core', /*'TwbBundle', */'Auth', 'Cv', 'Applications', 'Jobs', 'Settings', 'Pdf',
    );

   ...
   ?>

currently the following modules exists:

.. toctree::
   :maxdepth: 2

   modules/core/index
   modules/auth/index
   modules/cv/index
   modules/applications/index
   modules/jobs/index
   modules/pdf/index

