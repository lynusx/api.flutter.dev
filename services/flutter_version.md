# FlutterVersion

```dart
abstract final class FlutterVersion {}
```

Details about the Flutter version this app was compiled with, corresponding to the output of `flutter --version`.

When this Flutter version was built from a fork, or when Flutter runs in a custom embedder, these values might be unreliable.

See also:

- [Platform.version]

### version

```dart
String? version
```

The Flutter version used to compile the app.

### channel

```dart
String? channel
```

The Flutter channel used to compile the app.

### gitUrl

```dart
String? gitUrl
```

The URL of the Git repository from which Flutter was obtained.

### frameworkRevision

```dart
String? frameworkRevision
```

The Flutter framework revision, as a (short) Git commit ID.

### engineRevision

```dart
String? engineRevision
```

The Flutter engine revision.

### dartVersion

```dart
String? dartVersion
```

The Dart version used to compile the app.
