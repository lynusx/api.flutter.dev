@docImport 'package:flutter/material.dart';

# SnapshotMode

```dart
enum SnapshotMode {}
```

Controls how the [SnapshotWidget] paints its child.

The child is snapshotted, but only if all descendants can be snapshotted.

If there is a platform view in the children of a snapshot widget, the snapshot will not be used and the child will be rendered using [SnapshotPainter.paint]. This uses an un-snapshotted child and by default paints it with no additional modification.

An error is thrown if the child cannot be snapshotted.

This setting is the default state of the [SnapshotWidget].

The child is snapshotted and any child platform views are ignored.

This mode can be useful if there is a platform view descendant that does not need to be included in the snapshot.

# SnapshotController

```dart
class SnapshotController extends ChangeNotifier {}
```

A controller for the [SnapshotWidget] that controls when the child image is displayed and when to regenerated the child image.

When the value of [allowSnapshotting] is true, the [SnapshotWidget] will paint the child widgets based on the [SnapshotMode] of the snapshot widget.

The controller notifies its listeners when the value of [allowSnapshotting] changes or when [clear] is called.

To force [SnapshotWidget] to recreate the child image, call [clear].

### SnapshotController()

```dart
SnapshotController({bool allowSnapshotting = false})
```

Create a new [SnapshotController].

By default, [allowSnapshotting] is `false` and cannot be `null`.

### clear()

```dart
void clear()
```

Reset the snapshot held by any listening [SnapshotWidget].

This has no effect if [allowSnapshotting] is `false`.

### allowSnapshotting

```dart
bool get allowSnapshotting
```

Whether a snapshot of this child widget is painted in its place.

### allowSnapshotting

```dart
set allowSnapshotting(bool value)
```

# SnapshotWidget

```dart
class SnapshotWidget extends SingleChildRenderObjectWidget {}
```

A widget that can replace its child with a snapshotted version of the child.

A snapshot is a frozen texture-backed representation of all child pictures and layers stored as a [ui.Image].

This widget is useful for performing short animations that would otherwise be expensive or that cannot rely on raster caching. For example, scale and skew animations are often expensive to perform on complex children, as are blurs. For a short animation, a widget that contains these expensive effects can be replaced with a snapshot of itself and manipulated instead.

For example, the Android Q [ZoomPageTransitionsBuilder] uses a snapshot widget for the forward and entering route to avoid the expensive scale animation. This also has the effect of briefly pausing any animations on the page.

Generally, this widget should not be used in places where users expect the child widget to continue animating or to be responsive, such as an unbounded animation.

Caveats:

- The contents of platform views cannot be captured by a snapshot widget. If a platform view is encountered, then the snapshot widget will determine how to render its children based on the [SnapshotMode]. This defaults to [SnapshotMode.normal] which will throw an exception if a platform view is encountered.

- On the CanvasKit backend of Flutter, the performance of using this widget may regress performance due to the fact that both the UI and engine share a single thread.

### SnapshotWidget()

```dart
SnapshotWidget({dynamic key, SnapshotMode mode = SnapshotMode.normal, SnapshotPainter painter = const _DefaultSnapshotPainter(), bool autoresize = false, required SnapshotController controller, required Widget? child})
```

Create a new [SnapshotWidget].

The [controller] and [child] arguments are required.

### controller

```dart
SnapshotController controller
```

The controller that determines when to display the children as a snapshot.

### mode

```dart
SnapshotMode mode
```

Configuration that controls how the snapshot widget decides to paint its children.

Defaults to [SnapshotMode.normal], which throws an error when a platform view or texture view is encountered.

See [SnapshotMode] for more information.

### autoresize

```dart
bool autoresize
```

Whether or not changes in render object size should automatically re-create the snapshot.

Defaults to false.

### painter

```dart
SnapshotPainter painter
```

The painter used to paint the child snapshot or child widgets.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderObject renderObject)
```

# SnapshotPainter

```dart
abstract class SnapshotPainter extends ChangeNotifier {}
```

A painter used to paint either a snapshot or the child widgets that would be a snapshot.

The painter can call [notifyListeners] to have the [SnapshotWidget] re-paint (re-using the same raster). This allows animations to be performed without re-snapshotting of children. For certain scale or perspective changing transforms, such as a rotation, this can be significantly faster than performing the same animation at the widget level.

By default, the [SnapshotWidget] includes a delegate that draws the child raster exactly as the child widgets would have been drawn. Nevertheless, this can also be used to efficiently transform the child raster and apply complex paint effects.

{@tool snippet}

The following method shows how to efficiently rotate the child raster.

```dart
void paint(PaintingContext context, Offset offset, Size size, ui.Image image, double pixelRatio) {
  const double radians = 0.5; // Could be driven by an animation.
  final Matrix4 transform = Matrix4.rotationZ(radians);
  context.canvas.transform(transform.storage);
  final Rect src = Rect.fromLTWH(0, 0, image.width.toDouble(), image.height.toDouble());
  final Rect dst = Rect.fromLTWH(offset.dx, offset.dy, size.width, size.height);
  final Paint paint = Paint()
    ..filterQuality = FilterQuality.medium;
  context.canvas.drawImageRect(image, src, dst, paint);
}
```

{@end-tool}

### SnapshotPainter()

```dart
SnapshotPainter()
```

Creates an instance of [SnapshotPainter].

### paintSnapshot()

```dart
void paintSnapshot(PaintingContext context, Offset offset, Size size, ui.Image image, Size sourceSize, double pixelRatio)
```

Called whenever the [image] that represents a [SnapshotWidget]s child should be painted.

The image is rasterized at the physical pixel resolution and should be scaled down by [pixelRatio] to account for device independent pixels.

{@tool snippet}

The following method shows how the default implementation of the delegate used by the [SnapshotPainter] paints the snapshot. This must account for the fact that the image width and height will be given in physical pixels, while the image must be painted with device independent pixels. That is, the width and height of the image is the widget and height of the provided `size`, multiplied by the `pixelRatio`. In addition, the actual size of the scene captured by the `image` is not `image.width` or `image.height`, but indeed `sourceSize`, because the former is a rounded inaccurate integer:

```dart
void paint(PaintingContext context, Offset offset, Size size, ui.Image image, Size sourceSize, double pixelRatio) {
  final Rect src = Rect.fromLTWH(0, 0, sourceSize.width, sourceSize.height);
  final Rect dst = Rect.fromLTWH(offset.dx, offset.dy, size.width, size.height);
  final Paint paint = Paint()
    ..filterQuality = FilterQuality.medium;
  context.canvas.drawImageRect(image, src, dst, paint);
}
```

{@end-tool}

### paint()

```dart
void paint(PaintingContext context, Offset offset, Size size, PaintingContextCallback painter)
```

Paint the child via [painter], applying any effects that would have been painted in [SnapshotPainter.paintSnapshot].

This method is called when snapshotting is disabled, or when [SnapshotMode.permissive] is used and a child platform view prevents snapshotting.

The [offset] and [size] are the location and dimensions of the render object.

### shouldRepaint()

```dart
bool shouldRepaint(SnapshotPainter oldPainter)
```

Called whenever a new instance of the snapshot widget delegate class is provided to the [SnapshotWidget] object, or any time that a new [SnapshotPainter] object is created with a new instance of the delegate class (which amounts to the same thing, because the latter is implemented in terms of the former).

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If the method returns false, then the [paint] call might be optimized away.

It's possible that the [paint] method will get called even if [shouldRepaint] returns false (e.g. if an ancestor or descendant needed to be repainted). It's also possible that the [paint] method will get called without [shouldRepaint] being called at all (e.g. if the box changes size).

Changing the delegate will not cause the child image retained by the [SnapshotWidget] to be updated. Instead, [SnapshotController.clear] can be used to force the generation of a new image.

The `oldPainter` argument will never be null.
