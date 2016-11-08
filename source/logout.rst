.. _logout:

***********
Logging Out
***********

OAuth 2.0 Logout
----------------

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