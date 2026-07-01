@docImport 'bottom_navigation_bar.dart'; @docImport 'floating_action_button.dart'; @docImport 'icons.dart'; @docImport 'scaffold.dart';

# NavigationRail

```dart
class NavigationRail extends StatefulWidget {}
```

A Material Design widget that is meant to be displayed at the left or right of an app to navigate between a small number of views, typically between three and five.

{@youtube 560 315 https://www.youtube.com/watch?v=y9xchtVTtqQ}

The navigation rail is meant for layouts with wide viewports, such as a desktop web or tablet landscape layout. For smaller layouts, like mobile portrait, a [BottomNavigationBar] should be used instead.

A navigation rail is usually used as the first or last element of a [Row] which defines the app's [Scaffold] body.

The appearance of all of the [NavigationRail]s within an app can be specified with [NavigationRailTheme]. The default values for null theme properties are based on the [Theme]'s [ThemeData.textTheme], [ThemeData.iconTheme], and [ThemeData.colorScheme].

Adaptive layouts can build different instances of the [Scaffold] in order to have a navigation rail for more horizontal layouts and a bottom navigation bar for more vertical layouts. See [the adaptive_scaffold.dart sample](https://github.com/flutter/demos/blob/main/web_dashboard/lib/src/widgets/third_party/adaptive_scaffold.dart) for an example.

{@tool dartpad} This sample shows the creation of [NavigationRail] widget used within a Scaffold with 3 [NavigationRailDestination]s, as described in: https://m3.material.io/components/navigation-rail/overview

** See code in examples/api/lib/material/navigation_rail/navigation_rail.0.dart ** {@end-tool}

See also:

- [Scaffold], which can display the navigation rail within a [Row] of the [Scaffold.body] slot.
- [NavigationRailDestination], which is used as a model to create tappable destinations in the navigation rail.
- [BottomNavigationBar], which is a similar navigation widget that's laid out horizontally.
- <https://material.io/components/navigation-rail/>
- <https://m3.material.io/components/navigation-rail>

### NavigationRail()

```dart
NavigationRail({dynamic key, Color? backgroundColor, bool extended = false, Widget? leading, Widget? trailing, required List<NavigationRailDestination> destinations, required int? selectedIndex, ValueChanged<int>? onDestinationSelected, double? elevation, double? groupAlignment, NavigationRailLabelType? labelType, TextStyle? unselectedLabelTextStyle, TextStyle? selectedLabelTextStyle, IconThemeData? unselectedIconTheme, IconThemeData? selectedIconTheme, double? minWidth, double? minExtendedWidth, bool? useIndicator, Color? indicatorColor, ShapeBorder? indicatorShape, bool leadingAtTop = true, bool trailingAtBottom = false, bool scrollable = false, MainAxisAlignment? mainAxisAlignment})
```

Creates a Material Design navigation rail.

The value of [destinations] must be a list of zero or more [NavigationRailDestination] values.

If [elevation] is specified, it must be non-negative.

If [minWidth] is specified, it must be non-negative, and if [minExtendedWidth] is specified, it must be non-negative and greater than [minWidth].

The [extended] argument can only be set to true when the [labelType] is null or [NavigationRailLabelType.none].

If [backgroundColor], [elevation], [groupAlignment], [labelType], [unselectedLabelTextStyle], [selectedLabelTextStyle], [unselectedIconTheme], or [selectedIconTheme] are null, then their [NavigationRailThemeData] values will be used. If the corresponding [NavigationRailThemeData] property is null, then the navigation rail defaults are used. See the individual properties for more information.

Typically used within a [Row] that defines the [Scaffold.body] property.

### backgroundColor

```dart
Color? backgroundColor
```

Sets the color of the Container that holds all of the [NavigationRail]'s contents.

The default value is [NavigationRailThemeData.backgroundColor]. If [NavigationRailThemeData.backgroundColor] is null, then the default value is based on [ColorScheme.surface] of [ThemeData.colorScheme].

### extended

```dart
bool extended
```

Indicates that the [NavigationRail] should be in the extended state.

The extended state has a wider rail container, and the labels are positioned next to the icons. [minExtendedWidth] can be used to set the minimum width of the rail when it is in this state.

The rail will implicitly animate between the extended and normal state.

If the rail is going to be in the extended state, then the [labelType] must be set to [NavigationRailLabelType.none].

The default value is false.

### leading

```dart
Widget? leading
```

The leading widget in the rail that is placed above the destinations.

It is placed at the top of the rail, above the [destinations]. Its location is not affected by [groupAlignment].

This is commonly a [FloatingActionButton], but may also be a non-button, such as a logo.

The default value is null.

### trailing

```dart
Widget? trailing
```

The trailing widget in the rail that is placed below the destinations.

The trailing widget is placed below the last [NavigationRailDestination]. It's location is affected by [groupAlignment].

This is commonly a list of additional options or destinations that is usually only rendered when [extended] is true.

The default value is null.

### destinations

```dart
List<NavigationRailDestination> destinations
```

Defines the appearance of the button items that are arrayed within the navigation rail.

The value must be a list of zero or more [NavigationRailDestination] values.

### selectedIndex

```dart
int? selectedIndex
```

The index into [destinations] for the current selected [NavigationRailDestination] or null if no destination is selected.

### onDestinationSelected

```dart
ValueChanged<int>? onDestinationSelected
```

Called when one of the [destinations] is selected.

The stateful widget that creates the navigation rail needs to keep track of the index of the selected [NavigationRailDestination] and call `setState` to rebuild the navigation rail with the new [selectedIndex].

### elevation

```dart
double? elevation
```

The rail's elevation or z-coordinate.

If [Directionality] is [TextDirection.ltr], the inner side is the right side, and if [Directionality] is [TextDirection.rtl], it is the left side.

The default value is 0.

### groupAlignment

```dart
double? groupAlignment
```

The vertical alignment for the group of [destinations] within the rail.

The [NavigationRailDestination]s are by default grouped together with the [trailing] widget, due to [trailingAtBottom] being `false`. The [leading] widget, can also be in the aligned group by setting [leadingAtTop] to `false`. If these widgets are not included in the group, they are placed at the top and bottom, respectively, of the rail and only the space between them is considered for the alignment.

The value must be between -1.0 and 1.0.

If [groupAlignment] is -1.0, then the items are aligned to the top. If [groupAlignment] is 0.0, then the items are aligned to the center. If [groupAlignment] is 1.0, then the items are aligned to the bottom.

The default is -1.0.

See also:

- [Alignment.y]

### labelType

```dart
NavigationRailLabelType? labelType
```

Defines the layout and behavior of the labels for the default, unextended [NavigationRail].

When a navigation rail is [extended], the labels are always shown.

The default value is [NavigationRailThemeData.labelType]. If [NavigationRailThemeData.labelType] is null, then the default value is [NavigationRailLabelType.none].

See also:

- [NavigationRailLabelType] for information on the meaning of different types.

### unselectedLabelTextStyle

```dart
TextStyle? unselectedLabelTextStyle
```

The [TextStyle] of a destination's label when it is unselected.

When one of the [destinations] is selected the [selectedLabelTextStyle] will be used instead.

The default value is based on the [Theme]'s [TextTheme.bodyLarge]. The default color is based on the [Theme]'s [ColorScheme.onSurface].

Properties from this text style, or [NavigationRailThemeData.unselectedLabelTextStyle] if this is null, are merged into the defaults.

### selectedLabelTextStyle

```dart
TextStyle? selectedLabelTextStyle
```

The [TextStyle] of a destination's label when it is selected.

When a [NavigationRailDestination] is not selected, [unselectedLabelTextStyle] will be used.

The default value is based on the [TextTheme.bodyLarge] of [ThemeData.textTheme]. The default color is based on the [Theme]'s [ColorScheme.primary].

Properties from this text style, or [NavigationRailThemeData.selectedLabelTextStyle] if this is null, are merged into the defaults.

### unselectedIconTheme

```dart
IconThemeData? unselectedIconTheme
```

The visual properties of the icon in the unselected destination.

If this field is not provided, or provided with any null properties, then a copy of the [IconThemeData.fallback] with a custom [NavigationRail] specific color will be used.

The default value is the [Theme]'s [ThemeData.iconTheme] with a color of the [Theme]'s [ColorScheme.onSurface] with an opacity of 0.64. Properties from this icon theme, or [NavigationRailThemeData.unselectedIconTheme] if this is null, are merged into the defaults.

### selectedIconTheme

```dart
IconThemeData? selectedIconTheme
```

The visual properties of the icon in the selected destination.

When a [NavigationRailDestination] is not selected, [unselectedIconTheme] will be used.

The default value is the [Theme]'s [ThemeData.iconTheme] with a color of the [Theme]'s [ColorScheme.primary]. Properties from this icon theme, or [NavigationRailThemeData.selectedIconTheme] if this is null, are merged into the defaults.

### minWidth

```dart
double? minWidth
```

The smallest possible width for the rail regardless of the destination's icon or label size.

The default is 72.

This value also defines the min width and min height of the destinations.

To make a compact rail, set this to 56 and use [NavigationRailLabelType.none].

### minExtendedWidth

```dart
double? minExtendedWidth
```

The final width when the animation is complete for setting [extended] to true.

This is only used when [extended] is set to true.

The default value is 256.

### useIndicator

```dart
bool? useIndicator
```

If `true`, adds a rounded [NavigationIndicator] behind the selected destination's icon.

The indicator's shape will be circular if [labelType] is [NavigationRailLabelType.none], or a [StadiumBorder] if [labelType] is [NavigationRailLabelType.all] or [NavigationRailLabelType.selected].

If `null`, defaults to [NavigationRailThemeData.useIndicator]. If that is `null`, defaults to [ThemeData.useMaterial3].

### indicatorColor

```dart
Color? indicatorColor
```

Overrides the default value of [NavigationRail]'s selection indicator color, when [useIndicator] is true.

If this is null, [NavigationRailThemeData.indicatorColor] is used. If that is null, defaults to [ColorScheme.secondaryContainer].

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

Overrides the default value of [NavigationRail]'s selection indicator shape, when [useIndicator] is true.

If this is null, [NavigationRailThemeData.indicatorShape] is used. If that is null, defaults to [StadiumBorder].

### leadingAtTop

```dart
bool leadingAtTop
```

Pin the [leading] widget to the top.

If `true`, the [leading] widget is pinned to the top of the [NavigationRail]. Otherwise it precedes directly the main group of [destinations].

See also [scrollable] for a description of the interplay of these parameters.

### trailingAtBottom

```dart
bool trailingAtBottom
```

Pin the [trailing] widget to the bottom.

If `true`, the [trailing] widget is pinned to the bottom of the [NavigationRail]. Otherwise it follows directly the main group of [destinations].

See also [scrollable] for a description of the interplay of these parameters.

### scrollable

```dart
bool scrollable
```

Whether the main group of items should be scrollable when vertical space is insufficient to show all of [destinations], [leading] and [trailing].

If [leadingAtTop] or [trailingAtBottom] are false, [leading] or [trailing] widgets, respectively, are part of the main group in addition to [destinations]. Otherwise these are statical at the top or bottom, respectively.

### mainAxisAlignment

```dart
MainAxisAlignment? mainAxisAlignment
```

How the [destinations] should be placed along the vertical axis.

When there is extra vertical space in the [NavigationRail], this property controls the alignment and spacing of the items. For example, setting this to [MainAxisAlignment.spaceEvenly] will distribute the destinations equally along the available vertical space.

When this property is not null, [groupAlignment] is ignored.

If null, the layout behaves as if [MainAxisAlignment.start] was specified.

See also:

- [Column.mainAxisAlignment], which describes the different values and their effects on the layout.

### extendedAnimation()

```dart
Animation<double> extendedAnimation(BuildContext context)
```

Returns the animation that controls the [NavigationRail.extended] state.

This can be used to synchronize animations in the [leading] or [trailing] widget, such as an animated menu or a [FloatingActionButton] animation.

{@tool dartpad} This example shows how to use this animation to create a [FloatingActionButton] that animates itself between the normal and extended states of the [NavigationRail].

An instance of `MyNavigationRailFab` is created for [NavigationRail.leading]. Pressing the FAB button toggles the "extended" state of the [NavigationRail].

** See code in examples/api/lib/material/navigation_rail/navigation_rail.extended_animation.0.dart ** {@end-tool}

### createState()

```dart
State<NavigationRail> createState()
```

# NavigationRailLabelType

```dart
enum NavigationRailLabelType {}
```

Defines the behavior of the labels of a [NavigationRail].

See also:

- [NavigationRail]

Only the [NavigationRailDestination]s are shown.

Only the selected [NavigationRailDestination] will show its label.

The label will animate in and out as new [NavigationRailDestination]s are selected.

All [NavigationRailDestination]s will show their label.

# NavigationRailDestination

```dart
class NavigationRailDestination {}
```

Defines a [NavigationRail] button that represents one "destination" view.

See also:

- [NavigationRail]

### NavigationRailDestination()

```dart
NavigationRailDestination({required Widget icon, Widget? selectedIcon, Color? indicatorColor, ShapeBorder? indicatorShape, required Widget label, EdgeInsetsGeometry? padding, bool disabled = false})
```

Creates a destination that is used with [NavigationRail.destinations].

When the [NavigationRail.labelType] is [NavigationRailLabelType.none], the label is still used for semantics, and may still be used if [NavigationRail.extended] is true.

### icon

```dart
Widget icon
```

The icon of the destination.

Typically the icon is an [Icon] or an [ImageIcon] widget. If another type of widget is provided then it should configure itself to match the current [IconTheme] size and color.

If [selectedIcon] is provided, this will only be displayed when the destination is not selected.

To make the [NavigationRail] more accessible, consider choosing an icon with a stroked and filled version, such as [Icons.cloud] and [Icons.cloud_queue]. The [icon] should be set to the stroked version and [selectedIcon] to the filled version.

### selectedIcon

```dart
Widget selectedIcon
```

An alternative icon displayed when this destination is selected.

If this icon is not provided, the [NavigationRail] will display [icon] in either state. The size, color, and opacity of the [NavigationRail.selectedIconTheme] will still apply.

See also:

- [NavigationRailDestination.icon], for a description of how to pair icons.

### indicatorColor

```dart
Color? indicatorColor
```

The color of the [indicatorShape] when this destination is selected.

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

The shape of the selection indicator.

### label

```dart
Widget label
```

The label for the destination.

The label must be provided when used with the [NavigationRail]. When the [NavigationRail.labelType] is [NavigationRailLabelType.none], the label is still used for semantics, and may still be used if [NavigationRail.extended] is true.

### padding

```dart
EdgeInsetsGeometry? padding
```

The amount of space to inset the destination item.

### disabled

```dart
bool disabled
```

Indicates that this destination is inaccessible.
