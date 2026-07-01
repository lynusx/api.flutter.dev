@docImport 'scrollbar.dart';

# ScrollbarThemeData

```dart
class ScrollbarThemeData with Diagnosticable {}
```

Defines default property values for descendant [Scrollbar] widgets.

Descendant widgets obtain the current [ScrollbarThemeData] object with `ScrollbarTheme.of(context)`. Instances of [ScrollbarThemeData] can be customized with [ScrollbarThemeData.copyWith].

Typically the [ScrollbarThemeData] of a [ScrollbarTheme] is specified as part of the overall [Theme] with [ThemeData.scrollbarTheme].

All [ScrollbarThemeData] properties are `null` by default. When null, the [Scrollbar] computes its own default values, typically based on the overall theme's [ThemeData.colorScheme].

See also:

- [ThemeData], which describes the overall theme information for the application.

### ScrollbarThemeData()

```dart
ScrollbarThemeData({WidgetStateProperty<bool?>? thumbVisibility, WidgetStateProperty<double?>? thickness, WidgetStateProperty<bool?>? trackVisibility, Radius? radius, WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackBorderColor, double? crossAxisMargin, double? mainAxisMargin, double? minThumbLength, bool? interactive})
```

Creates a theme that can be used for [ThemeData.scrollbarTheme].

### thumbVisibility

```dart
WidgetStateProperty<bool?>? thumbVisibility
```

Overrides the default value of [Scrollbar.thumbVisibility] in all descendant [Scrollbar] widgets.

### thickness

```dart
WidgetStateProperty<double?>? thickness
```

Overrides the default value of [Scrollbar.thickness] in all descendant [Scrollbar] widgets.

Resolves in the following states:

- [WidgetState.hovered] on web and desktop platforms.

### trackVisibility

```dart
WidgetStateProperty<bool?>? trackVisibility
```

Overrides the default value of [Scrollbar.trackVisibility] in all descendant [Scrollbar] widgets.

### interactive

```dart
bool? interactive
```

Overrides the default value of [Scrollbar.interactive] in all descendant [Scrollbar] widgets.

### radius

```dart
Radius? radius
```

Overrides the default value of [Scrollbar.radius] in all descendant widgets.

### thumbColor

```dart
WidgetStateProperty<Color?>? thumbColor
```

Overrides the default [Color] of the [Scrollbar] thumb in all descendant [Scrollbar] widgets.

Resolves in the following states:

- [WidgetState.dragged].
- [WidgetState.hovered] on web and desktop platforms.

### trackColor

```dart
WidgetStateProperty<Color?>? trackColor
```

Overrides the default [Color] of the [Scrollbar] track when [trackVisibility] is true in all descendant [Scrollbar] widgets.

Resolves in the following states:

- [WidgetState.hovered] on web and desktop platforms.

### trackBorderColor

```dart
WidgetStateProperty<Color?>? trackBorderColor
```

Overrides the default [Color] of the [Scrollbar] track border when [trackVisibility] is true in all descendant [Scrollbar] widgets.

Resolves in the following states:

- [WidgetState.hovered] on web and desktop platforms.

### crossAxisMargin

```dart
double? crossAxisMargin
```

Overrides the default value of the [ScrollbarPainter.crossAxisMargin] property in all descendant [Scrollbar] widgets.

See also:

- [ScrollbarPainter.crossAxisMargin], which sets the distance from the scrollbar's side to the nearest edge in logical pixels.

### mainAxisMargin

```dart
double? mainAxisMargin
```

Overrides the default value of the [ScrollbarPainter.mainAxisMargin] property in all descendant [Scrollbar] widgets.

See also:

- [ScrollbarPainter.mainAxisMargin], which sets the distance from the scrollbar's start and end to the edge of the viewport in logical pixels.

### minThumbLength

```dart
double? minThumbLength
```

Overrides the default value of the [ScrollbarPainter.minLength] property in all descendant [Scrollbar] widgets.

See also:

- [ScrollbarPainter.minLength], which sets the preferred smallest size the scrollbar can shrink to when the total scrollable extent is large, the current visible viewport is small, and the viewport is not overscrolled.

### copyWith()

```dart
ScrollbarThemeData copyWith({WidgetStateProperty<bool?>? thumbVisibility, WidgetStateProperty<double?>? thickness, WidgetStateProperty<bool?>? trackVisibility, bool? interactive, Radius? radius, WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackBorderColor, double? crossAxisMargin, double? mainAxisMargin, double? minThumbLength})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
ScrollbarThemeData lerp(ScrollbarThemeData? a, ScrollbarThemeData? b, double t)
```

Linearly interpolate between two Scrollbar themes.

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

# ScrollbarTheme

```dart
class ScrollbarTheme extends InheritedTheme {}
```

Applies a scrollbar theme to descendant [Scrollbar] widgets.

Descendant widgets obtain the current theme's [ScrollbarThemeData] using [ScrollbarTheme.of]. When a widget uses [ScrollbarTheme.of], it is automatically rebuilt if the theme later changes.

A scrollbar theme can be specified as part of the overall Material theme using [ThemeData.scrollbarTheme].

See also:

- [ScrollbarThemeData], which describes the configuration of a scrollbar theme.

### ScrollbarTheme()

```dart
ScrollbarTheme({dynamic key, required ScrollbarThemeData data, required dynamic child})
```

Constructs a scrollbar theme that configures all descendant [Scrollbar] widgets.

### data

```dart
ScrollbarThemeData data
```

The properties used for all descendant [Scrollbar] widgets.

### of()

```dart
ScrollbarThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [ScrollbarTheme] ancestor. If there is no ancestor, it returns [ThemeData.scrollbarTheme].

Typical usage is as follows:

```dart
ScrollbarThemeData theme = ScrollbarTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ScrollbarTheme oldWidget)
```
