@docImport 'package:flutter/cupertino.dart';

@docImport 'app.dart'; @docImport 'checkbox_theme.dart'; @docImport 'dropdown_menu.dart'; @docImport 'radio_theme.dart';

# MenuAnchorChildBuilder

```dart
typedef MenuAnchorChildBuilder = Widget Function(BuildContext context, MenuController controller, Widget? child)
```

The type of builder function used by [MenuAnchor.builder] to build the widget that the [MenuAnchor] surrounds.

The `context` is the context that the widget is being built in.

The `controller` is the [MenuController] that can be used to open and close the menu with.

The `child` is an optional child supplied as the [MenuAnchor.child] attribute. The child is intended to be incorporated in the result of the function.

# MenuAnchor

```dart
class MenuAnchor extends StatefulWidget {}
```

A widget used to mark the "anchor" for a set of submenus, defining the rectangle used to position the menu, which can be done either with an explicit location, or with an alignment.

When creating a menu with [MenuBar] or a [SubmenuButton], a [MenuAnchor] is not needed, since they provide their own internally.

The [MenuAnchor] is meant to be a slightly lower level interface than [MenuBar], used in situations where a [MenuBar] isn't appropriate, or to construct widgets or screen regions that have submenus.

To programmatically control a [MenuAnchor], like opening or closing it, or checking its state, you can get its associated [MenuController]. Use `MenuController.maybeOf(BuildContext context)` to retrieve the controller for the closest [MenuAnchor] ancestor of a given [BuildContext]. More detailed usage of [MenuController] is available in its class documentation.

{@tool dartpad} This example shows how to use a [MenuAnchor] to wrap a button and open a cascading menu from the button. This example also shows how to use [onAnimationStatusChanged] to track animation status and toggle the menu.

** See code in examples/api/lib/material/menu_anchor/menu_anchor.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to use a [MenuAnchor] to create a cascading context menu in a region of the view, positioned where the user clicks the mouse with Ctrl pressed. The [anchorTapClosesMenu] attribute is set to true so that clicks on the [MenuAnchor] area will cause the menus to be closed.

** See code in examples/api/lib/material/menu_anchor/menu_anchor.1.dart ** {@end-tool}

{@tool dartpad} This example demonstrates a simplified cascading menu using the [MenuAnchor] widget.

** See code in examples/api/lib/material/menu_anchor/menu_anchor.3.dart ** {@end-tool}

The [MenuStyle.visualDensity] setting only affects horizontal padding, and it will never make it negative. Vertical padding is not affected at all.

### MenuAnchor()

```dart
MenuAnchor({dynamic key, MenuController? controller, FocusNode? childFocusNode, MenuStyle? style, Offset? alignmentOffset = Offset.zero, EdgeInsetsGeometry? reservedPadding, LayerLink? layerLink, Clip clipBehavior = Clip.hardEdge, bool anchorTapClosesMenu = false, bool consumeOutsideTap = false, VoidCallback? onOpen, VoidCallback? onClose, bool crossAxisUnconstrained = true, bool useRootOverlay = false, bool animated = false, ValueChanged<AnimationStatus>? onAnimationStatusChanged, required List<Widget> menuChildren, MenuAnchorChildBuilder? builder, Widget? child})
```

Creates a const [MenuAnchor].

The [menuChildren] argument is required.

### controller

```dart
MenuController? controller
```

An optional controller that allows opening and closing of the menu from other widgets.

### childFocusNode

```dart
FocusNode? childFocusNode
```

The [childFocusNode] attribute is the optional [FocusNode] also associated to the [child] or [builder] widget that opens the menu.

The focus node should be attached to the widget that should receive focus if keyboard focus traversal moves the focus off of the submenu with the arrow keys.

If not supplied, then keyboard traversal from the menu back to the controlling button when the menu is open is disabled.

### style

```dart
MenuStyle? style
```

The [MenuStyle] that defines the visual attributes of the menu bar.

Colors and sizing of the menus is controllable via the [MenuStyle].

Defaults to the ambient [MenuThemeData.style].

### alignmentOffset

```dart
Offset? alignmentOffset
```

{@template flutter.material.MenuAnchor.alignmentOffset} The offset of the menu relative to the alignment origin determined by [MenuStyle.alignment] on the [style] attribute and the ambient [Directionality].

Use this for adjustments of the menu placement.

Increasing [Offset.dy] values of [alignmentOffset] move the menu position down.

If the [MenuStyle.alignment] from [style] is not an [AlignmentDirectional] (e.g. [Alignment]), then increasing [Offset.dx] values of [alignmentOffset] move the menu position to the right.

If the [MenuStyle.alignment] from [style] is an [AlignmentDirectional], then in a [TextDirection.ltr] [Directionality], increasing [Offset.dx] values of [alignmentOffset] move the menu position to the right. In a [TextDirection.rtl] directionality, increasing [Offset.dx] values of [alignmentOffset] move the menu position to the left.

Defaults to [Offset.zero]. {@endtemplate}

### layerLink

```dart
LayerLink? layerLink
```

An optional [LayerLink] to attach the menu to the widget that this [MenuAnchor] surrounds.

When provided, the menu will follow the widget that this [MenuAnchor] surrounds if it moves because of view insets changes.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### anchorTapClosesMenu

```dart
bool anchorTapClosesMenu
```

Whether the menus will be closed if the anchor area is tapped.

For menus opened by buttons that toggle the menu, if the button is tapped when the menu is open, the button should close the menu. But if [anchorTapClosesMenu] is true, then the menu will close, and (surprisingly) immediately re-open. This is because tapping on the button closes the menu before the `onPressed` or `onTap` handler is called because of it being considered to be "outside" the menu system, and then the button (seeing that the menu is closed) immediately reopens the menu. The result is that the user thinks that tapping on the button does nothing. So, for button-initiated menus, this value is typically false so that the menu anchor area is considered "inside" of the menu system and doesn't cause it to close unless [MenuController.close] is called.

For menus that are positioned using [MenuController.open]'s `position` parameter, it is often desirable that clicking on the anchor always closes the menu since the anchor area isn't usually considered part of the menu system by the user. In this case [anchorTapClosesMenu] should be true.

Defaults to false.

### consumeOutsideTap

```dart
bool consumeOutsideTap
```

Whether or not a tap event that closes the menu will be permitted to continue on to the gesture arena.

If false, then tapping outside of a menu when the menu is open will both close the menu, and allow the tap to participate in the gesture arena. If true, then it will only close the menu, and the tap event will be consumed.

Defaults to false.

### onOpen

```dart
VoidCallback? onOpen
```

A callback that is invoked when the menu begins opening.

Defaults to null.

### onClose

```dart
VoidCallback? onClose
```

A callback that is invoked when the menu finishes closing.

Defaults to null.

### crossAxisUnconstrained

```dart
bool crossAxisUnconstrained
```

Determine if the menu panel can be wrapped by a [UnconstrainedBox] which allows the panel to render at its "natural" size.

Defaults to true as it allows developers to render the menu panel at the size it should be. When it is set to false, it can be useful when the menu should be constrained in both main axis and cross axis, such as a [DropdownMenu].

### useRootOverlay

```dart
bool useRootOverlay
```

{@macro flutter.widgets.RawMenuAnchor.useRootOverlay}

Defaults to false.

### animated

```dart
bool animated
```

Whether this widget should open or close a submenu with an animation.

Defaults to false.

### onAnimationStatusChanged

```dart
ValueChanged<AnimationStatus>? onAnimationStatusChanged
```

An optional callback that is invoked when the [AnimationStatus] of the menu changes during open and close animations.

If [animated] is false, this callback will only be invoked with [AnimationStatus.completed] when the menu is opened, and [AnimationStatus.dismissed] when the menu is closed.

This callback provides a way to determine when the menu is opening or closing. This is necessary because the [MenuController.isOpen] property remains true throughout the opening, opened, and closing phases, and therefore cannot be used on its own to determine the current animation direction.

{@tool snippet} This example shows how to use the [onAnimationStatusChanged] callback to create a [MenuAnchor] that will toggle between opening and closing.

```dart
MenuAnchor(
  animated: true,
  onAnimationStatusChanged: (AnimationStatus status) {
    // Typically, animationStatus would be stored in a State object.
    animationStatus = status;
  },
  menuChildren: <Widget>[MenuItemButton(onPressed: () {}, child: const Text('Menu Item'))],
  builder: (BuildContext context, MenuController controller, Widget? child) {
    return IconButton(
      onPressed: () {
        if (animationStatus.isForwardOrCompleted) {
          controller.close();
        } else {
          controller.open();
        }
      },
      icon: const Icon(Icons.more_vert),
    );
  },
);
```

{@end-tool}

Defaults to null.

### menuChildren

```dart
List<Widget> menuChildren
```

A list of children containing the menu items that are the contents of the menu surrounded by this [MenuAnchor].

{@macro flutter.material.MenuBar.shortcuts_note}

### builder

```dart
MenuAnchorChildBuilder? builder
```

The widget that this [MenuAnchor] surrounds.

Typically this is a button used to open the menu by calling [MenuController.open] on the `controller` passed to the builder.

If not supplied, then the [MenuAnchor] will be the size that its parent allocates for it.

If provided, the builder will be called each time the menu is opened or closed.

### child

```dart
Widget? child
```

The optional child to be passed to the [builder].

Supply this child if there is a portion of the widget tree built in [builder] that doesn't depend on the `controller` or `context` supplied to the [builder]. It will be more efficient, since Flutter doesn't then need to rebuild this child when those change.

### reservedPadding

```dart
EdgeInsetsGeometry? reservedPadding
```

The padding between the edge of the safe area and the menu panel.

Defaults to EdgeInsets.all(8).

### createState()

```dart
State<MenuAnchor> createState()
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MenuBar

```dart
class MenuBar extends StatelessWidget {}
```

A menu bar that manages cascading child menus.

This is a Material Design menu bar that typically resides above the main body of an application (but can go anywhere) that defines a menu system for invoking callbacks in response to user selection of a menu item.

The menus can be opened with a click or tap. Once a menu is opened, it can be navigated by using the arrow and tab keys or via mouse hover. Selecting a menu item can be done by pressing enter, or by clicking or tapping on the menu item. Clicking or tapping on any part of the user interface that isn't part of the menu system controlled by the same controller will cause all of the menus controlled by that controller to close, as will pressing the escape key.

When a menu item with a submenu is clicked on, it toggles the visibility of the submenu. When the menu item is hovered over, the submenu will open, and hovering over other items will close the previous menu and open the newly hovered one. When those open/close transitions occur, [SubmenuButton.onOpen], and [SubmenuButton.onClose] are called on the corresponding [SubmenuButton] child of the menu bar.

{@template flutter.material.MenuBar.shortcuts_note} Menus using [MenuItemButton] can have a [SingleActivator] or [CharacterActivator] assigned to them as their [MenuItemButton.shortcut], which will display an appropriate shortcut hint. Even though the shortcut labels are displayed in the menu, shortcuts are not automatically handled. They must be available in whatever context they are appropriate, and handled via another mechanism.

If shortcuts should be generally enabled, but are not easily defined in a context surrounding the menu bar, consider registering them with a [ShortcutRegistry] (one is already included in the [WidgetsApp], and thus also [MaterialApp] and [CupertinoApp]), as shown in the example below. To be sure that selecting a menu item and triggering the shortcut do the same thing, it is recommended that they call the same callback.

{@tool dartpad} This example shows a [MenuBar] that contains a single top level menu, containing three items: "About", a checkbox menu item for showing a message, and "Quit". The items are identified with an enum value, and the shortcuts are registered globally with the [ShortcutRegistry].

** See code in examples/api/lib/material/menu_anchor/menu_bar.0.dart ** {@end-tool} {@endtemplate}

{@macro flutter.material.MenuAcceleratorLabel.accelerator_sample}

See also:

- [MenuAnchor], a widget that creates a region with a submenu and shows it when requested.
- [SubmenuButton], a menu item which manages a submenu.
- [MenuItemButton], a leaf menu item which displays the label, an optional shortcut label, and optional leading and trailing icons.
- [PlatformMenuBar], which creates a menu bar that is rendered by the host platform instead of by Flutter (on macOS, for example).
- [ShortcutRegistry], a registry of shortcuts that apply for the entire application.
- [VoidCallbackIntent], to define intents that will call a [VoidCallback] and work with the [Actions] and [Shortcuts] system.
- [CallbackShortcuts], to define shortcuts that call a callback without involving [Actions].

### MenuBar()

```dart
MenuBar({dynamic key, MenuStyle? style, Clip clipBehavior = Clip.none, MenuController? controller, required List<Widget> children})
```

Creates a const [MenuBar].

The [children] argument is required.

### style

```dart
MenuStyle? style
```

The [MenuStyle] that defines the visual attributes of the menu bar.

Colors and sizing of the menus is controllable via the [MenuStyle].

Defaults to the ambient [MenuThemeData.style].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### controller

```dart
MenuController? controller
```

The [MenuController] to use for this menu bar.

### children

```dart
List<Widget> children
```

The list of menu items that are the top level children of the [MenuBar].

A Widget in Flutter is immutable, so directly modifying the [children] with [List] APIs such as `someMenuBarWidget.menus.add(...)` will result in incorrect behaviors. Whenever the menus list is modified, a new list object must be provided.

{@macro flutter.material.MenuBar.shortcuts_note}

### build()

```dart
Widget build(BuildContext context)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MenuItemButton

```dart
class MenuItemButton extends StatefulWidget {}
```

A button for use in a [MenuBar], in a menu created with [MenuAnchor], or on its own, that can be activated by click or keyboard navigation.

This widget represents a leaf entry in a menu hierarchy that is typically part of a [MenuBar], but may be used independently, or as part of a menu created with a [MenuAnchor].

{@macro flutter.material.MenuBar.shortcuts_note}

See also:

- [MenuBar], a class that creates a top level menu bar in a Material Design style.
- [MenuAnchor], a widget that creates a region with a submenu and shows it when requested.
- [SubmenuButton], a menu item similar to this one which manages a submenu.
- [PlatformMenuBar], which creates a menu bar that is rendered by the host platform instead of by Flutter (on macOS, for example).
- [ShortcutRegistry], a registry of shortcuts that apply for the entire application.
- [VoidCallbackIntent], to define intents that will call a [VoidCallback] and work with the [Actions] and [Shortcuts] system.
- [CallbackShortcuts] to define shortcuts that call a callback without involving [Actions].

### MenuItemButton()

```dart
MenuItemButton({dynamic key, VoidCallback? onPressed, ValueChanged<bool>? onHover, bool requestFocusOnHover = true, ValueChanged<bool>? onFocusChange, FocusNode? focusNode, bool autofocus = false, MenuSerializableShortcut? shortcut, String? semanticsLabel, ButtonStyle? style, MaterialStatesController? statesController, Clip clipBehavior = Clip.none, Widget? leadingIcon, Widget? trailingIcon, bool closeOnActivate = true, Axis overflowAxis = Axis.horizontal, Widget? child})
```

Creates a const [MenuItemButton].

The [child] attribute is required.

### onPressed

```dart
VoidCallback? onPressed
```

Called when the button is tapped or otherwise activated.

If this callback is null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the button response area.

The value passed to the callback is true if a pointer has entered button area and false if a pointer has exited.

### requestFocusOnHover

```dart
bool requestFocusOnHover
```

Determine if hovering can request focus.

Defaults to true.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### shortcut

```dart
MenuSerializableShortcut? shortcut
```

The optional shortcut that selects this [MenuItemButton].

{@macro flutter.material.MenuBar.shortcuts_note}

### semanticsLabel

```dart
String? semanticsLabel
```

An optional Semantics label, applied to the entire [MenuItemButton].

A screen reader will default to reading the derived text on the [MenuItemButton] itself, which is not guaranteed to be readable. (For some shortcuts, such as comma, semicolon, and other punctuation, screen readers read silence).

Setting this label overwrites the semantics properties of the entire Widget, including its children. Consider wrapping this widget in [Semantics] if you want to customize other properties besides just the label.

Null by default.

### style

```dart
ButtonStyle? style
```

Customizes this button's appearance.

Non-null properties of this style override the corresponding properties in [themeStyleOf] and [defaultStyleOf]. [WidgetStateProperty]s that resolve to non-null values will similarly override the corresponding [WidgetStateProperty]s in [themeStyleOf] and [defaultStyleOf].

Null by default.

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### leadingIcon

```dart
Widget? leadingIcon
```

An optional icon to display before the [child] label.

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon to display after the [child] label.

### closeOnActivate

```dart
bool closeOnActivate
```

{@template flutter.material.menu_anchor.closeOnActivate} Determines if the menu will be closed when a [MenuItemButton] is pressed.

Defaults to true. {@endtemplate}

### overflowAxis

```dart
Axis overflowAxis
```

The direction in which the menu item expands.

If the menu item button is a descendent of [MenuAnchor] or [MenuBar], then this property is ignored.

If [overflowAxis] is [Axis.vertical], the menu will be expanded vertically. If [overflowAxis] is [Axis.horizontal], then the menu will be expanded horizontally.

Defaults to [Axis.horizontal].

### child

```dart
Widget? child
```

The widget displayed in the center of this button.

Typically this is the button's label, using a [Text] widget.

{@macro flutter.widgets.ProxyWidget.child}

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

To enable a button, set its [onPressed] property to a non-null value.

### createState()

```dart
State<MenuItemButton> createState()
```

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Defines the button's default appearance.

{@macro flutter.material.text_button.default_style_of}

{@macro flutter.material.text_button.material3_defaults}

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the [MenuButtonThemeData.style] of the closest [MenuButtonTheme] ancestor.

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, Color? disabledIconColor, TextStyle? textStyle, Color? overlayColor, double? elevation, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, BorderSide? side, OutlinedBorder? shape, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory})
```

A static convenience method that constructs a [MenuItemButton]'s [ButtonStyle] given simple values.

The [foregroundColor] color is used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor] value. Specify a value for [foregroundColor] to specify the color of the button's icons. Use [backgroundColor] for the button's background fill color. Use [disabledForegroundColor] and [disabledBackgroundColor] to specify the button's disabled icon and fill color.

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null, by default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default foreground color for a [MenuItemButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
MenuItemButton(
  leadingIcon: const Icon(Icons.pets),
  style: MenuItemButton.styleFrom(foregroundColor: Colors.green),
  onPressed: () {
    // ...
  },
  child: const Text('Button Label'),
),
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# CheckboxMenuButton

```dart
class CheckboxMenuButton extends StatelessWidget {}
```

A menu item that combines a [Checkbox] widget with a [MenuItemButton].

To style the checkbox separately from the button, add a [CheckboxTheme] ancestor.

{@tool dartpad} This example shows a menu with a checkbox that shows a message in the body of the app if checked.

** See code in examples/api/lib/material/menu_anchor/checkbox_menu_button.0.dart ** {@end-tool}

See also:

- [MenuBar], a widget that creates a menu bar of cascading menu items.
- [MenuAnchor], a widget that defines a region which can host a cascading menu.

### CheckboxMenuButton()

```dart
CheckboxMenuButton({dynamic key, required bool? value, bool tristate = false, bool isError = false, required ValueChanged<bool?>? onChanged, ValueChanged<bool>? onHover, ValueChanged<bool>? onFocusChange, FocusNode? focusNode, MenuSerializableShortcut? shortcut, ButtonStyle? style, MaterialStatesController? statesController, Clip clipBehavior = Clip.none, Widget? trailingIcon, bool closeOnActivate = true, required Widget? child})
```

Creates a const [CheckboxMenuButton].

The [child], [value], and [onChanged] attributes are required.

### value

```dart
bool? value
```

Whether this checkbox is checked.

When [tristate] is true, a value of null corresponds to the mixed state. When [tristate] is false, this value must not be null.

### tristate

```dart
bool tristate
```

If true, then the checkbox's [value] can be true, false, or null.

[CheckboxMenuButton] displays a dash when its value is null.

When a tri-state checkbox ([tristate] is true) is tapped, its [onChanged] callback will be applied to true if the current value is false, to null if value is true, and to false if value is null (i.e. it cycles through false => true => null => false when tapped).

If tristate is false (the default), [value] must not be null.

### isError

```dart
bool isError
```

True if this checkbox wants to show an error state.

The checkbox will have different default container color and check color when this is true. This is only used when [ThemeData.useMaterial3] is set to true.

Defaults to false.

### onChanged

```dart
ValueChanged<bool?>? onChanged
```

Called when the value of the checkbox should change.

The checkbox passes the new value to the callback but does not actually change state until the parent widget rebuilds the checkbox with the new value.

If this callback is null, the menu item will be displayed as disabled and will not respond to input gestures.

When the checkbox is tapped, if [tristate] is false (the default) then the [onChanged] callback will be applied to `!value`. If [tristate] is true this callback cycle from false to true to null and then back to false again.

The callback provided to [onChanged] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt; for example:

```dart
CheckboxMenuButton(
  value: _throwShotAway,
  child: const Text('THROW'),
  onChanged: (bool? newValue) {
    setState(() {
      _throwShotAway = newValue!;
    });
  },
)
```

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the button response area.

The value passed to the callback is true if a pointer has entered button area and false if a pointer has exited.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### shortcut

```dart
MenuSerializableShortcut? shortcut
```

The optional shortcut that selects this [MenuItemButton].

{@macro flutter.material.MenuBar.shortcuts_note}

### style

```dart
ButtonStyle? style
```

Customizes this button's appearance.

Non-null properties of this style override the corresponding properties in [MenuItemButton.themeStyleOf] and [MenuItemButton.defaultStyleOf]. [WidgetStateProperty]s that resolve to non-null values will similarly override the corresponding [WidgetStateProperty]s in [MenuItemButton.themeStyleOf] and [MenuItemButton.defaultStyleOf].

Null by default.

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon to display after the [child] label.

### closeOnActivate

```dart
bool closeOnActivate
```

{@macro flutter.material.menu_anchor.closeOnActivate}

### child

```dart
Widget? child
```

The widget displayed in the center of this button.

Typically this is the button's label, using a [Text] widget.

{@macro flutter.widgets.ProxyWidget.child}

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

To enable a button, set its [onChanged] property to a non-null value.

### build()

```dart
Widget build(BuildContext context)
```

# RadioMenuButton

```dart
class RadioMenuButton<T> extends StatelessWidget {}
```

A menu item that combines a [Radio] widget with a [MenuItemButton].

To style the radio button separately from the overall button, add a [RadioTheme] ancestor.

{@tool dartpad} This example shows a menu with three radio buttons with shortcuts that changes the background color of the body when the buttons are selected.

** See code in examples/api/lib/material/menu_anchor/radio_menu_button.0.dart ** {@end-tool}

See also:

- [MenuBar], a widget that creates a menu bar of cascading menu items.
- [MenuAnchor], a widget that defines a region which can host a cascading menu.

### RadioMenuButton()

```dart
RadioMenuButton({dynamic key, required T value, required T? groupValue, required ValueChanged<T?>? onChanged, bool toggleable = false, ValueChanged<bool>? onHover, ValueChanged<bool>? onFocusChange, FocusNode? focusNode, MenuSerializableShortcut? shortcut, ButtonStyle? style, MaterialStatesController? statesController, Clip clipBehavior = Clip.none, Widget? trailingIcon, bool closeOnActivate = true, required Widget? child})
```

Creates a const [RadioMenuButton].

The [child] attribute is required.

### value

```dart
T value
```

The value represented by this radio button.

This radio button is considered selected if its [value] matches the [groupValue].

### groupValue

```dart
T? groupValue
```

The currently selected value for a group of radio buttons.

This radio button is considered selected if its [value] matches the [groupValue].

### toggleable

```dart
bool toggleable
```

Set to true if this radio button is allowed to be returned to an indeterminate state by selecting it again when selected.

To indicate returning to an indeterminate state, [onChanged] will be called with null.

If true, [onChanged] is called with [value] when selected while [groupValue] != [value], and with null when selected again while [groupValue] == [value].

If false, [onChanged] will be called with [value] when it is selected while [groupValue] != [value], and only by selecting another radio button in the group (i.e. changing the value of [groupValue]) can this radio button be unselected.

The default is false.

### onChanged

```dart
ValueChanged<T?>? onChanged
```

Called when the user selects this radio button.

The radio button passes [value] as a parameter to this callback. The radio button does not actually change state until the parent widget rebuilds the radio button with the new [groupValue].

If null, the radio button will be displayed as disabled.

The provided callback will not be invoked if this radio button is already selected.

The callback provided to [onChanged] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt; for example:

```dart
RadioMenuButton<SingingCharacter>(
  value: SingingCharacter.lafayette,
  groupValue: _character,
  onChanged: (SingingCharacter? newValue) {
    setState(() {
      _character = newValue;
    });
  },
  child: const Text('Lafayette'),
)
```

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the button response area.

The value passed to the callback is true if a pointer has entered button area and false if a pointer has exited.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### shortcut

```dart
MenuSerializableShortcut? shortcut
```

The optional shortcut that selects this [MenuItemButton].

{@macro flutter.material.MenuBar.shortcuts_note}

### style

```dart
ButtonStyle? style
```

Customizes this button's appearance.

Non-null properties of this style override the corresponding properties in [MenuItemButton.themeStyleOf] and [MenuItemButton.defaultStyleOf]. [WidgetStateProperty]s that resolve to non-null values will similarly override the corresponding [WidgetStateProperty]s in [MenuItemButton.themeStyleOf] and [MenuItemButton.defaultStyleOf].

Null by default.

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon to display after the [child] label.

### closeOnActivate

```dart
bool closeOnActivate
```

{@macro flutter.material.menu_anchor.closeOnActivate}

### child

```dart
Widget? child
```

The widget displayed in the center of this button.

Typically this is the button's label, using a [Text] widget.

{@macro flutter.widgets.ProxyWidget.child}

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

To enable a button, set its [onChanged] property to a non-null value.

### build()

```dart
Widget build(BuildContext context)
```

# SubmenuButton

```dart
class SubmenuButton extends StatefulWidget {}
```

A menu button that displays a cascading menu.

It can be used as part of a [MenuBar], or as a standalone widget.

This widget represents a menu item that has a submenu. Like the leaf [MenuItemButton], it shows a label with an optional leading or trailing icon, but additionally shows an arrow icon showing that it has a submenu.

By default the submenu will appear to the side of the controlling button. The alignment and offset of the submenu can be controlled by setting [MenuStyle.alignment] on the [style] and the [alignmentOffset] argument, respectively.

When activated (by being clicked, through keyboard navigation, or via hovering with a mouse), it will open a submenu containing the [menuChildren].

If [menuChildren] is empty, then this menu item will appear disabled.

See also:

- [MenuItemButton], a widget that represents a leaf menu item that does not host a submenu.
- [MenuBar], a widget that renders menu items in a row in a Material Design style.
- [MenuAnchor], a widget that creates a region with a submenu and shows it when requested.
- [PlatformMenuBar], a widget that renders similar menu bar items from a [PlatformMenuItem] using platform-native APIs instead of Flutter.

### SubmenuButton()

```dart
SubmenuButton({dynamic key, ValueChanged<bool>? onHover, ValueChanged<bool>? onFocusChange, VoidCallback? onOpen, VoidCallback? onClose, MenuController? controller, ButtonStyle? style, MenuStyle? menuStyle, Offset? alignmentOffset, Clip clipBehavior = Clip.hardEdge, FocusNode? focusNode, MaterialStatesController? statesController, Widget? leadingIcon, Widget? trailingIcon, WidgetStateProperty<Widget?>? submenuIcon, bool useRootOverlay = false, Duration hoverOpenDelay = Duration.zero, bool animated = false, ValueChanged<AnimationStatus>? onAnimationStatusChanged, required List<Widget> menuChildren, required Widget? child})
```

Creates a const [SubmenuButton].

The [child] and [menuChildren] attributes are required.

### onHover

```dart
ValueChanged<bool>? onHover
```

Called when a pointer enters or exits the button response area.

The value passed to the callback is true if a pointer has entered this part of the button and false if a pointer has exited.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's [focusNode] gains focus, and false if it loses focus.

### onOpen

```dart
VoidCallback? onOpen
```

A callback that is invoked when the menu is opened.

### onClose

```dart
VoidCallback? onClose
```

A callback that is invoked when the menu is closed.

### controller

```dart
MenuController? controller
```

An optional [MenuController] for this submenu.

### style

```dart
ButtonStyle? style
```

Customizes this button's appearance.

Non-null properties of this style override the corresponding properties in [themeStyleOf] and [defaultStyleOf]. [WidgetStateProperty]s that resolve to non-null values will similarly override the corresponding [WidgetStateProperty]s in [themeStyleOf] and [defaultStyleOf].

Null by default.

### menuStyle

```dart
MenuStyle? menuStyle
```

The [MenuStyle] of the menu specified by [menuChildren].

Defaults to the value of [MenuThemeData.style] of the ambient [MenuTheme].

### alignmentOffset

```dart
Offset? alignmentOffset
```

The offset of the menu relative to the alignment origin determined by [MenuStyle.alignment] on the [style] attribute.

Use this for fine adjustments of the menu placement.

Defaults to an offset that takes into account the padding of the menu so that the top starting corner of the first menu item is aligned with the top of the [MenuAnchor] region.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### statesController

```dart
MaterialStatesController? statesController
```

{@macro flutter.material.inkwell.statesController}

### leadingIcon

```dart
Widget? leadingIcon
```

An optional icon to display before the [child].

### submenuIcon

```dart
WidgetStateProperty<Widget?>? submenuIcon
```

If provided, the widget replaces the default [SubmenuButton] arrow icon.

Resolves in the following states:

- [WidgetState.disabled].
- [WidgetState.hovered].
- [WidgetState.focused].

If this is null, then the value of [MenuThemeData.submenuIcon] is used. If that is also null, then defaults to a right arrow icon with the size of 24 pixels.

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon to display after the [child].

### useRootOverlay

```dart
bool useRootOverlay
```

{@macro flutter.widgets.RawMenuAnchor.useRootOverlay}

Defaults to false.

### onAnimationStatusChanged

```dart
ValueChanged<AnimationStatus>? onAnimationStatusChanged
```

An optional callback that is invoked when the [AnimationStatus] of the menu changes during open and close animations.

If [animated] is false, this callback will only be invoked with [AnimationStatus.completed] when the menu is opened, and [AnimationStatus.dismissed] when the menu is closed.

Because the [MenuController.isOpen] property is true while the menu is opening, opened, and closing, it cannot be used to determine whether the menu is in the process of closing or opening. As such, this callback provides a way to determine when the menu is opening or closing.

Defaults to null.

### menuChildren

```dart
List<Widget> menuChildren
```

The list of widgets that appear in the menu when it is opened.

These can be any widget, but are typically either [MenuItemButton] or [SubmenuButton] widgets.

If [menuChildren] is empty, then the button for this menu item will be disabled.

### hoverOpenDelay

```dart
Duration hoverOpenDelay
```

The duration to wait before opening the menu when the button is hovered.

Because [MenuBar] children can only be opened by hover if a sibling [SubmenuButton] is already open, providing a [hoverOpenDelay] to direct children of a [MenuBar] will throw an assertion error. This is to avoid the case where the [hoverOpenDelay] for a [SubmenuButton] is longer than the duration of a sibling's closing animation, which leads to that menu never opening.

Defaults to [Duration.zero].

### animated

```dart
bool animated
```

Whether the menu should open and close with an animation.

Defaults to false.

### child

```dart
Widget? child
```

The widget displayed in the middle portion of this button.

Typically this is the button's label, using a [Text] widget.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<SubmenuButton> createState()
```

### defaultStyleOf()

```dart
ButtonStyle defaultStyleOf(BuildContext context)
```

Defines the button's default appearance.

{@macro flutter.material.text_button.default_style_of}

{@macro flutter.material.text_button.material3_defaults}

### themeStyleOf()

```dart
ButtonStyle? themeStyleOf(BuildContext context)
```

Returns the [MenuButtonThemeData.style] of the closest [MenuButtonTheme] ancestor.

### styleFrom()

```dart
ButtonStyle styleFrom({Color? foregroundColor, Color? backgroundColor, Color? disabledForegroundColor, Color? disabledBackgroundColor, Color? shadowColor, Color? surfaceTintColor, Color? iconColor, double? iconSize, Color? disabledIconColor, TextStyle? textStyle, Color? overlayColor, double? elevation, EdgeInsetsGeometry? padding, Size? minimumSize, Size? fixedSize, Size? maximumSize, MouseCursor? enabledMouseCursor, MouseCursor? disabledMouseCursor, BorderSide? side, OutlinedBorder? shape, VisualDensity? visualDensity, MaterialTapTargetSize? tapTargetSize, Duration? animationDuration, bool? enableFeedback, AlignmentGeometry? alignment, InteractiveInkFeatureFactory? splashFactory})
```

A static convenience method that constructs a [SubmenuButton]'s [ButtonStyle] given simple values.

The [foregroundColor] color is used to create a [WidgetStateProperty] [ButtonStyle.foregroundColor] value. Specify a value for [foregroundColor] to specify the color of the button's icons. Use [backgroundColor] for the button's background fill color. Use [disabledForegroundColor] and [disabledBackgroundColor] to specify the button's disabled icon and fill color.

Similarly, the [enabledMouseCursor] and [disabledMouseCursor] parameters are used to construct [ButtonStyle.mouseCursor].

The [iconColor], [disabledIconColor] are used to construct [ButtonStyle.iconColor] and [iconSize] is used to construct [ButtonStyle.iconSize].

All of the other parameters are either used directly or used to create a [WidgetStateProperty] with a single value for all states.

All parameters default to null, by default this method returns a [ButtonStyle] that doesn't override anything.

For example, to override the default foreground color for a [SubmenuButton], as well as its overlay color, with all of the standard opacity adjustments for the pressed, focused, and hovered states, one could write:

```dart
SubmenuButton(
  leadingIcon: const Icon(Icons.pets),
  style: SubmenuButton.styleFrom(foregroundColor: Colors.green),
  menuChildren: const <Widget>[ /* ... */ ],
  child: const Text('Button Label'),
),
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# MenuAcceleratorCallbackBinding

```dart
class MenuAcceleratorCallbackBinding extends InheritedWidget {}
```

An [InheritedWidget] that provides a descendant [MenuAcceleratorLabel] with the function to invoke when the accelerator is pressed.

This is used when creating your own custom menu item for use with [MenuAnchor] or [MenuBar]. Provided menu items such as [MenuItemButton] and [SubmenuButton] already supply this wrapper internally.

### MenuAcceleratorCallbackBinding()

```dart
MenuAcceleratorCallbackBinding({dynamic key, VoidCallback? onInvoke, bool hasSubmenu = false, required dynamic child})
```

Create a const [MenuAcceleratorCallbackBinding].

The [child] parameter is required.

### onInvoke

```dart
VoidCallback? onInvoke
```

The function that pressing the accelerator defined in a descendant [MenuAcceleratorLabel] will invoke.

If set to null, then the accelerator won't be enabled.

### hasSubmenu

```dart
bool hasSubmenu
```

Whether or not the associated label will host its own submenu or not.

This setting determines when accelerators are active, since accelerators for menu items that open submenus shouldn't be active when the submenu is open.

### updateShouldNotify()

```dart
bool updateShouldNotify(MenuAcceleratorCallbackBinding oldWidget)
```

### maybeOf()

```dart
MenuAcceleratorCallbackBinding? maybeOf(BuildContext context)
```

Returns the active [MenuAcceleratorCallbackBinding] in the given context, if any, and creates a dependency relationship that will rebuild the context when [onInvoke] changes.

If no [MenuAcceleratorCallbackBinding] is found, returns null.

See also:

- [of], which is similar, but asserts if no [MenuAcceleratorCallbackBinding] is found.

### of()

```dart
MenuAcceleratorCallbackBinding of(BuildContext context)
```

Returns the active [MenuAcceleratorCallbackBinding] in the given context, and creates a dependency relationship that will rebuild the context when [onInvoke] changes.

If no [MenuAcceleratorCallbackBinding] is found, returns will assert in debug mode and throw an exception in release mode.

See also:

- [maybeOf], which is similar, but returns null if no [MenuAcceleratorCallbackBinding] is found.

# MenuAcceleratorChildBuilder

```dart
typedef MenuAcceleratorChildBuilder = Widget Function(BuildContext context, String label, int index)
```

The type of builder function used for building a [MenuAcceleratorLabel]'s [MenuAcceleratorLabel.builder] function.

{@template flutter.material.menu_anchor.menu_accelerator_child_builder.args} The arguments to the function are as follows:

- The `context` supplies the [BuildContext] to use.
- The `label` is the [MenuAcceleratorLabel.label] attribute for the relevant [MenuAcceleratorLabel] with the accelerator markers stripped out of it.
- The `index` is the index of the accelerator character within the `label.characters` that applies to this accelerator. If it is -1, then the accelerator should not be highlighted. Otherwise, the given character should be highlighted somehow in the rendered label (typically with an underscore). Importantly, `index` is not an index into the [String] `label`, it is an index into the [Characters] iterable returned by `label.characters`, so that it is in terms of user-visible characters (a.k.a. grapheme clusters), not Unicode code points. {@endtemplate}

See also:

- [MenuAcceleratorLabel.defaultLabelBuilder], which is the implementation used as the default value for [MenuAcceleratorLabel.builder].

# MenuAcceleratorLabel

```dart
class MenuAcceleratorLabel extends StatefulWidget {}
```

A widget that draws the label text for a menu item (typically a [MenuItemButton] or [SubmenuButton]) and renders its child with information about the currently active keyboard accelerator.

On platforms other than macOS and iOS, this widget listens for the Alt key to be pressed, and when it is down, will update the label by calling the builder again with the position of the accelerator in the label string. While the Alt key is pressed, it registers a shortcut with the [ShortcutRegistry] mapped to a [VoidCallbackIntent] containing the callback defined by the nearest [MenuAcceleratorCallbackBinding].

Because the accelerators are registered with the [ShortcutRegistry], any other shortcuts in the widget tree between the [primaryFocus] and the [ShortcutRegistry] that define Alt-based shortcuts using the same keys will take precedence over the accelerators.

Because accelerators aren't used on macOS and iOS, the label ignores the Alt key on those platforms, and the [builder] is always given -1 as an accelerator index. Accelerator labels are still stripped of their accelerator markers.

The built-in menu items [MenuItemButton] and [SubmenuButton] already provide the appropriate [MenuAcceleratorCallbackBinding], so unless you are creating your own custom menu item type that takes a [MenuAcceleratorLabel], it is not necessary to provide one.

{@template flutter.material.MenuAcceleratorLabel.accelerator_sample} {@tool dartpad} This example shows a [MenuBar] that handles keyboard accelerators using [MenuAcceleratorLabel]. To use the accelerators, press the Alt key to see which letters are underlined in the menu bar, and then press the appropriate letter. Accelerators are not supported on macOS or iOS since those platforms don't support them natively, so this demo will only show a regular Material menu bar on those platforms.

** See code in examples/api/lib/material/menu_anchor/menu_accelerator_label.0.dart ** {@end-tool} {@endtemplate}

### MenuAcceleratorLabel()

```dart
MenuAcceleratorLabel(String label, {dynamic key, MenuAcceleratorChildBuilder builder = defaultLabelBuilder})
```

Creates a const [MenuAcceleratorLabel].

The [label] parameter is required.

### label

```dart
String label
```

The label string that should be displayed.

The label string provides the label text, as well as the possible characters which could be used as accelerators in the menu system.

{@template flutter.material.menu_anchor.menu_accelerator_label.label} To indicate which letters in the label are to be used as accelerators, add an "&" character before the character in the string. If more than one character has an "&" in front of it, then the characters appearing earlier in the string are preferred. To represent a literal "&", insert "&&" into the string. All other ampersands will be removed from the string before calling [MenuAcceleratorLabel.builder]. Bare ampersands at the end of the string or before whitespace are stripped and ignored. {@endtemplate}

See also:

- [displayLabel], which returns the [label] with all of the ampersands stripped out of it, and double ampersands converted to ampersands.
- [stripAcceleratorMarkers], which returns the supplied string with all of the ampersands stripped out of it, and double ampersands converted to ampersands, and optionally calls a callback with the index of the accelerator character found.

### displayLabel

```dart
String get displayLabel
```

Returns the [label] with any accelerator markers removed.

This getter just calls [stripAcceleratorMarkers] with the [label].

### builder

```dart
MenuAcceleratorChildBuilder builder
```

The optional [MenuAcceleratorChildBuilder] which is used to build the widget that displays the label itself.

The [defaultLabelBuilder] function serves as the default value for [builder], rendering the label as a [RichText] widget with appropriate [TextSpan]s for rendering the label with an underscore under the selected accelerator for the label when accelerators have been activated.

{@macro flutter.material.menu_anchor.menu_accelerator_child_builder.args}

When writing the builder function, it's not necessary to take the current platform into account. On platforms which don't support accelerators (e.g. macOS and iOS), the passed accelerator index will always be -1, and the accelerator markers will already be stripped.

### hasAccelerator

```dart
bool get hasAccelerator
```

Whether [label] contains an accelerator definition.

{@macro flutter.material.menu_anchor.menu_accelerator_label.label}

### defaultLabelBuilder()

```dart
Widget defaultLabelBuilder(BuildContext context, String label, int index)
```

Serves as the default value for [builder], rendering the label as a [RichText] widget with appropriate [TextSpan]s for rendering the label with an underscore under the selected accelerator for the label when the [index] is non-negative, and a [Text] widget when the [index] is negative.

{@macro flutter.material.menu_anchor.menu_accelerator_child_builder.args}

### stripAcceleratorMarkers()

```dart
String stripAcceleratorMarkers(String label, {void Function(int index)? setIndex})
```

Strips out any accelerator markers from the given [label], and unescapes any escaped ampersands.

If [setIndex] is supplied, it will be called before this function returns with the index in the returned string of the accelerator character.

{@macro flutter.material.menu_anchor.menu_accelerator_label.label}

### createState()

```dart
State<MenuAcceleratorLabel> createState()
```

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
