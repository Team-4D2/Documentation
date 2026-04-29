societies
=========

/join_society
^^^^^^^^^^^^^

**POST**

Allows the user to join a society. The user must provide the society ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be a plain string:

.. code-block:: text

   "The <User ID> has joined the society"

Possible errors (returned as plain strings):

* ``"Error Bad Soc ID"`` - if the society ID is invalid or does not exist.
* ``"<User ID> Does not exist"`` - if the user ID from the token does not exist in the database.
* ``"<User ID> is all ready in the society"`` - if the user is already a member.

/leave_society
^^^^^^^^^^^^^^^

**POST**

This endpoint allows the user to leave a society. The user must provide the society ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be a plain string:

.. code-block:: text

   "user <Username> left society <Society ID>"

Possible errors (returned as plain strings):

* ``"Invalid society id"`` - if the society ID is missing or negative.
* ``"socierty does not exsist"`` - if the society does not exist in the database.
* ``"error, user is not a member of this socierty"`` - if the user is not a member of the specified society.



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