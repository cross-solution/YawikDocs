.. index:: Core; Options

Options
-------

To modify the options, copy the module.core.options.local.php.dist_ to you ``config/autoload`` directory, remove the
``.dist`` prefix and adjust the values

+-------------------+--------+----------------------------------------------------------------------------------------+
|Name               | type   | description                                                                            |
+===================+========+========================================================================================+
|siteName           | string | The siteName is used in Mails. Typically it's the name of your website                 |
+-------------------+--------+----------------------------------------------------------------------------------------+
|operator           | array  | Contact Data, which can be used in Mail signatures or the imprint page                 |
+-------------------+--------+----------------------------------------------------------------------------------------+
|supportedLanguages | array  | supported frontend languages a user can switch to                                      |
+-------------------+--------+----------------------------------------------------------------------------------------+
|defaultLanguages   | string | default language to use, if no language is set. Default "en"                           |
+-------------------+--------+----------------------------------------------------------------------------------------+
|detectLanguage     | bool   | if enabled, YAWIK tries to detect the language from browser settings                   |
|                   |        | (if no language is set in the users settings)                                          |
+-------------------+--------+----------------------------------------------------------------------------------------+
|defaultCurrency    | string | default currency to use, if no currency is set. Default "USD"                          |
+-------------------+--------+----------------------------------------------------------------------------------------+
|defaultTaxRate     | string | default tax rate to use, if no tax rate is set. Default "19"                           |
+-------------------+--------+----------------------------------------------------------------------------------------+

.. _module.core.options.local.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Core/config/module.core.options.local.php.dist
