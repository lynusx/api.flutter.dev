@docImport 'menu_bar_theme.dart';

# MenuThemeData

```dart
class MenuThemeData with Diagnosticable {}
```

Defines the configuration of the submenus created by the [SubmenuButton], [MenuBar], or [MenuAnchor] widgets.

Descendant widgets obtain the current [MenuThemeData] object using [MenuTheme.of].

Typically, a [MenuThemeData] is specified as part of the overall [Theme] with [ThemeData.menuTheme]. Otherwise, [MenuTheme] can be used to configure its own widget subtree.

All [MenuThemeData] properties are `null` by default. If any of these properties are null, the menu bar will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme for the application.
- [MenuBarThemeData], which describes the theme for the menu bar itself in a [MenuBar] widget.

### MenuThemeData()

```dart
MenuThemeData({MenuStyle? style, WidgetStateProperty<Widget?>? submenuIcon})
```

Creates a const set of properties used to configure [MenuTheme].

### style

```dart
MenuStyle? style
```

The [MenuStyle] of a [SubmenuButton] menu.

Any values not set in the [MenuStyle] will use the menu default for that property.

### submenuIcon

```dart
WidgetStateProperty<Widget?>? submenuIcon
```

If provided, the widget replaces the default [SubmenuButton] arrow icon.

Resolves in the following states:

- [WidgetState.disabled].
- [WidgetState.hovered].
- [WidgetState.focused].

### lerp()

```dart
MenuThemeData? lerp(MenuThemeData? a, MenuThemeData? b, double t)
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

# MenuTheme

```dart
class MenuTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration in this widget's descendants for menus created by the [SubmenuButton], [MenuBar], or [MenuAnchor] widgets.

Values specified here are used for [SubmenuButton]'s menu properties that are not given an explicit non-null value.

See also:

- [MenuThemeData], a configuration object that holds attributes of a menu used by this theme.
- [MenuBarTheme], which does the same thing for the [MenuBar] widget.
- [MenuBar], a widget that manages [MenuItemButton]s.
- [MenuAnchor], a widget that creates a region that has a submenu.
- [MenuItemButton], a widget that is a selectable item in a menu bar menu.
- [SubmenuButton], a widget that specifies an item with a cascading submenu in a [MenuBar] menu.

### MenuTheme()

```dart
MenuTheme({dynamic key, required MenuThemeData data, required dynamic child})
```

Creates a const theme that controls the configurations for the menus created by the [SubmenuButton] or [MenuAnchor] widgets.

### data

```dart
MenuThemeData data
```

The properties for [MenuBar] and [MenuItemButton] in this widget's descendants.

### of()

```dart
MenuThemeData of(BuildContext context)
```

Returns the closest instance of this class's [data] value that encloses the given context. If there is no ancestor, it returns [ThemeData.menuTheme].

Typical usage is as follows:

```dart
MenuThemeData theme = MenuTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(MenuTheme oldWidget)
```
