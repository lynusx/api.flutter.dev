@docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'box_decoration.dart'; @docImport 'image_resolution.dart';

# ImageRepeat

```dart
enum ImageRepeat {}
```

How to paint any portions of a box not covered by an image.

Repeat the image in both the x and y directions until the box is filled.

Repeat the image in the x direction until the box is filled horizontally.

Repeat the image in the y direction until the box is filled vertically.

Leave uncovered portions of the box transparent.

# DecorationImage

```dart
class DecorationImage {}
```

An image for a box decoration.

The image is painted using [paintImage], which describes the meanings of the various fields on this class in more detail.

### DecorationImage()

```dart
DecorationImage({required ImageProvider image, ImageErrorListener? onError, ColorFilter? colorFilter, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, Rect? centerSlice, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false, double scale = 1.0, double opacity = 1.0, FilterQuality filterQuality = FilterQuality.medium, bool invertColors = false, bool isAntiAlias = false})
```

Creates an image to show in a [BoxDecoration].

### image

```dart
ImageProvider image
```

The image to be painted into the decoration.

Typically this will be an [AssetImage] (for an image shipped with the application) or a [NetworkImage] (for an image obtained from the network).

### onError

```dart
ImageErrorListener? onError
```

An optional error callback for errors emitted when loading [image].

### colorFilter

```dart
ColorFilter? colorFilter
```

A color filter to apply to the image before painting it.

### fit

```dart
BoxFit? fit
```

How the image should be inscribed into the box.

The default is [BoxFit.scaleDown] if [centerSlice] is null, and [BoxFit.fill] if [centerSlice] is not null.

See the discussion at [paintImage] for more details.

### alignment

```dart
AlignmentGeometry alignment
```

How to align the image within its bounds.

The alignment aligns the given position in the image to the given position in the layout bounds. For example, an [Alignment] alignment of (-1.0, -1.0) aligns the image to the top-left corner of its layout bounds, while a [Alignment] alignment of (1.0, 1.0) aligns the bottom right of the image with the bottom right corner of its layout bounds. Similarly, an alignment of (0.0, 1.0) aligns the bottom middle of the image with the middle of the bottom edge of its layout bounds.

To display a subpart of an image, consider using a [CustomPainter] and [Canvas.drawImageRect].

If the [alignment] is [TextDirection]-dependent (i.e. if it is a [AlignmentDirectional]), then a [TextDirection] must be available when the image is painted.

Defaults to [Alignment.center].

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### centerSlice

```dart
Rect? centerSlice
```

The center slice for a nine-patch image.

The region of the image inside the center slice will be stretched both horizontally and vertically to fit the image into its destination. The region of the image above and below the center slice will be stretched only horizontally and the region of the image to the left and right of the center slice will be stretched only vertically.

The stretching will be applied in order to make the image fit into the box specified by [fit]. When [centerSlice] is not null, [fit] defaults to [BoxFit.fill], which distorts the destination image size relative to the image's original aspect ratio. Values of [BoxFit] which do not distort the destination image size will result in [centerSlice] having no effect (since the nine regions of the image will be rendered with the same scaling, as if it wasn't specified).

### repeat

```dart
ImageRepeat repeat
```

How to paint any portions of the box that would not otherwise be covered by the image.

### matchTextDirection

```dart
bool matchTextDirection
```

Whether to paint the image in the direction of the [TextDirection].

If this is true, then in [TextDirection.ltr] contexts, the image will be drawn with its origin in the top left (the "normal" painting direction for images); and in [TextDirection.rtl] contexts, the image will be drawn with a scaling factor of -1 in the horizontal direction so that the origin is in the top right.

### scale

```dart
double scale
```

Defines image pixels to be shown per logical pixels.

By default the value of scale is 1.0. The scale for the image is calculated by multiplying [scale] with [scale] of the given [ImageProvider].

### opacity

```dart
double opacity
```

If non-null, the value is multiplied with the opacity of each image pixel before painting onto the canvas.

This is more efficient than using [Opacity] or [FadeTransition] to change the opacity of an image.

### filterQuality

```dart
FilterQuality filterQuality
```

Used to set the filterQuality of the image.

Defaults to [FilterQuality.medium].

### invertColors

```dart
bool invertColors
```

Whether the colors of the image are inverted when drawn.

Inverting the colors of an image applies a new color filter to the paint. If there is another specified color filter, the invert will be applied after it. This is primarily used for implementing smart invert on iOS.

See also:

- [Paint.invertColors], for the dart:ui implementation.

### isAntiAlias

```dart
bool isAntiAlias
```

Whether to paint the image with anti-aliasing.

Anti-aliasing alleviates the sawtooth artifact when the image is rotated.

### createPainter()

```dart
DecorationImagePainter createPainter(VoidCallback onChanged)
```

Creates a [DecorationImagePainter] for this [DecorationImage].

The `onChanged` argument will be called whenever the image needs to be repainted, e.g. because it is loading incrementally or because it is animated.

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

### lerp()

```dart
DecorationImage? lerp(DecorationImage? a, DecorationImage? b, double t)
```

Linearly interpolates between two [DecorationImage]s.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a`, 1.0 meaning that the interpolation has finished, returning `b`, and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `this`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

# DecorationImagePainter

```dart
abstract interface class DecorationImagePainter {}
```

The painter for a [DecorationImage].

To obtain a painter, call [DecorationImage.createPainter].

To paint, call [paint]. The `onChanged` callback passed to [DecorationImage.createPainter] will be called if the image needs to paint again (e.g. because it is animated or because it had not yet loaded the first time the [paint] method was called).

This object should be disposed using the [dispose] method when it is no longer needed.

### paint()

```dart
void paint(Canvas canvas, Rect rect, Path? clipPath, ImageConfiguration configuration, {double blend = 1.0, BlendMode blendMode = BlendMode.srcOver})
```

Draw the image onto the given canvas.

The image is drawn at the position and size given by the `rect` argument.

The image is clipped to the given `clipPath`, if any.

The `configuration` object is used to resolve the image (e.g. to pick resolution-specific assets), and to implement the [DecorationImage.matchTextDirection] feature.

If the image needs to be painted again, e.g. because it is animated or because it had not yet been loaded the first time this method was called, then the `onChanged` callback passed to [DecorationImage.createPainter] will be called.

The `blend` argument specifies the opacity that should be applied to the image due to this image being blended with another. The `blendMode` argument can be specified to override the [DecorationImagePainter]'s default [BlendMode] behavior. It is usually set to [BlendMode.srcOver] if this is the first or only image being blended, and [BlendMode.plus] if it is being blended with an image below.

### dispose()

```dart
void dispose()
```

Releases the resources used by this painter.

This should be called whenever the painter is no longer needed.

After this method has been called, the object is no longer usable.

# debugFlushLastFrameImageSizeInfo()

```dart
void debugFlushLastFrameImageSizeInfo()
```

Flushes inter-frame tracking of image size information from [paintImage].

Has no effect if asserts are disabled.

# paintImage()

```dart
void paintImage({required Canvas canvas, required Rect rect, required ui.Image image, String? debugImageLabel, double scale = 1.0, double opacity = 1.0, ColorFilter? colorFilter, BoxFit? fit, Alignment alignment = Alignment.center, Rect? centerSlice, ImageRepeat repeat = ImageRepeat.noRepeat, bool flipHorizontally = false, bool invertColors = false, FilterQuality filterQuality = FilterQuality.medium, bool isAntiAlias = false, BlendMode blendMode = BlendMode.srcOver})
```

Paints an image into the given rectangle on the canvas.

The arguments have the following meanings:

- `canvas`: The canvas onto which the image will be painted.

- `rect`: The region of the canvas into which the image will be painted. The image might not fill the entire rectangle (e.g., depending on the `fit`). If `rect` is empty, nothing is painted.

- `image`: The image to paint onto the canvas.

- `scale`: The number of image pixels for each logical pixel.

- `opacity`: The opacity to paint the image onto the canvas with.

- `colorFilter`: If non-null, the color filter to apply when painting the image.

- `fit`: How the image should be inscribed into `rect`. If null, the default behavior depends on `centerSlice`. If `centerSlice` is also null, the default behavior is [BoxFit.scaleDown]. If `centerSlice` is non-null, the default behavior is [BoxFit.fill]. See [BoxFit] for details.

- `alignment`: How the destination rectangle defined by applying `fit` is aligned within `rect`. For example, if `fit` is [BoxFit.contain] and `alignment` is [Alignment.bottomRight], the image will be as large as possible within `rect` and placed with its bottom right corner at the bottom right corner of `rect`. Defaults to [Alignment.center].

- `centerSlice`: The image is drawn in nine portions described by splitting the image by drawing two horizontal lines and two vertical lines, where `centerSlice` describes the rectangle formed by the four points where these four lines intersect each other. (This forms a 3-by-3 grid of regions, the center region being described by `centerSlice`.) The four regions in the corners are drawn, without scaling, in the four corners of the destination rectangle defined by applying `fit`. The remaining five regions are drawn by stretching them to fit such that they exactly cover the destination rectangle while maintaining their relative positions. See also [Canvas.drawImageNine].

- `repeat`: If the image does not fill `rect`, whether and how the image should be repeated to fill `rect`. By default, the image is not repeated. See [ImageRepeat] for details.

- `flipHorizontally`: Whether to flip the image horizontally. This is occasionally used with images in right-to-left environments, for images that were designed for left-to-right locales (or vice versa). Be careful, when using this, to not flip images with integral shadows, text, or other effects that will look incorrect when flipped.

- `invertColors`: Inverting the colors of an image applies a new color filter to the paint. If there is another specified color filter, the invert will be applied after it. This is primarily used for implementing smart invert on iOS.

- `filterQuality`: Use this to change the quality when scaling an image. Defaults to [FilterQuality.medium].

See also:

- [paintBorder], which paints a border around a rectangle on a canvas.
- [DecorationImage], which holds a configuration for calling this function.
- [BoxDecoration], which uses this function to paint a [DecorationImage].
