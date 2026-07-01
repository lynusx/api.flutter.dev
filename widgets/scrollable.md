@docImport 'package:flutter/material.dart';

@docImport 'page_storage.dart'; @docImport 'page_view.dart'; @docImport 'scroll_metrics.dart'; @docImport 'scroll_notification.dart'; @docImport 'scroll_view.dart'; @docImport 'single_child_scroll_view.dart'; @docImport 'two_dimensional_scroll_view.dart'; @docImport 'two_dimensional_viewport.dart';

# ViewportBuilder

```dart
typedef ViewportBuilder = Widget Function(BuildContext context, ViewportOffset position)
```

Signature used by [Scrollable] to build the viewport through which the scrollable content is displayed.

# TwoDimensionalViewportBuilder

```dart
typedef TwoDimensionalViewportBuilder = Widget Function(BuildContext context, ViewportOffset verticalPosition, ViewportOffset horizontalPosition)
```

Signature used by [TwoDimensionalScrollable] to build the viewport through which the scrollable content is displayed.

# Scrollable

```dart
class Scrollable extends StatefulWidget {}
```

A widget that manages scrolling in one dimension and informs the [Viewport] through which the content is viewed.

[Scrollable] implements the interaction model for a scrollable widget, including gesture recognition, but does not have an opinion about how the viewport, which actually displays the children, is constructed.

It's rare to construct a [Scrollable] directly. Instead, consider [ListView] or [GridView], which combine scrolling, viewporting, and a layout model. To combine layout models (or to use a custom layout mode), consider using [CustomScrollView].

The static [Scrollable.of] and [Scrollable.ensureVisible] functions are often used to interact with the [Scrollable] widget inside a [ListView] or a [GridView].

To further customize scrolling behavior with a [Scrollable]:

1.  You can provide a [viewportBuilder] to customize the child model. For example, [SingleChildScrollView] uses a viewport that displays a single box child whereas [CustomScrollView] uses a [Viewport] or a [ShrinkWrappingViewport], both of which display a list of slivers.

2.  You can provide a custom [ScrollController] that creates a custom [ScrollPosition] subclass. For example, [PageView] uses a [PageController], which creates a page-oriented scroll position subclass that keeps the same page visible when the [Scrollable] resizes.

## Persisting the scroll position during a session

Scrollables attempt to persist their scroll position using [PageStorage]. This can be disabled by setting [ScrollController.keepScrollOffset] to false on the [controller]. If it is enabled, using a [PageStorageKey] for the [key] of this widget (or one of its ancestors, e.g. a [ScrollView]) is recommended to help disambiguate different [Scrollable]s from each other.

See also:

- [ListView], which is a commonly used [ScrollView] that displays a scrolling, linear list of child widgets.
- [PageView], which is a scrolling list of child widgets that are each the size of the viewport.
- [GridView], which is a [ScrollView] that displays a scrolling, 2D array of child widgets.
- [CustomScrollView], which is a [ScrollView] that creates custom scroll effects using slivers.
- [SingleChildScrollView], which is a scrollable widget that has a single child.
- [ScrollNotification] and [NotificationListener], which can be used to watch the scroll position without using a [ScrollController].

### Scrollable()

```dart
Scrollable({dynamic key, AxisDirection axisDirection = AxisDirection.down, ScrollController? controller, ScrollPhysics? physics, required ViewportBuilder viewportBuilder, ScrollIncrementCalculator? incrementCalculator, bool excludeFromSemantics = false, int? semanticChildCount, DragStartBehavior dragStartBehavior = DragStartBehavior.start, String? restorationId, ScrollBehavior? scrollBehavior, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque})
```

Creates a widget that scrolls.

### axisDirection

```dart
AxisDirection axisDirection
```

{@template flutter.widgets.Scrollable.axisDirection} The direction in which this widget scrolls.

For example, if the [Scrollable.axisDirection] is [AxisDirection.down], increasing the scroll position will cause content below the bottom of the viewport to become visible through the viewport. Similarly, if the axisDirection is [AxisDirection.right], increasing the scroll position will cause content beyond the right edge of the viewport to become visible through the viewport.

Defaults to [AxisDirection.down]. {@endtemplate}

### controller

```dart
ScrollController? controller
```

{@template flutter.widgets.Scrollable.controller} An object that can be used to control the position to which this widget is scrolled.

A [ScrollController] serves several purposes. It can be used to control the initial scroll position (see [ScrollController.initialScrollOffset]). It can be used to control whether the scroll view should automatically save and restore its scroll position in the [PageStorage] (see [ScrollController.keepScrollOffset]). It can be used to read the current scroll position (see [ScrollController.offset]), or change it (see [ScrollController.animateTo]).

If null, a [ScrollController] will be created internally by [Scrollable] in order to create and manage the [ScrollPosition].

See also:

- [Scrollable.ensureVisible], which animates the scroll position to reveal a given [BuildContext]. {@endtemplate}

### physics

```dart
ScrollPhysics? physics
```

{@template flutter.widgets.Scrollable.physics} How the widgets should respond to user input.

For example, determines how the widget continues to animate after the user stops dragging the scroll view.

Defaults to matching platform conventions via the physics provided from the ambient [ScrollConfiguration].

If an explicit [ScrollBehavior] is provided to [Scrollable.scrollBehavior], the [ScrollPhysics] provided by that behavior will take precedence after [Scrollable.physics].

The physics can be changed dynamically, but new physics will only take effect if the _class_ of the provided object changes. Merely constructing a new instance with a different configuration is insufficient to cause the physics to be reapplied. (This is because the final object used is generated dynamically, which can be relatively expensive, and it would be inefficient to speculatively create this object each frame to see if the physics should be updated.)

See also:

- [AlwaysScrollableScrollPhysics], which can be used to indicate that the scrollable should react to scroll requests (and possible overscroll) even if the scrollable's contents fit without scrolling being necessary. {@endtemplate}

### viewportBuilder

```dart
ViewportBuilder viewportBuilder
```

Builds the viewport through which the scrollable content is displayed.

A typical viewport uses the given [ViewportOffset] to determine which part of its content is actually visible through the viewport.

See also:

- [Viewport], which is a viewport that displays a list of slivers.
- [ShrinkWrappingViewport], which is a viewport that displays a list of slivers and sizes itself based on the size of the slivers.

### incrementCalculator

```dart
ScrollIncrementCalculator? incrementCalculator
```

{@template flutter.widgets.Scrollable.incrementCalculator} An optional function that will be called to calculate the distance to scroll when the scrollable is asked to scroll via the keyboard using a [ScrollAction].

If not supplied, the [Scrollable] will scroll a default amount when a keyboard navigation key is pressed (e.g. pageUp/pageDown, control-upArrow, etc.), or otherwise invoked by a [ScrollAction].

If [incrementCalculator] is null, the default for [ScrollIncrementType.page] is 80% of the size of the scroll window, and for [ScrollIncrementType.line], 50 logical pixels. {@endtemplate}

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

{@template flutter.widgets.scrollable.excludeFromSemantics} Whether the scroll actions introduced by this [Scrollable] are exposed in the semantics tree.

Text fields with an overflow are usually scrollable to make sure that the user can get to the beginning/end of the entered text. However, these scrolling actions are generally not exposed to the semantics layer. {@endtemplate}

See also:

- [GestureDetector.excludeFromSemantics], which is used to accomplish the exclusion.

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@template flutter.widgets.scrollable.hitTestBehavior} Defines the behavior of gesture detector used in this [Scrollable].

This defaults to [HitTestBehavior.opaque] which means it prevents targets behind this [Scrollable] from receiving events. {@endtemplate}

See also:

- [HitTestBehavior], for an explanation on different behaviors.

### semanticChildCount

```dart
int? semanticChildCount
```

The number of children that will contribute semantic information.

The value will be null if the number of children is unknown or unbounded.

Some subtypes of [ScrollView] can infer this value automatically. For example [ListView] will use the number of widgets in the child list, while the [ListView.separated] constructor will use half that amount.

For [CustomScrollView] and other types which do not receive a builder or list of widgets, the child count must be explicitly provided.

See also:

- [CustomScrollView], for an explanation of scroll semantics.
- [SemanticsConfiguration.scrollChildCount], the corresponding semantics property.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@template flutter.widgets.scrollable.dragStartBehavior} Determines the way that drag start behavior is handled.

If set to [DragStartBehavior.start], scrolling drag behavior will begin at the position where the drag gesture won the arena. If set to [DragStartBehavior.down] it will begin at the position where a down event is first detected.

In general, setting this to [DragStartBehavior.start] will make drag animation smoother and setting it to [DragStartBehavior.down] will make drag behavior feel slightly more reactive.

By default, the drag start behavior is [DragStartBehavior.start].

See also:

- [DragGestureRecognizer.dragStartBehavior], which gives an example for the different behaviors.

{@endtemplate}

### restorationId

```dart
String? restorationId
```

{@template flutter.widgets.scrollable.restorationId} Restoration ID to save and restore the scroll offset of the scrollable.

If a restoration id is provided, the scrollable will persist its current scroll offset and restore it during state restoration.

The scroll offset is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter. {@endtemplate}

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@template flutter.widgets.scrollable.scrollBehavior} A [ScrollBehavior] that will be applied to this widget individually.

Defaults to null, wherein the inherited [ScrollBehavior] is copied and modified to alter the viewport decoration, like [Scrollbar]s.

[ScrollBehavior]s also provide [ScrollPhysics]. If an explicit [ScrollPhysics] is provided in [physics], it will take precedence, followed by [scrollBehavior], and then the inherited ancestor [ScrollBehavior]. {@endtemplate}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

This is passed to decorators in [ScrollableDetails], and does not directly affect clipping of the [Scrollable]. This reflects the same [Clip] that is provided to [ScrollView.clipBehavior] and is supplied to the [Viewport].

### axis

```dart
Axis get axis
```

The axis along which the scroll view scrolls.

Determined by the [axisDirection].

### createState()

```dart
ScrollableState createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### maybeOf()

```dart
ScrollableState? maybeOf(BuildContext context, {Axis? axis})
```

The state from the closest instance of this class that encloses the given context, or null if none is found.

Typical usage is as follows:

```dart
ScrollableState? scrollable = Scrollable.maybeOf(context);
```

Calling this method will create a dependency on the [ScrollableState] that is returned, if there is one. This is typically the closest [Scrollable], but may be a more distant ancestor if [axis] is used to target a specific [Scrollable].

Using the optional [Axis] is useful when Scrollables are nested and the target [Scrollable] is not the closest instance. When [axis] is provided, the nearest enclosing [ScrollableState] in that [Axis] is returned, or null if there is none.

This finds the nearest _ancestor_ [Scrollable] of the `context`. This means that if the `context` is that of a [Scrollable], it will _not_ find _that_ [Scrollable].

See also:

- [Scrollable.of], which is similar to this method, but asserts if no [Scrollable] ancestor is found.

### of()

```dart
ScrollableState of(BuildContext context, {Axis? axis})
```

The state from the closest instance of this class that encloses the given context.

Typical usage is as follows:

```dart
ScrollableState scrollable = Scrollable.of(context);
```

Calling this method will create a dependency on the [ScrollableState] that is returned, if there is one. This is typically the closest [Scrollable], but may be a more distant ancestor if [axis] is used to target a specific [Scrollable].

Using the optional [Axis] is useful when Scrollables are nested and the target [Scrollable] is not the closest instance. When [axis] is provided, the nearest enclosing [ScrollableState] in that [Axis] is returned.

This finds the nearest _ancestor_ [Scrollable] of the `context`. This means that if the `context` is that of a [Scrollable], it will _not_ find _that_ [Scrollable].

If no [Scrollable] ancestor is found, then this method will assert in debug mode, and throw an exception in release mode.

See also:

- [Scrollable.maybeOf], which is similar to this method, but returns null if no [Scrollable] ancestor is found.

### recommendDeferredLoadingForContext()

```dart
bool recommendDeferredLoadingForContext(BuildContext context, {Axis? axis})
```

Provides a heuristic to determine if expensive frame-bound tasks should be deferred for the [context] at a specific point in time.

Calling this method does _not_ create a dependency on any other widget. This also means that the value returned is only good for the point in time when it is called, and callers will not get updated if the value changes.

The heuristic used is determined by the [physics] of this [Scrollable] via [ScrollPhysics.recommendDeferredLoading]. That method is called with the current [ScrollPosition.activity]'s [ScrollActivity.velocity].

The optional [Axis] allows targeting of a specific [Scrollable] of that axis, useful when Scrollables are nested. When [axis] is provided, [ScrollPosition.recommendDeferredLoading] is called for the nearest [Scrollable] in that [Axis].

If there is no [Scrollable] in the widget tree above the [context], this method returns false.

### ensureVisible()

```dart
Future<void> ensureVisible(BuildContext context, {double alignment = 0.0, Duration duration = Duration.zero, Curve curve = Curves.ease, ScrollPositionAlignmentPolicy alignmentPolicy = ScrollPositionAlignmentPolicy.explicit})
```

Scrolls all scrollables that enclose the given context so as to make the given context visible.

If a [Scrollable] enclosing the provided [BuildContext] is a [TwoDimensionalScrollable], both vertical and horizontal axes will ensure the target is made visible.

# ScrollableState

```dart
class ScrollableState extends State<Scrollable> with TickerProviderStateMixin, RestorationMixin implements ScrollContext {}
```

State object for a [Scrollable] widget.

To manipulate a [Scrollable] widget's scroll position, use the object obtained from the [position] property.

To be informed of when a [Scrollable] widget is scrolling, use a [NotificationListener] to listen for [ScrollNotification] notifications.

This class is not intended to be subclassed. To specialize the behavior of a [Scrollable], provide it with a [ScrollPhysics].

### position

```dart
ScrollPosition get position
```

The manager for this [Scrollable] widget's viewport position.

To control what kind of [ScrollPosition] is created for a [Scrollable], provide it with custom [ScrollController] that creates the appropriate [ScrollPosition] in its [ScrollController.createScrollPosition] method.

### resolvedPhysics

```dart
ScrollPhysics? get resolvedPhysics
```

The resolved [ScrollPhysics] of the [ScrollableState].

### deltaToScrollOrigin

```dart
Offset get deltaToScrollOrigin
```

An [Offset] that represents the absolute distance from the origin, or 0, of the [ScrollPosition] expressed in the associated [Axis].

Used by [EdgeDraggingAutoScroller] to progress the position forward when a drag gesture reaches the edge of the [Viewport].

### axisDirection

```dart
AxisDirection get axisDirection
```

### vsync

```dart
TickerProvider get vsync
```

### devicePixelRatio

```dart
double get devicePixelRatio
```

### notificationContext

```dart
BuildContext? get notificationContext
```

### storageContext

```dart
BuildContext get storageContext
```

### restorationId

```dart
String? get restorationId
```

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

### saveOffset()

```dart
void saveOffset(double offset)
```

### initState()

```dart
void initState()
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(Scrollable oldWidget)
```

### dispose()

```dart
void dispose()
```

### setSemanticsActions()

```dart
void setSemanticsActions(Set<SemanticsAction> actions)
```

### setCanDrag()

```dart
void setCanDrag(bool value)
```

### setIgnorePointer()

```dart
void setIgnorePointer(bool value)
```

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DiagonalDragBehavior

```dart
enum DiagonalDragBehavior {}
```

Specifies how to configure the [DragGestureRecognizer]s of a [TwoDimensionalScrollable].

This behavior will not allow for any diagonal scrolling.

Drag gestures in one direction or the other will lock the input axis until the gesture is released.

This behavior will only allow diagonal scrolling on a weighted scale per gesture event.

This means that after initially evaluating the drag gesture, the weighted evaluation (based on [kTouchSlop]) stands until the gesture is released.

This behavior will only allow diagonal scrolling on a weighted scale that is evaluated throughout a gesture event.

This means that during each update to the drag gesture, the scrolling axis will be allowed to scroll diagonally if it exceeds the [kTouchSlop].

This behavior allows free movement in any and all directions when dragging.

# TwoDimensionalScrollable

```dart
class TwoDimensionalScrollable extends StatefulWidget {}
```

A widget that manages scrolling in both the vertical and horizontal dimensions and informs the [TwoDimensionalViewport] through which the content is viewed.

[TwoDimensionalScrollable] implements the interaction model for a scrollable widget in both the vertical and horizontal axes, including gesture recognition, but does not have an opinion about how the [TwoDimensionalViewport], which actually displays the children, is constructed.

It's rare to construct a [TwoDimensionalScrollable] directly. Instead, consider subclassing [TwoDimensionalScrollView], which combines scrolling, viewporting, and a layout model in both dimensions.

See also:

- [TwoDimensionalScrollView], an abstract base class for displaying a scrolling array of children in both directions.
- [TwoDimensionalViewport], which can be used to customize the child layout model.

### TwoDimensionalScrollable()

```dart
TwoDimensionalScrollable({dynamic key, required ScrollableDetails horizontalDetails, required ScrollableDetails verticalDetails, required TwoDimensionalViewportBuilder viewportBuilder, ScrollIncrementCalculator? incrementCalculator, String? restorationId, bool excludeFromSemantics = false, DiagonalDragBehavior diagonalDragBehavior = DiagonalDragBehavior.none, DragStartBehavior dragStartBehavior = DragStartBehavior.start, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque})
```

Creates a widget that scrolls in two dimensions.

The [horizontalDetails], [verticalDetails], and [viewportBuilder] must not be null.

### diagonalDragBehavior

```dart
DiagonalDragBehavior diagonalDragBehavior
```

How scrolling gestures should lock to one axis, or allow free movement in both axes.

### horizontalDetails

```dart
ScrollableDetails horizontalDetails
```

The configuration of the horizontal [Scrollable].

These [ScrollableDetails] can be used to set the [AxisDirection], [ScrollController], [ScrollPhysics] and more for the horizontal axis.

### verticalDetails

```dart
ScrollableDetails verticalDetails
```

The configuration of the vertical [Scrollable].

These [ScrollableDetails] can be used to set the [AxisDirection], [ScrollController], [ScrollPhysics] and more for the vertical axis.

### viewportBuilder

```dart
TwoDimensionalViewportBuilder viewportBuilder
```

Builds the viewport through which the scrollable content is displayed.

A [TwoDimensionalViewport] uses two given [ViewportOffset]s to determine which part of its content is actually visible through the viewport.

See also:

- [TwoDimensionalViewport], which is a viewport that displays a span of widgets in both dimensions.

### incrementCalculator

```dart
ScrollIncrementCalculator? incrementCalculator
```

{@macro flutter.widgets.Scrollable.incrementCalculator}

This value applies in both axes.

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

Internally, the [TwoDimensionalScrollable] will introduce a [RestorationScope] that will be assigned this value. The two [Scrollable]s within will then be given unique IDs within this scope.

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

{@macro flutter.widgets.scrollable.excludeFromSemantics}

This value applies to both axes.

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

This value applies to both axes.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

This value applies in both axes.

### createState()

```dart
State<TwoDimensionalScrollable> createState()
```

### maybeOf()

```dart
TwoDimensionalScrollableState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context, or null if none is found.

Typical usage is as follows:

```dart
TwoDimensionalScrollableState? scrollable = TwoDimensionalScrollable.maybeOf(context);
```

Calling this method will create a dependency on the closest [TwoDimensionalScrollable] in the [context]. The internal [Scrollable]s can be accessed through [TwoDimensionalScrollableState.verticalScrollable] and [TwoDimensionalScrollableState.horizontalScrollable].

Alternatively, [Scrollable.maybeOf] can be used by providing the desired [Axis] to the `axis` parameter.

See also:

- [TwoDimensionalScrollable.of], which is similar to this method, but asserts if no [Scrollable] ancestor is found.

### of()

```dart
TwoDimensionalScrollableState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

Typical usage is as follows:

```dart
TwoDimensionalScrollableState scrollable = TwoDimensionalScrollable.of(context);
```

Calling this method will create a dependency on the closest [TwoDimensionalScrollable] in the [context]. The internal [Scrollable]s can be accessed through [TwoDimensionalScrollableState.verticalScrollable] and [TwoDimensionalScrollableState.horizontalScrollable].

If no [TwoDimensionalScrollable] ancestor is found, then this method will assert in debug mode, and throw an exception in release mode.

Alternatively, [Scrollable.of] can be used by providing the desired [Axis] to the `axis` parameter.

See also:

- [TwoDimensionalScrollable.maybeOf], which is similar to this method, but returns null if no [TwoDimensionalScrollable] ancestor is found.

# TwoDimensionalScrollableState

```dart
class TwoDimensionalScrollableState extends State<TwoDimensionalScrollable> {}
```

State object for a [TwoDimensionalScrollable] widget.

To manipulate one of the internal [Scrollable] widget's scroll position, use the object obtained from the [verticalScrollable] or [horizontalScrollable] property.

To be informed of when a [TwoDimensionalScrollable] widget is scrolling, use a [NotificationListener] to listen for [ScrollNotification]s. Both axes will have the same viewport depth since there is only one viewport, and so should be differentiated by the [Axis] of the [ScrollMetrics] provided by the notification.

### verticalScrollable

```dart
ScrollableState get verticalScrollable
```

The [ScrollableState] of the vertical axis.

Accessible by calling [TwoDimensionalScrollable.of].

Alternatively, [Scrollable.of] can be used by providing [Axis.vertical] to the `axis` parameter.

### horizontalScrollable

```dart
ScrollableState get horizontalScrollable
```

The [ScrollableState] of the horizontal axis.

Accessible by calling [TwoDimensionalScrollable.of].

Alternatively, [Scrollable.of] can be used by providing [Axis.horizontal] to the `axis` parameter.

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(TwoDimensionalScrollable oldWidget)
```

### build()

```dart
Widget build(BuildContext context)
```

### dispose()

```dart
void dispose()
```
