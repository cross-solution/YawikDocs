.. index:: JobsByMail

JobsByMail
----------

.. sidebar:: JobsByMail

   =======================  ==========================================
   ``Repository``            `yawik/JobsByMail`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

.. |coverage| raw:: html

	<a href='https://coveralls.io/github/yawik/JobsByMail?branch=develop'><img src='https://coveralls.io/repos/github/yawik/JobsByMail/badge.svg?branch=develop' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/JobsByMail"><img src="https://travis-ci.org/yawik/JobsByMail.svg?branch=develop"></a>


Requirements
^^^^^^^^^^^^


Installation
^^^^^^^^^^^^

to install the `yawik/JobsByMail`_ Modul into a running YAWIK, change into the `YAWIK/modules` directory and clone
the yawik/solr module.

.. code-block:: sh

 git clone https://github.com/yawik/JobsByMail

To activate the module create a php file named ``WhateverYouWant.module.php`` in your config autoload directory containing:

.. code-block:: php

 <?php
 return ['JobsByMail'];

.. _yawik/JobsByMail: https://github.com/yawik/JobsByMail
