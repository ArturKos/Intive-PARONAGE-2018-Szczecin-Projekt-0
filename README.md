# Intive Patronage 2018 -- TODO App

An Android TODO / expense-tracking application built with **SQLite**, **ContentProvider**, and **CursorLoader**, developed as part of the Intive Patronage 2018 recruitment programme in Szczecin.

![Java](https://img.shields.io/badge/Java-8-orange)
![Android](https://img.shields.io/badge/Android-SDK%2026-brightgreen)
![SQLite](https://img.shields.io/badge/SQLite-3-blue)
![Gradle](https://img.shields.io/badge/Gradle-build-02303A)

## Features

- **SQLite-backed persistence** with a custom `TodoDatabaseHelper` and schema managed by `TodoTable`
- **ContentProvider** (`MyTodoContentProvider`) exposing CRUD operations via content URIs with `UriMatcher`
- **CursorLoader** for asynchronous, lifecycle-aware data loading in the list activity
- **Custom CursorAdapter** (`TodoCursorAdapter`) binding database columns to list row views
- **Create, edit, and delete** TODO entries with name, date, type (spinner), and value fields
- **Long-press context menu** for deleting entries directly from the list
- **Splash screen** with a 5-second branded intro before navigating to the main activity
- **Multi-column list view** displaying name, type, date, and value per row

## Dependencies

| Component | Version | Purpose |
|-----------|---------|---------|
| Android SDK | 26 (Oreo) | Target and compile SDK |
| Support Library | 26.1.0 | AppCompat, Support-v4 |
| Architecture Components | 1.0.0-rc1 | Lifecycle, Room (declared) |
| JUnit | 4.12 | Unit testing |
| Espresso | 3.0.1 | UI testing |
| Gradle | Android Plugin | Build system |

## Building

1. Open the project in **Android Studio** (3.0+).
2. Let Gradle sync and download dependencies.
3. Build and run on an emulator or device with API 21+:

```
./gradlew assembleDebug
```

## Architecture

The app follows the classic Android **ContentProvider + CursorLoader** pattern:

```
User Action
    |
    v
Projekt_0 (ListActivity)  <-->  CursorLoader
    |                                |
    v                                v
TodoDetailActivity          MyTodoContentProvider
                                     |
                                     v
                              TodoDatabaseHelper
                                     |
                                     v
                                  SQLite
```

## Database Schema

**Table `wydatek`** (expense/todo):

| Column | Type | Description |
|--------|------|-------------|
| `_id` | INTEGER | Primary key, auto-increment |
| `nazwa` | TEXT | Entry name |
| `data` | TEXT | Date |
| `type_id` | TEXT | Category/type |
| `wartosc` | TEXT | Value/amount |

## Project Structure

```
Intive-PARONAGE-2018-Szczecin-Projekt-0/
├── app/
│   ├── build.gradle                          # App-level Gradle config
│   ├── src/
│   │   ├── main/
│   │   │   ├── AndroidManifest.xml           # Activities and ContentProvider declaration
│   │   │   ├── java/com/example/artur/arturkos/
│   │   │   │   ├── Projekt_0.java            # Main ListActivity with CursorLoader
│   │   │   │   ├── TodoDetailActivity.java   # Create/edit form activity
│   │   │   │   ├── TodoCursorAdapter.java    # Custom CursorAdapter for list rows
│   │   │   │   ├── SplashScreen.java         # Branded splash screen
│   │   │   │   ├── contentprovider/
│   │   │   │   │   └── MyTodoContentProvider.java  # ContentProvider with UriMatcher
│   │   │   │   └── database/
│   │   │   │       ├── TodoDatabaseHelper.java     # SQLiteOpenHelper
│   │   │   │       └── TodoTable.java              # Table schema and migration
│   │   │   └── res/
│   │   │       ├── layout/                   # XML layouts (list, row, edit, splash)
│   │   │       ├── menu/                     # Options menu
│   │   │       └── values/                   # Strings, colors, styles
│   │   ├── test/                             # Unit tests
│   │   └── androidTest/                      # Instrumented tests
├── build.gradle                              # Project-level Gradle config
├── settings.gradle
└── gradle.properties
```

## License

This project is provided as-is for educational purposes.
