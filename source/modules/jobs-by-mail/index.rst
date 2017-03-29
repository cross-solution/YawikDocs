.. index:: JobsByMail

JobsByMail (Work in Progress)
-----------------------------

.. sidebar:: JobsByMail

   =======================  ==========================================
   ``Repository``            `yawik/JobsByMail`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

The JobsByMail module offers a simple Formular to sign up to get the latest jobs by email. By activating the module you'll
be able to the Form into the search result `<?= $this->`

Features

* view script for the formular and a result page.
* form ist pre-filled with the latest search parameters
* form can be used as an authenticated and as an anonymous user

If the formular is used by an anonymous users, a confirmation mail is send to the subscriber. Search profiles width
confirmed email adresses will receive new jobs my mail.

The Infomation Mail about new Jobs contains an unsubscribe Link.


.. |coverage| raw:: html

	<a href='https://coveralls.io/github/yawik/JobsByMail?branch=develop'><img src='https://coveralls.io/repos/github/yawik/JobsByMail/badge.svg?branch=develop' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/JobsByMail"><img src="https://travis-ci.org/yawik/JobsByMail.svg?branch=develop"></a>

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


Usage
^^^^^

