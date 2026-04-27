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



/get_users_events
^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns all events from societies that the authenticated user is a member of. It requires authentication.

The response will be:

.. code-block:: json

   {
       "events": [
           {
               "id": 1,
               "name": "Event Name",
               "description": "Event Description",
               "event_date": "2024-03-01T10:00:00Z"
           }
       ]
   }

Events
------

/get_society_events/{society_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


**GET**

This endpoint returns all events for a specific society. It does not require authentication.

Parameters:

* ``society_id`` - The ID of the society (path parameter).

The response will be:

.. code-block:: json

   {
       "events": [
           {
               "id": 1,
               "name": "Event Name",
               "description": "Event Description",
               "event_date": "2024-03-01T10:00:00Z"
           }
       ]
   }

/get_event_details/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns detailed information about a specific event. It does not require authentication.

Parameters:

* ``event_id`` - The ID of the event (path parameter).

The response will be:

.. code-block:: json

   {
       "id": 1,
       "name": "Event Name",
       "description": "Event Description",
       "event_date": "2024-03-01T10:00:00Z",
       "society_name": "Society Name"
   }

Possible errors:

* ``"Event not found"`` - if the event ID does not exist.

/get_my_details
^^^^^^^^^^^^^^^

**GET**

This endpoint returns the profile information of the authenticated user, including their societies and friends. It requires authentication.

The response will be:

.. code-block:: json

   {
       "username": "user_username",
       "email": "user@myport.ac.uk",
       "created_at": "2024-01-01T00:00:00Z",
       "societies": [
           {
               "id": 1,
               "name": "Society Name"
           }
       ],
       "friends": [
           {
               "id": 2,
               "username": "friend_username"
           }
       ]
   }


/create_event
^^^^^^^^^^^^^^

**POST**

This endpoint allows committee members and presidents to create a new event. It requires authentication.

Request parameters:

* ``society_id`` - The ID of the society (required).
* ``name`` - The name of the event (required, minimum 4 characters).
* ``description`` - A description of the event (required).
* ``event_date`` - The date and time of the event (required, format DD/MM/YYYY).
* ``location`` - The location of the event (required).

The response will be:

.. code-block:: json

   {
       "message": "Event created successfully"
   }

Possible errors (some returned as plain strings, some as JSON):

* ``"Error, empty title"`` (string) - if the name is empty.
* ``"Title must be at least 4 chars long"`` (string) - if the name is shorter than 4 characters.
* ``"Location must exist"`` (string) - if the location is empty.
* ``"Error, need eescription"`` (string) - if the description is empty.
* ``"Error, Can't set a data in the past"`` (string) - if the date is before year 2000.
* ``"<Society ID> does not exist"`` (string) - if the society ID does not exist.
* ``{"error": "Only committee members and presidents can create events"}`` (JSON) - if the user lacks permissions.

/update_event/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^

**PUT**

This endpoint allows committee members and presidents to update an existing event. It requires authentication.

Parameters:

* ``event_id`` - The ID of the event to update (path parameter).

Request parameters (all optional):

* ``name`` - The new name of the event.
* ``description`` - The new description of the event.
* ``event_date`` - The new date and time of the event.
* ``location`` - The new location of the event.

The response will be:

.. code-block:: json

   {
       "message": "Event updated successfully"
   }

If no update parameters are provided, the response will be:

.. code-block:: json

   {
       "message": "No updates provided"
   }

Possible errors:

* ``"Event not found"`` - if the event ID does not exist.
* ``"Only committee members and presidents can update events"`` - if the user is not a committee member or president.

/delete_event/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows committee members and presidents to delete an event. It requires authentication.

Parameters:

* ``event_id`` - The ID of the event to delete (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Event deleted successfully"
   }

Possible errors:

* ``"Event not found"`` - if the event ID does not exist.
* ``"Only committee members and presidents can delete events"`` - if the user is not a committee member or president.

Posts
-----


/create_post
^^^^^^^^^^^^

**POST**

This endpoint allows committee members and presidents to create a new post. It requires authentication.

Request parameters:

* ``society_id`` - The ID of the society (required).
* ``content`` - The content of the post (required).

The response will be:

.. code-block:: json

   {
       "message": "Post created successfully"
   }

Possible errors:

* ``"Only committee members and presidents can create posts"`` - if the user is not a committee member or president.

/update_post/{post_id}
^^^^^^^^^^^^^^^^^^^^^^

**PUT**

This endpoint allows committee members and presidents to update an existing post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to update (path parameter).

Request parameters:

* ``content`` - The new content of the post (required).

The response will be:

.. code-block:: json

   {
       "message": "Post updated successfully"
   }

Possible errors:

* ``"Post not found"`` - if the post ID does not exist.
* ``"Only committee members and presidents can update posts"`` - if the user is not a committee member or president.

/delete_post/{post_id}
^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows committee members and presidents to delete a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to delete (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Post deleted successfully"
   }

Possible errors:

* ``"Post not found"`` - if the post ID does not exist.
* ``"Only committee members and presidents can delete posts"`` - if the user is not a committee member or president.

/get_society_posts/{society_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns all posts for a specific society, ordered by creation date (newest first). It does not require authentication.

Parameters:

* ``society_id`` - The ID of the society (path parameter).

The response will be:

.. code-block:: json

   {
       "posts": [
           {
               "id": 1,
               "content": "Post content",
               "created_at": "2024-01-01T00:00:00Z",
               "author": "author_username",
               "author_id": 1
           }
       ]
   }

Event Interactions
------------------

/like_event/{event_id}
^^^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows an authenticated user to like an event. It requires authentication.

Parameters:

* ``event_id`` - The ID of the event to like (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Event liked successfully"
   }

Possible errors:

* ``"Event not found"`` - if the event ID does not exist.
* ``"User has already liked this event"`` - if the user has already liked this event.

/unlike_event/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows an authenticated user to unlike an event. It requires authentication.

Parameters:

* ``event_id`` - The ID of the event to unlike (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Event unliked successfully"
   }

Possible errors:

* ``"User has not liked this event"`` - if the user has not liked this event.

/get_event_likes/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns the number of likes and a list of users who have liked an event. It does not require authentication.

Parameters:

* ``event_id`` - The ID of the event (path parameter).

The response will be:

.. code-block:: json

   {
       "like_count": 5,
       "users": [
           {
               "id": 1,
               "username": "user1"
           },
           {
               "id": 2,
               "username": "user2"
           }
       ]
   }

Post Interactions
-----------------

/like_post/{post_id}
^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows an authenticated user to like a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to like (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Post liked successfully"
   }

Possible errors:

* ``"Post not found"`` - if the post ID does not exist.
* ``"User has already liked this post"`` - if the user has already liked this post.

/unlike_post/{post_id}
^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows an authenticated user to unlike a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to unlike (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Post unliked successfully"
   }

Possible errors:

* ``"User has not liked this post"`` - if the user has not liked this post.

/get_post_likes/{post_id}
^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns the number of likes and a list of users who have liked a post. It does not require authentication.

Parameters:

* ``post_id`` - The ID of the post (path parameter).

The response will be:

.. code-block:: json

   {
       "like_count": 3,
       "users": [
           {
               "id": 1,
               "username": "user1"
           }
       ]
   }


Event Replies
-------------

/reply_event/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows an authenticated user to reply to an event. It requires authentication.

Parameters:

* ``event_id`` - The ID of the event to reply to (path parameter).

Request parameters:

* ``content`` - The content of the reply (required).

The response will be:

.. code-block:: json

   {
       "message": "Reply added successfully"
   }

Possible errors:

* ``"Event not found"`` - if the event ID does not exist.

/get_event_replies/{event_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns all replies for a specific event. It does not require authentication.

Parameters:

* ``event_id`` - The ID of the event (path parameter).

The response will be:

.. code-block:: json

   {
       "replies": [
           {
               "id": 1,
               "content": "Reply content",
               "created_at": "2024-01-01T00:00:00Z",
               "author": "author_username",
               "author_id": 1
           }
       ]
   }

/delete_event_reply/{reply_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows the author of a reply or a committee member of the hosting society to delete the reply. It requires authentication.

Parameters:

* ``reply_id`` - The ID of the reply to delete (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Reply deleted successfully"
   }

Possible errors:

* ``"Reply not found"`` - if the reply ID does not exist.
* ``"Unauthorized to delete this reply"`` - if the user is not the author and not a committee member.

Post Replies
------------

/reply_post/{post_id}
^^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows an authenticated user to reply to a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to reply to (path parameter).

Request parameters:

* ``content`` - The content of the reply (required).

The response will be:

.. code-block:: json

   {
       "message": "Reply added successfully"
   }

Possible errors:

* ``"Post not found"`` - if the post ID does not exist.

/get_post_replies/{post_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns all replies for a specific post. It does not require authentication.

Parameters:

* ``post_id`` - The ID of the post (path parameter).

The response will be:

.. code-block:: json

   {
       "replies": [
           {
               "id": 1,
               "content": "Reply content",
               "created_at": "2024-01-01T00:00:00Z",
               "author": "author_username",
               "author_id": 1
           }
       ]
   }

/delete_post_reply/{reply_id}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows the author of a reply or a committee member of the hosting society to delete the reply. It requires authentication.

Parameters:

* ``reply_id`` - The ID of the reply to delete (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Reply deleted successfully"
   }

Possible errors:

* ``"Reply not found"`` - if the reply ID does not exist.
* ``"Unauthorized to delete this reply"`` - if the user is not the author and not a committee member.

Response Codes
--------------
