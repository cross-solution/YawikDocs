.. index:: Auth

Auth
----

.. raw:: html

    <div style="float:right; width: 50%">
    <img src="https://www.transifex.com/projects/p/yawik/resource/auth/chart/image_png"/>
    <br/>translation state of Auth module.
    </div>

the auth module is based on hybridauth_. The social networks Facebook, Xing 
and LinkedIn are ready to connect, just by configuring their API key and secret.
Other Networks can be easily added.

User Data are stored in the ``users`` collection.

The Auth module offers the following features

* Register with Facebook, Xing or LinkedIn
* Register via registration form
* I forgot my Password
* Roles for applicants and recruiters

.. _hybridauth: http://hybridauth.sourceforge.net/

Mails
~~~~~

+------------------------+---------------------------------------------+---------------------------------+
|template                |purpose                                      |triggered from                   |
+========================+=============================================+=================================+
|register                | contains a confirmation-link to ensure      |                                 |
|                        | the email-adress. Without this assurance    |                                 |
|                        | the account will not be fully activated     |                                 |
+------------------------+---------------------------------------------+---------------------------------+
|forgot-password         | send a link for a requery of the password   |                                 |
|                        | this mail is submitted to the stored email  |                                 |
|                        | address of the register process             |                                 |
+------------------------+---------------------------------------------+---------------------------------+
|first-socialmedia-login |                                             |                                 |
+------------------------+---------------------------------------------+---------------------------------+
|first-external-login    |                                             |                                 |
+------------------------+---------------------------------------------+---------------------------------+