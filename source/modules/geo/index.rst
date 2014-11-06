.. index:: Geo

Geo
---

The Core module provides a form-field of the type "Location".
This Form-field should be used whenever a Location i.e. is entered.
In the Core this Form-Field is an alias to a standard Text-Input.

The Geo-Module redirects this Field to an autocompletion-field.
It is still a standard Text-Input, which will be operable even if the connection to the location database is lost.
If the autocompletion is operable, it will provide a list of proposals by name, zip and even country-code.
