@docImport 'package:flutter/material.dart';

# AssetBundle

```dart
abstract class AssetBundle {}
```

A collection of resources used by the application.

Asset bundles contain resources, such as images and strings, that can be used by an application. Access to these resources is asynchronous so that they can be transparently loaded over a network (e.g., from a [NetworkAssetBundle]) or from the local file system without blocking the application's user interface.

Applications have a [rootBundle], which contains the resources that were packaged with the application when it was built. To add resources to the [rootBundle] for your application, add them to the `assets` subsection of the `flutter` section of your application's `pubspec.yaml` manifest.

For example:

```yaml
name: my_awesome_application
flutter:
  assets:
    - images/hamilton.jpeg
    - images/lafayette.jpeg
```

Rather than accessing the [rootBundle] global static directly, consider obtaining the [AssetBundle] for the current [BuildContext] using [DefaultAssetBundle.of]. This layer of indirection lets ancestor widgets substitute a different [AssetBundle] (e.g., for testing or localization) at runtime rather than directly replying upon the [rootBundle] created at build time. For convenience, the [WidgetsApp] or [MaterialApp] widget at the top of the widget hierarchy configures the [DefaultAssetBundle] to be the [rootBundle].

See also:

- [DefaultAssetBundle]
- [NetworkAssetBundle]
- [rootBundle]

### load()

```dart
Future<ByteData> load(String key)
```

Retrieve a binary resource from the asset bundle as a data stream.

Throws an exception if the asset is not found.

The returned [ByteData] can be converted to a [Uint8List] (a list of bytes) using [Uint8List.sublistView]. Lists of bytes can be used with APIs that accept [Uint8List] objects, such as [decodeImageFromList], as well as any API that accepts a [List<int>], such as [File.writeAsBytes] or [Utf8Codec.decode] (accessible via [utf8]).

### loadBuffer()

```dart
Future<ui.ImmutableBuffer> loadBuffer(String key)
```

Retrieve a binary resource from the asset bundle as an immutable buffer.

Throws an exception if the asset is not found.

### loadString()

```dart
Future<String> loadString(String key, {bool cache = true})
```

Retrieve a string from the asset bundle.

Throws an exception if the asset is not found.

If the `cache` argument is set to false, then the data will not be cached, and reading the data may bypass the cache. This is useful if the caller is going to be doing its own caching. (It might not be cached if it's set to true either, depending on the asset bundle implementation.)

The function expects the stored string to be UTF-8-encoded as [Utf8Codec] will be used for decoding the string. If the string is larger than 50 KB, the decoding process is delegated to an isolate to avoid jank on the main thread.

### loadStructuredData()

```dart
Future<T> loadStructuredData<T>(String key, Future<T> Function(String value) parser)
```

Retrieve a string from the asset bundle, parse it with the given function, and return that function's result.

The result is not cached by the default implementation; the parser is run each time the resource is fetched. However, some subclasses may implement caching (notably, subclasses of [CachingAssetBundle]).

### loadStructuredBinaryData()

```dart
Future<T> loadStructuredBinaryData<T>(String key, FutureOr<T> Function(ByteData data) parser)
```

Retrieve [ByteData] from the asset bundle, parse it with the given function, and return that function's result.

The result is not cached by the default implementation; the parser is run each time the resource is fetched. However, some subclasses may implement caching (notably, subclasses of [CachingAssetBundle]).

### evict()

```dart
void evict(String key)
```

If this is a caching asset bundle, and the given key describes a cached asset, then evict the asset from the cache so that the next time it is loaded, the cache will be reread from the asset bundle.

### clear()

```dart
void clear()
```

If this is a caching asset bundle, clear all cached data.

### toString()

```dart
String toString()
```

# NetworkAssetBundle

```dart
class NetworkAssetBundle extends AssetBundle {}
```

An [AssetBundle] that loads resources over the network.

This asset bundle does not cache any resources, though the underlying network stack may implement some level of caching itself.

### NetworkAssetBundle()

```dart
NetworkAssetBundle(Uri baseUrl)
```

Creates a network asset bundle that resolves asset keys as URLs relative to the given base URL.

### load()

```dart
Future<ByteData> load(String key)
```

### toString()

```dart
String toString()
```

# CachingAssetBundle

```dart
abstract class CachingAssetBundle extends AssetBundle {}
```

An [AssetBundle] that permanently caches string and structured resources that have been fetched.

Strings (for [loadString] and [loadStructuredData]) are decoded as UTF-8. Data that is cached is cached for the lifetime of the asset bundle (typically the lifetime of the application).

Binary resources (from [load]) are not cached.

### loadString()

```dart
Future<String> loadString(String key, {bool cache = true})
```

### loadStructuredData()

```dart
Future<T> loadStructuredData<T>(String key, Future<T> Function(String value) parser)
```

Retrieve a string from the asset bundle, parse it with the given function, and return the function's result.

The result of parsing the string is cached (the string itself is not, unless you also fetch it with [loadString]). For any given `key`, the `parser` is only run the first time.

Once the value has been successfully parsed, the future returned by this function for subsequent calls will be a [SynchronousFuture], which resolves its callback synchronously.

Failures are not cached, and are returned as [Future]s with errors.

### loadStructuredBinaryData()

```dart
Future<T> loadStructuredBinaryData<T>(String key, FutureOr<T> Function(ByteData data) parser)
```

Retrieve bytedata from the asset bundle, parse it with the given function, and return the function's result.

The result of parsing the bytedata is cached (the bytedata itself is not). For any given `key`, the `parser` is only run the first time.

Once the value has been successfully parsed, the future returned by this function for subsequent calls will be a [SynchronousFuture], which resolves its callback synchronously.

Failures are not cached, and are returned as [Future]s with errors.

### evict()

```dart
void evict(String key)
```

### clear()

```dart
void clear()
```

### loadBuffer()

```dart
Future<ui.ImmutableBuffer> loadBuffer(String key)
```

# PlatformAssetBundle

```dart
class PlatformAssetBundle extends CachingAssetBundle {}
```

An [AssetBundle] that loads resources using platform messages.

### load()

```dart
Future<ByteData> load(String key)
```

### loadBuffer()

```dart
Future<ui.ImmutableBuffer> loadBuffer(String key)
```

# rootBundle

```dart
AssetBundle rootBundle
```

The [AssetBundle] from which this application was loaded.

The [rootBundle] contains the resources that were packaged with the application when it was built. To add resources to the [rootBundle] for your application, add them to the `assets` subsection of the `flutter` section of your application's `pubspec.yaml` manifest.

For example:

```yaml
name: my_awesome_application
flutter:
  assets:
    - images/hamilton.jpeg
    - images/lafayette.jpeg
```

Rather than using [rootBundle] directly, consider obtaining the [AssetBundle] for the current [BuildContext] using [DefaultAssetBundle.of]. This layer of indirection lets ancestor widgets substitute a different [AssetBundle] at runtime (e.g., for testing or localization) rather than directly replying upon the [rootBundle] created at build time. For convenience, the [WidgetsApp] or [MaterialApp] widget at the top of the widget hierarchy configures the [DefaultAssetBundle] to be the [rootBundle].

See also:

- [DefaultAssetBundle]
- [NetworkAssetBundle]
