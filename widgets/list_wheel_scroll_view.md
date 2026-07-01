@docImport 'package:flutter/material.dart';

@docImport 'scroll_view.dart'; @docImport 'viewport.dart';

# ChangeReportingBehavior

```dart
enum ChangeReportingBehavior {}
```

The behavior of reporting the selected item index in a [ListWheelScrollView].

This determines when the `onSelectedItemChanged` callback is called.

Report the selected item index only when the scroll view stops scrolling.

Report the selected item index on every scroll update.

# ListWheelChildDelegate

```dart
abstract class ListWheelChildDelegate {}
```

A delegate that supplies children for [ListWheelScrollView].

[ListWheelScrollView] lazily constructs its children during layout to avoid creating more children than are visible through the [Viewport]. This delegate is responsible for providing children to [ListWheelScrollView] during that stage.

See also:

- [ListWheelChildListDelegate], a delegate that supplies children using an explicit list.
- [ListWheelChildLoopingListDelegate], a delegate that supplies infinite children by looping an explicit list.
- [ListWheelChildBuilderDelegate], a delegate that supplies children using a builder callback.

### build()

```dart
Widget? build(BuildContext context, int index)
```

Return the child at the given index. If the child at the given index does not exist, return null.

### estimatedChildCount

```dart
int? get estimatedChildCount
```

Returns an estimate of the number of children this delegate will build.

### trueIndexOf()

```dart
int trueIndexOf(int index)
```

Returns the true index for a child built at a given index. Defaults to the given index, however if the delegate is [ListWheelChildLoopingListDelegate], this value is the index of the true element that the delegate is looping to.

Example: [ListWheelChildLoopingListDelegate] is built by looping a list of length 8. Then, trueIndexOf(10) = 2 and trueIndexOf(-5) = 3.

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildDelegate oldDelegate)
```

Called to check whether this and the old delegate are actually 'different', so that the caller can decide to rebuild or not.

# ListWheelChildListDelegate

```dart
class ListWheelChildListDelegate extends ListWheelChildDelegate {}
```

A delegate that supplies children for [ListWheelScrollView] using an explicit list.

[ListWheelScrollView] lazily constructs its children to avoid creating more children than are visible through the [Viewport]. This delegate provides children using an explicit list, which is convenient but reduces the benefit of building children lazily.

In general building all the widgets in advance is not efficient. It is better to create a delegate that builds them on demand using [ListWheelChildBuilderDelegate] or by subclassing [ListWheelChildDelegate] directly.

This class is provided for the cases where either the list of children is known well in advance (ideally the children are themselves compile-time constants, for example), and therefore will not be built each time the delegate itself is created, or the list is small, such that it's likely always visible (and thus there is nothing to be gained by building it on demand). For example, the body of a dialog box might fit both of these conditions.

### ListWheelChildListDelegate()

```dart
ListWheelChildListDelegate({required List<Widget> children})
```

Constructs the delegate from a concrete list of children.

### children

```dart
List<Widget> children
```

The list containing all children that can be supplied.

### estimatedChildCount

```dart
int get estimatedChildCount
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildListDelegate oldDelegate)
```

# ListWheelChildLoopingListDelegate

```dart
class ListWheelChildLoopingListDelegate extends ListWheelChildDelegate {}
```

A delegate that supplies infinite children for [ListWheelScrollView] by looping an explicit list.

[ListWheelScrollView] lazily constructs its children to avoid creating more children than are visible through the [Viewport]. This delegate provides children using an explicit list, which is convenient but reduces the benefit of building children lazily.

In general building all the widgets in advance is not efficient. It is better to create a delegate that builds them on demand using [ListWheelChildBuilderDelegate] or by subclassing [ListWheelChildDelegate] directly.

This class is provided for the cases where either the list of children is known well in advance (ideally the children are themselves compile-time constants, for example), and therefore will not be built each time the delegate itself is created, or the list is small, such that it's likely always visible (and thus there is nothing to be gained by building it on demand). For example, the body of a dialog box might fit both of these conditions.

### ListWheelChildLoopingListDelegate()

```dart
ListWheelChildLoopingListDelegate({required List<Widget> children})
```

Constructs the delegate from a concrete list of children.

### children

```dart
List<Widget> children
```

The list containing all children that can be supplied.

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### trueIndexOf()

```dart
int trueIndexOf(int index)
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildLoopingListDelegate oldDelegate)
```

# ListWheelChildBuilderDelegate

```dart
class ListWheelChildBuilderDelegate extends ListWheelChildDelegate {}
```

A delegate that supplies children for [ListWheelScrollView] using a builder callback.

[ListWheelScrollView] lazily constructs its children to avoid creating more children than are visible through the [Viewport]. This delegate provides children using an [IndexedWidgetBuilder] callback, so that the children do not have to be built until they are displayed.

### ListWheelChildBuilderDelegate()

```dart
ListWheelChildBuilderDelegate({required NullableIndexedWidgetBuilder builder, int? childCount})
```

Constructs the delegate from a builder callback.

### builder

```dart
NullableIndexedWidgetBuilder builder
```

Called lazily to build children.

### childCount

```dart
int? childCount
```

{@template flutter.widgets.ListWheelChildBuilderDelegate.childCount} If non-null, [childCount] is the maximum number of children that can be provided, and children are available from 0 to [childCount] - 1.

If null, then the lower and upper limit are not known. However the [builder] must provide children for a contiguous segment. If the builder returns null at some index, the segment terminates there. {@endtemplate}

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildBuilderDelegate oldDelegate)
```

# FixedExtentScrollController

```dart
class FixedExtentScrollController extends ScrollController {}
```

A controller for scroll views whose items have the same size.

Similar to a standard [ScrollController] but with the added convenience mechanisms to read and go to item indices rather than a raw pixel scroll offset.

See also:

- [ListWheelScrollView], a scrollable view widget with fixed size items that this widget controls.
- [FixedExtentMetrics], the `metrics` property exposed by [ScrollNotification] from [ListWheelScrollView] which can be used to listen to the current item index on a push basis rather than polling the [FixedExtentScrollController].

### FixedExtentScrollController()

```dart
FixedExtentScrollController({int initialItem = 0, bool keepScrollOffset, String? debugLabel, void Function(ScrollPosition)? onAttach, void Function(ScrollPosition)? onDetach})
```

Creates a scroll controller for scrollables whose items have the same size.

[initialItem] defaults to zero.

### initialItem

```dart
int initialItem
```

The page to show when first creating the scroll view.

Defaults to zero.

### selectedItem

```dart
int get selectedItem
```

The currently selected item index that's closest to the center of the viewport.

There are circumstances that this [FixedExtentScrollController] can't know the current item. Reading [selectedItem] will throw an [AssertionError] in the following cases:

1.  No scroll view is currently using this [FixedExtentScrollController].
2.  More than one scroll views using the same [FixedExtentScrollController].

The [hasClients] property can be used to check if a scroll view is attached prior to accessing [selectedItem].

### animateToItem()

```dart
Future<void> animateToItem(int itemIndex, {required Duration duration, required Curve curve})
```

Animates the controlled scroll view to the given item index.

The animation lasts for the given duration and follows the given curve. The returned [Future] resolves when the animation completes.

### jumpToItem()

```dart
void jumpToItem(int itemIndex)
```

Changes which item index is centered in the controlled scroll view.

Jumps the item index position from its current value to the given value, without animation, and without checking if the new value is in range.

### createScrollPosition()

```dart
ScrollPosition createScrollPosition(ScrollPhysics physics, ScrollContext context, ScrollPosition? oldPosition)
```

# FixedExtentMetrics

```dart
class FixedExtentMetrics extends FixedScrollMetrics {}
```

Metrics for a [ScrollPosition] to a scroll view with fixed item sizes.

The metrics are available on [ScrollNotification]s generated from a scroll views such as [ListWheelScrollView]s with a [FixedExtentScrollController] and exposes the current [itemIndex] and the scroll view's extents.

`FixedExtent` refers to the fact that the scrollable items have the same size. This is distinct from `Fixed` in the parent class name's [FixedScrollMetrics] which refers to its immutability.

### FixedExtentMetrics()

```dart
FixedExtentMetrics({required double? minScrollExtent, required double? maxScrollExtent, required double? pixels, required double? viewportDimension, required dynamic axisDirection, required int itemIndex, required double devicePixelRatio})
```

Creates an immutable snapshot of values associated with a [ListWheelScrollView].

### copyWith()

```dart
FixedExtentMetrics copyWith({double? minScrollExtent, double? maxScrollExtent, double? pixels, double? viewportDimension, AxisDirection? axisDirection, int? itemIndex, double? devicePixelRatio})
```

### itemIndex

```dart
int itemIndex
```

The scroll view's currently selected item index.

# FixedExtentScrollPhysics

```dart
class FixedExtentScrollPhysics extends ScrollPhysics {}
```

A snapping physics that always lands directly on items instead of anywhere within the scroll extent.

Behaves similarly to a slot machine wheel except the ballistics simulation never overshoots and rolls back within a single item if it's to settle on that item.

Must be used with a scrollable that uses a [FixedExtentScrollController].

Defers back to the parent beyond the scroll extents.

### FixedExtentScrollPhysics()

```dart
FixedExtentScrollPhysics({ScrollPhysics? parent})
```

Creates a scroll physics that always lands on items.

### applyTo()

```dart
FixedExtentScrollPhysics applyTo(ScrollPhysics? ancestor)
```

### createBallisticSimulation()

```dart
Simulation? createBallisticSimulation(ScrollMetrics position, double velocity)
```

# ListWheelScrollView

```dart
class ListWheelScrollView extends StatefulWidget {}
```

A box in which children on a wheel can be scrolled.

This widget is similar to a [ListView] but with the restriction that all children must be the same size along the scrolling axis.

{@youtube 560 315 https://www.youtube.com/watch?v=dUhmWAz4C7Y}

When the list is at the zero scroll offset, the first child is aligned with the middle of the viewport. When the list is at the final scroll offset, the last child is aligned with the middle of the viewport.

The children are rendered as if rotating on a wheel instead of scrolling on a plane.

### ListWheelScrollView()

```dart
ListWheelScrollView({dynamic key, ScrollController? controller, ScrollPhysics? physics, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, ValueChanged<int>? onSelectedItemChanged, bool renderChildrenOutsideViewport = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required List<Widget> children})
```

Constructs a list in which children are scrolled a wheel. Its children are passed to a delegate and lazily built during layout.

### ListWheelScrollView.useDelegate()

```dart
ListWheelScrollView.useDelegate({dynamic key, ScrollController? controller, ScrollPhysics? physics, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, ValueChanged<int>? onSelectedItemChanged, bool renderChildrenOutsideViewport = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required ListWheelChildDelegate childDelegate})
```

Constructs a list in which children are scrolled a wheel. Its children are managed by a delegate and are lazily built during layout.

### controller

```dart
ScrollController? controller
```

Typically a [FixedExtentScrollController] used to control the current item.

A [FixedExtentScrollController] can be used to read the currently selected/centered child item and can be used to change the current item.

If none is provided, a new [FixedExtentScrollController] is implicitly created.

If a [ScrollController] is used instead of [FixedExtentScrollController], [ScrollNotification.metrics] will no longer provide [FixedExtentMetrics] to indicate the current item index and [onSelectedItemChanged] will not work.

To read the current selected item only when the value changes, use [onSelectedItemChanged].

### physics

```dart
ScrollPhysics? physics
```

How the scroll view should respond to user input.

For example, determines how the scroll view continues to animate after the user stops dragging the scroll view.

If an explicit [ScrollBehavior] is provided to [scrollBehavior], the [ScrollPhysics] provided by that behavior will take precedence after [physics].

Defaults to matching platform conventions.

### diameterRatio

```dart
double diameterRatio
```

{@macro flutter.rendering.RenderListWheelViewport.diameterRatio}

### perspective

```dart
double perspective
```

{@macro flutter.rendering.RenderListWheelViewport.perspective}

### offAxisFraction

```dart
double offAxisFraction
```

{@macro flutter.rendering.RenderListWheelViewport.offAxisFraction}

### useMagnifier

```dart
bool useMagnifier
```

{@macro flutter.rendering.RenderListWheelViewport.useMagnifier}

### magnification

```dart
double magnification
```

{@macro flutter.rendering.RenderListWheelViewport.magnification}

### overAndUnderCenterOpacity

```dart
double overAndUnderCenterOpacity
```

{@macro flutter.rendering.RenderListWheelViewport.overAndUnderCenterOpacity}

### itemExtent

```dart
double itemExtent
```

Size of each child in the main axis.

Must be positive.

### squeeze

```dart
double squeeze
```

{@macro flutter.rendering.RenderListWheelViewport.squeeze}

Defaults to 1.

### onSelectedItemChanged

```dart
ValueChanged<int>? onSelectedItemChanged
```

On optional listener that's called when the centered item changes.

### renderChildrenOutsideViewport

```dart
bool renderChildrenOutsideViewport
```

{@macro flutter.rendering.RenderListWheelViewport.renderChildrenOutsideViewport}

### childDelegate

```dart
ListWheelChildDelegate childDelegate
```

A delegate that helps lazily instantiating child.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

Defaults to [HitTestBehavior.opaque].

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.widgets.scrollable.scrollBehavior}

The [ScrollBehavior] of the inherited [ScrollConfiguration] will be modified by default to not apply a [Scrollbar].

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### changeReportingBehavior

```dart
ChangeReportingBehavior changeReportingBehavior
```

The behavior of reporting the selected item index.

This determines when the [onSelectedItemChanged] callback is called. Defaults to [ChangeReportingBehavior.onScrollUpdate].

### createState()

```dart
State<ListWheelScrollView> createState()
```

# ListWheelElement

```dart
class ListWheelElement extends RenderObjectElement implements ListWheelChildManager {}
```

Element that supports building children lazily for [ListWheelViewport].

### ListWheelElement()

```dart
ListWheelElement(ListWheelViewport widget)
```

Creates an element that lazily builds children for the given widget.

### renderObject

```dart
RenderListWheelViewport get renderObject
```

### update()

```dart
void update(ListWheelViewport newWidget)
```

### childCount

```dart
int? get childCount
```

### performRebuild()

```dart
void performRebuild()
```

### retrieveWidget()

```dart
Widget? retrieveWidget(int index)
```

Asks the underlying delegate for a widget at the given index.

Normally the builder is only called once for each index and the result will be cached. However when the element is rebuilt, the cache will be cleared.

### childExistsAt()

```dart
bool childExistsAt(int index)
```

### createChild()

```dart
void createChild(int index, {required RenderBox? after})
```

### removeChild()

```dart
void removeChild(RenderBox child)
```

### updateChild()

```dart
Element? updateChild(Element? child, Widget? newWidget, Object? newSlot)
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, int slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, int oldSlot, int newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, int slot)
```

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

# ListWheelViewport

```dart
class ListWheelViewport extends RenderObjectWidget {}
```

A viewport showing a subset of children on a wheel.

Typically used with [ListWheelScrollView], this viewport is similar to [Viewport] in that it shows a subset of children in a scrollable based on the scrolling offset and the children's dimensions. But uses [RenderListWheelViewport] to display the children on a wheel.

See also:

- [ListWheelScrollView], widget that combines this viewport with a scrollable.
- [RenderListWheelViewport], the render object that renders the children on a wheel.

### ListWheelViewport()

```dart
ListWheelViewport({dynamic key, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, bool renderChildrenOutsideViewport = false, required ViewportOffset offset, required ListWheelChildDelegate childDelegate, Clip clipBehavior = Clip.hardEdge})
```

Creates a viewport where children are rendered onto a wheel.

The [diameterRatio] argument defaults to 2.

The [perspective] argument defaults to 0.003.

The [itemExtent] argument in pixels must be provided and must be positive.

The [clipBehavior] argument defaults to [Clip.hardEdge].

The [renderChildrenOutsideViewport] argument defaults to false and must not be null.

The [offset] argument must be provided.

### diameterRatio

```dart
double diameterRatio
```

{@macro flutter.rendering.RenderListWheelViewport.diameterRatio}

### perspective

```dart
double perspective
```

{@macro flutter.rendering.RenderListWheelViewport.perspective}

### offAxisFraction

```dart
double offAxisFraction
```

{@macro flutter.rendering.RenderListWheelViewport.offAxisFraction}

### useMagnifier

```dart
bool useMagnifier
```

{@macro flutter.rendering.RenderListWheelViewport.useMagnifier}

### magnification

```dart
double magnification
```

{@macro flutter.rendering.RenderListWheelViewport.magnification}

### overAndUnderCenterOpacity

```dart
double overAndUnderCenterOpacity
```

{@macro flutter.rendering.RenderListWheelViewport.overAndUnderCenterOpacity}

### itemExtent

```dart
double itemExtent
```

{@macro flutter.rendering.RenderListWheelViewport.itemExtent}

### squeeze

```dart
double squeeze
```

{@macro flutter.rendering.RenderListWheelViewport.squeeze}

Defaults to 1.

### renderChildrenOutsideViewport

```dart
bool renderChildrenOutsideViewport
```

{@macro flutter.rendering.RenderListWheelViewport.renderChildrenOutsideViewport}

### offset

```dart
ViewportOffset offset
```

[ViewportOffset] object describing the content that should be visible in the viewport.

### childDelegate

```dart
ListWheelChildDelegate childDelegate
```

A delegate that lazily instantiates children.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### createElement()

```dart
ListWheelElement createElement()
```

### createRenderObject()

```dart
RenderListWheelViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderListWheelViewport renderObject)
```
