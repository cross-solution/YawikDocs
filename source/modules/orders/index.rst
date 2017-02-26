.. index:: Orders

Orders
------

.. sidebar:: Orders

   =======================  ==========================================
   ``Repository``            `yawik/orders`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

.. |coverage| raw:: html

        <a href='https://coveralls.io/github/yawik/Orders?branch=master'><img src='https://coveralls.io/repos/github/yawik/Orders/badge.svg?branch=master' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/Orders"><img src="https://travis-ci.org/yawik/Orders.svg?branch=master"></a>



.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/orders/chart/image_png"/>
    <br/>translation state of Orders module.
    </div>

Requirements
^^^^^^^^^^^^

a running YAWIK

Installation
^^^^^^^^^^^^


to install the `yawik/orders`_ Module into a running YAWIK, change into the `YAWIK/modules` directory and clone
the yawik/orders module.

.. code-block:: sh

 git clone https://github.com/yawik/Orders

To activate the module create a php file named ``WhateverYouWant.module.php`` in your config autoload directory containing:

.. code-block:: php

 <?php
 return ['Orders'];

.. _yawik/orders: https://github.com/yawik/Orders


Description
^^^^^^^^^^^

the oder module injects a billing address to to wizard for entering job postings. the order module adds a storage for orders. By submitting a job posting, an order is created. 
The order contains all relevant data needed for billings. In addition, the module adds an invoice formular, which can be added into the order
process. Default values of the invoice formular can be set in Settings/Orders.

Technically, the oder module offers the feature to take a snapshot of an entity.


