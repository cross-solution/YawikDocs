.. index:: Solr

Solr
----

this module is deactivated by default, because you need a solr server and the PHP solr pecl extension.

Requirements
^^^^^^^^^^^^

current development is using:

* php5-solr (pecl >= 2.4.0)
* apache solr (6.1)

Installation
^^^^^^^^^^^^

* https://cwiki.apache.org/confluence/display/solr/Installing+Solr
* http://nl3.php.net/manual/en/solr.installation.php

.. note::

 Solr needs a schema. The schema is currently a work in progress. You can use the schema in "Solr/contrib"_.

.. _Solr/conrtib: https://github.com/yawik/Solr/tree/master/contrib

copy the Solr options file into you autoload directory and adjust the value

.. code-block:: sh
 
  cp module/Solr/config/solr.moduleoptions.local.php.dist config/autoload/solr.moduleoptions.local.php


you can initially index all active jobs by:

.. code-block:: sh

 bin/console solr index job


Description
^^^^^^^^^^^

YAWIK entities are searchable using the fulltext feature offered by mongodb. These features are great and normally
sufficient, to offer e.g. jobs on a career page. If you want to use YAWIK as a jobboard, the requirements increase.
A jobboard normally offers millions of jobs to millions of visitors. At first you need a scaling search engine.
Currently Solr is supported.

Using the solr module, you'll get full featured search engine offering the following features:

* facet searches (e.g. list of categories showing possible matches)
* highlight matches in the search result

