@docImport 'package:flutter/widgets.dart';

# WrapAlignment

```dart
enum WrapAlignment {}
```

How [Wrap] should align objects.

Used both to align children within a run in the main axis as well as to align the runs themselves in the cross axis.

Place the objects as close to the start of the axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the start is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the start is the top or the bottom.

Place the objects as close to the end of the axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the end is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the end is the top or the bottom.

Place the objects as close to the middle of the axis as possible.

Place the free space evenly between the objects.

Place the free space evenly between the objects as well as half of that space before and after the first and last objects.

Place the free space evenly between the objects as well as before and after the first and last objects.

# WrapCrossAlignment

```dart
enum WrapCrossAlignment {}
```

Who [Wrap] should align children within a run in the cross axis.

Place the children as close to the start of the run in the cross axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the start is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the start is the top or the bottom.

Place the children as close to the end of the run in the cross axis as possible.

If this value is used in a horizontal direction, a [TextDirection] must be available to determine if the end is the left or the right.

If this value is used in a vertical direction, a [VerticalDirection] must be available to determine if the end is the top or the bottom.

Place the children as close to the middle of the run in the cross axis as possible.

# WrapParentData

```dart
class WrapParentData extends ContainerBoxParentData<RenderBox> {}
```

Parent data for use with [RenderWrap].

# RenderWrap

```dart
class RenderWrap extends RenderBox with ContainerRenderObjectMixin<RenderBox, WrapParentData>, RenderBoxContainerDefaultsMixin<RenderBox, WrapParentData> {}
```

Displays its children in multiple horizontal or vertical runs.

A [RenderWrap] lays out each child and attempts to place the child adjacent to the previous child in the main axis, given by [direction], leaving [spacing] space in between. If there is not enough space to fit the child, [RenderWrap] creates a new _run_ adjacent to the existing children in the cross axis.

After all the children have been allocated to runs, the children within the runs are positioned according to the [alignment] in the main axis and according to the [crossAxisAlignment] in the cross axis.

The runs themselves are then positioned in the cross axis according to the [runSpacing] and [runAlignment].

### RenderWrap()

```dart
RenderWrap({List<RenderBox>? children, Axis direction = Axis.horizontal, WrapAlignment alignment = WrapAlignment.start, double spacing = 0.0, WrapAlignment runAlignment = WrapAlignment.start, double runSpacing = 0.0, WrapCrossAlignment crossAxisAlignment = WrapCrossAlignment.start, TextDirection? textDirection, VerticalDirection verticalDirection = VerticalDirection.down, Clip clipBehavior = Clip.none})
```

Creates a wrap render object.

By default, the wrap layout is horizontal and both the children and the runs are aligned to the start.

### direction

```dart
Axis get direction
```

The direction to use as the main axis.

For example, if [direction] is [Axis.horizontal], the default, the children are placed adjacent to one another in a horizontal run until the available horizontal space is consumed, at which point a subsequent children are placed in a new run vertically adjacent to the previous run.

### direction

```dart
set direction(Axis value)
```

### alignment

```dart
WrapAlignment get alignment
```

How the children within a run should be placed in the main axis.

For example, if [alignment] is [WrapAlignment.center], the children in each run are grouped together in the center of their run in the main axis.

Defaults to [WrapAlignment.start].

See also:

- [runAlignment], which controls how the runs are placed relative to each other in the cross axis.
- [crossAxisAlignment], which controls how the children within each run are placed relative to each other in the cross axis.

### alignment

```dart
set alignment(WrapAlignment value)
```

### spacing

```dart
double get spacing
```

How much space to place between children in a run in the main axis.

For example, if [spacing] is 10.0, the children will be spaced at least 10.0 logical pixels apart in the main axis.

If there is additional free space in a run (e.g., because the wrap has a minimum size that is not filled or because some runs are longer than others), the additional free space will be allocated according to the [alignment].

Defaults to 0.0.

### spacing

```dart
set spacing(double value)
```

### runAlignment

```dart
WrapAlignment get runAlignment
```

How the runs themselves should be placed in the cross axis.

For example, if [runAlignment] is [WrapAlignment.center], the runs are grouped together in the center of the overall [RenderWrap] in the cross axis.

Defaults to [WrapAlignment.start].

See also:

- [alignment], which controls how the children within each run are placed relative to each other in the main axis.
- [crossAxisAlignment], which controls how the children within each run are placed relative to each other in the cross axis.

### runAlignment

```dart
set runAlignment(WrapAlignment value)
```

### runSpacing

```dart
double get runSpacing
```

How much space to place between the runs themselves in the cross axis.

For example, if [runSpacing] is 10.0, the runs will be spaced at least 10.0 logical pixels apart in the cross axis.

If there is additional free space in the overall [RenderWrap] (e.g., because the wrap has a minimum size that is not filled), the additional free space will be allocated according to the [runAlignment].

Defaults to 0.0.

### runSpacing

```dart
set runSpacing(double value)
```

### crossAxisAlignment

```dart
WrapCrossAlignment get crossAxisAlignment
```

How the children within a run should be aligned relative to each other in the cross axis.

For example, if this is set to [WrapCrossAlignment.end], and the [direction] is [Axis.horizontal], then the children within each run will have their bottom edges aligned to the bottom edge of the run.

Defaults to [WrapCrossAlignment.start].

See also:

- [alignment], which controls how the children within each run are placed relative to each other in the main axis.
- [runAlignment], which controls how the runs are placed relative to each other in the cross axis.

### crossAxisAlignment

```dart
set crossAxisAlignment(WrapCrossAlignment value)
```

### textDirection

```dart
TextDirection? get textDirection
```

Determines the order to lay children out horizontally and how to interpret `start` and `end` in the horizontal direction.

If the [direction] is [Axis.horizontal], this controls the order in which children are positioned (left-to-right or right-to-left), and the meaning of the [alignment] property's [WrapAlignment.start] and [WrapAlignment.end] values.

If the [direction] is [Axis.horizontal], and either the [alignment] is either [WrapAlignment.start] or [WrapAlignment.end], or there's more than one child, then the [textDirection] must not be null.

If the [direction] is [Axis.vertical], this controls the order in which runs are positioned, the meaning of the [runAlignment] property's [WrapAlignment.start] and [WrapAlignment.end] values, as well as the [crossAxisAlignment] property's [WrapCrossAlignment.start] and [WrapCrossAlignment.end] values.

If the [direction] is [Axis.vertical], and either the [runAlignment] is either [WrapAlignment.start] or [WrapAlignment.end], the [crossAxisAlignment] is either [WrapCrossAlignment.start] or [WrapCrossAlignment.end], or there's more than one child, then the [textDirection] must not be null.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### verticalDirection

```dart
VerticalDirection get verticalDirection
```

Determines the order to lay children out vertically and how to interpret `start` and `end` in the vertical direction.

If the [direction] is [Axis.vertical], this controls which order children are painted in (down or up), the meaning of the [alignment] property's [WrapAlignment.start] and [WrapAlignment.end] values.

If the [direction] is [Axis.vertical], and either the [alignment] is either [WrapAlignment.start] or [WrapAlignment.end], or there's more than one child, then the [verticalDirection] must not be null.

If the [direction] is [Axis.horizontal], this controls the order in which runs are positioned, the meaning of the [runAlignment] property's [WrapAlignment.start] and [WrapAlignment.end] values, as well as the [crossAxisAlignment] property's [WrapCrossAlignment.start] and [WrapCrossAlignment.end] values.

If the [direction] is [Axis.horizontal], and either the [runAlignment] is either [WrapAlignment.start] or [WrapAlignment.end], the [crossAxisAlignment] is either [WrapCrossAlignment.start] or [WrapCrossAlignment.end], or there's more than one child, then the [verticalDirection] must not be null.

### verticalDirection

```dart
set verticalDirection(VerticalDirection value)
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

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
