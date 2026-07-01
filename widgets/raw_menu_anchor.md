@docImport 'package:flutter/material.dart';

# RawMenuOverlayInfo

```dart
class RawMenuOverlayInfo {}
```

Anchor and menu information passed to [RawMenuAnchor].

### RawMenuOverlayInfo()

```dart
RawMenuOverlayInfo({required ui.Rect anchorRect, required ui.Size overlaySize, required Object tapRegionGroupId, Offset? position})
```

Creates a [RawMenuOverlayInfo].

### anchorRect

```dart
ui.Rect anchorRect
```

The position of the anchor widget that the menu is attached to, relative to the nearest ancestor [Overlay] when [RawMenuAnchor.useRootOverlay] is false, or the root [Overlay] when [RawMenuAnchor.useRootOverlay] is true.

### overlaySize

```dart
ui.Size overlaySize
```

The [Size] of the overlay that the menu is being shown in.

### position

```dart
Offset? position
```

The `position` argument passed to [MenuController.open].

The position should be used to offset the menu relative to the top-left corner of the anchor.

### tapRegionGroupId

```dart
Object tapRegionGroupId
```

The [TapRegion.groupId] of the [TapRegion] that wraps widgets in this menu system.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# RawMenuAnchorOverlayBuilder

```dart
typedef RawMenuAnchorOverlayBuilder = Widget Function(BuildContext context, RawMenuOverlayInfo info)
```

Signature for the builder function used by [RawMenuAnchor.overlayBuilder] to build a menu's overlay.

The `context` is the context that the overlay is being built in.

The `info` describes the anchor's [Rect], the [Size] of the overlay, the [TapRegion.groupId] used by members of the menu system, and the `position` argument passed to [MenuController.open].

# RawMenuAnchorChildBuilder

```dart
typedef RawMenuAnchorChildBuilder = Widget Function(BuildContext context, MenuController controller, Widget? child)
```

Signature for the builder function used by [RawMenuAnchor.builder] to build the widget that the [RawMenuAnchor] surrounds.

The `context` is the context in which the anchor is being built.

The `controller` is the [MenuController] that can be used to open and close the menu.

The `child` is an optional child supplied as the [RawMenuAnchor.child] attribute. The child is intended to be incorporated in the result of the function.

# RawMenuAnchorOpenRequestedCallback

```dart
typedef RawMenuAnchorOpenRequestedCallback = void Function(Offset? position, VoidCallback showOverlay)
```

Signature for the callback used by [RawMenuAnchor.onOpenRequested] to intercept requests to open a menu.

See [RawMenuAnchor.onOpenRequested] for more information.

# RawMenuAnchorCloseRequestedCallback

```dart
typedef RawMenuAnchorCloseRequestedCallback = void Function(VoidCallback hideOverlay)
```

Signature for the callback used by [RawMenuAnchor.onCloseRequested] to intercept requests to close a menu.

See [RawMenuAnchor.onCloseRequested] for more information.

# RawMenuAnchor

```dart
class RawMenuAnchor extends StatefulWidget {}
```

A widget that wraps a child and anchors a floating menu.

The child can be any widget, but is typically a button, a text field, or, in the case of context menus, the entire screen.

The menu overlay of a [RawMenuAnchor] is shown by calling [MenuController.open] on an attached [MenuController].

When a [RawMenuAnchor] is opened, [overlayBuilder] is called to construct the menu contents within an [Overlay]. The [Overlay] allows the menu to "float" on top of other widgets. The `info` argument passed to [overlayBuilder] provides the anchor's [Rect], the [Size] of the overlay, the [TapRegion.groupId] used by members of the menu system, and the `position` argument passed to [MenuController.open].

If [MenuController.open] is called with a `position` argument, it will be passed to the `info` argument of the `overlayBuilder` function.

The [RawMenuAnchor] does not manage semantics and focus of the menu.

### Adding animations to menus

A [RawMenuAnchor] has no knowledge of animations, as evident from its APIs, which don't involve [AnimationController] at all. It only knows whether the overlay is shown or hidden.

If another widget intends to implement a menu with opening and closing transitions, [RawMenuAnchor]'s overlay should remain visible throughout both the opening and closing animation durations.

This means that the `showOverlay` callback passed to [onOpenRequested] should be called before the first frame of the opening animation. Conversely, `hideOverlay` within [onCloseRequested] should only be called after the closing animation has completed.

This also means that, if [MenuController.open] is called while the overlay is already visible, [RawMenuAnchor] has no way of knowing whether the menu is currently opening, closing, or stably displayed. The parent widget will need to manage additional information (such as the state of an [AnimationController]) to determine how to respond in such scenarios.

To programmatically control a [RawMenuAnchor], like opening or closing it, or checking its state, you can get its associated [MenuController]. Use `MenuController.maybeOf(BuildContext context)` to retrieve the controller for the closest [RawMenuAnchor] ancestor of a given `BuildContext`. More detailed usage of [MenuController] is available in its class documentation.

{@tool dartpad}

This example uses a [RawMenuAnchor] to build a basic select menu with four items.

** See code in examples/api/lib/widgets/raw_menu_anchor/raw_menu_anchor.0.dart ** {@end-tool}

{@tool dartpad}

This example uses [RawMenuAnchor.onOpenRequested] and [RawMenuAnchor.onCloseRequested] to build an animated menu.

** See code in examples/api/lib/widgets/raw_menu_anchor/raw_menu_anchor.2.dart ** {@end-tool}

{@tool dartpad}

This example uses [RawMenuAnchor.onOpenRequested] and [RawMenuAnchor.onCloseRequested] to build an animated nested menu.

** See code in examples/api/lib/widgets/raw_menu_anchor/raw_menu_anchor.3.dart ** {@end-tool}

### RawMenuAnchor()

```dart
RawMenuAnchor({dynamic key, FocusNode? childFocusNode, bool consumeOutsideTaps = false, VoidCallback? onOpen, VoidCallback? onClose, RawMenuAnchorOpenRequestedCallback onOpenRequested = _defaultOnOpenRequested, RawMenuAnchorCloseRequestedCallback onCloseRequested = _defaultOnCloseRequested, bool useRootOverlay = false, RawMenuAnchorChildBuilder? builder, required MenuController controller, required RawMenuAnchorOverlayBuilder overlayBuilder, Widget? child})
```

A [RawMenuAnchor] that delegates overlay construction to an [overlayBuilder].

The [overlayBuilder] must not be null.

### onOpen

```dart
VoidCallback? onOpen
```

Called when the menu overlay is shown.

When [MenuController.open] is called, [onOpenRequested] is invoked with a `showOverlay` callback that, when called, shows the menu overlay and triggers [onOpen].

The default implementation of [onOpenRequested] calls `showOverlay` synchronously, thereby calling [onOpen] synchronously. In this case, [onOpen] is called regardless of whether the menu overlay is already showing.

Custom implementations of [onOpenRequested] can delay the call to `showOverlay`, or not call it at all, in which case [onOpen] will not be called. Calling `showOverlay` after disposal is a no-op, and will not trigger [onOpen].

A typical usage is to respond when the menu first becomes interactive, such as by setting focus to a menu item.

### onClose

```dart
VoidCallback? onClose
```

Called when the menu overlay is hidden.

When [MenuController.close] is called, [onCloseRequested] is invoked with a `hideOverlay` callback that, when called, hides the menu overlay and triggers [onClose].

The default implementation of [onCloseRequested] calls `hideOverlay` synchronously, thereby calling [onClose] synchronously. In this case, [onClose] is called regardless of whether the menu overlay is already hidden.

Custom implementations of [onCloseRequested] can delay the call to `hideOverlay` or not call it at all, in which case [onClose] will not be called. Calling `hideOverlay` after disposal is a no-op, and will not trigger [onClose].

### onOpenRequested

```dart
RawMenuAnchorOpenRequestedCallback onOpenRequested
```

Called when a request is made to open the menu.

This callback is triggered every time [MenuController.open] is called, even when the menu overlay is already showing. As a result, this callback is a good place to begin menu opening animations, or observe when a menu is repositioned.

After an open request is intercepted, the `showOverlay` callback should be called when the menu overlay (the widget built by [overlayBuilder]) is ready to be shown. This can occur immediately (the default behavior), or after a delay. Calling `showOverlay` sets [MenuController.isOpen] to true, builds (or rebuilds) the overlay widget, and shows the menu overlay at the front of the overlay stack.

If `showOverlay` is not called, the menu will stay hidden. Calling `showOverlay` after disposal is a no-op, meaning it will not trigger [onOpen] or show the menu overlay.

If a [RawMenuAnchor] is used in a themed menu that plays an opening animation, the themed menu should show the overlay before starting the opening animation, since the animation plays on the overlay itself.

The `position` argument is the `position` that [MenuController.open] was called with.

A typical [onOpenRequested] consists of the following steps:

1.  Optional delay.
2.  Call `showOverlay` (whose call chain eventually invokes [onOpen]).
3.  Optionally start the opening animation.

Defaults to a callback that immediately shows the menu.

### onCloseRequested

```dart
RawMenuAnchorCloseRequestedCallback onCloseRequested
```

Called when a request is made to close the menu.

This callback can be used to add a delay or a closing animation before the menu is hidden.

This callback is triggered every time [MenuController.close] is called, even when the menu overlay is already hidden.

This callback is also triggered when a sibling [RawMenuAnchor] is opened. In this case, the callback can be used to add a delay or a closing animation while the sibling menu opens. When implementing this behavior, consider disabling interactions so that the closing menu does not interfere with the opening sibling menu. Also consider disabling semantics, focus, and hit testing for the closing menu for the duration of the closing animation.

Pending timers or animations started in a previous call to [onCloseRequested] should be canceled when this callback is triggered to prevent them from closing the menu at an unintended time.

If the menu is not closed, this callback will also be called when the root menu anchor is scrolled and when the screen is resized.

After a close request is intercepted and closing behaviors have completed, the `hideOverlay` callback should be called. This callback sets [MenuController.isOpen] to false and hides the menu overlay widget. If the [RawMenuAnchor] is used in a themed menu that plays a closing animation, `hideOverlay` should be called after the closing animation has ended, since the animation plays on the overlay itself. This means that [MenuController.isOpen] will stay true while closing animations are running.

Calling `hideOverlay` after disposal is a no-op, meaning it will not trigger [onClose] or hide the menu overlay.

Typically, [onCloseRequested] consists of the following steps:

1.  Optionally start the closing animation and wait for it to complete.
2.  Call `hideOverlay` (whose call chain eventually invokes [onClose]).

Throughout the closing sequence, menus should typically not be focusable or interactive.

Defaults to a callback that immediately hides the menu.

### builder

```dart
RawMenuAnchorChildBuilder? builder
```

A builder that builds the widget that this [RawMenuAnchor] surrounds.

Typically, this is a button used to open the menu by calling [MenuController.open] on the `controller` passed to the builder.

If not supplied, then the [RawMenuAnchor] will be the size that its parent allocates for it.

### child

```dart
Widget? child
```

The optional child to be passed to the [builder].

Supply this child if there is a portion of the widget tree built in [builder] that doesn't depend on the `controller` or `context` supplied to the [builder]. It will be more efficient, since Flutter doesn't then need to rebuild this child when those change.

### overlayBuilder

```dart
RawMenuAnchorOverlayBuilder overlayBuilder
```

Called to build and position the menu overlay.

The [overlayBuilder] function is passed a [RawMenuOverlayInfo] object that defines the anchor's [Rect], the [Size] of the overlay, the [TapRegion.groupId] for the menu system, and the position [Offset] passed to [MenuController.open].

To ensure taps are properly consumed, the [RawMenuOverlayInfo.tapRegionGroupId] should be passed to a [TapRegion] widget that wraps the menu panel.

```dart
TapRegion(
  groupId: info.tapRegionGroupId,
  onTapOutside: (PointerDownEvent event) {
    MenuController.maybeOf(context)?.close();
  },
  child: Column(children: menuItems),
)
```

### useRootOverlay

```dart
bool useRootOverlay
```

{@template flutter.widgets.RawMenuAnchor.useRootOverlay} Whether the menu panel should be rendered in the root [Overlay].

When true, the menu is mounted in the root overlay. Rendering the menu in the root overlay prevents the menu from being obscured by other widgets.

When false, the menu is rendered in the nearest ancestor [Overlay].

Submenus will always use the same overlay as their top-level ancestor, so setting a [useRootOverlay] value on a submenu will have no effect. {@endtemplate}

Defaults to false on overlay menus.

### childFocusNode

```dart
FocusNode? childFocusNode
```

The [FocusNode] attached to the widget that takes focus when the menu is opened or closed.

If not supplied, the anchor will not retain focus when the menu is opened.

### consumeOutsideTaps

```dart
bool consumeOutsideTaps
```

Whether a tap event that closes the menu will be permitted to continue on to the gesture arena.

If false, then tapping outside of a menu when the menu is open will both close the menu, and allow the tap to participate in the gesture arena.

If true, then it will only close the menu, and the tap event will be consumed.

Defaults to false.

### controller

```dart
MenuController controller
```

A [MenuController] that allows opening and closing of the menu from other widgets.

### createState()

```dart
State<RawMenuAnchor> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RawMenuAnchorGroup

```dart
class RawMenuAnchorGroup extends StatefulWidget {}
```

Creates a menu anchor that is always visible and is not displayed in an [OverlayPortal].

A [RawMenuAnchorGroup] can be used to create a menu bar that handles external taps and keyboard shortcuts, but defines no default focus or keyboard traversal to enable more flexibility.

When a [MenuController] is given to a [RawMenuAnchorGroup],

- [MenuController.open] has no effect.
- [MenuController.close] closes all child [RawMenuAnchor]s that are open.
- [MenuController.isOpen] reflects whether any child [RawMenuAnchor] is open.

A [child] must be provided.

{@tool dartpad}

This example uses [RawMenuAnchorGroup] to build a menu bar with four submenus. Hovering over a menu item opens its respective submenu. Selecting a menu item will close the menu and update the selected item text.

** See code in examples/api/lib/widgets/raw_menu_anchor/raw_menu_anchor.1.dart ** {@end-tool}

See also:

- [MenuBar], which wraps this widget with standard layout and semantics and focus management.
- [MenuAnchor], a menu anchor that follows the Material Design guidelines.
- [RawMenuAnchor], a widget that defines a region attached to a floating submenu.

### RawMenuAnchorGroup()

```dart
RawMenuAnchorGroup({dynamic key, required Widget child, required MenuController controller})
```

Creates a [RawMenuAnchorGroup].

### child

```dart
Widget child
```

The child displayed by the [RawMenuAnchorGroup].

To access the [MenuController] from the [child], place the child in a builder and call [MenuController.maybeOf].

### controller

```dart
MenuController controller
```

An [MenuController] that allows the closing of the menu from other widgets.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createState()

```dart
State<RawMenuAnchorGroup> createState()
```

# MenuController

```dart
class MenuController {}
```

A controller used to manage a menu created by a subclass of [RawMenuAnchor], such as [MenuAnchor], [MenuBar], [SubmenuButton].

A [MenuController] is used to control and interrogate a menu after it has been created, with methods such as [open] and [close], and state accessors like [isOpen].

[MenuController.maybeOf] can be used to retrieve a controller from the [BuildContext] of a widget that is a descendant of a [MenuAnchor], [MenuBar], [SubmenuButton], or [RawMenuAnchor]. Doing so will not establish a dependency relationship.

See also:

- [MenuAnchor], a menu anchor that follows the Material Design guidelines.
- [MenuBar], a widget that creates a menu bar that can take an optional [MenuController].
- [SubmenuButton], a widget that has a button that manages a submenu.
- [RawMenuAnchor], a widget that defines a region that has submenu.

### isOpen

```dart
bool get isOpen
```

Whether or not the menu associated with this [MenuController] is open.

### open()

```dart
void open({Offset? position})
```

Opens the menu that this [MenuController] is associated with.

If `position` is given, then the menu will open at the position given, in the coordinate space of the [RawMenuAnchor] that this controller is attached to.

If given, the `position` will override the [MenuAnchor.alignmentOffset] given to the [MenuAnchor].

If the menu's anchor point is scrolled by an ancestor, or the view changes size, then any open menu will automatically close.

### close()

```dart
void close()
```

Close the menu that this [MenuController] is associated with.

Associating with a menu is done by passing a [MenuController] to a [MenuAnchor], [RawMenuAnchor], or [RawMenuAnchorGroup].

If the menu's anchor point is scrolled by an ancestor, or the view changes size, then any open menu will automatically close.

### closeChildren()

```dart
void closeChildren()
```

Close the children of the menu associated with this [MenuController], without closing the menu itself.

### maybeOf()

```dart
MenuController? maybeOf(BuildContext context)
```

Returns the [MenuController] of the ancestor [RawMenuAnchor] nearest to the given `context`, if one exists. Otherwise, returns null.

This method will not establish a dependency relationship, so the calling widget will not rebuild when the menu opens and closes, nor when the [MenuController] changes.

### maybeIsOpenOf()

```dart
bool? maybeIsOpenOf(BuildContext context)
```

Returns the value of [MenuController.isOpen] of the ancestor [RawMenuAnchor] or [RawMenuAnchorGroup] nearest to the given `context`, if one exists. Otherwise, returns null.

This method will establish a dependency relationship, so the calling widget will rebuild when the menu opens and closes.

### toString()

```dart
String toString()
```

# DismissMenuAction

```dart
class DismissMenuAction extends DismissAction {}
```

An action that closes all the menus associated with the given [MenuController].

See also:

- [MenuAnchor], a material-themed widget that hosts a cascading submenu.
- [MenuBar], a widget that defines a menu bar with cascading submenus.
- [RawMenuAnchor], a widget that hosts a cascading submenu.
- [MenuController], a controller used to manage menus created by a [RawMenuAnchor].

### DismissMenuAction()

```dart
DismissMenuAction({required MenuController controller})
```

Creates a [DismissMenuAction].

### controller

```dart
MenuController controller
```

The [MenuController] that manages the menu which should be dismissed upon invocation.

### invoke()

```dart
void invoke(DismissIntent intent)
```

### isEnabled()

```dart
bool isEnabled(DismissIntent intent)
```
