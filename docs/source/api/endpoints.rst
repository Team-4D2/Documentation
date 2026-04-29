Endpoints
=========

Overview
--------
This page describes the endpoints of the API used by the server.

Authentication
--------------
A token will be sent after a successful login. 
This token must be included in the header of all subsequent requests to access protected endpoints.
The header should be in the format: ``Authorization: Bearer <token>``

Available Endpoints
-------------------

.. toctree::
   :maxdepth: 2

   login_and_registration
   friends
   societies
   events
   event interactions <event_interactions>
   event replies <event_replies>
   posts
   post interactions <post_interactions>
   post replies <post_replies>

Error codes
-----------

.. caution::
	the errors are returned with 200 or 201 error codes so the response body will need to be checked if there is an error.