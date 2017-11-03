.. index:: Solr
.. _solr:

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

.. note:: Debian 8 ships with php5-solr 1.0.2. You can build your solr extension by:

    .. code-block:: sh

        aptitude install php5-dev libcurl4-openssl-dev libxml2-dev
        pecl install solr
        echo "extension=solr.so" > /etc/php5/mods-available/solr.ini
        php5enmod solr
        php -m| grep solr # should show the activated solr extension


Good resources on how to install solr:

* https://cwiki.apache.org/confluence/display/solr/Installing+Solr
* http://nl3.php.net/manual/en/solr.installation.php

Here is the way we've installed it in our Demo. First, you need JAVA. On Debian 8 you can install it via:

.. code-block:: sh

    apt install -t jessie-backports  openjdk-8-jre-headless ca-certificates-java


then get a binary version of solr. The binary package contains an installation script. So unzip/untar it and execute the
installation script. By default you'll find your solr server in :file:`/opt/solr/`. The solr data are stored in
:file:`/var/solr/data/`. After the installation you can remove the downloaded and extracted files.


.. code-block:: sh


   > wget http://apache.lauf-forum.at/lucene/solr/6.6.0/solr-6.6.0.tgz
   > tar xzf solr-6.6.0.tgz
   > solr-6.6.0/bin/install_solr_service.sh solr-6.6.0.tgz


After the installation, solr server ist running at localhost port 8983. This is enough for yawik to be able the access
the solr Server.

If you want to be able the access the solr frontend via https without touching the solr installation at all, an apache
proxy may be a solution. If you want to use this solution, you have to enable the apache proxy module.


.. code-block:: sh

    > a2enmod proxy proxy_http

For setting up an apache Proxy you can use a Virtual Host which looks like

.. code-block:: sh

    <VirtualHost *:8443>

         ProxyRequests Off
         <Proxy *>
            AuthType Basic
            AuthName "Solr Search"
            AuthBasicProvider file
            AuthUserFile /etc/apache2/solr.passwd
            Require valid-user
            Order deny,allow
            Allow from all
         </Proxy>

         ProxyPass / http://localhost:8983/
         ProxyPassReverse / http://localhost:8983/

    </VirtualHost>


Set the the user/pass in :file:`/etc/apache2/solr.passwd` via :command:`htpasswd /etc/apache2/solr.passwd username`





Installation
^^^^^^^^^^^^

to install the `yawik/solr`_ Modul into a running YAWIK, change into the `YAWIK/modules` directory and clone
the yawik/solr module .

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

.. note:: at least one field needs JTS. So if you want to use the contributed schema, you have to install JTS
    via:

    .. code-block:: sh

        mkdir tmp
        cd tmp
        wget wget https://downloads.sourceforge.net/project/jts-topo-suite/jts/1.14/jts-1.14.zip
        unzip jts-1.14.zip
        cp lib/*.jar /opt/solr-6.6.0/server/solr-webapp/webapp/WEB-INF/lib/


    Or take a look at the issue https://github.com/yawik/Solr/issues/4 . Maybe the fiels using JTS is not needed by
    YAWIK any more.


If you want to set a user/password for solr you first have to enable an `Authorization Plugin`_.  Since Solr6 you can do
so by copying the following json to :file:`/var/solr/data/security.json`

.. ::

    {
    "authentication":{
       "blockUnknown": true,
       "class":"solr.BasicAuthPlugin",
       "credentials":{"solr":"IV0EHq1OnNrj6gvRCwvFwTrZ1+z1oBbnQdiVC3otuq0= Ndd7LKvVBAaZIF0QAVi1ekCfAJXr1GGfLtRUXhgrF8c="}
    },
    "authorization":{
       "class":"solr.RuleBasedAuthorizationPlugin",
       "permissions":[{"name":"security-edit",
          "role":"admin"}],
       "user-role":{"solr":"admin"}
    }}


This will add a user "solr" with the password "SolrRocks". After that you can change the password with

.. _Authorization Plugin: https://lucene.apache.org/solr/guide/6_6/basic-authentication-plugin.html

.. code-block:: sh

    curl --user solr:SolrRocks http://localhost:8983/solr/admin/authentication -H 'Content-type:application/json' \
        -d '{"set-user": {"solr" : "myPassword"}}'


you can initially index all active jobs by:

.. code-block:: sh

 bin/console solr index job

Schema
^^^^^^

==================================== ===================================================================================
 fields
==================================== ===================================================================================
 id                                   Primary key
 title                                Job title
 city                                 city of the job opening
 lang                                 language of the job opening
 entityName                           possible values "job", "location" or "organization"
 *_MultiString*                       Used by categories. E.g. region_MultiString, industry_MultiString,
                                      profession_MultiString
==================================== ===================================================================================


Description
^^^^^^^^^^^

YAWIK entities are searchable using the fulltext feature offered by mongodb. These features are great and normally
sufficient, to offer e.g. jobs on a career page. If you want to use YAWIK as a jobboard, the requirements increase.
A jobboard normally offers millions of jobs to millions of visitors. At first you need a scaling search engine.
Currently Solr is supported.

Using the solr module, you'll get full featured search engine offering the following features:

* facet searches (e.g. list of categories showing possible matches)
* highlight matches in the search result

