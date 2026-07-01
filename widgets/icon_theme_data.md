@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'icon.dart'; @docImport 'icon_theme.dart';

# IconThemeData

```dart
class IconThemeData with Diagnosticable {}
```

Defines the size, font variations, color, opacity, and shadows of icons.

Used by [IconTheme] to control those properties in a widget subtree.

To obtain the current icon theme, use [IconTheme.of]. To convert an icon theme to a version with all the fields filled in, use [IconThemeData.fallback].

### IconThemeData()

```dart
IconThemeData({double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, double? opacity, List<Shadow>? shadows, bool? applyTextScaling})
```

Creates an icon theme data.

The opacity applies to both explicit and default icon colors. The value is clamped between 0.0 and 1.0.

### IconThemeData.fallback()

```dart
IconThemeData.fallback()
```

Creates an icon theme with some reasonable default values.

The [size] is 24.0, [fill] is 0.0, [weight] is 400.0, [grade] is 0.0, opticalSize is 48.0, [color] is black, and [opacity] is 1.0.

### copyWith()

```dart
IconThemeData copyWith({double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, double? opacity, List<Shadow>? shadows, bool? applyTextScaling})
```

Creates a copy of this icon theme but with the given fields replaced with the new values.

### merge()

```dart
IconThemeData merge(IconThemeData? other)
```

Returns a new icon theme that matches this icon theme but with some values replaced by the non-null parameters of the given icon theme. If the given icon theme is null, returns this icon theme.

### resolve()

```dart
IconThemeData resolve(BuildContext context)
```

Called by [IconTheme.of] to convert this instance to an [IconThemeData] that fits the given [BuildContext].

This method gives the ambient [IconThemeData] a chance to update itself, after it's been retrieved by [IconTheme.of], and before being returned as the final result. For instance, [CupertinoIconThemeData] overrides this method to resolve [color], in case [color] is a [CupertinoDynamicColor] and needs to be resolved against the given [BuildContext] before it can be used as a regular [Color].

The default implementation returns this [IconThemeData] as-is.

See also:

- [CupertinoIconThemeData.resolve] an implementation that resolves the color of [CupertinoIconThemeData] before returning.

### isConcrete

```dart
bool get isConcrete
```

Whether all the properties (except shadows) of this object are non-null.

### size

```dart
double? size
```

The default for [Icon.size].

Falls back to 24.0.

### fill

```dart
double? fill
```

The default for [Icon.fill].

Falls back to 0.0.

### weight

```dart
double? weight
```

The default for [Icon.weight].

Falls back to 400.0.

### grade

```dart
double? grade
```

The default for [Icon.grade].

Falls back to 0.0.

### opticalSize

```dart
double? opticalSize
```

The default for [Icon.opticalSize].

Falls back to 48.0.

### color

```dart
Color? color
```

The default for [Icon.color].

In material apps, if there is a [Theme] without any [IconTheme]s specified, icon colors default to white if [ThemeData.brightness] is dark and black if [ThemeData.brightness] is light.

Otherwise, falls back to black.

### opacity

```dart
double? get opacity
```

An opacity to apply to both explicit and default icon colors.

Falls back to 1.0.

### shadows

```dart
List<Shadow>? shadows
```

The default for [Icon.shadows].

### applyTextScaling

```dart
bool? applyTextScaling
```

The default for [Icon.applyTextScaling].

### lerp()

```dart
IconThemeData lerp(IconThemeData? a, IconThemeData? b, double t)
```

Linearly interpolate between two icon theme data objects.

{@macro dart.ui.shadow.lerp}

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
