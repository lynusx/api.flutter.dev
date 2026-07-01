@docImport 'text_button.dart';

# TextButtonThemeData

```dart
class TextButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] that overrides the default appearance of [TextButton]s when it's used with [TextButtonTheme] or with the overall [Theme]'s [ThemeData.textButtonTheme].

The [style]'s properties override [TextButton]'s default style, i.e. the [ButtonStyle] returned by [TextButton.defaultStyleOf]. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [TextButtonTheme], the theme which is configured with this class.
- [TextButton.defaultStyleOf], which returns the default [ButtonStyle] for text buttons.
- [TextButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [TextButton]'s defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.textButtonTheme], which can be used to override the default [ButtonStyle] for [TextButton]s below the overall [Theme].

### TextButtonThemeData()

```dart
TextButtonThemeData({ButtonStyle? style})
```

Creates a [TextButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [TextButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the [ButtonStyle] returned by [TextButton.defaultStyleOf].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
TextButtonThemeData? lerp(TextButtonThemeData? a, TextButtonThemeData? b, double t)
```

Linearly interpolate between two text button themes.

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

# TextButtonTheme

```dart
class TextButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [TextButton] descendants.

See also:

- [TextButtonThemeData], which is used to configure this theme.
- [TextButton.defaultStyleOf], which returns the default [ButtonStyle] for text buttons.
- [TextButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with [TextButton]'s defaults.
- [ThemeData.textButtonTheme], which can be used to override the default [ButtonStyle] for [TextButton]s below the overall [Theme].

### TextButtonTheme()

```dart
TextButtonTheme({dynamic key, required TextButtonThemeData data, required dynamic child})
```

Create a [TextButtonTheme].

### data

```dart
TextButtonThemeData data
```

The configuration of this theme.

### of()

```dart
TextButtonThemeData of(BuildContext context)
```

Retrieves the [TextButtonThemeData] from the closest ancestor [TextButtonTheme].

If there is no enclosing [TextButtonTheme] widget, then [ThemeData.textButtonTheme] is used.

Typical usage is as follows:

```dart
TextButtonThemeData theme = TextButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(TextButtonTheme oldWidget)
```
