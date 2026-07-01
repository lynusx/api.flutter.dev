# SliderComponentShape

```dart
abstract class SliderComponentShape {}
```

Base class for slider thumb, thumb overlay, and value indicator shapes.

Create a subclass of this if you would like a custom shape.

All shapes are painted to the same canvas and ordering is important. The overlay is painted first, then the value indicator, then the thumb.

The thumb painting can be skipped by specifying [noThumb] for [SliderThemeData.thumbShape].

The overlay painting can be skipped by specifying [noOverlay] for [SliderThemeData.overlayShape].

See also:

- [RoundSliderThumbShape], which is the default [Slider]'s thumb shape that paints a solid circle.
- [RoundSliderOverlayShape], which is the default [Slider] and [RangeSlider]'s overlay shape that paints a transparent circle.
- [PaddleSliderValueIndicatorShape], which is the default [Slider]'s value indicator shape that paints a custom path with text in it.

### SliderComponentShape()

```dart
SliderComponentShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

Returns the preferred size of the shape, based on the given conditions.

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

Paints the shape, taking into account the state passed to it.

{@template flutter.material.SliderComponentShape.paint.context} The `context` argument is the same as the one that includes the [Slider]'s render box. {@endtemplate}

{@template flutter.material.SliderComponentShape.paint.center} The `center` argument is the offset for where this shape's center should be painted. This offset is relative to the origin of the [context] canvas. {@endtemplate}

The `activationAnimation` argument is an animation triggered when the user begins to interact with the slider. It reverses when the user stops interacting with the slider.

{@template flutter.material.SliderComponentShape.paint.enableAnimation} The `enableAnimation` argument is an animation triggered when the [Slider] is enabled, and it reverses when the slider is disabled. The [Slider] is enabled when [Slider.onChanged] is not null. Use this to paint intermediate frames for this shape when the slider changes enabled state. {@endtemplate}

{@template flutter.material.SliderComponentShape.paint.isDiscrete} The `isDiscrete` argument is true if [Slider.divisions] is non-null. When true, the slider will render tick marks on top of the track. {@endtemplate}

If the `labelPainter` argument is non-null, then [TextPainter.paint] should be called on the `labelPainter` with the location that the label should appear. If the `labelPainter` argument is null, then no label was supplied to the [Slider].

{@template flutter.material.SliderComponentShape.paint.parentBox} The `parentBox` argument is the [RenderBox] of the [Slider]. Its attributes, such as size, can be used to assist in painting this shape. {@endtemplate}

{@template flutter.material.SliderComponentShape.paint.sliderTheme} the `sliderTheme` argument is the theme assigned to the [Slider] that this shape belongs to. {@endtemplate}

The `textDirection` argument can be used to determine how any extra text or graphics (besides the text painted by the `labelPainter`) should be positioned. The `labelPainter` already has the [textDirection] set.

The `value` argument is the current parametric value (from 0.0 to 1.0) of the slider.

{@template flutter.material.SliderComponentShape.paint.textScaleFactor} The `textScaleFactor` argument can be used to determine whether the component should paint larger or smaller, depending on whether [textScaleFactor] is greater than 1 for larger, and between 0 and 1 for smaller. It's usually computed from [MediaQueryData.textScaler]. {@endtemplate}

{@template flutter.material.SliderComponentShape.paint.sizeWithOverflow} The `sizeWithOverflow` argument can be used to determine the bounds the drawing of the components that are outside of the regular slider bounds. It's the size of the box, whose center is aligned with the slider's bounds, that the value indicators must be drawn within. Typically, it is bigger than the slider. {@endtemplate}

### noThumb

```dart
SliderComponentShape noThumb
```

Special instance of [SliderComponentShape] to skip the thumb drawing.

See also:

- [SliderThemeData.thumbShape], which is the shape that the [Slider] uses when painting the thumb.

### noOverlay

```dart
SliderComponentShape noOverlay
```

Special instance of [SliderComponentShape] to skip the overlay drawing.

See also:

- [SliderThemeData.overlayShape], which is the shape that the [Slider] uses when painting the overlay.

# RoundSliderOverlayShape

```dart
class RoundSliderOverlayShape extends SliderComponentShape {}
```

The default shape of a [Slider]'s thumb overlay.

The shape of the overlay is a circle with the same center as the thumb, but with a larger radius. It animates to full size when the thumb is pressed, and animates back down to size 0 when it is released. It is painted behind the thumb, and is expected to extend beyond the bounds of the thumb so that it is visible.

The overlay color is defined by [SliderThemeData.overlayColor].

See also:

- [Slider], which includes an overlay defined by this shape.
- [SliderTheme], which can be used to configure the overlay shape of all sliders in a widget subtree.

### RoundSliderOverlayShape()

```dart
RoundSliderOverlayShape({double overlayRadius = 24.0})
```

Create a slider thumb overlay that draws a circle.

### overlayRadius

```dart
double overlayRadius
```

The preferred radius of the round thumb shape when enabled.

If it is not provided, then half of the [SliderThemeData.trackHeight] is used.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# RectangularSliderValueIndicatorShape

```dart
class RectangularSliderValueIndicatorShape extends SliderComponentShape {}
```

The default shape of a [Slider]'s value indicator.

![A slider widget, consisting of 5 divisions and showing the rectangular slider value indicator shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rectangular_slider_value_indicator_shape.png)

See also:

- [Slider], which includes a value indicator defined by this shape.
- [SliderTheme], which can be used to configure the slider value indicator of all sliders in a widget subtree.

### RectangularSliderValueIndicatorShape()

```dart
RectangularSliderValueIndicatorShape()
```

Create a slider value indicator that resembles a rectangular tooltip.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# RectangularRangeSliderValueIndicatorShape

```dart
class RectangularRangeSliderValueIndicatorShape extends RangeSliderValueIndicatorShape {}
```

The default shape of a [RangeSlider]'s value indicators.

![A slider widget, consisting of 5 divisions and showing the rectangular range slider value indicator shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rectangular_range_slider_value_indicator_shape.png)

See also:

- [RangeSlider], which includes value indicators defined by this shape.
- [SliderTheme], which can be used to configure the range slider value indicator of all sliders in a widget subtree.

### RectangularRangeSliderValueIndicatorShape()

```dart
RectangularRangeSliderValueIndicatorShape()
```

Create a range slider value indicator that resembles a rectangular tooltip.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {required TextPainter labelPainter, required double textScaleFactor})
```

### getHorizontalShift()

```dart
double getHorizontalShift({RenderBox? parentBox, Offset? center, TextPainter? labelPainter, Animation<double>? activationAnimation, double? textScaleFactor, Size? sizeWithOverflow})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {Animation<double>? activationAnimation, Animation<double>? enableAnimation, bool? isDiscrete, bool? isOnTop, TextPainter? labelPainter, double? textScaleFactor, Size? sizeWithOverflow, RenderBox? parentBox, SliderThemeData? sliderTheme, TextDirection? textDirection, double? value, Thumb? thumb})
```

# PaddleSliderValueIndicatorShape

```dart
class PaddleSliderValueIndicatorShape extends SliderComponentShape {}
```

A variant shape of a [Slider]'s value indicator . The value indicator is in the shape of an upside-down pear.

![A slider widget, consisting of 5 divisions and showing the paddle slider value indicator shape.](https://flutter.github.io/assets-for-api-docs/assets/material/paddle_slider_value_indicator_shape.png)

See also:

- [Slider], which includes a value indicator defined by this shape.
- [SliderTheme], which can be used to configure the slider value indicator of all sliders in a widget subtree.

### PaddleSliderValueIndicatorShape()

```dart
PaddleSliderValueIndicatorShape()
```

Create a slider value indicator in the shape of an upside-down pear.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# PaddleRangeSliderValueIndicatorShape

```dart
class PaddleRangeSliderValueIndicatorShape extends RangeSliderValueIndicatorShape {}
```

A variant shape of a [RangeSlider]'s value indicators. The value indicator is in the shape of an upside-down pear.

![A slider widget, consisting of 5 divisions and showing the paddle range slider value indicator shape.](https://flutter.github.io/assets-for-api-docs/assets/material/paddle_range_slider_value_indicator_shape.png)

See also:

- [RangeSlider], which includes value indicators defined by this shape.
- [SliderTheme], which can be used to configure the range slider value indicator of all sliders in a widget subtree.

### PaddleRangeSliderValueIndicatorShape()

```dart
PaddleRangeSliderValueIndicatorShape()
```

Create a slider value indicator in the shape of an upside-down pear.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {required TextPainter labelPainter, required double textScaleFactor})
```

### getHorizontalShift()

```dart
double getHorizontalShift({RenderBox? parentBox, Offset? center, TextPainter? labelPainter, Animation<double>? activationAnimation, double? textScaleFactor, Size? sizeWithOverflow})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool? isDiscrete, bool isOnTop = false, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, TextDirection? textDirection, Thumb? thumb, double? value, double? textScaleFactor, Size? sizeWithOverflow})
```
