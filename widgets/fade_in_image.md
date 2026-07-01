# FadeInImage

```dart
class FadeInImage extends StatefulWidget {}
```

An image that shows a [placeholder] image while the target [image] is loading, then fades in the new image when it loads.

Use this class to display long-loading images, such as [NetworkImage.new], so that the image appears on screen with a graceful animation rather than abruptly popping onto the screen.

{@youtube 560 315 https://www.youtube.com/watch?v=pK738Pg9cxc}

If the [image] emits an [ImageInfo] synchronously, such as when the image has been loaded and cached, the [image] is displayed immediately, and the [placeholder] is never displayed.

The [fadeOutDuration] and [fadeOutCurve] properties control the fade-out animation of the [placeholder].

The [fadeInDuration] and [fadeInCurve] properties control the fade-in animation of the target [image].

Prefer a [placeholder] that's already cached so that it is displayed immediately. This prevents it from popping onto the screen.

When [image] changes, it is resolved to a new [ImageStream]. If the new [ImageStream.key] is different, this widget subscribes to the new stream and replaces the displayed image with images emitted by the new stream.

When [placeholder] changes and the [image] has not yet emitted an [ImageInfo], then [placeholder] is resolved to a new [ImageStream]. If the new [ImageStream.key] is different, this widget subscribes to the new stream and replaces the displayed image to images emitted by the new stream.

When either [placeholder] or [image] changes, this widget continues showing the previously loaded image (if any) until the new image provider provides a different image. This is known as "gapless playback" (see also [Image.gaplessPlayback]).

{@tool snippet}

```dart
FadeInImage(
  // here `bytes` is a Uint8List containing the bytes for the in-memory image
  placeholder: MemoryImage(bytes),
  image: const NetworkImage('https://backend.example.com/image.png'),
)
```

{@end-tool}

### FadeInImage()

```dart
FadeInImage({dynamic key, required ImageProvider placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required ImageProvider image, ImageErrorWidgetBuilder? imageErrorBuilder, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, double? width, double? height, BoxFit? fit, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false})
```

Creates a widget that displays a [placeholder] while an [image] is loading, then fades-out the placeholder and fades-in the image.

The [placeholder] and [image] may be composed in a [ResizeImage] to provide a custom decode/cache size.

The [placeholder] and [image] may have their own BoxFit settings via [fit] and [placeholderFit].

The [placeholder] and [image] may have their own FilterQuality settings via [filterQuality] and [placeholderFilterQuality].

If [excludeFromSemantics] is true, then [imageSemanticLabel] will be ignored.

### FadeInImage.memoryNetwork()

```dart
FadeInImage.memoryNetwork({dynamic key, required Uint8List placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required String image, ImageErrorWidgetBuilder? imageErrorBuilder, double placeholderScale = 1.0, double imageScale = 1.0, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, double? width, double? height, BoxFit? fit, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false, int? placeholderCacheWidth, int? placeholderCacheHeight, int? imageCacheWidth, int? imageCacheHeight})
```

Creates a widget that uses a placeholder image stored in memory while loading the final image from the network.

The `placeholder` argument contains the bytes of the in-memory image.

The `image` argument is the URL of the final image.

The `placeholderScale` and `imageScale` arguments are passed to their respective [ImageProvider]s (see also [ImageInfo.scale]).

If [placeholderCacheWidth], [placeholderCacheHeight], [imageCacheWidth], or [imageCacheHeight] are provided, it indicates to the engine that the respective image should be decoded at the specified size. The image will be rendered to the constraints of the layout or [width] and [height] regardless of these parameters. These parameters are primarily intended to reduce the memory usage of [ImageCache].

The [placeholder], [image], [placeholderScale], [imageScale], [fadeOutDuration], [fadeOutCurve], [fadeInDuration], [fadeInCurve], [alignment], [repeat], and [matchTextDirection] arguments must not be null.

See also:

- [Image.memory], which has more details about loading images from memory.
- [Image.network], which has more details about loading images from the network.

### FadeInImage.assetNetwork()

```dart
FadeInImage.assetNetwork({dynamic key, required String placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required String image, ImageErrorWidgetBuilder? imageErrorBuilder, AssetBundle? bundle, double? placeholderScale, double imageScale = 1.0, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, double? width, double? height, BoxFit? fit, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false, int? placeholderCacheWidth, int? placeholderCacheHeight, int? imageCacheWidth, int? imageCacheHeight})
```

Creates a widget that uses a placeholder image stored in an asset bundle while loading the final image from the network.

The `placeholder` argument is the key of the image in the asset bundle.

The `image` argument is the URL of the final image.

The `placeholderScale` and `imageScale` arguments are passed to their respective [ImageProvider]s (see also [ImageInfo.scale]).

If `placeholderScale` is omitted or is null, pixel-density-aware asset resolution will be attempted for the [placeholder] image. Otherwise, the exact asset specified will be used.

If [placeholderCacheWidth], [placeholderCacheHeight], [imageCacheWidth], or [imageCacheHeight] are provided, it indicates to the engine that the respective image should be decoded at the specified size. The image will be rendered to the constraints of the layout or [width] and [height] regardless of these parameters. These parameters are primarily intended to reduce the memory usage of [ImageCache].

See also:

- [Image.asset], which has more details about loading images from asset bundles.
- [Image.network], which has more details about loading images from the network.

### placeholder

```dart
ImageProvider placeholder
```

Image displayed while the target [image] is loading.

### placeholderErrorBuilder

```dart
ImageErrorWidgetBuilder? placeholderErrorBuilder
```

A builder function that is called if an error occurs during placeholder image loading.

If this builder is not provided, any exceptions will be reported to [FlutterError.onError]. If it is provided, the caller should either handle the exception by providing a replacement widget, or rethrow the exception.

### image

```dart
ImageProvider image
```

The target image that is displayed once it has loaded.

### imageErrorBuilder

```dart
ImageErrorWidgetBuilder? imageErrorBuilder
```

A builder function that is called if an error occurs during image loading.

If this builder is not provided, any exceptions will be reported to [FlutterError.onError]. If it is provided, the caller should either handle the exception by providing a replacement widget, or rethrow the exception.

### fadeOutDuration

```dart
Duration fadeOutDuration
```

The duration of the fade-out animation for the [placeholder].

### fadeOutCurve

```dart
Curve fadeOutCurve
```

The curve of the fade-out animation for the [placeholder].

### fadeInDuration

```dart
Duration fadeInDuration
```

The duration of the fade-in animation for the [image].

### fadeInCurve

```dart
Curve fadeInCurve
```

The curve of the fade-in animation for the [image].

### width

```dart
double? width
```

If non-null, require the image to have this width.

If null, the image will pick a size that best preserves its intrinsic aspect ratio. This may result in a sudden change if the size of the placeholder image does not match that of the target image. The size is also affected by the scale factor.

### color

```dart
Color? color
```

If non-null, this color is blended with each image pixel using [colorBlendMode].

Color applies to the [image].

See Also:

- [placeholderColor], the color which applies to the [placeholder].

### colorBlendMode

```dart
BlendMode? colorBlendMode
```

Used to combine [color] with this [image].

The default is [BlendMode.srcIn]. In terms of the blend mode, [color] is the source and this image is the destination.

See also:

- [BlendMode], which includes an illustration of the effect of each blend mode.
- [placeholderColorBlendMode], the color blend mode which applies to the [placeholder].

### placeholderColor

```dart
Color? placeholderColor
```

If non-null, this color is blended with each placeholder image pixel using [placeholderColorBlendMode].

Color applies to the [placeholder].

See Also:

- [color], the color which applies to the [image].

### placeholderColorBlendMode

```dart
BlendMode? placeholderColorBlendMode
```

Used to combine [placeholderColor] with the [placeholder] image.

The default is [BlendMode.srcIn]. In terms of the blend mode, [placeholderColor] is the source and this placeholder is the destination.

See also:

- [BlendMode], which includes an illustration of the effect of each blend mode.
- [colorBlendMode], the color blend mode which applies to the [image].

### height

```dart
double? height
```

If non-null, require the image to have this height.

If null, the image will pick a size that best preserves its intrinsic aspect ratio. This may result in a sudden change if the size of the placeholder image does not match that of the target image. The size is also affected by the scale factor.

### fit

```dart
BoxFit? fit
```

How to inscribe the image into the space allocated during layout.

The default varies based on the other fields. See the discussion at [paintImage].

### placeholderFit

```dart
BoxFit? placeholderFit
```

How to inscribe the placeholder image into the space allocated during layout.

If not value set, it will fallback to [fit].

### filterQuality

```dart
FilterQuality filterQuality
```

The rendering quality of the image.

{@macro flutter.widgets.image.filterQuality}

### placeholderFilterQuality

```dart
FilterQuality? placeholderFilterQuality
```

The rendering quality of the placeholder image.

{@macro flutter.widgets.image.filterQuality}

### alignment

```dart
AlignmentGeometry alignment
```

How to align the image within its bounds.

The alignment aligns the given position in the image to the given position in the layout bounds. For example, an [Alignment] alignment of (-1.0, -1.0) aligns the image to the top-left corner of its layout bounds, while an [Alignment] alignment of (1.0, 1.0) aligns the bottom right of the image with the bottom right corner of its layout bounds. Similarly, an alignment of (0.0, 1.0) aligns the bottom middle of the image with the middle of the bottom edge of its layout bounds.

If the [alignment] is [TextDirection]-dependent (i.e. if it is a [AlignmentDirectional]), then an ambient [Directionality] widget must be in scope.

Defaults to [Alignment.center].

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### repeat

```dart
ImageRepeat repeat
```

How to paint any portions of the layout bounds not covered by the image.

### matchTextDirection

```dart
bool matchTextDirection
```

Whether to paint the image in the direction of the [TextDirection].

If this is true, then in [TextDirection.ltr] contexts, the image will be drawn with its origin in the top left (the "normal" painting direction for images); and in [TextDirection.rtl] contexts, the image will be drawn with a scaling factor of -1 in the horizontal direction so that the origin is in the top right.

This is occasionally used with images in right-to-left environments, for images that were designed for left-to-right locales. Be careful, when using this, to not flip images with integral shadows, text, or other effects that will look incorrect when flipped.

If this is true, there must be an ambient [Directionality] widget in scope.

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

Whether to exclude this image from semantics.

This is useful for images which do not contribute meaningful information to an application.

### imageSemanticLabel

```dart
String? imageSemanticLabel
```

A semantic description of the [image].

Used to provide a description of the [image] to TalkBack on Android, and VoiceOver on iOS.

This description will be used both while the [placeholder] is shown and once the image has loaded.

### createState()

```dart
State<FadeInImage> createState()
```
