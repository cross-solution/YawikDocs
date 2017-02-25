.. index:: Solr

Solr
----

.. sidebar:: Solr

   =======================  ==========================================
   ``Repository``            `yawik/solr`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

.. |coverage| raw:: html

	<a href='https://coveralls.io/github/yawik/Solr?branch=develop'><img src='https://coveralls.io/repos/github/yawik/Solr/badge.svg?branch=develop' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/Solr"><img src="https://travis-ci.org/yawik/Solr.svg?branch=master"></a>


Requirements
^^^^^^^^^^^^

current development is using:

* php5-solr (pecl >= 2.4.0)
* apache solr (6.1)

Good resources on how to install solr:

* https://cwiki.apache.org/confluence/display/solr/Installing+Solr
* http://nl3.php.net/manual/en/solr.installation.php

Installation
^^^^^^^^^^^^

to install the `yawik/solr`_ Modul into a running YAWIK, change into the `YAWIK/modules` directory and clone
the yawik/solr module.

.. code-block:: sh

 git clone https://github.com/yawik/Solr

To activate the module create a php file named ``WhateverYouWant.module.php`` in your config autoload directory containing:

.. code-block:: php

 <?php
 return ['Solr'];

To configure the solr connection copy the Solr options file into you autoload directory and adjust the values.

.. code-block:: sh
 
  cp module/Solr/config/solr.moduleoptions.local.php.dist config/autoload/solr.moduleoptions.local.php

.. note::

 Solr needs a schema. The schema is currently a work in progress. You can use the schema in `Solr/contrib`_.

.. _yawik/solr: https://github.com/yawik/Solr
.. _Solr/contrib: https://github.com/yawik/Solr/tree/master/contrib


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

