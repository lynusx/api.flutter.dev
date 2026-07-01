# KeyboardInsertedContent

```dart
class KeyboardInsertedContent {}
```

A class representing rich content (such as a PNG image) inserted via the system input method.

The following data is represented in this class:

- MIME Type
- Bytes
- URI

### KeyboardInsertedContent()

```dart
KeyboardInsertedContent({required String mimeType, required String uri, Uint8List? data})
```

Creates an object to represent content that is inserted from the virtual keyboard.

The mime type and URI will always be provided, but the bytedata may be null.

### KeyboardInsertedContent.fromJson()

```dart
KeyboardInsertedContent.fromJson(Map<String, dynamic> metadata)
```

Converts JSON received from the Flutter Engine into the Dart class.

### mimeType

```dart
String mimeType
```

The mime type of the inserted content.

### uri

```dart
String uri
```

The URI (location) of the inserted content, usually a "content://" URI.

### data

```dart
Uint8List? data
```

The bytedata of the inserted content.

### hasData

```dart
bool get hasData
```

Convenience getter to check if bytedata is available for the inserted content.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
