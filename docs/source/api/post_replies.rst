Post Replies
============

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