Endpoints
=========

Overview
--------
This page describes the endpoints of the API used by the server.

Base URL
--------

Authentication
--------------
A token will be sent after a successful login. 
This token must be included in the header of all subsequent requests to access protected endpoints.
The header should be in the format: ``Authorization: Bearer <token>``

Available Endpoints
-------------------

/login
^^^^^^

**POST**

This endpoint is used to authenticate users and obtain a token for subsequent requests.
It accepts user credentials (email and password) and returns a token if the credentials are valid.
If successful, it returns a JSON response containing the token in the field ``access_token``.

The full response looks like this:

.. code-block:: json

   {
       "access_token": "<Token>",
       "token_type": "bearer",
       "username": "<Username>"
   }

If there is an error, the response will look like this:

.. code-block:: json

   {
       "error": "<Error Message>"
   }

The errors that can be returned are:

* ``"invalid email or password"`` - if the provided credentials are incorrect.
* ``"email and password are required"`` - if either the email or password is missing from the request.

/register
^^^^^^^^^

**POST**

This endpoint is used to create a new user account. You need to provide a username, email, and password to register a new user.

If successful, it returns this:

.. code-block:: json

   {
       "message": "User registered successfully"
   }

If there is an error, the response will look like this:

.. code-block:: json

   {
       "error": "<Error Message>"
   }

The errors that can be returned are:

* ``"username, email and password are required"`` - if any of the required fields are missing.
* ``"email must end in @myport.ac.uk"`` - if the email does not end with @myport.ac.uk.

/join_society
^^^^^^^^^^^^^

**POST**

Allows the user to join a society. The user must provide the society ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be:

.. code-block:: json

   {
       "message": "User <Username> joined society <Society ID>"
   }

This endpoint always succeeds and does not return any error messages.

/friend_request
^^^^^^^^^^^^^^^

**POST**

This endpoint allows a user to send a friend request to another user. The user must provide the recipient's ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be:

.. code-block:: json

   {
       "message": "Friend request sent to user <Recipient ID>"
   }

This endpoint always succeeds and does not return any error messages.

/accept_friend_request
^^^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows a user to accept a friend request from another user. The user must provide the sender's ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be:

.. code-block:: json

   {
       "message": "Friend request from user <Sender ID> accepted"
   }

This endpoint always succeeds and does not return any error messages.

/list_all_societies
^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns a list of all societies in the database. It does not require authentication and can be accessed by anyone.

The response will be a JSON array of society objects, each containing the following fields:

* ``id`` - The unique identifier of the society.
* ``name`` - The name of the society.
* ``description`` - A brief description of the society.
* ``created_at`` - The date and time when the society was created.

This is an example of the response:

.. code-block:: json

   {
       "societies": [
           {
               "id": 1,
               "name": "Society Name",
               "description": "Society Description",
               "created_at": "2024-01-01T00:00:00Z"
           },
           {
               "id": 2,
               "name": "Another Society",
               "description": "Another Description",
               "created_at": "2024-02-01T00:00:00Z"
           }
       ]
   }

This endpoint always succeeds and does not return any error messages.

/list_user_societies
^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns the societies that the authenticated user has joined. It requires authentication to use.

The response will be a JSON array of society objects, each containing the following fields:

* ``id`` - The unique identifier of the society.
* ``name`` - The name of the society.
* ``description`` - A brief description of the society.
* ``created_at`` - The date and time when the society was created.

This is an example of the response:

.. code-block:: json

   {
       "societies": [
           {
               "id": 1,
               "name": "Society Name",
               "description": "Society Description",
               "created_at": "2024-01-01T00:00:00Z"
           },
           {
               "id": 2,
               "name": "Another Society",
               "description": "Another Description",
               "created_at": "2024-02-01T00:00:00Z"
           }
       ]
   }

This endpoint always succeeds and does not return any error messages.
Users
^^^^^

Posts
^^^^^

Comments
^^^^^^^^

Response Codes
--------------
