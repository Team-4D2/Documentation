Events
======

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
