@docImport 'menu_theme.dart';

# MenuButtonThemeData

```dart
class MenuButtonThemeData with Diagnosticable {}
```

A [ButtonStyle] theme that overrides the default appearance of [SubmenuButton]s and [MenuItemButton]s.

Descendant widgets obtain the current [MenuButtonThemeData] object using [MenuButtonTheme.of].

A [MenuButtonThemeData] is often specified as part of the overall [Theme] with [ThemeData.menuButtonTheme].

The [style]'s properties override [MenuItemButton]'s and [SubmenuButton]'s default style, i.e. the [ButtonStyle] returned by [MenuItemButton.defaultStyleOf] and [SubmenuButton.defaultStyleOf]. Only the style's non-null property values or resolved non-null [WidgetStateProperty] values are used.

See also:

- [MenuButtonTheme], the theme which is configured with this class.
- [MenuTheme], the theme used to configure the look of the menus these buttons reside in.
- [MenuItemButton.defaultStyleOf] and [SubmenuButton.defaultStyleOf] which return the default [ButtonStyle]s for menu buttons.
- [MenuItemButton.styleFrom] and [SubmenuButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with their respective defaults.
- [WidgetStateProperty.resolve], "resolve" a material state property to a simple value based on a set of [WidgetState]s.
- [ThemeData.menuButtonTheme], which can be used to override the default [ButtonStyle] for [MenuItemButton]s and [SubmenuButton]s below the overall [Theme].
- [MenuAnchor], a widget which hosts cascading menus.
- [MenuBar], a widget which defines a menu bar of buttons hosting cascading menus.

### MenuButtonThemeData()

```dart
MenuButtonThemeData({ButtonStyle? style})
```

Creates a [MenuButtonThemeData].

The [style] may be null.

### style

```dart
ButtonStyle? style
```

Overrides for [SubmenuButton] and [MenuItemButton]'s default style.

Non-null properties or non-null resolved [WidgetStateProperty] values override the [ButtonStyle] returned by [SubmenuButton.defaultStyleOf] or [MenuItemButton.defaultStyleOf].

If [style] is null, then this theme doesn't override anything.

### lerp()

```dart
MenuButtonThemeData? lerp(MenuButtonThemeData? a, MenuButtonThemeData? b, double t)
```

Linearly interpolate between two menu button themes.

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

# MenuButtonTheme

```dart
class MenuButtonTheme extends InheritedTheme {}
```

Overrides the default [ButtonStyle] of its [MenuItemButton] and [SubmenuButton] descendants.

See also:

- [MenuButtonThemeData], which is used to configure this theme.
- [MenuTheme], the theme used to configure the look of the menus themselves.
- [MenuItemButton.defaultStyleOf] and [SubmenuButton.defaultStyleOf] which return the default [ButtonStyle]s for menu buttons.
- [MenuItemButton.styleFrom] and [SubmenuButton.styleFrom], which converts simple values into a [ButtonStyle] that's consistent with their respective defaults.
- [ThemeData.menuButtonTheme], which can be used to override the default [ButtonStyle] for [MenuItemButton]s and [SubmenuButton]s below the overall [Theme].

### MenuButtonTheme()

```dart
MenuButtonTheme({dynamic key, required MenuButtonThemeData data, required dynamic child})
```

Create a [MenuButtonTheme].

### data

```dart
MenuButtonThemeData data
```

The configuration of this theme.

### of()

```dart
MenuButtonThemeData of(BuildContext context)
```

The closest instance of this class that encloses the given context.

If there is no enclosing [MenuButtonTheme] widget, then [ThemeData.menuButtonTheme] is used.

Typical usage is as follows:

```dart
MenuButtonThemeData theme = MenuButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(MenuButtonTheme oldWidget)
```
