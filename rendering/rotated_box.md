@docImport 'proxy_box.dart';

# RenderRotatedBox

```dart
class RenderRotatedBox extends RenderBox with RenderObjectWithChildMixin<RenderBox> {}
```

Rotates its child by a integral number of quarter turns.

Unlike [RenderTransform], which applies a transform just prior to painting, this object applies its rotation prior to layout, which means the entire rotated box consumes only as much space as required by the rotated child.

### RenderRotatedBox()

```dart
RenderRotatedBox({required int quarterTurns, RenderBox? child})
```

Creates a rotated render box.

### quarterTurns

```dart
int get quarterTurns
```

The number of clockwise quarter turns the child should be rotated.

### quarterTurns

```dart
set quarterTurns(int value)
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

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```
