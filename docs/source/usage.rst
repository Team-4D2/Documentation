Usage
=====

.. _installation:

Installation
------------

To use UniFeed, first install it using pip:

.. code-block:: console

   (.venv) $ pip install unifeed

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``unifeed.get_random_ingredients()`` function:

.. autofunction:: unifeed.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`unifeed.get_random_ingredients`
will raise an exception.

.. autoexception:: unifeed.InvalidKindError

For example:

>>> import unifeed
>>> unifeed.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

