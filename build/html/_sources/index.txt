.. Stormpath Client API Guide documentation master file, created by
   sphinx-quickstart on Mon Nov  7 14:07:56 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Stormpath Client API Guide's documentation!
======================================================

What is the Client API?
=======================

Client-side authentication is intended for developers of Single Page Applications (SPAs) and mobile applications who are either using a serverless architecture, or do not want to implement Stormpath on their backend application servers.

Since these client applications are not able to securely store API Keys, the Client API endpoints allow for basic user registration and management tasks to be performed without requiring any authentication. This means that your client applications can use these endpoints in order to, for example, authenticate a user and get back a session. With this session in hand, the client application can then continue on with its own functionality, or securely communicate with a back-end application server.

Why should I use the Client API?
--------------------------------

Scenario 1: A serverless client application...

This is relatively straightforward. The Client API is used solo, with token validation done by Stormpath.

Scenario 2: A serverful client application...

Your Stormpath-powered server is used for token validation, search, etc. Basically all of the Stormpath functionality not covered by the Client API.

How does the Client API Work?
=============================

The Client API exposes a configurable set of endpoints to your applications. Using these endpoints, the applications can:

- Authenticate an existing user and get back OAuth 2.0 tokens
- Retrieve the current user's Account information
- Revoke the user's OAuth tokens
- Register a new user
- Trigger the email verification workflow, as well as send a verification of that email
- Trigger the password reset email, as well as send an updated password

Since all of these endpoints do not require an API Key, you do not have to worry about storing one on your client application, or having to inject one via a proxy server. Additionally, these endpoints allow your client applications to use Stormpath's entire identity management system without having to add any Stormpath code to your application backend.

An example user flow could look as follows:

1. The user lands on the login page for your Angular application
2. They fill out and submit their username and password.
3. The username and password is sent to the Client API's `/oauth/token` endpoint over HTTPS
4. Stormpath validates the credentials and responds with OAuth 2.0 Access and Refresh tokens
5. Your Angular app stores the cookies in, for example, local storage

You can now get `/me`, or your application could link a Stormpath user to a user of external API like Fitbit.

For more information, continue on to one of these sections:

.. toctree::
  :maxdepth: 2

  configuration
  client_config
  registration
  authentication
  email_verification
  password_reset
  user_context




.. Indices and tables
  ==================

