Endpoints
=========

This section documents the REST API endpoints available in UniFeed.

Overview
--------

UniFeed exposes a RESTful API built with FastAPI. All endpoints return JSON responses and follow REST conventions.

Base URL
--------

All API requests should be made to::

    https://api.unifeed.example.com/v1

Authentication
--------------

Most endpoints require authentication using a Bearer token in the Authorization header::

    Authorization: Bearer <your_access_token>

Available Endpoints
-------------------

Users
^^^^^

.. list-table::
   :header-rows: 1
   :widths: 15 25 60

   * - Method
     - Endpoint
     - Description
   * - GET
     - ``/users/{user_id}``
     - Retrieve a user's profile
   * - POST
     - ``/users``
     - Create a new user account
   * - PUT
     - ``/users/{user_id}``
     - Update user profile
   * - DELETE
     - ``/users/{user_id}``
     - Delete a user account

Posts
^^^^^

.. list-table::
   :header-rows: 1
   :widths: 15 25 60

   * - Method
     - Endpoint
     - Description
   * - GET
     - ``/posts``
     - List all posts (paginated)
   * - GET
     - ``/posts/{post_id}``
     - Retrieve a specific post
   * - POST
     - ``/posts``
     - Create a new post
   * - PUT
     - ``/posts/{post_id}``
     - Update a post
   * - DELETE
     - ``/posts/{post_id}``
     - Delete a post

Comments
^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 15 25 60

   * - Method
     - Endpoint
     - Description
   * - GET
     - ``/posts/{post_id}/comments``
     - List comments on a post
   * - POST
     - ``/posts/{post_id}/comments``
     - Add a comment to a post
   * - DELETE
     - ``/comments/{comment_id}``
     - Delete a comment

Response Codes
--------------

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Code
     - Description
   * - 200
     - Success
   * - 201
     - Created
   * - 400
     - Bad Request
   * - 401
     - Unauthorized
   * - 404
     - Not Found
   * - 500
     - Internal Server Error
