friends
=======

/friend_request
^^^^^^^^^^^^^^^

**POST**

This endpoint allows a user to send a friend request to another user. The user must provide the recipient's ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be a plain string:

.. code-block:: text

   "Friend request sent by user <Recipient ID>"

Possible errors (returned as plain strings):

* ``"null friend id"`` - if no friend ID is provided.
* ``"invalid friend id"`` - if the friend ID is negative or the user does not exist.
* ``"Already sent a friend request"`` - if a request has already been sent to this user.

/accept_friend_request
^^^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows a user to accept a friend request from another user. The user must provide the sender's ID and the token received by the ``/login`` endpoint in the header of the request.

The response will be a plain string:

.. code-block:: text

   "Friend requset from <Sender ID> accepted"

Possible errors (returned as plain strings):

* ``"null sender id"`` - if no sender ID is provided.
* ``"invalid sender id"`` - if the sender ID is invalid or no pending request exists.

/list_friends
^^^^^^^^^^^^^^

**GET**

This endpoint returns a list of all accepted friends for the authenticated user. It requires authentication.

The response will be:

.. code-block:: json

   {
       "friends": [
           {
               "id": 1,
               "username": "friend_username",
               "email": "friend@example.com"
           }
       ]
   }