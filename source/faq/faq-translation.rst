================
FAQ: Translation
================


How can I translate my module
-----------------------------

we use gettext for translation as default. Gettext by default scans the sources for ``translate()`` and ``setLabel()``
function calls. In addition, we'de defined, that strings following the annotation /*@translate*/ should be translated as
well. This is done by a little script in ``bin/translate``.


executing ``bin/translate module/MyModule`` will scan all .php and .phtml files for texts to translate. This will
create .po file in the ``module/MyModule/language`` directory, which you may translate with poedit_

.. _poedit: https://poedit.net/