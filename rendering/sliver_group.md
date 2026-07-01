@docImport 'package:flutter/widgets.dart';

# RenderSliverCrossAxisGroup

```dart
class RenderSliverCrossAxisGroup extends RenderSliver with ContainerRenderObjectMixin<RenderSliver, SliverPhysicalContainerParentData> {}
```

A sliver that places multiple sliver children in a linear array along the cross axis.

Since the extent of the viewport in the cross axis direction is finite, this extent will be divided up and allocated to the children slivers.

The algorithm for dividing up the cross axis extent is as follows. Every widget has a [SliverPhysicalParentData.crossAxisFlex] value associated with them. First, lay out all of the slivers with flex of 0 or null, in which case the slivers themselves will figure out how much cross axis extent to take up. For example, [SliverConstrainedCrossAxis] is an example of a widget which sets its own flex to 0. Then [RenderSliverCrossAxisGroup] will divide up the remaining space to all the remaining children proportionally to each child's flex factor. By default, children of [SliverCrossAxisGroup] are setup to have a flex factor of 1, but a different flex factor can be specified via the [SliverCrossAxisExpanded] widgets.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderSliver child)
```

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderSliver child)
```

### performLayout()

```dart
void performLayout()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderSliver child, Matrix4 transform)
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

# RenderSliverMainAxisGroup

```dart
class RenderSliverMainAxisGroup extends RenderSliver with ContainerRenderObjectMixin<RenderSliver, SliverPhysicalContainerParentData> {}
```

A sliver that places multiple sliver children in a linear array along the main axis.

The layout algorithm lays out slivers one by one. If the sliver is at the top of the viewport or above the top, then we pass in a nonzero [SliverConstraints.scrollOffset] to inform the sliver at what point along the main axis we should start layout. For the slivers that come after it, we compute the amount of space taken up so far to be used as the [SliverPhysicalParentData.paintOffset] and the [SliverConstraints.remainingPaintExtent] to be passed in as a constraint.

Finally, this sliver will also ensure that all child slivers are painted within the total scroll extent of the group by adjusting the child's [SliverPhysicalParentData.paintOffset] as necessary. This can happen for slivers such as [SliverPersistentHeader] which, when pinned, positions itself at the top of the [Viewport] regardless of the scroll offset.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### childScrollOffset()

```dart
double? childScrollOffset(RenderObject child)
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderSliver child)
```

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderSliver child)
```

### performLayout()

```dart
void performLayout()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderSliver child, Matrix4 transform)
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```
