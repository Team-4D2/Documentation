Usage
=====

.. _installation:

Installation
------------

To install the SETaP API, follow these steps:

1. Clone the repository.
2. Navigate to the ``SETaP-API`` directory.
3. Create a virtual environment:

   .. code-block:: bash

      python -m venv venv

4. Activate the virtual environment:

   - On Linux/macOS: ``source venv/bin/activate``
   - On Windows: ``venv\Scripts\activate``

5. Install the dependencies:

   .. code-block:: bash

      pip install -r requirement.txt

Testing
-------

The API includes a comprehensive suite of unit tests implemented using ``pytest`` and ``pytest-asyncio``. These tests cover authentication, society management, event creation, and friendship requests.

To run the tests:

1. Ensure you are in the ``SETaP-API`` directory.
2. Activate your virtual environment.
3. Run the following command:

   .. code-block:: bash

      pytest test_main.py

Test Coverage
^^^^^^^^^^^^^

The unit tests in ``test_main.py`` verify the following behaviors:

* **Authentication**: Token generation, expired tokens, and missing credentials.
* **Societies**: Joining and leaving societies, including various error cases (already a member, invalid society ID).
* **Events**: Creating events with validation for title length, location, and past dates.
* **Friends**: Sending and accepting friend requests.
* **Database**: Automatic database setup and cleanup for each test run using a fixture.

Mocking and Fixtures
^^^^^^^^^^^^^^^^^^^^

The tests use an asynchronous fixture to set up a clean ``database.db`` before each test, ensuring test isolation. It also populates the database with test users and societies.


