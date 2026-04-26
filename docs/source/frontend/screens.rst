Screens & Components
=====================

This page documents every screen (page) and shared component in the Flutter frontend.

Navigation & Routing
--------------------

Named routes are registered in ``lib/main.dart``:

.. list-table::
   :header-rows: 1
   :widths: 25 30 45

   * - Route
     - Widget
     - Description
   * - ``/login``
     - ``LoginPage``
     - Email/password login form
   * - ``/register``
     - ``RegisterPage``
     - New account registration form
   * - ``/home``
     - ``HomePage``
     - Main shell with bottom navigation
   * - ``/societies``
     - ``SocsPage``
     - Browse all societies

On launch, the app reads the stored token from ``flutter_secure_storage``. If a token exists the user is taken directly to ``HomePage``; otherwise they are taken to ``LoginPage``.

----

Login Page
----------

**File:** ``lib/login.dart`` : ``LoginPage``

Presents two text fields (email, password) and two action buttons.

* **Login** — POSTs to ``/login`` with the email and password as query parameters. On success the ``access_token`` from the response is written to secure storage under the key ``login_token`` and the user is navigated to ``/home``. On failure a ``SnackBar`` displays the error message returned by the API.
* **Register** — Navigates to ``/register``.

The page uses the shared ``SecureTextEntry`` widget for both inputs.

----

Register Page
-------------

**File:** ``lib/register.dart`` : ``RegisterPage``

Presents four text fields: email, username, password, and confirm password.

* Client-side validation checks that the two password fields match before making any network request.
* On submit, POSTs to ``/register`` with ``username``, ``email``, and ``password`` as query parameters.
* A success ``SnackBar`` is shown and all fields are cleared. The user must tap **Login** to proceed to ``LoginPage``.
* API-level errors (e.g., non-``@myport.ac.uk`` email) are displayed via ``SnackBar``.

----

Home Page
---------

**File:** ``lib/home.dart`` : ``HomePage``

The main application shell. Displays a persistent ``AppBar`` titled *UniFeed* and a ``NavigationBar`` at the bottom with three destinations:

.. list-table::
   :header-rows: 1
   :widths: 15 20 65

   * - Index
     - Label
     - Content widget
   * - 0
     - Home
     - ``_HomeContent`` : upcoming events feed
   * - 1
     - Societies
     - ``SocsPage`` : all societies list
   * - 2
     - Join
     - ``JoinPage`` : societies the user has joined

A **Logout** icon button in the ``AppBar`` deletes the stored token and redirects to ``/login``.

Home Tab (Upcoming Events)
^^^^^^^^^^^^^^^^^^^^^^^^^^

``_HomeContent`` (private, defined in ``lib/home.dart``) fetches events via ``Event.getUserEvents()``, which calls ``GET /get_users_events`` with the bearer token. Each event is rendered as a tappable ``Card`` showing the name, a two line truncated description, and the date. Tapping navigates to ``EventDetailsPage``.

Pull-to-refresh is supported via ``RefreshIndicator``.

----

Societies Page
--------------

**File:** ``lib/socs_page.dart`` : ``SocsPage``

Calls ``Soc.listAllSocs()``, which hits ``GET /list_all_societies``. Renders a scrollable list of ``Soc`` widgets. Tapping a society navigates to ``SocietyDetailsPage``.

Join Page
^^^^^^^^^

``JoinPage`` (also in ``lib/socs_page.dart``) is the third tab in ``HomePage``. Calls ``Soc.listUserSocs()``, which hits ``GET /list_user_societies`` with the bearer token. Displays only the societies the authenticated user has joined. Shows the message *"You haven't joined any societies yet"* when the list is empty.

----

Society Details Page
--------------------

**File:** ``lib/society_details.dart`` : ``SocietyDetailsPage``

Receives a ``Soc`` object as a constructor argument. On load, fetches the society's events (``Event.getSocietyEvents(id)`` → ``GET /get_society_events/{society_id}``) and checks whether the user is already a member by comparing against ``Soc.listUserSocs()``.

Layout (top to bottom):

1. Society name (large bold heading).
2. Society description.
3. Full-width **Join Society** / **Leave Society** button (purple when joining, red when leaving). Calls ``POST /join_society`` or ``POST /leave_society`` respectively.
4. **Events** section — list of event cards identical in style to the home feed, each tappable to open ``EventDetailsPage``.

----

Event Details Page
------------------

**File:** ``lib/event_details.dart`` : ``EventDetailsPage``

Receives an ``eventId`` integer. Calls ``Event.getEventDetails(id)`` → ``GET /get_event_details/{event_id}`` on load.

Layout (top to bottom):

1. Event name (large bold heading).
2. Society name badge (tinted purple pill, shown only when ``societyName`` is non-null).
3. Date & Time container (bordered box with a calendar icon).
4. Description section (grey rounded box).
5. Event ID in small grey text at the bottom.

Shows an error state with a **Retry** button if the API call fails.

----

Make Post Page
--------------

**File:** ``lib/make_post.dart`` : ``MakePostPage``

A stub UI for composing society posts. Currently contains:

* A ``TextField`` for the post description.
* A disabled **Upload Image** button (not yet implemented).
* A **Create Post** button with no-op ``onPressed`` (implementation pending).

This screen is not yet wired into the main navigation flow.

----

Shared Widgets
--------------

**File:** ``lib/common_widgets.dart`` : ``CommonWidgets``

SecureTextEntry
^^^^^^^^^^^^^^^

A styled ``TextField`` wrapper used on the login and register screens.

.. list-table::
   :header-rows: 1
   :widths: 25 15 60

   * - Parameter
     - Type
     - Description
   * - ``hint``
     - ``String?``
     - Placeholder text shown inside the field
   * - ``textController``
     - ``TextEditingController``
     - Controller bound to the input
   * - ``obscureText``
     - ``bool?``
     - Hides input when ``true`` (defaults to ``true``)
   * - ``alignment``
     - ``TextAlign?``
     - Text alignment (defaults to ``center``)

Post Widget
^^^^^^^^^^^

A stub ``StatelessWidget`` that models a post (description, optional image, like count). The ``build`` method currently returns an empty ``Container``; full rendering is pending.

----

Data Models
-----------

**File:** ``lib/soc_manager.dart``

Soc Widget
^^^^^^^^^^

``Soc`` is both a data model and a ``StatefulWidget``. It holds ``id``, ``name``, and ``description``. Its ``_SocState`` renders a card-style tile with the society name, description, and a **Join**/**Leave** button that calls ``POST /join_society`` or ``POST /leave_society``.

Static factory methods:

* ``Soc.listAllSocs()`` : GETs ``/list_all_societies``, returns ``List<Soc>``.
* ``Soc.listUserSocs()`` : GETs ``/list_user_societies`` with bearer token, returns ``List<Soc>``.

Both methods return a single error-sentinel ``Soc`` (``id = -1``) on failure so callers can detect errors without throwing.

Event Model
^^^^^^^^^^^

``Event`` is a plain Dart class (not a widget) with fields ``id``, ``name``, ``description``, ``eventDate``, and optional ``societyName``.

Static factory methods:

* ``Event.getUserEvents()`` : GETs ``/get_users_events`` with bearer token.
* ``Event.getEventDetails(int id)`` : GETs ``/get_event_details/{id}``, returns ``Event?``.
* ``Event.getSocietyEvents(int societyId)`` : GETs ``/get_society_events/{id}``.

All methods return an empty list (or ``null``) on failure rather than throwing.
