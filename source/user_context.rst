.. _user-context:

************
User Context
************

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/me``

.. note::

  This call requires authentication.

**Request**

.. code-block:: http

  GET /me HTTP/1.1
  Content-Type: application/json; charset=utf-8
  Cookie: access_token=eyJraW[...]tIUxpdhBJz74LR0dd90RQTnl-u-_hgOOkpA
  Host: smooth-ensign.apps.dev.stormpath.io

**Response**

``200 OK`` along with current session's Account information:

.. code-block:: json

  {
    "account": {
      "href": "https://dev.i.stormpath.com/v1/accounts/7gzK1RBUk2tF3VNhZ3AYFI",
      "createdAt": "2016-10-26T16:48:14.457Z",
      "modifiedAt": "2016-10-26T16:48:14.457Z",
      "username": "jakub",
      "email": "jakub@stormpath.com",
      "givenName": "Jakub",
      "middleName": "",
      "surname": "Sw",
      "status": "ENABLED",
      "fullName": "Jakub Sw"
      "emailVerificationStatus":"VERIFIED"
    }
  }

By default this call will return:

- ``href``
- ``createdAt``
- ``modifiedAt``
- ``username``
- ``email``
- ``givenName``
- ``middleName``
- ``surname``
- ``status``
- ``fullName``
- ``emailVerificationStatus``

You can also get back the Account's expanded:

- API Keys
- Applications
- Custom Data
- Group Memberships
- Groups
- Provider Data
- Directory
- Tenant

For more information see the :ref:`configuration` chapter.