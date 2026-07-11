# DartPluginRegistrant

```dart
abstract final class DartPluginRegistrant {}
```

Helper functions for Dart Plugin Registrants.

### ensureInitialized()

```dart
void ensureInitialized()
```

Makes sure the that the Dart Plugin Registrant has been called for this isolate. This can safely be executed multiple times on the same isolate, but should not be called on the Root isolate.
