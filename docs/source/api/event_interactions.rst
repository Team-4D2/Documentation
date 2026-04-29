Event Interactions
==================

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
