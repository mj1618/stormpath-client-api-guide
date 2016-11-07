**************
Authentication
**************

Get Login View
^^^^^^^^^^^^^^

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/login``

.. code-block:: http

  GET /login HTTP/1.1
  Accept: application/json
  Host: smooth-ensign.apps.dev.stormpath.io

**On Success**

200 OK along with the JSON view model. The collection of Account Stores that returns will only include non-Cloud Directories (e.g. Facebook).

.. code-block:: json

  {
    "form": {
      "fields": [
        {
          "name": "login",
          "label": "Username or Email",
          "placeholder": "Username or Email",
          "required": true,
          "type": "text"
        },
        {
          "name": "password",
          "label": "Password",
          "placeholder": "Password",
          "required": true,
          "type": "password"
        }
      ]
    },
    "accountStores": [
      {
        "provider": {
          "href": "https://dev.i.stormpath.com/v1/directories/2TRsNjHx8DB6Ca3rBal536/provider",
          "providerId": "facebook",
          "clientId": "1401818363453044"
        },
        "href": "https://dev.i.stormpath.com/v1/directories/2TRsNjHx8DB6Ca3rBal536",
        "name": "Fake Facebook Dir"
      }
    ]
  }

OAuth 2.0 Login
^^^^^^^^^^^^^^^

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/oauth/token``

The OAuth endpoint takes one of the following:

- Username & Password (URL-encoded)
- Client Credentials (Basic Auth Base64 encoded API Key ID & Secret)
- Refresh Token (URL-encoded)

And returns OAuth 2.0 Access and Refresh tokens.

Password
""""""""

**Request**

.. code-block:: http

  POST /oauth/token HTTP/1.1
  Accept: application/json
  Content-Type: application/x-www-form-urlencoded
  Host: smooth-ensign.apps.dev.stormpath.io

  grant_type=password&username=jakub%40stormpath.com&password=Password1%21

**Response**

.. code-block:: json

  {
    "access_token": "eyJraWQi[...]0dTpiM",
    "refresh_token": "eyJraWQi[...]okvVI",
    "token_type": "Bearer",
    "expires_in": 3600
  }

.. note::

  The ``username`` can also be the ``email``

Client Credentials
""""""""""""""""""

**Request**

.. code-block:: http

  POST /oauth/token HTTP/1.1
  Accept: application/json
  Content-Type: application/x-www-form-urlencoded
  Authorization: Basic MzZGT1dDWUJBMk1KMVBQWlVZ[...]4SWFhQkpSUTZhZ3ZHajZnSWMyeEVV
  Host: smooth-ensign.apps.dev.stormpath.io

  grant_type=client_credentials

**Response**

.. code-block:: json

  {
    "access_token": "eyJraWQ[...]NRaztg0",
    "token_type": "Bearer",
    "expires_in": 3600
  }

Refresh Token
"""""""""""""

**Request**

.. code-block:: http

  POST /oauth/token HTTP/1.1
  Accept: application/json
  Content-Type: application/x-www-form-urlencoded
  Host: smooth-ensign.apps.dev.stormpath.io

  grant_type=refresh_token&refresh_token=eyJraWQ[...]FMQIh-fwns


**Response**

.. code-block:: json

  {
    "access_token": "eyJraWQ[...]urs4iqPY",
    "refresh_token": "eyJraWQ[...]fwns",
    "token_type": "Bearer",
    "expires_in": 3600
  }

OAuth 2.0 Logout
^^^^^^^^^^^^^^^^

This endpoint takes a POST with your current OAuth token and revokes the Access and Refresh tokens.

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/oauth/revoke``

**Request**

.. code-block:: http

  POST /oauth/revoke HTTP/1.1
  Accept: application/json
  Content-Type: application/x-www-form-urlencoded; charset=utf-8
  Cookie: access_token=eyJraWQ[...]9OMqlSgbuMeoFSYA3r2bSQJxIsDQg
  Host: perfect-rank.apps.dev.stormpath.io

**Response**

200 OK
