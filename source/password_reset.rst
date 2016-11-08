.. _password-reset:

**************
Password Reset
**************

FORGOT

Used to trigger the password reset email

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/forgot``

**Request**

.. code-block:: http

  POST /forgot HTTP/1.1
  Accept: application/json
  Content-Type: application/json; charset=utf-8
  Host: violet-peace.apps.dev.stormpath.io

  {
    "email": "jakub@stormpath.com"
  }

**Response**

HTTP/1.1 200

CHANGE

To actually change the password. This is the endpoint that a user will use if they have received a password reset email and have clicked on the link in the email. The link will point to this endpoint, and contain the sptoken query parameter.

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/change``

**Request**

.. code-block:: http

  POST /change HTTP/1.1
  Accept: application/json
  Content-Type: application/json; charset=utf-8
  Host: violet-peace.apps.dev.stormpath.io

  {
    "sptoken": "eyJ0aWQiOiIyWnU4ekw2ZndvMjdUVEtBeGp0dmVtIiwic3R0IjoiYXNzZXJ0aW9uIiwiYWxnIjoiSFMyNTYifQ%2EeyJleHAiOjE0Nzc3NzUzNjIsImp0aSI6IjZFMWo0aTN4QkdPV1g2OXhrVDNSRG8ifQ%2ECOmIVRr3pQ4jsIhKl7wWjHkYTfX1Reg3BV0kAlMSQpc",
    "password": "Password1!"
  }

**Response**

HTTP/1.1 200