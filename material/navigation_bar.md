@docImport 'package:flutter/services.dart'; @docImport 'bottom_navigation_bar.dart'; @docImport 'navigation_rail.dart'; @docImport 'scaffold.dart';

# NavigationBar

```dart
class NavigationBar extends StatelessWidget {}
```

Material 3 Navigation Bar component.

{@youtube 560 315 https://www.youtube.com/watch?v=DVGYddFaLv0}

Navigation bars offer a persistent and convenient way to switch between primary destinations in an app.

This widget does not adjust its size with the [ThemeData.visualDensity].

The [MediaQueryData.textScaler] does not adjust the size of this widget but rather the size of the [Tooltip]s displayed on long presses of the destinations.

The style for the icons and text are not affected by parent [DefaultTextStyle]s or [IconTheme]s but rather controlled by parameters or the [NavigationBarThemeData].

This widget holds a collection of destinations (usually [NavigationDestination]s).

{@tool dartpad} This example shows a [NavigationBar] as it is used within a [Scaffold] widget. The [NavigationBar] has three [NavigationDestination] widgets and the initial [selectedIndex] is set to index 0. The [onDestinationSelected] callback changes the selected item's index and displays a corresponding widget in the body of the [Scaffold].

** See code in examples/api/lib/material/navigation_bar/navigation_bar.0.dart ** {@end-tool}

{@tool dartpad} This example showcases [NavigationBar] label behaviors. When tapping on one of the label behavior options, the [labelBehavior] of the [NavigationBar] will be updated.

** See code in examples/api/lib/material/navigation_bar/navigation_bar.1.dart ** {@end-tool}

{@tool dartpad} This example shows a [NavigationBar] within a main [Scaffold] widget that's used to control the visibility of destination pages. Each destination has its own scaffold and a nested navigator that provides local navigation. The example's [NavigationBar] has four [NavigationDestination] widgets with different color schemes. Its [onDestinationSelected] callback changes the selected destination's index and displays a corresponding page with its own local navigator and scaffold - all within the body of the main scaffold. The destination pages are organized in a [Stack] and switching destinations fades out the current page and fades in the new one. Destinations that aren't visible or animating are kept [Offstage].

** See code in examples/api/lib/material/navigation_bar/navigation_bar.2.dart ** {@end-tool} See also:

- [NavigationDestination]
- [BottomNavigationBar]
- <https://api.flutter.dev/flutter/material/NavigationDestination-class.html>
- <https://m3.material.io/components/navigation-bar>

### NavigationBar()

```dart
NavigationBar({dynamic key, Duration? animationDuration, int selectedIndex = 0, required List<Widget> destinations, ValueChanged<int>? onDestinationSelected, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Color? indicatorColor, ShapeBorder? indicatorShape, double? height, NavigationDestinationLabelBehavior? labelBehavior, WidgetStateProperty<Color?>? overlayColor, WidgetStateProperty<TextStyle?>? labelTextStyle, EdgeInsetsGeometry? labelPadding, bool maintainBottomViewPadding = false})
```

Creates a Material 3 Navigation Bar component.

The value of [destinations] must be a list of two or more [NavigationDestination] values.

### animationDuration

```dart
Duration? animationDuration
```

Determines the transition time for each destination as it goes between selected and unselected.

### selectedIndex

```dart
int selectedIndex
```

Determines which one of the [destinations] is currently selected.

When this is updated, the destination (from [destinations]) at [selectedIndex] goes from unselected to selected.

### destinations

```dart
List<Widget> destinations
```

The list of destinations (usually [NavigationDestination]s) in this [NavigationBar].

When [selectedIndex] is updated, the destination from this list at [selectedIndex] will animate from 0 (unselected) to 1.0 (selected). When the animation is increasing or completed, the destination is considered selected, when the animation is decreasing or dismissed, the destination is considered unselected.

### onDestinationSelected

```dart
ValueChanged<int>? onDestinationSelected
```

Called when one of the [destinations] is selected.

This callback usually updates the int passed to [selectedIndex].

Upon updating [selectedIndex], the [NavigationBar] will be rebuilt.

### backgroundColor

```dart
Color? backgroundColor
```

The color of the [NavigationBar] itself.

If null, [NavigationBarThemeData.backgroundColor] is used. If that is also null, then if [ThemeData.useMaterial3] is true, the value is [ColorScheme.surfaceContainer]. If that is false, the default blends [ColorScheme.surface] and [ColorScheme.onSurface] using an [ElevationOverlay].

### elevation

```dart
double? elevation
```

The elevation of the [NavigationBar] itself.

If null, [NavigationBarThemeData.elevation] is used. If that is also null, then if [ThemeData.useMaterial3] is true then it will be 3.0 otherwise 0.0.

### shadowColor

```dart
Color? shadowColor
```

The color used for the drop shadow to indicate elevation.

If null, [NavigationBarThemeData.shadowColor] is used. If that is also null, the default value is [Colors.transparent] which indicates that no drop shadow will be displayed.

See [Material.shadowColor] for more details on drop shadows.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color used as an overlay on [backgroundColor] to indicate elevation.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If null, [NavigationBarThemeData.surfaceTintColor] is used. If that is also null, the default value is [Colors.transparent].

See [Material.surfaceTintColor] for more details on how this overlay is applied.

### indicatorColor

```dart
Color? indicatorColor
```

The color of the [indicatorShape] when this destination is selected.

If null, [NavigationBarThemeData.indicatorColor] is used. If that is also null and [ThemeData.useMaterial3] is true, [ColorScheme.secondaryContainer] is used. Otherwise, [ColorScheme.secondary] with an opacity of 0.24 is used.

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

The shape of the selected indicator.

If null, [NavigationBarThemeData.indicatorShape] is used. If that is also null and [ThemeData.useMaterial3] is true, [StadiumBorder] is used. Otherwise, [RoundedRectangleBorder] with a circular border radius of 16 is used.

### height

```dart
double? height
```

The height of the [NavigationBar] itself.

If this is used in [Scaffold.bottomNavigationBar] and the scaffold is full-screen, the safe area padding is also added to the height automatically.

The height does not adjust with [ThemeData.visualDensity] or [MediaQueryData.textScaler] as this component loses usability at larger and smaller sizes due to the truncating of labels or smaller tap targets.

If null, [NavigationBarThemeData.height] is used. If that is also null, the default is 80.

### labelBehavior

```dart
NavigationDestinationLabelBehavior? labelBehavior
```

Defines how the [destinations]' labels will be laid out and when they'll be displayed.

Can be used to show all labels, show only the selected label, or hide all labels.

If null, [NavigationBarThemeData.labelBehavior] is used. If that is also null, the default is [NavigationDestinationLabelBehavior.alwaysShow].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The highlight color that's typically used to indicate that the [NavigationDestination] is focused, hovered, or pressed.

### labelTextStyle

```dart
WidgetStateProperty<TextStyle?>? labelTextStyle
```

/ The text style of the label.

If null, [NavigationBarThemeData.labelTextStyle] is used. If that is also null, the default text style is [TextTheme.labelMedium] with [ColorScheme.onSurface] when the destination is selected, and [ColorScheme.onSurfaceVariant] when the destination is unselected, and [ColorScheme.onSurfaceVariant] with an opacity of 0.38 when the destination is disabled.

If [ThemeData.useMaterial3] is false, then the default text style is [TextTheme.labelSmall] with [ColorScheme.onSurface].

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

The padding around the [NavigationDestination.label] widget.

When [labelPadding] is null, [NavigationBarThemeData.labelPadding] is used. If that is also null, the default padding is 4 pixels on the top.

### maintainBottomViewPadding

```dart
bool maintainBottomViewPadding
```

Specifies whether the underlying [SafeArea] should maintain the bottom [MediaQueryData.viewPadding] instead of the bottom [MediaQueryData.padding].

When true, this will prevent the [NavigationBar] from shifting when opening a software keyboard due to the change in the padding value, especially when the app uses [SystemUiMode.edgeToEdge], which renders the system bars over the application instead of outside it.

Defaults to false.

See also:

- [SafeArea.maintainBottomViewPadding], which specifies whether the [SafeArea] should maintain the bottom [MediaQueryData.viewPadding].
- [SystemUiMode.edgeToEdge], which sets a fullscreen display with status and navigation elements rendered over the application.

### build()

```dart
Widget build(BuildContext context)
```

# NavigationDestinationLabelBehavior

```dart
enum NavigationDestinationLabelBehavior {}
```

Specifies when each [NavigationDestination]'s label should appear.

This is used to determine the behavior of [NavigationBar]'s destinations.

Always shows all of the labels under each navigation bar destination, selected and unselected.

Never shows any of the labels under the navigation bar destinations, regardless of selected vs unselected.

Only shows the labels of the selected navigation bar destination.

When a destination is unselected, the label will be faded out, and the icon will be centered.

When a destination is selected, the label will fade in and the label and icon will slide up so that they are both centered.

# NavigationDestination

```dart
class NavigationDestination extends StatelessWidget {}
```

A Material 3 [NavigationBar] destination.

Displays a label below an icon. Use with [NavigationBar.destinations].

See also:

- [NavigationBar], for an interactive code sample.

### NavigationDestination()

```dart
NavigationDestination({dynamic key, required Widget icon, Widget? selectedIcon, required String label, String? tooltip, bool enabled = true})
```

Creates a navigation bar destination with an icon and a label, to be used in the [NavigationBar.destinations].

### icon

```dart
Widget icon
```

The [Widget] (usually an [Icon]) that's displayed for this [NavigationDestination].

The icon will use [NavigationBarThemeData.iconTheme]. If this is null, the default [IconThemeData] would use a size of 24.0 and [ColorScheme.onSurface].

### selectedIcon

```dart
Widget? selectedIcon
```

The optional [Widget] (usually an [Icon]) that's displayed when this [NavigationDestination] is selected.

If [selectedIcon] is non-null, the destination will fade from [icon] to [selectedIcon] when this destination goes from unselected to selected.

The icon will use [NavigationBarThemeData.iconTheme] with [WidgetState.selected]. If this is null, the default [IconThemeData] would use a size of 24.0 and [ColorScheme.onSurface].

### label

```dart
String label
```

The text label that appears below the icon of this [NavigationDestination].

The accompanying [Text] widget will use [NavigationBarThemeData.labelTextStyle]. If this is null, the default text style will use [TextTheme.labelMedium] with [ColorScheme.onSurface] when the destination is selected and [ColorScheme.onSurfaceVariant] when the destination is unselected. If [ThemeData.useMaterial3] is false, then the default text style will use [TextTheme.labelSmall] with [ColorScheme.onSurface].

### tooltip

```dart
String? tooltip
```

The text to display in the tooltip for this [NavigationDestination], when the user long presses the destination.

If [tooltip] is an empty string, no tooltip will be used.

Defaults to null, in which case the [label] text will be used.

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

# NavigationIndicator

```dart
class NavigationIndicator extends StatelessWidget {}
```

Selection Indicator for the Material 3 [NavigationBar] and [NavigationRail] components.

When [animation] is 0, the indicator is not present. As [animation] grows from 0 to 1, the indicator scales in on the x axis.

Used in a [Stack] widget behind the icons in the Material 3 Navigation Bar to illuminate the selected destination.

### NavigationIndicator()

```dart
NavigationIndicator({dynamic key, required Animation<double> animation, Color? color, double width = _kIndicatorWidth, double height = _kIndicatorHeight, BorderRadius borderRadius = const BorderRadius.all(Radius.circular(16)), ShapeBorder? shape})
```

Builds an indicator, usually used in a stack behind the icon of a navigation bar destination.

### animation

```dart
Animation<double> animation
```

Determines the scale of the indicator.

When [animation] is 0, the indicator is not present. The indicator scales in as [animation] grows from 0 to 1.

### color

```dart
Color? color
```

The fill color of this indicator.

If null, defaults to [ColorScheme.secondary].

### width

```dart
double width
```

The width of this indicator.

Defaults to `64`.

### height

```dart
double height
```

The height of this indicator.

Defaults to `32`.

### borderRadius

```dart
BorderRadius borderRadius
```

The border radius of the shape of the indicator.

This is used to create a [RoundedRectangleBorder] shape for the indicator. This is ignored if [shape] is non-null.

Defaults to `BorderRadius.circular(16)`.

### shape

```dart
ShapeBorder? shape
```

The shape of the indicator.

If non-null this is used as the shape used to draw the background of the indicator. If null then a [RoundedRectangleBorder] with the [borderRadius] is used.

### build()

```dart
Widget build(BuildContext context)
```
