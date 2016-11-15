================
FAQ: Mails
================

Is it possible to configure an SMTP Server
------------------------------------------

Yes. Copy the ``Core/config/MailServiceOptions.config.local.php.dist`` into you autoload directory and adjects the values.

How can I translate Mails?
--------------------------

translating mails with gettext_ is possible, but you will propably like to translate mails a little different. You can
code the language into the name of the view script.

example:

your're creating a mail using the viewscript ``MyModule/view/myMail/mailtext.phtml``. If you wannt to translate this mail
into the french lanuage, you simple copy it to ``MyModule/view/myMail/mailtext.fr.phtml``.




.. _gettext: https://www.gnu.org/software/gettext/