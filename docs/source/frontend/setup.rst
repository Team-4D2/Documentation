Setup
=====

Prerequisites
-------------

* `Flutter SDK <https://docs.flutter.dev/get-started/install>`_ (stable channel)
* Dart (bundled with Flutter)
* Android Studio or VS Code with the Flutter extension (for device emulation)
* The UniFeed backend running locally (see :ref:`installation`)

Installation
------------

1. Clone the repository.
2. Navigate to the ``Frontend`` directory.
3. Fetch dependencies:

   .. code-block:: bash

      flutter pub get

4. Ensure the backend is running on ``http://127.0.0.1:8000``.
5. Launch the app:

   .. code-block:: bash

      flutter run

   To target a specific platform explicitly:

   .. code-block:: bash

      flutter run -d chrome     # web
      flutter run -d android    # Android emulator or device

Dependencies
------------

The project uses the following packages (defined in ``pubspec.yaml``):

* ``http`` — HTTP client for all API requests.
* ``flutter_secure_storage`` — Encrypted local storage used to persist the authentication token across sessions.

Configuration
-------------

The backend base URL is currently hardcoded as ``http://127.0.0.1:8000`` throughout the source files. To point the app at a different host, update the ``Uri.parse(...)`` calls in:

* ``lib/login.dart``
* ``lib/register.dart``
* ``lib/soc_manager.dart``
* ``lib/society_details.dart``

Theming
-------

App-wide colours are defined in ``lib/app_styles.dart``:

.. list-table::
   :header-rows: 1
   :widths: 30 20 50

   * - Constant
     - Hex
     - Usage
   * - ``portsmouthPurple``
     - ``#4D2963``
     - AppBar background, primary accent, join/leave buttons
   * - ``portsmouthBlue``
     - ``#019EE2``
     - AppBar foreground, event date border highlight
