@docImport 'package:flutter/rendering.dart';

# ImgElementPlatformView

```dart
class ImgElementPlatformView extends StatelessWidget {}
```

Displays an `<img>` element with `src` set to [src].

### ImgElementPlatformView()

```dart
ImgElementPlatformView(String? src, {dynamic key})
```

Creates a platform view backed with an `<img>` element.

### src

```dart
String? src
```

The `src` URL for the `<img>` tag.

### build()

```dart
Widget build(BuildContext context)
```

# RawWebImage

```dart
class RawWebImage extends SingleChildRenderObjectWidget {}
```

A widget which displays and lays out an underlying HTML element in a platform view.

### RawWebImage()

```dart
RawWebImage({dynamic key, required WebImageInfo image, String? debugImageLabel, double? width, double? height, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, bool matchTextDirection = false})
```

Creates a [RawWebImage].

### image

```dart
WebImageInfo image
```

The underlying HTML element to be displayed.

### debugImageLabel

```dart
String? debugImageLabel
```

A debug label explaining the image.

### width

```dart
double? width
```

The requested width for this widget.

### height

```dart
double? height
```

The requested height for this widget.

### fit

```dart
BoxFit? fit
```

How the HTML element should be inscribed in the box constraining it.

### alignment

```dart
AlignmentGeometry alignment
```

How the image should be aligned in the box constraining it.

### matchTextDirection

```dart
bool matchTextDirection
```

Whether or not the alignment of the image should match the text direction.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderWebImage renderObject)
```

# RenderWebImage

```dart
class RenderWebImage extends RenderShiftedBox {}
```

Lays out and positions the child HTML element similarly to [RenderImage].

### RenderWebImage()

```dart
RenderWebImage({RenderBox? child, required web.HTMLImageElement image, double? width, double? height, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, bool matchTextDirection = false, TextDirection? textDirection})
```

Creates a new [RenderWebImage].

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

### image

```dart
web.HTMLImageElement get image
```

The image to display.

### image

```dart
set image(web.HTMLImageElement value)
```

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

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
