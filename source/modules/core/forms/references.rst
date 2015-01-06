:Author: Mathias Gelhausen <gelhausen@cross-solution.de>
:Author: Mathias Weitz <weitz@cross-solution.de>

.. index:: Core; Forms; Forms

Build-In form classes and helpers
*********************************

[TODO: Fill in.. ]

Form classes
============

\\Core\\Form\\Form
------------------

This is the very base YAWIK form class, which extends \\Zend\\Form\\Form.

It implements \\Core\\Form\\DescriptionAwareFormInterface and
\\Core\\Form\\DisableElementsCapableInterface.

It sets the default hydrator to \\Core\\Entity\\Hydrator\\EntityHydrator (which allows the form to bind YAWIK entities.)

\\Core\\Form\\BaseForm
----------------------

An extension of \\Core\\Form\\Form, which creates a form with a target fieldset and a default buttons fieldset.

It is meant to provide a ad-hoc solution for creating forms with a consistent look and handling.

\\Core\\Form\\Container
-----------------------

The Container bundles several forms together, which work on one entity, enabling them to patch their behaviour together.
Container have some specific methods for identifying or handle an explicit form. Most of these methods just pass some information
to all subsequent forms

.. code-block:: php

    setParams(array $params)

is placing a hidden input filed in every subordinated forms. This comes in handy for the identification of an entitity.

.. code-block:: php

    setEntity(EntityInterface $entity)


Interfaces
==========

View helpers
============

\\Core\\Form\\View\\Helper\\FormContainer
-----------------------------------------

\\Core\\Form\\View\\Helper\\Form
--------------------------------

\\Core\\Form\\View\\Helper\\SummaryForm
---------------------------------------


