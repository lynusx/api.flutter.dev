@docImport 'color_scheme.dart'; @docImport 'range_slider.dart'; @docImport 'text_theme.dart';

# RangeSliderThumbShape

```dart
abstract class RangeSliderThumbShape {}
```

Base class for [RangeSlider] thumb shapes.

See also:

- [RoundRangeSliderThumbShape] for the default [RangeSlider]'s thumb shape that paints a solid circle.
- [RangeSliderTickMarkShape], which can be used to create custom shapes for the [RangeSlider]'s tick marks.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RangeSliderValueIndicatorShape], which can be used to create custom shapes for the [RangeSlider]'s value indicator.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### RangeSliderThumbShape()

```dart
RangeSliderThumbShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

Returns the preferred size of the shape, based on the given conditions.

{@template flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete} The `isDiscrete` argument is true if [RangeSlider.divisions] is non-null. When true, the slider will render tick marks on top of the track. {@endtemplate}

{@template flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled} The `isEnabled` argument is false when [RangeSlider.onChanged] is null and true otherwise. When true, the slider will respond to input. {@endtemplate}

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool isDiscrete, bool isEnabled, bool isOnTop, TextDirection textDirection, required SliderThemeData sliderTheme, Thumb thumb, bool isPressed})
```

Paints the thumb shape based on the state passed to it.

{@template flutter.material.RangeSliderThumbShape.paint.context} The `context` argument represents the [RangeSlider]'s render box. {@endtemplate}

{@macro flutter.material.SliderComponentShape.paint.center}

{@template flutter.material.RangeSliderThumbShape.paint.activationAnimation} The `activationAnimation` argument is an animation triggered when the user begins to interact with the [RangeSlider]. It reverses when the user stops interacting with the slider. {@endtemplate}

{@template flutter.material.RangeSliderThumbShape.paint.enableAnimation} The `enableAnimation` argument is an animation triggered when the [RangeSlider] is enabled, and it reverses when the slider is disabled. The [RangeSlider] is enabled when [RangeSlider.onChanged] is not null. Use this to paint intermediate frames for this shape when the slider changes enabled state. {@endtemplate}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

If the `isOnTop` argument is true, this thumb is painted on top of the other slider thumb because this thumb is the one that was most recently selected.

{@template flutter.material.RangeSliderThumbShape.paint.sliderTheme} The `sliderTheme` argument is the theme assigned to the [RangeSlider] that this shape belongs to. {@endtemplate}

The `textDirection` argument can be used to determine how the orientation of either slider thumb should be changed, such as drawing different shapes for the left and right thumb.

{@template flutter.material.RangeSliderThumbShape.paint.thumb} The `thumb` argument is the specifier for which of the two thumbs this method should paint (start or end). {@endtemplate}

The `isPressed` argument can be used to give the selected thumb additional selected or pressed state visual feedback, such as a larger shadow.

# RangeSliderValueIndicatorShape

```dart
abstract class RangeSliderValueIndicatorShape {}
```

Base class for [RangeSlider] value indicator shapes.

See also:

- [PaddleRangeSliderValueIndicatorShape] for the default [RangeSlider]'s value indicator shape that paints a custom path with text in it.
- [RangeSliderTickMarkShape], which can be used to create custom shapes for the [RangeSlider]'s tick marks.
- [RangeSliderThumbShape], which can be used to create custom shapes for the [RangeSlider]'s thumb.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### RangeSliderValueIndicatorShape()

```dart
RangeSliderValueIndicatorShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {required TextPainter labelPainter, required double textScaleFactor})
```

Returns the preferred size of the shape, based on the given conditions.

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete}

The `labelPainter` argument helps determine the width of the shape. It is variable width because it is derived from a formatted string.

{@macro flutter.material.SliderComponentShape.paint.textScaleFactor}

### getHorizontalShift()

```dart
double getHorizontalShift({RenderBox? parentBox, Offset? center, TextPainter? labelPainter, Animation<double>? activationAnimation, double? textScaleFactor, Size? sizeWithOverflow})
```

Determines the best offset to keep this shape on the screen.

Override this method when the center of the value indicator should be shifted from the vertical center of the thumb.

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool isDiscrete, bool isOnTop, required TextPainter labelPainter, double textScaleFactor, Size sizeWithOverflow, required RenderBox parentBox, required SliderThemeData sliderTheme, TextDirection textDirection, double value, Thumb thumb})
```

Paints the value indicator shape based on the state passed to it.

{@macro flutter.material.RangeSliderThumbShape.paint.context}

{@macro flutter.material.SliderComponentShape.paint.center}

{@macro flutter.material.RangeSliderThumbShape.paint.activationAnimation}

{@macro flutter.material.RangeSliderThumbShape.paint.enableAnimation}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete}

The `isOnTop` argument is the top-most value indicator between the two value indicators, which is always the indicator for the most recently selected thumb. In the default case, this is used to paint a stroke around the top indicator for better visibility between the two indicators.

{@macro flutter.material.SliderComponentShape.paint.textScaleFactor}

{@macro flutter.material.SliderComponentShape.paint.sizeWithOverflow}

{@template flutter.material.RangeSliderValueIndicatorShape.paint.parentBox} The `parentBox` argument is the [RenderBox] of the [RangeSlider]. Its attributes, such as size, can be used to assist in painting this shape. {@endtemplate}

{@macro flutter.material.RangeSliderThumbShape.paint.sliderTheme}

The `textDirection` argument can be used to determine how any extra text or graphics, besides the text painted by the [labelPainter] should be positioned. The `labelPainter` argument already has the `textDirection` set.

The `value` argument is the current parametric value (from 0.0 to 1.0) of the slider.

{@macro flutter.material.RangeSliderThumbShape.paint.thumb}

# RangeSliderTickMarkShape

```dart
abstract class RangeSliderTickMarkShape {}
```

Base class for [RangeSlider] tick mark shapes.

This is a simplified version of [SliderComponentShape] with a [SliderThemeData] passed when getting the preferred size.

See also:

- [RoundRangeSliderTickMarkShape] for the default [RangeSlider]'s tick mark shape that paints a solid circle.
- [RangeSliderThumbShape], which can be used to create custom shapes for the [RangeSlider]'s thumb.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RangeSliderValueIndicatorShape], which can be used to create custom shapes for the [RangeSlider]'s value indicator.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### RangeSliderTickMarkShape()

```dart
RangeSliderTickMarkShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredSize()

```dart
Size getPreferredSize({required SliderThemeData sliderTheme, bool isEnabled})
```

Returns the preferred size of the shape.

It is used to help position the tick marks within the slider.

{@macro flutter.material.RangeSliderThumbShape.paint.sliderTheme}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

### paint()

```dart
void paint(PaintingContext context, Offset center, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled, required TextDirection textDirection})
```

Paints the slider track.

{@macro flutter.material.RangeSliderThumbShape.paint.context}

{@macro flutter.material.SliderComponentShape.paint.center}

{@macro flutter.material.RangeSliderValueIndicatorShape.paint.parentBox}

{@macro flutter.material.RangeSliderThumbShape.paint.sliderTheme}

{@macro flutter.material.RangeSliderThumbShape.paint.enableAnimation}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

The `textDirection` argument can be used to determine how the tick marks are painted depending on whether they are on an active track segment or not.

{@template flutter.material.RangeSliderTickMarkShape.paint.trackSegment} The track segment between the two thumbs is the active track segment. The track segments between the thumb and each end of the slider are the inactive track segments. In [TextDirection.ltr], the start of the slider is on the left, and in [TextDirection.rtl], the start of the slider is on the right. {@endtemplate}

# RangeSliderTrackShape

```dart
abstract class RangeSliderTrackShape {}
```

Base class for [RangeSlider] track shapes.

The slider's thumbs move along the track. A discrete slider's tick marks are drawn after the track, but before the thumb, and are aligned with the track.

The [getPreferredRect] helps position the slider thumbs and tick marks relative to the track.

See also:

- [RoundedRectRangeSliderTrackShape] for the default [RangeSlider]'s track shape that paints a stadium-like track.
- [RangeSliderTickMarkShape], which can be used to create custom shapes for the [RangeSlider]'s tick marks.
- [RangeSliderThumbShape], which can be used to create custom shapes for the [RangeSlider]'s thumb.
- [RangeSliderValueIndicatorShape], which can be used to create custom shapes for the [RangeSlider]'s value indicator.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.

### RangeSliderTrackShape()

```dart
RangeSliderTrackShape()
```

This abstract const constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getPreferredRect()

```dart
Rect getPreferredRect({required RenderBox parentBox, Offset offset = Offset.zero, required SliderThemeData sliderTheme, bool isEnabled, bool isDiscrete})
```

Returns the preferred bounds of the shape.

It is used to provide horizontal boundaries for the position of the thumbs, and to help position the slider thumbs and tick marks relative to the track.

The `parentBox` argument can be used to help determine the preferredRect relative to attributes of the render box of the slider itself, such as size.

The `offset` argument is relative to the caller's bounding box. It can be used to convert gesture coordinates from global to slider-relative coordinates.

{@macro flutter.material.RangeSliderThumbShape.paint.sliderTheme}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete}

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled = false, bool isDiscrete = false, required TextDirection textDirection})
```

Paints the track shape based on the state passed to it.

{@macro flutter.material.SliderComponentShape.paint.context}

The `offset` argument is the offset of the origin of the `parentBox` to the origin of its `context` canvas. This shape must be painted relative to this offset. See [PaintingContextCallback].

{@macro flutter.material.RangeSliderValueIndicatorShape.paint.parentBox}

{@macro flutter.material.RangeSliderThumbShape.paint.sliderTheme}

{@macro flutter.material.RangeSliderThumbShape.paint.enableAnimation}

The `startThumbCenter` argument is the offset of the center of the start thumb relative to the origin of the [PaintingContext.canvas]. It can be used as one point that divides the track between inactive and active.

The `endThumbCenter` argument is the offset of the center of the end thumb relative to the origin of the [PaintingContext.canvas]. It can be used as one point that divides the track between inactive and active.

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isEnabled}

{@macro flutter.material.RangeSliderThumbShape.getPreferredSize.isDiscrete}

The `textDirection` argument can be used to determine how the track segments are painted depending on whether they are on an active track segment or not.

{@macro flutter.material.RangeSliderTickMarkShape.paint.trackSegment}

### isRounded

```dart
bool get isRounded
```

Whether the track shape is rounded. This is used to determine the correct position of the thumbs in relation to the track. Defaults to false.

# BaseRangeSliderTrackShape

```dart
mixin BaseRangeSliderTrackShape {}
```

Base range slider track shape that provides an implementation of [getPreferredRect] for default sizing.

The height is set from [SliderThemeData.trackHeight] and the width of the parent box less the larger of the widths of [SliderThemeData.rangeThumbShape] and [SliderThemeData.overlayShape].

See also:

- [RectangularRangeSliderTrackShape], which is a track shape with sharp rectangular edges

### getPreferredRect()

```dart
Rect getPreferredRect({required RenderBox parentBox, Offset offset = Offset.zero, required SliderThemeData sliderTheme, bool isEnabled = false, bool isDiscrete = false})
```

Returns a rect that represents the track bounds that fits within the [Slider].

The width is the width of the [RangeSlider], but padded by the max of the overlay and thumb radius. The height is defined by the [SliderThemeData.trackHeight].

The [Rect] is centered both horizontally and vertically within the slider bounds.

# RectangularRangeSliderTrackShape

```dart
class RectangularRangeSliderTrackShape extends RangeSliderTrackShape with BaseRangeSliderTrackShape {}
```

A [RangeSlider] track that's a simple rectangle.

It paints a solid colored rectangle, vertically centered in the `parentBox`. The track rectangle extends to the bounds of the `parentBox`, but is padded by the [RoundSliderOverlayShape] radius. The height is defined by the [SliderThemeData.trackHeight]. The color is determined by the [Slider]'s enabled state and the track segment's active state which are defined by: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

{@macro flutter.material.RangeSliderTickMarkShape.paint.trackSegment}

![A range slider widget, consisting of 5 divisions and showing the rectangular range slider track shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rectangular_range_slider_track_shape.png)

See also:

- [RangeSlider], for the component that is meant to display this shape.
- [SliderThemeData], where an instance of this class is set to inform the slider of the visual details of the its track.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RoundedRectRangeSliderTrackShape], for a similar track with rounded edges.

### RectangularRangeSliderTrackShape()

```dart
RectangularRangeSliderTrackShape()
```

Create a slider track with rectangular outer edges.

The middle track segment is the selected range and is active, and the two outer track segments are inactive.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double>? enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled = false, bool isDiscrete = false, required TextDirection textDirection})
```

# RoundedRectRangeSliderTrackShape

```dart
class RoundedRectRangeSliderTrackShape extends RangeSliderTrackShape with BaseRangeSliderTrackShape {}
```

The default shape of a [RangeSlider]'s track.

It paints a solid colored rectangle with rounded edges, vertically centered in the `parentBox`. The track rectangle extends to the bounds of the `parentBox`, but is padded by the larger of [RoundSliderOverlayShape]'s radius and [RoundRangeSliderThumbShape]'s radius. The height is defined by the [SliderThemeData.trackHeight]. The color is determined by the [RangeSlider]'s enabled state and the track segment's active state which are defined by: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

{@macro flutter.material.RangeSliderTickMarkShape.paint.trackSegment}

![A range slider widget, consisting of 5 divisions and showing the rounded rect range slider track shape.](https://flutter.github.io/assets-for-api-docs/assets/material/rounded_rect_range_slider_track_shape.png)

See also:

- [RangeSlider], for the component that is meant to display this shape.
- [SliderThemeData], where an instance of this class is set to inform the slider of the visual details of the its track.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RectangularRangeSliderTrackShape], for a similar track with sharp edges.

### RoundedRectRangeSliderTrackShape()

```dart
RoundedRectRangeSliderTrackShape()
```

Create a slider track with rounded outer edges.

The middle track segment is the selected range and is active, and the two outer track segments are inactive.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled = false, bool isDiscrete = false, required TextDirection textDirection, double additionalActiveTrackHeight = 2})
```

### isRounded

```dart
bool get isRounded
```

# RoundRangeSliderTickMarkShape

```dart
class RoundRangeSliderTickMarkShape extends RangeSliderTickMarkShape {}
```

The default shape of each [RangeSlider] tick mark.

Tick marks are only displayed if the slider is discrete, which can be done by setting the [RangeSlider.divisions] to an integer value.

It paints a solid circle, centered on the track. The color is determined by the [Slider]'s enabled state and track's active states. These colors are defined in: [SliderThemeData.activeTrackColor], [SliderThemeData.inactiveTrackColor], [SliderThemeData.disabledActiveTrackColor], [SliderThemeData.disabledInactiveTrackColor].

![A slider widget, consisting of 5 divisions and showing the round range slider tick mark shape.](https://flutter.github.io/assets-for-api-docs/assets/material/round_range_slider_tick_mark_shape.png)

See also:

- [RangeSlider], which includes tick marks defined by this shape.
- [SliderTheme], which can be used to configure the tick mark shape of all sliders in a widget subtree.

### RoundRangeSliderTickMarkShape()

```dart
RoundRangeSliderTickMarkShape({double? tickMarkRadius})
```

Create a range slider tick mark that draws a circle.

### tickMarkRadius

```dart
double? tickMarkRadius
```

The preferred radius of the round tick mark.

If it is not provided, then 1/4 of the [SliderThemeData.trackHeight] is used.

### getPreferredSize()

```dart
Size getPreferredSize({required SliderThemeData sliderTheme, bool isEnabled = false})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled = false, required TextDirection textDirection})
```

# RoundRangeSliderThumbShape

```dart
class RoundRangeSliderThumbShape extends RangeSliderThumbShape {}
```

The default shape of a [RangeSlider]'s thumbs.

There is a shadow for the resting and pressed state.

![A slider widget, consisting of 5 divisions and showing the round range slider thumb shape.](https://flutter.github.io/assets-for-api-docs/assets/material/round_range_slider_thumb_shape.png)

See also:

- [RangeSlider], which includes thumbs defined by this shape.
- [SliderTheme], which can be used to configure the thumb shapes of all range sliders in a widget subtree.

### RoundRangeSliderThumbShape()

```dart
RoundRangeSliderThumbShape({double enabledThumbRadius = 10.0, double? disabledThumbRadius, double elevation = 1.0, double pressedElevation = 6.0})
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

If no disabledRadius is provided, then it is equal to the [enabledThumbRadius].

### elevation

```dart
double elevation
```

The resting elevation adds shadow to the unpressed thumb.

The default is 1.

### pressedElevation

```dart
double pressedElevation
```

The pressed elevation adds shadow to the pressed thumb.

The default is 6.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool isDiscrete = false, bool isEnabled = false, bool? isOnTop, required SliderThemeData sliderTheme, TextDirection? textDirection, Thumb? thumb, bool? isPressed})
```

# RangeThumbSelector

```dart
typedef RangeThumbSelector = Thumb? Function(TextDirection textDirection, RangeValues values, double tapValue, Size thumbSize, Size trackSize, double dx)
```

Decides which thumbs (if any) should be selected.

The default finds the closest thumb, but if the thumbs are close to each other, it waits for movement defined by [dx] to determine the selected thumb.

Override [SliderThemeData.thumbSelector] for custom thumb selection.

# RangeValues

```dart
class RangeValues {}
```

Object for representing range slider thumb values.

This object is passed into [RangeSlider.values] to set its values, and it is emitted in [RangeSlider.onChanged], [RangeSlider.onChangeStart], and [RangeSlider.onChangeEnd] when the values change.

### RangeValues()

```dart
RangeValues(double start, double end)
```

Creates pair of start and end values.

### start

```dart
double start
```

The value of the start thumb.

For LTR text direction, the start is the left thumb, and for RTL text direction, the start is the right thumb.

### end

```dart
double end
```

The value of the end thumb.

For LTR text direction, the end is the right thumb, and for RTL text direction, the end is the left thumb.

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

# RangeLabels

```dart
class RangeLabels {}
```

Object for setting range slider label values that appear in the value indicator for each thumb.

Used in combination with [SliderThemeData.showValueIndicator] to display labels above the thumbs.

### RangeLabels()

```dart
RangeLabels(String start, String end)
```

Creates pair of start and end labels.

### start

```dart
String start
```

The label of the start thumb.

For LTR text direction, the start is the left thumb, and for RTL text direction, the start is the right thumb.

### end

```dart
String end
```

The label of the end thumb.

For LTR text direction, the end is the right thumb, and for RTL text direction, the end is the left thumb.

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

# GappedRangeSliderTrackShape

```dart
class GappedRangeSliderTrackShape extends RangeSliderTrackShape with BaseRangeSliderTrackShape {}
```

The [GappedRangeSliderTrackShape] consists of active and inactive tracks. The active track uses the [SliderThemeData.activeTrackColor] and the inactive tracks uses the [SliderThemeData.inactiveTrackColor].

The track shape uses circular corner radius for the edge corners and a corner radius of 2 pixels for the inside corners.

Between the active and inactive tracks there are gaps of size [SliderThemeData.trackGap]. If the [SliderThemeData.thumbShape] is [HandleRangeSliderThumbShape] and the thumb is pressed, the thumb's width is reduced; as a result, the track gaps size in [GappedRangeSliderTrackShape] is also reduced.

If [SliderThemeData.trackGap] is null, then the track gaps size defaults to 6 pixels.

If [ThemeData.useMaterial3] is true and [RangeSlider.year2023] is false, then the [RangeSlider] will use [GappedRangeSliderTrackShape] as the default track shape.

See also:

- [RangeSlider], which includes a track defined by this shape.
- [SliderTheme], which can be used to configure the track shape of all range sliders in a widget subtree.

### GappedRangeSliderTrackShape()

```dart
GappedRangeSliderTrackShape()
```

Create a range slider track that draws 3 rounded rectangles with rounded outer edges.

### paint()

```dart
void paint(PaintingContext context, Offset offset, {required RenderBox parentBox, required SliderThemeData sliderTheme, required Animation<double> enableAnimation, required Offset startThumbCenter, required Offset endThumbCenter, bool isEnabled = false, bool isDiscrete = false, required TextDirection textDirection, double additionalActiveTrackHeight = 2})
```

### isRounded

```dart
bool get isRounded
```

# HandleRangeSliderThumbShape

```dart
class HandleRangeSliderThumbShape extends RangeSliderThumbShape {}
```

The bar shape of [RangeSlider]'s thumbs.

When the range slider is enabled, the [ColorScheme.primary] color is used for the thumb. When the slider is disabled, the [ColorScheme.onSurface] color with an opacity of 0.38 is used for the thumb.

The thumb bar shape width is reduced when the thumb is pressed.

If [SliderThemeData.thumbSize] is null, then the thumb size is 4 pixels for the width and 44 pixels for the height.

If [ThemeData.useMaterial3] is true and [RangeSlider.year2023] is false, then the [RangeSlider] will use [HandleRangeSliderThumbShape] as the default track shape.

See also:

- [RangeSlider], which includes thumbs defined by this shape.
- [SliderTheme], which can be used to configure the thumbs shape of all range sliders in a widget subtree.

### HandleRangeSliderThumbShape()

```dart
HandleRangeSliderThumbShape()
```

Create a range slider thumb that draws a bar.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete)
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool isDiscrete = false, bool isEnabled = false, bool? isOnTop, required SliderThemeData sliderTheme, TextDirection? textDirection, Thumb? thumb, bool? isPressed})
```

# RoundedRectRangeSliderValueIndicatorShape

```dart
class RoundedRectRangeSliderValueIndicatorShape extends RangeSliderValueIndicatorShape {}
```

The rounded rectangle shape of a [RangeSlider]'s value indicators.

If the [SliderThemeData.valueIndicatorColor] is null, then the shape uses the [ColorScheme.inverseSurface] color to draw the value indicator.

If the [SliderThemeData.valueIndicatorTextStyle] is null, then the indicator label text style defaults to [TextTheme.labelMedium] with the color set to [ColorScheme.onInverseSurface]. If the [ThemeData.useMaterial3] is set to false, then the indicator label text style defaults to [TextTheme.bodyLarge] with the color set to [ColorScheme.onInverseSurface].

If the [SliderThemeData.valueIndicatorStrokeColor] is provided, then the value indicator is drawn with a stroke border with the color provided.

If [ThemeData.useMaterial3] is true and [RangeSlider.year2023] is false, then the [RangeSlider] will use [RoundedRectRangeSliderValueIndicatorShape] as the default value indicators shape.

See also:

- [RangeSlider], which includes value indicators defined by this shape.
- [SliderTheme], which can be used to configure the range slider value indicators of all range sliders in a widget subtree.

### RoundedRectRangeSliderValueIndicatorShape()

```dart
RoundedRectRangeSliderValueIndicatorShape()
```

Create range slider value indicators that resembles a rounded rectangle.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool? isDiscrete, bool? isOnTop, required TextPainter labelPainter, double? textScaleFactor, Size? sizeWithOverflow, required RenderBox parentBox, required SliderThemeData sliderTheme, TextDirection? textDirection, double? value, Thumb? thumb})
```

# DropRangeSliderValueIndicatorShape

```dart
class DropRangeSliderValueIndicatorShape extends RangeSliderValueIndicatorShape {}
```

The shape of a Material 3 [RangeSlider]'s value indicators.

If the [SliderThemeData.valueIndicatorColor] is null, then the shape uses the [ColorScheme.primary] color to draw the value indicator.

If the [SliderThemeData.valueIndicatorTextStyle] is null, then the indicator label text style defaults to [TextTheme.labelMedium] with the color set to [ColorScheme.onPrimary]. If the [ThemeData.useMaterial3] is set to false, then the indicator label text style defaults to [TextTheme.bodyLarge] with the color set to [ColorScheme.onInverseSurface].

If the [SliderThemeData.valueIndicatorStrokeColor] is provided, then the value indicator is drawn with a stroke border with the color provided.

See also:

- [RangeSlider], which includes value indicators defined by this shape.
- [SliderTheme], which can be used to configure the range slider value indicators of all range sliders in a widget subtree.

### DropRangeSliderValueIndicatorShape()

```dart
DropRangeSliderValueIndicatorShape()
```

Create a range slider value indicator that resembles a drop shape.

### getPreferredSize()

```dart
Size getPreferredSize(bool isEnabled, bool isDiscrete, {TextPainter? labelPainter, double? textScaleFactor})
```

### paint()

```dart
void paint(PaintingContext context, Offset center, {required Animation<double> activationAnimation, required Animation<double> enableAnimation, bool? isDiscrete, bool? isOnTop, required TextPainter labelPainter, double? textScaleFactor, Size? sizeWithOverflow, required RenderBox parentBox, required SliderThemeData sliderTheme, TextDirection? textDirection, double? value, Thumb? thumb})
```
