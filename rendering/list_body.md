# ListBodyParentData

```dart
class ListBodyParentData extends ContainerBoxParentData<RenderBox> {}
```

Parent data for use with [RenderListBody].

# RenderListBody

```dart
class RenderListBody extends RenderBox with ContainerRenderObjectMixin<RenderBox, ListBodyParentData>, RenderBoxContainerDefaultsMixin<RenderBox, ListBodyParentData> {}
```

Displays its children sequentially along a given axis, forcing them to the dimensions of the parent in the other axis.

This layout algorithm arranges its children linearly along the main axis (either horizontally or vertically). In the cross axis, children are stretched to match the box's cross-axis extent. In the main axis, children are given unlimited space and the box expands its main axis to contain all its children. Because [RenderListBody] boxes expand in the main axis, they must be given unlimited space in the main axis, typically by being contained in a viewport with a scrolling direction that matches the box's main axis.

### RenderListBody()

```dart
RenderListBody({List<RenderBox>? children, AxisDirection axisDirection = AxisDirection.down})
```

Creates a render object that arranges its children sequentially along a given axis.

By default, children are arranged along the vertical axis.

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### axisDirection

```dart
AxisDirection get axisDirection
```

The direction in which the children are laid out.

For example, if the [axisDirection] is [AxisDirection.down], each child will be laid out below the next, vertically.

### axisDirection

```dart
set axisDirection(AxisDirection value)
```

### mainAxis

```dart
Axis get mainAxis
```

The axis (horizontal or vertical) corresponding to the current [axisDirection].

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

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
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

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```
