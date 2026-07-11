# DrainChannelCallback

```dart
typedef DrainChannelCallback = Future<void> Function(ByteData? data, PlatformMessageResponseCallback callback)
```

Deprecated. Migrate to [ChannelCallback] instead.

Signature for [ChannelBuffers.drain]'s `callback` argument.

The first argument is the data sent by the plugin.

The second argument is a closure that, when called, will send messages back to the plugin.

# ChannelCallback

```dart
typedef ChannelCallback = void Function(ByteData? data, PlatformMessageResponseCallback callback)
```

Signature for [ChannelBuffers.setListener]'s `callback` argument.

The first argument is the data sent by the plugin.

The second argument is a closure that, when called, will send messages back to the plugin.

See also:

- [PlatformMessageResponseCallback], the type used for replies.

# ChannelBuffers

```dart
class ChannelBuffers {}
```

The buffering and dispatch mechanism for messages sent by plugins on the engine side to their corresponding plugin code on the framework side.

Messages for a channel are stored until a listener is provided for that channel, using [setListener]. Only one listener may be configured per channel.

Typically these buffers are drained once a callback is set up on the [BinaryMessenger] in the Flutter framework. (See [setListener].)

## Channel names

By convention, channels are normally named with a reverse-DNS prefix, a slash, and then a domain-specific name. For example, `com.example/demo`.

Channel names cannot contain the U+0000 NULL character, because they are passed through APIs that use null-terminated strings.

## Buffer capacity and overflow

Each channel has a finite buffer capacity and messages will be deleted in a first-in-first-out (FIFO) manner if the capacity is exceeded.

By default buffers store one message per channel, and when a message overflows, in debug mode, a message is printed to the console. The message looks like the following:

> A message on the com.example channel was discarded before it could be
> handled.
> This happens when a plugin sends messages to the framework side before the
> framework has had an opportunity to register a listener. See the
> ChannelBuffers API documentation for details on how to configure the channel
> to expect more messages, or to expect messages to get discarded:
> https://api.flutter.dev/flutter/dart-ui/ChannelBuffers-class.html

There are tradeoffs associated with any size. The correct size should be chosen for the semantics of the channel. To change the size a plugin can send a message using the control channel, as described below.

Size 0 is appropriate for channels where messages sent before the engine and framework are ready should be ignored. For example, a plugin that notifies the framework any time a radiation sensor detects an ionization event might set its size to zero since past ionization events are typically not interesting, only instantaneous readings are worth tracking.

Size 1 is appropriate for level-triggered plugins. For example, a plugin that notifies the framework of the current value of a pressure sensor might leave its size at one (the default), while sending messages continually; once the framework side of the plugin registers with the channel, it will immediately receive the most up to date value and earlier messages will have been discarded.

Sizes greater than one are appropriate for plugins where every message is important. For example, a plugin that itself registers with another system that has been buffering events, and immediately forwards all the previously-buffered events, would likely wish to avoid having any messages dropped on the floor. In such situations, it is important to select a size that will avoid overflows. It is also important to consider the potential for the framework side to never fully initialize (e.g. if the user starts the application, but terminates it soon afterwards, leaving time for the platform side of a plugin to run but not the framework side).

## The control channel

A plugin can configure its channel's buffers by sending messages to the control channel, `dev.flutter/channel-buffers` (see [kControlChannelName]).

There are two messages that can be sent to this control channel, to adjust the buffer size and to disable the overflow warnings. See [handleMessage] for details on these messages.

### ChannelBuffers()

```dart
ChannelBuffers()
```

Create a buffer pool for platform messages.

It is generally not necessary to create an instance of this class; the global [channelBuffers] instance is the one used by the engine.

### kDefaultBufferSize

```dart
int kDefaultBufferSize
```

The number of messages that channel buffers will store by default.

### kControlChannelName

```dart
String kControlChannelName
```

The name of the channel that plugins can use to communicate with the channel buffers system.

These messages are handled by [handleMessage].

### push()

```dart
void push(String name, ByteData? data, PlatformMessageResponseCallback callback)
```

Adds a message (`data`) to the named channel buffer (`name`).

The `callback` argument is a closure that, when called, will send messages back to the plugin.

If a message overflows the channel, and the channel has not been configured to expect overflow, then, in debug mode, a message will be printed to the console warning about the overflow.

Channel names cannot contain the U+0000 NULL character, because they are passed through APIs that use null-terminated strings.

### setListener()

```dart
void setListener(String name, ChannelCallback callback)
```

Sets the listener for the specified channel.

When there is a listener, messages are sent immediately.

Each channel may have up to one listener set at a time. Setting a new listener on a channel with an existing listener clears the previous one.

Callbacks are invoked in their own stack frame and use the zone that was current when the callback was registered.

## Draining

If any messages were queued before the listener is added, they are drained asynchronously after this method returns.

Each message is handled in its own microtask. No messages can be queued by plugins while the queue is being drained, but any microtasks queued by the handler itself will be processed before the next message is handled.

The draining stops if the listener is removed.

### clearListener()

```dart
void clearListener(String name)
```

Clears the listener for the specified channel.

When there is no listener, messages on that channel are queued, up to [kDefaultBufferSize] (or the size configured via the control channel), and then discarded in a first-in-first-out fashion.

### sendChannelUpdate()

```dart
void sendChannelUpdate(String name, {required bool listening})
```

### drain()

```dart
Future<void> drain(String name, DrainChannelCallback callback)
```

Deprecated. Migrate to [setListener] instead.

Remove and process all stored messages for a given channel.

This should be called once a channel is prepared to handle messages (i.e. when a message handler is set up in the framework).

The messages are processed by calling the given `callback`. Each message is processed in its own microtask.

### handleMessage()

```dart
void handleMessage(ByteData data)
```

Handle a control message.

This is intended to be called by the platform messages dispatcher, forwarding messages from plugins to the [kControlChannelName] channel.

Messages use the [StandardMethodCodec] format. There are two methods supported: `resize` and `overflow`. The `resize` method changes the size of the buffer, and the `overflow` method controls whether overflow is expected or not.

## `resize`

The `resize` method takes as its argument a list with two values, first the channel name (a UTF-8 string less than 254 bytes long and not containing any null bytes), and second the allowed size of the channel buffer (an integer between 0 and 2147483647).

Upon receiving the message, the channel's buffer is resized. If necessary, messages are silently discarded to ensure the buffer is no bigger than specified.

For historical reasons, this message can also be sent using a bespoke format consisting of a UTF-8-encoded string with three parts separated from each other by U+000D CARRIAGE RETURN (CR) characters, the three parts being the string `resize`, the string giving the channel name, and then the string giving the decimal serialization of the new channel buffer size. For example: `resize\rchannel\r1`

## `overflow`

The `overflow` method takes as its argument a list with two values, first the channel name (a UTF-8 string less than 254 bytes long and not containing any null bytes), and second a boolean which is true if overflow is expected and false if it is not.

This sets a flag on the channel in debug mode. In release mode the message is silently ignored. The flag indicates whether overflow is expected on this channel. When the flag is set, messages are discarded silently. When the flag is cleared (the default), any overflow on the channel causes a message to be printed to the console, warning that a message was lost.

### resize()

```dart
void resize(String name, int newSize)
```

Changes the capacity of the queue associated with the given channel.

This could result in the dropping of messages if newSize is less than the current length of the queue.

This is expected to be called by platform-specific plugin code (indirectly via the control channel), not by code on the framework side. See [handleMessage].

Calling this from framework code is redundant since by the time framework code can be running, it can just subscribe to the relevant channel and there is therefore no need for any buffering.

### allowOverflow()

```dart
void allowOverflow(String name, bool allowed)
```

Toggles whether the channel should show warning messages when discarding messages due to overflow.

This is expected to be called by platform-specific plugin code (indirectly via the control channel), not by code on the framework side. See [handleMessage].

Calling this from framework code is redundant since by the time framework code can be running, it can just subscribe to the relevant channel and there is therefore no need for any messages to overflow.

This method has no effect in release builds.

# channelBuffers

```dart
ChannelBuffers channelBuffers
```

[ChannelBuffers] that allow the storage of messages between the Engine and the Framework. Typically messages that can't be delivered are stored here until the Framework is able to process them.

See also:

- [BinaryMessenger], where [ChannelBuffers] are typically read.
