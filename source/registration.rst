.. _registration:

*****************
User Registration
*****************

Account Registration
--------------------

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/register``

**Request**

.. code-block:: http

  POST /register HTTP/1.1
  Content-Type: application/json; charset=utf-8
  Host: violet-peace.apps.dev.stormpath.io

  {
    "email": "jakub@stormpath.com",
    "password": "Password",
    "givenName": "Jakub",
    "surname": "S"
  }

**Response**

.. code-block:: json

  {
    "account": {
      "href": "https://dev.i.stormpath.com/v1/accounts/5kYvdJyROImkrMHVD2fhSG",
      "createdAt": "2016-10-28T20:40:18.463Z",
      "modifiedAt": "2016-10-28T20:40:18.463Z",
      "username": "jakub+test9@stormpath.com",
      "email": "jakub+test9@stormpath.com",
      "givenName": "Jakub",
      "middleName": null,
      "surname": "S",
      "status": "ENABLED",
      "fullName": "Jakub S"
    }
  }