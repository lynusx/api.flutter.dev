# MessageCodec

```dart
abstract class MessageCodec<T> {}
```

A message encoding/decoding mechanism.

Both operations throw an exception, if conversion fails. Such situations should be treated as programming errors.

See also:

- [BasicMessageChannel], which use [MessageCodec]s for communication between Flutter and platform plugins.

### encodeMessage()

```dart
ByteData? encodeMessage(T message)
```

Encodes the specified [message] in binary.

Returns null if the message is null.

### decodeMessage()

```dart
T? decodeMessage(ByteData? message)
```

Decodes the specified [message] from binary.

Returns null if the message is null.

# MethodCall

```dart
class MethodCall {}
```

A command object representing the invocation of a named method.

### MethodCall()

```dart
MethodCall(String method, [dynamic arguments])
```

Creates a [MethodCall] representing the invocation of [method] with the specified [arguments].

### method

```dart
String method
```

The name of the method to be called.

### arguments

```dart
dynamic arguments
```

The arguments for the method.

Must be a valid value for the [MethodCodec] used.

This property is `dynamic`, which means type-checking is skipped when accessing this property. To minimize the risk of type errors at runtime, the value should be cast to `Object?` when accessed.

### toString()

```dart
String toString()
```

# MethodCodec

```dart
abstract class MethodCodec {}
```

A codec for method calls and enveloped results.

All operations throw an exception, if conversion fails.

See also:

- [MethodChannel], which use [MethodCodec]s for communication between Flutter and platform plugins.
- [EventChannel], which use [MethodCodec]s for communication between Flutter and platform plugins.

### encodeMethodCall()

```dart
ByteData encodeMethodCall(MethodCall methodCall)
```

Encodes the specified [methodCall] into binary.

### decodeMethodCall()

```dart
MethodCall decodeMethodCall(ByteData? methodCall)
```

Decodes the specified [methodCall] from binary.

### decodeEnvelope()

```dart
dynamic decodeEnvelope(ByteData envelope)
```

Decodes the specified result [envelope] from binary.

Throws [PlatformException], if [envelope] represents an error, otherwise returns the enveloped result.

The type returned from [decodeEnvelope] is `dynamic` (not `Object?`), which means _no type checking is performed on its return value_. It is strongly recommended that the return value be immediately cast to a known type to prevent runtime errors due to typos that the type checker could otherwise catch.

### encodeSuccessEnvelope()

```dart
ByteData encodeSuccessEnvelope(Object? result)
```

Encodes a successful [result] into a binary envelope.

### encodeErrorEnvelope()

```dart
ByteData encodeErrorEnvelope({required String code, String? message, Object? details})
```

Encodes an error result into a binary envelope.

The specified error [code], human-readable error [message] and error [details] correspond to the fields of [PlatformException].

# PlatformException

```dart
class PlatformException implements Exception {}
```

Thrown to indicate that a platform interaction failed in the platform plugin.

See also:

- [MethodCodec], which throws a [PlatformException], if a received result envelope represents an error.
- [MethodChannel.invokeMethod], which completes the returned future with a [PlatformException], if invoking the platform plugin method results in an error envelope.
- [EventChannel.receiveBroadcastStream], which emits [PlatformException]s as error events, whenever an event received from the platform plugin is wrapped in an error envelope.

### PlatformException()

```dart
PlatformException({required String code, String? message, dynamic details, String? stacktrace})
```

Creates a [PlatformException] with the specified error [code] and optional [message], and with the optional error [details] which must be a valid value for the [MethodCodec] involved in the interaction.

### code

```dart
String code
```

An error code.

### message

```dart
String? message
```

A human-readable error message, possibly null.

### details

```dart
dynamic details
```

Error details, possibly null.

This property is `dynamic`, which means type-checking is skipped when accessing this property. To minimize the risk of type errors at runtime, the value should be cast to `Object?` when accessed.

### stacktrace

```dart
String? stacktrace
```

Native stacktrace for the error, possibly null.

This contains the native platform stack trace, not the Dart stack trace.

The stack trace for Dart exceptions can be obtained using try-catch blocks, for example:

```dart
try {
  // ...
} catch (e, stacktrace) {
  print(stacktrace);
}
```

On Android this field is populated when a `RuntimeException` or a subclass of it is thrown in the method call handler, as shown in the following example:

```kotlin
import androidx.annotation.NonNull
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugin.common.MethodChannel

class MainActivity: FlutterActivity() {
  private val CHANNEL = "channel_name"

  override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
    super.configureFlutterEngine(flutterEngine)
    MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler {
      call, result -> throw RuntimeException("Oh no")
    }
  }
}
```

It is also populated on Android if the method channel result is not serializable. If the result is not serializable, an exception gets thrown during the serialization process. This can be seen in the following example:

```kotlin
import androidx.annotation.NonNull
import io.flutter.embedding.android.FlutterActivity
import io.flutter.embedding.engine.FlutterEngine
import io.flutter.plugin.common.MethodChannel

class MainActivity: FlutterActivity() {
  private val CHANNEL = "channel_name"

  override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
    super.configureFlutterEngine(flutterEngine)
    MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler {
      call, result -> result.success(Object())
    }
  }
}
```

In the cases described above, the content of [stacktrace] will be the unprocessed output of calling `toString()` on the exception.

MacOS, iOS, Linux and Windows don't support querying the native stacktrace.

On custom Flutter embedders this value will be null on platforms that don't support querying the call stack.

### toString()

```dart
String toString()
```

# MissingPluginException

```dart
class MissingPluginException implements Exception {}
```

Thrown to indicate that a platform interaction failed to find a handling plugin.

See also:

- [MethodChannel.invokeMethod], which completes the returned future with a [MissingPluginException], if no plugin handler for the method call was found.
- [OptionalMethodChannel.invokeMethod], which completes the returned future with null, if no plugin handler for the method call was found.

### MissingPluginException()

```dart
MissingPluginException([String? message])
```

Creates a [MissingPluginException] with an optional human-readable error message.

### message

```dart
String? message
```

A human-readable error message, possibly null.

### toString()

```dart
String toString()
```
