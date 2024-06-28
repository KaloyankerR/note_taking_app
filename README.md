Sure! Here is the complete README file in Markdown syntax:

# Flutter Note-Taking App

## Description

This is a simple and intuitive note-taking app built with Flutter. It allows you to create, update, delete, and view notes. The app also features a settings page where you can toggle between dark and light modes. The notes are stored locally using the Isar database.

## Features

- **Home Page**: View all your notes in one place.
- **Add Note**: Click the add button to open a pop-up window where you can add a new note.
- **Update Note**: Update existing notes.
- **Delete Note**: Delete notes that you no longer need.
- **Settings Page**: Switch between dark and light modes.
- **Local Storage**: Notes are stored locally using the Isar database.

## Screenshots

| Home Page (Light Mode) | Drawer (Light Mode) |
| --- | --- |
| ![Home Page](https://github.com/KaloyankerR/note_taking_app/assets/54742816/0254e23d-35ec-4095-91e7-64b1f3f8b4b2) | ![Drawer](https://github.com/KaloyankerR/note_taking_app/assets/54742816/1ef74722-bacd-43f8-8300-460db12ca4d2) |

| Settings Page (Dark Mode) | Note Tile (Dark Mode) |
| --- | --- |
| ![Settings Page](https://github.com/KaloyankerR/note_taking_app/assets/54742816/fa759208-3161-4aaa-b0d9-a402a602a22f) | ![Note Tile](https://github.com/KaloyankerR/note_taking_app/assets/54742816/0b34d5d7-766d-47dc-b9f1-30e96d68ef18) |

| Update Note (Dark Mode) | Create Note (Dark Mode) |
| --- | --- |
| ![Update Note](https://github.com/KaloyankerR/note_taking_app/assets/54742816/9280d953-92e8-461f-9c1a-04606af7484f) | ![Create Note](https://github.com/KaloyankerR/note_taking_app/assets/54742816/e297a88c-5945-4334-9b56-0f7384ee74ed) |


## Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```

2. **Install dependencies**:
   ```sh
   flutter pub get
   ```

3. **Run the app**:
   ```sh
   flutter run
   ```

## Usage

### Home Page

- **View Notes**: On the home page, you can see all the notes you have created.
- **Add Note**: Click the add button (typically a floating action button) to open a pop-up window where you can enter the text for your new note.

### Add Note

- Enter the text for your new note in the pop-up window and click the save button to add it to your list of notes.

### Update and Delete Notes

- **Update**: Click on an existing note to edit its text.
- **Delete**: Swipe left on a note or click the delete button to remove it.

### Settings Page

- **Toggle Mode**: Open the settings page from the navigation drawer or a settings icon. Here, you can switch between dark mode and light mode.

## Database

The app uses the **Isar** database to store notes locally. Isar is a high-performance database designed for Flutter and Dart.

### Initialize Database

To initialize the Isar database, ensure you have the following setup in your code:

```dart
import 'package:isar/isar.dart';
import 'package:path_provider/path_provider.dart';
import 'dart:developer';
import 'dart:io';

class NoteDatabase extends ChangeNotifier {
  static late Isar isar;

  static Future<void> clearDatabase() async {
    final dir = await getApplicationDocumentsDirectory();
    final dbDir = Directory(dir.path);
    if (await dbDir.exists()) {
      dbDir.deleteSync(recursive: true);
    }
  }

  static Future<void> initialize() async {
    try {
      await clearDatabase();
      final dir = await getApplicationDocumentsDirectory();
      log('Database directory: ${dir.path}');
      isar = await Isar.open([NoteSchema], directory: dir.path);
      log('Database initialized successfully');
    } catch (e) {
      log('Error initializing database: $e');
      rethrow;
    }
  }
}
```

### Schema Definition

Ensure your schema is defined correctly:

```dart
import 'package:isar/isar.dart';

// Generates the file
// Run dart run build_runner build
part 'note.g.dart';

@Collection()
class Note {
  Id id = Isar.autoIncrement;
  late String text;
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any bugs, features, or enhancements.
