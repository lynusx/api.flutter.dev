@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'drag_target.dart'; @docImport 'implicit_animations.dart'; @docImport 'media_query.dart'; @docImport 'navigator.dart'; @docImport 'routes.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver.dart'; @docImport 'text.dart';

# OverlayChildLayoutBuilder

```dart
typedef OverlayChildLayoutBuilder = Widget Function(BuildContext context, OverlayChildLayoutInfo info)
```

The signature of the widget builder callback used in [OverlayPortal.overlayChildLayoutBuilder].

# OverlayChildLayoutInfo

```dart
extension type OverlayChildLayoutInfo._((Size childSize, Matrix4 childPaintTransform, Size overlaySize) _info) {}
```

The additional layout information available to the [OverlayPortal.overlayChildLayoutBuilder] callback.

### childSize

```dart
Size get childSize
```

The size of [OverlayPortal.child] in its own coordinates.

### childPaintTransform

```dart
Matrix4 get childPaintTransform
```

The paint transform of [OverlayPortal.child], in the target [Overlay]'s coordinates.

### overlaySize

```dart
Size get overlaySize
```

The size of the target [Overlay] in its own coordinates.

# OverlayEntry

```dart
class OverlayEntry implements Listenable {}
```

A place in an [Overlay] that can contain a widget.

Overlay entries are inserted into an [Overlay] using the [OverlayState.insert] or [OverlayState.insertAll] functions. To find the closest enclosing overlay for a given [BuildContext], use the [Overlay.of] function.

An overlay entry can be in at most one overlay at a time. To remove an entry from its overlay, call the [remove] function on the overlay entry.

Because an [Overlay] uses a [Stack] layout, overlay entries can use [Positioned] and [AnimatedPositioned] to position themselves within the overlay.

For example, [Draggable] uses an [OverlayEntry] to show the drag avatar that follows the user's finger across the screen after the drag begins. Using the overlay to display the drag avatar lets the avatar float over the other widgets in the app. As the user's finger moves, draggable calls [markNeedsBuild] on the overlay entry to cause it to rebuild. In its build, the entry includes a [Positioned] with its top and left property set to position the drag avatar near the user's finger. When the drag is over, [Draggable] removes the entry from the overlay to remove the drag avatar from view.

By default, if there is an entirely [opaque] entry over this one, then this one will not be included in the widget tree (in particular, stateful widgets within the overlay entry will not be instantiated). To ensure that your overlay entry is still built even if it is not visible, set [maintainState] to true. This is more expensive, so should be done with care. In particular, if widgets in an overlay entry with [maintainState] set to true repeatedly call [State.setState], the user's battery will be drained unnecessarily.

[OverlayEntry] is a [Listenable] that notifies when the widget built by [builder] is mounted or unmounted, whose exact state can be queried by [mounted]. After the owner of the [OverlayEntry] calls [remove] and then [dispose], the widget may not be immediately removed from the widget tree. As a result listeners of the [OverlayEntry] can get notified for one last time after the [dispose] call, when the widget is eventually unmounted.

{@macro flutter.widgets.overlayPortalVsOverlayEntry}

See also:

- [OverlayPortal], an alternative API for inserting widgets into an [Overlay] using a builder callback.
- [Overlay], a stack of entries that can be managed independently.
- [OverlayState], the current state of an Overlay.
- [WidgetsApp], a convenience widget that wraps a number of widgets that are commonly required for an application.
- [MaterialApp], a convenience widget that wraps a number of widgets that are commonly required for Material Design applications.

### OverlayEntry()

```dart
OverlayEntry({required WidgetBuilder builder, bool opaque = false, bool maintainState = false, bool canSizeOverlay = false})
```

Creates an overlay entry.

To insert the entry into an [Overlay], first find the overlay using [Overlay.of] and then call [OverlayState.insert]. To remove the entry, call [remove] on the overlay entry itself.

### builder

```dart
WidgetBuilder builder
```

This entry will include the widget built by this builder in the overlay at the entry's position.

To cause this builder to be called again, call [markNeedsBuild] on this overlay entry.

### opaque

```dart
bool get opaque
```

Whether this entry occludes the entire overlay.

If an entry claims to be opaque, then, for efficiency, the overlay will skip building entries below that entry unless they have [maintainState] set.

### opaque

```dart
set opaque(bool value)
```

### maintainState

```dart
bool get maintainState
```

Whether this entry must be included in the tree even if there is a fully [opaque] entry above it.

By default, if there is an entirely [opaque] entry over this one, then this one will not be included in the widget tree (in particular, stateful widgets within the overlay entry will not be instantiated). To ensure that your overlay entry is still built even if it is not visible, set [maintainState] to true. This is more expensive, so should be done with care. In particular, if widgets in an overlay entry with [maintainState] set to true repeatedly call [State.setState], the user's battery will be drained unnecessarily.

This is used by the [Navigator] and [Route] objects to ensure that routes are kept around even when in the background, so that [Future]s promised from subsequent routes will be handled properly when they complete.

### maintainState

```dart
set maintainState(bool value)
```

### canSizeOverlay

```dart
bool canSizeOverlay
```

Whether the content of this [OverlayEntry] can be used to size the [Overlay].

In most situations the overlay sizes itself based on its incoming constraints to be as large as possible. However, if that would result in an infinite size, it has to rely on one of its children to size itself. In this situation, the overlay will consult the topmost non-[Positioned] overlay entry that has this property set to true, lay it out with the incoming [BoxConstraints] of the overlay, and force all other non-[Positioned] overlay entries to have the same size. The [Positioned] entries are laid out as usual based on the calculated size of the overlay.

Overlay entries that set this to true must be able to handle unconstrained [BoxConstraints].

Setting this to true has no effect if the overlay entry uses a [Positioned] widget to position itself in the overlay.

### mounted

```dart
bool get mounted
```

Whether the [OverlayEntry] is currently mounted in the widget tree.

The [OverlayEntry] notifies its listeners when this value changes.

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### remove()

```dart
void remove()
```

Remove this entry from the overlay.

This should only be called once.

This method removes this overlay entry from the overlay immediately. The UI will be updated in the same frame if this method is called before the overlay rebuild in this frame; otherwise, the UI will be updated in the next frame. This means that it is safe to call during builds, but also that if you do call this after the overlay rebuild, the UI will not update until the next frame (i.e. many milliseconds later).

### markNeedsBuild()

```dart
void markNeedsBuild()
```

Cause this entry to rebuild during the next pipeline flush.

You need to call this function if the output of [builder] has changed.

### dispose()

```dart
void dispose()
```

Discards any resources used by this [OverlayEntry].

The [remove] method must be called before this method if the [OverlayEntry] is inserted into an [Overlay].

After this is called, the object is not in a usable state and should be discarded (calls to [addListener] will throw after the object is disposed). However, the listeners registered may not be immediately released until the widget built using this [OverlayEntry] is unmounted from the widget tree.

This method should only be called by the object's owner.

### toString()

```dart
String toString()
```

# Overlay

```dart
class Overlay extends StatefulWidget {}
```

A stack of entries that can be managed independently.

Overlays let independent child widgets "float" visual elements on top of other widgets by inserting them into the overlay's stack. The overlay lets each of these widgets manage their participation in the overlay using [OverlayEntry] objects.

Although you can create an [Overlay] directly, it's most common to use the overlay created by the [Navigator] in a [WidgetsApp], [CupertinoApp] or a [MaterialApp]. The navigator uses its overlay to manage the visual appearance of its routes.

The [Overlay] widget uses a custom stack implementation, which is very similar to the [Stack] widget. The main use case of [Overlay] is related to navigation and being able to insert widgets on top of the pages in an app. For layout purposes unrelated to navigation, consider using [Stack] instead.

An [Overlay] widget requires a [Directionality] widget to be in scope, so that it can resolve direction-sensitive coordinates of any [Positioned.directional] children.

For widgets drawn in an [OverlayEntry], do not assume that the size of the [Overlay] is the size returned by [MediaQuery.sizeOf]. Nested overlays can have different sizes.

{@tool dartpad} This example shows how to use the [Overlay] to highlight the [NavigationBar] destination.

** See code in examples/api/lib/widgets/overlay/overlay.0.dart ** {@end-tool}

See also:

- [OverlayEntry], the class that is used for describing the overlay entries.
- [OverlayState], which is used to insert the entries into the overlay.
- [WidgetsApp], which inserts an [Overlay] widget indirectly via its [Navigator].
- [MaterialApp], which inserts an [Overlay] widget indirectly via its [Navigator].
- [CupertinoApp], which inserts an [Overlay] widget indirectly via its [Navigator].
- [Stack], which allows directly displaying a stack of widgets.

### Overlay()

```dart
Overlay({dynamic key, List<OverlayEntry> initialEntries = const <OverlayEntry>[], Clip clipBehavior = Clip.hardEdge, bool alwaysSizeToContent = false})
```

Creates an overlay.

The initial entries will be inserted into the overlay when its associated [OverlayState] is initialized.

Rather than creating an overlay, consider using the overlay that is created by the [Navigator] in a [WidgetsApp], [CupertinoApp], or a [MaterialApp] for the application.

### wrap()

```dart
Widget wrap({Key? key, Clip clipBehavior = Clip.hardEdge, bool alwaysSizeToContent = false, required Widget child})
```

Wrap the provided `child` in an [Overlay] to allow other visual elements (packed in [OverlayEntry]s) to float on top of the child.

This is a convenience method over the regular [Overlay] constructor: It creates an [Overlay] and puts the provided `child` in an [OverlayEntry] at the bottom of that newly created Overlay.

### initialEntries

```dart
List<OverlayEntry> initialEntries
```

The entries to include in the overlay initially.

These entries are only used when the [OverlayState] is initialized. If you are providing a new [Overlay] description for an overlay that's already in the tree, then the new entries are ignored.

To add entries to an [Overlay] that is already in the tree, use [Overlay.of] to obtain the [OverlayState] (or assign a [GlobalKey] to the [Overlay] widget and obtain the [OverlayState] via [GlobalKey.currentState]), and then use [OverlayState.insert] or [OverlayState.insertAll].

To remove an entry from an [Overlay], use [OverlayEntry.remove].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### alwaysSizeToContent

```dart
bool alwaysSizeToContent
```

Determines that the overlay should always size itself to content.

Normally overlay will only size itself to content if the incoming constraints are infinite and there is a [OverlayEntry] that can size the overlay. Setting this to `true` will force this behavior even for finite (but possibly loose) constraints.

Setting this to true requires an [OverlayEntry] that can size the overlay based on itself ([OverlayEntry.canSizeOverlay] set to true). If not provided an exception is thrown.

### of()

```dart
OverlayState of(BuildContext context, {bool rootOverlay = false, Widget? debugRequiredFor})
```

The [OverlayState] from the closest instance of [Overlay] that encloses the given context within the closest [LookupBoundary], and, in debug mode, will throw if one is not found.

In debug mode, if the `debugRequiredFor` argument is provided and an overlay isn't found, then this function will throw an exception containing the runtime type of the given widget in the error message. The exception attempts to explain that the calling [Widget] (the one given by the `debugRequiredFor` argument) needs an [Overlay] to be present to function. If `debugRequiredFor` is not supplied, then the error message is more generic.

Typical usage is as follows:

```dart
OverlayState overlay = Overlay.of(context);
```

{@template flutter.widgets.Overlay.of} If `rootOverlay` is set to true, the state from the furthest instance of this class is given instead. Useful for installing overlay entries above all subsequent instances of [Overlay]. {@endtemplate}

See also:

- [Overlay.maybeOf] for a similar function that returns null if an [Overlay] is not found.

### maybeOf()

```dart
OverlayState? maybeOf(BuildContext context, {bool rootOverlay = false})
```

The [OverlayState] from the closest instance of [Overlay] that encloses the given context within the closest [LookupBoundary], if any.

Typical usage is as follows:

```dart
OverlayState? overlay = Overlay.maybeOf(context);
```

{@macro flutter.widgets.Overlay.of}

See also:

- [Overlay.of] for a similar function that returns a non-nullable result and throws if an [Overlay] is not found.

### createState()

```dart
OverlayState createState()
```

# OverlayState

```dart
class OverlayState extends State<Overlay> with TickerProviderStateMixin {}
```

The current state of an [Overlay].

Used to insert [OverlayEntry]s into the overlay using the [insert] and [insertAll] functions.

### initState()

```dart
void initState()
```

### insert()

```dart
void insert(OverlayEntry entry, {OverlayEntry? below, OverlayEntry? above})
```

Insert the given entry into the overlay.

If `below` is non-null, the entry is inserted just below `below`. If `above` is non-null, the entry is inserted just above `above`. Otherwise, the entry is inserted on top.

It is an error to specify both `above` and `below`.

### insertAll()

```dart
void insertAll(Iterable<OverlayEntry> entries, {OverlayEntry? below, OverlayEntry? above})
```

Insert all the entries in the given iterable.

If `below` is non-null, the entries are inserted just below `below`. If `above` is non-null, the entries are inserted just above `above`. Otherwise, the entries are inserted on top.

It is an error to specify both `above` and `below`.

### rearrange()

```dart
void rearrange(Iterable<OverlayEntry> newEntries, {OverlayEntry? below, OverlayEntry? above})
```

Remove all the entries listed in the given iterable, then reinsert them into the overlay in the given order.

Entries mention in `newEntries` but absent from the overlay are inserted as if with [insertAll].

Entries not mentioned in `newEntries` but present in the overlay are positioned as a group in the resulting list relative to the entries that were moved, as specified by one of `below` or `above`, which, if specified, must be one of the entries in `newEntries`:

If `below` is non-null, the group is positioned just below `below`. If `above` is non-null, the group is positioned just above `above`. Otherwise, the group is left on top, with all the rearranged entries below.

It is an error to specify both `above` and `below`.

### debugIsVisible()

```dart
bool debugIsVisible(OverlayEntry entry)
```

(DEBUG ONLY) Check whether a given entry is visible (i.e., not behind an opaque entry).

This is an O(N) algorithm, and should not be necessary except for debug asserts. To avoid people depending on it, this function is implemented only in debug mode, and always returns false in release mode.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OverlayPortalController

```dart
class OverlayPortalController {}
```

A class to show, hide and bring to top an [OverlayPortal]'s overlay child in the target [Overlay].

A [OverlayPortalController] can only be given to at most one [OverlayPortal] at a time. When an [OverlayPortalController] is moved from one [OverlayPortal] to another, its [isShowing] state does not carry over.

[OverlayPortalController.show] and [OverlayPortalController.hide] can be called even before the controller is assigned to any [OverlayPortal], but they typically should not be called while the widget tree is being rebuilt.

### OverlayPortalController()

```dart
OverlayPortalController({String? debugLabel})
```

Creates an [OverlayPortalController], optionally with a String identifier `debugLabel`.

### show()

```dart
void show()
```

Show the overlay child of the [OverlayPortal] this controller is attached to, at the top of the target [Overlay].

When there are more than one [OverlayPortal]s that target the same [Overlay], the overlay child of the last [OverlayPortal] to have called [show] appears at the top level, unobstructed.

If [isShowing] is already true, calling this method brings the overlay child it controls to the top.

This method should typically not be called while the widget tree is being rebuilt.

### hide()

```dart
void hide()
```

Hide the [OverlayPortal]'s overlay child.

Once hidden, the overlay child will be removed from the widget tree the next time the widget tree rebuilds, and stateful widgets in the overlay child may lose states as a result.

This method should typically not be called while the widget tree is being rebuilt.

### isShowing

```dart
bool get isShowing
```

Whether the associated [OverlayPortal] should build and show its overlay child, using its `overlayChildBuilder`.

### toggle()

```dart
void toggle()
```

Convenience method for toggling the current [isShowing] status.

This method should typically not be called while the widget tree is being rebuilt.

### toString()

```dart
String toString()
```

# OverlayChildLocation

```dart
enum OverlayChildLocation {}
```

The location of the [Overlay] that an [OverlayPortal] renders its overlay child on.

This is typically used in [OverlayPortal].

The [OverlayPortal] renders its overlay child on the closest ancestor [Overlay] above the widget tree.

The [OverlayPortal] renders its overlay child on the root [Overlay] above the widget tree.

In case of multi-view apps, the root [Overlay] refers to the first Overlay below the View.

# OverlayPortal

```dart
class OverlayPortal extends StatefulWidget {}
```

A widget that renders its overlay child on an [Overlay].

The overlay child is initially hidden until [OverlayPortalController.show] is called on the associated [controller]. The [OverlayPortal] uses [overlayChildBuilder] to build its overlay child and renders it on the specified [Overlay] as if it was inserted using an [OverlayEntry], while it can depend on the same set of [InheritedWidget]s (such as [Theme]) that this widget can depend on.

This widget requires an [Overlay] ancestor in the widget tree when its overlay child is showing. The overlay child is rendered by the [Overlay] ancestor, not by the widget itself. This allows the overlay child to float above other widgets, independent of its position in the widget tree.

When [OverlayPortalController.hide] is called, the widget built using [overlayChildBuilder] will be removed from the widget tree the next time the widget rebuilds. Stateful descendants in the overlay child subtree may lose states as a result.

{@tool dartpad} This example uses an [OverlayPortal] to build a tooltip that becomes visible when the user taps on the [child] widget. There's a [DefaultTextStyle] above the [OverlayPortal] controlling the [TextStyle] of both the [child] widget and the widget [overlayChildBuilder] builds, which isn't otherwise doable if the tooltip was added as an [OverlayEntry].

** See code in examples/api/lib/widgets/overlay/overlay_portal.0.dart ** {@end-tool}

### Paint Order

In an [Overlay], an overlay child is painted after the [OverlayEntry] associated with its [OverlayPortal] (that is, the [OverlayEntry] closest to the [OverlayPortal] in the widget tree, which usually represents the enclosing [Route]), and before the next [OverlayEntry].

When an [OverlayEntry] has multiple associated [OverlayPortal]s, the paint order between their overlay children is the order in which [OverlayPortalController.show] was called. The last [OverlayPortal] to have called `show` gets to paint its overlay child in the foreground.

### Semantics

The semantics subtree generated by the overlay child is considered attached to [OverlayPortal] instead of the target [Overlay]. An [OverlayPortal]'s semantics subtree can be dropped from the semantics tree due to invisibility while the overlay child is still visible (for example, when the [OverlayPortal] is completely invisible in a [ListView] but kept alive by a [KeepAlive] widget). When this happens the semantics subtree generated by the overlay child is also dropped, even if the overlay child is still visible on screen.

{@template flutter.widgets.overlayPortalVsOverlayEntry}

### Differences between [OverlayPortal] and [OverlayEntry]

The main difference between [OverlayEntry] and [OverlayPortal] is that [OverlayEntry] builds its widget subtree as a child of the target [Overlay], while [OverlayPortal] uses [OverlayPortal.overlayChildBuilder] to build a child widget of itself. This allows [OverlayPortal]'s overlay child to depend on the same set of [InheritedWidget]s as [OverlayPortal], and it's also guaranteed that the overlay child will not outlive its [OverlayPortal].

On the other hand, [OverlayPortal]'s implementation is more complex. For instance, it does a bit more work than a regular widget during global key reparenting. If the content to be shown on the [Overlay] doesn't benefit from being a part of [OverlayPortal]'s subtree, consider using an [OverlayEntry] instead. {@endtemplate}

See also:

- [OverlayEntry], an alternative API for inserting widgets into an [Overlay].
- [Positioned], which can be used to size and position the overlay child in relation to the target [Overlay]'s boundaries.
- [CompositedTransformFollower], which can be used to position the overlay child in relation to the linked [CompositedTransformTarget] widget.

### OverlayPortal()

```dart
OverlayPortal({dynamic key, required OverlayPortalController controller, required WidgetBuilder overlayChildBuilder, OverlayChildLocation overlayLocation = OverlayChildLocation.nearestOverlay, Widget? child})
```

Creates an [OverlayPortal] that renders the widget [overlayChildBuilder] builds on the closest [Overlay] when [OverlayPortalController.show] is called.

The [overlayLocation] sets which [Overlay] this widget attaches the widget returned by [overlayChildBuilder] to. Defaults to [OverlayChildLocation.nearestOverlay].

### OverlayPortal.targetsRootOverlay()

```dart
OverlayPortal.targetsRootOverlay({dynamic key, required OverlayPortalController controller, required WidgetBuilder overlayChildBuilder, Widget? child})
```

Creates an [OverlayPortal] that renders the widget [overlayChildBuilder] builds on the root [Overlay] when [OverlayPortalController.show] is called.

### OverlayPortal.overlayChildLayoutBuilder()

```dart
OverlayPortal.overlayChildLayoutBuilder({Key? key, required OverlayPortalController controller, required OverlayChildLayoutBuilder overlayChildBuilder, OverlayChildLocation overlayLocation = OverlayChildLocation.nearestOverlay, required Widget? child})
```

Creates an [OverlayPortal] that renders the widget `overlayChildBuilder` builds on the closest [Overlay] when [OverlayPortalController.show] is called.

Developers can use `overlayChildBuilder` to configure the overlay child based on the size and the location of [OverlayPortal.child] within the target [Overlay], as well as the size of the [Overlay] itself. This allows the overlay child to, for example, always follow [OverlayPortal.child] and at the same time resize itself base on how close it is to the edges of the [Overlay].

The `overlayChildBuilder` callback is called during layout. To ensure the paint transform of [OverlayPortal.child] in relation to the target [Overlay] is up-to-date by then, all [RenderObject]s between the [OverlayPortal] to the target [Overlay] must establish their paint transform during the layout phase, which most [RenderObject]s do. One exception is the [CompositedTransformFollower] widget, whose [RenderObject] only establishes the paint transform when composited. Putting a [CompositedTransformFollower] between the [OverlayPortal] and the [Overlay] may result in an incorrect child paint transform being provided to the `overlayChildBuilder` and will cause an assertion in debug mode.

The [overlayLocation] sets which [Overlay] this widget attaches the widget returned by `overlayChildBuilder` to. Defaults to [OverlayChildLocation.nearestOverlay].

### controller

```dart
OverlayPortalController controller
```

The controller to show, hide and bring to top the overlay child.

### overlayChildBuilder

```dart
WidgetBuilder overlayChildBuilder
```

A [WidgetBuilder] used to build a widget below this widget in the tree, that renders on the closest [Overlay].

The said widget will only be built and shown in the closest [Overlay] once [OverlayPortalController.show] is called on the associated [controller]. It will be painted in front of the [OverlayEntry] closest to this widget in the widget tree (which is usually the enclosing [Route]).

The built overlay child widget is inserted below this widget in the widget tree, allowing it to depend on [InheritedWidget]s above it, and be notified when the [InheritedWidget]s change.

Unlike [child], the built overlay child can visually extend outside the bounds of this widget without being clipped, and receive hit-test events outside of this widget's bounds, as long as it does not extend outside of the [Overlay] on which it is rendered.

### child

```dart
Widget? child
```

A widget below this widget in the tree.

### overlayLocation

```dart
OverlayChildLocation overlayLocation
```

The [Overlay] that the widget returns from [overlayChildBuilder] is attached to.

### createState()

```dart
State<OverlayPortal> createState()
```
