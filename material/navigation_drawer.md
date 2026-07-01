@docImport 'scaffold.dart';

# NavigationDrawer

```dart
class NavigationDrawer extends StatelessWidget {}
```

Material Design Navigation Drawer component.

On top of [Drawer]s, Navigation drawers offer a persistent and convenient way to switch between primary destinations in an app.

The style for the icons and text are not affected by parent [DefaultTextStyle]s or [IconTheme]s but rather controlled by parameters or the [NavigationDrawerThemeData].

The [children] are a list of widgets to be displayed in the drawer. These can be a mixture of any widgets, but there is special handling for [NavigationDrawerDestination]s. They are treated as a group and when one is selected, the [onDestinationSelected] is called with the index into the group that corresponds to the selected destination.

{@tool dartpad} This example shows a [NavigationDrawer] used within a [Scaffold] widget. The [NavigationDrawer] has headline widget, divider widget and three [NavigationDrawerDestination] widgets. The initial [selectedIndex] is 0. The [onDestinationSelected] callback changes the selected item's index and displays a corresponding widget in the body of the [Scaffold].

** See code in examples/api/lib/material/navigation_drawer/navigation_drawer.0.dart ** {@end-tool}

See also:

- [Scaffold.drawer], where one specifies a [Drawer] so that it can be shown.
- [Scaffold.of], to obtain the current [ScaffoldState], which manages the display and animation of the drawer.
- [ScaffoldState.openDrawer], which displays its [Drawer], if any.
- <https://material.io/design/components/navigation-drawer.html>

### NavigationDrawer()

```dart
NavigationDrawer({dynamic key, required List<Widget> children, Widget? header, Widget? footer, Color? backgroundColor, Color? shadowColor, Color? surfaceTintColor, double? elevation, Color? indicatorColor, ShapeBorder? indicatorShape, ValueChanged<int>? onDestinationSelected, int? selectedIndex = 0, EdgeInsetsGeometry tilePadding = const EdgeInsets.symmetric(horizontal: 12.0)})
```

Creates a Material Design Navigation Drawer component.

### backgroundColor

```dart
Color? backgroundColor
```

The background color of the [Material] that holds the [NavigationDrawer]'s contents.

If this is null, then [NavigationDrawerThemeData.backgroundColor] is used. If that is also null, then it falls back to [ColorScheme.surfaceContainerLow].

### shadowColor

```dart
Color? shadowColor
```

The color used for the drop shadow to indicate elevation.

If null, [NavigationDrawerThemeData.shadowColor] is used. If that is also null, the default value is [Colors.transparent] which indicates that no drop shadow will be displayed.

See [Material.shadowColor] for more details on drop shadows.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The surface tint of the [Material] that holds the [NavigationDrawer]'s contents.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If this is null, then [NavigationDrawerThemeData.surfaceTintColor] is used. If that is also null, the default value is [Colors.transparent].

### elevation

```dart
double? elevation
```

The elevation of the [NavigationDrawer] itself.

If null, [NavigationDrawerThemeData.elevation] is used. If that is also null, it will be 1.0.

### indicatorColor

```dart
Color? indicatorColor
```

The color of the [indicatorShape] when this destination is selected.

If this is null, [NavigationDrawerThemeData.indicatorColor] is used. If that is also null, defaults to [ColorScheme.secondaryContainer].

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

The shape of the selected indicator.

If this is null, [NavigationDrawerThemeData.indicatorShape] is used. If that is also null, defaults to [StadiumBorder].

### children

```dart
List<Widget> children
```

Defines the appearance of the items within the navigation drawer.

The list contains [NavigationDrawerDestination] widgets and/or customized widgets like headlines and dividers.

### header

```dart
Widget? header
```

A widget to display at the top of the layout.

Typically used for titles, navigation bars, or other header content.

### footer

```dart
Widget? footer
```

A widget to display at the bottom of the layout.

Typically used for actions, navigation controls, or other footer content.

### selectedIndex

```dart
int? selectedIndex
```

The index into destinations for the current selected [NavigationDrawerDestination] or null if no destination is selected.

A valid [selectedIndex] satisfies 0 <= [selectedIndex] < number of [NavigationDrawerDestination]. For an invalid [selectedIndex] like `-1`, all destinations will appear unselected.

### onDestinationSelected

```dart
ValueChanged<int>? onDestinationSelected
```

Called when one of the [NavigationDrawerDestination] children is selected.

This callback usually updates the int passed to [selectedIndex].

Upon updating [selectedIndex], the [NavigationDrawer] will be rebuilt.

### tilePadding

```dart
EdgeInsetsGeometry tilePadding
```

Defines the padding for [NavigationDrawerDestination] widgets (Drawer items).

Defaults to `EdgeInsets.symmetric(horizontal: 12.0)`.

### build()

```dart
Widget build(BuildContext context)
```

# NavigationDrawerDestination

```dart
class NavigationDrawerDestination extends StatelessWidget {}
```

A Material Design [NavigationDrawer] destination.

Displays an icon with a label, for use in [NavigationDrawer.children].

### NavigationDrawerDestination()

```dart
NavigationDrawerDestination({dynamic key, Color? backgroundColor, required Widget icon, Widget? selectedIcon, required Widget label, bool enabled = true})
```

Creates a navigation drawer destination.

### backgroundColor

```dart
Color? backgroundColor
```

The background color of the destination.

If this is null, no background is set and [NavigationDrawer.backgroundColor] will be visible.

This is the background color of the whole rectangular area behind the drawer destination. To customize only the indicator color consider using [NavigationDrawer.indicatorColor].

### icon

```dart
Widget icon
```

The [Widget] (usually an [Icon]) that's displayed for this [NavigationDestination].

The icon will use [NavigationDrawerThemeData.iconTheme]. If this is null, the default [IconThemeData] would use a size of 24.0 and [ColorScheme.onSurfaceVariant].

### selectedIcon

```dart
Widget? selectedIcon
```

The optional [Widget] (usually an [Icon]) that's displayed when this [NavigationDestination] is selected.

If [selectedIcon] is non-null, the destination will fade from [icon] to [selectedIcon] when this destination goes from unselected to selected.

The icon will use [NavigationDrawerThemeData.iconTheme] with [WidgetState.selected]. If this is null, the default [IconThemeData] would use a size of 24.0 and [ColorScheme.onSecondaryContainer].

### label

```dart
Widget label
```

The text label that appears on the right of the icon

The accompanying [Text] widget will use [NavigationDrawerThemeData.labelTextStyle]. If this are null, the default text style would use [TextTheme.labelLarge] with [ColorScheme.onSurfaceVariant].

### enabled

```dart
bool enabled
```

Indicates that this destination is selectable.

Defaults to true.

### build()

```dart
Widget build(BuildContext context)
```
