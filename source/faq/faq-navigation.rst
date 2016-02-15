===============
FAQ: Navigation
===============


How can I add a Link to the Navigation?
----------------------------------------

Place the following
configuration into your ``autoload/my-navigation.local.php``


.. code-block:: php

    <?php
    return [
        'navigation' => [
            'default' => [
                'My-Identifier' => [
                    'label' => 'Bewerbungsverwaltung',
                    'route' => 'lang/applications',
                    'order' => 100,
                    'pages' => [
                        'Identifier-Page-1' => [
                            'label' => 'Page 1',
                            'route' => 'lang/applications',
                        ],
                        'Identifier-Page-2' => [
                            'label' => 'Page 2',
                            'route' => 'lang/applications',
                        ],
                    ],
                ],
            ],
        ],
    ];


How can I remove Mait templates from the settings menu?
-------------------------------------------------------

Modules can implement SettingEntities. If they do so, they will be automatically inserted into the navigation.
If you want to disable this feature, you can unset Modules Settings in your configuration. Place the following
configuration into your ``autoload/my-navigation.local.php``


.. code-block:: php

    <?php
    return [
        'Applications' => [
            'settings' => null,
        ],
        'Core' => [
            'settings' => null,
        ]
    ];



How can I add a Link only for Recruiters?
-----------------------------------------

Place the following
configuration into your ``autoload/my-navigation.local.php``

.. code-block:: php

    <?php
    return [
        'acl' => [
            'rules' => [
                'recruiter' => [
                    'deny' => [
                        'route/lang/applications',
                    ],
                ],
            ],
        ]
    ]


