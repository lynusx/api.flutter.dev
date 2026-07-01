@docImport 'package:flutter/material.dart';

# CupertinoMenuEntry

```dart
abstract interface class CupertinoMenuEntry {}
```

Implement [CupertinoMenuEntry] to define how a menu item should be drawn in a menu.

### hasLeading()

```dart
bool hasLeading(BuildContext context)
```

Whether this menu item has a leading widget.

If [hasLeading] returns true, siblings of this menu item that are missing a leading widget will have leading space added to align the leading edges of all menu items.

### isDivider

```dart
bool get isDivider
```

Whether this menu item is a divider.

When true, a divider will not be drawn above or below this menu item. Otherwise, adjacent menu items will be separated by a divider.

# CupertinoMenuAnimationStatusChangedCallback

```dart
typedef CupertinoMenuAnimationStatusChangedCallback = void Function(AnimationStatus status)
```

Signature for the callback called in response to a [CupertinoMenuAnchor] changing its [AnimationStatus].

# CupertinoMenuAnchor

```dart
class CupertinoMenuAnchor extends StatefulWidget {}
```

A widget used to mark the "anchor" for a menu, defining the rectangle used to position the menu, which can be done with an explicit location, or with an alignment.

The [CupertinoMenuAnchor] is typically used to wrap a button that opens a menu when pressed. The menu is displayed as a popup overlay that is positioned relative to the anchor rectangle, and will automatically reposition itself to remain fully visible within the screen bounds.

A [MenuController] must be used to open and close the menu, and can be obtained from the [builder] callback, or provided to [controller] parameter. Calling [MenuController.open] will open the menu, and calling [MenuController.close] will close the menu. The [onOpen] callback is invoked when the menu popup is mounted and the menu status changes _from_ [AnimationStatus.dismissed]. The [onClose] callback is invoked when the menu popup is unmounted and the menu status changes _to_ [AnimationStatus.dismissed]. The [onAnimationStatusChanged] callback is invoked every time the [AnimationStatus] of the menu animation changes.

## Usage

{@tool sample} This example demonstrates a simple [CupertinoMenuAnchor] that wraps a button.

** See code in examples/api/lib/cupertino/menu_anchor/menu_anchor.0.dart ** {@end-tool}

{@tool dartpad} This example demonstrates a [CupertinoMenuAnchor] that wraps a button and shows a menu with three [CupertinoMenuItem]s and one [CupertinoMenuDivider].

** See code in examples/api/lib/cupertino/menu_anchor/menu_anchor.1.dart ** {@end-tool}

See also:

- [CupertinoMenuItem], a Cupertino-themed menu item used in a [CupertinoMenuAnchor].
- [CupertinoMenuDivider], a large divider used to separate [CupertinoMenuItem]s.
- [CupertinoMenuEntry], an interface that can be implemented to customize the appearance of menu items in a [CupertinoMenuAnchor].

### CupertinoMenuAnchor()

```dart
CupertinoMenuAnchor({dynamic key, MenuController? controller, VoidCallback? onOpen, VoidCallback? onClose, CupertinoMenuAnimationStatusChangedCallback? onAnimationStatusChanged, BoxConstraints? constraints, bool constrainCrossAxis = false, bool consumeOutsideTaps = false, bool enableSwipe = true, bool enableLongPressToOpen = false, bool useRootOverlay = false, EdgeInsetsGeometry overlayPadding = const EdgeInsets.all(8), required List<Widget> menuChildren, RawMenuAnchorChildBuilder? builder, Widget? child, FocusNode? childFocusNode})
```

Creates a [CupertinoMenuAnchor].

### controller

```dart
MenuController? controller
```

An optional controller that allows opening and closing of the menu from other widgets.

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

### onAnimationStatusChanged

```dart
CupertinoMenuAnimationStatusChangedCallback? onAnimationStatusChanged
```

An optional callback that is invoked when the [AnimationStatus] of the menu changes.

This callback provides a way to determine when the menu is opening or closing. This is necessary because the [MenuController.isOpen] property remains true throughout the opening, opened, and closing phases, and therefore cannot be used on its own to determine the current animation direction.

Defaults to null.

### constraints

```dart
BoxConstraints? constraints
```

The constraints to apply to the menu scrollable.

### constrainCrossAxis

```dart
bool constrainCrossAxis
```

Whether the menu's cross axis should be constrained by the overlay.

If true, when the menu is wider than the overlay, the menu width will shrink to fit the overlay bounds.

If false, the menu will grow to fit the size of its contents. If the menu is wider than the overlay, it will be clipped to the overlay's bounds.

Defaults to false.

### consumeOutsideTaps

```dart
bool consumeOutsideTaps
```

Whether or not a tap event that closes the menu will be permitted to continue on to the gesture arena.

If false, then tapping outside of a menu when the menu is open will both close the menu, and allow the tap to participate in the gesture arena. If true, then it will only close the menu, and the tap event will be consumed.

Defaults to false.

### enableSwipe

```dart
bool enableSwipe
```

Whether or not swiping is enabled on the menu.

When swiping is enabled, a [MultiDragGestureRecognizer] is added around the widget built by [builder] and menu items. The [MultiDragGestureRecognizer] allows for users to press, move, and activate adjacent menu items in a single gesture. Swiping also scales the menu panel when users drag their pointer away from the menu.

Disabling swiping can be useful if the menu swipe effects interfere with another swipe gesture, such as in the case of dragging a menu anchor around the screen.

Defaults to true.

### enableLongPressToOpen

```dart
bool enableLongPressToOpen
```

Whether or not the menu should open in response to a long-press on the anchor.

When a menu is opened via long-press, the menu can be swiped in the same gesture to select and activate menu items.

Because long-press-to-open relies on the swipe gesture, [enableSwipe] must be true if [enableLongPressToOpen] is true.

If the widget built by [builder] is disabled, [enableLongPressToOpen] should be set to false to prevent the menu from opening on long-press.

Defaults to false, which disables the behavior.

### useRootOverlay

```dart
bool useRootOverlay
```

{@macro flutter.widgets.RawMenuAnchor.useRootOverlay}

### overlayPadding

```dart
EdgeInsetsGeometry overlayPadding
```

The padding inside the overlay between its boundary and the menu content.

If the menu width is larger than the available space in the overlay minus the [overlayPadding] and [constrainCrossAxis] is false, the menu will be positioned against the starting edge of the overlay (left when the ambient [Directionality] is [TextDirection.ltr], and right when the ambient [Directionality] is [TextDirection.rtl]). If [constrainCrossAxis] is true, the menu width will shrink to fit within the overlay bounds minus the [overlayPadding].

Defaults to `EdgeInsets.all(8)`.

### menuChildren

```dart
List<Widget> menuChildren
```

A list of menu items to display in the menu.

### builder

```dart
RawMenuAnchorChildBuilder? builder
```

The widget that this [CupertinoMenuAnchor] surrounds.

Typically, this is a button that calls [MenuController.open] when pressed.

The [builder] will rebuild when the menu's [AnimationStatus] changes.

If null, the [CupertinoMenuAnchor] will be the size that its parent allocates for it.

### child

```dart
Widget? child
```

An optional child to be passed to the [builder].

Supply this child if there is a portion of the widget tree built in [builder] that doesn't depend on the `controller` or `context` supplied to the [builder]. It will be more efficient, since Flutter doesn't then need to rebuild this child when those change.

### childFocusNode

```dart
FocusNode? childFocusNode
```

The [childFocusNode] attribute is the optional [FocusNode] also associated the [child] or [builder] widget that opens the menu.

The focus node should be attached to the widget that should receive focus if keyboard focus traversal moves the focus off of the submenu with the arrow keys.

If not supplied, then focus will not traverse from the menu to the controlling button after the menu opens.

### maybeHasLeadingOf()

```dart
bool? maybeHasLeadingOf(BuildContext context)
```

Returns whether any ancestor [CupertinoMenuAnchor] has menu items with leading widgets.

This can be used by menu items to determine whether they need to allocate space for a leading widget to align with sibling menu items.

### createState()

```dart
State<CupertinoMenuAnchor> createState()
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# CupertinoMenuDivider

```dart
class CupertinoMenuDivider extends StatelessWidget implements CupertinoMenuEntry {}
```

A large horizontal divider that is used to separate [CupertinoMenuItem]s in a [CupertinoMenuAnchor].

The divider has a height of 8 logical pixels. The [color] parameter can be provided to customize the color of the divider.

See also:

- [CupertinoMenuItem], a Cupertino-style menu item.
- [CupertinoMenuAnchor], a widget that creates a Cupertino-style popup menu.
- [CupertinoMenuEntry], an interface that can be used to control whether dividers are shown before or after a menu item.

### CupertinoMenuDivider()

```dart
CupertinoMenuDivider({dynamic key, Color color = kDefaultColor})
```

Creates a large horizontal divider for a [CupertinoMenuAnchor].

### color

```dart
Color color
```

The color of the divider.

Defaults to [CupertinoMenuDivider.kDefaultColor].

### isDivider

```dart
bool get isDivider
```

### hasLeading()

```dart
bool hasLeading(BuildContext context)
```

### kDefaultColor

```dart
CupertinoDynamicColor kDefaultColor
```

Default color for a [CupertinoMenuDivider].

### build()

```dart
Widget build(BuildContext context)
```

# CupertinoMenuItem

```dart
class CupertinoMenuItem extends StatelessWidget implements CupertinoMenuEntry {}
```

A menu item for use in a [CupertinoMenuAnchor].

## Layout

The menu item is unconstrained by default and will grow to fit the size of its container. To constrain the size of a [CupertinoMenuItem], the [constraints] parameter can be set. When set, the [constraints] apply to the total area occupied by the content and its [padding]. This means that [padding] will only affect the size of this menu item if this item's minimum constraints are less than the sum of its [padding] and the size of its contents.

The [leading] and [trailing] widgets display before and after the [child] widget, respectively. The [leadingWidth] and [trailingWidth] parameters control the horizontal space that these widgets occupy. The [leadingMidpointAlignment] and [trailingMidpointAlignment] parameters control the alignment of the leading and trailing widgets within their respective spaces.

## Input

In order to respond to user input, an [onPressed] callback must be provided. If absent, user input callbacks ([onFocusChange], [onHover], and [onPressed]) will be ignored. The [behavior] parameter can be used to control whether hit tests can travel behind the menu item, and the [mouseCursor] parameter can be used to change the cursor that appears when the user hovers over the menu.

The [requestCloseOnActivate] parameter can be set to false to prevent the menu from closing when the item is activated. By default, the menu will close when an item is pressed.

The [requestFocusOnHover] parameter, when true, focuses the menu item when the item is hovered.

## Visuals

The [decoration] parameter can be used to change the background color of the menu item when hovered, focused, pressed, or swiped. If these parameters are not set, the menu item will use [CupertinoMenuItem.kDefaultDecoration].

The [isDestructiveAction] parameter should be set to true if the menu item will perform a destructive action, and will color the text of the menu item [CupertinoColors.systemRed].

{@tool sample} This example demonstrates a simple [CupertinoMenuAnchor] that wraps a button.

** See code in examples/api/lib/cupertino/menu_anchor/menu_anchor.0.dart ** {@end-tool}

{@tool dartpad} This example demonstrates a [CupertinoMenuAnchor] that wraps a button and shows a menu with three [CupertinoMenuItem]s and one [CupertinoMenuDivider].

** See code in examples/api/lib/cupertino/menu_anchor/menu_anchor.1.dart ** {@end-tool}

See also:

- [CupertinoMenuAnchor], a Cupertino-style widget that shows a menu of actions in a popup
- [RawMenuAnchor], a lower-level widget that creates a region with a submenu that is the basis for [CupertinoMenuAnchor].
- [PlatformMenuBar], which creates a menu bar that is rendered by the host platform instead of by Flutter (on macOS, for example).

### CupertinoMenuItem()

```dart
CupertinoMenuItem({dynamic key, required Widget child, Widget? subtitle, Widget? leading, double? leadingWidth, AlignmentGeometry? leadingMidpointAlignment, Widget? trailing, double? trailingWidth, AlignmentGeometry? trailingMidpointAlignment, EdgeInsetsGeometry? padding, BoxConstraints? constraints, bool autofocus = false, FocusNode? focusNode, ValueChanged<bool>? onFocusChange, ValueChanged<bool>? onHover, VoidCallback? onPressed, WidgetStateProperty<BoxDecoration>? decoration, WidgetStateProperty<MouseCursor>? mouseCursor, HitTestBehavior behavior = HitTestBehavior.opaque, bool requestCloseOnActivate = true, bool requestFocusOnHover = true, bool isDestructiveAction = false})
```

Creates a [CupertinoMenuItem]

The [child] parameter is required and must not be null.

### child

```dart
Widget child
```

The widget displayed in the center of this button.

Typically this is the button's label, using a [Text] widget.

{@macro flutter.widgets.ProxyWidget.child}

### padding

```dart
EdgeInsetsGeometry? padding
```

The padding applied to this menu item.

### leading

```dart
Widget? leading
```

The widget shown before the label. Typically an [Icon].

### trailing

```dart
Widget? trailing
```

The widget shown after the label. Typically an [Icon].

### subtitle

```dart
Widget? subtitle
```

A widget displayed underneath the [child]. Typically a [Text] widget.

### onPressed

```dart
VoidCallback? onPressed
```

Called when this menu is tapped or otherwise activated.

If a callback is not provided, then the button will be disabled.

### onHover

```dart
ValueChanged<bool>? onHover
```

Triggered when a pointer moves into a position within this widget without buttons pressed.

Usually this is only fired for pointers which report their location when not down (e.g. mouse pointers). Certain devices also fire this event on single taps in accessibility mode.

This callback is not triggered by the movement of the widget.

The time that this callback is triggered is during the callback of a pointer event, which is always between frames.

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

{@macro flutter.material.inkwell.onFocusChange}

### requestFocusOnHover

```dart
bool requestFocusOnHover
```

Whether hovering should request focus for this widget.

Defaults to true.

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### decoration

```dart
WidgetStateProperty<BoxDecoration>? decoration
```

The decoration to paint behind the menu item.

If null, defaults to [CupertinoMenuItem.kDefaultDecoration].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor>? mouseCursor
```

The mouse cursor to display on hover.

### behavior

```dart
HitTestBehavior behavior
```

How the menu item should respond to hit tests.

### requestCloseOnActivate

```dart
bool requestCloseOnActivate
```

Determines if the menu will be closed when a [CupertinoMenuItem] is pressed.

Defaults to true.

### isDestructiveAction

```dart
bool isDestructiveAction
```

Whether pressing this item will perform a destructive action

Defaults to false. If true, the default color of this item's label and icon will be [CupertinoColors.systemRed].

### leadingWidth

```dart
double? leadingWidth
```

The horizontal space in which the [leading] widget can be placed.

### trailingWidth

```dart
double? trailingWidth
```

The horizontal space in which the [trailing] widget can be placed.

### leadingMidpointAlignment

```dart
AlignmentGeometry? leadingMidpointAlignment
```

The alignment of the center point of the leading widget within the [leadingWidth] of the menu item.

### trailingMidpointAlignment

```dart
AlignmentGeometry? trailingMidpointAlignment
```

The alignment of the center point of the trailing widget within the [trailingWidth] of the menu item.

### constraints

```dart
BoxConstraints? constraints
```

The [BoxConstraints] to apply to the menu item.

Because [padding] is applied to the menu item prior to [constraints], the [padding] will only affect the size of the menu item if the vertical [padding] plus the height of the menu item's children exceeds the [BoxConstraints.minHeight].

### hasLeading()

```dart
bool hasLeading(BuildContext context)
```

### isDivider

```dart
bool get isDivider
```

### kDefaultDecoration

```dart
WidgetStateProperty<BoxDecoration> kDefaultDecoration
```

The decoration of a [CupertinoMenuItem] when pressed.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
