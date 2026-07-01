# RenderImage

```dart
class RenderImage extends RenderBox {}
```

An image in the render tree.

The render image attempts to find a size for itself that fits in the given constraints and preserves the image's intrinsic aspect ratio.

The image is painted using [paintImage], which describes the meanings of the various fields on this class in more detail.

### RenderImage()

```dart
RenderImage({ui.Image? image, String? debugImageLabel, double? width, double? height, double scale = 1.0, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, TextDirection? textDirection, bool invertColors = false, bool isAntiAlias = false, FilterQuality filterQuality = FilterQuality.medium})
```

Creates a render box that displays an image.

The [textDirection] argument must not be null if [alignment] will need resolving or if [matchTextDirection] is true.

### image

```dart
ui.Image? get image
```

The image to display.

### image

```dart
set image(ui.Image? value)
```

### debugImageLabel

```dart
String? debugImageLabel
```

A string used to identify the source of the image.

### width

```dart
double? get width
```

If non-null, requires the image to have this width.

If null, the image will pick a size that best preserves its intrinsic aspect ratio.

### width

```dart
set width(double? value)
```

### height

```dart
double? get height
```

If non-null, require the image to have this height.

If null, the image will pick a size that best preserves its intrinsic aspect ratio.

### height

```dart
set height(double? value)
```

### scale

```dart
double get scale
```

Specifies the image's scale.

Used when determining the best display size for the image.

### scale

```dart
set scale(double value)
```

### color

```dart
Color? get color
```

If non-null, this color is blended with each image pixel using [colorBlendMode].

### color

```dart
set color(Color? value)
```

### opacity

```dart
Animation<double>? get opacity
```

If non-null, the value from the [Animation] is multiplied with the opacity of each image pixel before painting onto the canvas.

### opacity

```dart
set opacity(Animation<double>? value)
```

### filterQuality

```dart
FilterQuality get filterQuality
```

Used to set the filterQuality of the image.

Defaults to [FilterQuality.medium].

### filterQuality

```dart
set filterQuality(FilterQuality value)
```

### colorBlendMode

```dart
BlendMode? get colorBlendMode
```

Used to combine [color] with this image.

The default is [BlendMode.srcIn]. In terms of the blend mode, [color] is the source and this image is the destination.

See also:

- [BlendMode], which includes an illustration of the effect of each blend mode.

### colorBlendMode

```dart
set colorBlendMode(BlendMode? value)
```

### fit

```dart
BoxFit? get fit
```

How to inscribe the image into the space allocated during layout.

The default varies based on the other fields. See the discussion at [paintImage].

### fit

```dart
set fit(BoxFit? value)
```

### alignment

```dart
AlignmentGeometry get alignment
```

How to align the image within its bounds.

If this is set to a text-direction-dependent value, [textDirection] must not be null.

### alignment

```dart
set alignment(AlignmentGeometry value)
```

### repeat

```dart
ImageRepeat get repeat
```

How to repeat this image if it doesn't fill its layout bounds.

### repeat

```dart
set repeat(ImageRepeat value)
```

### centerSlice

```dart
Rect? get centerSlice
```

The center slice for a nine-patch image.

The region of the image inside the center slice will be stretched both horizontally and vertically to fit the image into its destination. The region of the image above and below the center slice will be stretched only horizontally and the region of the image to the left and right of the center slice will be stretched only vertically.

### centerSlice

```dart
set centerSlice(Rect? value)
```

### invertColors

```dart
bool get invertColors
```

Whether to invert the colors of the image.

Inverting the colors of an image applies a new color filter to the paint. If there is another specified color filter, the invert will be applied after it. This is primarily used for implementing smart invert on iOS.

### invertColors

```dart
set invertColors(bool value)
```

### matchTextDirection

```dart
bool get matchTextDirection
```

Whether to paint the image in the direction of the [TextDirection].

If this is true, then in [TextDirection.ltr] contexts, the image will be drawn with its origin in the top left (the "normal" painting direction for images); and in [TextDirection.rtl] contexts, the image will be drawn with a scaling factor of -1 in the horizontal direction so that the origin is in the top right.

This is occasionally used with images in right-to-left environments, for images that were designed for left-to-right locales. Be careful, when using this, to not flip images with integral shadows, text, or other effects that will look incorrect when flipped.

If this is set to true, [textDirection] must not be null.

### matchTextDirection

```dart
set matchTextDirection(bool value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [alignment].

This may be changed to null, but only after the [alignment] and [matchTextDirection] properties have been changed to values that do not depend on the direction.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### isAntiAlias

```dart
bool get isAntiAlias
```

Whether to paint the image with anti-aliasing.

Anti-aliasing alleviates the sawtooth artifact when the image is rotated.

### isAntiAlias

```dart
set isAntiAlias(bool value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
