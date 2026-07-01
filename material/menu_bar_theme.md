@docImport 'menu_button_theme.dart';

# MenuBarThemeData

```dart
class MenuBarThemeData extends MenuThemeData {}
```

A data class that [MenuBarTheme] uses to define the visual properties of [MenuBar] widgets.

This class defines the visual properties of [MenuBar] widgets themselves, but not their submenus. Those properties are defined by [MenuThemeData] or [MenuButtonThemeData] instead.

Descendant widgets obtain the current [MenuBarThemeData] object using [MenuBarTheme.of].

Typically, a [MenuBarThemeData] is specified as part of the overall [Theme] with [ThemeData.menuBarTheme]. Otherwise, [MenuTheme] can be used to configure its own widget subtree.

All [MenuBarThemeData] properties are `null` by default. If any of these properties are null, the menu bar will provide its own defaults.

See also:

- [MenuThemeData], which describes the theme for the submenus of a [MenuBar].
- [MenuButtonThemeData], which describes the theme for the [MenuItemButton]s in a menu.
- [ThemeData], which describes the overall theme for the application.

### MenuBarThemeData()

```dart
MenuBarThemeData({MenuStyle? style})
```

Creates a const set of properties used to configure [MenuTheme].

### lerp()

```dart
MenuBarThemeData? lerp(MenuBarThemeData? a, MenuBarThemeData? b, double t)
```

Linearly interpolate between two [MenuBar] themes.

# MenuBarTheme

```dart
class MenuBarTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for the [MenuBar] widgets in this widget's descendants.

This class defines the visual properties of [MenuBar] widgets themselves, but not their submenus. Those properties are defined by [MenuTheme] or [MenuButtonTheme] instead.

Values specified here are used for [MenuBar]'s properties that are not given an explicit non-null value.

See also:

- [MenuStyle], a configuration object that holds attributes of a menu, and is used by this theme to define those attributes.
- [MenuTheme], which does the same thing for the menus created by a [SubmenuButton] or [MenuAnchor].
- [MenuButtonTheme], which does the same thing for the [MenuItemButton]s inside of the menus.
- [SubmenuButton], a button that manages a submenu that uses these properties.
- [MenuBar], a widget that creates a menu bar that can use [SubmenuButton]s.

### MenuBarTheme()

```dart
MenuBarTheme({dynamic key, required MenuBarThemeData data, required dynamic child})
```

Creates a theme that controls the configurations for [MenuBar] and [MenuItemButton] in its widget subtree.

### data

```dart
MenuBarThemeData data
```

The properties to set for [MenuBar] in this widget's descendants.

### of()

```dart
MenuBarThemeData of(BuildContext context)
```

Returns the closest instance of this class's [data] value that encloses the given context. If there is no ancestor, it returns [ThemeData.menuBarTheme].

Typical usage is as follows:

```dart
MenuBarThemeData theme = MenuBarTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(MenuBarTheme oldWidget)
```
