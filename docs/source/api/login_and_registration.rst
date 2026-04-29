
login and registration
======================

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

* ``"Username, email and password are required"`` - if any of the required fields are missing.
* ``"Email must end with @myport.ac.uk"`` - if the email does not end with @myport.ac.uk.

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

* ``"Invalid email or password"`` - if the provided credentials are incorrect.
* ``"Email and password are required"`` - if either the email or password is missing from the request.


