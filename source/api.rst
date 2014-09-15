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

    curl -c "/tmp/cookie" -d "appkey=SecretYawikDemoKey&user=demo&pass=demo" http://yawik.org/demo/login/extern?format=json

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
email.

.. code-block:: sh

    curl -b /tmp/cookie -d "applyId=1234" 'http://yawik.org/DEMO/de/saveJob?format=json'
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

    curl -b /tmp/cookie -d "applyId=1234&title=this%20is%20a%20test%20job&company=MyComishStart=2014-09-15&link=http://example.com/myjob.html" \
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
