@docImport 'color_scheme.dart'; @docImport 'slider.dart'; @docImport 'text_theme.dart';

# SliderTickMarkShape

```dart
abstract class SliderTickMarkShape {}
```

Base class for [Slider] tick mark shapes.

Create a subclass of this if you would like a custom slider tick mark shape.

The tick mark painting can be skipped by specifying [noTickMark] for [SliderThemeData.tickMarkShape].

See also:

- [RoundSliderTickMarkShape], which is the default [Slider]'s tick mark shape that paints a solid circle.
- [SliderTrackShape], which can be used to create custom shapes for the [Slider]'s track.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### SliderTickMarkShape()

```dart
SliderTickMarkShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredSize()

```dart
Size getPreferredSize({required SliderThemeData sliderTheme, required bool isEnabled})
```

Returns the preferred size of the shape.

It is used to help position the tick marks within the slider.

{@macro flutter.material.SliderComponentShape.paint.sliderTheme}

{@template flutter.material.SliderTickMarkShape.getPreferredSize.isEnabled} The `isEnabled` argument is false when [Slider.onChanged] is null and true otherwise. When true, the slider will respond to input. {@endtemplate}

### paint()

```dart
void paint(PaintingContext context, Offset center, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset thumbCenter, required bool isEnabled, required TextDirection textDirection})
```

Paints the slider track.

{@macro flutter.material.SliderComponentShape.paint.context}

{@macro flutter.material.SliderComponentShape.paint.center}

{@macro flutter.material.SliderComponentShape.paint.parentBox}

{@macro flutter.material.SliderComponentShape.paint.sliderTheme}

{@macro flutter.material.SliderComponentShape.paint.enableAnimation}

{@macro flutter.material.SliderTickMarkShape.getPreferredSize.isEnabled}

The `textDirection` argument can be used to determine how the tick marks are painting depending on whether they are on an active track segment or not. The track segment between the start of the slider and the thumb is the active track segment. The track segment between the thumb and the end of the slider is the inactive track segment. In LTR text direction, the start of the slider is on the left, and in RTL text direction, the start of the slider is on the right.

### noTickMark

```dart
SliderTickMarkShape noTickMark
```

Special instance of [SliderTickMarkShape] to skip the tick mark painting.

See also:

- [SliderThemeData.tickMarkShape], which is the shape that the [Slider] uses when painting tick marks.

# SliderTrackShape

```dart
abstract class SliderTrackShape {}
```

Base class for slider track shapes.

The slider's thumb moves along the track. A discrete slider's tick marks are drawn after the track, but before the thumb, and are aligned with the track.

The [getPreferredRect] helps position the slider thumb and tick marks relative to the track.

See also:

- [RoundedRectSliderTrackShape] for the default [Slider]'s track shape that paints a stadium-like track.
- [SliderTickMarkShape], which can be used to create custom shapes for the [Slider]'s tick marks.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### SliderTrackShape()

```dart
SliderTrackShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredRect()

```dart
Rect getPreferredRect({required RenderBox parentBox, Offset offset = Offset.zero, required SliderThemeData sliderTheme, bool isEnabled, bool isDiscrete})
```

Returns the preferred bounds of the shape.

It is used to provide horizontal boundaries for the thumb's position, and to help position the slider thumb and tick marks relative to the track.

The `parentBox` argument can be used to help determine the preferredRect relative to attributes of the render box of the slider itself, such as size.

The `offset` argument is relative to the caller's bounding box. It can be used to convert gesture coordinates from global to slider-relative coordinates.

{@macro flutter.material.SliderComponentShape.paint.sliderTheme}

{@macro flutter.material.SliderTickMarkShape.getPreferredSize.isEnabled}

{@macro flutter.material.SliderComponentShape.paint.isDiscrete}

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset thumbCenter, Offset? secondaryOffset, bool isEnabled, bool isDiscrete, required TextDirection textDirection})
```

Paints the track shape based on the state passed to it.

{@macro flutter.material.SliderComponentShape.paint.context}

The `offset` argument the offset of the origin of the `parentBox` to the origin of its `context` canvas. This shape must be painted relative to this offset. See [PaintingContextCallback].

{@macro flutter.material.SliderComponentShape.paint.parentBox}

{@macro flutter.material.SliderComponentShape.paint.sliderTheme}

{@macro flutter.material.SliderComponentShape.paint.enableAnimation}

The `thumbCenter` argument is the offset of the center of the thumb relative to the origin of the [PaintingContext.canvas]. It can be used as the point that divides the track into 2 segments.

The `secondaryOffset` argument is the offset of the secondary value relative to the origin of the [PaintingContext.canvas].

If not null, the track is divided into 3 segments.

{@macro flutter.material.SliderTickMarkShape.getPreferredSize.isEnabled}

{@macro flutter.material.SliderComponentShape.paint.isDiscrete}

The `textDirection` argument can be used to determine how the track segments are painted depending on whether they are active or not.

{@template flutter.material.SliderTrackShape.paint.trackSegment} The track segment between the start of the slider and the thumb is the active track segment. The track segment between the thumb and the end of the slider is the inactive track segment. In [TextDirection.ltr], the start of the slider is on the left, and in [TextDirection.rtl], the start of the slider is on the right. {@endtemplate}

### isRounded

```dart
bool get isRounded
```

Whether the track shape is rounded.

This is used to determine the correct position of the thumb in relation to the track.

# BaseSliderTrackShape

```dart
mixin BaseSliderTrackShape {}
```

Base track shape that provides an implementation of [getPreferredRect] for default sizing.

The height is set from [SliderThemeData.trackHeight] and the width of the parent box less the larger of the widths of [SliderThemeData.thumbShape] and [SliderThemeData.overlayShape].

See also:

- [RectangularSliderTrackShape], which is a track shape with sharp rectangular edges
- [RoundedRectSliderTrackShape], which is a track shape with round stadium-like edges.

### getPreferredRect()

```dart
Rect getPreferredRect({required RenderBox parentBox, Offset offset = Offset.zero, required SliderThemeData sliderTheme, bool isEnabled = false, bool isDiscrete = false})
```

Returns a rect that represents the track bounds that fits within the [Slider].

The width is the width of the [Slider] or [RangeSlider], but padded by the max of the overlay and thumb radius. The height is defined by the [SliderThemeData.trackHeight].

The [Rect] is centered both horizontally and vertically within the slider bounds.

### isRounded

```dart
bool get isRounded
```

Whether the track shape is rounded. This is used to determine the correct position of the thumb in relation to the track. Defaults to false.

# RectangularSliderTrackShape

```dart
class RectangularSliderTrackShape extends SliderTrackShape with BaseSliderTrackShape {}
```

A [Slider] track that's a simple rectangle.

It paints a solid colored rectangle, vertically centered in the `parentBox`. The track rectangle extends to the bounds of the `parentBox`, but is padded by the [RoundSliderOverlayShape] radius. The height is defined by the [SliderThemeData.trackHeight]. The color is determined by the [Slider]'s enabled state and the track segment's active state which are defined by: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

{@macro flutter.material.SliderTrackShape.paint.trackSegment}

![A slider widget, consisting of 5 divisions and showing the rectangular slider track shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rectangular_slider_track_shape.png)

See also:

- [Slider], for the component that is meant to display this shape.
- [SliderThemeData], where an instance of this class is set to inform the slider of the visual details of the its track.
- [SliderTrackShape], which can be used to create custom shapes for the [Slider]'s track.
- [RoundedRectSliderTrackShape], for a similar track with rounded edges.

### RectangularSliderTrackShape()

```dart
RectangularSliderTrackShape()
```

Creates a slider track that draws 2 rectangles.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required TextDirection textDirection, required Offset thumbCenter, Offset? secondaryOffset, bool isDiscrete = false, bool isEnabled = false})
```

# RoundedRectSliderTrackShape

```dart
class RoundedRectSliderTrackShape extends SliderTrackShape with BaseSliderTrackShape {}
```

The default shape of a [Slider]'s track.

It paints a solid colored rectangle with rounded edges, vertically centered in the `parentBox`. The track rectangle extends to the bounds of the `parentBox`, but is padded by the larger of [RoundSliderOverlayShape]'s radius and [RoundSliderThumbShape]'s radius. The height is defined by the [SliderThemeData.trackHeight]. The color is determined by the [Slider]'s enabled state and the track segment's active state which are defined by: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

{@macro flutter.material.SliderTrackShape.paint.trackSegment}

![A slider widget, consisting of 5 divisions and showing the rounded rect slider track shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rounded_rect_slider_track_shape.png)

See also:

- [Slider], for the component that is meant to display this shape.
- [SliderThemeData], where an instance of this class is set to inform the slider of the visual details of the its track.
- [SliderTrackShape], which can be used to create custom shapes for the [Slider]'s track.
- [RectangularSliderTrackShape], for a similar track with sharp edges.

### RoundedRectSliderTrackShape()

```dart
RoundedRectSliderTrackShape()
```

Create a slider track that draws two rectangles with rounded outer edges.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required TextDirection textDirection, required Offset thumbCenter, Offset? secondaryOffset, bool isDiscrete = false, bool isEnabled = false, double additionalActiveTrackHeight = 2})
```

### isRounded

```dart
bool get isRounded
```

# RoundSliderTickMarkShape

```dart
class RoundSliderTickMarkShape extends SliderTickMarkShape {}
```

The default shape of each [Slider] tick mark.

Tick marks are only displayed if the slider is discrete, which can be done by setting the [Slider.divisions] to an integer value.

It paints a solid circle, centered in the on the track. The color is determined by the [Slider]'s enabled state and track's active states. These colors are defined in: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

![A slider widget, consisting of 5 divisions and showing the round slider tick mark shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rounded_slider_tick_mark_shape.png)

See also:

- [Slider], which includes tick marks defined by this shape.
- [SliderTheme], which can be used to configure the tick mark shape of all sliders in a widget subtree.

### RoundSliderTickMarkShape()

```dart
RoundSliderTickMarkShape({double? tickMarkRadius})
```

Create a slider tick mark that draws a circle.

### tickMarkRadius

```dart
double? tickMarkRadius
```

The preferred radius of the round tick mark.

If it is not provided, then 1/4 of the [SliderThemeData.trackHeight] is used.

### getPreferredSize()

```dart
Size getPreferredSize({required SliderThemeData sliderTheme, required bool isEnabled})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required TextDirection textDirection, required Offset thumbCenter, required bool isEnabled})
```

# RoundSliderThumbShape

```dart
class RoundSliderThumbShape extends SliderComponentShape {}
```

The default shape of a [Slider]'s thumb.

There is a shadow for the resting, pressed, hovered, and focused state.

![A slider widget, consisting of 5 divisions and showing the round slider thumb shape.](https://flutter.github.io/assets-for-api-docs/assets/material/round_slider_thumb_shape.png)

See also:

- [Slider], which includes a thumb defined by this shape.
- [SliderTheme], which can be used to configure the thumb shape of all sliders in a widget subtree.

### RoundSliderThumbShape()

```dart
RoundSliderThumbShape({double enabledThumbRadius = 10.0, double? disabledThumbRadius, double elevation = 1.0, double pressedElevation = 6.0})
```

Create a slider thumb that draws a circle.

### enabledThumbRadius

```dart
double enabledThumbRadius
```

The preferred radius of the round thumb shape when the slider is enabled.

If it is not provided, then the Material Design default of 10 is used.

### disabledThumbRadius

```dart
double? disabledThumbRadius
```

The preferred radius of the round thumb shape when the slider is disabled.

If no disabledRadius is provided, then it is equal to the [enabledThumbRadius]

### elevation

```dart
double elevation
```

The resting elevation adds shadow to the unpressed thumb.

The default is 1.

Use 0 for no shadow. The higher the value, the larger the shadow. For example, a value of 12 will create a very large shadow.

### pressedElevation

```dart
double pressedElevation
```

The pressed elevation adds shadow to the pressed thumb.

The default is 6.

Use 0 for no shadow. The higher the value, the larger the shadow. For example, a value of 12 will create a very large shadow.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# DropSliderValueIndicatorShape

```dart
class DropSliderValueIndicatorShape extends SliderComponentShape {}
```

The default shape of a Material 3 [Slider]'s value indicator.

See also:

- [Slider], which includes a value indicator defined by this shape.
- [SliderTheme], which can be used to configure the slider value indicator of all sliders in a widget subtree.

### DropSliderValueIndicatorShape()

```dart
DropSliderValueIndicatorShape()
```

Create a slider value indicator that resembles a drop shape.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# HandleThumbShape

```dart
class HandleThumbShape extends SliderComponentShape {}
```

The bar shape of a [Slider]'s thumb.

When the slider is enabled, the [ColorScheme.primary] color is used for the thumb. When the slider is disabled, the [ColorScheme.onSurface] color with an opacity of 0.38 is used for the thumb.

The thumb bar shape width is reduced when the thumb is pressed.

If [SliderThemeData.thumbSize] is null, then the thumb size is 4 pixels for the width and 44 pixels for the height.

This is the default thumb shape for [Slider]. If [ThemeData.useMaterial3] is false, then the default thumb shape is [RoundSliderThumbShape].

See also:

- [Slider], which includes an overlay defined by this shape.
- [SliderTheme], which can be used to configure the overlay shape of all sliders in a widget subtree.

### HandleThumbShape()

```dart
HandleThumbShape()
```

Create a slider thumb that draws a bar.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```

# GappedSliderTrackShape

```dart
class GappedSliderTrackShape extends SliderTrackShape with BaseSliderTrackShape {}
```

The gapped shape of a [Slider]'s track.

The [GappedSliderTrackShape] consists of active and inactive tracks. The active track uses the [SliderThemeData.activeTrackColor] and the inactive track uses the [SliderThemeData.inactiveTrackColor].

The track shape uses circular corner radius for the edge corners and a corner radius of 2 pixels for the inside corners.

Between the active and inactive tracks there is a gap of size [SliderThemeData.trackGap]. If the [SliderThemeData.thumbShape] is [HandleThumbShape] and the thumb is pressed, the thumb's width is reduced; as a result, the track gap size in [GappedSliderTrackShape] is also reduced.

If [SliderThemeData.trackGap] is null, then the track gap size defaults to 6 pixels.

This is the default track shape for [Slider]. If [ThemeData.useMaterial3] is false, then the default track shape is [RoundedRectSliderTrackShape].

See also:

- [Slider], which includes an overlay defined by this shape.
- [SliderTheme], which can be used to configure the overlay shape of all sliders in a widget subtree.

### GappedSliderTrackShape()

```dart
GappedSliderTrackShape()
```

Create a slider track that draws two rectangles with rounded outer edges.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required TextDirection textDirection, required Offset thumbCenter, Offset? secondaryOffset, bool isDiscrete = false, bool isEnabled = false, double additionalActiveTrackHeight = 2})
```

### isRounded

```dart
bool get isRounded
```

# RoundedRectSliderValueIndicatorShape

```dart
class RoundedRectSliderValueIndicatorShape extends SliderComponentShape {}
```

The rounded rectangle shape of a [Slider]'s value indicator.

If the [SliderThemeData.valueIndicatorColor] is null, then the shape uses the [ColorScheme.inverseSurface] color to draw the value indicator.

If the [SliderThemeData.valueIndicatorTextStyle] is null, then the indicator label text style defaults to [TextTheme.labelMedium] with the color set to [ColorScheme.onInverseSurface]. If the [ThemeData.useMaterial3] is set to false, then the indicator label text style defaults to [TextTheme.bodyLarge] with the color set to [ColorScheme.onInverseSurface].

If the [SliderThemeData.valueIndicatorStrokeColor] is provided, then the value indicator is drawn with a stroke border with the color provided.

This is the default value indicator shape for [Slider]. If [ThemeData.useMaterial3] is false, then the default value indicator shape is [RectangularSliderValueIndicatorShape].

See also:

- [Slider], which includes a value indicator defined by this shape.
- [SliderTheme], which can be used to configure the slider value indicator of all sliders in a widget subtree.

### RoundedRectSliderValueIndicatorShape()

```dart
RoundedRectSliderValueIndicatorShape()
```

Create a slider value indicator that resembles a rounded rectangle.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, required bool isDiscrete, required TextPainter labelPainter, required RenderBox parentBox, required SliderThemeData sliderTheme, required TextDirection textDirection, required double value, required double textScaleFactor, required Size sizeWithOverflow})
```
