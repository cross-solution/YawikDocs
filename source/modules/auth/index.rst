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
^^^^^

.. index:: Mail

+-------------------------+---------------------------------------------+---------------------------------+
|template                 |purpose                                      |triggered from                   |
+=========================+=============================================+=================================+
|register_                | contains a confirmation-link to ensure      |                                 |
|                         | the email-address. Without this assurance   |                                 |
|                         | the account will not be fully activated     |                                 |
+-------------------------+---------------------------------------------+---------------------------------+
|forgot-password_         | Mail containing a link which enables        |                                 |
|                         | the user to reset the password              |                                 |
+-------------------------+---------------------------------------------+---------------------------------+
|first-socialmedia-login_ |                                             |                                 |
+-------------------------+---------------------------------------------+---------------------------------+
|first-external-login_    |                                             |                                 |
+-------------------------+---------------------------------------------+---------------------------------+

.. _register: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/register.phtml
.. _forgot-password: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/forgot-password.phtml
.. _first-socialmedia-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-socialmedia-login.phtml
.. _first-external-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-external-login.phtml

