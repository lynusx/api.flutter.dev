@docImport 'color_scheme.dart'; @docImport 'range_slider.dart'; @docImport 'text_theme.dart';

# SliderTheme

```dart
class SliderTheme extends InheritedTheme {}
```

Applies a slider theme to descendant [Slider] widgets.

A slider theme describes the colors and shape choices of the slider components.

Descendant widgets obtain the current theme's [SliderThemeData] object using [SliderTheme.of]. When a widget uses [SliderTheme.of], it is automatically rebuilt if the theme later changes.

The slider is as big as the largest of the [SliderComponentShape.getPreferredSize] of the thumb shape, the [SliderComponentShape.getPreferredSize] of the overlay shape, and the [SliderTickMarkShape.getPreferredSize] of the tick mark shape.

See also:

- [SliderThemeData], which describes the actual configuration of a slider theme.
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.
- [SliderTrackShape], which can be used to create custom shapes for the [Slider]'s track.
- [SliderTickMarkShape], which can be used to create custom shapes for the [Slider]'s tick marks.
- [RangeSliderThumbShape], which can be used to create custom shapes for the [RangeSlider]'s thumb.
- [RangeSliderValueIndicatorShape], which can be used to create custom shapes for the [RangeSlider]'s value indicator.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RangeSliderTickMarkShape], which can be used to create custom shapes for the [RangeSlider]'s tick marks.

### SliderTheme()

```dart
SliderTheme({dynamic key, required SliderThemeData data, required dynamic child})
```

Applies the given theme [data] to [child].

### data

```dart
SliderThemeData data
```

Specifies the color and shape values for descendant slider widgets.

### of()

```dart
SliderThemeData of(BuildContext context)
```

Returns the data from the closest [SliderTheme] instance that encloses the given context.

Defaults to the ambient [ThemeData.sliderTheme] if there is no [SliderTheme] in the given build context.

{@tool snippet}

```dart
class Launch extends StatefulWidget {
  const Launch({super.key});

  @override
  State createState() => LaunchState();
}

class LaunchState extends State<Launch> {
  double _rocketThrust = 0;

  @override
  Widget build(BuildContext context) {
    return SliderTheme(
      data: SliderTheme.of(context).copyWith(activeTrackColor: const Color(0xff804040)),
      child: Slider(
        onChanged: (double value) { setState(() { _rocketThrust = value; }); },
        value: _rocketThrust,
      ),
    );
  }
}
```

{@end-tool}

See also:

- [SliderThemeData], which describes the actual configuration of a slider theme.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SliderTheme oldWidget)
```

# ShowValueIndicator

```dart
enum ShowValueIndicator {}
```

Describes the conditions under which the value indicator on a [Slider] will be shown. Used in [Slider.showValueIndicator] and [SliderThemeData.showValueIndicator].

See also:

- [Slider], a Material Design slider widget.
- [SliderThemeData], which describes the actual configuration of a slider theme.

The value indicator will only be shown while dragging for discrete sliders (sliders where [Slider.divisions] is non-null).

The value indicator will only be shown while dragging for continuous sliders (sliders where [Slider.divisions] is null).

The value indicator is shown while dragging.

The value indicator is shown while dragging.

The value indicator is always displayed as long as the slider has a [Slider.onChanged] callback.

The value indicator will never be shown.

# Thumb

```dart
enum Thumb {}
```

Identifier for a thumb.

There are 2 thumbs in a [RangeSlider], [start] and [end].

For [TextDirection.ltr], the [start] thumb is the left-most thumb and the [end] thumb is the right-most thumb. For [TextDirection.rtl] the [start] thumb is the right-most thumb, and the [end] thumb is the left-most thumb.

Left-most thumb for [TextDirection.ltr], otherwise, right-most thumb.

Right-most thumb for [TextDirection.ltr], otherwise, left-most thumb.

# SliderThemeData

```dart
class SliderThemeData with Diagnosticable {}
```

Overrides the default values of visual properties for descendant [Slider] widgets.

Descendant widgets obtain the current [SliderThemeData] object with [SliderTheme.of]. Instances of [SliderThemeData] can be customized with [SliderThemeData.copyWith].

Typically a [SliderThemeData] is specified as part of the overall [Theme] with [ThemeData.sliderTheme].

This theme is for both the [Slider] and the [RangeSlider]. The properties that are only for the [Slider] are: [tickMarkShape], [thumbShape], [trackShape], and [valueIndicatorShape]. The properties that are only for the [RangeSlider] are [rangeTickMarkShape], [rangeThumbShape], [rangeTrackShape], [rangeValueIndicatorShape], [overlappingShapeStrokeColor], [minThumbSeparation], and [thumbSelector]. All other properties are used by both the [Slider] and the [RangeSlider].

The parts of a slider are:

- The "thumb", which is a shape that slides horizontally when the user drags it.
- The "track", which is the line that the slider thumb slides along.
- The "tick marks", which are regularly spaced marks that are drawn when using discrete divisions.
- The "value indicator", which appears when the user is dragging the thumb to indicate the value being selected.
- The "overlay", which appears around the thumb, and is shown when the thumb is pressed, focused, or hovered. It is painted underneath the thumb, so it must extend beyond the bounds of the thumb itself to actually be visible.
- The "active" side of the slider is the side between the thumb and the minimum value.
- The "inactive" side of the slider is the side between the thumb and the maximum value.
- The [Slider] is disabled when it is not accepting user input. See [Slider] for details on when this happens.

The thumb, track, tick marks, value indicator, and overlay can be customized by creating subclasses of [SliderTrackShape], [SliderComponentShape], and/or [SliderTickMarkShape]. See [RoundSliderThumbShape], [RectangularSliderTrackShape], [RoundSliderTickMarkShape], [RectangularSliderValueIndicatorShape], and [RoundSliderOverlayShape] for examples.

The track painting can be skipped by specifying 0 for [trackHeight]. The thumb painting can be skipped by specifying [SliderComponentShape.noThumb] for [SliderThemeData.thumbShape]. The overlay painting can be skipped by specifying [SliderComponentShape.noOverlay] for [SliderThemeData.overlayShape]. The tick mark painting can be skipped by specifying [SliderTickMarkShape.noTickMark] for [SliderThemeData.tickMarkShape]. The value indicator painting can be skipped by specifying the appropriate [ShowValueIndicator] for [SliderThemeData.showValueIndicator].

See also:

- [SliderTheme] widget, which can override the slider theme of its children.
- [Theme] widget, which performs a similar function to [SliderTheme], but for overall themes.
- [ThemeData], which has a default [SliderThemeData].
- [SliderComponentShape], which can be used to create custom shapes for the [Slider]'s thumb, overlay, and value indicator and the [RangeSlider]'s overlay.
- [SliderTrackShape], which can be used to create custom shapes for the [Slider]'s track.
- [SliderTickMarkShape], which can be used to create custom shapes for the [Slider]'s tick marks.
- [RangeSliderThumbShape], which can be used to create custom shapes for the [RangeSlider]'s thumb.
- [RangeSliderValueIndicatorShape], which can be used to create custom shapes for the [RangeSlider]'s value indicator.
- [RangeSliderTrackShape], which can be used to create custom shapes for the [RangeSlider]'s track.
- [RangeSliderTickMarkShape], which can be used to create custom shapes for the [RangeSlider]'s tick marks.

### SliderThemeData()

```dart
SliderThemeData({double? trackHeight, Color? activeTrackColor, Color? inactiveTrackColor, Color? secondaryActiveTrackColor, Color? disabledActiveTrackColor, Color? disabledInactiveTrackColor, Color? disabledSecondaryActiveTrackColor, Color? activeTickMarkColor, Color? inactiveTickMarkColor, Color? disabledActiveTickMarkColor, Color? disabledInactiveTickMarkColor, Color? thumbColor, Color? overlappingShapeStrokeColor, Color? disabledThumbColor, Color? overlayColor, Color? valueIndicatorColor, Color? valueIndicatorStrokeColor, SliderComponentShape? overlayShape, SliderTickMarkShape? tickMarkShape, SliderComponentShape? thumbShape, SliderTrackShape? trackShape, SliderComponentShape? valueIndicatorShape, RangeSliderTickMarkShape? rangeTickMarkShape, RangeSliderThumbShape? rangeThumbShape, RangeSliderTrackShape? rangeTrackShape, RangeSliderValueIndicatorShape? rangeValueIndicatorShape, ShowValueIndicator? showValueIndicator, TextStyle? valueIndicatorTextStyle, double? minThumbSeparation, RangeThumbSelector? thumbSelector, WidgetStateProperty<MouseCursor?>? mouseCursor, SliderInteraction? allowedInteraction, EdgeInsetsGeometry? padding, WidgetStateProperty<Size?>? thumbSize, double? trackGap, bool? year2023})
```

Create a [SliderThemeData] given a set of exact values.

This will rarely be used directly. It is used by [lerp] to create intermediate themes based on two themes.

The simplest way to create a SliderThemeData is to use [copyWith] on the one you get from [SliderTheme.of], or create an entirely new one with [SliderThemeData.fromPrimaryColors].

{@tool snippet}

```dart
class Blissful extends StatefulWidget {
  const Blissful({super.key});

  @override
  State createState() => BlissfulState();
}

class BlissfulState extends State<Blissful> {
  double _bliss = 0;

  @override
  Widget build(BuildContext context) {
    return SliderTheme(
      data: SliderTheme.of(context).copyWith(activeTrackColor: const Color(0xff404080)),
      child: Slider(
        onChanged: (double value) { setState(() { _bliss = value; }); },
        value: _bliss,
      ),
    );
  }
}
```

{@end-tool}

### SliderThemeData.fromPrimaryColors()

```dart
SliderThemeData.fromPrimaryColors({required Color primaryColor, required Color primaryColorDark, required Color primaryColorLight, required TextStyle valueIndicatorTextStyle})
```

Generates a SliderThemeData from three main colors.

Usually these are the primary, dark and light colors from a [ThemeData].

The opacities of these colors will be overridden with the Material Design defaults when assigning them to the slider theme component colors.

This is used to generate the default slider theme for a [ThemeData].

### trackHeight

```dart
double? trackHeight
```

The height of the [Slider] track.

### activeTrackColor

```dart
Color? activeTrackColor
```

The color of the [Slider] track between the [Slider.min] position and the current thumb position.

### inactiveTrackColor

```dart
Color? inactiveTrackColor
```

The color of the [Slider] track between the current thumb position and the [Slider.max] position.

### secondaryActiveTrackColor

```dart
Color? secondaryActiveTrackColor
```

The color of the [Slider] track between the current thumb position and the [Slider.secondaryTrackValue] position.

### disabledActiveTrackColor

```dart
Color? disabledActiveTrackColor
```

The color of the [Slider] track between the [Slider.min] position and the current thumb position when the [Slider] is disabled.

### disabledSecondaryActiveTrackColor

```dart
Color? disabledSecondaryActiveTrackColor
```

The color of the [Slider] track between the current thumb position and the [Slider.secondaryTrackValue] position when the [Slider] is disabled.

### disabledInactiveTrackColor

```dart
Color? disabledInactiveTrackColor
```

The color of the [Slider] track between the current thumb position and the [Slider.max] position when the [Slider] is disabled.

### activeTickMarkColor

```dart
Color? activeTickMarkColor
```

The color of the track's tick marks that are drawn between the [Slider.min] position and the current thumb position.

### inactiveTickMarkColor

```dart
Color? inactiveTickMarkColor
```

The color of the track's tick marks that are drawn between the current thumb position and the [Slider.max] position.

### disabledActiveTickMarkColor

```dart
Color? disabledActiveTickMarkColor
```

The color of the track's tick marks that are drawn between the [Slider.min] position and the current thumb position when the [Slider] is disabled.

### disabledInactiveTickMarkColor

```dart
Color? disabledInactiveTickMarkColor
```

The color of the track's tick marks that are drawn between the current thumb position and the [Slider.max] position when the [Slider] is disabled.

### thumbColor

```dart
Color? thumbColor
```

The color given to the [thumbShape] to draw itself with.

### overlappingShapeStrokeColor

```dart
Color? overlappingShapeStrokeColor
```

The color given to the perimeter of the top [rangeThumbShape] when the thumbs are overlapping and the top [rangeValueIndicatorShape] when the value indicators are overlapping.

### disabledThumbColor

```dart
Color? disabledThumbColor
```

The color given to the [thumbShape] to draw itself with when the [Slider] is disabled.

### overlayColor

```dart
Color? overlayColor
```

The color of the overlay drawn around the slider thumb when it is pressed, focused, or hovered.

This is typically a semi-transparent color.

### valueIndicatorColor

```dart
Color? valueIndicatorColor
```

The color given to the [valueIndicatorShape] to draw itself with.

### valueIndicatorStrokeColor

```dart
Color? valueIndicatorStrokeColor
```

The color given to the [valueIndicatorShape] stroke.

### overlayShape

```dart
SliderComponentShape? overlayShape
```

The shape that will be used to draw the [Slider]'s overlay.

Both the [overlayColor] and a non default [overlayShape] may be specified. The default [overlayShape] refers to the [overlayColor].

The default value is [RoundSliderOverlayShape].

### tickMarkShape

```dart
SliderTickMarkShape? tickMarkShape
```

The shape that will be used to draw the [Slider]'s tick marks.

The [SliderTickMarkShape.getPreferredSize] is used to help determine the location of each tick mark on the track. The slider's minimum size will be at least this big.

The default value is [RoundSliderTickMarkShape].

See also:

- [RoundRangeSliderTickMarkShape], which is the default tick mark shape for the range slider.

### thumbShape

```dart
SliderComponentShape? thumbShape
```

The shape that will be used to draw the [Slider]'s thumb.

The default value is [RoundSliderThumbShape].

See also:

- [RoundRangeSliderThumbShape], which is the default thumb shape for the [RangeSlider].

### trackShape

```dart
SliderTrackShape? trackShape
```

The shape that will be used to draw the [Slider]'s track.

The [SliderTrackShape.getPreferredRect] method is used to map slider-relative gesture coordinates to the correct thumb position on the track. It is also used to horizontally position tick marks, when the slider is discrete.

The default value is [RoundedRectSliderTrackShape].

See also:

- [RoundedRectRangeSliderTrackShape], which is the default track shape for the [RangeSlider].

### valueIndicatorShape

```dart
SliderComponentShape? valueIndicatorShape
```

The shape that will be used to draw the [Slider]'s value indicator.

The default value is [PaddleSliderValueIndicatorShape].

See also:

- [PaddleRangeSliderValueIndicatorShape], which is the default value indicator shape for the [RangeSlider].

### rangeTickMarkShape

```dart
RangeSliderTickMarkShape? rangeTickMarkShape
```

The shape that will be used to draw the [RangeSlider]'s tick marks.

The [RangeSliderTickMarkShape.getPreferredSize] is used to help determine the location of each tick mark on the track. The slider's minimum size will be at least this big.

The default value is [RoundRangeSliderTickMarkShape].

See also:

- [RoundSliderTickMarkShape], which is the default tick mark shape for the [Slider].

### rangeThumbShape

```dart
RangeSliderThumbShape? rangeThumbShape
```

The shape that will be used for the [RangeSlider]'s thumbs.

By default the same shape is used for both thumbs, but strokes the top thumb when it overlaps the bottom thumb. The top thumb is always the last selected thumb.

The default value is [RoundRangeSliderThumbShape].

See also:

- [RoundSliderThumbShape], which is the default thumb shape for the [Slider].

### rangeTrackShape

```dart
RangeSliderTrackShape? rangeTrackShape
```

The shape that will be used to draw the [RangeSlider]'s track.

The [SliderTrackShape.getPreferredRect] method is used to map slider-relative gesture coordinates to the correct thumb position on the track. It is also used to horizontally position the tick marks, when the slider is discrete.

The default value is [RoundedRectRangeSliderTrackShape].

See also:

- [RoundedRectSliderTrackShape], which is the default track shape for the [Slider].

### rangeValueIndicatorShape

```dart
RangeSliderValueIndicatorShape? rangeValueIndicatorShape
```

The shape that will be used for the [RangeSlider]'s value indicators.

The default shape uses the same value indicator for each thumb, but strokes the top value indicator when it overlaps the bottom value indicator. The top indicator corresponds to the top thumb, which is always the most recently selected thumb.

The default value is [PaddleRangeSliderValueIndicatorShape].

See also:

- [PaddleSliderValueIndicatorShape], which is the default value indicator shape for the [Slider].

### showValueIndicator

```dart
ShowValueIndicator? showValueIndicator
```

Whether the value indicator should be shown for different types of sliders.

By default, [showValueIndicator] is set to [ShowValueIndicator.onlyForDiscrete]. The value indicator is only shown when the thumb is being touched.

### valueIndicatorTextStyle

```dart
TextStyle? valueIndicatorTextStyle
```

The text style for the text on the value indicator.

### minThumbSeparation

```dart
double? minThumbSeparation
```

Limits the thumb's separation distance.

Use this only if you want to control the visual appearance of the thumbs in terms of a logical pixel value. This can be done when you want a specific look for thumbs when they are close together. To limit with the real values, rather than logical pixels, the values can be restricted by the parent.

### thumbSelector

```dart
RangeThumbSelector? thumbSelector
```

Determines which thumb should be selected when the slider is interacted with.

If null, the default thumb selector finds the closest thumb, excluding taps that are between the thumbs and not within any one touch target. When the selection is within the touch target bounds of both thumbs, no thumb is selected until the selection is moved.

Override this for custom thumb selection.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.slider.mouseCursor}

If specified, overrides the default value of [Slider.mouseCursor].

### allowedInteraction

```dart
SliderInteraction? allowedInteraction
```

Allowed way for the user to interact with the [Slider].

If specified, overrides the default value of [Slider.allowedInteraction].

### padding

```dart
EdgeInsetsGeometry? padding
```

Determines the padding around the [Slider].

If specified, this padding overrides the default vertical padding of the [Slider], defaults to the height of the overlay shape, and the horizontal padding, defaults to the width of the thumb shape or overlay shape, whichever is larger.

### thumbSize

```dart
WidgetStateProperty<Size?>? thumbSize
```

The size of the [HandleThumbShape] thumb.

If [SliderThemeData.thumbShape] is [HandleThumbShape], this property is used to set the size of the thumb. Otherwise, the default thumb size is 4 pixels for the width and 44 pixels for the height.

### trackGap

```dart
double? trackGap
```

The size of the gap between the active and inactive tracks of the [GappedSliderTrackShape].

If [SliderThemeData.trackShape] is [GappedSliderTrackShape], this property is used to set the gap between the active and inactive tracks. Otherwise, the default gap size is 6.0 pixels.

The Slider defaults to [GappedSliderTrackShape] when the track shape is not specified, and the [trackGap] can be used to adjust the gap size.

If [Slider.year2023] is true or [ThemeData.useMaterial3] is false, then the Slider track shape defaults to [RoundedRectSliderTrackShape] and the [trackGap] is ignored. In this case, set the track shape to [GappedSliderTrackShape] to use the [trackGap].

Defaults to 6.0 pixels of gap between the active and inactive tracks.

### year2023

```dart
bool? year2023
```

Overrides the default value of [Slider.year2023] and [RangeSlider.year2023].

When true, the [Slider] and [RangeSlider] will use the 2023 Material Design 3 appearance. Defaults to true.

If this is set to false, the [Slider] and [RangeSlider] will use the latest Material Design 3 appearance, which was introduced in December 2023.

If [ThemeData.useMaterial3] is false, then this property is ignored.

### copyWith()

```dart
SliderThemeData copyWith({double? trackHeight, Color? activeTrackColor, Color? inactiveTrackColor, Color? secondaryActiveTrackColor, Color? disabledActiveTrackColor, Color? disabledInactiveTrackColor, Color? disabledSecondaryActiveTrackColor, Color? activeTickMarkColor, Color? inactiveTickMarkColor, Color? disabledActiveTickMarkColor, Color? disabledInactiveTickMarkColor, Color? thumbColor, Color? overlappingShapeStrokeColor, Color? disabledThumbColor, Color? overlayColor, Color? valueIndicatorColor, Color? valueIndicatorStrokeColor, SliderComponentShape? overlayShape, SliderTickMarkShape? tickMarkShape, SliderComponentShape? thumbShape, SliderTrackShape? trackShape, SliderComponentShape? valueIndicatorShape, RangeSliderTickMarkShape? rangeTickMarkShape, RangeSliderThumbShape? rangeThumbShape, RangeSliderTrackShape? rangeTrackShape, RangeSliderValueIndicatorShape? rangeValueIndicatorShape, ShowValueIndicator? showValueIndicator, TextStyle? valueIndicatorTextStyle, double? minThumbSeparation, RangeThumbSelector? thumbSelector, WidgetStateProperty<MouseCursor?>? mouseCursor, SliderInteraction? allowedInteraction, EdgeInsetsGeometry? padding, WidgetStateProperty<Size?>? thumbSize, double? trackGap, bool? year2023})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
SliderThemeData lerp(SliderThemeData a, SliderThemeData b, double t)
```

Linearly interpolate between two slider themes.

{@macro dart.ui.shadow.lerp}

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SemanticFormatterCallback

```dart
typedef SemanticFormatterCallback = String Function(double value)
```

A callback that formats a numeric value from a [Slider] or [RangeSlider] widget.

See also:

- [Slider.semanticFormatterCallback], which shows an example use case.
- [RangeSlider.semanticFormatterCallback], which shows an example use case.
