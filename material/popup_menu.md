@docImport 'menu_anchor.dart'; @docImport 'text_button.dart';

# PopupMenuEntry

```dart
abstract class PopupMenuEntry<T> extends StatefulWidget {}
```

A base class for entries in a Material Design popup menu.

The popup menu widget uses this interface to interact with the menu items. To show a popup menu, use the [showMenu] function. To create a button that shows a popup menu, consider using [PopupMenuButton].

The type `T` is the type of the value(s) the entry represents. All the entries in a given menu must represent values with consistent types.

A [PopupMenuEntry] may represent multiple values, for example a row with several icons, or a single entry, for example a menu item with an icon (see [PopupMenuItem]), or no value at all (for example, [PopupMenuDivider]).

See also:

- [PopupMenuItem], a popup menu entry for a single value.
- [PopupMenuDivider], a popup menu entry that is just a horizontal line.
- [CheckedPopupMenuItem], a popup menu item with a checkmark.
- [showMenu], a method to dynamically show a popup menu at a given location.
- [PopupMenuButton], an [IconButton] that automatically shows a menu when it is tapped.

### PopupMenuEntry()

```dart
PopupMenuEntry({dynamic key})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### height

```dart
double get height
```

The amount of vertical space occupied by this entry.

This value is used at the time the [showMenu] method is called, if the `initialValue` argument is provided, to determine the position of this entry when aligning the selected entry over the given `position`. It is otherwise ignored.

### represents()

```dart
bool represents(T? value)
```

Whether this entry represents a particular value.

This method is used by [showMenu], when it is called, to align the entry representing the `initialValue`, if any, to the given `position`, and then later is called on each entry to determine if it should be highlighted (if the method returns true, the entry will have its background color set to the ambient [ThemeData.highlightColor]). If `initialValue` is null, then this method is not called.

If the [PopupMenuEntry] represents a single value, this should return true if the argument matches that value. If it represents multiple values, it should return true if the argument matches any of them.

# PopupMenuDivider

```dart
class PopupMenuDivider extends PopupMenuEntry<Never> {}
```

A horizontal divider in a Material Design popup menu.

This widget adapts the [Divider] for use in popup menus.

See also:

- [PopupMenuItem], for the kinds of items that this widget divides.
- [showMenu], a method to dynamically show a popup menu at a given location.
- [PopupMenuButton], an [IconButton] that automatically shows a menu when it is tapped.

### PopupMenuDivider()

```dart
PopupMenuDivider({dynamic key, double height = _kMenuDividerHeight, double? thickness, double? indent, double? endIndent, BorderRadiusGeometry? radius, Color? color})
```

Creates a horizontal divider for a popup menu.

By default, the divider has a height of 16 logical pixels.

### height

```dart
double height
```

The height of the divider entry.

Defaults to 16 pixels.

### thickness

```dart
double? thickness
```

The thickness of the line drawn within the [PopupMenuDivider].

{@macro flutter.material.Divider.thickness}

### indent

```dart
double? indent
```

The amount of empty space to the leading edge of the [PopupMenuDivider].

{@macro flutter.material.Divider.indent}

### endIndent

```dart
double? endIndent
```

The amount of empty space to the trailing edge of the [PopupMenuDivider].

{@macro flutter.material.Divider.endIndent}

### radius

```dart
BorderRadiusGeometry? radius
```

The amount of radius for the border of the [PopupMenuDivider].

{@macro flutter.material.Divider.radius}

### color

```dart
Color? color
```

{@macro flutter.material.Divider.color}

{@tool snippet}

```dart
const PopupMenuDivider(
  color: Colors.deepOrange,
)
```

{@end-tool}

### represents()

```dart
bool represents(void value)
```

### createState()

```dart
State<PopupMenuDivider> createState()
```

# PopupMenuItem

```dart
class PopupMenuItem<T> extends PopupMenuEntry<T> {}
```

An item in a Material Design popup menu.

To show a popup menu, use the [showMenu] function. To create a button that shows a popup menu, consider using [PopupMenuButton].

To show a checkmark next to a popup menu item, consider using [CheckedPopupMenuItem].

Typically the [child] of a [PopupMenuItem] is a [Text] widget. More elaborate menus with icons can use a [ListTile]. By default, a [PopupMenuItem] is [kMinInteractiveDimension] pixels high. If you use a widget with a different height, it must be specified in the [height] property.

{@tool snippet}

Here, a [Text] widget is used with a popup menu item. The `Menu` type is an enum, not shown here.

```dart
const PopupMenuItem<Menu>(
  value: Menu.itemOne,
  child: Text('Item 1'),
)
```

{@end-tool}

See the example at [PopupMenuButton] for how this example could be used in a complete menu, and see the example at [CheckedPopupMenuItem] for one way to keep the text of [PopupMenuItem]s that use [Text] widgets in their [child] slot aligned with the text of [CheckedPopupMenuItem]s or of [PopupMenuItem] that use a [ListTile] in their [child] slot.

See also:

- [PopupMenuDivider], which can be used to divide items from each other.
- [CheckedPopupMenuItem], a variant of [PopupMenuItem] with a checkmark.
- [showMenu], a method to dynamically show a popup menu at a given location.
- [PopupMenuButton], an [IconButton] that automatically shows a menu when it is tapped.

### PopupMenuItem()

```dart
PopupMenuItem({dynamic key, T? value, VoidCallback? onTap, bool enabled = true, double height = kMinInteractiveDimension, EdgeInsets? padding, TextStyle? textStyle, WidgetStateProperty<TextStyle?>? labelTextStyle, MouseCursor? mouseCursor, required Widget? child})
```

Creates an item for a popup menu.

By default, the item is [enabled].

### value

```dart
T? value
```

The value that will be returned by [showMenu] if this entry is selected.

### onTap

```dart
VoidCallback? onTap
```

Called when the menu item is tapped.

### enabled

```dart
bool enabled
```

Whether the user is permitted to select this item.

Defaults to true. If this is false, then the item will not react to touches.

### height

```dart
double height
```

The minimum height of the menu item.

Defaults to [kMinInteractiveDimension] pixels.

### padding

```dart
EdgeInsets? padding
```

The padding of the menu item.

The [height] property may interact with the applied padding. For example, If a [height] greater than the height of the sum of the padding and [child] is provided, then the padding's effect will not be visible.

If this is null and [ThemeData.useMaterial3] is true, the horizontal padding defaults to 12.0 on both sides.

If this is null and [ThemeData.useMaterial3] is false, the horizontal padding defaults to 16.0 on both sides.

### textStyle

```dart
TextStyle? textStyle
```

The text style of the popup menu item.

If this property is null, then [PopupMenuThemeData.textStyle] is used. If [PopupMenuThemeData.textStyle] is also null, then [TextTheme.titleMedium] of [ThemeData.textTheme] is used.

### labelTextStyle

```dart
WidgetStateProperty<TextStyle?>? labelTextStyle
```

The label style of the popup menu item.

When [ThemeData.useMaterial3] is true, this styles the text of the popup menu item.

If this property is null, then [PopupMenuThemeData.labelTextStyle] is used. If [PopupMenuThemeData.labelTextStyle] is also null, then [TextTheme.labelLarge] is used with the [ColorScheme.onSurface] color when popup menu item is enabled and the [ColorScheme.onSurface] color with 0.38 opacity when the popup menu item is disabled.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

{@template flutter.material.popupmenu.mouseCursor} The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If null, then the value of [PopupMenuThemeData.mouseCursor] is used. If that is also null, then [WidgetStateMouseCursor.adaptiveClickable] is used.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

Typically a single-line [ListTile] (for menus with icons) or a [Text]. An appropriate [DefaultTextStyle] is put in scope for the child. In either case, the text should be short enough that it won't wrap.

### represents()

```dart
bool represents(T? value)
```

### createState()

```dart
PopupMenuItemState<T, PopupMenuItem<T>> createState()
```

# PopupMenuItemState

```dart
class PopupMenuItemState<T, W extends PopupMenuItem<T>> extends State<W> {}
```

The [State] for [PopupMenuItem] subclasses.

By default this implements the basic styling and layout of Material Design popup menu items.

The [buildChild] method can be overridden to adjust exactly what gets placed in the menu. By default it returns [PopupMenuItem.child].

The [handleTap] method can be overridden to adjust exactly what happens when the item is tapped. By default, it uses [Navigator.pop] to return the [PopupMenuItem.value] from the menu route.

This class takes two type arguments. The second, `W`, is the exact type of the [Widget] that is using this [State]. It must be a subclass of [PopupMenuItem]. The first, `T`, must match the type argument of that widget class, and is the type of values returned from this menu.

### buildChild()

```dart
Widget? buildChild()
```

The menu item contents.

Used by the [build] method.

By default, this returns [PopupMenuItem.child]. Override this to put something else in the menu entry.

### handleTap()

```dart
void handleTap()
```

The handler for when the user selects the menu item.

Used by the [InkWell] inserted by the [build] method.

By default, uses [Navigator.pop] to return the [PopupMenuItem.value] from the menu route.

### build()

```dart
Widget build(BuildContext context)
```

### buildSemantics()

```dart
Widget buildSemantics({required Widget child})
```

Builds the semantic wrapper for the popup menu item.

This method creates the [Semantics] widget that provides accessibility information for the menu item. By default, it sets the semantic role to [SemanticsRole.menuItem] and includes the enabled state and button flag.

Subclasses can override this method to customize the semantic properties. For example, [CheckedPopupMenuItem] overrides this to use [SemanticsRole.menuItemCheckbox] and include checked state information.

# CheckedPopupMenuItem

```dart
class CheckedPopupMenuItem<T> extends PopupMenuItem<T> {}
```

An item with a checkmark in a Material Design popup menu.

To show a popup menu, use the [showMenu] function. To create a button that shows a popup menu, consider using [PopupMenuButton].

A [CheckedPopupMenuItem] is kMinInteractiveDimension pixels high, which matches the default minimum height of a [PopupMenuItem]. The horizontal layout uses [ListTile]; the checkmark is an [Icons.done] icon, shown in the [ListTile.leading] position.

{@tool snippet}

Suppose a `Commands` enum exists that lists the possible commands from a particular popup menu, including `Commands.heroAndScholar` and `Commands.hurricaneCame`, and further suppose that there is a `_heroAndScholar` member field which is a boolean. The example below shows a menu with one menu item with a checkmark that can toggle the boolean, and one menu item without a checkmark for selecting the second option. (It also shows a divider placed between the two menu items.)

```dart
PopupMenuButton<Commands>(
  onSelected: (Commands result) {
    switch (result) {
      case Commands.heroAndScholar:
        setState(() { _heroAndScholar = !_heroAndScholar; });
      case Commands.hurricaneCame:
        // ...handle hurricane option
        break;
      // ...other items handled here
    }
  },
  itemBuilder: (BuildContext context) => <PopupMenuEntry<Commands>>[
    CheckedPopupMenuItem<Commands>(
      checked: _heroAndScholar,
      value: Commands.heroAndScholar,
      child: const Text('Hero and scholar'),
    ),
    const PopupMenuDivider(),
    const PopupMenuItem<Commands>(
      value: Commands.hurricaneCame,
      child: ListTile(leading: Icon(null), title: Text('Bring hurricane')),
    ),
    // ...other items listed here
  ],
)
```

{@end-tool}

In particular, observe how the second menu item uses a [ListTile] with a blank [Icon] in the [ListTile.leading] position to get the same alignment as the item with the checkmark.

See also:

- [PopupMenuItem], a popup menu entry for picking a command (as opposed to toggling a value).
- [PopupMenuDivider], a popup menu entry that is just a horizontal line.
- [showMenu], a method to dynamically show a popup menu at a given location.
- [PopupMenuButton], an [IconButton] that automatically shows a menu when it is tapped.

### CheckedPopupMenuItem()

```dart
CheckedPopupMenuItem({dynamic key, T? value, bool checked = false, bool enabled, dynamic padding, double height, dynamic labelTextStyle, dynamic mouseCursor, dynamic child, dynamic onTap})
```

Creates a popup menu item with a checkmark.

By default, the menu item is [enabled] but unchecked. To mark the item as checked, set [checked] to true.

### checked

```dart
bool checked
```

Whether to display a checkmark next to the menu item.

Defaults to false.

When true, an [Icons.done] checkmark is displayed.

When this popup menu item is selected, the checkmark will fade in or out as appropriate to represent the implied new state.

### child

```dart
Widget? get child
```

The widget below this widget in the tree.

Typically a [Text]. An appropriate [DefaultTextStyle] is put in scope for the child. The text should be short enough that it won't wrap.

This widget is placed in the [ListTile.title] slot of a [ListTile] whose [ListTile.leading] slot is an [Icons.done] icon.

### createState()

```dart
PopupMenuItemState<T, CheckedPopupMenuItem<T>> createState()
```

# PopupMenuPositionBuilder

```dart
typedef PopupMenuPositionBuilder = RelativeRect Function(BuildContext context, BoxConstraints constraints)
```

A builder that creates a [RelativeRect] to position a popup menu. Both [BuildContext] and [BoxConstraints] are from the [PopupRoute] that displays this menu.

The returned [RelativeRect] determines the position of the popup menu relative to the bounds of the [Navigator]'s overlay. The menu dimensions are not yet known when this callback is invoked, as they depend on the items and other properties of the menu.

The coordinate system used by the [RelativeRect] has its origin at the top left of the [Navigator]'s overlay. Positive y coordinates are down (below the origin), and positive x coordinates are to the right of the origin.

See also:

- [RelativeRect.fromLTRB], which creates a [RelativeRect] from left, top, right, and bottom coordinates.
- [RelativeRect.fromRect], which creates a [RelativeRect] from two [Rect]s, one representing the size of the popup menu and one representing the size of the overlay.

# showMenu()

```dart
Future<T?> showMenu<T>({required BuildContext context, RelativeRect? position, PopupMenuPositionBuilder? positionBuilder, required List<PopupMenuEntry<T>> items, T? initialValue, double? elevation, Color? shadowColor, Color? surfaceTintColor, String? semanticLabel, ShapeBorder? shape, EdgeInsetsGeometry? menuPadding, Color? color, bool useRootNavigator = false, BoxConstraints? constraints, Clip clipBehavior = Clip.none, RouteSettings? routeSettings, AnimationStyle? popUpAnimationStyle, bool? requestFocus})
```

Shows a popup menu that contains the `items` at `position`.

The `items` parameter must not be empty.

Only one of [position] or [positionBuilder] should be provided. Providing both throws an assertion error. The [positionBuilder] is called at the time the menu is shown to compute its position and every time the layout is updated, which is useful when the position needs to be determined at runtime based on the current layout.

If `initialValue` is specified then the first item with a matching value will be highlighted and the value of `position` gives the rectangle whose vertical center will be aligned with the vertical center of the highlighted item (when possible).

If `initialValue` is not specified then the top of the menu will be aligned with the top of the `position` rectangle.

In both cases, the menu position will be adjusted if necessary to fit on the screen.

Horizontally, the menu is positioned so that it grows in the direction that has the most room. For example, if the `position` describes a rectangle on the left edge of the screen, then the left edge of the menu is aligned with the left edge of the `position`, and the menu grows to the right. If both edges of the `position` are equidistant from the opposite edge of the screen, then the ambient [Directionality] is used as a tie-breaker, preferring to grow in the reading direction.

The positioning of the `initialValue` at the `position` is implemented by iterating over the `items` to find the first whose [PopupMenuEntry.represents] method returns true for `initialValue`, and then summing the values of [PopupMenuEntry.height] for all the preceding widgets in the list.

The `elevation` argument specifies the z-coordinate at which to place the menu. The elevation defaults to 8, the appropriate elevation for popup menus.

The `context` argument is used to look up the [Navigator] and [Theme] for the menu. It is only used when the method is called. Its corresponding widget can be safely removed from the tree before the popup menu is closed.

The `useRootNavigator` argument is used to determine whether to push the menu to the [Navigator] furthest from or nearest to the given `context`. It is `false` by default.

The `semanticLabel` argument is used by accessibility frameworks to announce screen transitions when the menu is opened and closed. If this label is not provided, it will default to [MaterialLocalizations.popupMenuLabel].

The `clipBehavior` argument is used to clip the shape of the menu. Defaults to [Clip.none].

The `requestFocus` argument specifies whether the menu should request focus when it appears. If it is null, [Navigator.requestFocus] is used instead.

See also:

- [PopupMenuItem], a popup menu entry for a single value.
- [PopupMenuDivider], a popup menu entry that is just a horizontal line.
- [CheckedPopupMenuItem], a popup menu item with a checkmark.
- [PopupMenuButton], which provides an [IconButton] that shows a menu by calling this method automatically.
- [SemanticsConfiguration.namesRoute], for a description of edge triggered semantics.

# PopupMenuItemSelected

```dart
typedef PopupMenuItemSelected<T> = void Function(T value)
```

Signature for the callback invoked when a menu item is selected. The argument is the value of the [PopupMenuItem] that caused its menu to be dismissed.

Used by [PopupMenuButton.onSelected].

# PopupMenuCanceled

```dart
typedef PopupMenuCanceled = void Function()
```

Signature for the callback invoked when a [PopupMenuButton] is dismissed without selecting an item.

Used by [PopupMenuButton.onCanceled].

# PopupMenuItemBuilder

```dart
typedef PopupMenuItemBuilder<T> = List<PopupMenuEntry<T>> Function(BuildContext context)
```

Signature used by [PopupMenuButton] to lazily construct the items shown when the button is pressed.

Used by [PopupMenuButton.itemBuilder].

# PopupMenuButton

```dart
class PopupMenuButton<T> extends StatefulWidget {}
```

Displays a menu when pressed and calls [onSelected] when the menu is dismissed because an item was selected. The value passed to [onSelected] is the value of the selected menu item.

One of [child] or [icon] may be provided, but not both. If [icon] is provided, then [PopupMenuButton] behaves like an [IconButton].

If both are null, then a standard overflow icon is created (depending on the platform).

## Updating to [MenuAnchor]

There is a Material 3 component, [MenuAnchor] that is preferred for applications that are configured for Material 3 (see [ThemeData.useMaterial3]). The [MenuAnchor] widget's visuals are a little bit different, see the Material 3 spec at <https://m3.material.io/components/menus/guidelines> for more details.

The [MenuAnchor] widget's API is also slightly different. [MenuAnchor]'s were built to be lower level interface for creating menus that are displayed from an anchor.

There are a few steps you would take to migrate from [PopupMenuButton] to [MenuAnchor]:

1.  Instead of using the [PopupMenuButton.itemBuilder] to build a list of [PopupMenuEntry]s, you would use the [MenuAnchor.menuChildren] which takes a list of [Widget]s. Usually, you would use a list of [MenuItemButton]s as shown in the example below.

2.  Instead of using the [PopupMenuButton.onSelected] callback, you would set individual callbacks for each of the [MenuItemButton]s using the [MenuItemButton.onPressed] property.

3.  To anchor the [MenuAnchor] to a widget, you would use the [MenuAnchor.builder] to return the widget of choice - usually a [TextButton] or an [IconButton].

4.  You may want to style the [MenuItemButton]s, see the [MenuItemButton] documentation for details.

Use the sample below for an example of migrating from [PopupMenuButton] to [MenuAnchor].

{@tool dartpad} This example shows a menu with three items, selecting between an enum's values and setting a `selectedMenu` field based on the selection.

** See code in examples/api/lib/material/popup_menu/popup_menu.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to migrate the above to a [MenuAnchor].

** See code in examples/api/lib/material/menu_anchor/menu_anchor.2.dart ** {@end-tool}

{@tool dartpad} This sample shows the creation of a popup menu, as described in: https://m3.material.io/components/menus/overview

** See code in examples/api/lib/material/popup_menu/popup_menu.1.dart ** {@end-tool}

{@tool dartpad} This sample showcases how to override the [PopupMenuButton] animation curves and duration using [AnimationStyle].

** See code in examples/api/lib/material/popup_menu/popup_menu.2.dart ** {@end-tool}

See also:

- [PopupMenuItem], a popup menu entry for a single value.
- [PopupMenuDivider], a popup menu entry that is just a horizontal line.
- [CheckedPopupMenuItem], a popup menu item with a checkmark.
- [showMenu], a method to dynamically show a popup menu at a given location.

### PopupMenuButton()

```dart
PopupMenuButton({dynamic key, required PopupMenuItemBuilder<T> itemBuilder, T? initialValue, VoidCallback? onOpened, PopupMenuItemSelected<T>? onSelected, PopupMenuCanceled? onCanceled, String? tooltip, double? elevation, Color? shadowColor, Color? surfaceTintColor, EdgeInsetsGeometry padding = const EdgeInsets.all(8.0), EdgeInsetsGeometry? menuPadding, Widget? child, BorderRadius? borderRadius, double? splashRadius, Widget? icon, double? iconSize, Offset offset = Offset.zero, bool enabled = true, ShapeBorder? shape, Color? color, Color? iconColor, bool? enableFeedback, BoxConstraints? constraints, PopupMenuPosition? position, Clip clipBehavior = Clip.none, bool useRootNavigator = false, AnimationStyle? popUpAnimationStyle, RouteSettings? routeSettings, ButtonStyle? style, bool? requestFocus})
```

Creates a button that shows a popup menu.

### itemBuilder

```dart
PopupMenuItemBuilder<T> itemBuilder
```

Called when the button is pressed to create the items to show in the menu.

### initialValue

```dart
T? initialValue
```

The value of the menu item, if any, that should be highlighted when the menu opens.

### onOpened

```dart
VoidCallback? onOpened
```

Called when the popup menu is shown.

### onSelected

```dart
PopupMenuItemSelected<T>? onSelected
```

Called when the user selects a value from the popup menu created by this button.

If the popup menu is dismissed without selecting a value, [onCanceled] is called instead.

### onCanceled

```dart
PopupMenuCanceled? onCanceled
```

Called when the user dismisses the popup menu without selecting an item.

If the user selects a value, [onSelected] is called instead.

### tooltip

```dart
String? tooltip
```

Text that describes the action that will occur when the button is pressed.

This text is displayed when the user long-presses on the button and is used for accessibility.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place the menu when open. This controls the size of the shadow below the menu.

Defaults to 8, the appropriate elevation for popup menus.

### shadowColor

```dart
Color? shadowColor
```

The color used to paint the shadow below the menu.

If null then the ambient [PopupMenuThemeData.shadowColor] is used. If that is null too, then the overall theme's [ThemeData.shadowColor] (default black) is used.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color used as an overlay on [color] to indicate elevation.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If null, [PopupMenuThemeData.surfaceTintColor] is used. If that is also null, the default value is [Colors.transparent].

See [Material.surfaceTintColor] for more details on how this overlay is applied.

### padding

```dart
EdgeInsetsGeometry padding
```

Matches IconButton's 8 dps padding by default. In some cases, notably where this button appears as the trailing element of a list item, it's useful to be able to set the padding to zero.

### menuPadding

```dart
EdgeInsetsGeometry? menuPadding
```

If provided, menu padding is used for empty space around the outside of the popup menu.

If this property is null, then [PopupMenuThemeData.menuPadding] is used. If [PopupMenuThemeData.menuPadding] is also null, then vertical padding of 8 pixels is used.

### splashRadius

```dart
double? splashRadius
```

The splash radius.

If null, default splash radius of [InkWell] or [IconButton] is used.

### child

```dart
Widget? child
```

If provided, [child] is the widget used for this button and the button will utilize an [InkWell] for taps.

### borderRadius

```dart
BorderRadius? borderRadius
```

The border radius for the [InkWell] that wraps the [child].

Defaults to null, which indicates no border radius should be applied.

### icon

```dart
Widget? icon
```

If provided, the [icon] is used for this button and the button will behave like an [IconButton].

### offset

```dart
Offset offset
```

The offset is applied relative to the initial position set by the [position].

When not set, the offset defaults to [Offset.zero].

### enabled

```dart
bool enabled
```

Whether this popup menu button is interactive.

Defaults to true.

If true, the button will respond to presses by displaying the menu.

If false, the button is styled with the disabled color from the current [Theme] and will not respond to presses or show the popup menu and [onSelected], [onCanceled] and [itemBuilder] will not be called.

This can be useful in situations where the app needs to show the button, but doesn't currently have anything to show in the menu.

### shape

```dart
ShapeBorder? shape
```

If provided, the shape used for the menu.

If this property is null, then [PopupMenuThemeData.shape] is used. If [PopupMenuThemeData.shape] is also null, then the default shape for [MaterialType.card] is used. This default shape is a rectangle with rounded edges of BorderRadius.circular(2.0).

### color

```dart
Color? color
```

If provided, the background color used for the menu.

If this property is null, then [PopupMenuThemeData.color] is used. If [PopupMenuThemeData.color] is also null, then [ThemeData.cardColor] is used in Material 2. In Material3, defaults to [ColorScheme.surfaceContainer].

### iconColor

```dart
Color? iconColor
```

If provided, this color is used for the button icon.

If this property is null, then [PopupMenuThemeData.iconColor] is used. If [PopupMenuThemeData.iconColor] is also null then defaults to [IconThemeData.color].

### enableFeedback

```dart
bool? enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### iconSize

```dart
double? iconSize
```

If provided, the size of the [Icon].

If this property is null, then [IconThemeData.size] is used. If [IconThemeData.size] is also null, then default size is 24.0 pixels.

### constraints

```dart
BoxConstraints? constraints
```

Optional size constraints for the menu.

When unspecified, defaults to:

```dart
const BoxConstraints(
  minWidth: 2.0 * 56.0,
  maxWidth: 5.0 * 56.0,
)
```

The default constraints ensure that the menu width matches maximum width recommended by the Material Design guidelines. Specifying this parameter enables creation of menu wider than the default maximum width.

### position

```dart
PopupMenuPosition? position
```

Whether the popup menu is positioned over or under the popup menu button.

[offset] is used to change the position of the popup menu relative to the position set by this parameter.

If this property is `null`, then [PopupMenuThemeData.position] is used. If [PopupMenuThemeData.position] is also `null`, then the position defaults to [PopupMenuPosition.over] which makes the popup menu appear directly over the button that was used to create it.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

The [clipBehavior] argument is used the clip shape of the menu.

Defaults to [Clip.none].

### useRootNavigator

```dart
bool useRootNavigator
```

Used to determine whether to push the menu to the [Navigator] furthest from or nearest to the given `context`.

Defaults to false.

### popUpAnimationStyle

```dart
AnimationStyle? popUpAnimationStyle
```

Used to override the default animation curves and durations of the popup menu's open and close transitions.

If [AnimationStyle.curve] is provided, it will be used to override the default popup animation curve. Otherwise, defaults to [Curves.linear].

If [AnimationStyle.reverseCurve] is provided, it will be used to override the default popup animation reverse curve. Otherwise, defaults to `Interval(0.0, 2.0 / 3.0)`.

If [AnimationStyle.duration] is provided, it will be used to override the default popup animation duration. Otherwise, defaults to 300ms.

To disable the theme animation, use [AnimationStyle.noAnimation].

If this is null, then the default animation will be used.

### routeSettings

```dart
RouteSettings? routeSettings
```

Optional route settings for the menu.

See [RouteSettings] for details.

### style

```dart
ButtonStyle? style
```

Customizes this icon button's appearance.

The [style] is only used for Material 3 [IconButton]s. If [ThemeData.useMaterial3] is set to true, [style] is preferred for icon button customization, and any parameters defined in [style] will override the same parameters in [IconButton].

Null by default.

### requestFocus

```dart
bool? requestFocus
```

Whether to request focus when the menu appears.

If null, [Navigator.requestFocus] will be used instead.

### createState()

```dart
PopupMenuButtonState<T> createState()
```

# PopupMenuButtonState

```dart
class PopupMenuButtonState<T> extends State<PopupMenuButton<T>> {}
```

The [State] for a [PopupMenuButton].

See [showButtonMenu] for a way to programmatically open the popup menu of your button state.

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### showButtonMenu()

```dart
void showButtonMenu()
```

A method to show a popup menu with the items supplied to [PopupMenuButton.itemBuilder] at the position of your [PopupMenuButton].

By default, it is called when the user taps the button and [PopupMenuButton.enabled] is set to `true`. Moreover, you can open the button by calling the method manually.

You would access your [PopupMenuButtonState] using a [GlobalKey] and show the menu of the button with `globalKey.currentState.showButtonMenu`.

### build()

```dart
Widget build(BuildContext context)
```
