.. index:: Core; Notifications

Notifications
-------------

YAWIK comes with a notification system which allows to easy set notifcation messages
to be displayed to the user regardless, if the request will make a redirect or not.

Notification messages are displayed via a child model which is injected in the
layout. Therefor they are rendered centralized and are easily changeable.


Controller Plugin
^^^^^^^^^^^^^^^^^

The controller plugin is merely a wrapper for Zend Framework's FlashMessenger.
It provides own namespaces and shortcut methods to add notifications according to
Twitter Bootstrap alert class names. 

The plugin is registered in the ControllerPluginManager under the key
"Notification"

 =========  ===============================  ===============================
 Namespace  Class Constant                   Meaning
 =========  ===============================  ===============================
 success    Notification::NAMESPACE_SUCCESS  An action was successfull
 warning    Notification::NAMESPACE_WARNING  Action was (partly) successfull
 danger     Notification::NAMESPACE_DANGER   Action was not successfull (error)
 info       Notification::NAMESPACE_INFO     General info notification w/o special meaning
 =========  ===============================  ===============================


In a controller action, simply call the plugin via the magic __call mechanism

.. code-block:: php

  $this->notification()->success('Updates successfully changed.');
  return $this->redirect(...);

The plugin provides following methods:

 * success($message)
 * warning($message)
 * danger($message)
 * error($message)   [alias for danger(), for convinience]
 * info($message)
 * addMessage($message, $namespace = 'info')
 * __invoke($message = null, $namespace = 'info')
 
 
Rendering
^^^^^^^^^

To render notifications it is necessary to render the
template which is registered under the
key `core/notifications`_ in the view manager's template map.

The default view script provided renders all notifications in a div container
with the class "yk-notifications" using the "Alert" view helper.

Notifications are rendered in the following order:
 - Danger
 - Warning
 - Success
 - Info

You can place notifications into your general layout by following these steps:

 1. In the layout script, above the output of the headScript-Helper, render the
    notifications partial and capture to a variable. (Because the template injects
    a javascript to the headscript container)

 2. Echo the capture variable at the position where the notifications should be.


.. code-block:: php

    <?php $notifications = $this->partial('core/notifications'); ?>

    //...

    <?php echo $this->headScript(); ?>

    // ...

    <?php echo $notifications; ?>


.. note::   In earlier versions there was a child model injected to the layout view.
            This leads to problems, where no notifications are needed in a layout.
            Due to internal Zend Framework procedures, child models will be rendered
            BEFORE the containing model.

            So, injecting a child model in the layout view model always renders the notifications
            even if not needed, resulting in unneeded javascript beeing loaded as well as the general
            rendering overhead.

.. _core/notifications: https://github.com/cross-solution/YAWIK/blob/master/module/Core/view/partial/notifications.phtml
.. _layout.phtml: https://github.com/cbleek/YawikDemoSkin/blob/master/view/layout.phtml#L98

Alert View Helper
^^^^^^^^^^^^^^^^^

The alert view helper is registered in the view helper manager under the key
"Alert". It takes a message and renders it in the bootstrap markup for an 
dismissable alert box.

It is also possible to capture content or using shortcut methods. 

.. code-block:: php
	
    <?php // capture content
    $this->alert()->start('info'); ?>
    <p>This is an info message</p>
    <?php echo $this->alert()->end(); ?>

    <?php // via __invoke
    echo $this->alert('warning', 'This is a warning');
    
    // via shortcut methods
    echo $this->alert()->danger('This is an error message.');
    
The helper provides following methods

 * __invoke($type = null, $content = null)
 * start($type)
 * end()
 * info($content = true)
 * warning($content = true)
 * danger($content = true)
 * success($content = true)

Passing "true" (or nothing) to a shortcut method is the same as starting capture
with the according type.
 
.. code-block:: php

    <?php $this->alert()->info() ?>
    <p> This is an info message </p>
    <?php echo $this->alert()->end() ?>
    
