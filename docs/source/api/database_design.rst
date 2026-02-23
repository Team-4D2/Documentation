Database Design
===============

This section covers the database architecture for UniFeed.

Overview
--------

UniFeed uses SQLite with AIOSQLite for asynchronous database operations. This allows for non-blocking database queries, which is essential for maintaining performance in an async FastAPI application.

Database Schema
---------------

.. note::

   The database schema is designed to support the core features of the UniFeed social media platform.

Tables
^^^^^^

The following tables are used in the UniFeed database:

* **users** - Stores user account information
* **posts** - Stores user-generated content
* **comments** - Stores comments on posts
* **likes** - Stores likes/reactions on posts
* **follows** - Stores follower/following relationships

Connection Management
---------------------

AIOSQLite provides an async context manager for database connections::

    import aiosqlite

    async with aiosqlite.connect("unifeed.db") as db:
        async with db.execute("SELECT * FROM users") as cursor:
            rows = await cursor.fetchall()

Best Practices
--------------

1. Always use parameterized queries to prevent SQL injection
2. Use transactions for operations that modify multiple tables
3. Close connections properly using async context managers
4. Use connection pooling for high-traffic scenarios
