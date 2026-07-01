@docImport 'dart:ui';

# ScrollAwareImageProvider

```dart
class ScrollAwareImageProvider<T extends Object> extends ImageProvider<T> {}
```

An [ImageProvider] that makes use of [Scrollable.recommendDeferredLoadingForContext] to avoid loading images when rapidly scrolling.

This provider assumes that its wrapped [imageProvider] correctly uses the [ImageCache], and does not attempt to re-acquire or decode images in the cache.

Calling [resolve] on this provider will cause it to obtain the image key and then check the following:

1.  If the returned [ImageStream] has been completed, end. This can happen if the caller sets the completer on the stream.
2.  If the [ImageCache] has a completer for the key for this image, ask the wrapped provider to resolve. This can happen if the image was precached, or another [ImageProvider] already resolved the same image.
3.  If the [context] has been disposed, end. This can happen if the caller has been disposed and is no longer interested in resolving the image.
4.  If the widget is scrolling with high velocity at this point in time, wait until the beginning of the next frame and go back to step 1.
5.  Delegate loading the image to the wrapped provider and finish.

If the cycle ends at steps 1 or 3, the [ImageStream] will never be marked as complete and listeners will not be notified.

The [Image] widget wraps its incoming providers with this provider to avoid overutilization of resources for images that would never appear on screen or only be visible for a very brief period.

### ScrollAwareImageProvider()

```dart
ScrollAwareImageProvider({required DisposableBuildContext context, required ImageProvider<T> imageProvider})
```

Creates a [ScrollAwareImageProvider].

The [context] object is the [BuildContext] of the [State] using this provider. It is used to determine scrolling velocity during [resolve].

The [imageProvider] is used to create a key and load the image. It must not be null, and is assumed to interact with the cache in the normal way that [ImageProvider.resolveStreamForKey] does.

### context

```dart
DisposableBuildContext context
```

The context that may or may not be enclosed by a [Scrollable].

Once [DisposableBuildContext.dispose] is called on this context, the provider will stop trying to resolve the image if it has not already been resolved.

### imageProvider

```dart
ImageProvider<T> imageProvider
```

The wrapped image provider to delegate [obtainKey] and [loadImage] to.

### resolveStreamForKey()

```dart
void resolveStreamForKey(ImageConfiguration configuration, ImageStream stream, T key, ImageErrorListener handleError)
```

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(T key, DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(T key, ImageDecoderCallback decode)
```

### obtainKey()

```dart
Future<T> obtainKey(ImageConfiguration configuration)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
