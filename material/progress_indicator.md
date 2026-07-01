@docImport 'package:flutter/semantics.dart';

@docImport 'refresh_indicator.dart';

# ProgressIndicator

```dart
abstract class ProgressIndicator extends StatefulWidget {}
```

A base class for Material Design progress indicators.

This widget cannot be instantiated directly. For a linear progress indicator, see [LinearProgressIndicator]. For a circular progress indicator, see [CircularProgressIndicator].

See also:

- <https://material.io/components/progress-indicators>

### ProgressIndicator()

```dart
ProgressIndicator({dynamic key, double? value, Color? backgroundColor, Color? color, Animation<Color?>? valueColor, String? semanticsLabel, String? semanticsValue})
```

Creates a progress indicator.

{@template flutter.material.ProgressIndicator.ProgressIndicator} The [value] argument can either be null for an indeterminate progress indicator, or a non-null value between 0.0 and 1.0 for a determinate progress indicator.

## Accessibility

The [semanticsLabel] can be used to identify the purpose of this progress bar for screen reading software. The [semanticsValue] property may be used for determinate progress indicators to indicate how much progress has been made. {@endtemplate}

### value

```dart
double? value
```

If non-null, the value of this progress indicator.

A value of 0.0 means no progress and 1.0 means that progress is complete. The value will be clamped to be in the range 0.0-1.0.

If null, this progress indicator is indeterminate, which means the indicator displays a predetermined animation that does not indicate how much actual progress is being made.

### backgroundColor

```dart
Color? backgroundColor
```

The progress indicator's background color.

It is up to the subclass to implement this in whatever way makes sense for the given use case. See the subclass documentation for details.

### color

```dart
Color? color
```

{@template flutter.progress_indicator.ProgressIndicator.color} The progress indicator's color.

This is only used if [ProgressIndicator.valueColor] is null. If [ProgressIndicator.color] is also null, then the ambient [ProgressIndicatorThemeData.color] will be used. If that is null then the current theme's [ColorScheme.primary] will be used by default. {@endtemplate}

### valueColor

```dart
Animation<Color?>? valueColor
```

The progress indicator's color as an animated value.

If null, the progress indicator is rendered with [color]. If that is null, then it will use the ambient [ProgressIndicatorThemeData.color]. If that is also null then it defaults to the current theme's [ColorScheme.primary].

### semanticsLabel

```dart
String? semanticsLabel
```

{@template flutter.progress_indicator.ProgressIndicator.semanticsLabel} The [SemanticsProperties.label] for this progress indicator.

This value indicates the purpose of the progress bar, and will be read out by screen readers to indicate the purpose of this progress indicator. {@endtemplate}

### semanticsValue

```dart
String? semanticsValue
```

{@template flutter.progress_indicator.ProgressIndicator.semanticsValue} The [SemanticsProperties.value] for this progress indicator.

This will be used in conjunction with the [semanticsLabel] by screen reading software to identify the widget, and is primarily intended for use with determinate progress indicators to announce how far along they are.

For determinate progress indicators, this will be defaulted to [ProgressIndicator.value] expressed as a percentage, i.e. `0.1` will become '10%'. {@endtemplate}

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LinearProgressIndicator

```dart
class LinearProgressIndicator extends ProgressIndicator {}
```

A Material Design linear progress indicator, also known as a progress bar.

{@youtube 560 315 https://www.youtube.com/watch?v=O-rhXZLtpv0}

A widget that shows progress along a line. There are two kinds of linear progress indicators:

- _Determinate_. Determinate progress indicators have a specific value at each point in time, and the value should increase monotonically from 0.0 to 1.0, at which time the indicator is complete. To create a determinate progress indicator, use a non-null [value] between 0.0 and 1.0.
- _Indeterminate_. Indeterminate progress indicators do not have a specific value at each point in time and instead indicate that progress is being made without indicating how much progress remains. To create an indeterminate progress indicator, use a null [value].

The indicator line is displayed with [valueColor], an animated value. To specify a constant color value use: `AlwaysStoppedAnimation<Color>(color)`.

The minimum height of the indicator can be specified using [minHeight]. The indicator can be made taller by wrapping the widget with a [SizedBox].

{@tool dartpad} This example showcases determinate and indeterminate [LinearProgressIndicator]s. The [LinearProgressIndicator]s will use the ![updated Material 3 Design appearance](https://m3.material.io/components/progress-indicators/overview) when setting the [LinearProgressIndicator.year2023] flag to false.

** See code in examples/api/lib/material/progress_indicator/linear_progress_indicator.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of a [LinearProgressIndicator] with a changing value. When toggling the switch, [LinearProgressIndicator] uses a determinate value. As described in: https://m3.material.io/components/progress-indicators/overview

** See code in examples/api/lib/material/progress_indicator/linear_progress_indicator.1.dart ** {@end-tool}

{@macro flutter.material.ProgressIndicator.AnimationSynchronization}

See the documentation of [CircularProgressIndicator] for an example on this topic.

See also:

- [CircularProgressIndicator], which shows progress along a circular arc.
- [RefreshIndicator], which automatically displays a [CircularProgressIndicator] when the underlying vertical scrollable is overscrolled.
- <https://material.io/design/components/progress-indicators.html#linear-progress-indicators>

### LinearProgressIndicator()

```dart
LinearProgressIndicator({dynamic key, double? value, dynamic backgroundColor, dynamic color, dynamic valueColor, double? minHeight, String? semanticsLabel, String? semanticsValue, BorderRadiusGeometry? borderRadius, Color? stopIndicatorColor, double? stopIndicatorRadius, double? trackGap, bool? year2023, AnimationController? controller})
```

Creates a linear progress indicator.

{@macro flutter.material.ProgressIndicator.ProgressIndicator}

### backgroundColor

```dart
Color? get backgroundColor
```

{@template flutter.material.LinearProgressIndicator.trackColor} Color of the track being filled by the linear indicator.

If [LinearProgressIndicator.backgroundColor] is null then the ambient [ProgressIndicatorThemeData.linearTrackColor] will be used. If that is null, then the ambient theme's [ColorScheme.background] will be used to draw the track. {@endtemplate}

### minHeight

```dart
double? minHeight
```

{@template flutter.material.LinearProgressIndicator.minHeight} The minimum height of the line used to draw the linear indicator.

If [LinearProgressIndicator.minHeight] is null then it will use the ambient [ProgressIndicatorThemeData.linearMinHeight]. If that is null it will use 4dp. {@endtemplate}

### borderRadius

```dart
BorderRadiusGeometry? borderRadius
```

The border radius of both the indicator and the track.

If null, then the [ProgressIndicatorThemeData.borderRadius] will be used. If that is also null, then defaults to radius of 2, which produces a rounded shape with a rounded indicator. If [ThemeData.useMaterial3] is false, then defaults to [BorderRadius.zero], which produces a rectangular shape with a rectangular indicator.

### stopIndicatorColor

```dart
Color? stopIndicatorColor
```

The color of the stop indicator.

If [year2023] is true or [ThemeData.useMaterial3] is false, then no stop indicator will be drawn.

If null, then the [ProgressIndicatorThemeData.stopIndicatorColor] will be used. If that is null, then the [ColorScheme.primary] will be used.

### stopIndicatorRadius

```dart
double? stopIndicatorRadius
```

The radius of the stop indicator.

If [year2023] is true or [ThemeData.useMaterial3] is false, then no stop indicator will be drawn.

Set [stopIndicatorRadius] to 0 to hide the stop indicator.

If null, then the [ProgressIndicatorThemeData.stopIndicatorRadius] will be used. If that is null, then defaults to 2.

### trackGap

```dart
double? trackGap
```

The gap between the indicator and the track.

If [year2023] is true or [ThemeData.useMaterial3] is false, then no track gap will be drawn.

Set [trackGap] to 0 to hide the track gap.

If null, then the [ProgressIndicatorThemeData.trackGap] will be used. If that is null, then defaults to 4.

### year2023

```dart
bool? year2023
```

When true, the [LinearProgressIndicator] will use the 2023 Material Design 3 appearance.

If null, then the [ProgressIndicatorThemeData.year2023] will be used. If that is null, then defaults to true.

If this is set to false, the [LinearProgressIndicator] will use the latest Material Design 3 appearance, which was introduced in December 2023.

If [ThemeData.useMaterial3] is false, then this property is ignored.

### controller

```dart
AnimationController? controller
```

{@template flutter.material.ProgressIndicator.controller} An optional [AnimationController] that controls the animation of this indeterminate progress indicator.

This controller is only used when the indicator is indeterminate (i.e., when [value] is null). If this property is non-null, [value] must be null.

The controller's value is expected to be a linear progression from 0.0 to 1.0, which represents one full cycle of the indeterminate animation.

If this controller is null (and [value] is also null), the widget will look for a [ProgressIndicatorThemeData.controller]. If that is also null, the widget will create and manage its own internal [AnimationController] to drive the default indeterminate animation. {@endtemplate}

See also:

- [LinearProgressIndicator.defaultAnimationDuration], default duration for one full cycle of the indeterminate animation.

### defaultAnimationDuration

```dart
Duration defaultAnimationDuration
```

The default duration for one full cycle of the indeterminate animation.

This duration is used when the widget creates its own [AnimationController] because no [controller] was provided, either directly or through a [ProgressIndicatorTheme].

### createState()

```dart
State<LinearProgressIndicator> createState()
```

# CircularProgressIndicator

```dart
class CircularProgressIndicator extends ProgressIndicator {}
```

A Material Design circular progress indicator, which spins to indicate that the application is busy.

{@youtube 560 315 https://www.youtube.com/watch?v=O-rhXZLtpv0}

A widget that shows progress along a circle. There are two kinds of circular progress indicators:

- _Determinate_. Determinate progress indicators have a specific value at each point in time, and the value should increase monotonically from 0.0 to 1.0, at which time the indicator is complete. To create a determinate progress indicator, use a non-null [value] between 0.0 and 1.0.
- _Indeterminate_. Indeterminate progress indicators do not have a specific value at each point in time and instead indicate that progress is being made without indicating how much progress remains. To create an indeterminate progress indicator, use a null [value].

The indicator arc is displayed with [valueColor], an animated value. To specify a constant color use: `AlwaysStoppedAnimation<Color>(color)`.

{@tool dartpad} This example showcases determinate and indeterminate [CircularProgressIndicator]s. The [CircularProgressIndicator]s will use the ![updated Material 3 Design appearance](https://m3.material.io/components/progress-indicators/overview) when setting the [CircularProgressIndicator.year2023] flag to false.

** See code in examples/api/lib/material/progress_indicator/circular_progress_indicator.0.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of a [CircularProgressIndicator] with a changing value. When toggling the switch, [CircularProgressIndicator] uses a determinate value. As described in: https://m3.material.io/components/progress-indicators/overview

** See code in examples/api/lib/material/progress_indicator/circular_progress_indicator.1.dart ** {@end-tool}

{@template flutter.material.ProgressIndicator.AnimationSynchronization}

## Animation synchronization

When multiple [CircularProgressIndicator]s or [LinearProgressIndicator]s are animating on screen simultaneously (e.g., in a list of loading items), their uncoordinated animations can appear visually cluttered. To address this, the animation of an indicator can be driven by a custom [AnimationController].

This allows multiple indicators to be synchronized to a single animation source. The most convenient way to achieve this for a group of indicators is by providing a controller via [ProgressIndicatorTheme] (see [ProgressIndicatorThemeData.controller]). All [CircularProgressIndicator]s or [LinearProgressIndicator]s within that theme's subtree will then share the same animation, resulting in a more coordinated and visually pleasing effect.

Alternatively, a specific [AnimationController] can be passed directly to the [controller] property of an individual indicator. {@endtemplate}

{@tool dartpad} This sample demonstrates how to synchronize the indeterminate animations of multiple [CircularProgressIndicator]s using a [Theme].

Tapping the buttons adds or removes indicators. By default, they all share a [ProgressIndicatorThemeData.controller], which keeps their animations in sync.

Tapping the "Toggle" button sets the theme's controller to null. This forces each indicator to create its own internal controller, causing their animations to become desynchronized.

** See code in examples/api/lib/material/progress_indicator/circular_progress_indicator.2.dart ** {@end-tool}

See also:

- [LinearProgressIndicator], which displays progress along a line.
- [RefreshIndicator], which automatically displays a [CircularProgressIndicator] when the underlying vertical scrollable is overscrolled.
- <https://material.io/design/components/progress-indicators.html#circular-progress-indicators>

### CircularProgressIndicator()

```dart
CircularProgressIndicator({dynamic key, double? value, dynamic backgroundColor, dynamic color, dynamic valueColor, double? strokeWidth, double? strokeAlign, String? semanticsLabel, String? semanticsValue, StrokeCap? strokeCap, BoxConstraints? constraints, double? trackGap, bool? year2023, EdgeInsetsGeometry? padding, AnimationController? controller})
```

Creates a circular progress indicator.

{@macro flutter.material.ProgressIndicator.ProgressIndicator}

### CircularProgressIndicator.adaptive()

```dart
CircularProgressIndicator.adaptive({dynamic key, double? value, dynamic backgroundColor, dynamic valueColor, double? strokeWidth, String? semanticsLabel, String? semanticsValue, StrokeCap? strokeCap, double? strokeAlign, BoxConstraints? constraints, double? trackGap, bool? year2023, EdgeInsetsGeometry? padding, AnimationController? controller})
```

Creates an adaptive progress indicator that is a [CupertinoActivityIndicator] on [TargetPlatform.iOS] & [TargetPlatform.macOS] and a [CircularProgressIndicator] in material theme/non-Apple platforms.

The [valueColor], [strokeWidth], [strokeAlign], [strokeCap], [semanticsLabel], [semanticsValue], [trackGap], [year2023] will be ignored on iOS & macOS.

{@macro flutter.material.ProgressIndicator.ProgressIndicator}

### backgroundColor

```dart
Color? get backgroundColor
```

{@template flutter.material.CircularProgressIndicator.trackColor} Color of the circular track being filled by the circular indicator.

If [CircularProgressIndicator.backgroundColor] is null then the ambient [ProgressIndicatorThemeData.circularTrackColor] will be used. If that is null, then the track will not be painted. {@endtemplate}

### strokeWidth

```dart
double? strokeWidth
```

The width of the line used to draw the circle.

### strokeAlign

```dart
double? strokeAlign
```

The relative position of the stroke on a [CircularProgressIndicator].

Values typically range from -1.0 ([strokeAlignInside], inside stroke) to 1.0 ([strokeAlignOutside], outside stroke), without any bound constraints (e.g., a value of -2.0 is not typical, but allowed). A value of 0 ([strokeAlignCenter]) will center the border on the edge of the widget.

If [year2023] is true, then the default value is [strokeAlignCenter]. Otherwise, the default value is [strokeAlignInside].

### strokeCap

```dart
StrokeCap? strokeCap
```

The progress indicator's line ending.

This determines the shape of the stroke ends of the progress indicator. By default, [strokeCap] is null. When [value] is null (indeterminate), the stroke ends are set to [StrokeCap.square]. When [value] is not null, the stroke ends are set to [StrokeCap.butt].

Setting [strokeCap] to [StrokeCap.round] will result in a rounded end. Setting [strokeCap] to [StrokeCap.butt] with [value] == null will result in a slightly different indeterminate animation; the indicator completely disappears and reappears on its minimum value. Setting [strokeCap] to [StrokeCap.square] with [value] != null will result in a different display of [value]. The indicator will start drawing from slightly less than the start, and end slightly after the end. This will produce an alternative result, as the default behavior, for example, that a [value] of 0.5 starts at 90 degrees and ends at 270 degrees. With [StrokeCap.square], it could start 85 degrees and end at 275 degrees.

### constraints

```dart
BoxConstraints? constraints
```

Defines minimum and maximum sizes for a [CircularProgressIndicator].

If null, then the [ProgressIndicatorThemeData.constraints] will be used. Otherwise, defaults to a minimum width and height of 36 pixels.

### trackGap

```dart
double? trackGap
```

The gap between the active indicator and the background track.

If [year2023] is true or [ThemeData.useMaterial3] is false, then no track gap will be drawn.

Set [trackGap] to 0 to hide the track gap.

If null, then the [ProgressIndicatorThemeData.trackGap] will be used. If that is null, then defaults to 4.

### year2023

```dart
bool? year2023
```

When true, the [CircularProgressIndicator] will use the 2023 Material Design 3 appearance.

If null, then the [ProgressIndicatorThemeData.year2023] will be used. If that is null, then defaults to true.

If this is set to false, the [CircularProgressIndicator] will use the latest Material Design 3 appearance, which was introduced in December 2023.

If [ThemeData.useMaterial3] is false, then this property is ignored.

### padding

```dart
EdgeInsetsGeometry? padding
```

The padding around the indicator track.

If null, then the [ProgressIndicatorThemeData.circularTrackPadding] will be used. If that is null and [year2023] is false, then defaults to `EdgeInsets.all(4.0)` padding. Otherwise, defaults to zero padding.

### controller

```dart
AnimationController? controller
```

{@macro flutter.material.ProgressIndicator.controller}

See also:

- [CircularProgressIndicator.defaultAnimationDuration], default duration for one full cycle of the indeterminate animation.

### strokeAlignInside

```dart
double strokeAlignInside
```

The indicator stroke is drawn fully inside of the indicator path.

This is a constant for use with [strokeAlign].

### strokeAlignCenter

```dart
double strokeAlignCenter
```

The indicator stroke is drawn on the center of the indicator path, with half of the [strokeWidth] on the inside, and the other half on the outside of the path.

This is a constant for use with [strokeAlign].

This is the default value for [strokeAlign].

### strokeAlignOutside

```dart
double strokeAlignOutside
```

The indicator stroke is drawn on the outside of the indicator path.

This is a constant for use with [strokeAlign].

### defaultAnimationDuration

```dart
Duration defaultAnimationDuration
```

The default duration for one full cycle of the indeterminate animation.

During this period, the indicator completes several full rotations.

This duration is used when the widget creates its own [AnimationController] because no [controller] was provided, either directly or through a [ProgressIndicatorTheme].

### createState()

```dart
State<CircularProgressIndicator> createState()
```

# RefreshProgressIndicator

```dart
class RefreshProgressIndicator extends CircularProgressIndicator {}
```

An indicator for the progress of refreshing the contents of a widget.

Typically used for swipe-to-refresh interactions. See [RefreshIndicator] for a complete implementation of swipe-to-refresh driven by a [Scrollable] widget.

The indicator arc is displayed with [valueColor], an animated value. To specify a constant color use: `AlwaysStoppedAnimation<Color>(color)`.

See also:

- [RefreshIndicator], which automatically displays a [CircularProgressIndicator] when the underlying vertical scrollable is overscrolled.

### RefreshProgressIndicator()

```dart
RefreshProgressIndicator({dynamic key, double? value, dynamic backgroundColor, dynamic color, dynamic valueColor, double? strokeWidth = defaultStrokeWidth, double? strokeAlign, String? semanticsLabel, String? semanticsValue, dynamic strokeCap, double elevation = 2.0, EdgeInsetsGeometry indicatorMargin = const EdgeInsets.all(4.0), EdgeInsetsGeometry indicatorPadding = const EdgeInsets.all(12.0)})
```

Creates a refresh progress indicator.

Rather than creating a refresh progress indicator directly, consider using a [RefreshIndicator] together with a [Scrollable] widget.

{@macro flutter.material.ProgressIndicator.ProgressIndicator}

### elevation

```dart
double elevation
```

{@macro flutter.material.material.elevation}

### indicatorMargin

```dart
EdgeInsetsGeometry indicatorMargin
```

The amount of space by which to inset the whole indicator. It accommodates the [elevation] of the indicator.

### indicatorPadding

```dart
EdgeInsetsGeometry indicatorPadding
```

The amount of space by which to inset the inner refresh indicator.

### defaultStrokeWidth

```dart
double defaultStrokeWidth
```

Default stroke width.

### backgroundColor

```dart
Color? get backgroundColor
```

{@template flutter.material.RefreshProgressIndicator.backgroundColor} Background color of that fills the circle under the refresh indicator.

If [RefreshIndicator.backgroundColor] is null then the ambient [ProgressIndicatorThemeData.refreshBackgroundColor] will be used. If that is null, then the ambient theme's [ThemeData.canvasColor] will be used. {@endtemplate}

### createState()

```dart
State<CircularProgressIndicator> createState()
```
