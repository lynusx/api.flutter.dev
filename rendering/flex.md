@docImport 'package:flutter/widgets.dart';

# FlexFit

```dart
enum FlexFit {}
```

How the child is inscribed into the available space.

See also:

- [RenderFlex], the flex render object.
- [Column], [Row], and [Flex], the flex widgets.
- [Expanded], the widget equivalent of [tight].
- [Flexible], the widget equivalent of [loose].

The child is forced to fill the available space.

The [Expanded] widget assigns this kind of [FlexFit] to its child.

The child can be at most as large as the available space (but is allowed to be smaller).

The [Flexible] widget assigns this kind of [FlexFit] to its child.

# FlexParentData

```dart
class FlexParentData extends ContainerBoxParentData<RenderBox> {}
```

Parent data for use with [RenderFlex].

### flex

```dart
int? flex
```

The flex factor to use for this child.

If null or zero, the child is inflexible and determines its own size. If non-zero, the amount of space the child's can occupy in the main axis is determined by dividing the free space (after placing the inflexible children) according to the flex factors of the flexible children.

### fit

```dart
FlexFit? fit
```

How a flexible child is inscribed into the available space.

If [flex] is non-zero, the [fit] determines whether the child fills the space the parent makes available during layout. If the fit is [FlexFit.tight], the child is required to fill the available space. If the fit is [FlexFit.loose], the child can be at most as large as the available space (but is allowed to be smaller).

### toString()

```dart
String toString()
```

# MainAxisSize

```dart
enum MainAxisSize {}
```

How much space should be occupied in the main axis.

During a flex layout, available space along the main axis is allocated to children. After allocating space, there might be some remaining free space. This value controls whether to maximize or minimize the amount of free space, subject to the incoming layout constraints.

See also:

- [Column], [Row], and [Flex], the flex widgets.
- [Expanded] and [Flexible], the widgets that controls a flex widgets' children's flex.
- [RenderFlex], the flex render object.
- [MainAxisAlignment], which controls how the free space is distributed.

Minimize the amount of free space along the main axis, subject to the incoming layout constraints.

If the incoming layout constraints have a large enough [BoxConstraints.minWidth] or [BoxConstraints.minHeight], there might still be a non-zero amount of free space.

If the incoming layout constraints are unbounded, and any children have a non-zero [FlexParentData.flex] and a [FlexFit.tight] fit (as applied by [Expanded]), the [RenderFlex] will assert, because there would be infinite remaining free space and boxes cannot be given infinite size.

Maximize the amount of free space along the main axis, subject to the incoming layout constraints.

If the incoming layout constraints have a small enough [BoxConstraints.maxWidth] or [BoxConstraints.maxHeight], there might still be no free space.

If the incoming layout constraints are unbounded, the [RenderFlex] will assert, because there would be infinite remaining free space and boxes cannot be given infinite size.

# MainAxisAlignment

```dart
enum MainAxisAlignment {}
```

How the children should be placed along the main axis in a flex layout.

See also:

- [Column], [Row], and [Flex], the flex widgets.
- [RenderFlex], the flex render object.

Place the children as close to the start of the main axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the start is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the start is the top or the bottom.

Place the children as close to the end of the main axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the end is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the end is the top or the bottom.

Place the children as close to the middle of the main axis as possible.

Place the free space evenly between the children.

Place the free space evenly between the children as well as half of that space before and after the first and last child.

Place the free space evenly between the children as well as before and after the first and last child.

# CrossAxisAlignment

```dart
enum CrossAxisAlignment {}
```

How the children should be placed along the cross axis in a flex layout.

See also:

- [Column], [Row], and [Flex], the flex widgets.
- [Flex.crossAxisAlignment], the property on flex widgets that has this type.
- [RenderFlex], the flex render object.

Place the children with their start edge aligned with the start side of the cross axis.

For example, in a column (a flex with a vertical axis) whose [TextDirection] is [TextDirection.ltr], this aligns the left edge of the children along the left edge of the column.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the start is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the start is the top or the bottom.

Place the children as close to the end of the cross axis as possible.

For example, in a column (a flex with a vertical axis) whose [TextDirection] is [TextDirection.ltr], this aligns the right edge of the children along the right edge of the column.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the end is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the end is the top or the bottom.

Place the children so that their centers align with the middle of the cross axis.

This is the default cross-axis alignment.

Require the children to fill the cross axis.

This causes the constraints passed to the children to be tight in the cross axis.

Place the children along the cross axis such that their baselines match.

Consider using this value for any horizontal main axis (as with [Row]) where the children primarily contain text. If the different children have text with different font metrics (for example because they differ in [TextStyle.fontSize] or other [TextStyle] properties, or because they use different fonts due to being written in different scripts), then this typically produces better visual alignment than the other [CrossAxisAlignment] values, which use no information about where the text sits vertically within its bounding box.

The baseline of a widget is typically the typographic baseline of the first text in the first [Text] or [RichText] widget it encloses, if any. The typographic baseline is a horizontal line used for aligning text, which is specified by each font; for alphabetic scripts, it ordinarily runs along the bottom of letters excluding any descenders.

Because baselines are always horizontal, this alignment is intended for horizontal main axes (as with [Row]). If the main axis is vertical (as with [Column]), then this value is treated like [start].

For horizontal main axes, if the minimum height constraint passed to the flex layout exceeds the intrinsic height of the cross axis, children will be aligned as close to the top as they can be while honoring the baseline alignment. In other words, the extra space will be below all the children.

Children who report no baseline will be top-aligned.

See also:

- [RenderBox.getDistanceToBaseline], which defines the baseline of a box.
- [IgnoreBaseline], which can be used to ignore a child for the purpose of baseline alignment.

# RenderFlex

```dart
class RenderFlex extends RenderBox with ContainerRenderObjectMixin<RenderBox, FlexParentData>, RenderBoxContainerDefaultsMixin<RenderBox, FlexParentData>, DebugOverflowIndicatorMixin {}
```

Displays its children in a one-dimensional array.

## Layout algorithm

_This section describes how the framework causes [RenderFlex] to position its children._ _See [BoxConstraints] for an introduction to box layout models._

Layout for a [RenderFlex] proceeds in six steps:

1.  Layout each child with a null or zero flex factor with unbounded main axis constraints and the incoming cross axis constraints. If the [crossAxisAlignment] is [CrossAxisAlignment.stretch], instead use tight cross axis constraints that match the incoming max extent in the cross axis.
2.  Divide the remaining main axis space among the children with non-zero flex factors according to their flex factor. For example, a child with a flex factor of 2.0 will receive twice the amount of main axis space as a child with a flex factor of 1.0.
3.  Layout each of the remaining children with the same cross axis constraints as in step 1, but instead of using unbounded main axis constraints, use max axis constraints based on the amount of space allocated in step 2. Children with [Flexible.fit] properties that are [FlexFit.tight] are given tight constraints (i.e., forced to fill the allocated space), and children with [Flexible.fit] properties that are [FlexFit.loose] are given loose constraints (i.e., not forced to fill the allocated space).
4.  The cross axis extent of the [RenderFlex] is the maximum cross axis extent of the children (which will always satisfy the incoming constraints).
5.  The main axis extent of the [RenderFlex] is determined by the [mainAxisSize] property. If the [mainAxisSize] property is [MainAxisSize.max], then the main axis extent of the [RenderFlex] is the max extent of the incoming main axis constraints. If the [mainAxisSize] property is [MainAxisSize.min], then the main axis extent of the [Flex] is the sum of the main axis extents of the children (subject to the incoming constraints).
6.  Determine the position for each child according to the [mainAxisAlignment] and the [crossAxisAlignment]. For example, if the [mainAxisAlignment] is [MainAxisAlignment.spaceBetween], any main axis space that has not been allocated to children is divided evenly and placed between the children.

See also:

- [Flex], the widget equivalent.
- [Row] and [Column], direction-specific variants of [Flex].

### RenderFlex()

```dart
RenderFlex({List<RenderBox>? children, Axis direction = Axis.horizontal, MainAxisSize mainAxisSize = MainAxisSize.max, MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, TextBaseline? textBaseline, Clip clipBehavior = Clip.none, double spacing = 0.0})
```

Creates a flex render object.

By default, the flex layout is horizontal and children are aligned to the start of the main axis and the center of the cross axis.

### direction

```dart
Axis get direction
```

The direction to use as the main axis.

### direction

```dart
set direction(Axis value)
```

### mainAxisAlignment

```dart
MainAxisAlignment get mainAxisAlignment
```

How the children should be placed along the main axis.

If the [direction] is [Axis.horizontal], and the [mainAxisAlignment] is either [MainAxisAlignment.start] or [MainAxisAlignment.end], then the [textDirection] must not be null.

If the [direction] is [Axis.vertical], and the [mainAxisAlignment] is either [MainAxisAlignment.start] or [MainAxisAlignment.end], then the [verticalDirection] must not be null.

### mainAxisAlignment

```dart
set mainAxisAlignment(MainAxisAlignment value)
```

### mainAxisSize

```dart
MainAxisSize get mainAxisSize
```

How much space should be occupied in the main axis.

After allocating space to children, there might be some remaining free space. This value controls whether to maximize or minimize the amount of free space, subject to the incoming layout constraints.

If some children have a non-zero flex factors (and none have a fit of [FlexFit.loose]), they will expand to consume all the available space and there will be no remaining free space to maximize or minimize, making this value irrelevant to the final layout.

### mainAxisSize

```dart
set mainAxisSize(MainAxisSize value)
```

### crossAxisAlignment

```dart
CrossAxisAlignment get crossAxisAlignment
```

How the children should be placed along the cross axis.

If the [direction] is [Axis.horizontal], and the [crossAxisAlignment] is either [CrossAxisAlignment.start] or [CrossAxisAlignment.end], then the [verticalDirection] must not be null.

If the [direction] is [Axis.vertical], and the [crossAxisAlignment] is either [CrossAxisAlignment.start] or [CrossAxisAlignment.end], then the [textDirection] must not be null.

### crossAxisAlignment

```dart
set crossAxisAlignment(CrossAxisAlignment value)
```

### textDirection

```dart
TextDirection? get textDirection
```

Determines the order to lay children out horizontally and how to interpret `start` and `end` in the horizontal direction.

If the [direction] is [Axis.horizontal], this controls the order in which children are positioned (left-to-right or right-to-left), and the meaning of the [mainAxisAlignment] property's [MainAxisAlignment.start] and [MainAxisAlignment.end] values.

If the [direction] is [Axis.horizontal], and either the [mainAxisAlignment] is either [MainAxisAlignment.start] or [MainAxisAlignment.end], or there's more than one child, then the [textDirection] must not be null.

If the [direction] is [Axis.vertical], this controls the meaning of the [crossAxisAlignment] property's [CrossAxisAlignment.start] and [CrossAxisAlignment.end] values.

If the [direction] is [Axis.vertical], and the [crossAxisAlignment] is either [CrossAxisAlignment.start] or [CrossAxisAlignment.end], then the [textDirection] must not be null.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### verticalDirection

```dart
VerticalDirection get verticalDirection
```

Determines the order to lay children out vertically and how to interpret `start` and `end` in the vertical direction.

If the [direction] is [Axis.vertical], this controls which order children are painted in (down or up), the meaning of the [mainAxisAlignment] property's [MainAxisAlignment.start] and [MainAxisAlignment.end] values.

If the [direction] is [Axis.vertical], and either the [mainAxisAlignment] is either [MainAxisAlignment.start] or [MainAxisAlignment.end], or there's more than one child, then the [verticalDirection] must not be null.

If the [direction] is [Axis.horizontal], this controls the meaning of the [crossAxisAlignment] property's [CrossAxisAlignment.start] and [CrossAxisAlignment.end] values.

If the [direction] is [Axis.horizontal], and the [crossAxisAlignment] is either [CrossAxisAlignment.start] or [CrossAxisAlignment.end], then the [verticalDirection] must not be null.

### verticalDirection

```dart
set verticalDirection(VerticalDirection value)
```

### textBaseline

```dart
TextBaseline? get textBaseline
```

If aligning items according to their baseline, which baseline to use.

Must not be null if [crossAxisAlignment] is [CrossAxisAlignment.baseline].

### textBaseline

```dart
set textBaseline(TextBaseline? value)
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### spacing

```dart
double get spacing
```

{@template flutter.rendering.RenderFlex.spacing} How much space to place between children in the main axis.

The spacing is only applied between children in the main axis.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.start], then the first child will be placed at the start of the main axis, and the second child will be placed 10.0 pixels after the first child in the main axis, and so on. The [spacing] is not applied before the first child or after the last child.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.end], then the last child will be placed at the end of the main axis, and the second-to-last child will be placed 10.0 pixels before the last child in the main axis, and so on. The [spacing] is not applied before the first child or after the last child.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.center], then the children will be placed in the center of the main axis with 10.0 pixels of space between the children. The [spacing] is not applied before the first child or after the last child.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.spaceBetween], then there will be a minimum of 10.0 pixels of space between each child in the main axis. If the free space is 100.0 pixels between the two children, then the minimum space between the children will be 10.0 pixels and the remaining 90.0 pixels will be the free space between the children. The [spacing] is not applied before the first child or after the last child.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.spaceAround], then there will be a minimum of 10.0 pixels of space between each child in the main axis, and the remaining free space will be placed between the children as well as before the first child and after the last child. The [spacing] is not applied before the first child or after the last child.

If the [spacing] is 10.0 and the [mainAxisAlignment] is [MainAxisAlignment.spaceEvenly], then there will be a minimum of 10.0 pixels of space between each child in the main axis, and the remaining free space will be evenly placed between the children as well as before the first child and after the last child. The [spacing] is not applied before the first child or after the last child.

When the [spacing] is non-zero, the layout size will be larger than the sum of the children's layout sizes in the main axis.

When the total children's layout sizes and total spacing between the children is greater than the maximum constraints in the main axis, then the children will overflow. For example, if there are two children and the maximum constraint is 100.0 pixels, the children's layout sizes are 50.0 pixels each, and the spacing is 10.0 pixels, then the children will overflow by 10.0 pixels.

Defaults to 0.0. {@endtemplate}

### spacing

```dart
set spacing(double value)
```

### setupParentData()

```dart
void setupParentData(RenderBox child)
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

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

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

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
