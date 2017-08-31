.. index:: Core; Navigation

Navigation
----------

YAWIK uses `Zend/Navigation`_. The following example shows, how you can modify the navigation.
Our Jobboard_ makes YAWIK running like a Jobboard. On a jobboard a navigation normally
contains a public link to employers, who are offering jobads. No authentication is required to
see the list of companies. This can be configured like:

.. code-block:: php

     'acl' => array(
            'rules' => array(
                    // guests are allowed to see a list of companies.
                    'guest' => array(
                            'allow' => array(
                                    'route/lang/organizations',
                             ),
                     ),
             ),
      ),

If YAWIK runs as an Applicant Tracking System (like in our YawikDemoSkin_), a list of companies may contain the customers of
a hr company. Such a list must not be show to the public. This can be configured like:

.. code-block:: php

     'acl' => array(
            'rules' => array(
                    // guests must not see a list of companies.
                    'guest' => array(
                            'deny' => array(
                                    'route/lang/organizations',
                             ),
                     ),
                    // recruiters see the link
                    'recruiter' => array(
                            'allow' => array(
                                    'route/lang/organizations',
                             ),
                     ),
             ),
      ),


.. _`Zend/Navigation`: http://framework.zend.com/manual/2.0/en/modules/zend.navigation.quick-start.html
.. _Jobboard: https://github.com/yawik/Jobboard
.. _YawikDemoSkin: https://github.com/cbleek/YawikDemoSkin