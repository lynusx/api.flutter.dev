@docImport 'package:flutter/material.dart';

@docImport 'page_storage.dart'; @docImport 'safe_area.dart'; @docImport 'scrollable.dart';

# NestedScrollViewHeaderSliversBuilder

```dart
typedef NestedScrollViewHeaderSliversBuilder = List<Widget> Function(BuildContext context, bool innerBoxIsScrolled)
```

Signature used by [NestedScrollView] for building its header.

The `innerBoxIsScrolled` argument is typically used to control the [SliverAppBar.forceElevated] property to ensure that the app bar shows a shadow, since it would otherwise not necessarily be aware that it had content ostensibly below it.

# NestedScrollView

```dart
class NestedScrollView extends StatefulWidget {}
```

A scrolling view inside of which can be nested other scrolling views, with their scroll positions being intrinsically linked.

The most common use case for this widget is a scrollable view with a flexible [SliverAppBar] containing a [TabBar] in the header (built by [headerSliverBuilder]), and with a [TabBarView] in the [body], such that the scrollable view's contents vary based on which tab is visible.

## Motivation

In a normal [ScrollView], there is one set of slivers (the components of the scrolling view). If one of those slivers hosted a [TabBarView] which scrolls in the opposite direction (e.g. allowing the user to swipe horizontally between the pages represented by the tabs, while the list scrolls vertically), then any list inside that [TabBarView] would not interact with the outer [ScrollView]. For example, flinging the inner list to scroll to the top would not cause a collapsed [SliverAppBar] in the outer [ScrollView] to expand.

[NestedScrollView] solves this problem by providing custom [ScrollController]s for the outer [ScrollView] and the inner [ScrollView]s (those inside the [TabBarView], hooking them together so that they appear, to the user, as one coherent scroll view.

{@tool dartpad} This example shows a [NestedScrollView] whose header is the combination of a [TabBar] in a [SliverAppBar] and whose body is a [TabBarView]. It uses a [SliverOverlapAbsorber]/[SliverOverlapInjector] pair to make the inner lists align correctly, and it uses [SafeArea] to avoid any horizontal disturbances (e.g. the "notch" on iOS when the phone is horizontal). In addition, [PageStorageKey]s are used to remember the scroll position of each tab's list.

** See code in examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.0.dart ** {@end-tool}

## [SliverAppBar]s with [NestedScrollView]s

Using a [SliverAppBar] in the outer scroll view, or [headerSliverBuilder], of a [NestedScrollView] may require special configurations in order to work as it would if the outer and inner were one single scroll view, like a [CustomScrollView].

### Pinned [SliverAppBar]s

A pinned [SliverAppBar] works in a [NestedScrollView] exactly as it would in another scroll view, like [CustomScrollView]. When using [SliverAppBar.pinned], the app bar remains visible at the top of the scroll view. The app bar can still expand and contract as the user scrolls, but it will remain visible rather than being scrolled out of view.

This works naturally in a [NestedScrollView], as the pinned [SliverAppBar] is not expected to move in or out of the visible portion of the viewport. As the inner or outer [Scrollable]s are moved, the app bar persists as expected.

If the app bar is floating, pinned, and using an expanded height, follow the floating convention laid out below.

### Floating [SliverAppBar]s

When placed in the outer scrollable, or the [headerSliverBuilder], a [SliverAppBar] that floats, using [SliverAppBar.floating] will not be triggered to float over the inner scroll view, or [body], automatically.

This is because a floating app bar uses the scroll offset of its own [Scrollable] to dictate the floating action. Being two separate inner and outer [Scrollable]s, a [SliverAppBar] in the outer header is not aware of changes in the scroll offset of the inner body.

In order to float the outer, use [NestedScrollView.floatHeaderSlivers]. When set to true, the nested scrolling coordinator will prioritize floating in the header slivers before applying the remaining drag to the body.

Furthermore, the `floatHeaderSlivers` flag should also be used when using an app bar that is floating, pinned, and has an expanded height. In this configuration, the flexible space of the app bar will open and collapse, while the primary portion of the app bar remains pinned.

{@tool dartpad} This simple example shows a [NestedScrollView] whose header contains a floating [SliverAppBar]. By using the [floatHeaderSlivers] property, the floating behavior is coordinated between the outer and inner [Scrollable]s, so it behaves as it would in a single scrollable.

** See code in examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.1.dart ** {@end-tool}

### Snapping [SliverAppBar]s

Floating [SliverAppBar]s also have the option to perform a snapping animation. If [SliverAppBar.snap] is true, then a scroll that exposes the floating app bar will trigger an animation that slides the entire app bar into view. Similarly if a scroll dismisses the app bar, the animation will slide the app bar completely out of view.

It is possible with a [NestedScrollView] to perform just the snapping animation without floating the app bar in and out. By not using the [NestedScrollView.floatHeaderSlivers], the app bar will snap in and out without floating.

The [SliverAppBar.snap] animation should be used in conjunction with the [SliverOverlapAbsorber] and [SliverOverlapInjector] widgets when implemented in a [NestedScrollView]. These widgets take any overlapping behavior of the [SliverAppBar] in the header and redirect it to the [SliverOverlapInjector] in the body. If it is missing, then it is possible for the nested "inner" scroll view below to end up under the [SliverAppBar] even when the inner scroll view thinks it has not been scrolled.

{@tool dartpad} This simple example shows a [NestedScrollView] whose header contains a snapping, floating [SliverAppBar]. _Without_ setting any additional flags, e.g [NestedScrollView.floatHeaderSlivers], the [SliverAppBar] will animate in and out without floating. The [SliverOverlapAbsorber] and [SliverOverlapInjector] maintain the proper alignment between the two separate scroll views.

** See code in examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.2.dart ** {@end-tool}

### Snapping and Floating [SliverAppBar]s

Currently, [NestedScrollView] does not support simultaneously floating and snapping the outer scrollable, e.g. when using [SliverAppBar.floating] & [SliverAppBar.snap] at the same time.

### Stretching [SliverAppBar]s

Currently, [NestedScrollView] does not support stretching the outer scrollable, e.g. when using [SliverAppBar.stretch].

See also:

- [SliverAppBar], for examples on different configurations like floating, pinned and snap behaviors.
- [SliverOverlapAbsorber], a sliver that wraps another, forcing its layout extent to be treated as overlap.
- [SliverOverlapInjector], a sliver that has a sliver geometry based on the values stored in a [SliverOverlapAbsorberHandle].

### NestedScrollView()

```dart
NestedScrollView({dynamic key, ScrollController? controller, Axis scrollDirection = Axis.vertical, bool reverse = false, ScrollPhysics? physics, required NestedScrollViewHeaderSliversBuilder headerSliverBuilder, required Widget body, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool floatHeaderSlivers = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior})
```

Creates a nested scroll view.

The [reverse], [headerSliverBuilder], and [body] arguments must not be null.

### controller

```dart
ScrollController? controller
```

An object that can be used to control the position to which the outer scroll view is scrolled.

### scrollDirection

```dart
Axis scrollDirection
```

{@macro flutter.widgets.scroll_view.scrollDirection}

This property only applies to the [Axis] of the outer scroll view, composed of the slivers returned from [headerSliverBuilder]. Since the inner scroll view is not directly configured by the [NestedScrollView], for the axes to match, configure the scroll view of the [body] the same way if they are expected to scroll in the same orientation. This allows for flexible configurations of the NestedScrollView.

### reverse

```dart
bool reverse
```

Whether the scroll view scrolls in the reading direction.

For example, if the reading direction is left-to-right and [scrollDirection] is [Axis.horizontal], then the scroll view scrolls from left to right when [reverse] is false and from right to left when [reverse] is true.

Similarly, if [scrollDirection] is [Axis.vertical], then the scroll view scrolls from top to bottom when [reverse] is false and from bottom to top when [reverse] is true.

This property only applies to the outer scroll view, composed of the slivers returned from [headerSliverBuilder]. Since the inner scroll view is not directly configured by the [NestedScrollView]. For both to scroll in reverse, configure the scroll view of the [body] the same way if they are expected to match. This allows for flexible configurations of the NestedScrollView.

Defaults to false.

### physics

```dart
ScrollPhysics? physics
```

How the scroll view should respond to user input.

For example, determines how the scroll view continues to animate after the user stops dragging the scroll view (providing a custom implementation of [ScrollPhysics.createBallisticSimulation] allows this particular aspect of the physics to be overridden).

If an explicit [ScrollBehavior] is provided to [scrollBehavior], the [ScrollPhysics] provided by that behavior will take precedence after [physics].

Defaults to matching platform conventions.

The [ScrollPhysics.applyBoundaryConditions] implementation of the provided object should not allow scrolling outside the scroll extent range described by the [ScrollMetrics.minScrollExtent] and [ScrollMetrics.maxScrollExtent] properties passed to that method. If that invariant is not maintained, the nested scroll view may respond to user scrolling erratically.

This property only applies to the outer scroll view, composed of the slivers returned from [headerSliverBuilder]. Since the inner scroll view is not directly configured by the [NestedScrollView]. For both to scroll with the same [ScrollPhysics], configure the scroll view of the [body] the same way if they are expected to match, or use a [ScrollBehavior] as an ancestor so both the inner and outer scroll views inherit the same [ScrollPhysics]. This allows for flexible configurations of the NestedScrollView.

The [ScrollPhysics] also determine whether or not the [NestedScrollView] can accept input from the user to change the scroll offset. For example, [NeverScrollableScrollPhysics] typically will not allow the user to drag a scroll view, but in this case, if one of the two scroll views can be dragged, then dragging will be allowed. Configuring both scroll views with [NeverScrollableScrollPhysics] will disallow dragging in this case.

### headerSliverBuilder

```dart
NestedScrollViewHeaderSliversBuilder headerSliverBuilder
```

A builder for any widgets that are to precede the inner scroll views (as given by [body]).

Typically this is used to create a [SliverAppBar] with a [TabBar].

### body

```dart
Widget body
```

The widget to show inside the [NestedScrollView].

Typically this will be [TabBarView].

The [body] is built in a context that provides a [PrimaryScrollController] that interacts with the [NestedScrollView]'s scroll controller. Any [ListView] or other [Scrollable]-based widget inside the [body] that is intended to scroll with the [NestedScrollView] should therefore not be given an explicit [ScrollController], instead allowing it to default to the [PrimaryScrollController] provided by the [NestedScrollView].

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### floatHeaderSlivers

```dart
bool floatHeaderSlivers
```

Whether or not the [NestedScrollView]'s coordinator should prioritize the outer scrollable over the inner when scrolling back.

This is useful for an outer scrollable containing a [SliverAppBar] that is expected to float.

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

The [ScrollBehavior] of the inherited [ScrollConfiguration] will be modified by default to not apply a [Scrollbar]. This is because the NestedScrollView cannot assume the configuration of the outer and inner [Scrollable] widgets, particularly whether to treat them as one scrollable, or separate and desirous of unique behaviors.

### sliverOverlapAbsorberHandleFor()

```dart
SliverOverlapAbsorberHandle sliverOverlapAbsorberHandleFor(BuildContext context)
```

Returns the [SliverOverlapAbsorberHandle] of the nearest ancestor [NestedScrollView].

This is necessary to configure the [SliverOverlapAbsorber] and [SliverOverlapInjector] widgets.

For sample code showing how to use this method, see the [NestedScrollView] documentation.

### createState()

```dart
NestedScrollViewState createState()
```

# NestedScrollViewState

```dart
class NestedScrollViewState extends State<NestedScrollView> {}
```

The [State] for a [NestedScrollView].

The [ScrollController]s, [innerController] and [outerController], of the [NestedScrollView]'s children may be accessed through its state. This is useful for obtaining respective scroll positions in the [NestedScrollView].

If you want to access the inner or outer scroll controller of a [NestedScrollView], you can get its [NestedScrollViewState] by supplying a `GlobalKey<NestedScrollViewState>` to the [NestedScrollView.key] parameter).

{@tool dartpad} [NestedScrollViewState] can be obtained using a [GlobalKey]. Using the following setup, you can access the inner scroll controller using `globalKey.currentState.innerController`.

** See code in examples/api/lib/widgets/nested_scroll_view/nested_scroll_view_state.0.dart ** {@end-tool}

### innerController

```dart
ScrollController get innerController
```

The [ScrollController] provided to the [ScrollView] in [NestedScrollView.body].

Manipulating the [ScrollPosition] of this controller pushes the outer header sliver(s) up and out of view. The position of the [outerController] will be set to [ScrollPosition.maxScrollExtent], unless you use [ScrollPosition.setPixels].

See also:

- [outerController], which exposes the [ScrollController] used by the sliver(s) contained in [NestedScrollView.headerSliverBuilder].

### outerController

```dart
ScrollController get outerController
```

The [ScrollController] provided to the [ScrollView] in [NestedScrollView.headerSliverBuilder].

This is equivalent to [NestedScrollView.controller], if provided.

Manipulating the [ScrollPosition] of this controller pushes the inner body sliver(s) down. The position of the [innerController] will be set to [ScrollPosition.minScrollExtent], unless you use [ScrollPosition.setPixels]. Visually, the inner body will be scrolled to its beginning.

See also:

- [innerController], which exposes the [ScrollController] used by the [ScrollView] contained in [NestedScrollView.body].

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
void didUpdateWidget(NestedScrollView oldWidget)
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

# SliverOverlapAbsorberHandle

```dart
class SliverOverlapAbsorberHandle extends ChangeNotifier {}
```

Handle to provide to a [SliverOverlapAbsorber], a [SliverOverlapInjector], and an [NestedScrollViewViewport], to shift overlap in a [NestedScrollView].

A particular [SliverOverlapAbsorberHandle] can only be assigned to a single [SliverOverlapAbsorber] at a time. It can also be (and normally is) assigned to one or more [SliverOverlapInjector]s, which must be later descendants of the same [NestedScrollViewViewport] as the [SliverOverlapAbsorber]. The [SliverOverlapAbsorber] must be a direct descendant of the [NestedScrollViewViewport], taking part in the same sliver layout. (The [SliverOverlapInjector] can be a descendant that takes part in a nested scroll view's sliver layout.)

Whenever the [NestedScrollViewViewport] is marked dirty for layout, it will cause its assigned [SliverOverlapAbsorberHandle] to fire notifications. It is the responsibility of the [SliverOverlapInjector]s (and any other clients) to mark themselves dirty when this happens, in case the geometry subsequently changes during layout.

See also:

- [NestedScrollView], which uses a [NestedScrollViewViewport] and a [SliverOverlapAbsorber] to align its children, and which shows sample usage for this class.

### SliverOverlapAbsorberHandle()

```dart
SliverOverlapAbsorberHandle()
```

Creates a [SliverOverlapAbsorberHandle].

### layoutExtent

```dart
double? get layoutExtent
```

The current amount of overlap being absorbed by the [SliverOverlapAbsorber].

This corresponds to the [SliverGeometry.layoutExtent] of the child of the [SliverOverlapAbsorber].

This is updated during the layout of the [SliverOverlapAbsorber]. It should not change at any other time. No notifications are sent when it changes; clients (e.g. [SliverOverlapInjector]s) are responsible for marking themselves dirty whenever this object sends notifications, which happens any time the [SliverOverlapAbsorber] might subsequently change the value during that layout.

### scrollExtent

```dart
double? get scrollExtent
```

The total scroll extent of the gap being absorbed by the [SliverOverlapAbsorber].

This corresponds to the [SliverGeometry.scrollExtent] of the child of the [SliverOverlapAbsorber].

This is updated during the layout of the [SliverOverlapAbsorber]. It should not change at any other time. No notifications are sent when it changes; clients (e.g. [SliverOverlapInjector]s) are responsible for marking themselves dirty whenever this object sends notifications, which happens any time the [SliverOverlapAbsorber] might subsequently change the value during that layout.

### toString()

```dart
String toString()
```

# SliverOverlapAbsorber

```dart
class SliverOverlapAbsorber extends SingleChildRenderObjectWidget {}
```

A sliver that wraps another, forcing its layout extent to be treated as overlap.

The difference between the overlap requested by the child `sliver` and the overlap reported by this widget, called the _absorbed overlap_, is reported to the [SliverOverlapAbsorberHandle], which is typically passed to a [SliverOverlapInjector].

See also:

- [NestedScrollView], whose documentation has sample code showing how to use this widget.

### SliverOverlapAbsorber()

```dart
SliverOverlapAbsorber({dynamic key, required SliverOverlapAbsorberHandle handle, Widget? sliver})
```

Creates a sliver that absorbs overlap and reports it to a [SliverOverlapAbsorberHandle].

### handle

```dart
SliverOverlapAbsorberHandle handle
```

The object in which the absorbed overlap is recorded.

A particular [SliverOverlapAbsorberHandle] can only be assigned to a single [SliverOverlapAbsorber] at a time.

### createRenderObject()

```dart
RenderSliverOverlapAbsorber createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOverlapAbsorber renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverOverlapAbsorber

```dart
class RenderSliverOverlapAbsorber extends RenderSliver with RenderObjectWithChildMixin<RenderSliver> {}
```

A sliver that wraps another, forcing its layout extent to be treated as overlap.

The difference between the overlap requested by the child `sliver` and the overlap reported by this widget, called the _absorbed overlap_, is reported to the [SliverOverlapAbsorberHandle], which is typically passed to a [RenderSliverOverlapInjector].

### RenderSliverOverlapAbsorber()

```dart
RenderSliverOverlapAbsorber({required SliverOverlapAbsorberHandle handle, RenderSliver? sliver})
```

Create a sliver that absorbs overlap and reports it to a [SliverOverlapAbsorberHandle].

The [sliver] must be a [RenderSliver].

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

The object in which the absorbed overlap is recorded.

A particular [SliverOverlapAbsorberHandle] can only be assigned to a single [RenderSliverOverlapAbsorber] at a time.

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### performLayout()

```dart
void performLayout()
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverOverlapInjector

```dart
class SliverOverlapInjector extends SingleChildRenderObjectWidget {}
```

A sliver that has a sliver geometry based on the values stored in a [SliverOverlapAbsorberHandle].

The [SliverOverlapAbsorber] must be an earlier descendant of a common ancestor [Viewport], so that it will always be laid out before the [SliverOverlapInjector] during a particular frame.

See also:

- [NestedScrollView], which uses a [SliverOverlapAbsorber] to align its children, and which shows sample usage for this class.

### SliverOverlapInjector()

```dart
SliverOverlapInjector({dynamic key, required SliverOverlapAbsorberHandle handle, Widget? sliver})
```

Creates a sliver that is as tall as the value of the given [handle]'s layout extent.

### handle

```dart
SliverOverlapAbsorberHandle handle
```

The handle to the [SliverOverlapAbsorber] that is feeding this injector.

This should be a handle owned by a [SliverOverlapAbsorber] and a [NestedScrollViewViewport].

### createRenderObject()

```dart
RenderSliverOverlapInjector createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOverlapInjector renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverOverlapInjector

```dart
class RenderSliverOverlapInjector extends RenderSliver {}
```

A sliver that has a sliver geometry based on the values stored in a [SliverOverlapAbsorberHandle].

The [RenderSliverOverlapAbsorber] must be an earlier descendant of a common ancestor [RenderViewport] (probably a [RenderNestedScrollViewViewport]), so that it will always be laid out before the [RenderSliverOverlapInjector] during a particular frame.

### RenderSliverOverlapInjector()

```dart
RenderSliverOverlapInjector({required SliverOverlapAbsorberHandle handle})
```

Creates a sliver that is as tall as the value of the given [handle]'s extent.

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

The object that specifies how wide to make the gap injected by this render object.

This should be a handle owned by a [RenderSliverOverlapAbsorber] and a [RenderNestedScrollViewViewport].

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### performLayout()

```dart
void performLayout()
```

### debugPaint()

```dart
void debugPaint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# NestedScrollViewViewport

```dart
class NestedScrollViewViewport extends Viewport {}
```

The [Viewport] variant used by [NestedScrollView].

This viewport takes a [SliverOverlapAbsorberHandle] and notifies it any time the viewport needs to recompute its layout (e.g. when it is scrolled).

### NestedScrollViewViewport()

```dart
NestedScrollViewViewport({dynamic key, dynamic axisDirection, dynamic crossAxisDirection, double anchor, required dynamic offset, dynamic center, List<Widget> slivers, required SliverOverlapAbsorberHandle handle, dynamic clipBehavior})
```

Creates a variant of [Viewport] that has a [SliverOverlapAbsorberHandle].

### handle

```dart
SliverOverlapAbsorberHandle handle
```

The handle to the [SliverOverlapAbsorber] that is feeding this injector.

### createRenderObject()

```dart
RenderNestedScrollViewViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderNestedScrollViewViewport renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderNestedScrollViewViewport

```dart
class RenderNestedScrollViewViewport extends RenderViewport {}
```

The [RenderViewport] variant used by [NestedScrollView].

This viewport takes a [SliverOverlapAbsorberHandle] and notifies it any time the viewport needs to recompute its layout (e.g. when it is scrolled).

### RenderNestedScrollViewViewport()

```dart
RenderNestedScrollViewViewport({dynamic axisDirection, required dynamic crossAxisDirection, required dynamic offset, dynamic anchor, dynamic children, dynamic center, required SliverOverlapAbsorberHandle handle, dynamic clipBehavior})
```

Create a variant of [RenderViewport] that has a [SliverOverlapAbsorberHandle].

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

The object to notify when [markNeedsLayout] is called.

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

Setting this will trigger notifications on the new object.

### markNeedsLayout()

```dart
void markNeedsLayout()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
