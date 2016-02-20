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

* Register with Facebook, Xing, LinkedIn, Google or GitHub
* Register via registration form
* I forgot my Password
* Roles for applicants and recruiters

By using the optional Module YawikCompanyRegistration_, users can register as a company. The module provides a
formular and creates a user and a company in one step.

.. _hybridauth: http://hybridauth.sourceforge.net/
.. _YawikCompanyRegistration: https://github.com/cross-solution/YawikCompanyRegistration


Mails
^^^^^

.. index:: Mail

+------------------------------+---------------------------------------------+---------------------------------+
|template                      |purpose                                      |triggered from                   |
+==============================+=============================================+=================================+
|mail/register_                | contains a confirmation-link to ensure      |                                 |
|                              | the email-address. Without this assurance   |                                 |
|                              | the account will not be fully activated     |                                 |
+------------------------------+---------------------------------------------+---------------------------------+
|mail/forgot-password_         | Mail containing a link which enables        |                                 |
|                              | the user to reset the password              |                                 |
+------------------------------+---------------------------------------------+---------------------------------+
|mail/first-socialmedia-login_ | contains username and password. Mail is     |                                 |
|                              | sent to the user after the first social     |                                 |
|                              | media login                                 |                                 |
+------------------------------+---------------------------------------------+---------------------------------+
|mauk/first-external-login_    | contains username and password. Mail is     |                                 |
|                              | sent, after a user was created by an        |                                 |
|                              | external application                        |                                 |
+------------------------------+---------------------------------------------+---------------------------------+

.. _register: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/register.phtml
.. _forgot-password: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/forgot-password.phtml
.. _first-socialmedia-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-socialmedia-login.phtml
.. _first-external-login: https://github.com/cross-solution/YAWIK/blob/develop/module/Auth/view/mail/first-external-login.phtml

