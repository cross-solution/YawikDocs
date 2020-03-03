.. index:: Core; Mails

Mails
^^^^^

Mails have two essential agents

* a message-service, which is liable for gathering and providing data and rendering the mail
* a mail-service, which is liable for sending the mail

when creating own mails, you usually extends the message

All related classes are in the Core-Modul, the interaction in in this diagram:
http://www.gliffy.com/go/publish/7191865

Using the MailService
---------------------

Mails can be used everywhere, where have access to the application-serviceLocator.


When you need to send a mail, there are four steps to do

1. call the mail-service
2. get a message-service from the mail-service (there are two distinguished types)
3. feed the message-service with informations
4. use the mail-service to send the message-service

The two types of message-service:

* **Templates**, which uses scripts for the body and render them like usual views.
    This is more preferred approach for mails with lots of text, and also with mails for different languages
* **Derived classes**, which is preferred when there is a lot of processing is involved.


Using a script as body
======================

When using a script the message-service in some way behaves like a viewmodel,
it takes in arbitrary variables, which can be accessed in the script.
Also you can set a template, which is resolved by view-maps or view-pathes.
In the scripts you can use PHP, and since the script is included into the message-service,
you can set or change in the script mail-specific attributes like header oder subject.
Scripts are an alike to views.

To use a script you have to instanciate a mail service and a htmltemplate service

.. code-block:: php

    $mailService             = $serviceManager->get('Core/MailService');
    $mail                    = $mailService->get('htmltemplate');
    $mail->entity            = $entity;
    $mail->link              = $previewLink;
    $mail->setTemplate('mail/myScript');
    $mail->setSubject( /*translate*/ 'A Title');
    $mail->setTo($email);
    $mail->setFrom($userEmail, $userName);
    $mailService->send($mail);

The script is set in the code, so there you can make the choice of the content, by simply choosing a script.
But always remember to consign the location of the script in the template-map.

.. note::
    The mail service injects itself in the view script in the variable "mail", so you can access the mail service with
    ``$this->mail``. But if you alter the headers (e.g. by setting a subject) you need to call the mail services ``renderBodyText()``
    method prior to sending. Otherwise when using some transports (e.g. Smtp), the modifications made to the headers are
    NOT affecting the actual mail to be send.

    This is caused by an internal implementation detail of the Zend Framework classes.


Using an own class
==================

Own classes provide all information by methods. Own classes are the preferred choice when informations are volatile or special (like including pictures or other mimetypes).
Look the classes in ``Applications\Mail`` for example. The own classes must be announced in the config like

.. code-block:: php

    'mails' => array(
        'invokables' => array(
            'myOwnClass' => 'xxx\Mail\myOwnClass',


With being announced, the mail-service can instantiate and initialize this class properly.

.. code-block:: php

    $mailService = $this->getServiceLocator()->get('Core/MailService');
    $mail = $mailService->get('myOwnClass');
    $mailService->send($mail);

Since most of the own classes are derived from laminas-mail_ (at least they should be derived from it),
they will have a full pledge of all the methods, which are provided especially for mails, like ``setEncoding``, ``setFrom`` etc...


_laminas-mail: https://docs.laminas.dev/laminas-mail/message/intro/