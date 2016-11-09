.. _authentication:

**************
Authentication
**************

Authentication in the Client API involves two endpoints:

- ``/login``
- ``/oauth/token``

The ``/login`` endpoint is used to retrieve the dynamic login JSON view model, while the ``/oauth/token`` endpoint receives credentials from your application and returns back OAuth Access and Refresh tokens. For more information about both of these endpoint, see below.

.. _get-login:

Get Login View
^^^^^^^^^^^^^^

**URL**

``https://{DNS-LABEL}.apps.stormpath.io/login``

The login view is returned in the form of JSON. It includes a ``form`` object that contains a ``fields`` collection to be rendered in the login form, as well another collection of ``accountStores``.

**Form Fields**

Each returned ``field`` has the following information:

.. list-table::
  :widths: 30 70
  :header-rows: 1

  * - Attribute
    - Description

  * - ``name``
    - The name of this field.

  * - ``label``
    - The label element for this field.

  * - ``placeholder``
    - Placeholder text, if any, to put in this field when it is empty.

  * - ``required``
    - Indicates whether this field is required or not.

  * - ``type``
    - The input type for this field (e.g. ``text`` or ``password``).

Any non-Cloud Account Stores mapped to this Application will also return as part of the response here, in order to allow for the rendering of Social Login buttons. They will return in an order determined by their order in the Account Store Mapping priority index. For more about this topic, please see `How Login Attempts Work <https://docs.stormpath.com/rest/product-guide/latest/auth_n.html#how-login-attempts-work-in-stormpath>`__ in the REST Product Guide.

**Account Stores**

Each returned ``accountStore`` has an ``href`` and a ``name``. It also contains an embedded ``provider`` object which contains the following information:

.. list-table::
  :widths: 30 70
  :header-rows: 1

  * - Attribute
    - Description

  * - ``href``
    - The location of the Provider resource for this Directory.

  * - ``providerId``
    - The ID for this Provider. For more information, see `the REST Reference chapter <https://docs.stormpath.com/rest/product-guide/latest/reference.html#provider>`__.

  * - ``clientId``
    - (Social Directories only) The OAuth 2.0 Client ID for this Provider.

  * - ``scope``
    - (Social Directories only) An array containing the scope(s) that are being requested from the social provider.

**Example Request**

.. code-block:: http

  GET /login HTTP/1.1
  Accept: application/json
  Host: smooth-ensign.apps.dev.stormpath.io

**Success Response**

``200 OK`` along with the JSON view model.

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

.. _post-oauth-token:

OAuth 2.0 Login
^^^^^^^^^^^^^^^

**URL**

  ``https://{DNS-LABEL}.apps.stormpath.io/oauth/token``

The OAuth endpoint takes one of the following:

- Username & Password (URL-encoded)
- Client Credentials (Basic Auth Base64 encoded API Key ID & Secret)
- Refresh Token (URL-encoded)

And returns OAuth 2.0 Access and Refresh tokens. Note that the names of the returned Access and Refresh tokens are configurable. For more information, see :ref:`configuration`.

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

  The ``username`` can also be the Account ``email``.

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


