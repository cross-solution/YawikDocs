.. index:: Applications

Applications
------------

.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/applications/chart/image_png"/>
    <br/>translation state of Applications module
    </div>

the application module offers an application formular, a list of applications and
a detail view of an application. Depending on the users privileges the detail
view offers a way to invite or reject an applicant, to rate an application or to
forward an application by email.

If the :ref:`PDF` Module is installed, the Application can be downloaded as a PDF
document with attachments and social profiles embedded.

Options
^^^^^^^

You can configure the possible mime-types or the maximum size of attachments by copying the applicationOptions_ into
your config/autoload directory. Remove the ".dist" extention and adjust the values.

.. _applicationOptions: https://github.com/cross-solution/YAWIK/blob/develop/module/Applications/config/applications.forms.global.php.dist

.. code-block:: php

  $options = array(
        /*
        * maximum size in bytes of an uploaded attachment, default 5MB
        */
        'attachmentsMaxSize' => '5000000',

        /*
        * allowed Mime-Type of an uploaded Attachment, default images, *.PDF, *.DOC, *.ODT
        */
        'attachmentsMimeType' => array('image','application/pdf', 'application/vnd.oasis.opendocument.text', 'application/msword'),


        /*
        * maximum amount of uploaded attachments
        */
        'attachmentsCount' => 5,

        /*
        * maximum size in bytes of an uploaded contact photo. default 500kB
        */
        'contactImageMaxSize' => '500000',

        /*
        * allowed Mime-Type of an uploaded contact photo
        */
        'contactImageMimeType' => array('image'),

        /*
        * allowed Mime-Types, images, plain text, *.PDF, *.DOC, *.ODT
        */
        'allowedMimeTypes' => array('image','text','application/pdf', 'application/vnd.oasis.opendocument.text', 'application/msword'),

    );


AbstractIdentifiableModificationDateAwareEntity

Events
^^^^^^

you can attach Listeners to the following events

+----------------------------------------+---------------------------+-----------------------------------------------------------------------+
|Name                                    |                           | description                                                           |
+========================================+===========================+=======================================================================+
| EVENT_APPLICATION_POST_CREATE          | application.post.create   | Thrown, after an application was saved in the Database                |
+----------------------------------------+---------------------------+-----------------------------------------------------------------------+
| EVENT_APPLICATION_PRE_DELETE           | application.pre.delete    | Thrown, befor an application is removed from the Database             |
+----------------------------------------+---------------------------+-----------------------------------------------------------------------+
| EVENT_APPLICATION_STATUS_CHANGE        | application.status.change | Thrown, befor an application is removed from the Database             |
+----------------------------------------+---------------------------+-----------------------------------------------------------------------+

API
^^^

It is possible to create an application through POST request to
`api/apply` passing in the apply id of the job ad as query parameter.

The data must be sent with the content type `multipart/form-data`

+-----------------------------------------------+------------------------------------------------------------------+
| Field                                         | Value                                                            |
+===============================================+==================================================================+
| Contact                                       |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[gender]                               |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[first_name]                           | First name                                                       |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[last_name]                            | Last name                                                        |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[birthday]                             | YYYY-mm-dd                                                       |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[street]                               |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[house_number]                         |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[postal_code]                          |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[city]                                 |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[country]                              |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[email]                                |                                                                  |
+-----------------------------------------------+------------------------------------------------------------------+
| contact[image]                                | user image (avatar) (must be an image)                           |
+-----------------------------------------------+------------------------------------------------------------------+

Every property of an application and its embedded documents can be send using the above mapping stategy.
Field name 'attachments[]' sends a file as attachment for example.

The response is a json string.

.. code-block::
    { "status": "OK" }

    { "status": "Error", "message": "" }




Workflow
^^^^^^^^

