.. _email-verification:

******************
Email Verification
******************

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/verify``

TRIGGER VERIFICATION EMAIL

**Request**

.. code-block:: http

  POST /verify HTTP/1.1
  Accept: application/json
  Content-Type: text/plain; charset=utf-8
  Host: violet-peace.apps.dev.stormpath.io

  {
    "email": "jakub@stormpath.com"
  }

**Response**

200 OK

SEND VERIFICATION TOKEN

**Request**

GET /verify?sptoken=10vphI5BzhVLczsxJKuImq HTTP/1.1
Accept: application/json
Host: violet-peace.apps.dev.stormpath.io

**Response**

200 OK