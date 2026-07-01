@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart';

@docImport 'image_cache.dart'; @docImport 'image_provider.dart';

# ImageInfo

```dart
class ImageInfo {}
```

A [dart:ui.Image] object with its corresponding scale.

ImageInfo objects are used by [ImageStream] objects to represent the actual data of the image once it has been obtained.

The disposing contract for [ImageInfo] (as well as for [ui.Image]) is different from traditional one, where an object should dispose a member if the object created the member. Instead, the disposal contract is as follows:

- [ImageInfo] disposes [image], even if it is received as a constructor argument.
- [ImageInfo] is expected to be disposed not by the object, that created it, but by the object that owns reference to it.
- It is expected that only one object owns reference to [ImageInfo] object.

Safety tips:

- To share the [ImageInfo] or [ui.Image] between objects, use the [clone] method, which will not clone the entire underlying image, but only reference to it and information about it.
- After passing a [ui.Image] or [ImageInfo] reference to another object, release the reference.

### ImageInfo()

```dart
ImageInfo({required ui.Image image, double scale = 1.0, String? debugLabel})
```

Creates an [ImageInfo] object for the given [image] and [scale].

The [debugLabel] may be used to identify the source of this image.

See details for disposing contract in the class description.

### clone()

```dart
ImageInfo clone()
```

Creates an [ImageInfo] with a cloned [image].

This method must be used in cases where a client holding an [ImageInfo] needs to share the image info object with another client and will still need to access the underlying image data at some later point, e.g. to share it again with another client.

See details for disposing contract in the class description.

See also:

- [ui.Image.clone], which describes how and why to clone images.

### isCloneOf()

```dart
bool isCloneOf(ImageInfo other)
```

Whether this [ImageInfo] is a [clone] of the `other`.

This method is a convenience wrapper for [ui.Image.isCloneOf], and is useful for clients that are trying to determine whether new layout or painting logic is required when receiving a new image reference.

{@tool snippet}

The following sample shows how to appropriately check whether the [ImageInfo] reference refers to new image data or not (in this case in a setter).

```dart
ImageInfo? get imageInfo => _imageInfo;
ImageInfo? _imageInfo;
set imageInfo (ImageInfo? value) {
  // If the image reference is exactly the same, do nothing.
  if (value == _imageInfo) {
    return;
  }
  // If it is a clone of the current reference, we must dispose of it and
  // can do so immediately. Since the underlying image has not changed,
  // We don't have any additional work to do here.
  if (value != null && _imageInfo != null && value.isCloneOf(_imageInfo!)) {
    value.dispose();
    return;
  }
  // It is a new image. Dispose of the old one and take a reference
  // to the new one.
  _imageInfo?.dispose();
  _imageInfo = value;
  // Perform work to determine size, paint the image, etc.
  // ...
}
```

{@end-tool}

### image

```dart
ui.Image image
```

The raw image pixels.

This is the object to pass to the [Canvas.drawImage], [Canvas.drawImageRect], or [Canvas.drawImageNine] methods when painting the image.

### sizeBytes

```dart
int get sizeBytes
```

The size of raw image pixels in bytes.

### scale

```dart
double scale
```

The linear scale factor for drawing this image at its intended size.

The scale factor applies to the width and the height.

{@template flutter.painting.imageInfo.scale} For example, if this is 2.0, it means that there are four image pixels for every one logical pixel, and the image's actual width and height (as given by the [dart:ui.Image.width] and [dart:ui.Image.height] properties) are double the height and width that should be used when painting the image (e.g. in the arguments given to [Canvas.drawImage]). {@endtemplate}

### debugLabel

```dart
String? debugLabel
```

A string used for debugging purposes to identify the source of this image.

### dispose()

```dart
void dispose()
```

Disposes of this object.

Once this method has been called, the object should not be used anymore, and no clones of it or the image it contains can be made.

### toString()

```dart
String toString()
```

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

# ImageStreamListener

```dart
class ImageStreamListener {}
```

Interface for receiving notifications about the loading of an image.

This class overrides [operator ==] and [hashCode] to compare the individual callbacks in the listener, meaning that if you add an instance of this class as a listener (e.g. via [ImageStream.addListener]), you can instantiate a _different_ instance of this class when you remove the listener, and the listener will be properly removed as long as all associated callbacks are equal.

Used by [ImageStream] and [ImageStreamCompleter].

### ImageStreamListener()

```dart
ImageStreamListener(ImageListener onImage, {ImageChunkListener? onChunk, ImageErrorListener? onError, bool reportErrors = true})
```

Creates a new [ImageStreamListener].

### onImage

```dart
ImageListener onImage
```

Callback for getting notified that an image is available.

This callback may fire multiple times (e.g. if the [ImageStreamCompleter] that drives the notifications fires multiple times). An example of such a case would be an image with multiple frames within it (such as an animated GIF).

For more information on how to interpret the parameters to the callback, see the documentation on [ImageListener].

See also:

- [onError], which will be called instead of [onImage] if an error occurs during loading.

### onChunk

```dart
ImageChunkListener? onChunk
```

Callback for getting notified when a chunk of bytes has been received during the loading of the image.

This callback may fire many times (e.g. when used with a [NetworkImage], where the image bytes are loaded incrementally over the wire) or not at all (e.g. when used with a [MemoryImage], where the image bytes are already available in memory).

This callback may also continue to fire after the [onImage] callback has fired (e.g. for multi-frame images that continue to load after the first frame is available).

### onError

```dart
ImageErrorListener? onError
```

Callback for getting notified when an error occurs while loading an image.

If an error occurs during loading, [onError] will be called instead of [onImage].

If [onError] is called and does not throw, then the error is considered to be handled. An error handler can explicitly rethrow the exception reported to it to safely indicate that it did not handle the exception.

If an image stream has no listeners that handled the error when the error was first encountered, then the error is reported using [FlutterError.reportError], with the [FlutterErrorDetails.silent] flag set to true. This report is suppressed if a listener whose [reportErrors] is false has ever been registered on the completer.

### reportErrors

```dart
bool reportErrors
```

Whether to report errors to [FlutterError.onError] after this listener is removed from the [ImageStreamCompleter].

Defaults to true. When false, errors that arrive after removal are silently discarded. This is useful when [FlutterError.onError] is configured to report errors to a server.

The [Image] widget sets this to false when an [Image.errorBuilder] is provided.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

# ImageListener

```dart
typedef ImageListener = void Function(ImageInfo image, bool synchronousCall)
```

Signature for callbacks reporting that an image is available.

Used in [ImageStreamListener].

The `image` argument contains information about the image to be rendered. The implementer of [ImageStreamListener.onImage] is expected to call dispose on the [ui.Image] it receives.

The `synchronousCall` argument is true if the listener is being invoked during the call to `addListener`. This can be useful if, for example, [ImageStream.addListener] is invoked during a frame, so that a new rendering frame is requested if the call was asynchronous (after the current frame) and no rendering frame is requested if the call was synchronous (within the same stack frame as the call to [ImageStream.addListener]).

# ImageChunkListener

```dart
typedef ImageChunkListener = void Function(ImageChunkEvent event)
```

Signature for listening to [ImageChunkEvent] events.

Used in [ImageStreamListener].

# ImageErrorListener

```dart
typedef ImageErrorListener = void Function(Object exception, StackTrace? stackTrace)
```

Signature for reporting errors when resolving images.

Used in [ImageStreamListener], as well as by [ImageCache.putIfAbsent] and [precacheImage], to report errors.

# ImageChunkEvent

```dart
class ImageChunkEvent with Diagnosticable {}
```

An immutable notification of image bytes that have been incrementally loaded.

Chunk events represent progress notifications while an image is being loaded (e.g. from disk or over the network).

See also:

- [ImageChunkListener], the means by which callers get notified of these events.

### ImageChunkEvent()

```dart
ImageChunkEvent({required int cumulativeBytesLoaded, required int? expectedTotalBytes})
```

Creates a new chunk event.

### cumulativeBytesLoaded

```dart
int cumulativeBytesLoaded
```

The number of bytes that have been received across the wire thus far.

### expectedTotalBytes

```dart
int? expectedTotalBytes
```

The expected number of bytes that need to be received to finish loading the image.

This value is not necessarily equal to the expected _size_ of the image in bytes, as the bytes required to load the image may be compressed.

This value will be null if the number is not known in advance.

When this value is null, the chunk event may still be useful as an indication that data is loading (and how much), but it cannot represent a loading completion percentage.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ImageStream

```dart
class ImageStream with Diagnosticable {}
```

A handle to an image resource.

ImageStream represents a handle to a [dart:ui.Image] object and its scale (together represented by an [ImageInfo] object). The underlying image object might change over time, either because the image is animating or because the underlying image resource was mutated.

ImageStream objects can also represent an image that hasn't finished loading.

ImageStream objects are backed by [ImageStreamCompleter] objects.

The [ImageCache] will consider an image to be live until the listener count drops to zero after adding at least one listener. The [ImageStreamCompleter.addOnLastListenerRemovedCallback] method is used for tracking this information.

See also:

- [ImageProvider], which has an example that includes the use of an [ImageStream] in a [Widget].

### ImageStream()

```dart
ImageStream()
```

Create an initially unbound image stream.

Once an [ImageStreamCompleter] is available, call [setCompleter].

### completer

```dart
ImageStreamCompleter? get completer
```

The completer that has been assigned to this image stream.

Generally there is no need to deal with the completer directly.

### setCompleter()

```dart
void setCompleter(ImageStreamCompleter value)
```

Assigns a particular [ImageStreamCompleter] to this [ImageStream].

This is usually done automatically by the [ImageProvider] that created the [ImageStream].

This method can only be called once per stream. To have an [ImageStream] represent multiple images over time, assign it a completer that completes several images in succession.

### addListener()

```dart
void addListener(ImageStreamListener listener)
```

Adds a listener callback that is called whenever a new concrete [ImageInfo] object is available. If a concrete image is already available, this object will call the listener synchronously.

If the assigned [completer] completes multiple images over its lifetime, this listener will fire multiple times.

{@template flutter.painting.imageStream.addListener} The listener will be passed a flag indicating whether a synchronous call occurred. If the listener is added within a render object paint function, then use this flag to avoid calling [RenderObject.markNeedsPaint] during a paint.

If a duplicate `listener` is registered N times, then it will be called N times when the image stream completes (whether because a new image is available or because an error occurs). Likewise, to remove all instances of the listener, [removeListener] would need to called N times as well.

When a `listener` receives an [ImageInfo] object, the `listener` is responsible for disposing of the [ImageInfo.image]. {@endtemplate}

### removeListener()

```dart
void removeListener(ImageStreamListener listener)
```

Stops listening for events from this stream's [ImageStreamCompleter].

If [listener] has been added multiple times, this removes the _first_ instance of the listener.

### key

```dart
Object get key
```

Returns an object which can be used with `==` to determine if this [ImageStream] shares the same listeners list as another [ImageStream].

This can be used to avoid un-registering and re-registering listeners after calling [ImageProvider.resolve] on a new, but possibly equivalent, [ImageProvider].

The key may change once in the lifetime of the object. When it changes, it will go from being different than other [ImageStream]'s keys to potentially being the same as others'. No notification is sent when this happens.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ImageStreamCompleterHandle

```dart
class ImageStreamCompleterHandle {}
```

An opaque handle that keeps an [ImageStreamCompleter] alive even if it has lost its last listener.

To create a handle, use [ImageStreamCompleter.keepAlive].

Such handles are useful when an image cache needs to keep a completer alive but does not actually have a listener subscribed, or when a widget that displays an image needs to temporarily unsubscribe from the completer but may re-subscribe in the future, for example when the [TickerMode] changes.

### dispose()

```dart
void dispose()
```

Call this method to signal the [ImageStreamCompleter] that it can now be disposed when its last listener drops.

This method must only be called once per object.

# ImageStreamCompleter

```dart
abstract class ImageStreamCompleter with Diagnosticable {}
```

Base class for those that manage the loading of [dart:ui.Image] objects for [ImageStream]s.

[ImageStreamListener] objects are rarely constructed directly. Generally, an [ImageProvider] subclass will return an [ImageStream] and automatically configure it with the right [ImageStreamCompleter] when possible.

### debugLabel

```dart
String? debugLabel
```

A string identifying the source of the underlying image.

### hasListeners

```dart
bool get hasListeners
```

Whether any listeners are currently registered.

Clients should not depend on this value for their behavior, because having one listener's logic change when another listener happens to start or stop listening will lead to extremely hard-to-track bugs. Subclasses might use this information to determine whether to do any work when there are no listeners, however; for example, [MultiFrameImageStreamCompleter] uses it to determine when to iterate through frames of an animated image.

Typically this is used by overriding [addListener], checking if [hasListeners] is false before calling `super.addListener()`, and if so, starting whatever work is needed to determine when to notify listeners; and similarly, by overriding [removeListener], checking if [hasListeners] is false after calling `super.removeListener()`, and if so, stopping that same work.

The ephemeral error listeners (added through [addEphemeralErrorListener]) will not be taken into consideration in this property.

### addListener()

```dart
void addListener(ImageStreamListener listener)
```

Adds a listener callback that is called whenever a new concrete [ImageInfo] object is available or an error is reported. If a concrete image is already available, or if an error has been already reported, this object will notify the listener synchronously.

If the [ImageStreamCompleter] completes multiple images over its lifetime, this listener's [ImageStreamListener.onImage] will fire multiple times.

{@macro flutter.painting.imageStream.addListener}

See also:

- [addEphemeralErrorListener], which adds an error listener that is automatically removed after first image load or error.

### addEphemeralErrorListener()

```dart
void addEphemeralErrorListener(ImageErrorListener listener)
```

Adds an error listener callback that is called when the first error is reported.

The callback will be removed automatically after the first successful image load or the first error - that is why it is called "ephemeral".

If a concrete image is already available, the listener will be discarded synchronously. If an error has been already reported, the listener will be notified synchronously.

The presence of a listener will affect neither the lifecycle of this object nor what [hasListeners] reports.

It is different from [addListener] in a few points: Firstly, this one only listens to errors, while [addListener] listens to all kinds of events. Secondly, this listener will be automatically removed according to the rules mentioned above, while [addListener] will need manual removal. Thirdly, this listener will not affect how this object is disposed, while any non-removed listener added via [addListener] will forbid this object from disposal.

When you want to know full information and full control, use [addListener]. When you only want to get notified for an error ephemerally, use this function.

See also:

- [addListener], which adds a full-featured listener and needs manual removal.

### keepAlive()

```dart
ImageStreamCompleterHandle keepAlive()
```

Creates an [ImageStreamCompleterHandle] that will prevent this stream from being disposed at least until the handle is disposed.

Such handles are useful when an image cache needs to keep a completer alive but does not itself have a listener subscribed, or when a widget that displays an image needs to temporarily unsubscribe from the completer but may re-subscribe in the future, for example when the [TickerMode] changes.

### removeListener()

```dart
void removeListener(ImageStreamListener listener)
```

Stops the specified [listener] from receiving image stream events.

If [listener] has been added multiple times, this removes the _first_ instance of the listener.

Once all listeners have been removed and all [keepAlive] handles have been disposed, this image stream is no longer usable.

### onDisposed()

```dart
void onDisposed()
```

Called when this [ImageStreamCompleter] has actually been disposed.

Subclasses should override this if they need to clean up resources when they are disposed.

### maybeDispose()

```dart
void maybeDispose()
```

Disposes this [ImageStreamCompleter] unless:

1.  It is already disposed
2.  It has listeners.
3.  It has active "keep alive" handles.

### addOnLastListenerRemovedCallback()

```dart
void addOnLastListenerRemovedCallback(VoidCallback callback)
```

Adds a callback to call when [removeListener] results in an empty list of listeners and there are no [keepAlive] handles outstanding.

This callback will never fire if [removeListener] is never called.

### removeOnLastListenerRemovedCallback()

```dart
void removeOnLastListenerRemovedCallback(VoidCallback callback)
```

Removes a callback previously supplied to [addOnLastListenerRemovedCallback].

### setImage()

```dart
void setImage(ImageInfo image)
```

Calls all the registered listeners to notify them of a new image.

### reportError()

```dart
void reportError({DiagnosticsNode? context, required Object exception, StackTrace? stack, InformationCollector? informationCollector, bool silent = false})
```

Calls all the registered error listeners to notify them of an error that occurred while resolving the image.

If no error listeners (listeners with an [ImageStreamListener.onError] specified) are attached, or if the handlers all rethrow the exception verbatim (with `throw exception`), a [FlutterError] will be reported using [FlutterError.reportError]. This report is suppressed if [ImageStreamListener] whose [ImageStreamListener.reportErrors] is false has ever been registered on this completer.

The `context` should be a string describing where the error was caught, in a form that will make sense in English when following the word "thrown", as in "thrown while obtaining the image from the network" (for the context "while obtaining the image from the network").

The `exception` is the error being reported; the `stack` is the [StackTrace] associated with the exception.

The `informationCollector` is a callback (of type [InformationCollector]) that is called when the exception is used by [FlutterError.reportError]. It is used to obtain further details to include in the logs, which may be expensive to collect, and thus should only be collected if the error is to be logged in the first place.

The `silent` argument causes the exception to not be reported to the logs in release builds, if passed to [FlutterError.reportError]. (It is still sent to error handlers.) It should be set to true if the error is one that is expected to be encountered in release builds, for example network errors. That way, logs on end-user devices will not have spurious messages, but errors during development will still be reported.

See [FlutterErrorDetails] for further details on these values.

### reportImageChunkEvent()

```dart
void reportImageChunkEvent(ImageChunkEvent event)
```

Calls all the registered [ImageChunkListener]s (listeners with an [ImageStreamListener.onChunk] specified) to notify them of a new [ImageChunkEvent].

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder description)
```

Accumulates a list of strings describing the object's state. Subclasses should override this to have their information included in [toString].

# OneFrameImageStreamCompleter

```dart
class OneFrameImageStreamCompleter extends ImageStreamCompleter {}
```

Manages the loading of [dart:ui.Image] objects for static [ImageStream]s (those with only one frame).

### OneFrameImageStreamCompleter()

```dart
OneFrameImageStreamCompleter(Future<ImageInfo> image, {InformationCollector? informationCollector})
```

Creates a manager for one-frame [ImageStream]s.

The image resource awaits the given [Future]. When the future resolves, it notifies the [ImageListener]s that have been registered with [addListener].

The [InformationCollector], if provided, is invoked if the given [Future] resolves with an error, and can be used to supplement the reported error message (for example, giving the image's URL).

Errors are reported using [FlutterError.reportError] with the `silent` argument on [FlutterErrorDetails] set to true, meaning that by default the message is only dumped to the console in debug mode (see [ FlutterErrorDetails]).

# MultiFrameImageStreamCompleter

```dart
class MultiFrameImageStreamCompleter extends ImageStreamCompleter {}
```

Manages the decoding and scheduling of image frames.

New frames will only be emitted while there are registered listeners to the stream (registered with [addListener]).

This class deals with 2 types of frames:

- image frames - image frames of an animated image.
- app frames - frames that the flutter engine is drawing to the screen to show the app GUI.

For single frame images the stream will only complete once.

For animated images, this class eagerly decodes the next image frame, and notifies the listeners that a new frame is ready on the first app frame that is scheduled after the image frame duration has passed.

Scheduling new timers only from scheduled app frames, makes sure we pause the animation when the app is not visible (as new app frames will not be scheduled).

See the following timeline example:

| Time | Event | Comment | |------|--------------------------------------------|---------------------------| | t1 | App frame scheduled (image frame A posted) | | | t2 | App frame scheduled | | | t3 | App frame scheduled | | | t4 | Image frame B decoded | | | t5 | App frame scheduled | t5 - t1 < frameB_duration | | t6 | App frame scheduled (image frame B posted) | t6 - t1 > frameB_duration |

### MultiFrameImageStreamCompleter()

```dart
MultiFrameImageStreamCompleter({required Future<ui.Codec> codec, required double scale, String? debugLabel, Stream<ImageChunkEvent>? chunkEvents, InformationCollector? informationCollector})
```

Creates a image stream completer.

Immediately starts decoding the first image frame when the codec is ready.

The `codec` parameter is a future for an initialized [ui.Codec] that will be used to decode the image. This completer takes ownership of the passed `codec` and will dispose it once it is no longer needed.

The `scale` parameter is the linear scale factor for drawing this frames of this image at their intended size.

The `tag` parameter is passed on to created [ImageInfo] objects to help identify the source of the image.

The `chunkEvents` parameter is an optional stream of notifications about the loading progress of the image. If this stream is provided, the events produced by the stream will be delivered to registered [ImageChunkListener]s (see [addListener]).

### addListener()

```dart
void addListener(ImageStreamListener listener)
```

### removeListener()

```dart
void removeListener(ImageStreamListener listener)
```
