:Author: Mathias Gelhausen <gelhausen@cross-solution.de>

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



Interfaces
==========

View helpers
============

