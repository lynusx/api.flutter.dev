@docImport 'elevated_button.dart';

# ElevatedButtonThemeData

```dart
class ElevatedButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] that overrides the default appearance of [ElevatedButton]s when it's used with [ElevatedButtonTheme] or with the overall [Theme]'s [ThemeData.elevatedButtonTheme].

The [style]'s properties override [ElevatedButton]'s default style, i.e. the [ButtonStyle] returned by [ElevatedButton.defaultStyleOf]. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [ElevatedButtonTheme], the theme which is configured with this class.
- [ElevatedButton.defaultStyleOf], which returns the default [ButtonStyle] for text buttons.
- [ElevatedButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [ElevatedButton]'s defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.elevatedButtonTheme], which can be used to override the default [ButtonStyle] for [ElevatedButton]s below the overall [Theme].

### ElevatedButtonThemeData()

```dart
ElevatedButtonThemeData({ButtonStyle? style})
```

Creates an [ElevatedButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [ElevatedButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the [ButtonStyle] returned by [ElevatedButton.defaultStyleOf].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
ElevatedButtonThemeData? lerp(ElevatedButtonThemeData? a, ElevatedButtonThemeData? b, double t)
```

Linearly interpolate between two elevated button themes.

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

# ElevatedButtonTheme

```dart
class ElevatedButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [ElevatedButton] descendants.

See also:

- [ElevatedButtonThemeData], which is used to configure this theme.
- [ElevatedButton.defaultStyleOf], which returns the default [ButtonStyle] for elevated buttons.
- [ElevatedButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [ElevatedButton]'s defaults.
- [ThemeData.elevatedButtonTheme], which can be used to override the default [ButtonStyle] for [ElevatedButton]s below the overall [Theme].

### ElevatedButtonTheme()

```dart
ElevatedButtonTheme({dynamic key, required ElevatedButtonThemeData data, required dynamic child})
```

Create a [ElevatedButtonTheme].

### data

```dart
ElevatedButtonThemeData data
```

The configuration of this theme.

### of()

```dart
ElevatedButtonThemeData of(BuildContext context)
```

Retrieves the [ElevatedButtonThemeData] from the closest ancestor [ElevatedButtonTheme].

If there is no enclosing [ElevatedButtonTheme] widget, then [ThemeData.elevatedButtonTheme] is used.

Typical usage is as follows:

```dart
ElevatedButtonThemeData theme = ElevatedButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ElevatedButtonTheme oldWidget)
```
