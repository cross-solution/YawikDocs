.. index:: Import

.. _import:

SimpleImport
------------

.. sidebar:: SimpleImport

   =======================  ==========================================
   ``Repository``            `yawik/SimpleImport`_
   ``coverage``              |coverage|
   ``buid``                  |build|
   =======================  ==========================================

.. |coverage| raw:: html

	<a href='https://coveralls.io/github/yawik/SimpleImport?branch=master'><img src='https://coveralls.io/repos/github/yawik/SimpleImport/badge.svg?branch=master' alt='Coverage Status' /></a>


.. |build| raw:: html

        <a href="https://travis-ci.org/yawik/SimpleImport"><img src="https://travis-ci.org/yawik/SimpleImport.svg?branch=master"></a>



.. _yawik/SimpleImport: https://github.com/yawik/SimpleImport.git


The SimpleImport module offers a command line tool to import jobs from feeds. It's usefull, if you plan to use YAWIK as a jobportal and if you would like to import jobs from customers.


.. code-block:: sh

    Simple import operations
      console simpleimport import [--limit]                                                                           Executes a data import for all
                                                                                                                      registered crawlers
      console simpleimport add-crawler --name --organization= --feed-uri [--runDelay] [--type] [--jobInitialState]    Adds a new import crawler

      --limit=INT                 Number of crawlers to check per run. Default 3. 0 means no limit
      --name=STRING               The name of a crawler
      --organization==STRING      The ID of an organization
      --feed-uri=STRING           The URI pointing to a data to import
      --runDelay=INT              The number of minutes the next import run will be proceeded again
      --type=STRING               The type of an import (e.g. job)
      --jobInitialState=STRING    The initial state of an imported job




Feeds have to be formatted as defined in :ref:`the scrapy docs<scrapy:format>`.


Example: Add a feed to a an organization

.. code-block:: sh

    root@yawik:/var/www/YAWIK# ./bin/console simpleimport add-crawler --name=example-crawler \
                                                                      --organization=59e4b53e7bb2b553412f9be9 \
                                                                      --feed-uri=http://ftp.yawik.org/example.json
    A new crawler with the ID "59e4b5a87bb2b567468b4567" has been successfully added.


This command created a crawler in the mongo collection ``simpleimport.crawler`` and returns the ObjectId.


.. code-block:: sh

    > db.simpleimport.crawler.find({"_id":ObjectId("59e4b5a87bb2b567468b4567")}).pretty();
    {
            "_id" : ObjectId("59e4b5a87bb2b567468b4567"),
            "name" : "example-crawler",
            "organization" : ObjectId("59e4b53e7bb2b553412f9be9"),
            "type" : "job",
            "feedUri" : "http://ftp.yawik.org/example.json",
            "runDelay" : NumberLong(1440),
            "dateLastRun" : {
                    "date" : ISODate("1970-01-01T00:00:00Z"),
                    "tz" : "+00:00"
            },
            "options" : {
                    "initialState" : "active",
                    "_doctrine_class_name" : "SimpleImport\\Entity\\JobOptions"
            }
    }


.. note:: if you execute the command twice, the crawler will be added twice. If you want to remove a crawler, you have to
    do so on the mongo cli.




