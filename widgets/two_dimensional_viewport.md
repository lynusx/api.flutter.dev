@docImport 'primary_scroll_controller.dart'; @docImport 'scrollable.dart'; @docImport 'two_dimensional_scroll_view.dart'; @docImport 'viewport.dart';

# TwoDimensionalIndexedWidgetBuilder

```dart
typedef TwoDimensionalIndexedWidgetBuilder = Widget? Function(BuildContext context, ChildVicinity vicinity)
```

Signature for a function that creates a widget for a given [ChildVicinity], e.g., in a [TwoDimensionalScrollView], but may return null.

Used by [TwoDimensionalChildBuilderDelegate.builder] and other APIs that use lazily-generated widgets where the child count may not be known ahead of time.

Unlike most builders, this callback can return null, indicating the [ChildVicinity.xIndex] or [ChildVicinity.yIndex] is out of range. Whether and when this is valid depends on the semantics of the builder. For example, [TwoDimensionalChildBuilderDelegate.builder] returns null when one or both of the indices is out of range, where the range is defined by the [TwoDimensionalChildBuilderDelegate.maxXIndex] or [TwoDimensionalChildBuilderDelegate.maxYIndex]; so in that case the vicinity values may determine whether returning null is valid or not.

See also:

- [WidgetBuilder], which is similar but only takes a [BuildContext].
- [NullableIndexedWidgetBuilder], which is similar but may return null.
- [IndexedWidgetBuilder], which is similar but not nullable.

# TwoDimensionalViewport

```dart
abstract class TwoDimensionalViewport extends RenderObjectWidget {}
```

A widget through which a portion of larger content can be viewed, typically in combination with a [TwoDimensionalScrollable].

[TwoDimensionalViewport] is the visual workhorse of the two dimensional scrolling machinery. It displays a subset of its children according to its own dimensions and the given [horizontalOffset] an [verticalOffset]. As the offsets vary, different children are visible through the viewport.

Subclasses must implement [createRenderObject] and [updateRenderObject]. Both of these methods require the render object to be a subclass of [RenderTwoDimensionalViewport]. This class will create its own [RenderObjectElement] which already implements the [TwoDimensionalChildManager], which means subclasses should cast the [BuildContext] to provide as the child manager to the [RenderTwoDimensionalViewport].

{@tool snippet} This is an example of a subclass implementation of [TwoDimensionalViewport], `SimpleTwoDimensionalViewport`. The `RenderSimpleTwoDimensionalViewport` is a subclass of [RenderTwoDimensionalViewport].

```dart
class SimpleTwoDimensionalViewport extends TwoDimensionalViewport {
  const SimpleTwoDimensionalViewport({
    super.key,
    required super.verticalOffset,
    required super.verticalAxisDirection,
    required super.horizontalOffset,
    required super.horizontalAxisDirection,
    required super.delegate,
    required super.mainAxis,
    super.scrollCacheExtent,
    super.clipBehavior = Clip.hardEdge,
  });

  @override
  RenderSimpleTwoDimensionalViewport createRenderObject(BuildContext context) {
    return RenderSimpleTwoDimensionalViewport(
      horizontalOffset: horizontalOffset,
      horizontalAxisDirection: horizontalAxisDirection,
      verticalOffset: verticalOffset,
      verticalAxisDirection: verticalAxisDirection,
      mainAxis: mainAxis,
      delegate: delegate,
      childManager: context as TwoDimensionalChildManager,
      scrollCacheExtent: scrollCacheExtent,
      clipBehavior: clipBehavior,
    );
  }

  @override
  void updateRenderObject(BuildContext context, RenderSimpleTwoDimensionalViewport renderObject) {
    renderObject
      ..horizontalOffset = horizontalOffset
      ..horizontalAxisDirection = horizontalAxisDirection
      ..verticalOffset = verticalOffset
      ..verticalAxisDirection = verticalAxisDirection
      ..mainAxis = mainAxis
      ..delegate = delegate
      ..scrollCacheExtent = scrollCacheExtent
      ..clipBehavior = clipBehavior;
  }
}
```

{@end-tool}

See also:

- [Viewport], the equivalent of this widget that scrolls in only one dimension.

### TwoDimensionalViewport()

```dart
TwoDimensionalViewport({dynamic key, required ViewportOffset verticalOffset, required AxisDirection verticalAxisDirection, required ViewportOffset horizontalOffset, required AxisDirection horizontalAxisDirection, required TwoDimensionalChildDelegate delegate, required Axis mainAxis, double? cacheExtent, CacheExtentStyle? cacheExtentStyle, ScrollCacheExtent? scrollCacheExtent, Clip clipBehavior = Clip.hardEdge})
```

Creates a viewport for [RenderBox] objects that extend and scroll in both horizontal and vertical dimensions.

The viewport listens to the [horizontalOffset] and [verticalOffset], which means this widget does not need to be rebuilt when the offsets change.

### verticalOffset

```dart
ViewportOffset verticalOffset
```

Which part of the content inside the viewport should be visible in the vertical axis.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport vertically, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### verticalAxisDirection

```dart
AxisDirection verticalAxisDirection
```

The direction in which the [verticalOffset]'s [ViewportOffset.pixels] increases.

For example, if the axis direction is [AxisDirection.down], a scroll offset of zero is at the top of the viewport and increases towards the bottom of the viewport.

Must be either [AxisDirection.down] or [AxisDirection.up] in correlation with an [Axis.vertical].

### horizontalOffset

```dart
ViewportOffset horizontalOffset
```

Which part of the content inside the viewport should be visible in the horizontal axis.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport horizontally, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### horizontalAxisDirection

```dart
AxisDirection horizontalAxisDirection
```

The direction in which the [horizontalOffset]'s [ViewportOffset.pixels] increases.

For example, if the axis direction is [AxisDirection.right], a scroll offset of zero is at the left of the viewport and increases towards the right of the viewport.

Must be either [AxisDirection.left] or [AxisDirection.right] in correlation with an [Axis.horizontal].

### mainAxis

```dart
Axis mainAxis
```

The main axis of the two.

Used to determine the paint order of the children of the viewport. When the main axis is [Axis.vertical], children will be painted in row major order, according to their associated [ChildVicinity]. When the main axis is [Axis.horizontal], the children will be painted in column major order.

### cacheExtent

```dart
double? cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

### cacheExtentStyle

```dart
CacheExtentStyle? cacheExtentStyle
```

{@macro flutter.rendering.RenderViewportBase.cacheExtentStyle}

### scrollCacheExtent

```dart
ScrollCacheExtent? scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

### delegate

```dart
TwoDimensionalChildDelegate delegate
```

A delegate that provides the children for the [TwoDimensionalViewport].

### createElement()

```dart
RenderObjectElement createElement()
```

### createRenderObject()

```dart
RenderTwoDimensionalViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderTwoDimensionalViewport renderObject)
```

# TwoDimensionalViewportParentData

```dart
class TwoDimensionalViewportParentData extends ParentData with KeepAliveParentDataMixin {}
```

Parent data structure used by [RenderTwoDimensionalViewport].

The parent data primarily describes where a child is in the viewport. The [layoutOffset] must be set by subclasses of [RenderTwoDimensionalViewport], during [RenderTwoDimensionalViewport.layoutChildSequence] which represents the position of the child in the viewport.

The [paintOffset] is computed by [RenderTwoDimensionalViewport] after [RenderTwoDimensionalViewport.layoutChildSequence]. If subclasses of RenderTwoDimensionalViewport override the paint method, the [paintOffset] should be used to position the child in the viewport in order to account for a reversed [AxisDirection] in one or both dimensions.

### layoutOffset

```dart
Offset? layoutOffset
```

The offset at which to paint the child in the parent's coordinate system.

This [Offset] represents the top left corner of the child of the [TwoDimensionalViewport].

This value must be set by implementors during [RenderTwoDimensionalViewport.layoutChildSequence]. After the method is complete, the [RenderTwoDimensionalViewport] will compute the [paintOffset] based on this value to account for the [AxisDirection].

### vicinity

```dart
ChildVicinity vicinity
```

The logical positioning of children in two dimensions.

While children may not be strictly laid out in rows and columns, the relative positioning determines traversal of children in row or column major format.

This is set in the [RenderTwoDimensionalViewport.buildOrObtainChildFor].

### isVisible

```dart
bool get isVisible
```

Whether or not the child is actually visible within the viewport.

For example, if a child is contained within the [RenderTwoDimensionalViewport.cacheExtent] and out of view.

This is used during [RenderTwoDimensionalViewport.paint] in order to skip painting children that cannot be seen.

### paintOffset

```dart
Offset? paintOffset
```

The position of the child relative to the bounds and [AxisDirection] of the viewport.

This is the distance from the top left visible corner of the parent to the top left visible corner of the child. When the [AxisDirection]s are [AxisDirection.down] or [AxisDirection.right], this value is the same as the [layoutOffset]. This value deviates when scrolling in the reverse directions of [AxisDirection.up] and [AxisDirection.left] to reposition the children correctly.

This is set in [RenderTwoDimensionalViewport.updateChildPaintData], after [RenderTwoDimensionalViewport.layoutChildSequence].

If overriding [RenderTwoDimensionalViewport.paint], use this value to position the children instead of [layoutOffset].

### keptAlive

```dart
bool get keptAlive
```

### toString()

```dart
String toString()
```

# RenderTwoDimensionalViewport

```dart
abstract class RenderTwoDimensionalViewport extends RenderBox implements RenderAbstractViewport {}
```

A base class for viewing render objects that scroll in two dimensions.

The viewport listens to two [ViewportOffset]s, which determines the visible content.

Subclasses must implement [layoutChildSequence], calling on [buildOrObtainChildFor] to manage the children of the viewport.

Subclasses should not override [performLayout], as it handles housekeeping on either side of the call to [layoutChildSequence].

### RenderTwoDimensionalViewport()

```dart
RenderTwoDimensionalViewport({required ViewportOffset horizontalOffset, required AxisDirection horizontalAxisDirection, required ViewportOffset verticalOffset, required AxisDirection verticalAxisDirection, required TwoDimensionalChildDelegate delegate, required Axis mainAxis, required TwoDimensionalChildManager childManager, double? cacheExtent, CacheExtentStyle? cacheExtentStyle, ScrollCacheExtent? scrollCacheExtent, Clip clipBehavior = Clip.hardEdge})
```

Initializes fields for subclasses.

The [cacheExtent], if null, defaults to [RenderAbstractViewport.defaultCacheExtent].

### horizontalOffset

```dart
ViewportOffset get horizontalOffset
```

Which part of the content inside the viewport should be visible in the horizontal axis.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport horizontally, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### horizontalOffset

```dart
set horizontalOffset(ViewportOffset value)
```

### horizontalAxisDirection

```dart
AxisDirection get horizontalAxisDirection
```

The direction in which the [horizontalOffset] increases.

For example, if the axis direction is [AxisDirection.right], a scroll offset of zero is at the left of the viewport and increases towards the right of the viewport.

### horizontalAxisDirection

```dart
set horizontalAxisDirection(AxisDirection value)
```

### verticalOffset

```dart
ViewportOffset get verticalOffset
```

Which part of the content inside the viewport should be visible in the vertical axis.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport vertically, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### verticalOffset

```dart
set verticalOffset(ViewportOffset value)
```

### verticalAxisDirection

```dart
AxisDirection get verticalAxisDirection
```

The direction in which the [verticalOffset] increases.

For example, if the axis direction is [AxisDirection.down], a scroll offset of zero is at the top the viewport and increases towards the bottom of the viewport.

### verticalAxisDirection

```dart
set verticalAxisDirection(AxisDirection value)
```

### delegate

```dart
TwoDimensionalChildDelegate get delegate
```

Supplies children for layout in the viewport.

### delegate

```dart
set delegate(TwoDimensionalChildDelegate value)
```

### mainAxis

```dart
Axis get mainAxis
```

The major axis of the two dimensions.

This is can be used by subclasses to determine paint order, visitor patterns like row and column major ordering, or hit test precedence.

See also:

- [TwoDimensionalScrollView], which assigns the [PrimaryScrollController] to the [TwoDimensionalScrollView.mainAxis] and shares this value.

### mainAxis

```dart
set mainAxis(Axis value)
```

### cacheExtent

```dart
double get cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

### cacheExtent

```dart
set cacheExtent(double? value)
```

### cacheExtentStyle

```dart
CacheExtentStyle get cacheExtentStyle
```

{@macro flutter.rendering.RenderViewportBase.cacheExtentStyle}

### cacheExtentStyle

```dart
set cacheExtentStyle(CacheExtentStyle? value)
```

### scrollCacheExtent

```dart
ScrollCacheExtent get scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### scrollCacheExtent

```dart
set scrollCacheExtent(ScrollCacheExtent? value)
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### sizedByParent

```dart
bool get sizedByParent
```

### firstChild

```dart
RenderBox? get firstChild
```

The first child of the viewport according to the traversal order of the [mainAxis].

{@template flutter.rendering.twoDimensionalViewport.paintOrder} The [mainAxis] correlates with the [ChildVicinity] of each child to paint the children in a row or column major order.

By default, the [mainAxis] is [Axis.vertical], which would result in a row major paint order, visiting children in the horizontal indices before advancing to the next vertical index. {@endtemplate}

This value is null during [layoutChildSequence] as children are reified into the correct order after layout is completed. This can be used when overriding [paint] in order to paint the children in the correct order.

### lastChild

```dart
RenderBox? get lastChild
```

The last child in the viewport according to the traversal order of the [mainAxis].

{@macro flutter.rendering.twoDimensionalViewport.paintOrder}

This value is null during [layoutChildSequence] as children are reified into the correct order after layout is completed. This can be used when overriding [paint] in order to paint the children in the correct order.

### childBefore()

```dart
RenderBox? childBefore(RenderBox child)
```

The previous child before the given child in the child list according to the traversal order of the [mainAxis].

{@macro flutter.rendering.twoDimensionalViewport.paintOrder}

This method is useful when overriding [paint] in order to paint children in the correct order.

### childAfter()

```dart
RenderBox? childAfter(RenderBox child)
```

The next child after the given child in the child list according to the traversal order of the [mainAxis].

{@macro flutter.rendering.twoDimensionalViewport.paintOrder}

This method is useful when overriding [paint] in order to paint children in the correct order.

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### parentDataOf()

```dart
TwoDimensionalViewportParentData parentDataOf(RenderBox child)
```

Convenience method for retrieving and casting the [ParentData] of the viewport's children.

Children must have a [ParentData] of type [TwoDimensionalViewportParentData], or a subclass thereof.

### getChildFor()

```dart
RenderBox? getChildFor(ChildVicinity vicinity)
```

Returns the active child located at the provided [ChildVicinity], if there is one.

This can be used by subclasses to access currently active children to make use of their size or [TwoDimensionalViewportParentData], such as when overriding the [paint] method.

Returns null if there is no active child for the given [ChildVicinity].

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### viewportDimension

```dart
Size get viewportDimension
```

The dimensions of the viewport.

This [Size] represents the width and height of the visible area.

### performResize()

```dart
void performResize()
```

### getOffsetToReveal()

```dart
RevealedOffset getOffsetToReveal(RenderObject target, double alignment, {Rect? rect, Axis? axis})
```

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

### showInViewport()

```dart
Rect? showInViewport({RenderObject? descendant, Rect? rect, required RenderTwoDimensionalViewport viewport, Duration duration = Duration.zero, Curve curve = Curves.ease, AxisDirection? axisDirection})
```

Make (a portion of) the given `descendant` of the given `viewport` fully visible in one or both dimensions of the `viewport` by manipulating the [ViewportOffset]s.

The `axisDirection` determines from which axes the `descendant` will be revealed. When the `axisDirection` is null, both axes will be updated to reveal the descendant.

The optional `rect` parameter describes which area of the `descendant` should be shown in the viewport. If `rect` is null, the entire `descendant` will be revealed. The `rect` parameter is interpreted relative to the coordinate system of `descendant`.

The returned [Rect] describes the new location of `descendant` or `rect` in the viewport after it has been revealed. See [RevealedOffset.rect] for a full definition of this [Rect].

The parameter `viewport` is required and cannot be null. If `descendant` is null, this is a no-op and `rect` is returned.

If both `descendant` and `rect` are null, null is returned because there is nothing to be shown in the viewport.

The `duration` parameter can be set to a non-zero value to animate the target object into the viewport with an animation defined by `curve`.

See also:

- [RenderObject.showOnScreen], overridden by [RenderTwoDimensionalViewport] to delegate to this method.

### didResize

```dart
bool get didResize
```

Should be used by subclasses to invalidate any cached metrics for the viewport.

This is set to true when the viewport has been resized, indicating that any cached dimensions are invalid.

After performLayout, the value is set to false until the viewport dimensions are changed again in [performResize].

Subclasses are not required to use this value, but it can be used to safely cache layout information in between layout calls.

### needsDelegateRebuild

```dart
bool get needsDelegateRebuild
```

Should be used by subclasses to invalidate any cached data from the [delegate].

This value is set to false after [layoutChildSequence]. If [markNeedsLayout] is called `withDelegateRebuild` set to true, then this value will be updated to true, signifying any cached delegate information needs to be updated in the next call to [layoutChildSequence].

Subclasses are not required to use this value, but it can be used to safely cache layout information in between layout calls.

### markNeedsLayout()

```dart
void markNeedsLayout({bool withDelegateRebuild = false})
```

### layoutChildSequence()

```dart
void layoutChildSequence()
```

Primary work horse of [performLayout].

Subclasses must implement this method to layout the children of the viewport. The [TwoDimensionalViewportParentData.layoutOffset] must be set during this method in order for the children to be positioned during paint. Further, children of the viewport must be laid out with the expectation that the parent (this viewport) will use their size.

```dart
child.layout(constraints, parentUsesSize: true);
```

The primary methods used for creating and obtaining children is [buildOrObtainChildFor], which takes a [ChildVicinity] that is used by the [TwoDimensionalChildDelegate]. If a child is not provided by the delegate for the provided vicinity, the method will return null, otherwise, it will return the [RenderBox] of the child.

After [layoutChildSequence] is completed, any remaining children that were not obtained will be disposed.

### performLayout()

```dart
void performLayout()
```

### buildOrObtainChildFor()

```dart
RenderBox? buildOrObtainChildFor(ChildVicinity vicinity)
```

Returns the child for a given [ChildVicinity], should be called during [layoutChildSequence] in order to instantiate or retrieve children.

This method will build the child if it has not been already, or will reuse it if it already exists, whether it was part of the previous frame or kept alive.

Children for the given [ChildVicinity] will be inserted into the active children list, and so should be visible, or contained within the [cacheExtent].

### updateChildPaintData()

```dart
void updateChildPaintData(RenderBox child)
```

Called after [layoutChildSequence] to compute the [TwoDimensionalViewportParentData.paintOffset] and [TwoDimensionalViewportParentData._paintExtent] of the child.

### computeChildPaintExtent()

```dart
Size computeChildPaintExtent(Offset layoutOffset, Size childSize)
```

Computes the portion of the child that is visible, assuming that only the region from the [ViewportOffset.pixels] of both dimensions to the [cacheExtent] is visible, and that the relationship between scroll offsets and paint offsets is linear.

For example, if the [ViewportOffset]s each have a scroll offset of 100 and the arguments to this method describe a child with [layoutOffset] of `Offset(50.0, 50.0)`, with a size of `Size(200.0, 200.0)`, then the returned value would be `Size(150.0, 150.0)`, representing the visible extent of the child.

### computeAbsolutePaintOffsetFor()

```dart
Offset computeAbsolutePaintOffsetFor(RenderBox child, {required Offset layoutOffset})
```

The offset at which the given `child` should be painted.

The returned offset is from the top left corner of the inside of the viewport to the top left corner of the paint coordinate system of the `child`.

This is useful when the one or both of the axes of the viewport are reversed. The normalized layout offset of the child is used to compute the paint offset in relation to the [verticalAxisDirection] and [horizontalAxisDirection].

### paint()

```dart
void paint(PaintingContext context, Offset offset)
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

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### dispose()

```dart
void dispose()
```

# TwoDimensionalChildManager

```dart
abstract class TwoDimensionalChildManager {}
```

A delegate used by [RenderTwoDimensionalViewport] to manage its children.

[RenderTwoDimensionalViewport] objects reify their children lazily to avoid spending resources on children that are not visible in the viewport. This delegate lets these objects create, reuse and remove children.

# ChildVicinity

```dart
class ChildVicinity implements Comparable<ChildVicinity> {}
```

The relative position of a child in a [TwoDimensionalViewport] in relation to other children of the viewport.

While children can be plotted arbitrarily in two dimensional space, the [ChildVicinity] is used to disambiguate their positions, determining how to traverse the children of the space.

Combined with the [RenderTwoDimensionalViewport.mainAxis], each child's vicinity determines its paint order among all of the children.

### ChildVicinity()

```dart
ChildVicinity({required int xIndex, required int yIndex})
```

Creates a reference to a child in a two dimensional plane, with the [xIndex] and [yIndex] being relative to other children in the viewport.

### invalid

```dart
ChildVicinity invalid
```

Represents an unassigned child position. The given child may be in the process of moving from one position to another.

### xIndex

```dart
int xIndex
```

The index of the child in the horizontal axis, relative to neighboring children.

While children's offset and positioning may not be strictly defined in terms of rows and columns, like a table, [ChildVicinity.xIndex] and [ChildVicinity.yIndex] represents order of traversal in row or column major format.

### yIndex

```dart
int yIndex
```

The index of the child in the vertical axis, relative to neighboring children.

While children's offset and positioning may not be strictly defined in terms of rows and columns, like a table, [ChildVicinity.xIndex] and [ChildVicinity.yIndex] represents order of traversal in row or column major format.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### compareTo()

```dart
int compareTo(ChildVicinity other)
```

### toString()

```dart
String toString()
```
