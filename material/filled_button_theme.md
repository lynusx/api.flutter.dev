@docImport 'filled_button.dart';

# FilledButtonThemeData

```dart
class FilledButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] that overrides the default appearance of [FilledButton]s when it's used with [FilledButtonTheme] or with the overall [Theme]'s [ThemeData.filledButtonTheme].

The [style]'s properties override [FilledButton]'s default style, i.e. the [ButtonStyle] returned by [FilledButton.defaultStyleOf]. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [FilledButtonTheme], the theme which is configured with this class.
- [FilledButton.defaultStyleOf], which returns the default [ButtonStyle] for text buttons.
- [FilledButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [FilledButton]'s defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.filledButtonTheme], which can be used to override the default [ButtonStyle] for [FilledButton]s below the overall [Theme].

### FilledButtonThemeData()

```dart
FilledButtonThemeData({ButtonStyle? style})
```

Creates an [FilledButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [FilledButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the [ButtonStyle] returned by [FilledButton.defaultStyleOf].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
FilledButtonThemeData? lerp(FilledButtonThemeData? a, FilledButtonThemeData? b, double t)
```

Linearly interpolate between two filled button themes.

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

# FilledButtonTheme

```dart
class FilledButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [FilledButton] descendants.

See also:

- [FilledButtonThemeData], which is used to configure this theme.
- [FilledButton.defaultStyleOf], which returns the default [ButtonStyle] for filled buttons.
- [FilledButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [FilledButton]'s defaults.
- [ThemeData.filledButtonTheme], which can be used to override the default [ButtonStyle] for [FilledButton]s below the overall [Theme].

### FilledButtonTheme()

```dart
FilledButtonTheme({dynamic key, required FilledButtonThemeData data, required dynamic child})
```

Create a [FilledButtonTheme].

### data

```dart
FilledButtonThemeData data
```

The configuration of this theme.

### of()

```dart
FilledButtonThemeData of(BuildContext context)
```

Retrieves the [FilledButtonThemeData] from the closest ancestor [FilledButtonTheme].

If there is no enclosing [FilledButtonTheme] widget, then [ThemeData.filledButtonTheme] is used.

Typical usage is as follows:

```dart
FilledButtonThemeData theme = FilledButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(FilledButtonTheme oldWidget)
```
