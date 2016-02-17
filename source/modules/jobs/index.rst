.. index:: Jobs

Jobs
----


.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/jobs/chart/image_png"/>
    <br/>translation state of Jobs module.
    </div>

The Jobs module allows to enter and manage job ads. In addition it generates a 
list of jobs. List of Jobs can be generated in a recruiter (:ref:`recruiter-mode`) 
and a public search (:ref:`search-mode`) mode

The entering process is defined at: http://www.gliffy.com/go/publish/6254781


.. _recruiter-mode:

.. figure:: ../../images/jobs_list-recruiter-mode.png
    :scale: 50%
    :align: right

    Recruiter Mode

in the recruiter mode the recruiter can see active and inactive jobs. In addition the 
list contains informations like number of applications (total/new) or the recruiters
name, who is responsible for the position.

.. _search-mode:


.. figure:: ../../images/jobs_list-search-mode.png 
    :scale: 50%
    :align: right

    Public Search Mode

in search mode the users only see published jobs. This is normally used as a list of
current vacancies, which is often used on a corporate website.

The list mode is defined by the users role.

It is also possible to configure YAWIK to run as a jobboard. There is a `jobboard
module`_ which lets YAWIK act like a jobboard. This module is running on

http://jobs.yawik.org

.. _`jobboard module`: https://github.com/cbleek/YawikDemoJobboard


Job Templates
^^^^^^^^^^^^^

you can create templates_ for entering job ads. All you need is an HTML version of your
job opening. Simply replace the `requirements`, `qualifications` or `benefits` with a small piece
of code. E.g.

.. code-block:: php

    <h4>Requirements:</h4>
    <?php echo $this->requirements;?>

YAWIK replaces this code with an inline Wysiwyg HTML Editor if you want to modify your
job opening. Otherwise the code is replaced by the HTML code, which was entered.

Modifications to the label fields ``labelBenefits``, ``labelQualifications`` and 
``labelRequirements`` are applied to all jobs of company, which are using the template.

You currently can use the following placeholders:

+----------------------------+-------------------------------------+
| Name                       | Description                         |
+============================+=====================================+
| $this->benefits            | Employee benefits                   |
+----------------------------+-------------------------------------+
| $this->city                | City of the company                 |
+----------------------------+-------------------------------------+
| $this->description         | description of the company          |
+----------------------------+-------------------------------------+
| $this->descriptionEditable | editable description of the company |
+----------------------------+-------------------------------------+
| $this->qualifications      | Needed qualifications               |
+----------------------------+-------------------------------------+
| $this->location            | Location of the job                 |
+----------------------------+-------------------------------------+
| $this->labelBenefits       | Label of the Benefits Section       |
+----------------------------+-------------------------------------+
| $this->labelQualifications | Label of the Qualifications Section |
+----------------------------+-------------------------------------+
| $this->labelRequirements   | Label of the Requirements Secion    |
+----------------------------+-------------------------------------+
| $this->oraganizationName   | Name of the company                 |
+----------------------------+-------------------------------------+
| $this->postalCode          | postalCode of the company           |
+----------------------------+-------------------------------------+
| $this->requirements        | requirements of the job posting     |
+----------------------------+-------------------------------------+
| $this->street              | Street of the company               |
+----------------------------+-------------------------------------+
| $this->title               | editable title of the job posting   |
+----------------------------+-------------------------------------+
| $this->titleHead           | title of the job posting            |
+----------------------------+-------------------------------------+
| $this->uriApply            | URL a an application form           |
+----------------------------+-------------------------------------+
| $this->uriLogo             | URL of a company logo               |
+----------------------------+-------------------------------------+

Yawik comes with the example temples "default", "modern" and "classic". If you want to change the Templates within your
Module, you can overwrite the template mapping adding the following configuration to your module config. Eg. you can put
a file ``templates.config.php`` into your ``MyModule/config`` directory.

.. code-block:: php

 <?php
 return ['view_manager' => [
        'templates/default/index' => __DIR__ . '/../view/yourTemplate1/index.phtml',
        'templates/modern/index' => __DIR__ . '/../view/yourTemplate2/index.phtml',
        'templates/classic/index' => __DIR__ . '/../view/yourTemplate3/index.phtml',
       ]
 ];

If you want to modify the selection of the templates (iframe_) add the following mapping

.. code-block:: php

    'iframe/iFrame.phtml' => __DIR__ . '/../view/YourTemplateSelection.phtml',



.. _iframe:  https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/view/iframe/iFrame.phtml
.. _templates: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/public/templates/default/index.phtml

Mails
^^^^^

+----------------------------+-------------------------------------------------------------------------------------+
| Name                       | Description                                                                         |
+============================+=====================================================================================+
| job-created_               | mail is sent to th approval team                                                    |
+----------------------------+-------------------------------------------------------------------------------------+
| job-pending_               | mail is sent to the person, who created the job.                                    |
+----------------------------+-------------------------------------------------------------------------------------+
| job-accepted_              | mail informs the person, who created the job, that the job is going to be published |
+----------------------------+-------------------------------------------------------------------------------------+
| job-rejected_              | mail informs the person, who created the job, that the job was rejected             |
+----------------------------+-------------------------------------------------------------------------------------+

.. _job-created: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/view/mails/job-created.phtml
.. _job-pending: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/view/mails/job-pending.phtml
.. _job-rejected: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/view/mails/job-rejected.phtml
.. _job-accepted: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/view/mails/job-accepted.phtml


Options
^^^^^^^

To modify the options, copy the module.jobs.options.local.php.dist_ to you ``config/autoload`` directory, remove the
``.dist`` prefix and adjust the values

+----------------------------+--------+----------------------------------------------------------------------------------------+
|Name                        | type   | description                                                                            |
+============================+========+========================================================================================+
|multipostingApprovalMail    | string | recipient email of the approval team                                                   |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|multipostingTargetUri       | string | Send a Rest Request to this target on status changes of a job opening. The URI can     |
|                            |        | contain username/password. eg:  ``http://user:pass@host/location?query``               |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|defaultLogo                 | string | The default Logo is shown in a job opening and in the application form                 |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|companyLogoMaxSize          | int    | Maximum size in bytes of a company Logo. Default 200kB                                 |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|companyLogoMimeType         | array  | Allowed Mime-Types for company Logos                                                   |
+----------------------------+--------+----------------------------------------------------------------------------------------+

.. _module.jobs.options.local.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/config/module.jobs.options.local.php.dist


Channel Options
^^^^^^^^^^^^^^^

The Channel Options contain information about publishing channels, a user can select to publish a job posting. To modify the
options, copy the channel.options.local.php.dist_ to you ``config/autoload`` directory, remove the ``.dist`` prefix and
adjust the values

+----------------------------+--------+----------------------------------------------------------------------------------------+
|Name                        | type   | description                                                                            |
+============================+========+========================================================================================+
|externalKey                 | string | external key of a channel. Eg. a provider offers the channel "MyJobboard" with the key |
|                            |        | "123". YAWIK provides a channel "MyJobboard" using the key "myJobborad".               |
|                            |        | Set externalKey to "123", if the job is published to the provider.                     |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|prices                      | array  | [base,list,min] You can define 3 prices which you can use in your price-calculation_   |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|currency                    | string | currency of the price. Default: CoreOptions::defaultCurrency                           |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|tax                         | int    | tax rate of the channel. Default: CoreOptions::defaultTaxRate                          |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|label                       | string | label of the channel                                                                   |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|publishDuration             | int    | number of days a job opening can be published                                          |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|category                    | string | Category of the channel. Default: "General"                                            |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|headline                    | string | Headline of the channel                                                                |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|description                 | string | Description of the channel                                                             |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|linktext                    | string | Linktext of a link to further information of the channel                               |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|linkTarget                  | string | Link target  of a link to further information of the channel                           |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|route                       | string | Route to a content page with details about the channel                                 |
+----------------------------+--------+----------------------------------------------------------------------------------------+
|params                      | array  |Parameter, which can be used for linking the detail page about the channel              |
+----------------------------+--------+----------------------------------------------------------------------------------------+


.. _channel.options.local.php.dist: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/config/module.jobs.options.local.php.dist


ATS Mode
^^^^^^^^

The ATS (Applicant Tracking System) Mode defines, how applications should be processed. The following modes exist:

+----------------------------+----------------------------------------------------------------------------------------+
|Name                        | description                                                                            |
+============================+========================================================================================+
|intern                      | Applications are stored within the local YAWIK instance                                |
+----------------------------+----------------------------------------------------------------------------------------+
|uri                         | Application Form is pointed to en external ATS System                                  |
+----------------------------+----------------------------------------------------------------------------------------+
|email                       | Application Form is forwarded via Email                                                |
+----------------------------+----------------------------------------------------------------------------------------+
|none                        | The Application Formular is deactivated                                                |
+----------------------------+----------------------------------------------------------------------------------------+



Widget
^^^^^^

by using the folloging Javascript Widget you can add your jobs into your personal homepage. 


.. code-block:: javascript

 <script>
    (function (window, document) {
        var loader = function () {
            var script = document.createElement("script"), tag = document.getElementsByTagName("script")[0];
            script.src = "view-source:https://yawik.org/YawikWidget/yawik.min.js";
            tag.parentNode.insertBefore(script, tag);
        };
        window.addEventListener ? window.addEventListener("load", loader, false) : window.attachEvent("onload", loader);
    })(window, document);
 </script>


The javascript renders a joblist inside a container with the id ``YawikWidget``

.. code-block:: html

 <div id="YawikWidget"
     data-organization="55ae775c6b10f8f05b8b457f"
     data-yawik="https://yawik.org/">
 </div>


The attribute data-organizations takes an organization id, provided by your used yawik. The attribute data-yawik 
takes the location of the used yawik.

Source Code of the Widget: https://github.com/cbleek/YawikWidget


Price Calculation
^^^^^^^^^^^^^^^^^

.. _price-calculation:


The price calculations can be overridden by creating a MyCalculation.php. You can start by coping the 
ChannelPrices.php_ to MyCalculation.php. Adjust the namespace and implement your logic within the 
filter function.

To use your MyCalculation.php, you have to copy the ChannelPricesFactory.php_ into YourModule. Adjust 
the namespace and the $filterClass value.

To use your filter, you have to put the following config into your modules.config.php 

.. code-block:: php

 'filters' => [
   'factories'=> [
      'Jobs/ChannelPrices'  => 'YourModule\Factory\Filter\MyCalculation',
      ...
     ]
  ]


.. _ChannelPrices.php: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/src/Jobs/Filter/ChannelPrices.php
.. _ChannelPricesFactory.php: https://github.com/cross-solution/YAWIK/blob/develop/module/Jobs/src/Jobs/Factory/Filter/ChannelPricesFactory.php

