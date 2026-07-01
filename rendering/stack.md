@docImport 'package:flutter/widgets.dart';

@docImport 'flow.dart'; @docImport 'proxy_box.dart';

# RelativeRect

```dart
class RelativeRect {}
```

An immutable 2D, axis-aligned, floating-point rectangle whose coordinates are given relative to another rectangle's edges, known as the container. Since the dimensions of the rectangle are relative to those of the container, this class has no width and height members. To determine the width or height of the rectangle, convert it to a [Rect] using [toRect()] (passing the container's own Rect), and then examine that object.

### RelativeRect.fromLTRB()

```dart
RelativeRect.fromLTRB(double left, double top, double right, double bottom)
```

Creates a RelativeRect with the given values.

### RelativeRect.fromSize()

```dart
RelativeRect.fromSize(Rect rect, Size container)
```

Creates a RelativeRect from a Rect and a Size. The Rect (first argument) and the RelativeRect (the output) are in the coordinate space of the rectangle described by the Size, with 0,0 being at the top left.

### RelativeRect.fromRect()

```dart
RelativeRect.fromRect(Rect rect, Rect container)
```

Creates a RelativeRect from two Rects. The second Rect provides the container, the first provides the rectangle, in the same coordinate space, that is to be converted to a RelativeRect. The output will be in the container's coordinate space.

For example, if the top left of the rect is at 0,0, and the top left of the container is at 100,100, then the top left of the output will be at -100,-100.

If the first rect is actually in the container's coordinate space, then use [RelativeRect.fromSize] and pass the container's size as the second argument instead.

### RelativeRect.fromDirectional()

```dart
RelativeRect.fromDirectional({required TextDirection textDirection, required double start, required double top, required double end, required double bottom})
```

Creates a RelativeRect from horizontal position using `start` and `end` rather than `left` and `right`.

If `textDirection` is [TextDirection.rtl], then the `start` argument is used for the [right] property and the `end` argument is used for the [left] property. Otherwise, if `textDirection` is [TextDirection.ltr], then the `start` argument is used for the [left] property and the `end` argument is used for the [right] property.

### fill

```dart
RelativeRect fill
```

A rect that covers the entire container.

### left

```dart
double left
```

Distance from the left side of the container to the left side of this rectangle.

May be negative if the left side of the rectangle is outside of the container.

### top

```dart
double top
```

Distance from the top side of the container to the top side of this rectangle.

May be negative if the top side of the rectangle is outside of the container.

### right

```dart
double right
```

Distance from the right side of the container to the right side of this rectangle.

May be positive if the right side of the rectangle is outside of the container.

### bottom

```dart
double bottom
```

Distance from the bottom side of the container to the bottom side of this rectangle.

May be positive if the bottom side of the rectangle is outside of the container.

### hasInsets

```dart
bool get hasInsets
```

Returns whether any of the values are greater than zero.

This corresponds to one of the sides ([left], [top], [right], or [bottom]) having some positive inset towards the center.

### shift()

```dart
RelativeRect shift(Offset offset)
```

Returns a new rectangle object translated by the given offset.

### inflate()

```dart
RelativeRect inflate(double delta)
```

Returns a new rectangle with edges moved outwards by the given delta.

### deflate()

```dart
RelativeRect deflate(double delta)
```

Returns a new rectangle with edges moved inwards by the given delta.

### intersect()

```dart
RelativeRect intersect(RelativeRect other)
```

Returns a new rectangle that is the intersection of the given rectangle and this rectangle.

### toRect()

```dart
Rect toRect(Rect container)
```

Convert this [RelativeRect] to a [Rect], in the coordinate space of the container.

See also:

- [toSize], which returns the size part of the rect, based on the size of the container.

### toSize()

```dart
Size toSize(Size container)
```

Convert this [RelativeRect] to a [Size], assuming a container with the given size.

See also:

- [toRect], which also computes the position relative to the container.

### lerp()

```dart
RelativeRect? lerp(RelativeRect? a, RelativeRect? b, double t)
```

Linearly interpolate between two RelativeRects.

If either rect is null, this function interpolates from [RelativeRect.fill].

{@macro dart.ui.shadow.lerp}

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

# StackParentData

```dart
class StackParentData extends ContainerBoxParentData<RenderBox> {}
```

Parent data for use with [RenderStack].

### top

```dart
double? top
```

The distance by which the child's top edge is inset from the top of the stack.

### right

```dart
double? right
```

The distance by which the child's right edge is inset from the right of the stack.

### bottom

```dart
double? bottom
```

The distance by which the child's bottom edge is inset from the bottom of the stack.

### left

```dart
double? left
```

The distance by which the child's left edge is inset from the left of the stack.

### width

```dart
double? width
```

The child's width.

Ignored if both left and right are non-null.

### height

```dart
double? height
```

The child's height.

Ignored if both top and bottom are non-null.

### rect

```dart
RelativeRect get rect
```

Get or set the current values in terms of a RelativeRect object.

### rect

```dart
set rect(RelativeRect value)
```

### isPositioned

```dart
bool get isPositioned
```

Whether this child is considered positioned.

A child is positioned if any of the top, right, bottom, or left properties are non-null. Positioned children do not factor into determining the size of the stack but are instead placed relative to the non-positioned children in the stack.

### positionedChildConstraints()

```dart
BoxConstraints positionedChildConstraints(Size stackSize)
```

Computes the [BoxConstraints] the stack layout algorithm would give to this child, given the [Size] of the stack.

This method should only be called when [isPositioned] is true for the child.

### toString()

```dart
String toString()
```

# StackFit

```dart
enum StackFit {}
```

How to size the non-positioned children of a [Stack].

This enum is used with [Stack.fit] and [RenderStack.fit] to control how the [BoxConstraints] passed from the stack's parent to the stack's child are adjusted.

See also:

- [Stack], the widget that uses this.
- [RenderStack], the render object that implements the stack algorithm.

The constraints passed to the stack from its parent are loosened.

For example, if the stack has constraints that force it to 350x600, then this would allow the non-positioned children of the stack to have any width from zero to 350 and any height from zero to 600.

See also:

- [Center], which loosens the constraints passed to its child and then centers the child in itself.
- [BoxConstraints.loosen], which implements the loosening of box constraints.

The constraints passed to the stack from its parent are tightened to the biggest size allowed.

For example, if the stack has loose constraints with a width in the range 10 to 100 and a height in the range 0 to 600, then the non-positioned children of the stack would all be sized as 100 pixels wide and 600 high.

The constraints passed to the stack from its parent are passed unmodified to the non-positioned children.

For example, if a [Stack] is an [Expanded] child of a [Row], the horizontal constraints will be tight and the vertical constraints will be loose.

# RenderStack

```dart
class RenderStack extends RenderBox with ContainerRenderObjectMixin<RenderBox, StackParentData>, RenderBoxContainerDefaultsMixin<RenderBox, StackParentData> {}
```

Implements the stack layout algorithm.

In a stack layout, the children are positioned on top of each other in the order in which they appear in the child list. First, the non-positioned children (those with null values for top, right, bottom, and left) are laid out and initially placed in the upper-left corner of the stack. The stack is then sized to enclose all of the non-positioned children. If there are no non-positioned children, the stack becomes as large as possible.

The final location of non-positioned children is determined by the alignment parameter. The left of each non-positioned child becomes the difference between the stack's width and the child's width multiplied by (alignment.x + 1.0) / 2.0. The top of each non-positioned child is computed similarly from the stack's height, the child's height, and `alignment.y`.

So if the alignment x and y properties are -1.0, then the non-positioned children remain in the upper-left corner (the top-start). If the alignment x and y properties are 0.0, then the non-positioned children are centered within the stack.

Next, the positioned children are laid out. If a child has top and bottom values that are both non-null, the child is given a fixed height determined by subtracting the sum of the top and bottom values from the height of the stack. Similarly, if the child has right and left values that are both non-null, the child is given a fixed width derived from the stack's width. Otherwise, the child is given unbounded constraints in the non-fixed dimensions.

Once the child is laid out, the stack positions the child according to the top, right, bottom, and left properties of their [StackParentData]. For example, if the bottom value is 10.0, the bottom edge of the child will be inset 10.0 pixels from the bottom edge of the stack. If the child extends beyond the bounds of the stack, the stack will clip the child's painting to the bounds of the stack.

See also:

- [RenderFlow]

### RenderStack()

```dart
RenderStack({List<RenderBox>? children, AlignmentGeometry alignment = AlignmentDirectional.topStart, TextDirection? textDirection, StackFit fit = StackFit.loose, Clip clipBehavior = Clip.hardEdge})
```

Creates a stack render object.

By default, the non-positioned children of the stack are aligned by their top left corners.

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### alignment

```dart
AlignmentGeometry get alignment
```

How to align the non-positioned or partially-positioned children in the stack.

The non-positioned children are placed relative to each other such that the points determined by [alignment] are co-located. For example, if the [alignment] is [Alignment.topLeft], then the top left corner of each non-positioned child will be located at the same global coordinate.

Partially-positioned children, those that do not specify an alignment in a particular axis (e.g. that have neither `top` nor `bottom` set), use the alignment to determine how they should be positioned in that under-specified axis.

If this is set to an [AlignmentDirectional] object, then [textDirection] must not be null.

### alignment

```dart
set alignment(AlignmentGeometry value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [alignment].

This may be changed to null, but only after the [alignment] has been changed to a value that does not depend on the direction.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### fit

```dart
StackFit get fit
```

How to size the non-positioned children in the stack.

The constraints passed into the [RenderStack] from its parent are either loosened ([StackFit.loose]) or tightened to their biggest size ([StackFit.expand]).

### fit

```dart
set fit(StackFit value)
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Stacks only clip children whose geometry overflow the stack. A child that paints outside its bounds (e.g. a box with a shadow) will not be clipped, regardless of the value of this property. Similarly, a child that itself has a descendant that overflows the stack will not be clipped, as only the geometry of the stack's direct children are considered.

To clip children whose geometry does not overflow the stack, consider using a [RenderClipRect] render object.

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### getIntrinsicDimension()

```dart
double getIntrinsicDimension(RenderBox? firstChild, double Function(RenderBox child) mainChildSizeGetter)
```

Helper function for calculating the intrinsics metrics of a Stack.

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

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

### layoutPositionedChild()

```dart
bool layoutPositionedChild(RenderBox child, StackParentData childParentData, Size size, Alignment alignment)
```

Lays out the positioned `child` according to `alignment` within a Stack of `size`.

Returns true when the child has visual overflow.

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paintStack()

```dart
void paintStack(PaintingContext context, Offset offset)
```

Override in subclasses to customize how the stack paints.

By default, the stack uses [defaultPaint]. This function is called by [paint] after potentially applying a clip to contain visual overflow.

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### describeApproximatePaintClip()

```dart
Rect? describeApproximatePaintClip(RenderObject child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderIndexedStack

```dart
class RenderIndexedStack extends RenderStack {}
```

Implements the same layout algorithm as RenderStack but only paints the child specified by index.

Although only one child is displayed, the cost of the layout algorithm is still O(N), like an ordinary stack.

### RenderIndexedStack()

```dart
RenderIndexedStack({List<RenderBox>? children, dynamic alignment, dynamic textDirection, StackFit fit, dynamic clipBehavior, int? index = 0})
```

Creates a stack render object that paints a single child.

If the [index] parameter is null, nothing is displayed.

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### index

```dart
int? get index
```

The index of the child to show, null if nothing is to be displayed.

### index

```dart
set index(int? value)
```

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paintStack()

```dart
void paintStack(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```
