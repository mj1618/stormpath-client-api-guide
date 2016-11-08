******************************************
Welcome to the Stormpath Client API Guide!
******************************************

The Stormpath Client API is intended for developers of Single Page Applications (SPAs) and mobile applications. Using the Client API endpoints, your application can:

- Authenticate an existing user and get back OAuth 2.0 tokens
- Retrieve the current user's Account information
- Revoke the user's OAuth tokens
- Register a new user
- Trigger the email verification workflow, as well as send a verification of that email
- Trigger the password reset email, as well as send an updated password

All Client API endpoints do not require an administrative API Key, so you don't have to worry about storing one on your client application, or having to inject one via a proxy server.

How is this different from using Stormpath without the Client API?
==================================================================

Stormpath is a cloud service allows you to register users, authenticate them, and store information about them, and all without having to implement your own encryption or user databases. However, access to the Stormpath API normally requires that your application pass an administrative API Key to authenticate each request, and client-side applications are not able to securely store API Keys.

To accommodate these client applications, the Client API allows for basic user registration and authentication tasks to be performed without requiring an administrative API key. This means that your client applications can use these endpoints in order to, for example, authenticate a user and get back a session. With this session in hand, the client application can then continue on with its own functionality, or securely communicate with a back-end application server.

[A diagram here would be key]

How does the Client API Work?
=============================

The Client API exposes a configurable set of endpoints to your applications. The endpoints are hosted by Stormpath, in URLs that are customized for each one of your Stormpath Applications:

``https://{word-pair}.apps.stormpath.io/{endpoint}``

The word pair is randomly assigned (for example ``violet-peace``) when you create an Application and stored in your Application's ``webConfig`` resource. For more information, see (jakub.todo).

The list of currently-available endpoints is as follows:

.. list-table::
  :widths: 30 70
  :header-rows: 1

  * - Endpoint
    - Functionality

  * - ``oauth/token``
    - Authenticates a user and returns an OAuth token. See :ref:`here <authentication>` for more info.

  * - ``oauth/revoke``
    - Revokes a user's existing OAuth tokens. See :ref:`here <logout>` for more info.

  * - ``/register``
    - Registers a new user. See :ref:`here <registration>` for more info.

  * - ``verify``
    - Verifies an email address. See :ref:`here <email-verification>` for more info.

  * - ``forgot``
    - Initiates the password reset workflow. See :ref:`here <password-reset>` for more info.

  * - ``change``
    - Sends an updated password. See :ref:`here <password-reset>` for more info.

  * - ``login``
    - Retrieves the login view data for your Application. See :ref:`here <authentication>` for more info.

  * - ``me``
    - Retrieves the current user's information. See :ref:`here <user-context>` for more info.

An example user flow using these endpoints could look as follows:

1. The user lands on the login page for your Angular application
2. They fill out and submit their username and password.
3. The username and password is sent to the Client API's ``/oauth/token`` endpoint over HTTPS
4. Stormpath validates the credentials and responds with OAuth 2.0 Access and Refresh tokens
5. Your Angular app stores the cookies in, for example, local storage.
6. The cookie is now passed along with a request to the ``/me`` endpoint in order to populate the user's Profile page.
7. The user chooses to log out, and the "Logout" button sends a request to ``/oauth/revoke``, which revokes the existing OAuth Access and Refresh tokens.

For more information, continue on to one of these sections:

.. toctree::
  :maxdepth: 1

  configuration
  client_config
  registration
  authentication
  logout
  email_verification
  password_reset
  user_context




.. Indices and tables
  ==================

