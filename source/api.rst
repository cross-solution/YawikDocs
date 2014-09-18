API
===

YAWIK currently offers a simple API to create Jobs. If you are able to create HTML formatted job ads and if you can
put application links to the HTML source of your jobs, you might find the API usefull to put your jobs into YAWIK,
which enables you the use the application forms.

We'll later replace this simple API with a full featured. Maybe build with https://apigility.org/.

YAWIK allows an external application to post jobs via http POST requests. At first you have to authenticate. This can be
done by:

Example:

.. code-block:: sh

    curl -c "/tmp/cookie" -d "appKey=SecretYawikDemoKey&user=demo&pass=demo" http://yawik.org/demo/login/extern?format=json

The following parameters can be passed:

+---------+-------------------------+---------------------------------------------------------------------------+
|Param    |Value                    |Description                                                                |
+=========+=========================+===========================================================================+
|appKey   |string                   |pre-shared key between your app and your YAWIK                             |
+---------+-------------------------+---------------------------------------------------------------------------+
|user     |string                   |user name of an YAWIK Account                                              |
+---------+-------------------------+---------------------------------------------------------------------------+
|pass     |string                   |password of an YAWIK Account                                               |
+---------+-------------------------+---------------------------------------------------------------------------+
|email    |email adress             |If an YAWIK Account is created, the password is sent to this email address |
+---------+-------------------------+---------------------------------------------------------------------------+
|role     |recruiter or user        |If an YAWIK Account is created, this role is used                          |
+---------+-------------------------+---------------------------------------------------------------------------+

The appKey authenticates your external application. The to "top secret" pre-shared key of the YAWIK demo is
``SecretYawikDemoKey``. Normally this key is only known by YAWIK and the external App.

Success:

.. code-block:: sh

    {"status":"success","token":"em7ke40ec5sskqce5jgtt912m5"}

Failure:

.. code-block:: sh

    {"status":"failure","code":0,"messages":["Invalid application key"]}

Once you've logged in, the cookie returned by YAWIK has to be stored on the external application site. In case you're
testing it with the above curl statement, the cookie is stored in /tmp/cookie.

If the application Key is valid and the user is unknown, a user is simply created. The password of the user is sent via
email (if an email-value is provided in the curl-call).
Authentification via CURL and the normal login are traded different. Every authentification with an external application
uses a separate key, therefore the external application is liable to provide privacy.
An user can root out any external application by simply revoking it's key without affecting any other authentification.



These parameters are available or must be set to transmit a job:

+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|Param            |Value                    |example  |mandatory |Description                                                                |
+=================+=========================+=========+==========+===========================================================================+
|applyId          |string                   |AMS79j   |yes       |the id is an unique key to adress your job                                 |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|company          |string                   |         |yes       |name of the company                                                        |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|companyId        |string                   |         |no        |if an id is provided, the company is stored in the YAWIK-DB                |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|contactEmail     |email adress             |         |no        |for automatic informations like new applicants                             |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|title            |string                   |         |yes       |for tabular overview                                                       |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|location         |string                   |         |no        |for overview, will be later prone for indexing                             |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|link             |http adress              |         |yes       |the job offer weblink                                                      |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|datePublishStart |YYYY-MM-DD               |         |yes       |                                                                           |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|status           |string                   |         |no        |                                                                           |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|reference        |string                   |         |no        |an internal reference from the publisher                                   |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|logoRef          |http adress              |         |no        |Logo for the Company                                                       |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+
|publisher        |http adress              |         |no        |who get the credit for any application                                     |
+-----------------+-------------------------+---------+----------+---------------------------------------------------------------------------+

some remarks:

applyId
    The applyId must be unique just to the provider, this key along with your authentification is the only access to your data.
    Consistently there is no key provided by YAWIK.

company, companyId
    companies can managed alongside the job if a companyId is passed, the companyId is an assurance for yawik, that different jobs with the same companyId belong to the same company.
    The name is for that a to weak criteria.

contactEmail
    Although a contact-email is not obligatory, it is a crucial enhancement of service. Whenever something happens to your job, you get an update.
    This includes new applicants for a job.

link
    This link should be an appealing presentation of the job. YAWIK can not (up to now) display Jobs on it own, so this link is mandatory.

publisher
    One of the basic ideas of YAWIK is to distribute jobs automatically. Even though, every job may have an owner who wants to administer the job.


.. code-block:: sh

    curl -b /tmp/cookie -d "applyId=1234" 'http://yawik.org/demo/de/saveJob?format=json'
    {
        "token":"903rgbrs1j6p5gb2586tdci833",
        "isSaved":false,
        "post":{"applyId":"1234"},
        "valid Error":
            {
            "job":
                {
                    "company":{"isEmpty":"Es wird ein Eingabewert ben\u00f6tigt. Dieser darf nicht leer sein"},
                    "title":{"isEmpty":"Es wird ein Eingabewert ben\u00f6tigt. Dieser darf nicht leer sein"},
                    "link":{"isEmpty":"Es wird ein Eingabewert ben\u00f6tigt. Dieser darf nicht leer sein"},
                    "datePublishStart":{"isEmpty":"Es wird ein Eingabewert ben\u00f6tigt. Dieser darf nicht leer sein"
                }
            }
        }
    }


A successfull request returns:

.. code-block:: sh

    curl -b /tmp/cookie -d "applyId=1234&title=this%20is%20a%20test%20job&company=MyCompany&datePublishStart=2014-09-15&link=http://example.com/myjob.html" \
           'http://yawik.org/demo/de/saveJob?format=json'
    {
        "token":"903rgbrs1j6p5gb2586tdci833",
        "isSaved":true,
        "post":{
            "applyId":"1234",
            "title":"this is a test job",
            "company":"MyCompany",
            "datePublishStart":"2014-09-15",
            "link":"http:\/\/example.com\/myjob.html"
        }
    }
