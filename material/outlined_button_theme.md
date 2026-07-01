@docImport 'outlined_button.dart';

# OutlinedButtonThemeData

```dart
class OutlinedButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] that overrides the default appearance of [OutlinedButton]s when it's used with [OutlinedButtonTheme] or with the overall [Theme]'s [ThemeData.outlinedButtonTheme].

The [style]'s properties override [OutlinedButton]'s default style, i.e. the [ButtonStyle] returned by [OutlinedButton.defaultStyleOf]. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [OutlinedButtonTheme], the theme which is configured with this class.
- [OutlinedButton.defaultStyleOf], which returns the default [ButtonStyle] for outlined buttons.
- [OutlinedButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [OutlinedButton]'s defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.outlinedButtonTheme], which can be used to override the default [ButtonStyle] for [OutlinedButton]s below the overall [Theme].

### OutlinedButtonThemeData()

```dart
OutlinedButtonThemeData({ButtonStyle? style})
```

Creates a [OutlinedButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [OutlinedButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the [ButtonStyle] returned by [OutlinedButton.defaultStyleOf].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
OutlinedButtonThemeData? lerp(OutlinedButtonThemeData? a, OutlinedButtonThemeData? b, double t)
```

Linearly interpolate between two outlined button themes.

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

# OutlinedButtonTheme

```dart
class OutlinedButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [OutlinedButton] descendants.

See also:

- [OutlinedButtonThemeData], which is used to configure this theme.
- [OutlinedButton.defaultStyleOf], which returns the default [ButtonStyle] for outlined buttons.
- [OutlinedButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [OutlinedButton]'s defaults.
- [ThemeData.outlinedButtonTheme], which can be used to override the default [ButtonStyle] for [OutlinedButton]s below the overall [Theme].

### OutlinedButtonTheme()

```dart
OutlinedButtonTheme({dynamic key, required OutlinedButtonThemeData data, required dynamic child})
```

Create a [OutlinedButtonTheme].

### data

```dart
OutlinedButtonThemeData data
```

The configuration of this theme.

### of()

```dart
OutlinedButtonThemeData of(BuildContext context)
```

Retrieves the [OutlinedButtonThemeData] from the closest ancestor [OutlinedButtonTheme].

If there is no enclosing [OutlinedButtonTheme] widget, then [ThemeData.outlinedButtonTheme] is used.

Typical usage is as follows:

```dart
OutlinedButtonThemeData theme = OutlinedButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(OutlinedButtonTheme oldWidget)
```
