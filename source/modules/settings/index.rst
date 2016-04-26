.. index:: Settings

Settings
--------

The settings module takes settings of other modules.

Eg. The order modules adds the possibility to configure an invoice address. This is simply done by defining a Settings
Entity and a Settings Fieldset. The Settings module ensures that forms are rendered, values are stored and the
navigation is extended by the corresponding sections.

Eg:

https://github.com/cross-solution/YAWIK/blob/develop/module/Orders/src/Entity/SettingsContainer.php

https://github.com/cross-solution/YAWIK/blob/develop/module/Orders/src/Form/InvoiceAddressSettingsFieldset.php


