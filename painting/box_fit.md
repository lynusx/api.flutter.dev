@docImport 'package:flutter/widgets.dart';

@docImport 'box_decoration.dart';

# BoxFit

```dart
enum BoxFit {}
```

How a box should be inscribed into another box.

See also:

- [applyBoxFit], which applies the sizing semantics of these values (though not the alignment semantics).

Fill the target box by distorting the source's aspect ratio.

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fill.png)

As large as possible while still containing the source entirely within the target box.

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_contain.png)

As small as possible while still covering the entire target box.

{@template flutter.painting.BoxFit.cover} To actually clip the content, use `clipBehavior: Clip.hardEdge` alongside this in a [FittedBox]. {@endtemplate}

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_cover.png)

Make sure the full width of the source is shown, regardless of whether this means the source overflows the target box vertically.

{@macro flutter.painting.BoxFit.cover}

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fitWidth.png)

Make sure the full height of the source is shown, regardless of whether this means the source overflows the target box horizontally.

{@macro flutter.painting.BoxFit.cover}

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_fitHeight.png)

Align the source within the target box (by default, centering) and discard any portions of the source that lie outside the box.

The source image is not resized.

{@macro flutter.painting.BoxFit.cover}

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_none.png)

Align the source within the target box (by default, centering) and, if necessary, scale the source down to ensure that the source fits within the box.

This is the same as `contain` if that would shrink the image, otherwise it is the same as `none`.

![](https://flutter.github.io/assets-for-api-docs/assets/painting/box_fit_scaleDown.png)

# FittedSizes

```dart
class FittedSizes {}
```

The pair of sizes returned by [applyBoxFit].

### FittedSizes()

```dart
FittedSizes(Size source, Size destination)
```

Creates an object to store a pair of sizes, as would be returned by [applyBoxFit].

### source

```dart
Size source
```

The size of the part of the input to show on the output.

### destination

```dart
Size destination
```

The size of the part of the output on which to show the input.

# applyBoxFit()

```dart
FittedSizes applyBoxFit(BoxFit fit, Size inputSize, Size outputSize)
```

Apply a [BoxFit] value.

The arguments to this method, in addition to the [BoxFit] value to apply, are two sizes, ostensibly the sizes of an input box and an output box. Specifically, the `inputSize` argument gives the size of the complete source that is being fitted, and the `outputSize` gives the size of the rectangle into which the source is to be drawn.

This function then returns two sizes, combined into a single [FittedSizes] object.

The [FittedSizes.source] size is the subpart of the `inputSize` that is to be shown. If the entire input source is shown, then this will equal the `inputSize`, but if the input source is to be cropped down, this may be smaller.

The [FittedSizes.destination] size is the subpart of the `outputSize` in which to paint the (possibly cropped) source. If the [FittedSizes.destination] size is smaller than the `outputSize` then the source is being letterboxed (or pillarboxed).

This method does not express an opinion regarding the alignment of the source and destination sizes within the input and output rectangles. Typically they are centered (this is what [BoxDecoration] does, for instance, and is how [BoxFit] is defined). The [Alignment] class provides a convenience function, [Alignment.inscribe], for resolving the sizes to rects, as shown in the example below.

{@tool snippet}

This function paints a [dart:ui.Image] `image` onto the [Rect] `outputRect` on a [Canvas] `canvas`, using a [Paint] `paint`, applying the [BoxFit] algorithm `fit`:

```dart
void paintImage(ui.Image image, Rect outputRect, Canvas canvas, Paint paint, BoxFit fit) {
  final Size imageSize = Size(image.width.toDouble(), image.height.toDouble());
  final FittedSizes sizes = applyBoxFit(fit, imageSize, outputRect.size);
  final Rect inputSubrect = Alignment.center.inscribe(sizes.source, Offset.zero & imageSize);
  final Rect outputSubrect = Alignment.center.inscribe(sizes.destination, outputRect);
  canvas.drawImageRect(image, inputSubrect, outputSubrect, paint);
}
```

{@end-tool}

See also:

- [FittedBox], a widget that applies this algorithm to another widget.
- [paintImage], a function that applies this algorithm to images for painting.
- [DecoratedBox], [BoxDecoration], and [DecorationImage], which together provide access to [paintImage] at the widgets layer.
