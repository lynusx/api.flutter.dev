# BackgroundIsolateBinaryMessenger

```dart
class BackgroundIsolateBinaryMessenger extends BinaryMessenger {}
```

A [BinaryMessenger] for use on background (non-root) isolates.

### instance

```dart
BinaryMessenger get instance
```

The existing instance of this class, if any.

Throws if [ensureInitialized] has not been called at least once.

### ensureInitialized()

```dart
void ensureInitialized(ui.RootIsolateToken token)
```

Ensures that [BackgroundIsolateBinaryMessenger.instance] has been initialized.

The argument should be the value obtained from [ServicesBinding.rootIsolateToken] on the root isolate.

This function is idempotent (calling it multiple times is harmless but has no effect).

### handlePlatformMessage()

```dart
Future<void> handlePlatformMessage(String channel, ByteData? data, ui.PlatformMessageResponseCallback? callback)
```

### send()

```dart
Future<ByteData?>? send(String channel, ByteData? message)
```

### setMessageHandler()

```dart
void setMessageHandler(String channel, MessageHandler? handler)
```
