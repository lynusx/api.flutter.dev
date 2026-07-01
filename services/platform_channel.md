# shouldProfilePlatformChannels

```dart
bool get shouldProfilePlatformChannels
```

Profile and print statistics on Platform Channel usage.

When this is true statistics about the usage of Platform Channels will be printed out periodically to the console and Timeline events will show the time between sending and receiving a message (encoding and decoding time excluded).

The statistics include the total bytes transmitted and the average number of bytes per invocation in the last quantum. "Up" means in the direction of Flutter to the host platform, "down" is the host platform to flutter.

# kProfilePlatformChannels

```dart
bool kProfilePlatformChannels
```

Controls whether platform channel usage can be debugged in release mode.

See also:

- [shouldProfilePlatformChannels], which checks both [kProfilePlatformChannels] and [debugProfilePlatformChannels] for the current run mode.
- [debugProfilePlatformChannels], which determines whether platform channel usage can be debugged in non-release mode.

# BasicMessageChannel

```dart
class BasicMessageChannel<T> {}
```

A named channel for communicating with platform plugins using asynchronous message passing.

Messages are encoded into binary before being sent, and binary messages received are decoded into Dart values. The [MessageCodec] used must be compatible with the one used by the platform plugin. This can be achieved by creating a basic message channel counterpart of this channel on the platform side. The Dart type of messages sent and received is [T], but only the values supported by the specified [MessageCodec] can be used. The use of unsupported values should be considered programming errors, and will result in exceptions being thrown. The null message is supported for all codecs.

The logical identity of the channel is given by its name. Identically named channels will interfere with each other's communication.

All [BasicMessageChannel]s provided by the Flutter framework guarantee FIFO ordering. Applications can assume messages sent via a built-in [BasicMessageChannel] are delivered in the same order as they're sent.

See: <https://flutter.dev/to/platform-channels/>

### BasicMessageChannel()

```dart
BasicMessageChannel(String name, MessageCodec<T> codec, {BinaryMessenger? binaryMessenger})
```

Creates a [BasicMessageChannel] with the specified [name], [codec] and [binaryMessenger].

The default [ServicesBinding.defaultBinaryMessenger] instance is used if [binaryMessenger] is null.

### name

```dart
String name
```

The logical channel on which communication happens, not null.

### codec

```dart
MessageCodec<T> codec
```

The message codec used by this channel, not null.

### binaryMessenger

```dart
BinaryMessenger get binaryMessenger
```

The messenger which sends the bytes for this channel.

On the root isolate or web, this defaults to the [ServicesBinding.defaultBinaryMessenger]. In other contexts the default value is a [BackgroundIsolateBinaryMessenger] from [BackgroundIsolateBinaryMessenger.ensureInitialized].

### send()

```dart
Future<T?> send(T message)
```

Sends the specified [message] to the platform plugins on this channel.

Returns a [Future] which completes to the received response, which may be null.

### setMessageHandler()

```dart
void setMessageHandler(Future<T> Function(T? message)? handler)
```

Sets a callback for receiving messages from the platform plugins on this channel. Messages may be null.

The given callback will replace the currently registered callback for this channel, if any. To remove the handler, pass null as the `handler` argument.

The handler's return value is sent back to the platform plugins as a message reply. It may be null.

# MethodChannel

```dart
class MethodChannel {}
```

A named channel for communicating with platform plugins using asynchronous method calls.

Method calls are encoded into binary before being sent, and binary results received are decoded into Dart values. The [MethodCodec] used must be compatible with the one used by the platform plugin. This can be achieved by creating a method channel counterpart of this channel on the platform side. The Dart type of arguments and results is `dynamic`, but only values supported by the specified [MethodCodec] can be used. The use of unsupported values should be considered programming errors, and will result in exceptions being thrown. The null value is supported for all codecs.

The logical identity of the channel is given by its name. Identically named channels will interfere with each other's communication.

{@template flutter.services.method_channel.FIFO} All [MethodChannel]s provided by the Flutter framework guarantee FIFO ordering. Applications can assume method calls sent via a built-in [MethodChannel] are received by the platform plugins in the same order as they're sent. {@endtemplate}

See: <https://flutter.dev/to/platform-channels/>

### MethodChannel()

```dart
MethodChannel(String name, [MethodCodec codec = const StandardMethodCodec(), BinaryMessenger? binaryMessenger])
```

Creates a [MethodChannel] with the specified [name].

The [codec] used will be [StandardMethodCodec], unless otherwise specified.

The default [ServicesBinding.defaultBinaryMessenger] instance is used if [binaryMessenger] is null.

### name

```dart
String name
```

The logical channel on which communication happens, not null.

### codec

```dart
MethodCodec codec
```

The message codec used by this channel, not null.

### binaryMessenger

```dart
BinaryMessenger get binaryMessenger
```

The messenger which sends the bytes for this channel.

On the root isolate or web, this defaults to the [ServicesBinding.defaultBinaryMessenger]. In other contexts the default value is a [BackgroundIsolateBinaryMessenger] from [BackgroundIsolateBinaryMessenger.ensureInitialized].

### invokeMethod()

```dart
Future<T?> invokeMethod<T>(String method, [dynamic arguments])
```

Invokes a [method] on this channel with the specified [arguments].

The static type of [arguments] is `dynamic`, but only values supported by the [codec] of this channel can be used. The same applies to the returned result. The values supported by the default codec and their platform-specific counterparts are documented with [StandardMessageCodec].

The generic argument `T` of the method can be inferred by the surrounding context, or provided explicitly. If it does not match the returned type of the channel, a [TypeError] will be thrown at runtime. `T` cannot be a class with generics other than `dynamic`. For example, `Map<String, String>` is not supported but `Map<dynamic, dynamic>` or `Map` is.

Returns a [Future] which completes to one of the following:

- a result (possibly null), on successful invocation;
- a [PlatformException], if the invocation failed in the platform plugin;
- a [MissingPluginException], if the method has not been implemented by a platform plugin.

The following code snippets demonstrate how to invoke platform methods in Dart using a MethodChannel and how to implement those methods in Java (for Android) and Objective-C (for iOS).

{@tool snippet}

The code might be packaged up as a musical plugin, see <https://flutter.dev/to/develop-packages>:

```dart
abstract final class Music {
  static const MethodChannel _channel = MethodChannel('music');

  static Future<bool> isLicensed() async {
    // invokeMethod returns a Future<T?>, so we handle the case where
    // the return value is null by treating null as false.
    return _channel.invokeMethod<bool>('isLicensed').then<bool>((bool? value) => value ?? false);
  }

  static Future<List<Song>> songs() async {
    // invokeMethod here returns a Future<dynamic> that completes to a
    // List<dynamic> with Map<dynamic, dynamic> entries. Post-processing
    // code thus cannot assume e.g. List<Map<String, String>> even though
    // the actual values involved would support such a typed container.
    // The correct type cannot be inferred with any value of `T`.
    final List<dynamic>? songs = await _channel.invokeMethod<List<dynamic>>('getSongs');
    return songs?.cast<Map<String, Object?>>().map<Song>(Song.fromJson).toList() ?? <Song>[];
  }

  static Future<void> play(Song song, double volume) async {
    // Errors occurring on the platform side cause invokeMethod to throw
    // PlatformExceptions.
    try {
      return await _channel.invokeMethod('play', <String, dynamic>{
        'song': song.id,
        'volume': volume,
      });
    } on PlatformException catch (e) {
      throw ArgumentError('Unable to play ${song.title}: ${e.message}');
    }
  }
}

class Song {
  Song(this.id, this.title, this.artist);

  final String id;
  final String title;
  final String artist;

  static Song fromJson(Map<String, Object?> json) {
    return Song(json['id']! as String, json['title']! as String, json['artist']! as String);
  }
}
```

{@end-tool}

{@tool snippet}

Java (for Android):

```java
// Assumes existence of an Android MusicApi.
public class MusicPlugin implements MethodCallHandler {
  @Override
  public void onMethodCall(MethodCall call, Result result) {
    switch (call.method) {
      case "isLicensed":
        result.success(MusicApi.checkLicense());
        break;
      case "getSongs":
        final List<MusicApi.Track> tracks = MusicApi.getTracks();
        final List<Object> json = ArrayList<>(tracks.size());
        for (MusicApi.Track track : tracks) {
          json.add(track.toJson()); // Map<String, Object> entries
        }
        result.success(json);
        break;
      case "play":
        final String song = call.argument("song");
        final double volume = call.argument("volume");
        try {
          MusicApi.playSongAtVolume(song, volume);
          result.success(null);
        } catch (MusicalException e) {
          result.error("playError", e.getMessage(), null);
        }
        break;
      default:
        result.notImplemented();
    }
  }
  // Other methods elided.
}
```

{@end-tool}

{@tool snippet}

Objective-C (for iOS):

```objectivec
@interface MusicPlugin : NSObject<FlutterPlugin>
@end

// Assumes existence of an iOS Broadway Play Api.
@implementation MusicPlugin
- (void)handleMethodCall:(FlutterMethodCall*)call result:(FlutterResult)result {
  if ([@"isLicensed" isEqualToString:call.method]) {
    result([NSNumber numberWithBool:[BWPlayApi isLicensed]]);
  } else if ([@"getSongs" isEqualToString:call.method]) {
    NSArray* items = [BWPlayApi items];
    NSMutableArray* json = [NSMutableArray arrayWithCapacity:items.count];
    for (final BWPlayItem* item in items) {
      [json addObject:@{ @"id":item.itemId, @"title":item.name, @"artist":item.artist }];
    }
    result(json);
  } else if ([@"play" isEqualToString:call.method]) {
    NSString* itemId = call.arguments[@"song"];
    NSNumber* volume = call.arguments[@"volume"];
    NSError* error = nil;
    BOOL success = [BWPlayApi playItem:itemId volume:volume.doubleValue error:&error];
    if (success) {
      result(nil);
    } else {
      result([FlutterError errorWithCode:[NSString stringWithFormat:@"Error %ld", error.code]
                                 message:error.domain
                                 details:error.localizedDescription]);
    }
  } else {
    result(FlutterMethodNotImplemented);
  }
}
// Other methods elided.
@end
```

{@end-tool}

See also:

- [invokeListMethod], for automatically returning typed lists.
- [invokeMapMethod], for automatically returning typed maps.
- [StandardMessageCodec] which defines the payload values supported by [StandardMethodCodec].
- [JSONMessageCodec] which defines the payload values supported by [JSONMethodCodec].
- <https://api.flutter.dev/javadoc/io/flutter/plugin/common/MethodCall.html> for how to access method call arguments on Android.

### invokeListMethod()

```dart
Future<List<T>?> invokeListMethod<T>(String method, [dynamic arguments])
```

An implementation of [invokeMethod] that can return typed lists.

Dart generics are reified, meaning that an untyped `List<dynamic>` cannot masquerade as a `List<T>`. Since [invokeMethod] can only return dynamic lists, we instead create a new typed list using [List.cast].

See also:

- [invokeMethod], which this call delegates to.

### invokeMapMethod()

```dart
Future<Map<K, V>?> invokeMapMethod<K, V>(String method, [dynamic arguments])
```

An implementation of [invokeMethod] that can return typed maps.

Dart generics are reified, meaning that an untyped `Map<dynamic, dynamic>` cannot masquerade as a `Map<K, V>`. Since [invokeMethod] can only return dynamic maps, we instead create a new typed map using [Map.cast].

See also:

- [invokeMethod], which this call delegates to.

### setMethodCallHandler()

```dart
void setMethodCallHandler(Future<dynamic> Function(MethodCall call)? handler)
```

Sets a callback for receiving method calls on this channel.

The given callback will replace the currently registered callback for this channel, if any. To remove the handler, pass null as the `handler` argument.

If the future returned by the handler completes with a result, that value is sent back to the platform plugin caller wrapped in a success envelope as defined by the [codec] of this channel. If the future completes with a [PlatformException], the fields of that exception will be used to populate an error envelope which is sent back instead. If the future completes with a [MissingPluginException], an empty reply is sent similarly to what happens if no method call handler has been set. Any other exception results in an error envelope being sent.

# OptionalMethodChannel

```dart
class OptionalMethodChannel extends MethodChannel {}
```

A [MethodChannel] that ignores missing platform plugins.

When [invokeMethod] fails to find the platform plugin, it returns null instead of throwing an exception.

{@macro flutter.services.method_channel.FIFO}

### OptionalMethodChannel()

```dart
OptionalMethodChannel(String name, [MethodCodec codec, BinaryMessenger? binaryMessenger])
```

Creates a [MethodChannel] that ignores missing platform plugins.

### invokeMethod()

```dart
Future<T?> invokeMethod<T>(String method, [dynamic arguments])
```

# EventChannel

```dart
class EventChannel {}
```

A named channel for communicating with platform plugins using event streams.

Stream setup requests are encoded into binary before being sent, and binary events and errors received are decoded into Dart values. The [MethodCodec] used must be compatible with the one used by the platform plugin. This can be achieved by creating an [EventChannel] counterpart of this channel on the platform side. The Dart type of events sent and received is `dynamic`, but only values supported by the specified [MethodCodec] can be used.

The logical identity of the channel is given by its name. Identically named channels will interfere with each other's communication.

See: <https://flutter.dev/to/platform-channels/>

### EventChannel()

```dart
EventChannel(String name, [MethodCodec codec = const StandardMethodCodec(), BinaryMessenger? binaryMessenger])
```

Creates an [EventChannel] with the specified [name].

The [codec] used will be [StandardMethodCodec], unless otherwise specified.

Neither [name] nor [codec] may be null. The default [ServicesBinding.defaultBinaryMessenger] instance is used if [binaryMessenger] is null.

### name

```dart
String name
```

The logical channel on which communication happens, not null.

### codec

```dart
MethodCodec codec
```

The message codec used by this channel, not null.

### binaryMessenger

```dart
BinaryMessenger get binaryMessenger
```

The messenger which sends the bytes for this channel.

On the root isolate or web, this defaults to the [ServicesBinding.defaultBinaryMessenger]. In other contexts the default value is a [BackgroundIsolateBinaryMessenger] from [BackgroundIsolateBinaryMessenger.ensureInitialized].

### receiveBroadcastStream()

```dart
Stream<dynamic> receiveBroadcastStream([dynamic arguments])
```

Sets up a broadcast stream for receiving events on this channel.

Returns a broadcast [Stream] which emits events to listeners as follows:

- a decoded data event (possibly null) for each successful event received from the platform plugin;
- an error event containing a [PlatformException] for each error event received from the platform plugin.

Errors occurring during stream activation or deactivation are reported through the [FlutterError] facility. Stream activation happens only when stream listener count changes from 0 to 1. Stream deactivation happens only when stream listener count changes from 1 to 0.
