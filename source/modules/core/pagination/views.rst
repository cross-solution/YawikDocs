.. index:: Core; Pagination; Views

Pagination in the view layer
****************************

:Author: Mathias Gelhausen <gelhausen@cross-solution.de>


Syntax
======

The process described here assumes you render the actual content (the item list) of the pagination container
in a separate view script which allows you to load subsequent pages with an ajax request.

Add a pagination container in the main view script:

.. code-block:: html

   <div class="pagination-container">
        <div class="pagination-content">
        <!-- The item list should be rendered in here -->
        </div>
   </div>


This is the most basic container. The corresponding javascript will add a <div> for the "empty" message and
a <div> for the loading indicator.

The actual HTML will then look like

.. code-block:: html

   <div class="pagination-container">
        <div style="position:absolute;
                    z-index:1000;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background-color: rgba(250,250,250,0.5);"
             id="jobs-list-container-loading-indicator"
             class="pagination-loading"
        >
            <i class="fa-spin yk-icon-spinner yk-icon fa-2x"
               style="position:absolute; top: 25%; left: 50%;">
            </i>
        </div>

        <div class="pagination-message alert alert-warning">
            <strong>Sorry</strong>, your search yields no results.
        </div>

        <div class="pagination-error alert alert-danger">
            <strong>Sorry</strong>, loading results failed.'
        </div>

        <div class="pagination-content">
        <!-- The item list should be rendered in here -->
        </div>
   </div>


It is possible to alter any of the divs by simple render an element with the corresponding class name in the
pagination container.
If you want to simply alter the messages to be displayed you can also do this with data-* attributes on the
container div

.. code-block:: html

    <div class="pagination-container"
         data-message="Any valid escaped html content"
         data-error="This message will be injected to the div.pagination-error"
    >

The javascript will bind to the click events of any link inside an element with the class "pagination", as the
PaginationControl view helper of the Zend Framework will do.

Once such a link is clicked, the loading div is displayed, an AJAX request is issued to the url of that
links href attribute and the content of the div.pagination-content is replaced by the response.
The javascript will bind to the click events of any link inside an element with the class "pagination".

If an empty string is returned from the AJAX request, the div.content will get hidden and the div.message
will be displayed. On an error the div.error is displayed.

You can trigger a load programmatically with javascript

.. code-block:: javascript

   $('.pagination-container').paginationContainer('load', '/the/url/to/load/from?with=parameter');


Example
=======

This is taken from the Jobs Module and is the pagination container of the Jobboard.
$jobs in this case is the paginator service passed along from the controller.


.. code-block:: html

    <?php //description: Renders the list of public jobs. ?>
    <?php $this->headTitle($this->translate('Jobs'));
          $this->headScript()->appendFile($this->basepath('/Core/js/core.pagination-container.js'))?>

    <h1><?php echo $this->translate('Public Job Opportunities')?></h1>

    <?php echo $this->flashMessenger()->render('default', array('alert', 'alert-success')) ?>

    <nav class="navbar yk-toolbar" id="jobs-list-filter-wrapper">
    <?php echo $this->form($this->filterForm)  ?>
    </nav>

    <div id="jobs-list-container" class="pagination-container"
        data-message="<?php echo $this->escapeHtmlAttr(sprintf(
                          $this->translate('%sSorry%s, there are not any jobs matching your search criteria.'),
                          '<strong>', '</strong>'
                   ))?>">

        <div class="pagination-content">
        <?php echo $this->render('jobs/jobboard/index.ajax.phtml')?>
        </div>
    </div>

and the script which renders the items:

.. code-block:: html

    <?php if (count($jobs)): // We only want to render something, if there are items.?>
    <table class="pagination-content table table-striped table-bordered table-hover" id="jobs-list">
        <thead>
        <tr>
            <th><?php echo $this->translate('Title of the job')?> / <?php echo $this->translate('Companyname')?></th>
            <th><?php echo $this->translate('Location')?> / <?php echo $this->translate('Date of receipt')?></th>
            <th><?php echo $this->translate('Apply')?></th>
        </tr>
        </thead>

    <?php foreach ($jobs as $job):?>
    <tr>
        <td>
            <?php if ($job->organization && $job->organization->image &&  $job->organization->organizationName): ?>
                <div class="yk-logo-list">
                    <img class="yk-logo-sm" src="<?php echo $this->basePath().$job->organization->image->uri ?>">
                </div>
            <?php endif ?>
            <?php $href = $job->link ? $job->link : $this->url('lang/jobs/view', array(), array('query' => array('id' => $job->id)), true); ?>
            <a href="<?php echo $href ?>" target="_blank"><?php echo strip_tags($job->title)?></a>
            <br/><?php
                if (isset($job->organization) && isset($job->organization->organizationName) && isset($job->organization->organizationName->name)) {
                    echo $job->organization->organizationName->name;
                }
            ?>
        </td>
        <td>
            <div><?php echo $job->location?></div>
            <small>
                <?php
                if ($job->datePublishStart): echo $this->dateFormat($job->datePublishStart, 'short', 'none');
                elseif ($job->dateCreated): echo $this->dateFormat($job->dateCreated, 'short', 'none');
                endif?>
            </small>
        </td>
        <td>
            <?php
                echo $this->applyUrl($job);
            ?>
         </td>
    </tr>
    <?php endforeach?>
        </table>

    <?php echo $this->paginationControl($jobs, 'Sliding', 'pagination-control', array('lang' => $this->params('lang'), 'route' => 'lang/jobboard'));?>

    <?php endif ?>




