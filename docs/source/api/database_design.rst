Database Design
===============

Overview
--------

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
     - 
   * - USERNAME
     - TEXT
     - 
   * - EMAIL
     - TEXT
     - 
   * - PASSWORDHASH
     - TEXT
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 
   * - LAST_LOGIN
     - TIMESTAMP
     - 

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
     - 
   * - USER_ID
     - INTEGER
     - 
   * - FRIEND_ID
     - INTEGER
     - 
   * - STATUS
     - TEXT
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 

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
     - 
   * - NAME
     - TEXT
     - 
   * - DESCRIPTION
     - TEXT
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 

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
     - 
   * - SOCIETY_ID
     - INTEGER
     - 
   * - NAME
     - TEXT
     - 
   * - DESCRIPTION
     - TEXT
     - 
   * - EVENT_DATE
     - TIMESTAMP
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 

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
     - 
   * - USER_ID
     - INTEGER
     - 
   * - SOCIETY_ID
     - INTEGER
     - 
   * - ROLE
     - TEXT
     - 
   * - CREATED_AT
     - TIMESTAMP
     - 

SocietyPosts
""""""""""""

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

Connection Management
---------------------

Best Practices
--------------
