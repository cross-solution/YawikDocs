.. index:: JobsByMail

JobsByMail
----------

.. sidebar:: JobsByMail

   =======================  ==========================================
   ``Repository``            `yawik/JobsByMail`_
   ``coverage``              |coverage|
   ``build``                 |build|
   =======================  ==========================================

The JobsByMail module offers a simple Formular to sign up to get the latest jobs by email. By activating the module you'll
be able to add the subscriber in your view form by adding the line ``<?=$this->proxy('jobsByMailSubscriptionForm')->render()?>``

Features

* view script for the `subscriber form`_ and a `result page`_.
* form ist pre-filled with the latest search parameters
* form can be used as an authenticated and as an anonymous user
* module works with or without the :ref:`solr module<solr>`

If the form is used by an anonymous users, a confirmation mail is send to the subscriber. Search profiles width
confirmed email addresses will receive new jobs my mail.

The information Mail about new Jobs contains an unsubscribe Link.

.. _subscriber form: https://github.com/yawik/JobsByMail/blob/develop/view/jobs-by-mail/form/subscribe/form.phtml
.. _result page: https://github.com/yawik/JobsByMail/blob/develop/view/jobs-by-mail/form/subscribe/form.phtml

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

