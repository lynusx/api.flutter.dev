@docImport 'package:flutter/widgets.dart';

@docImport 'list_wheel_viewport.dart'; @docImport 'sliver_fixed_extent_list.dart'; @docImport 'sliver_grid.dart'; @docImport 'sliver_list.dart';

# ScrollCacheExtent

```dart
sealed class ScrollCacheExtent {}
```

The amount of additional content to display and lay out around the viewport.

The cache area is used to lay out slivers before they are visible on screen. Items that fall in this cache area are laid out even though they are not visible on screen. This allows the viewport to render them ahead of time, enabling a smoother scrolling experience as items scroll into view.

This class encapsulates both the value and the style of the cache extent. It allows the cache extent to be defined either as a fixed number of logical pixels using [ScrollCacheExtent.pixels] or as a multiplier of the viewport's main axis extent using [ScrollCacheExtent.viewport].

See also:

- [Viewport.scrollCacheExtent], which uses this class to define the cache area.

### ScrollCacheExtent.pixels()

```dart
ScrollCacheExtent.pixels(double pixels)
```

Creates a cache extent in logical pixels.

### ScrollCacheExtent.viewport()

```dart
ScrollCacheExtent.viewport(double value)
```

Creates a cache extent as a multiplier of the viewport's main axis extent.

The main axis extent is the size of the viewport in its main axis. For example, for a vertically scrolling list, the main axis extent is the height of the viewport. If the viewport is 600 logical pixels tall, then `ScrollCacheExtent.viewport(2.0)` results in a cache extent of 1200 logical pixels.

### style

```dart
CacheExtentStyle get style
```

Returns the style of the cache extent.

### value

```dart
double get value
```

Returns the raw value of the cache extent.

If [style] is [CacheExtentStyle.pixel], this is the number of pixels to cache.

If [style] is [CacheExtentStyle.viewport], this is the multiplier of the viewport's main axis extent to cache.

# CacheExtentStyle

```dart
enum CacheExtentStyle {}
```

The unit of measurement for a [Viewport.cacheExtent].

Treat the [Viewport.cacheExtent] as logical pixels.

Treat the [Viewport.cacheExtent] as a multiplier of the main axis extent.

# SliverPaintOrder

```dart
enum SliverPaintOrder {}
```

Specifies an order in which to paint the slivers of a [Viewport].

The slivers of a [ScrollView] are the list returned by [ScrollView.buildSlivers]. For a [CustomScrollView], this is the same list as [CustomScrollView.slivers]. For the other built-in subclasses of [ScrollView], there is only one sliver in the list, and this ordering has no effect.

Whichever order the slivers are painted in, they will be hit-tested in the opposite order.

This can also be thought of as an ordering in the z-direction: whichever sliver is painted last (and hit-tested first) is on top, because it will paint over other slivers if there is overlap. Similarly, whichever sliver is painted first (and hit-tested last) is on the bottom.

The first sliver paints on top, and the last sliver on bottom.

The slivers are painted in the reverse order of [Viewport.slivers] (for example, the reverse order of [ScrollView.buildSlivers] or [CustomScrollView.slivers]), and hit-tested in the same order as [Viewport.slivers].

This is the default order.

The last sliver paints on top, and the first sliver on bottom.

The slivers are painted in the same order as [Viewport.slivers] (for example, the same order as [ScrollView.buildSlivers] or [CustomScrollView.slivers]), and hit-tested in the reverse order.

# RenderAbstractViewport

```dart
abstract interface class RenderAbstractViewport extends RenderObject {}
```

An interface for render objects that are bigger on the inside.

Some render objects, such as [RenderViewport], present a portion of their content, which can be controlled by a [ViewportOffset]. This interface lets the framework recognize such render objects and interact with them without having specific knowledge of all the various types of viewports.

### maybeOf()

```dart
RenderAbstractViewport? maybeOf(RenderObject? object)
```

Returns the [RenderAbstractViewport] that most tightly encloses the given render object.

If the object does not have a [RenderAbstractViewport] as an ancestor, this function returns null.

See also:

- [RenderAbstractViewport.of], which is similar to this method, but asserts if no [RenderAbstractViewport] ancestor is found.

### of()

```dart
RenderAbstractViewport of(RenderObject? object)
```

Returns the [RenderAbstractViewport] that most tightly encloses the given render object.

If the object does not have a [RenderAbstractViewport] as an ancestor, this function will assert in debug mode, and throw an exception in release mode.

See also:

- [RenderAbstractViewport.maybeOf], which is similar to this method, but returns null if no [RenderAbstractViewport] ancestor is found.

### getOffsetToReveal()

```dart
RevealedOffset getOffsetToReveal(RenderObject target, double alignment, {Rect? rect, Axis? axis})
```

Returns the offset that would be needed to reveal the `target` [RenderObject].

This is used by [RenderViewportBase.showInViewport], which is itself used by [RenderObject.showOnScreen] for [RenderViewportBase], which is in turn used by the semantics system to implement scrolling for accessibility tools.

The optional `rect` parameter describes which area of that `target` object should be revealed in the viewport. If `rect` is null, the entire `target` [RenderObject] (as defined by its [RenderObject.paintBounds]) will be revealed. If `rect` is provided it has to be given in the coordinate system of the `target` object.

The `alignment` argument describes where the target should be positioned after applying the returned offset. If `alignment` is 0.0, the child must be positioned as close to the leading edge of the viewport as possible. If `alignment` is 1.0, the child must be positioned as close to the trailing edge of the viewport as possible. If `alignment` is 0.5, the child must be positioned as close to the center of the viewport as possible.

The `target` might not be a direct child of this viewport but it must be a descendant of the viewport. Other viewports in between this viewport and the `target` will not be adjusted.

This method assumes that the content of the viewport moves linearly, i.e. when the offset of the viewport is changed by x then `target` also moves by x within the viewport.

The optional [Axis] is used by [RenderTwoDimensionalViewport.getOffsetToReveal] to determine which of the two axes to compute an offset for. One dimensional subclasses like [RenderViewportBase] and [RenderListWheelViewport] will ignore the `axis` value if provided, since there is only one [Axis].

If the `axis` is omitted when called on [RenderTwoDimensionalViewport], the [RenderTwoDimensionalViewport.mainAxis] is used. To reveal an object properly in both axes, this method should be called for each [Axis] as the returned [RevealedOffset.offset] only represents the offset of one of the the two [ScrollPosition]s.

See also:

- [RevealedOffset], which describes the return value of this method.

### defaultCacheExtent

```dart
double defaultCacheExtent
```

The default value for the cache extent of the viewport.

This default assumes [CacheExtentStyle.pixel].

See also:

- [RenderViewportBase.cacheExtent] for a definition of the cache extent.

# RevealedOffset

```dart
class RevealedOffset {}
```

Return value for [RenderAbstractViewport.getOffsetToReveal].

It indicates the [offset] required to reveal an element in a viewport and the [rect] position said element would have in the viewport at that [offset].

### RevealedOffset()

```dart
RevealedOffset({required double offset, required Rect rect})
```

Instantiates a return value for [RenderAbstractViewport.getOffsetToReveal].

### offset

```dart
double offset
```

Offset for the viewport to reveal a specific element in the viewport.

See also:

- [RenderAbstractViewport.getOffsetToReveal], which calculates this value for a specific element.

### rect

```dart
Rect rect
```

The [Rect] in the outer coordinate system of the viewport at which the to-be-revealed element would be located if the viewport's offset is set to [offset].

A viewport usually has two coordinate systems and works as an adapter between the two:

The inner coordinate system has its origin at the top left corner of the content that moves inside the viewport. The origin of this coordinate system usually moves around relative to the leading edge of the viewport when the viewport offset changes.

The outer coordinate system has its origin at the top left corner of the visible part of the viewport. This origin stays at the same position regardless of the current viewport offset.

In other words: [rect] describes where the revealed element would be located relative to the top left corner of the visible part of the viewport if the viewport's offset is set to [offset].

See also:

- [RenderAbstractViewport.getOffsetToReveal], which calculates this value for a specific element.

### clampOffset()

```dart
RevealedOffset? clampOffset({required RevealedOffset leadingEdgeOffset, required RevealedOffset trailingEdgeOffset, required double currentOffset})
```

Determines which provided leading or trailing edge of the viewport, as [RevealedOffset]s, will be used for [RenderViewportBase.showInViewport] accounting for the size and already visible portion of the [RenderObject] that is being revealed.

Also used by [RenderTwoDimensionalViewport.showInViewport] for each horizontal and vertical [Axis].

If the target [RenderObject] is already fully visible, this will return null.

### toString()

```dart
String toString()
```

# RenderViewportBase

```dart
abstract class RenderViewportBase<ParentDataClass extends ContainerParentDataMixin<RenderSliver>> extends RenderBox with ContainerRenderObjectMixin<RenderSliver, ParentDataClass> implements RenderAbstractViewport {}
```

A base class for render objects that are bigger on the inside.

This render object provides the shared code for render objects that host [RenderSliver] render objects inside a [RenderBox]. The viewport establishes an [axisDirection], which orients the sliver's coordinate system, which is based on scroll offsets rather than Cartesian coordinates.

The viewport also listens to an [offset], which determines the [SliverConstraints.scrollOffset] input to the sliver layout protocol.

Subclasses typically override [performLayout] and call [layoutChildSequence], perhaps multiple times.

See also:

- [RenderSliver], which explains more about the Sliver protocol.
- [RenderBox], which explains more about the Box protocol.
- [RenderSliverToBoxAdapter], which allows a [RenderBox] object to be placed inside a [RenderSliver] (the opposite of this class).

### RenderViewportBase()

```dart
RenderViewportBase({AxisDirection axisDirection = AxisDirection.down, required AxisDirection crossAxisDirection, required ViewportOffset offset, double? cacheExtent, CacheExtentStyle cacheExtentStyle = CacheExtentStyle.pixel, ScrollCacheExtent? scrollCacheExtent, SliverPaintOrder paintOrder = SliverPaintOrder.firstIsTop, Clip clipBehavior = Clip.hardEdge})
```

Initializes fields for subclasses.

The [scrollCacheExtent] sets the amount of scrollable content that is cached.

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

Report the semantics of this node, for example for accessibility purposes.

[RenderViewportBase] adds [RenderViewport.useTwoPaneSemantics] to the provided [SemanticsConfiguration] to support children using [RenderViewport.excludeFromScrolling].

This method should be overridden by subclasses that have interesting semantic information. Overriding subclasses should call `super.describeSemanticsConfiguration(config)` to ensure [RenderViewport.useTwoPaneSemantics] is still added to `config`.

See also:

- [RenderObject.describeSemanticsConfiguration], for important details about not mutating a [SemanticsConfiguration] out of context.

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### axisDirection

```dart
AxisDirection get axisDirection
```

The direction in which the [SliverConstraints.scrollOffset] increases.

For example, if the [axisDirection] is [AxisDirection.down], a scroll offset of zero is at the top of the viewport and increases towards the bottom of the viewport.

### axisDirection

```dart
set axisDirection(AxisDirection value)
```

### crossAxisDirection

```dart
AxisDirection get crossAxisDirection
```

The direction in which child should be laid out in the cross axis.

For example, if the [axisDirection] is [AxisDirection.down], this property is typically [AxisDirection.left] if the ambient [TextDirection] is [TextDirection.rtl] and [AxisDirection.right] if the ambient [TextDirection] is [TextDirection.ltr].

### crossAxisDirection

```dart
set crossAxisDirection(AxisDirection value)
```

### axis

```dart
Axis get axis
```

The axis along which the viewport scrolls.

For example, if the [axisDirection] is [AxisDirection.down], then the [axis] is [Axis.vertical] and the viewport scrolls vertically.

### offset

```dart
ViewportOffset get offset
```

Which part of the content inside the viewport should be visible.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport, this value changes, which changes the content that is displayed.

### offset

```dart
set offset(ViewportOffset value)
```

### cacheExtent

```dart
double? get cacheExtent
```

{@template flutter.rendering.RenderViewportBase.cacheExtent} Deprecated. Use [scrollCacheExtent] instead. {@endtemplate}

### cacheExtent

```dart
set cacheExtent(double? value)
```

### scrollCacheExtent

```dart
ScrollCacheExtent get scrollCacheExtent
```

{@template flutter.rendering.RenderViewportBase.scrollCacheExtent} The viewport has an area before and after the visible area to cache items that are about to become visible when the user scrolls.

Items that fall in this cache area are laid out even though they are not (yet) visible on screen. The [scrollCacheExtent] describes how much the cache area extends before the leading edge and after the trailing edge of the viewport.

The total extent, which the viewport will try to cover with children, is [scrollCacheExtent] before the leading edge + extent of the main axis + [scrollCacheExtent] after the trailing edge.

The cache area is also used to implement implicit accessibility scrolling on iOS: When the accessibility focus moves from an item in the visible viewport to an invisible item in the cache area, the framework will bring that item into view with an (implicit) scroll action. {@endtemplate}

The getter can never return null, but the field is nullable because the setter can be set to null to reset the value to [RenderAbstractViewport.defaultCacheExtent] pixels (in which case [ScrollCacheExtent.style] must be [CacheExtentStyle.pixel]).

See also:

- [ScrollCacheExtent.style], which controls the units of the [scrollCacheExtent].

### scrollCacheExtent

```dart
set scrollCacheExtent(ScrollCacheExtent? value)
```

### cacheExtentStyle

```dart
CacheExtentStyle get cacheExtentStyle
```

{@template flutter.rendering.RenderViewportBase.cacheExtentStyle} Deprecated. Use [scrollCacheExtent] instead. {@endtemplate}

### cacheExtentStyle

```dart
set cacheExtentStyle(CacheExtentStyle value)
```

### paintOrder

```dart
SliverPaintOrder get paintOrder
```

{@template flutter.rendering.RenderViewportBase.paintOrder} The order in which to paint the slivers; equivalently, the order in which to arrange them in the z-direction.

Whichever order the slivers are painted in, they will be hit-tested in the opposite order.

To think of this as an ordering in the z-direction: whichever sliver is painted last (and hit-tested first) is on top, because it will paint over other slivers if there is overlap. Similarly, whichever sliver is painted first (and hit-tested last) is on the bottom. {@endtemplate}

The default is [SliverPaintOrder.firstIsTop].

### paintOrder

```dart
set paintOrder(SliverPaintOrder value)
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### debugThrowIfNotCheckingIntrinsics()

```dart
bool debugThrowIfNotCheckingIntrinsics()
```

Throws an exception saying that the object does not support returning intrinsic dimensions if, in debug mode, we are not in the [RenderObject.debugCheckingIntrinsics] mode.

This is used by [computeMinIntrinsicWidth] et al because viewports do not generally support returning intrinsic dimensions. See the discussion at [computeMinIntrinsicWidth].

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### layoutChildSequence()

```dart
double layoutChildSequence({required RenderSliver? child, required double scrollOffset, required double overlap, required double layoutOffset, required double remainingPaintExtent, required double mainAxisExtent, required double crossAxisExtent, required GrowthDirection growthDirection, required RenderSliver? Function(RenderSliver child) advance, required double remainingCacheExtent, required double cacheOrigin})
```

Determines the size and position of some of the children of the viewport.

This function is the workhorse of `performLayout` implementations in subclasses.

Layout starts with `child`, proceeds according to the `advance` callback, and stops once `advance` returns null.

- `scrollOffset` is the [SliverConstraints.scrollOffset] to pass the first child. The scroll offset is adjusted by [SliverGeometry.scrollExtent] for subsequent children.
- `overlap` is the [SliverConstraints.overlap] to pass the first child. The overlay is adjusted by the [SliverGeometry.paintOrigin] and [SliverGeometry.paintExtent] for subsequent children.
- `layoutOffset` is the layout offset at which to place the first child. The layout offset is updated by the [SliverGeometry.layoutExtent] for subsequent children.
- `remainingPaintExtent` is [SliverConstraints.remainingPaintExtent] to pass the first child. The remaining paint extent is updated by the [SliverGeometry.layoutExtent] for subsequent children.
- `mainAxisExtent` is the [SliverConstraints.viewportMainAxisExtent] to pass to each child.
- `crossAxisExtent` is the [SliverConstraints.crossAxisExtent] to pass to each child.
- `growthDirection` is the [SliverConstraints.growthDirection] to pass to each child.

Returns the first non-zero [SliverGeometry.scrollOffsetCorrection] encountered, if any. Otherwise returns 0.0. Typical callers will call this function repeatedly until it returns 0.0.

### describeApproximatePaintClip()

```dart
Rect? describeApproximatePaintClip(RenderSliver child)
```

### describeSemanticsClip()

```dart
Rect? describeSemanticsClip(RenderSliver? child)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### getOffsetToReveal()

```dart
RevealedOffset getOffsetToReveal(RenderObject target, double alignment, {Rect? rect, Axis? axis})
```

### computeAbsolutePaintOffset()

```dart
Offset computeAbsolutePaintOffset(RenderSliver child, double layoutOffset, GrowthDirection growthDirection)
```

The offset at which the given `child` should be painted.

The returned offset is from the top left corner of the inside of the viewport to the top left corner of the paint coordinate system of the `child`.

See also:

- [paintOffsetOf], which uses the layout offset and growth direction computed for the child during layout.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### hasVisualOverflow

```dart
bool get hasVisualOverflow
```

Whether the contents of this viewport would paint outside the bounds of the viewport if [paint] did not clip.

This property enables an optimization whereby [paint] can skip apply a clip of the contents of the viewport are known to paint entirely within the bounds of the viewport.

### updateOutOfBandData()

```dart
void updateOutOfBandData(GrowthDirection growthDirection, SliverGeometry childLayoutGeometry)
```

Called during [layoutChildSequence] for each child.

Typically used by subclasses to update any out-of-band data, such as the max scroll extent, for each child.

### updateChildLayoutOffset()

```dart
void updateChildLayoutOffset(RenderSliver child, double layoutOffset, GrowthDirection growthDirection)
```

Called during [layoutChildSequence] to store the layout offset for the given child.

Different subclasses using different representations for their children's layout offset (e.g., logical or physical coordinates). This function lets subclasses transform the child's layout offset before storing it in the child's parent data.

### paintOffsetOf()

```dart
Offset paintOffsetOf(RenderSliver child)
```

The offset at which the given `child` should be painted.

The returned offset is from the top left corner of the inside of the viewport to the top left corner of the paint coordinate system of the `child`.

See also:

- [computeAbsolutePaintOffset], which computes the paint offset from an explicit layout offset and growth direction instead of using the values computed for the child during layout.

### scrollOffsetOf()

```dart
double scrollOffsetOf(RenderSliver child, double scrollOffsetWithinChild)
```

Returns the scroll offset within the viewport for the given `scrollOffsetWithinChild` within the given `child`.

The returned value is an estimate that assumes the slivers within the viewport do not change the layout extent in response to changes in their scroll offset.

### maxScrollObstructionExtentBefore()

```dart
double maxScrollObstructionExtentBefore(RenderSliver child)
```

Returns the total scroll obstruction extent of all slivers in the viewport before [child].

This is the extent by which the actual area in which content can scroll is reduced. For example, an app bar that is pinned at the top will reduce the area in which content can actually scroll by the height of the app bar.

### computeChildMainAxisPosition()

```dart
double computeChildMainAxisPosition(RenderSliver child, double parentMainAxisPosition)
```

Converts the `parentMainAxisPosition` into the child's coordinate system.

The `parentMainAxisPosition` is a distance from the top edge (for vertical viewports) or left edge (for horizontal viewports) of the viewport bounds. This describes a line, perpendicular to the viewport's main axis, heretofore known as the target line.

The child's coordinate system's origin in the main axis is at the leading edge of the given child, as given by the child's [SliverConstraints.axisDirection] and [SliverConstraints.growthDirection].

This method returns the distance from the leading edge of the given child to the target line described above.

(The `parentMainAxisPosition` is not from the leading edge of the viewport, it's always the top or left edge.)

### indexOfFirstChild

```dart
int get indexOfFirstChild
```

The index of the first child of the viewport relative to the center child.

For example, the center child has index zero and the first child in the reverse growth direction has index -1.

### labelForChild()

```dart
String labelForChild(int index)
```

A short string to identify the child with the given index.

Used by [debugDescribeChildren] to label the children.

### childrenInPaintOrder

```dart
Iterable<RenderSliver> get childrenInPaintOrder
```

Provides an iterable that walks the children of the viewport, in the order that they should be painted.

This should be the reverse order of [childrenInHitTestOrder].

### childrenInHitTestOrder

```dart
Iterable<RenderSliver> get childrenInHitTestOrder
```

Provides an iterable that walks the children of the viewport, in the order that hit-testing should use.

This should be the reverse order of [childrenInPaintOrder].

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

### showInViewport()

```dart
Rect? showInViewport({RenderObject? descendant, Rect? rect, required RenderAbstractViewport viewport, required ViewportOffset offset, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

Make (a portion of) the given `descendant` of the given `viewport` fully visible in the `viewport` by manipulating the provided [ViewportOffset] `offset`.

The optional `rect` parameter describes which area of the `descendant` should be shown in the viewport. If `rect` is null, the entire `descendant` will be revealed. The `rect` parameter is interpreted relative to the coordinate system of `descendant`.

The returned [Rect] describes the new location of `descendant` or `rect` in the viewport after it has been revealed. See [RevealedOffset.rect] for a full definition of this [Rect].

If `descendant` is null, this is a no-op and `rect` is returned.

If both `descendant` and `rect` are null, null is returned because there is nothing to be shown in the viewport.

The `duration` parameter can be set to a non-zero value to animate the target object into the viewport with an animation defined by `curve`.

See also:

- [RenderObject.showOnScreen], overridden by [RenderViewportBase] and the renderer for [SingleChildScrollView] to delegate to this method.

# RenderViewport

```dart
class RenderViewport extends RenderViewportBase<SliverPhysicalContainerParentData> {}
```

A render object that is bigger on the inside.

[RenderViewport] is the visual workhorse of the scrolling machinery. It displays a subset of its children according to its own dimensions and the given [offset]. As the offset varies, different children are visible through the viewport.

[RenderViewport] hosts a bidirectional list of slivers in a single shared [Axis], anchored on a [center] sliver, which is placed at the zero scroll offset. The center widget is displayed in the viewport according to the [anchor] property.

Slivers that are earlier in the child list than [center] are displayed in reverse order in the reverse [axisDirection] starting from the [center]. For example, if the [axisDirection] is [AxisDirection.down], the first sliver before [center] is placed above the [center]. The slivers that are later in the child list than [center] are placed in order in the [axisDirection]. For example, in the preceding scenario, the first sliver after [center] is placed below the [center].

{@macro flutter.rendering.GrowthDirection.sample}

[RenderViewport] cannot contain [RenderBox] children directly. Instead, use a [RenderSliverList], [RenderSliverFixedExtentList], [RenderSliverGrid], or a [RenderSliverToBoxAdapter], for example.

See also:

- [RenderSliver], which explains more about the Sliver protocol.
- [RenderBox], which explains more about the Box protocol.
- [RenderSliverToBoxAdapter], which allows a [RenderBox] object to be placed inside a [RenderSliver] (the opposite of this class).
- [RenderShrinkWrappingViewport], a variant of [RenderViewport] that shrink-wraps its contents along the main axis.

### RenderViewport()

```dart
RenderViewport({dynamic axisDirection, required dynamic crossAxisDirection, required ViewportOffset offset, double anchor = 0.0, List<RenderSliver>? children, RenderSliver? center, double? cacheExtent, CacheExtentStyle cacheExtentStyle, ScrollCacheExtent? scrollCacheExtent, SliverPaintOrder paintOrder, dynamic clipBehavior})
```

Creates a viewport for [RenderSliver] objects.

If the [center] is not specified, then the first child in the `children` list, if any, is used.

The [offset] must be specified. For testing purposes, consider passing a [ViewportOffset.zero] or [ViewportOffset.fixed].

### useTwoPaneSemantics

```dart
SemanticsTag useTwoPaneSemantics
```

If a [RenderAbstractViewport] overrides [RenderObject.describeSemanticsConfiguration] to add the [SemanticsTag] [useTwoPaneSemantics] to its [SemanticsConfiguration], two semantics nodes will be used to represent the viewport with its associated scrolling actions in the semantics tree.

Two semantics nodes (an inner and an outer node) are necessary to exclude certain child nodes (via the [excludeFromScrolling] tag) from the scrollable area for semantic purposes: The [SemanticsNode]s of children that should be excluded from scrolling will be attached to the outer node. The semantic scrolling actions and the [SemanticsNode]s of scrollable children will be attached to the inner node, which itself is a child of the outer node.

See also:

- [RenderViewportBase.describeSemanticsConfiguration], which adds this tag to its [SemanticsConfiguration].

### excludeFromScrolling

```dart
SemanticsTag excludeFromScrolling
```

When a top-level [SemanticsNode] below a [RenderAbstractViewport] is tagged with [excludeFromScrolling] it will not be part of the scrolling area for semantic purposes.

This behavior is only active if the [RenderAbstractViewport] tagged its [SemanticsConfiguration] with [useTwoPaneSemantics]. Otherwise, the [excludeFromScrolling] tag is ignored.

As an example, a [RenderSliver] that stays on the screen within a [Scrollable] even though the user has scrolled past it (e.g. a pinned app bar) can tag its [SemanticsNode] with [excludeFromScrolling] to indicate that it should no longer be considered for semantic actions related to scrolling.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### anchor

```dart
double get anchor
```

The relative position of the zero scroll offset.

For example, if [anchor] is 0.5 and the [axisDirection] is [AxisDirection.down] or [AxisDirection.up], then the zero scroll offset is vertically centered within the viewport. If the [anchor] is 1.0, and the [axisDirection] is [AxisDirection.right], then the zero scroll offset is on the left edge of the viewport.

{@macro flutter.rendering.GrowthDirection.sample}

### anchor

```dart
set anchor(double value)
```

### center

```dart
RenderSliver? get center
```

The first child in the [GrowthDirection.forward] growth direction.

This child that will be at the position defined by [anchor] when the [ViewportOffset.pixels] of [offset] is `0`.

Children after [center] will be placed in the [axisDirection] relative to the [center].

Children before [center] will be placed in the opposite of the [axisDirection] relative to the [center]. These children above [center] will have a growth direction of [GrowthDirection.reverse].

The [center] must be a direct child of the viewport.

{@macro flutter.rendering.GrowthDirection.sample}

### center

```dart
set center(RenderSliver? value)
```

### sizedByParent

```dart
bool get sizedByParent
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### hasVisualOverflow

```dart
bool get hasVisualOverflow
```

### updateOutOfBandData()

```dart
void updateOutOfBandData(GrowthDirection growthDirection, SliverGeometry childLayoutGeometry)
```

### updateChildLayoutOffset()

```dart
void updateChildLayoutOffset(RenderSliver child, double layoutOffset, GrowthDirection growthDirection)
```

### paintOffsetOf()

```dart
Offset paintOffsetOf(RenderSliver child)
```

### scrollOffsetOf()

```dart
double scrollOffsetOf(RenderSliver child, double scrollOffsetWithinChild)
```

### maxScrollObstructionExtentBefore()

```dart
double maxScrollObstructionExtentBefore(RenderSliver child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### computeChildMainAxisPosition()

```dart
double computeChildMainAxisPosition(RenderSliver child, double parentMainAxisPosition)
```

### indexOfFirstChild

```dart
int get indexOfFirstChild
```

### labelForChild()

```dart
String labelForChild(int index)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderShrinkWrappingViewport

```dart
class RenderShrinkWrappingViewport extends RenderViewportBase<SliverLogicalContainerParentData> {}
```

A render object that is bigger on the inside and shrink wraps its children in the main axis.

[RenderShrinkWrappingViewport] displays a subset of its children according to its own dimensions and the given [offset]. As the offset varies, different children are visible through the viewport.

[RenderShrinkWrappingViewport] differs from [RenderViewport] in that [RenderViewport] expands to fill the main axis whereas [RenderShrinkWrappingViewport] sizes itself to match its children in the main axis. This shrink wrapping behavior is expensive because the children, and hence the viewport, could potentially change size whenever the [offset] changes (e.g., because of a collapsing header).

[RenderShrinkWrappingViewport] cannot contain [RenderBox] children directly. Instead, use a [RenderSliverList], [RenderSliverFixedExtentList], [RenderSliverGrid], or a [RenderSliverToBoxAdapter], for example.

See also:

- [RenderViewport], a viewport that does not shrink-wrap its contents.
- [RenderSliver], which explains more about the Sliver protocol.
- [RenderBox], which explains more about the Box protocol.
- [RenderSliverToBoxAdapter], which allows a [RenderBox] object to be placed inside a [RenderSliver] (the opposite of this class).

### RenderShrinkWrappingViewport()

```dart
RenderShrinkWrappingViewport({dynamic axisDirection, required dynamic crossAxisDirection, required ViewportOffset offset, SliverPaintOrder paintOrder, dynamic clipBehavior, ScrollCacheExtent? scrollCacheExtent, List<RenderSliver>? children})
```

Creates a viewport (for [RenderSliver] objects) that shrink-wraps its contents.

The [offset] must be specified. For testing purposes, consider passing a [ViewportOffset.zero] or [ViewportOffset.fixed].

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### debugThrowIfNotCheckingIntrinsics()

```dart
bool debugThrowIfNotCheckingIntrinsics()
```

### performLayout()

```dart
void performLayout()
```

### hasVisualOverflow

```dart
bool get hasVisualOverflow
```

### updateOutOfBandData()

```dart
void updateOutOfBandData(GrowthDirection growthDirection, SliverGeometry childLayoutGeometry)
```

### updateChildLayoutOffset()

```dart
void updateChildLayoutOffset(RenderSliver child, double layoutOffset, GrowthDirection growthDirection)
```

### paintOffsetOf()

```dart
Offset paintOffsetOf(RenderSliver child)
```

### scrollOffsetOf()

```dart
double scrollOffsetOf(RenderSliver child, double scrollOffsetWithinChild)
```

### maxScrollObstructionExtentBefore()

```dart
double maxScrollObstructionExtentBefore(RenderSliver child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### computeChildMainAxisPosition()

```dart
double computeChildMainAxisPosition(RenderSliver child, double parentMainAxisPosition)
```

### indexOfFirstChild

```dart
int get indexOfFirstChild
```

### labelForChild()

```dart
String labelForChild(int index)
```
