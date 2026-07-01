# ClipboardData

```dart
class ClipboardData {}
```

Data stored on the system clipboard.

The system clipboard can contain data of various media types. This data structure currently supports only plain text data, in the [text] property.

### ClipboardData()

```dart
ClipboardData({required String? text})
```

Creates data for the system clipboard.

### text

```dart
String? text
```

Plain text variant of this clipboard data.

# Clipboard

```dart
abstract final class Clipboard {}
```

Utility methods for interacting with the system's clipboard.

### kTextPlain

```dart
String kTextPlain
```

Plain text data format string.

Used with [getData].

### setData()

```dart
Future<void> setData(ClipboardData data)
```

Stores the given clipboard data on the clipboard.

### getData()

```dart
Future<ClipboardData?> getData(String format)
```

Retrieves data from the clipboard that matches the given format.

The `format` argument specifies the media type, such as `text/plain`, of the data to obtain.

Returns a future which completes to null if the data could not be obtained, and to a [ClipboardData] object if it could.

### hasStrings()

```dart
Future<bool> hasStrings()
```

Returns a future that resolves to true, if (and only if) the clipboard contains string data.

See also:

- [The iOS hasStrings method](https://developer.apple.com/documentation/uikit/uipasteboard/1829416-hasstrings?language=objc).
