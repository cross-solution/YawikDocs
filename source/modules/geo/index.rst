.. index:: Geo
.. _geo:

Geo
---

The Core module provides a form-field of the type "Location". This form-field should be used whenever a Location is
entered. In the Core the type "location" is an alias to a standard form field type "text". So if the Geo module is
inactive, a normal "text" field is used and nothing else happens.

But the Geo Module does a little bit more than just autocomplete the location. It uses a geo location service to enrich
the entered data with geo coordinates and informations about the country and the region. If you enter "Frankfurt am Main",
the location will be defined as:

.. code-block:: sh

 city = Frankfurt am Main
 region = Hessen
 Country = Germany
 corrdinates = [8.6820934,50.1106529], type:"Point"
 

This makes it possible to use the distance feature, when searching e.g. for jobs. The Geo module currently ca use two
different geo location services.

1) the photon_ service
2) the geo service

What's the differences between those services.

+-------------------------+-----------------------------+-------------------------------+
|         Feature         |           photon            |              geo              |
+=========================+=============================+===============================+
| multilingual            | yes                         | no (only german is supported) |
+-------------------------+-----------------------------+-------------------------------+
| countries               | worldwide                   | DE, AT, CH                    |
+-------------------------+-----------------------------+-------------------------------+
| search for postal codes | no                          | yes                           |
+-------------------------+-----------------------------+-------------------------------+
| Ranking                 | nearest by                  | population                    |
+-------------------------+-----------------------------+-------------------------------+
| needed requests         | 1                           | 2                             |
+-------------------------+-----------------------------+-------------------------------+
| Ranking                 | nearest by                  | population                    |
+-------------------------+-----------------------------+-------------------------------+
| synchronized with OSM   | yes                         | no                            |
+-------------------------+-----------------------------+-------------------------------+
| search for streets      | yes                         | no                            |
+-------------------------+-----------------------------+-------------------------------+
| sources available       | yes                         | no                            |
+-------------------------+-----------------------------+-------------------------------+
| free service available  | http://photon.yawik.org/api | http://api.cross-solution.de  |
+-------------------------+-----------------------------+-------------------------------+

The Geo module can be easily configured to use one of the geo services by copying and modifying the
Geo/config/Geo.options.local.php to the autoload directory of you YAWIK installation

.. code-block:: php

 <?php
 /**
  * Name of the used geo coder plugin. You can use 'photon' or 'geo'. Photon is recommended.
  */
 $plugin = 'photon';

 /**
  * Location of your geo coder server. If unsure, leave it unchanged. Possible values are:
  * - http://photon.yawik.org/api
  * - http://api.cross-solution.de/geo
  */
 $geoCoderUrl = 'http://photon.yawik.org/api';

 //
 // Do not change below this line!
 //

 return [
     'options' => [
         'Geo/Options' => [
             'options' => [
                 'plugin' => $plugin,
                 'geoCoderUrl' => $geoCoderUrl,
             ],
         ],
     ],
 ];

.. _photon: http://photon.komoot.de/

It it possible to configure