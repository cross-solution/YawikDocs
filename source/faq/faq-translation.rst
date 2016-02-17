================
FAQ: Translation
================


How can I translate my module?
------------------------------

we use gettext_ for translation as default. Gettext by default scans the sources for ``translate()`` and ``setLabel()``
function calls. In addition, we've defined, that strings following the annotation ``/*@translate*/`` should be
translated as well. This is done by the little script translate_. It scans .php and .phtml files for
``/*@translate*/`` annotations and puts all following strings into the ``module/MyModule/language/_annotated_trings.php``
file.

.. note::

    This mechanism has the limitation, that the string which follows the annotation must be in one line.

Example

.. code-block:: sh

  /*@translate*/ 'this will be found by gettext'

  /*@translate*/
  'this will not be found by gettext'


executing ``bin/translate module/MyModule`` will scan all .php and .phtml files for texts to translate. This will
create .po file in the ``module/MyModule/language`` directory, which you may translate with poedit_

.. _poedit: https://poedit.net/
.. _translate: https://github.com/cross-solution/YAWIK/blob/develop/bin/translate
.. _gettext: https://www.gnu.org/software/gettext/