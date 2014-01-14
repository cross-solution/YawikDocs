Modules
=======

we use module system of the ZF2_.

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

