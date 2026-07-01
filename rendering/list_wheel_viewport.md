@docImport 'package:flutter/widgets.dart';

# ListWheelChildManager

```dart
abstract class ListWheelChildManager {}
```

A delegate used by [RenderListWheelViewport] to manage its children.

[RenderListWheelViewport] during layout will ask the delegate to create children that are visible in the viewport and remove those that are not.

### childCount

```dart
int? get childCount
```

The maximum number of children that can be provided to [RenderListWheelViewport].

If non-null, the children will have index in the range `[0, childCount - 1]`.

If null, then there's no explicit limits to the range of the children except that it has to be contiguous. If [childExistsAt] for a certain index returns false, that index is already past the limit.

### childExistsAt()

```dart
bool childExistsAt(int index)
```

Checks whether the delegate is able to provide a child widget at the given index.

This function is not about whether the child at the given index is attached to the [RenderListWheelViewport] or not.

### createChild()

```dart
void createChild(int index, {required RenderBox? after})
```

Creates a new child at the given index and updates it to the child list of [RenderListWheelViewport]. If no child corresponds to `index`, then do nothing.

It is possible to create children with negative indices.

### removeChild()

```dart
void removeChild(RenderBox child)
```

Removes the child element corresponding with the given RenderBox.

# ListWheelParentData

```dart
class ListWheelParentData extends ContainerBoxParentData<RenderBox> {}
```

[ParentData] for use with [RenderListWheelViewport].

### index

```dart
int? index
```

Index of this child in its parent's child list.

This must be maintained by the [ListWheelChildManager].

### transform

```dart
Matrix4? transform
```

Transform applied to this child during painting.

Can be used to find the local bounds of this child in the viewport, and then use it, for example, in hit testing.

May be null if child was laid out, but not painted by the parent, but normally this shouldn't happen, because [RenderListWheelViewport] paints all of the children it has laid out.

# RenderListWheelViewport

```dart
class RenderListWheelViewport extends RenderBox with ContainerRenderObjectMixin<RenderBox, ListWheelParentData> implements RenderAbstractViewport {}
```

Render, onto a wheel, a bigger sequential set of objects inside this viewport.

Takes a scrollable set of fixed sized [RenderBox]es and renders them sequentially from top down on a vertical scrolling axis.

It starts with the first scrollable item in the center of the main axis and ends with the last scrollable item in the center of the main axis. This is in contrast to typical lists that start with the first scrollable item at the start of the main axis and ends with the last scrollable item at the end of the main axis.

Instead of rendering its children on a flat plane, it renders them as if each child is broken into its own plane and that plane is perpendicularly fixed onto a cylinder which rotates along the scrolling axis.

This class works in 3 coordinate systems:

1.  The **scrollable layout coordinates**. This coordinate system is used to communicate with [ViewportOffset] and describes its children's abstract offset from the beginning of the scrollable list at (0.0, 0.0).

The list is scrollable from the start of the first child item to the start of the last child item.

Children's layout coordinates don't change as the viewport scrolls.

2.  The **untransformed plane's viewport painting coordinates**. Children are not painted in this coordinate system. It's an abstract intermediary used before transforming into the next cylindrical coordinate system.

This system is the **scrollable layout coordinates** translated by the scroll offset such that (0.0, 0.0) is the top left corner of the viewport.

Because the viewport is centered at the scrollable list's scroll offset instead of starting at the scroll offset, there are paintable children ~1/2 viewport length before and after the scroll offset instead of ~1 viewport length after the scroll offset.

Children's visibility inclusion in the viewport is determined in this system regardless of the cylinder's properties such as [diameterRatio] or [perspective]. In other words, a 100px long viewport will always paint 10-11 visible 10px children if there are enough children in the viewport.

3.  The **transformed cylindrical space viewport painting coordinates**. Children from system 2 get their positions transformed into a cylindrical projection matrix instead of its Cartesian offset with respect to the scroll offset.

Children in this coordinate system are painted.

The wheel's size and the maximum and minimum visible angles are both controlled by [diameterRatio]. Children visible in the **untransformed plane's viewport painting coordinates**'s viewport will be radially evenly laid out between the maximum and minimum angles determined by intersecting the viewport's main axis length with a cylinder whose diameter is [diameterRatio] times longer, as long as those angles are between -pi/2 and pi/2.

For example, if [diameterRatio] is 2.0 and this [RenderListWheelViewport] is 100.0px in the main axis, then the diameter is 200.0. And children will be evenly laid out between that cylinder's -arcsin(1/2) and arcsin(1/2) angles.

The cylinder's 0 degree side is always centered in the [RenderListWheelViewport]. The transformation from **untransformed plane's viewport painting coordinates** is also done such that the child in the center of that plane will be mostly untransformed with children above and below it being transformed more as the angle increases.

### RenderListWheelViewport()

```dart
RenderListWheelViewport({required ListWheelChildManager childManager, required ViewportOffset offset, double diameterRatio = defaultDiameterRatio, double perspective = defaultPerspective, double offAxisFraction = 0, bool useMagnifier = false, double magnification = 1, double overAndUnderCenterOpacity = 1, required double itemExtent, double squeeze = 1, bool renderChildrenOutsideViewport = false, Clip clipBehavior = Clip.none, List<RenderBox>? children})
```

Creates a [RenderListWheelViewport] which renders children on a wheel.

Optional arguments have reasonable defaults.

### defaultDiameterRatio

```dart
double defaultDiameterRatio
```

An arbitrary but aesthetically reasonable default value for [diameterRatio].

### defaultPerspective

```dart
double defaultPerspective
```

An arbitrary but aesthetically reasonable default value for [perspective].

### diameterRatioZeroMessage

```dart
String diameterRatioZeroMessage
```

An error message to show when the provided [diameterRatio] is zero.

### perspectiveTooHighMessage

```dart
String perspectiveTooHighMessage
```

An error message to show when the [perspective] value is too high.

### clipBehaviorAndRenderChildrenOutsideViewportConflict

```dart
String clipBehaviorAndRenderChildrenOutsideViewportConflict
```

An error message to show when [clipBehavior] and [renderChildrenOutsideViewport] are set to conflicting values.

### childManager

```dart
ListWheelChildManager childManager
```

The delegate that manages the children of this object.

This delegate must maintain the [ListWheelParentData.index] value.

### offset

```dart
ViewportOffset get offset
```

The associated ViewportOffset object for the viewport describing the part of the content inside that's visible.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport, this value changes, which changes the content that is displayed.

### offset

```dart
set offset(ViewportOffset value)
```

### diameterRatio

```dart
double get diameterRatio
```

{@template flutter.rendering.RenderListWheelViewport.diameterRatio} A ratio between the diameter of the cylinder and the viewport's size in the main axis.

A value of 1 means the cylinder has the same diameter as the viewport's size.

A value smaller than 1 means items at the edges of the cylinder are entirely contained inside the viewport.

A value larger than 1 means angles less than ±[math.pi] / 2 from the center of the cylinder are visible.

The same number of children will be visible in the viewport regardless of the [diameterRatio]. The number of children visible is based on the viewport's length along the main axis divided by the children's [itemExtent]. Then the children are evenly distributed along the visible angles up to ±[math.pi] / 2.

Just as it's impossible to stretch a paper to cover the an entire half of a cylinder's surface where the cylinder has the same diameter as the paper's length, choosing a [diameterRatio] smaller than [math.pi] will leave same gaps between the children.

Defaults to an arbitrary but aesthetically reasonable number of 2.0.

Must be a positive number. {@endtemplate}

### diameterRatio

```dart
set diameterRatio(double value)
```

### perspective

```dart
double get perspective
```

{@template flutter.rendering.RenderListWheelViewport.perspective} Perspective of the cylindrical projection.

A number between 0 and 0.01 where 0 means looking at the cylinder from infinitely far with an infinitely small field of view and 1 means looking at the cylinder from infinitely close with an infinitely large field of view (which cannot be rendered).

Defaults to an arbitrary but aesthetically reasonable number of 0.003. A larger number brings the vanishing point closer and a smaller number pushes the vanishing point further.

Must be a positive number. {@endtemplate}

### perspective

```dart
set perspective(double value)
```

### offAxisFraction

```dart
double get offAxisFraction
```

{@template flutter.rendering.RenderListWheelViewport.offAxisFraction} How much the wheel is horizontally off-center, as a fraction of its width.

This property creates the visual effect of looking at a vertical wheel from its side where its vanishing points at the edge curves to one side instead of looking at the wheel head-on.

The value is horizontal distance between the wheel's center and the vertical vanishing line at the edges of the wheel, represented as a fraction of the wheel's width.

The value `0.0` means the wheel is looked at head-on and its vanishing line runs through the center of the wheel. Negative values means moving the wheel to the left of the observer, thus the edges curve to the right. Positive values means moving the wheel to the right of the observer, thus the edges curve to the left.

The visual effect causes the wheel's edges to curve rather than moving the center. So a value of `0.5` means the edges' vanishing line will touch the wheel's size's left edge.

Defaults to `0.0`, which means looking at the wheel head-on. The visual effect can be unaesthetic if this value is too far from the range `[-0.5, 0.5]`. {@endtemplate}

### offAxisFraction

```dart
set offAxisFraction(double value)
```

### useMagnifier

```dart
bool get useMagnifier
```

{@template flutter.rendering.RenderListWheelViewport.useMagnifier} Whether to use the magnifier for the center item of the wheel. {@endtemplate}

### useMagnifier

```dart
set useMagnifier(bool value)
```

### magnification

```dart
double get magnification
```

{@template flutter.rendering.RenderListWheelViewport.magnification} The zoomed-in rate of the magnifier, if it is used.

The default value is 1.0, which will not change anything. If the value is > 1.0, the center item will be zoomed in by that rate, and it will also be rendered as flat, not cylindrical like the rest of the list. The item will be zoomed out if magnification < 1.0.

Must be positive. {@endtemplate}

### magnification

```dart
set magnification(double value)
```

### overAndUnderCenterOpacity

```dart
double get overAndUnderCenterOpacity
```

{@template flutter.rendering.RenderListWheelViewport.overAndUnderCenterOpacity} The opacity value that will be applied to the wheel that appears below and above the magnifier.

The default value is 1.0, which will not change anything.

Must be greater than or equal to 0, and less than or equal to 1. {@endtemplate}

### overAndUnderCenterOpacity

```dart
set overAndUnderCenterOpacity(double value)
```

### itemExtent

```dart
double get itemExtent
```

{@template flutter.rendering.RenderListWheelViewport.itemExtent} The size of the children along the main axis. Children [RenderBox]es will be given the [BoxConstraints] of this exact size.

Must be a positive number. {@endtemplate}

### itemExtent

```dart
set itemExtent(double value)
```

### squeeze

```dart
double get squeeze
```

{@template flutter.rendering.RenderListWheelViewport.squeeze} The angular compactness of the children on the wheel.

This denotes a ratio of the number of children on the wheel vs the number of children that would fit on a flat list of equivalent size, assuming [diameterRatio] of 1.

For instance, if this RenderListWheelViewport has a height of 100px and [itemExtent] is 20px, 5 items would fit on an equivalent flat list. With a [squeeze] of 1, 5 items would also be shown in the RenderListWheelViewport. With a [squeeze] of 2, 10 items would be shown in the RenderListWheelViewport.

Changing this value will change the number of children built and shown inside the wheel.

Must be a positive number. {@endtemplate}

Defaults to 1.

### squeeze

```dart
set squeeze(double value)
```

### renderChildrenOutsideViewport

```dart
bool get renderChildrenOutsideViewport
```

{@template flutter.rendering.RenderListWheelViewport.renderChildrenOutsideViewport} Whether to paint children inside the viewport only.

If false, every child will be painted. However the [Scrollable] is still the size of the viewport and detects gestures inside only.

Defaults to false. Cannot be true if [clipBehavior] is not [Clip.none] since children outside the viewport will be clipped, and therefore cannot render children outside the viewport. {@endtemplate}

### renderChildrenOutsideViewport

```dart
set renderChildrenOutsideViewport(bool value)
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

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

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

### sizedByParent

```dart
bool get sizedByParent
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### indexOf()

```dart
int indexOf(RenderBox child)
```

Gets the index of a child by looking at its [parentData].

This relies on the [childManager] maintaining [ListWheelParentData.index].

### scrollOffsetToIndex()

```dart
int scrollOffsetToIndex(double scrollOffset)
```

Returns the index of the child at the given offset.

### indexToScrollOffset()

```dart
double indexToScrollOffset(int index)
```

Returns the scroll offset of the child with the given index.

### performLayout()

```dart
void performLayout()
```

Performs layout based on how [childManager] provides children.

From the current scroll offset, the minimum index and maximum index that is visible in the viewport can be calculated. The index range of the currently active children can also be acquired by looking directly at the current child list. This function has to modify the current index range to match the target index range by removing children that are no longer visible and creating those that are visible but not yet provided by [childManager].

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### describeApproximatePaintClip()

```dart
Rect? describeApproximatePaintClip(RenderObject child)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### getOffsetToReveal()

```dart
RevealedOffset getOffsetToReveal(RenderObject target, double alignment, {Rect? rect, Axis? axis})
```

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```
