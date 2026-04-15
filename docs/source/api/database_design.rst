Database Design
===============

Overview
--------

This document outlines the database schema for the SETaP API.

Database Schema
---------------

Tables
^^^^^^

User
""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the user.
   * - USERNAME
     - TEXT
     - The user's chosen display name.
   * - EMAIL
     - TEXT
     - The user's email address (must end in @myport.ac.uk).
   * - PASSWORDHASH
     - TEXT
     - Argon2 hash of the user's password.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the account was created.
   * - LAST_LOGIN
     - TIMESTAMP
     - Date and time of the user's last successful login.

Friends
"""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the friendship record.
   * - USER_ID
     - INTEGER
     - ID of the user who initiated the request.
   * - FRIEND_ID
     - INTEGER
     - ID of the user receiving the request.
   * - STATUS
     - TEXT
     - Current status of the friendship (e.g., 'pending', 'accepted').
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the request was sent.

Societies
"""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the society.
   * - NAME
     - TEXT
     - The name of the society.
   * - DESCRIPTION
     - TEXT
     - A brief description of the society's purpose.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the society was created.

Events
""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the event.
   * - SOCIETY_ID
     - INTEGER
     - ID of the society hosting the event.
   * - NAME
     - TEXT
     - The name of the event.
   * - DESCRIPTION
     - TEXT
     - A detailed description of the event.
   * - EVENT_DATE
     - TIMESTAMP
     - The scheduled date and time for the event.
   * - LOCATION
     - TEXT
     - The physical or virtual location of the event.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the event was created.
   * - CREATED_BY
     - INTEGER
     - ID of the user who created the event.

SocietyMemberships
""""""""""""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the membership.
   * - USER_ID
     - INTEGER
     - ID of the member user.
   * - SOCIETY_ID
     - INTEGER
     - ID of the society.
   * - ROLE
     - TEXT
     - The user's role (e.g., 'member', 'committee', 'president').
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the user joined.

Posts
"""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the post.
   * - SOCIETY_ID
     - INTEGER
     - ID of the society the post belongs to.
   * - CONTENT
     - TEXT
     - The text content of the post.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the post was created.
   * - CREATED_BY
     - INTEGER
     - ID of the user who created the post.

EventLikes
""""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - EVENT_ID
     - INTEGER
     - ID of the liked event.
   * - USER_ID
     - INTEGER
     - ID of the user who liked the event.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the like was added.

PostLikes
"""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - POST_ID
     - INTEGER
     - ID of the liked post.
   * - USER_ID
     - INTEGER
     - ID of the user who liked the post.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the like was added.

EventReplies
""""""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the reply.
   * - EVENT_ID
     - INTEGER
     - ID of the event being replied to.
   * - USER_ID
     - INTEGER
     - ID of the user who wrote the reply.
   * - CONTENT
     - TEXT
     - The text content of the reply.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the reply was created.

PostReplies
"""""""""""

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - Unique identifier for the reply.
   * - POST_ID
     - INTEGER
     - ID of the post being replied to.
   * - USER_ID
     - INTEGER
     - ID of the user who wrote the reply.
   * - CONTENT
     - TEXT
     - The text content of the reply.
   * - CREATED_AT
     - TIMESTAMP
     - Date and time the reply was created.

Connection Management
---------------------

Best Practices
--------------
