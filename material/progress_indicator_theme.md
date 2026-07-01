@docImport 'color_scheme.dart'; @docImport 'progress_indicator.dart';

# ProgressIndicatorThemeData

```dart
class ProgressIndicatorThemeData with Diagnosticable {}
```

Overrides the default values of visual properties for descendant [ProgressIndicator] widgets.

Descendant widgets obtain the current [ProgressIndicatorThemeData] object with [ProgressIndicatorTheme.of]. Instances of [ProgressIndicatorThemeData] can be customized with [ProgressIndicatorThemeData.copyWith].

Typically a [ProgressIndicatorThemeData] is specified as part of the overall [Theme] with [ThemeData.progressIndicatorTheme].

See also:

- [ProgressIndicatorTheme], an [InheritedWidget] that propagates the theme down its subtree.
- [ThemeData.progressIndicatorTheme], which describes the defaults for any progress indicators as part of the application's [ThemeData].

### ProgressIndicatorThemeData()

```dart
ProgressIndicatorThemeData({Color? color, Color? linearTrackColor, double? linearMinHeight, Color? circularTrackColor, Color? refreshBackgroundColor, BorderRadiusGeometry? borderRadius, Color? stopIndicatorColor, double? stopIndicatorRadius, double? strokeWidth, double? strokeAlign, StrokeCap? strokeCap, BoxConstraints? constraints, double? trackGap, EdgeInsetsGeometry? circularTrackPadding, bool? year2023, AnimationController? controller})
```

Creates the set of properties used to configure [ProgressIndicator] widgets.

### color

```dart
Color? color
```

The color of the [ProgressIndicator]'s indicator.

If null, then it will use [ColorScheme.primary] of the ambient [ThemeData.colorScheme].

See also:

- [ProgressIndicator.color], which specifies the indicator color for a specific progress indicator.
- [ProgressIndicator.valueColor], which specifies the indicator color a an animated color.

### linearTrackColor

```dart
Color? linearTrackColor
```

{@macro flutter.material.LinearProgressIndicator.trackColor}

### linearMinHeight

```dart
double? linearMinHeight
```

{@macro flutter.material.LinearProgressIndicator.minHeight}

### circularTrackColor

```dart
Color? circularTrackColor
```

{@macro flutter.material.CircularProgressIndicator.trackColor}

### refreshBackgroundColor

```dart
Color? refreshBackgroundColor
```

{@macro flutter.material.RefreshProgressIndicator.backgroundColor}

### borderRadius

```dart
BorderRadiusGeometry? borderRadius
```

Overrides the border radius of the [ProgressIndicator].

### stopIndicatorColor

```dart
Color? stopIndicatorColor
```

Overrides the stop indicator color of the [LinearProgressIndicator].

If [LinearProgressIndicator.year2023] is true or [ThemeData.useMaterial3] is false, then no stop indicator will be drawn.

### stopIndicatorRadius

```dart
double? stopIndicatorRadius
```

Overrides the stop indicator radius of the [LinearProgressIndicator].

If [LinearProgressIndicator.year2023] is true or [ThemeData.useMaterial3] is false, then no stop indicator will be drawn.

### strokeWidth

```dart
double? strokeWidth
```

Overrides the stroke width of the [CircularProgressIndicator].

### strokeAlign

```dart
double? strokeAlign
```

Overrides the stroke align of the [CircularProgressIndicator].

### strokeCap

```dart
StrokeCap? strokeCap
```

Overrides the stroke cap of the [CircularProgressIndicator].

### constraints

```dart
BoxConstraints? constraints
```

Overrides the constraints of the [CircularProgressIndicator].

### trackGap

```dart
double? trackGap
```

Overrides the active indicator and the background track.

If [CircularProgressIndicator.year2023] is true or [ThemeData.useMaterial3] is false, then no track gap will be drawn.

If [LinearProgressIndicator.year2023] is true or [ThemeData.useMaterial3] is false, then no track gap will be drawn.

### circularTrackPadding

```dart
EdgeInsetsGeometry? circularTrackPadding
```

Overrides the padding of the [CircularProgressIndicator].

### year2023

```dart
bool? year2023
```

Overrides the [CircularProgressIndicator.year2023] and [LinearProgressIndicator.year2023] properties.

When true, the [CircularProgressIndicator] and [LinearProgressIndicator] will use the 2023 Material Design 3 appearance. Defaults to true.

If this is set to false, the [CircularProgressIndicator] and [LinearProgressIndicator] will use the latest Material Design 3 appearance, which was introduced in December 2023.

If [ThemeData.useMaterial3] is false, then this property is ignored.

### controller

```dart
AnimationController? controller
```

Defines a default [AnimationController] for descendant [CircularProgressIndicator] and [LinearProgressIndicator] widgets.

If a descendant progress indicator's `controller` property is null, this controller will be used to drive its indeterminate animation. This allows a single controller to synchronize the animations of multiple indicators.

If this property is also null, the progress indicator will create and manage its own internal [AnimationController].

### copyWith()

```dart
ProgressIndicatorThemeData copyWith({Color? color, Color? linearTrackColor, double? linearMinHeight, Color? circularTrackColor, Color? refreshBackgroundColor, BorderRadiusGeometry? borderRadius, Color? stopIndicatorColor, double? stopIndicatorRadius, double? strokeWidth, double? strokeAlign, StrokeCap? strokeCap, BoxConstraints? constraints, double? trackGap, EdgeInsetsGeometry? circularTrackPadding, bool? year2023, AnimationController? controller})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
ProgressIndicatorThemeData? lerp(ProgressIndicatorThemeData? a, ProgressIndicatorThemeData? b, double t)
```

Linearly interpolate between two progress indicator themes.

If both arguments are null, then null is returned.

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

# ProgressIndicatorTheme

```dart
class ProgressIndicatorTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for [ProgressIndicator]s in this widget's subtree.

Values specified here are used for [ProgressIndicator] properties that are not given an explicit non-null value.

{@tool snippet}

Here is an example of a progress indicator theme that applies a red indicator color.

```dart
const ProgressIndicatorTheme(
  data: ProgressIndicatorThemeData(
    color: Colors.red,
  ),
  child: LinearProgressIndicator()
)
```

{@end-tool}

### ProgressIndicatorTheme()

```dart
ProgressIndicatorTheme({dynamic key, required ProgressIndicatorThemeData data, required dynamic child})
```

Creates a theme that controls the configurations for [ProgressIndicator] widgets.

### data

```dart
ProgressIndicatorThemeData data
```

The properties for descendant [ProgressIndicator] widgets.

### of()

```dart
ProgressIndicatorThemeData of(BuildContext context)
```

Returns the [data] from the closest [ProgressIndicatorTheme] ancestor. If there is no ancestor, it returns [ThemeData.progressIndicatorTheme].

Typical usage is as follows:

```dart
ProgressIndicatorThemeData theme = ProgressIndicatorTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ProgressIndicatorTheme oldWidget)
```
