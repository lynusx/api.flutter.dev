@docImport 'package:flutter/widgets.dart';

# RenderSliverEdgeInsetsPadding

```dart
abstract class RenderSliverEdgeInsetsPadding extends RenderSliver with RenderObjectWithChildMixin<RenderSliver> {}
```

Insets a [RenderSliver] by applying [resolvedPadding] on each side.

A [RenderSliverEdgeInsetsPadding] subclass wraps the [SliverGeometry.layoutExtent] of its child. Any incoming [SliverConstraints.overlap] is ignored and not passed on to the child.

{@template flutter.rendering.RenderSliverEdgeInsetsPadding} Applying padding in the main extent of the viewport to slivers that have scroll effects is likely to have undesired effects. For example, wrapping a [SliverPersistentHeader] with `pinned:true` will cause only the appbar to stay pinned while the padding will scroll away. {@endtemplate}

### resolvedPadding

```dart
EdgeInsets? get resolvedPadding
```

The amount to pad the child in each dimension.

The offsets are specified in terms of visual edges, left, top, right, and bottom. These values are not affected by the [TextDirection].

Must not be null or contain negative values when [performLayout] is called.

### beforePadding

```dart
double get beforePadding
```

The padding in the scroll direction on the side nearest the 0.0 scroll direction.

Only valid after layout has started, since before layout the render object doesn't know what direction it will be laid out in.

### afterPadding

```dart
double get afterPadding
```

The padding in the scroll direction on the side furthest from the 0.0 scroll offset.

Only valid after layout has started, since before layout the render object doesn't know what direction it will be laid out in.

### mainAxisPadding

```dart
double get mainAxisPadding
```

The total padding in the [SliverConstraints.axisDirection]. (In other words, for a vertical downwards-growing list, the sum of the padding on the top and bottom.)

Only valid after layout has started, since before layout the render object doesn't know what direction it will be laid out in.

### crossAxisPadding

```dart
double get crossAxisPadding
```

The total padding in the cross-axis direction. (In other words, for a vertical downwards-growing list, the sum of the padding on the left and right.)

Only valid after layout has started, since before layout the render object doesn't know what direction it will be laid out in.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### performLayout()

```dart
void performLayout()
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderSliver child)
```

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderSliver child)
```

### childScrollOffset()

```dart
double? childScrollOffset(RenderObject child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaint()

```dart
void debugPaint(PaintingContext context, Offset offset)
```

# RenderSliverPadding

```dart
class RenderSliverPadding extends RenderSliverEdgeInsetsPadding {}
```

Insets a [RenderSliver], applying padding on each side.

A [RenderSliverPadding] object wraps the [SliverGeometry.layoutExtent] of its child. Any incoming [SliverConstraints.overlap] is ignored and not passed on to the child.

{@macro flutter.rendering.RenderSliverEdgeInsetsPadding}

### RenderSliverPadding()

```dart
RenderSliverPadding({required EdgeInsetsGeometry padding, TextDirection? textDirection, RenderSliver? child})
```

Creates a render object that insets its child in a viewport.

The [padding] argument must have non-negative insets.

### resolvedPadding

```dart
EdgeInsets? get resolvedPadding
```

### padding

```dart
EdgeInsetsGeometry get padding
```

The amount to pad the child in each dimension.

If this is set to an [EdgeInsetsDirectional] object, then [textDirection] must not be null.

### padding

```dart
set padding(EdgeInsetsGeometry value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [padding].

This may be changed to null, but only after the [padding] has been changed to a value that does not depend on the direction.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### performLayout()

```dart
void performLayout()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
