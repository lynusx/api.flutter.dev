@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_driver/driver_extension.dart';

# PaintingBinding

```dart
mixin PaintingBinding on BindingBase, ServicesBinding {}
```

Binding for the painting library.

Hooks into the cache eviction logic to clear the image cache.

Requires the [ServicesBinding] to be mixed in earlier.

### initInstances()

```dart
void initInstances()
```

### instance

```dart
PaintingBinding get instance
```

The current [PaintingBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### shaderWarmUp

```dart
ShaderWarmUp? shaderWarmUp
```

[ShaderWarmUp] instance to be executed during [initInstances].

Defaults to `null`, meaning no shader warm-up is done. Some platforms may not support shader warm-up before at least one frame has been displayed.

If the application has scenes that require the compilation of complex shaders, it may cause jank in the middle of an animation or interaction. In that case, setting [shaderWarmUp] to a custom [ShaderWarmUp] before creating the binding (usually before [runApp] for normal Flutter apps, and before [enableFlutterDriverExtension] for Flutter driver tests) may help if that object paints the difficult scene in its [ShaderWarmUp.warmUpOnCanvas] method, as this allows Flutter to pre-compile and cache the required shaders during startup.

Currently the warm-up happens synchronously on the raster thread which means the rendering of the first frame on the raster thread will be postponed until the warm-up is finished.

The warm up is only costly (100ms-200ms, depending on the shaders to compile) during the first run after the installation or a data wipe. The warm up does not block the platform thread so there should be no "Application Not Responding" warning.

If this is null, no shader warm-up is executed.

See also:

- [ShaderWarmUp], the interface for implementing custom warm-up scenes.
- <https://docs.flutter.dev/perf/shader>

### imageCache

```dart
ImageCache get imageCache
```

The singleton that implements the Flutter framework's image cache.

The cache is used internally by [ImageProvider] and should generally not be accessed directly.

The image cache is created during startup by the [createImageCache] method.

### createImageCache()

```dart
ImageCache createImageCache()
```

Creates the [ImageCache] singleton (accessible via [imageCache]).

This method can be overridden to provide a custom image cache.

### instantiateImageCodecFromBuffer()

```dart
Future<ui.Codec> instantiateImageCodecFromBuffer(ui.ImmutableBuffer buffer, {int? cacheWidth, int? cacheHeight, bool allowUpscaling = false})
```

Calls through to [dart:ui.instantiateImageCodecFromBuffer] from [ImageCache].

The [buffer] parameter should be an [ui.ImmutableBuffer] instance which can be acquired from [ui.ImmutableBuffer.fromUint8List] or [ui.ImmutableBuffer.fromAsset].

The [cacheWidth] and [cacheHeight] parameters, when specified, indicate the size to decode the image to.

Both [cacheWidth] and [cacheHeight] must be positive values greater than or equal to 1, or null. It is valid to specify only one of `cacheWidth` and [cacheHeight] with the other remaining null, in which case the omitted dimension will be scaled to maintain the aspect ratio of the original dimensions. When both are null or omitted, the image will be decoded at its native resolution.

The [allowUpscaling] parameter determines whether the `cacheWidth` or [cacheHeight] parameters are clamped to the intrinsic width and height of the original image. By default, the dimensions are clamped to avoid unnecessary memory usage for images. Callers that wish to display an image above its native resolution should prefer scaling the canvas the image is drawn into.

### instantiateImageCodecWithSize()

```dart
Future<ui.Codec> instantiateImageCodecWithSize(ui.ImmutableBuffer buffer, {ui.TargetImageSizeCallback? getTargetSize})
```

Calls through to [dart:ui.instantiateImageCodecWithSize] from [ImageCache].

The [buffer] parameter should be an [ui.ImmutableBuffer] instance which can be acquired from [ui.ImmutableBuffer.fromUint8List] or [ui.ImmutableBuffer.fromAsset].

The [getTargetSize] parameter, when specified, will be invoked and passed the image's intrinsic size to determine the size to decode the image to. The width and the height of the size it returns must be positive values greater than or equal to 1, or null. It is valid to return a [TargetImageSize] that specifies only one of `width` and `height` with the other remaining null, in which case the omitted dimension will be scaled to maintain the aspect ratio of the original dimensions. When both are null or omitted, the image will be decoded at its native resolution (as will be the case if the [getTargetSize] parameter is omitted).

### evict()

```dart
void evict(String asset)
```

### handleMemoryPressure()

```dart
void handleMemoryPressure()
```

### systemFonts

```dart
Listenable get systemFonts
```

Listenable that notifies when the available fonts on the system have changed.

System fonts can change when the system installs or removes new font. To correctly reflect the change, it is important to relayout text related widgets when this happens.

Objects that show text and/or measure text (e.g. via [TextPainter] or [Paragraph]) should listen to this and redraw/remeasure.

### handleSystemMessage()

```dart
Future<void> handleSystemMessage(Object systemMessage)
```

# imageCache

```dart
ImageCache get imageCache
```

The singleton that implements the Flutter framework's image cache.

The cache is used internally by [ImageProvider] and should generally not be accessed directly.

The image cache is created during startup by the [PaintingBinding]'s [PaintingBinding.createImageCache] method.
