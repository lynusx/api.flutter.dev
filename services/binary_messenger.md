@docImport 'dart:ui';

@docImport 'package:flutter_test/flutter_test.dart';

# MessageHandler

```dart
typedef MessageHandler = Future<ByteData?>? Function(ByteData? message)
```

A function which takes a platform message and asynchronously returns an encoded response.

# BinaryMessenger

```dart
abstract class BinaryMessenger {}
```

A messenger which sends binary data across the Flutter platform barrier.

This class also registers handlers for incoming messages.

### BinaryMessenger()

```dart
BinaryMessenger()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### handlePlatformMessage()

```dart
Future<void> handlePlatformMessage(String channel, ByteData? data, ui.PlatformMessageResponseCallback? callback)
```

Queues a message.

The returned future completes immediately.

This method adds the provided message to the given channel (named by the `channel` argument) of the [ChannelBuffers] object. This simulates what happens when a plugin on the platform thread (e.g. Kotlin or Swift code) sends a message to the plugin package on the Dart thread.

The `data` argument contains the message as encoded bytes. (The format used for the message depends on the channel.)

The `callback` argument, if non-null, is eventually invoked with the response that would have been sent to the platform thread.

In production code, it is more efficient to call `ServicesBinding.instance.channelBuffers.push` directly.

In tests, consider using `tester.binding.defaultBinaryMessenger.handlePlatformMessage` (see [WidgetTester], [TestWidgetsFlutterBinding], [TestDefaultBinaryMessenger], and [TestDefaultBinaryMessenger.handlePlatformMessage] respectively).

To register a handler for a given message channel, see [setMessageHandler].

To send a message _to_ a plugin on the platform thread, see [send].

### send()

```dart
Future<ByteData?>? send(String channel, ByteData? message)
```

Send a binary message to the platform plugins on the given channel.

Returns a [Future] which completes to the received response, undecoded, in binary form.

### setMessageHandler()

```dart
void setMessageHandler(String channel, MessageHandler? handler)
```

Set a callback for receiving messages from the platform plugins on the given channel, without decoding them.

The given callback will replace the currently registered callback for that channel, if any. To remove the handler, pass null as the [handler] argument.

The handler's return value, if non-null, is sent as a response, unencoded.
