@docImport 'package:flutter/material.dart';

@docImport 'proxy_box.dart'; @docImport 'proxy_sliver.dart'; @docImport 'sliver_fill.dart'; @docImport 'sliver_grid.dart'; @docImport 'sliver_group.dart'; @docImport 'sliver_list.dart'; @docImport 'sliver_padding.dart'; @docImport 'sliver_persistent_header.dart';

# ItemExtentBuilder

```dart
typedef ItemExtentBuilder = double? Function(int index, SliverLayoutDimensions dimensions)
```

Called to get the item extent by the index of item.

Should return null if asked to build an item extent with a greater index than exists.

Used by [ListView.itemExtentBuilder] and [SliverVariedExtentList.itemExtentBuilder].

# SliverLayoutDimensions

```dart
class SliverLayoutDimensions {}
```

Relates the dimensions of the [RenderSliver] during layout.

Used by [ListView.itemExtentBuilder] and [SliverVariedExtentList.itemExtentBuilder].

### SliverLayoutDimensions()

```dart
SliverLayoutDimensions({required double scrollOffset, required double precedingScrollExtent, required double viewportMainAxisExtent, required double crossAxisExtent})
```

Constructs a [SliverLayoutDimensions] with the specified parameters.

### scrollOffset

```dart
double scrollOffset
```

{@macro flutter.rendering.SliverConstraints.scrollOffset}

### precedingScrollExtent

```dart
double precedingScrollExtent
```

{@macro flutter.rendering.SliverConstraints.precedingScrollExtent}

### viewportMainAxisExtent

```dart
double viewportMainAxisExtent
```

The number of pixels the viewport can display in the main axis.

For a vertical list, this is the height of the viewport.

### crossAxisExtent

```dart
double crossAxisExtent
```

The number of pixels in the cross-axis.

For a vertical list, this is the width of the sliver.

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```

### hashCode

```dart
int get hashCode
```

# GrowthDirection

```dart
enum GrowthDirection {}
```

The direction in which a sliver's contents are ordered, relative to the scroll offset axis.

For example, a vertical alphabetical list that is going [AxisDirection.down] with a [GrowthDirection.forward] would have the A at the top and the Z at the bottom, with the A adjacent to the origin, as would such a list going [AxisDirection.up] with a [GrowthDirection.reverse]. On the other hand, a vertical alphabetical list that is going [AxisDirection.down] with a [GrowthDirection.reverse] would have the Z at the top (at scroll offset zero) and the A below it.

{@template flutter.rendering.GrowthDirection.sample} Most scroll views by default are ordered [GrowthDirection.forward]. Changing the default values of [ScrollView.anchor], [ScrollView.center], or both, can configure a scroll view for [GrowthDirection.reverse].

{@tool dartpad} This sample shows a [CustomScrollView], with [Radio] buttons in the [AppBar.bottom] that change the [AxisDirection] to illustrate different configurations. The [CustomScrollView.anchor] and [CustomScrollView.center] properties are also set to have the 0 scroll offset positioned in the middle of the viewport, with [GrowthDirection.forward] and [GrowthDirection.reverse] illustrated on either side. The sliver that shares the [CustomScrollView.center] key is positioned at the [CustomScrollView.anchor].

** See code in examples/api/lib/rendering/growth_direction/growth_direction.0.dart ** {@end-tool} {@endtemplate}

See also:

- [applyGrowthDirectionToAxisDirection], which returns the direction in which the scroll offset increases.

This sliver's contents are ordered in the same direction as the [AxisDirection]. For example, a vertical alphabetical list that is going [AxisDirection.down] with a [GrowthDirection.forward] would have the A at the top and the Z at the bottom, with the A adjacent to the origin.

See also:

- [applyGrowthDirectionToAxisDirection], which returns the direction in which the scroll offset increases.

This sliver's contents are ordered in the opposite direction of the [AxisDirection].

See also:

- [applyGrowthDirectionToAxisDirection], which returns the direction in which the scroll offset increases.

# applyGrowthDirectionToAxisDirection()

```dart
AxisDirection applyGrowthDirectionToAxisDirection(AxisDirection axisDirection, GrowthDirection growthDirection)
```

Flips the [AxisDirection] if the [GrowthDirection] is [GrowthDirection.reverse].

Specifically, returns `axisDirection` if `growthDirection` is [GrowthDirection.forward], otherwise returns [flipAxisDirection] applied to `axisDirection`.

This function is useful in [RenderSliver] subclasses that are given both an [AxisDirection] and a [GrowthDirection] and wish to compute the [AxisDirection] in which growth will occur.

# applyGrowthDirectionToScrollDirection()

```dart
ScrollDirection applyGrowthDirectionToScrollDirection(ScrollDirection scrollDirection, GrowthDirection growthDirection)
```

Flips the [ScrollDirection] if the [GrowthDirection] is [GrowthDirection.reverse].

Specifically, returns `scrollDirection` if `scrollDirection` is [GrowthDirection.forward], otherwise returns [flipScrollDirection] applied to `scrollDirection`.

This function is useful in [RenderSliver] subclasses that are given both an [ScrollDirection] and a [GrowthDirection] and wish to compute the [ScrollDirection] in which growth will occur.

# SliverConstraints

```dart
class SliverConstraints extends Constraints {}
```

Immutable layout constraints for [RenderSliver] layout.

The [SliverConstraints] describe the current scroll state of the viewport from the point of view of the sliver receiving the constraints. For example, a [scrollOffset] of zero means that the leading edge of the sliver is visible in the viewport, not that the viewport itself has a zero scroll offset.

### SliverConstraints()

```dart
SliverConstraints({required AxisDirection axisDirection, required GrowthDirection growthDirection, required ScrollDirection userScrollDirection, required double scrollOffset, required double precedingScrollExtent, required double overlap, required double remainingPaintExtent, required double crossAxisExtent, required AxisDirection crossAxisDirection, required double viewportMainAxisExtent, required double remainingCacheExtent, required double cacheOrigin})
```

Creates sliver constraints with the given information.

### copyWith()

```dart
SliverConstraints copyWith({AxisDirection? axisDirection, GrowthDirection? growthDirection, ScrollDirection? userScrollDirection, double? scrollOffset, double? precedingScrollExtent, double? overlap, double? remainingPaintExtent, double? crossAxisExtent, AxisDirection? crossAxisDirection, double? viewportMainAxisExtent, double? remainingCacheExtent, double? cacheOrigin})
```

Creates a copy of this object but with the given fields replaced with the new values.

### axisDirection

```dart
AxisDirection axisDirection
```

The direction in which the [scrollOffset] and [remainingPaintExtent] increase.

{@tool dartpad} This sample shows a [CustomScrollView], with [Radio] buttons in the [AppBar.bottom] that change the [AxisDirection] to illustrate different configurations.

** See code in examples/api/lib/painting/axis_direction/axis_direction.0.dart ** {@end-tool}

### growthDirection

```dart
GrowthDirection growthDirection
```

The direction in which the contents of slivers are ordered, relative to the [axisDirection].

For example, if the [axisDirection] is [AxisDirection.up], and the [growthDirection] is [GrowthDirection.forward], then an alphabetical list will have A at the bottom, then B, then C, and so forth, with Z at the top, with the bottom of the A at scroll offset zero, and the top of the Z at the highest scroll offset.

If a viewport has an overall [AxisDirection] of [AxisDirection.down], then slivers above the absolute zero offset will have an axis of [AxisDirection.up] and a growth direction of [GrowthDirection.reverse], while slivers below the absolute zero offset will have the same axis direction as the viewport and a growth direction of [GrowthDirection.forward]. (The slivers with a reverse growth direction still see only positive scroll offsets; the scroll offsets are reversed as well, with zero at the absolute zero point, and positive numbers going away from there.)

Normally, the absolute zero offset is determined by the viewport's [RenderViewport.center] and [RenderViewport.anchor] properties.

{@macro flutter.rendering.GrowthDirection.sample}

### userScrollDirection

```dart
ScrollDirection userScrollDirection
```

The direction in which the user is attempting to scroll, relative to the [axisDirection] and [growthDirection].

For example, if [growthDirection] is [GrowthDirection.forward] and [axisDirection] is [AxisDirection.down], then a [ScrollDirection.reverse] means that the user is scrolling down, in the positive [scrollOffset] direction.

If the _user_ is not scrolling, this will return [ScrollDirection.idle] even if there is (for example) a [ScrollActivity] currently animating the position.

This is used by some slivers to determine how to react to a change in scroll offset. For example, [RenderSliverFloatingPersistentHeader] will only expand a floating app bar when the [userScrollDirection] is in the positive scroll offset direction.

{@macro flutter.rendering.ScrollDirection.sample}

### scrollOffset

```dart
double scrollOffset
```

{@template flutter.rendering.SliverConstraints.scrollOffset} The scroll offset, in this sliver's coordinate system, that corresponds to the earliest visible part of this sliver in the [AxisDirection] if [SliverConstraints.growthDirection] is [GrowthDirection.forward] or in the opposite [AxisDirection] direction if [SliverConstraints.growthDirection] is [GrowthDirection.reverse].

For example, if [AxisDirection] is [AxisDirection.down] and [SliverConstraints.growthDirection] is [GrowthDirection.forward], then scroll offset is the amount the top of the sliver has been scrolled past the top of the viewport.

This value is typically used to compute whether this sliver should still protrude into the viewport via [SliverGeometry.paintExtent] and [SliverGeometry.layoutExtent] considering how far the beginning of the sliver is above the beginning of the viewport.

For slivers whose top is not past the top of the viewport, the [scrollOffset] is `0` when [AxisDirection] is [AxisDirection.down] and [SliverConstraints.growthDirection] is [GrowthDirection.forward]. The set of slivers with [scrollOffset] `0` includes all the slivers that are below the bottom of the viewport.

[SliverConstraints.remainingPaintExtent] is typically used to accomplish the same goal of computing whether scrolled out slivers should still partially 'protrude in' from the bottom of the viewport.

Whether this corresponds to the beginning or the end of the sliver's contents depends on the [SliverConstraints.growthDirection]. {@endtemplate}

### precedingScrollExtent

```dart
double precedingScrollExtent
```

{@template flutter.rendering.SliverConstraints.precedingScrollExtent} The scroll distance that has been consumed by all [RenderSliver]s that came before this [RenderSliver].

# Edge Cases

[RenderSliver]s often lazily create their internal content as layout occurs, e.g., [SliverList]. In this case, when [RenderSliver]s exceed the viewport, their children are built lazily, and the [RenderSliver] does not have enough information to estimate its total extent, [precedingScrollExtent] will be [double.infinity] for all [RenderSliver]s that appear after the lazily constructed child. This is because a total [SliverGeometry.scrollExtent] cannot be calculated unless all inner children have been created and sized, or the number of children and estimated extents are provided. The infinite [SliverGeometry.scrollExtent] will become finite as soon as enough information is available to estimate the overall extent of all children within the given [RenderSliver].

[RenderSliver]s may legitimately be infinite, meaning that they can scroll content forever without reaching the end. For any [RenderSliver]s that appear after the infinite [RenderSliver], the [precedingScrollExtent] will be [double.infinity]. {@endtemplate}

### overlap

```dart
double overlap
```

The number of pixels from where the pixels corresponding to the [scrollOffset] will be painted up to the first pixel that has not yet been painted on by an earlier sliver, in the [axisDirection].

For example, if the previous sliver had a [SliverGeometry.paintExtent] of 100.0 pixels but a [SliverGeometry.layoutExtent] of only 50.0 pixels, then the [overlap] of this sliver will be 50.0.

This is typically ignored unless the sliver is itself going to be pinned or floating and wants to avoid doing so under the previous sliver.

### remainingPaintExtent

```dart
double remainingPaintExtent
```

The number of pixels of content that the sliver should consider providing. (Providing more pixels than this is inefficient.)

The actual number of pixels provided should be specified in the [RenderSliver.geometry] as [SliverGeometry.paintExtent].

This value may be infinite, for example if the viewport is an unconstrained [RenderShrinkWrappingViewport].

This value may be 0.0, for example if the sliver is scrolled off the bottom of a downwards vertical viewport.

### crossAxisExtent

```dart
double crossAxisExtent
```

The number of pixels in the cross-axis.

For a vertical list, this is the width of the sliver.

### crossAxisDirection

```dart
AxisDirection crossAxisDirection
```

The direction in which children should be placed in the cross axis.

Typically used in vertical lists to describe whether the ambient [TextDirection] is [TextDirection.rtl] or [TextDirection.ltr].

### viewportMainAxisExtent

```dart
double viewportMainAxisExtent
```

The number of pixels the viewport can display in the main axis.

For a vertical list, this is the height of the viewport.

### cacheOrigin

```dart
double cacheOrigin
```

Where the cache area starts relative to the [scrollOffset].

Slivers that fall into the cache area located before the leading edge and after the trailing edge of the viewport should still render content because they are about to become visible when the user scrolls.

The [cacheOrigin] describes where the [remainingCacheExtent] starts relative to the [scrollOffset]. A cache origin of 0 means that the sliver does not have to provide any content before the current [scrollOffset]. A [cacheOrigin] of -250.0 means that even though the first visible part of the sliver will be at the provided [scrollOffset], the sliver should render content starting 250.0 before the [scrollOffset] to fill the cache area of the viewport.

The [cacheOrigin] is always negative or zero and will never exceed -[scrollOffset]. In other words, a sliver is never asked to provide content before its zero [scrollOffset].

See also:

- [RenderViewport.cacheExtent] for a description of a viewport's cache area.

### remainingCacheExtent

```dart
double remainingCacheExtent
```

Describes how much content the sliver should provide starting from the [cacheOrigin].

Not all content in the [remainingCacheExtent] will be visible as some of it might fall into the cache area of the viewport.

Each sliver should start laying out content at the [cacheOrigin] and try to provide as much content as the [remainingCacheExtent] allows.

The [remainingCacheExtent] is always larger or equal to the [remainingPaintExtent]. Content, that falls in the [remainingCacheExtent], but is outside of the [remainingPaintExtent] is currently not visible in the viewport.

See also:

- [RenderViewport.cacheExtent] for a description of a viewport's cache area.

### axis

```dart
Axis get axis
```

The axis along which the [scrollOffset] and [remainingPaintExtent] are measured.

### normalizedGrowthDirection

```dart
GrowthDirection get normalizedGrowthDirection
```

Return what the [growthDirection] would be if the [axisDirection] was either [AxisDirection.down] or [AxisDirection.right].

This is the same as [growthDirection] unless the [axisDirection] is either [AxisDirection.up] or [AxisDirection.left], in which case it is the opposite growth direction.

This can be useful in combination with [axis] to view the [axisDirection] and [growthDirection] in different terms.

### isTight

```dart
bool get isTight
```

### isNormalized

```dart
bool get isNormalized
```

### asBoxConstraints()

```dart
BoxConstraints asBoxConstraints({double minExtent = 0.0, double maxExtent = double.infinity, double? crossAxisExtent})
```

Returns [BoxConstraints] that reflects the sliver constraints.

The `minExtent` and `maxExtent` are used as the constraints in the main axis. If non-null, the given `crossAxisExtent` is used as a tight constraint in the cross axis. Otherwise, the [crossAxisExtent] from this object is used as a constraint in the cross axis.

Useful for slivers that have [RenderBox] children.

### debugAssertIsValid()

```dart
bool debugAssertIsValid({bool isAppliedConstraint = false, InformationCollector? informationCollector})
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# SliverGeometry

```dart
class SliverGeometry with Diagnosticable {}
```

Describes the amount of space occupied by a [RenderSliver].

A sliver can occupy space in several different ways, which is why this class contains multiple values.

### SliverGeometry()

```dart
SliverGeometry({double scrollExtent = 0.0, double paintExtent = 0.0, double paintOrigin = 0.0, double? layoutExtent, double maxPaintExtent = 0.0, double maxScrollObstructionExtent = 0.0, double? crossAxisExtent, double? hitTestExtent, bool? visible, bool hasVisualOverflow = false, double? scrollOffsetCorrection, double? cacheExtent})
```

Creates an object that describes the amount of space occupied by a sliver.

If the [layoutExtent] argument is null, [layoutExtent] defaults to the [paintExtent]. If the [hitTestExtent] argument is null, [hitTestExtent] defaults to the [paintExtent]. If [visible] is null, [visible] defaults to whether [paintExtent] is greater than zero.

### copyWith()

```dart
SliverGeometry copyWith({double? scrollExtent, double? paintExtent, double? paintOrigin, double? layoutExtent, double? maxPaintExtent, double? maxScrollObstructionExtent, double? crossAxisExtent, double? hitTestExtent, bool? visible, bool? hasVisualOverflow, double? cacheExtent})
```

Creates a copy of this object but with the given fields replaced with the new values.

### zero

```dart
SliverGeometry zero
```

A sliver that occupies no space at all.

### scrollExtent

```dart
double scrollExtent
```

The (estimated) total scrollable extent that this sliver has content for.

This is the amount of scrolling the user needs to do to get from the beginning of this sliver to the end of this sliver.

The value is used to calculate the [SliverConstraints.scrollOffset] of all slivers in the scrollable and thus should be provided whether the sliver is currently in the viewport or not.

In a typical scrolling scenario, the [scrollExtent] is constant for a sliver throughout the scrolling while [paintExtent] and [layoutExtent] will progress from `0` when offscreen to between `0` and [scrollExtent] as the sliver scrolls partially into and out of the screen and is equal to [scrollExtent] while the sliver is entirely on screen. However, these relationships can be customized to achieve more special effects.

This value must be accurate if the [paintExtent] is less than the [SliverConstraints.remainingPaintExtent] provided during layout.

### paintOrigin

```dart
double paintOrigin
```

The visual location of the first visible part of this sliver relative to its layout position.

For example, if the sliver wishes to paint visually before its layout position, the [paintOrigin] is negative. The coordinate system this sliver uses for painting is relative to this [paintOrigin]. In other words, when [RenderSliver.paint] is called, the (0, 0) position of the [Offset] given to it is at this [paintOrigin].

The coordinate system used for the [paintOrigin] itself is relative to the start of this sliver's layout position rather than relative to its current position on the viewport. In other words, in a typical scrolling scenario, [paintOrigin] remains constant at 0.0 rather than tracking from 0.0 to [SliverConstraints.viewportMainAxisExtent] as the sliver scrolls past the viewport.

This value does not affect the layout of subsequent slivers. The next sliver is still placed at [layoutExtent] after this sliver's layout position. This value does affect where the [paintExtent] extent is measured from when computing the [SliverConstraints.overlap] for the next sliver.

Defaults to 0.0, which means slivers start painting at their layout position by default.

### paintExtent

```dart
double paintExtent
```

The amount of currently visible visual space that was taken by the sliver to render the subset of the sliver that covers all or part of the [SliverConstraints.remainingPaintExtent] in the current viewport.

This value does not affect how the next sliver is positioned. In other words, if this value was 100 and [layoutExtent] was 0, typical slivers placed after it would end up drawing in the same 100 pixel space while painting.

This must be between zero and [SliverConstraints.remainingPaintExtent].

This value is typically 0 when outside of the viewport and grows or shrinks from 0 or to 0 as the sliver is being scrolled into and out of the viewport unless the sliver wants to achieve a special effect and paint even when scrolled away.

This contributes to the calculation for the next sliver's [SliverConstraints.overlap].

### layoutExtent

```dart
double layoutExtent
```

The distance from the first visible part of this sliver to the first visible part of the next sliver, assuming the next sliver's [SliverConstraints.scrollOffset] is zero.

This must be between zero and [paintExtent]. It defaults to [paintExtent].

This value is typically 0 when outside of the viewport and grows or shrinks from 0 or to 0 as the sliver is being scrolled into and out of the viewport unless the sliver wants to achieve a special effect and push down the layout start position of subsequent slivers before the sliver is even scrolled into the viewport.

### maxPaintExtent

```dart
double maxPaintExtent
```

The (estimated) total paint extent that this sliver would be able to provide if the [SliverConstraints.remainingPaintExtent] was infinite.

This is used by viewports that implement shrink-wrapping.

By definition, this cannot be less than [paintExtent].

### maxScrollObstructionExtent

```dart
double maxScrollObstructionExtent
```

The maximum extent by which this sliver can reduce the area in which content can scroll if the sliver were pinned at the edge.

Slivers that never get pinned at the edge, should return zero.

A pinned app bar is an example for a sliver that would use this setting: When the app bar is pinned to the top, the area in which content can actually scroll is reduced by the height of the app bar.

### hitTestExtent

```dart
double hitTestExtent
```

The distance from where this sliver started painting to the bottom of where it should accept hits.

This must be between zero and [paintExtent]. It defaults to [paintExtent].

### visible

```dart
bool visible
```

Whether this sliver should be painted.

By default, this is true if [paintExtent] is greater than zero, and false if [paintExtent] is zero.

### hasVisualOverflow

```dart
bool hasVisualOverflow
```

Whether this sliver has visual overflow.

By default, this is false, which means the viewport does not need to clip its children. If any slivers have visual overflow, the viewport will apply a clip to its children.

### scrollOffsetCorrection

```dart
double? scrollOffsetCorrection
```

If this is non-zero after [RenderSliver.performLayout] returns, the scroll offset will be adjusted by the parent and then the entire layout of the parent will be rerun.

When the value is non-zero, the [RenderSliver] does not need to compute the rest of the values when constructing the [SliverGeometry] or call [RenderObject.layout] on its children since [RenderSliver.performLayout] will be called again on this sliver in the same frame after the [SliverConstraints.scrollOffset] correction has been applied, when the proper [SliverGeometry] and layout of its children can be computed.

If the parent is also a [RenderSliver], it must propagate this value in its own [RenderSliver.geometry] property until a viewport which adjusts its offset based on this value.

### cacheExtent

```dart
double cacheExtent
```

How many pixels the sliver has consumed in the [SliverConstraints.remainingCacheExtent].

This value should be equal to or larger than the [layoutExtent] because the sliver always consumes at least the [layoutExtent] from the [SliverConstraints.remainingCacheExtent] and possibly more if it falls into the cache area of the viewport.

See also:

- [RenderViewport.cacheExtent] for a description of a viewport's cache area.

### crossAxisExtent

```dart
double? crossAxisExtent
```

The amount of space allocated to the cross axis.

This value will be typically null unless it is different from [SliverConstraints.crossAxisExtent]. If null, then the cross axis extent of the sliver is assumed to be the same as the [SliverConstraints.crossAxisExtent]. This is because slivers typically consume all of the extent that is available in the cross axis.

See also:

- [SliverConstrainedCrossAxis] for an example of a sliver which takes up a smaller cross axis extent than the provided constraint.
- [SliverCrossAxisGroup] for an example of a sliver which makes use of this [crossAxisExtent] to lay out their children.

### debugAssertIsValid()

```dart
bool debugAssertIsValid({InformationCollector? informationCollector})
```

Asserts that this geometry is internally consistent.

Does nothing if asserts are disabled. Always returns true.

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverHitTest

```dart
typedef SliverHitTest = bool Function(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

Method signature for hit testing a [RenderSliver].

Used by [SliverHitTestResult.addWithAxisOffset] to hit test [RenderSliver] children.

See also:

- [RenderSliver.hitTest], which documents more details around hit testing [RenderSliver]s.

# SliverHitTestResult

```dart
class SliverHitTestResult extends HitTestResult {}
```

The result of performing a hit test on [RenderSliver]s.

An instance of this class is provided to [RenderSliver.hitTest] to record the result of the hit test.

### SliverHitTestResult()

```dart
SliverHitTestResult()
```

Creates an empty hit test result for hit testing on [RenderSliver].

### SliverHitTestResult.wrap()

```dart
SliverHitTestResult.wrap(dynamic result)
```

Wraps `result` to create a [HitTestResult] that implements the [SliverHitTestResult] protocol for hit testing on [RenderSliver]s.

This method is used by [RenderObject]s that adapt between the [RenderSliver]-world and the non-[RenderSliver]-world to convert a (subtype of) [HitTestResult] to a [SliverHitTestResult] for hit testing on [RenderSliver]s.

The [HitTestEntry] instances added to the returned [SliverHitTestResult] are also added to the wrapped `result` (both share the same underlying data structure to store [HitTestEntry] instances).

See also:

- [HitTestResult.wrap], which turns a [SliverHitTestResult] back into a generic [HitTestResult].
- [BoxHitTestResult.wrap], which turns a [SliverHitTestResult] into a [BoxHitTestResult] for hit testing on [RenderBox] children.

### addWithAxisOffset()

```dart
bool addWithAxisOffset({required Offset? paintOffset, required double mainAxisOffset, required double crossAxisOffset, required double mainAxisPosition, required double crossAxisPosition, required SliverHitTest hitTest})
```

Transforms `mainAxisPosition` and `crossAxisPosition` to the local coordinate system of a child for hit-testing the child.

The actual hit testing of the child needs to be implemented in the provided `hitTest` callback, which is invoked with the transformed `position` as argument.

For the transform `mainAxisOffset` is subtracted from `mainAxisPosition` and `crossAxisOffset` is subtracted from `crossAxisPosition`.

The `paintOffset` describes how the paint position of a point painted at the provided `mainAxisPosition` and `crossAxisPosition` would change after `mainAxisOffset` and `crossAxisOffset` have been applied. This `paintOffset` is used to properly convert [PointerEvent]s to the local coordinate system of the event receiver.

The `paintOffset` may be null if `mainAxisOffset` and `crossAxisOffset` are both zero.

The function returns the return value of `hitTest`.

# SliverHitTestEntry

```dart
class SliverHitTestEntry extends HitTestEntry<RenderSliver> {}
```

A hit test entry used by [RenderSliver].

The coordinate system used by this hit test entry is relative to the [AxisDirection] of the target sliver.

### SliverHitTestEntry()

```dart
SliverHitTestEntry(dynamic target, {required double mainAxisPosition, required double crossAxisPosition})
```

Creates a sliver hit test entry.

### mainAxisPosition

```dart
double mainAxisPosition
```

The distance in the [AxisDirection] from the edge of the sliver's painted area (as given by the [SliverConstraints.scrollOffset]) to the hit point. This can be an unusual direction, for example in the [AxisDirection.up] case this is a distance from the _bottom_ of the sliver's painted area.

### crossAxisPosition

```dart
double crossAxisPosition
```

The distance to the hit point in the axis opposite the [SliverConstraints.axis].

If the cross axis is horizontal (i.e. the [SliverConstraints.axisDirection] is either [AxisDirection.down] or [AxisDirection.up]), then the [crossAxisPosition] is a distance from the left edge of the sliver. If the cross axis is vertical (i.e. the [SliverConstraints.axisDirection] is either [AxisDirection.right] or [AxisDirection.left]), then the [crossAxisPosition] is a distance from the top edge of the sliver.

This is always a distance from the left or top of the parent, never a distance from the right or bottom.

### toString()

```dart
String toString()
```

# SliverLogicalParentData

```dart
class SliverLogicalParentData extends ParentData {}
```

Parent data structure used by parents of slivers that position their children using layout offsets.

This data structure is optimized for fast layout. It is best used by parents that expect to have many children whose relative positions don't change even when the scroll offset does.

### layoutOffset

```dart
double? layoutOffset
```

The position of the child relative to the zero scroll offset.

The number of pixels from the zero scroll offset of the parent sliver (the line at which its [SliverConstraints.scrollOffset] is zero) to the side of the child closest to that offset. A [layoutOffset] can be null when it cannot be determined. The value will be set after layout.

In a typical list, this does not change as the parent is scrolled.

Defaults to null.

### toString()

```dart
String toString()
```

# SliverLogicalContainerParentData

```dart
class SliverLogicalContainerParentData extends SliverLogicalParentData with ContainerParentDataMixin<RenderSliver> {}
```

Parent data for slivers that have multiple children and that position their children using layout offsets.

# SliverPhysicalParentData

```dart
class SliverPhysicalParentData extends ParentData {}
```

Parent data structure used by parents of slivers that position their children using absolute coordinates.

For example, used by [RenderViewport].

This data structure is optimized for fast painting, at the cost of requiring additional work during layout when the children change their offsets. It is best used by parents that expect to have few children, especially if those children will themselves be very tall relative to the parent.

### paintOffset

```dart
Offset paintOffset
```

The position of the child relative to the parent.

This is the distance from the top left visible corner of the parent to the top left visible corner of the sliver.

### crossAxisFlex

```dart
int? crossAxisFlex
```

The [crossAxisFlex] factor to use for this sliver child.

If used outside of a [SliverCrossAxisGroup] widget, this value has no meaning.

If null or zero, the child is inflexible and determines its own size in the cross axis. If non-zero, the amount of space the child can occupy in the cross axis is determined by dividing the free space (after placing the inflexible children) according to the flex factors of the flexible children.

This value is only used by the [SliverCrossAxisGroup] widget to determine how to allocate its [SliverConstraints.crossAxisExtent] to its children.

See also:

- [SliverCrossAxisGroup], which lays out multiple slivers along the cross axis direction.

### applyPaintTransform()

```dart
void applyPaintTransform(Matrix4 transform)
```

Apply the [paintOffset] to the given [transform].

Used to implement [RenderObject.applyPaintTransform] by slivers that use [SliverPhysicalParentData].

### toString()

```dart
String toString()
```

# SliverPhysicalContainerParentData

```dart
class SliverPhysicalContainerParentData extends SliverPhysicalParentData with ContainerParentDataMixin<RenderSliver> {}
```

Parent data for slivers that have multiple children and that position their children using absolute coordinates.

# RenderSliver

```dart
abstract class RenderSliver extends RenderObject {}
```

Base class for the render objects that implement scroll effects in viewports.

A [RenderViewport] has a list of child slivers. Each sliver — literally a slice of the viewport's contents — is laid out in turn, covering the viewport in the process. (Every sliver is laid out each time, including those that have zero extent because they are "scrolled off" or are beyond the end of the viewport.)

Slivers participate in the _sliver protocol_, wherein during [layout] each sliver receives a [SliverConstraints] object and computes a corresponding [SliverGeometry] that describes where it fits in the viewport. This is analogous to the box protocol used by [RenderBox], which gets a [BoxConstraints] as input and computes a [Size].

Slivers have a leading edge, which is where the position described by [SliverConstraints.scrollOffset] for this sliver begins. Slivers have several dimensions, the primary of which is [SliverGeometry.paintExtent], which describes the extent of the sliver along the main axis, starting from the leading edge, reaching either the end of the viewport or the end of the sliver, whichever comes first.

Slivers can change dimensions based on the changing constraints in a non-linear fashion, to achieve various scroll effects. For example, the various [RenderSliverPersistentHeader] subclasses, on which [SliverAppBar] is based, achieve effects such as staying visible despite the scroll offset, or reappearing at different offsets based on the user's scroll direction ([SliverConstraints.userScrollDirection]).

{@youtube 560 315 https://www.youtube.com/watch?v=Mz3kHQxBjGg}

## Writing a RenderSliver subclass

Slivers can have sliver children, or children from another coordinate system, typically box children. (For details on the box protocol, see [RenderBox].) Slivers can also have different child models, typically having either one child, or a list of children.

### Examples of slivers

A good example of a sliver with a single child that is also itself a sliver is [RenderSliverPadding], which indents its child. A sliver-to-sliver render object such as this must construct a [SliverConstraints] object for its child, then must take its child's [SliverGeometry] and use it to form its own [geometry].

The other common kind of one-child sliver is a sliver that has a single [RenderBox] child. An example of that would be [RenderSliverToBoxAdapter], which lays out a single box and sizes itself around the box. Such a sliver must use its [SliverConstraints] to create a [BoxConstraints] for the child, lay the child out (using the child's [layout] method), and then use the child's [RenderBox.size] to generate the sliver's [SliverGeometry].

The most common kind of sliver though is one with multiple children. The most straight-forward example of this is [RenderSliverList], which arranges its children one after the other in the main axis direction. As with the one-box-child sliver case, it uses its [constraints] to create a [BoxConstraints] for the children, and then it uses the aggregate information from all its children to generate its [geometry]. Unlike the one-child cases, however, it is judicious in which children it actually lays out (and later paints). If the scroll offset is 1000 pixels, and it previously determined that the first three children are each 400 pixels tall, then it will skip the first two and start the layout with its third child.

### Layout

As they are laid out, slivers decide their [geometry], which includes their size ([SliverGeometry.paintExtent]) and the position of the next sliver ([SliverGeometry.layoutExtent]), as well as the position of each of their children, based on the input [constraints] from the viewport such as the scroll offset ([SliverConstraints.scrollOffset]).

For example, a sliver that just paints a box 100 pixels high would say its [SliverGeometry.paintExtent] was 100 pixels when the scroll offset was zero, but would say its [SliverGeometry.paintExtent] was 25 pixels when the scroll offset was 75 pixels, and would say it was zero when the scroll offset was 100 pixels or more. (This is assuming that [SliverConstraints.remainingPaintExtent] was more than 100 pixels.)

The various dimensions that are provided as input to this system are in the [constraints]. They are described in detail in the documentation for the [SliverConstraints] class.

The [performLayout] function must take these [constraints] and create a [SliverGeometry] object that it must then assign to the [geometry] property. The different dimensions of the geometry that can be configured are described in detail in the documentation for the [SliverGeometry] class.

### Painting

In addition to implementing layout, a sliver must also implement painting. This is achieved by overriding the [paint] method.

The [paint] method is called with an [Offset] from the [Canvas] origin to the top-left corner of the sliver, _regardless of the axis direction_.

Subclasses should also override [applyPaintTransform] to provide the [Matrix4] describing the position of each child relative to the sliver. (This is used by, among other things, the accessibility layer, to determine the bounds of the child.)

### Hit testing

To implement hit testing, either override the [hitTestSelf] and [hitTestChildren] methods, or, for more complex cases, instead override the [hitTest] method directly.

To actually react to pointer events, the [handleEvent] method may be implemented. By default it does nothing. (Typically gestures are handled by widgets in the box protocol, not by slivers directly.)

### Helper methods

There are a number of methods that a sliver should implement which will make the other methods easier to implement. Each method listed below has detailed documentation. In addition, the [RenderSliverHelpers] class can be used to mix in some helpful methods.

#### childScrollOffset

If the subclass positions children anywhere other than at scroll offset zero, it should override [childScrollOffset]. For example, [RenderSliverList] and [RenderSliverGrid] override this method, but [RenderSliverToBoxAdapter] does not.

This is used by, among other things, [Scrollable.ensureVisible].

#### childMainAxisPosition

Subclasses should implement [childMainAxisPosition] to describe where their children are positioned.

#### childCrossAxisPosition

If the subclass positions children in the cross-axis at a position other than zero, then it should override [childCrossAxisPosition]. For example [RenderSliverGrid] overrides this method.

### ensureSemantics

```dart
bool get ensureSemantics
```

Whether this sliver should be included in the semantics tree.

This value is used by [RenderViewportBase] to ensure a sliver is included in the semantics tree regardless of its geometry.

A [RenderSliver] should override this value to `true` to ensure its child is included in the semantics tree. For example if your sliver is under a [RenderViewport] you may want to wrap it with a [SliverEnsureSemantics] to ensure that:

1.  It is still visited by [RenderViewportBase.visitChildrenForSemantics] regardless of its geometry. This includes cases where your sliver is outside the current viewport and cache extent.
2.  Its semantic information is not clipped out by the [RenderViewport] in [RenderViewportBase.describeSemanticsClip] or [RenderViewportBase.describeApproximatePaintClip].

If a given [RenderSliver] does not provide a valid [semanticBounds] it will still be dropped from the semantics tree.

Defaults to `false`.

### constraints

```dart
SliverConstraints get constraints
```

### geometry

```dart
SliverGeometry? get geometry
```

The amount of space this sliver occupies.

This value is stale whenever this object is marked as needing layout. During [performLayout], do not read the [geometry] of a child unless you pass true for parentUsesSize when calling the child's [layout] function.

The geometry of a sliver should be set only during the sliver's [performLayout] or [performResize] functions. If you wish to change the geometry of a sliver outside of those functions, call [markNeedsLayout] instead to schedule a layout of the sliver.

### geometry

```dart
set geometry(SliverGeometry? value)
```

### semanticBounds

```dart
Rect get semanticBounds
```

### paintBounds

```dart
Rect get paintBounds
```

### debugResetSize()

```dart
void debugResetSize()
```

### debugAssertDoesMeetConstraints()

```dart
void debugAssertDoesMeetConstraints()
```

### performResize()

```dart
void performResize()
```

### centerOffsetAdjustment

```dart
double get centerOffsetAdjustment
```

For a center sliver, the distance before the absolute zero scroll offset that this sliver can cover.

For example, if an [AxisDirection.down] viewport with an [RenderViewport.anchor] of 0.5 has a single sliver with a height of 100.0 and its [centerOffsetAdjustment] returns 50.0, then the sliver will be centered in the viewport when the scroll offset is 0.0.

The distance here is in the opposite direction of the [RenderViewport.axisDirection], so values will typically be positive.

### hitTest()

```dart
bool hitTest(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

Determines the set of render objects located at the given position.

Returns true if the given point is contained in this render object or one of its descendants. Adds any render objects that contain the point to the given hit test result.

The caller is responsible for providing the position in the local coordinate space of the callee. The callee is responsible for checking whether the given position is within its bounds.

Hit testing requires layout to be up-to-date but does not require painting to be up-to-date. That means a render object can rely upon [performLayout] having been called in [hitTest] but cannot rely upon [paint] having been called. For example, a render object might be a child of a [RenderOpacity] object, which calls [hitTest] on its children when its opacity is zero even though it does not [paint] its children.

## Coordinates for RenderSliver objects

The `mainAxisPosition` is the distance in the [AxisDirection] (after applying the [GrowthDirection]) from the edge of the sliver's painted area. This can be an unusual direction, for example in the [AxisDirection.up] case this is a distance from the _bottom_ of the sliver's painted area.

The `crossAxisPosition` is the distance in the other axis. If the cross axis is horizontal (i.e. the [SliverConstraints.axisDirection] is either [AxisDirection.down] or [AxisDirection.up]), then the `crossAxisPosition` is a distance from the left edge of the sliver. If the cross axis is vertical (i.e. the [SliverConstraints.axisDirection] is either [AxisDirection.right] or [AxisDirection.left]), then the `crossAxisPosition` is a distance from the top edge of the sliver.

## Implementing hit testing for slivers

The most straight-forward way to implement hit testing for a new sliver render object is to override its [hitTestSelf] and [hitTestChildren] methods.

### hitTestSelf()

```dart
bool hitTestSelf({required double mainAxisPosition, required double crossAxisPosition})
```

Override this method if this render object can be hit even if its children were not hit.

Used by [hitTest]. If you override [hitTest] and do not call this function, then you don't need to implement this function.

For a discussion of the semantics of the arguments, see [hitTest].

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

Override this method to check whether any children are located at the given position.

Typically children should be hit-tested in reverse paint order so that hit tests at locations where children overlap hit the child that is visually "on top" (i.e., paints later).

Used by [hitTest]. If you override [hitTest] and do not call this function, then you don't need to implement this function.

For a discussion of the semantics of the arguments, see [hitTest].

### calculatePaintOffset()

```dart
double calculatePaintOffset(SliverConstraints constraints, {required double from, required double to})
```

Computes the portion of the region from `from` to `to` that is visible, assuming that only the region from the [SliverConstraints.scrollOffset] that is [SliverConstraints.remainingPaintExtent] high is visible, and that the relationship between scroll offsets and paint offsets is linear.

For example, if the constraints have a scroll offset of 100 and a remaining paint extent of 100, and the arguments to this method describe the region 50..150, then the returned value would be 50 (from scroll offset 100 to scroll offset 150).

This method is not useful if there is not a 1:1 relationship between consumed scroll offset and consumed paint extent. For example, if the sliver always paints the same amount but consumes a scroll offset extent that is proportional to the [SliverConstraints.scrollOffset], then this function's results will not be consistent.

### calculateCacheOffset()

```dart
double calculateCacheOffset(SliverConstraints constraints, {required double from, required double to})
```

Computes the portion of the region from `from` to `to` that is within the cache extent of the viewport, assuming that only the region from the [SliverConstraints.cacheOrigin] that is [SliverConstraints.remainingCacheExtent] high is visible, and that the relationship between scroll offsets and paint offsets is linear.

This method is not useful if there is not a 1:1 relationship between consumed scroll offset and consumed cache extent.

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderObject child)
```

Returns the distance from the leading _visible_ edge of the sliver to the side of the given child closest to that edge.

For example, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.down], then this is the distance from the top of the visible portion of the sliver to the top of the child. On the other hand, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.up], then this is the distance from the bottom of the visible portion of the sliver to the bottom of the child. In both cases, this is the direction of increasing [SliverConstraints.scrollOffset] and [SliverLogicalParentData.layoutOffset].

For children that are [RenderSliver]s, the leading edge of the _child_ will be the leading _visible_ edge of the child, not the part of the child that would locally be a scroll offset 0.0. For children that are not [RenderSliver]s, for example a [RenderBox] child, it's the actual distance to the edge of the box, since those boxes do not know how to handle being scrolled.

This method differs from [childScrollOffset] in that [childMainAxisPosition] gives the distance from the leading _visible_ edge of the sliver whereas [childScrollOffset] gives the distance from the sliver's zero scroll offset.

Calling this for a child that is not visible is not valid.

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderObject child)
```

Returns the distance along the cross axis from the zero of the cross axis in this sliver's [paint] coordinate space to the nearest side of the given child.

For example, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.down], then this is the distance from the left of the sliver to the left of the child. Similarly, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.up], then this is value is the same. If the axis direction is [AxisDirection.left] or [AxisDirection.right], then it is the distance from the top of the sliver to the top of the child.

Calling this for a child that is not visible is not valid.

### childScrollOffset()

```dart
double? childScrollOffset(RenderObject child)
```

Returns the scroll offset for the leading edge of the given child.

The `child` must be a child of this sliver.

If there are pinned slivers before [child], the offset should be reduced by the extent of the pinned children. This can occur in [RenderSliver]s that have multiple sliver children, such as [RenderSliverMainAxisGroup].

This method differs from [childMainAxisPosition] in that [childMainAxisPosition] gives the distance from the leading _visible_ edge of the sliver whereas [childScrollOffset] gives the distance from sliver's zero scroll offset.

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### getAbsoluteSizeRelativeToOrigin()

```dart
Size getAbsoluteSizeRelativeToOrigin()
```

This returns a [Size] with dimensions relative to the leading edge of the sliver, specifically the same offset that is given to the [paint] method. This means that the dimensions may be negative.

This is only valid after [layout] has completed.

See also:

- [getAbsoluteSize], which returns absolute size.

### getAbsoluteSize()

```dart
Size getAbsoluteSize()
```

This returns the absolute [Size] of the sliver.

The dimensions are always positive and calling this is only valid after [layout] has completed.

See also:

- [getAbsoluteSizeRelativeToOrigin], which returns the size relative to the leading edge of the sliver.

### getMaxPaintRect()

```dart
Rect getMaxPaintRect()
```

Returns the [Rect] that covers the total paint extent of the sliver.

[Rect] is expressed in the [RenderSliver]'s local coordinate system, which is axis-aligned with the [PaintingContext]'s canvas. The coordinate system's origin (0,0) corresponds to the `offset` argument passed to the [paint] method.

### debugPaint()

```dart
void debugPaint(PaintingContext context, Offset offset)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event, SliverHitTestEntry entry)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverHelpers

```dart
mixin RenderSliverHelpers implements RenderSliver {}
```

Mixin for [RenderSliver] subclasses that provides some utility functions.

### hitTestBoxChild()

```dart
bool hitTestBoxChild(BoxHitTestResult result, RenderBox child, {required double mainAxisPosition, required double crossAxisPosition})
```

Utility function for [hitTestChildren] for use when the children are [RenderBox] widgets.

This function takes care of converting the position from the sliver coordinate system to the Cartesian coordinate system used by [RenderBox].

This function relies on [childMainAxisPosition] to determine the position of child in question.

Calling this for a child that is not visible is not valid.

### applyPaintTransformForBoxChild()

```dart
void applyPaintTransformForBoxChild(RenderBox child, Matrix4 transform)
```

Utility function for [applyPaintTransform] for use when the children are [RenderBox] widgets.

This function turns the value returned by [childMainAxisPosition] and [childCrossAxisPosition]for the child in question into a translation that it then applies to the given matrix.

Calling this for a child that is not visible is not valid.

# RenderSliverSingleBoxAdapter

```dart
abstract class RenderSliverSingleBoxAdapter extends RenderSliver with RenderObjectWithChildMixin<RenderBox>, RenderSliverHelpers {}
```

An abstract class for [RenderSliver]s that contains a single [RenderBox].

See also:

- [RenderSliver], which explains more about the Sliver protocol.
- [RenderBox], which explains more about the Box protocol.
- [RenderSliverToBoxAdapter], which extends this class to size the child according to its preferred size.
- [RenderSliverFillRemaining], which extends this class to size the child to fill the remaining space in the viewport.

### RenderSliverSingleBoxAdapter()

```dart
RenderSliverSingleBoxAdapter({RenderBox? child})
```

Creates a [RenderSliver] that wraps a [RenderBox].

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### setChildParentData()

```dart
void setChildParentData(RenderObject child, SliverConstraints constraints, SliverGeometry geometry)
```

Sets the [SliverPhysicalParentData.paintOffset] for the given child according to the [SliverConstraints.axisDirection] and [SliverConstraints.growthDirection] and the given geometry.

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderBox child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

# RenderSliverToBoxAdapter

```dart
class RenderSliverToBoxAdapter extends RenderSliverSingleBoxAdapter {}
```

A [RenderSliver] that contains a single [RenderBox].

The child will not be laid out if it is not visible. It is sized according to the child's preferences in the main axis, and with a tight constraint forcing it to the dimensions of the viewport in the cross axis.

See also:

- [RenderSliver], which explains more about the Sliver protocol.
- [RenderBox], which explains more about the Box protocol.
- [RenderViewport], which allows [RenderSliver] objects to be placed inside a [RenderBox] (the opposite of this class).

### RenderSliverToBoxAdapter()

```dart
RenderSliverToBoxAdapter({RenderBox? child})
```

Creates a [RenderSliver] that wraps a [RenderBox].

### performLayout()

```dart
void performLayout()
```
