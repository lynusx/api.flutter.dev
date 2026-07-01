@docImport 'icon_button.dart';

# IconButtonThemeData

```dart
class IconButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] that overrides the default appearance of [IconButton]s when it's used with the [IconButton], the [IconButtonTheme] or the overall [Theme]'s [ThemeData.iconButtonTheme].

The [IconButton] will be affected by [IconButtonTheme] and [IconButtonThemeData] only if [ThemeData.useMaterial3] is set to true; otherwise, [IconTheme] will be used.

The [style]'s properties override [IconButton]'s default style. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [IconButtonTheme], the theme which is configured with this class.
- [IconButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [IconButton]'s defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.iconButtonTheme], which can be used to override the default [ButtonStyle] for [IconButton]s below the overall [Theme].

### IconButtonThemeData()

```dart
IconButtonThemeData({ButtonStyle? style})
```

Creates a [IconButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [IconButton]'s default style if [ThemeData.useMaterial3] is set to true.

Non-null properties or non-null resolved [WidgetStateProperty] values override the default [ButtonStyle] in [IconButton].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
IconButtonThemeData? lerp(IconButtonThemeData? a, IconButtonThemeData? b, double t)
```

Linearly interpolate between two icon button themes.

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

# IconButtonTheme

```dart
class IconButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [IconButton] descendants.

See also:

- [IconButtonThemeData], which is used to configure this theme.
- [IconButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [IconButton]'s defaults.
- [ThemeData.iconButtonTheme], which can be used to override the default [ButtonStyle] for [IconButton]s below the overall [Theme].

### IconButtonTheme()

```dart
IconButtonTheme({dynamic key, required IconButtonThemeData data, required dynamic child})
```

Create a [IconButtonTheme].

### data

```dart
IconButtonThemeData data
```

The configuration of this theme.

### of()

```dart
IconButtonThemeData of(BuildContext context)
```

Retrieves the [IconButtonThemeData] from the closest ancestor [IconButtonTheme].

If there is no enclosing [IconButtonTheme] widget, then [ThemeData.iconButtonTheme] is used.

Typical usage is as follows:

```dart
IconButtonThemeData theme = IconButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(IconButtonTheme oldWidget)
```
