Database Design
===============

Overview
--------

This document outlines the database schema for the SETaP API. Note that there are currently discrepancies between the database initialization script (``setup.py``) and the application logic (``main.py``).

Schema Discrepancies
--------------------

The following discrepancies exist between the current codebase files:

* **Missing Tables in setup.py:** Several tables used in ``main.py`` (``Posts``, ``EventLikes``, ``PostLikes``, ``EventReplies``, ``PostReplies``) are not initialized in ``setup.py``.
* **Unused Table in main.py:** The ``SocietyPosts`` table is created by ``setup.py`` but is not referenced or used anywhere in ``main.py``. The application instead uses a table named ``Posts``.
* **Missing Columns in setup.py:** The ``Events`` table in ``setup.py`` is missing the ``CREATED_BY`` column which is required by the creation logic in ``main.py``.

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
     - ID of the user who created the event (Missing in ``setup.py``).

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

*Note: This table is used by main.py but not initialized in setup.py.*

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

SocietyPosts
""""""""""""

*Note: This table is created by setup.py but not used by main.py.*

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Column
     - Type
     - Description
   * - ID
     - INTEGER PRIMARY KEY
     - 
   * - SOCIETY_ID
     - INTEGER
     - 
   * - USER_ID
     - INTEGER
     - 
   * - CONTENT
     - TEXT
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 

EventLikes
""""""""""

*Note: This table is used by main.py but not initialized in setup.py.*

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

*Note: This table is used by main.py but not initialized in setup.py.*

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

*Note: This table is referenced by delete operations in main.py but not initialized in setup.py.*

PostReplies
"""""""""""

*Note: This table is referenced by delete operations in main.py but not initialized in setup.py.*

Connection Management
---------------------

Best Practices
--------------
