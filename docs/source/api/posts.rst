Posts
=====

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
