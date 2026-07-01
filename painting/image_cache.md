@docImport 'package:flutter/widgets.dart';

@docImport 'binding.dart'; @docImport 'image_provider.dart';

# ImageCache

```dart
class ImageCache {}
```

Class for caching images.

Implements a least-recently-used cache of up to 1000 images, and up to 100 MB. The maximum size can be adjusted using [maximumSize] and [maximumSizeBytes].

The cache also holds a list of 'live' references. An image is considered live if its [ImageStreamCompleter]'s listener count has never dropped to zero after adding at least one listener. The cache uses [ImageStreamCompleter.addOnLastListenerRemovedCallback] to determine when this has happened.

The [putIfAbsent] method is the main entry-point to the cache API. It returns the previously cached [ImageStreamCompleter] for the given key, if available; if not, it calls the given callback to obtain it first. In either case, the key is moved to the 'most recently used' position.

A caller can determine whether an image is already in the cache by using [containsKey], which will return true if the image is tracked by the cache in a pending or completed state. More fine grained information is available by using the [statusForKey] method.

Generally this class is not used directly. The [ImageProvider] class and its subclasses automatically handle the caching of images.

A shared instance of this cache is retained by [PaintingBinding] and can be obtained via the [imageCache] top-level property in the [painting] library.

{@tool snippet}

This sample shows how to supply your own caching logic and replace the global [imageCache] variable.

```dart
/// This is the custom implementation of [ImageCache] where we can override
/// the logic.
class MyImageCache extends ImageCache {
  @override
  void clear() {
    print('Clearing cache!');
    super.clear();
  }
}

class MyWidgetsBinding extends WidgetsFlutterBinding {
  @override
  ImageCache createImageCache() => MyImageCache();
}

void main() {
  // The constructor sets global variables.
  MyWidgetsBinding();
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

{@end-tool}

### maximumSize

```dart
int get maximumSize
```

Maximum number of entries to store in the cache.

Once this many entries have been cached, the least-recently-used entry is evicted when adding a new entry.

### maximumSize

```dart
set maximumSize(int value)
```

Changes the maximum cache size.

If the new size is smaller than the current number of elements, the extraneous elements are evicted immediately. Setting this to zero and then returning it to its original value will therefore immediately clear the cache.

### currentSize

```dart
int get currentSize
```

The current number of cached entries.

### maximumSizeBytes

```dart
int get maximumSizeBytes
```

Maximum size of entries to store in the cache in bytes.

Once more than this amount of bytes have been cached, the least-recently-used entry is evicted until there are fewer than the maximum bytes.

### maximumSizeBytes

```dart
set maximumSizeBytes(int value)
```

Changes the maximum cache bytes.

If the new size is smaller than the current size in bytes, the extraneous elements are evicted immediately. Setting this to zero and then returning it to its original value will therefore immediately clear the cache.

### currentSizeBytes

```dart
int get currentSizeBytes
```

The current size of cached entries in bytes.

### clear()

```dart
void clear()
```

Evicts all pending and keepAlive entries from the cache.

This is useful if, for instance, the root asset bundle has been updated and therefore new images must be obtained.

Images which have not finished loading yet will not be removed from the cache, and when they complete they will be inserted as normal.

This method does not clear live references to images, since clearing those would not reduce memory pressure. Such images still have listeners in the application code, and will still remain resident in memory.

To clear live references, use [clearLiveImages].

### evict()

```dart
bool evict(Object key, {bool includeLive = true})
```

Evicts a single entry from the cache, returning true if successful.

Pending images waiting for completion are removed as well, returning true if successful. When a pending image is removed the listener on it is removed as well to prevent it from adding itself to the cache if it eventually completes.

If this method removes a pending image, it will also remove the corresponding live tracking of the image, since it is no longer clear if the image will ever complete or have any listeners, and failing to remove the live reference could leave the cache in a state where all subsequent calls to [putIfAbsent] will return an [ImageStreamCompleter] that will never complete.

If this method removes a completed image, it will _not_ remove the live reference to the image, which will only be cleared when the listener count on the completer drops to zero. To clear live image references, whether completed or not, use [clearLiveImages].

The `key` must be equal to an object used to cache an image in [ImageCache.putIfAbsent].

If the key is not immediately available, as is common, consider using [ImageProvider.evict] to call this method indirectly instead.

The `includeLive` argument determines whether images that still have listeners in the tree should be evicted as well. This parameter should be set to true in cases where the image may be corrupted and needs to be completely discarded by the cache. It should be set to false when calls to evict are trying to relieve memory pressure, since an image with a listener will not actually be evicted from memory, and subsequent attempts to load it will end up allocating more memory for the image again.

See also:

- [ImageProvider], for providing images to the [Image] widget.

### putIfAbsent()

```dart
ImageStreamCompleter? putIfAbsent(Object key, ImageStreamCompleter Function() loader, {ImageErrorListener? onError})
```

Returns the previously cached [ImageStream] for the given key, if available; if not, calls the given callback to obtain it first. In either case, the key is moved to the 'most recently used' position.

In the event that the loader throws an exception, it will be caught only if `onError` is also provided. When an exception is caught resolving an image, no completers are cached and `null` is returned instead of a new completer.

Images that are larger than [maximumSizeBytes] are not cached, and do not cause other images in the cache to be evicted.

### statusForKey()

```dart
ImageCacheStatus statusForKey(Object key)
```

The [ImageCacheStatus] information for the given `key`.

### containsKey()

```dart
bool containsKey(Object key)
```

Returns whether this `key` has been previously added by [putIfAbsent].

### liveImageCount

```dart
int get liveImageCount
```

The number of live images being held by the [ImageCache].

Compare with [ImageCache.currentSize] for keepAlive images.

### pendingImageCount

```dart
int get pendingImageCount
```

The number of images being tracked as pending in the [ImageCache].

Compare with [ImageCache.currentSize] for keepAlive images.

### clearLiveImages()

```dart
void clearLiveImages()
```

Clears any live references to images in this cache.

An image is considered live if its [ImageStreamCompleter] has never hit zero listeners after adding at least one listener. The [ImageStreamCompleter.addOnLastListenerRemovedCallback] is used to determine when this has happened.

This is called after a hot reload to evict any stale references to image data for assets that have changed. Calling this method does not relieve memory pressure, since the live image caching only tracks image instances that are also being held by at least one other object.

# ImageCacheStatus

```dart
class ImageCacheStatus {}
```

Information about how the [ImageCache] is tracking an image.

A [pending] image is one that has not completed yet. It may also be tracked as [live] because something is listening to it.

A [keepAlive] image is being held in the cache, which uses Least Recently Used semantics to determine when to evict an image. These images are subject to eviction based on [ImageCache.maximumSizeBytes] and [ImageCache.maximumSize]. It may be [live], but not [pending].

A [live] image is being held until its [ImageStreamCompleter] has no more listeners. It may also be [pending] or [keepAlive].

An [untracked] image is not being cached.

To obtain an [ImageCacheStatus], use [ImageCache.statusForKey] or [ImageProvider.obtainCacheStatus].

### pending

```dart
bool pending
```

An image that has been submitted to [ImageCache.putIfAbsent], but not yet completed.

### keepAlive

```dart
bool keepAlive
```

An image that has been submitted to [ImageCache.putIfAbsent], has completed, fits based on the sizing rules of the cache, and has not been evicted.

Such images will be kept alive even if [live] is false, as long as they have not been evicted from the cache based on its sizing rules.

### live

```dart
bool live
```

An image that has been submitted to [ImageCache.putIfAbsent] and has at least one listener on its [ImageStreamCompleter].

Such images may also be [keepAlive] if they fit in the cache based on its sizing rules. They may also be [pending] if they have not yet resolved.

### tracked

```dart
bool get tracked
```

An image that is tracked in some way by the [ImageCache], whether [pending], [keepAlive], or [live].

### untracked

```dart
bool get untracked
```

An image that either has not been submitted to [ImageCache.putIfAbsent] or has otherwise been evicted from the [keepAlive] and [live] caches.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```
