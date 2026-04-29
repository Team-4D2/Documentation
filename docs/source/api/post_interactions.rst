Post Interactions
=================

/like_post/{post_id}
^^^^^^^^^^^^^^^^^^^^

**POST**

This endpoint allows an authenticated user to like a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to like (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Post liked successfully"
   }

Possible errors:

* ``"Post not found"`` - if the post ID does not exist.
* ``"User has already liked this post"`` - if the user has already liked this post.

/unlike_post/{post_id}
^^^^^^^^^^^^^^^^^^^^^^

**DELETE**

This endpoint allows an authenticated user to unlike a post. It requires authentication.

Parameters:

* ``post_id`` - The ID of the post to unlike (path parameter).

The response will be:

.. code-block:: json

   {
       "message": "Post unliked successfully"
   }

Possible errors:

* ``"User has not liked this post"`` - if the user has not liked this post.

/get_post_likes/{post_id}
^^^^^^^^^^^^^^^^^^^^^^^^^

**GET**

This endpoint returns the number of likes and a list of users who have liked a post. It does not require authentication.

Parameters:

* ``post_id`` - The ID of the post (path parameter).

The response will be:

.. code-block:: json

   {
       "like_count": 3,
       "users": [
           {
               "id": 1,
               "username": "user1"
           }
       ]
   }
