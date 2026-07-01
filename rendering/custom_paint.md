@docImport 'package:flutter/widgets.dart';

# SemanticsBuilderCallback

```dart
typedef SemanticsBuilderCallback = List<CustomPainterSemantics> Function(Size size)
```

Signature of the function returned by [CustomPainter.semanticsBuilder].

Builds semantics information describing the picture drawn by a [CustomPainter]. Each [CustomPainterSemantics] in the returned list is converted into a [SemanticsNode] by copying its properties.

The returned list must not be mutated after this function completes. To change the semantic information, the function must return a new list instead.

# CustomPainter

```dart
abstract class CustomPainter extends Listenable {}
```

The interface used by [CustomPaint] (in the widgets library) and [RenderCustomPaint] (in the rendering library).

To implement a custom painter, either subclass or implement this interface to define your custom paint delegate. [CustomPainter] subclasses must implement the [paint] and [shouldRepaint] methods, and may optionally also implement the [hitTest] and [shouldRebuildSemantics] methods, and the [semanticsBuilder] getter.

The [paint] method is called whenever the custom object needs to be repainted.

The [shouldRepaint] method is called when a new instance of the class is provided, to check if the new instance actually represents different information.

{@youtube 560 315 https://www.youtube.com/watch?v=vvI_NUXK00s}

The most efficient way to trigger a repaint is to either:

- Extend this class and supply a `repaint` argument to the constructor of the [CustomPainter], where that object notifies its listeners when it is time to repaint.
- Extend [Listenable] (e.g. via [ChangeNotifier]) and implement [CustomPainter], so that the object itself provides the notifications directly.

In either case, the [CustomPaint] widget or [RenderCustomPaint] render object will listen to the [Listenable] and repaint whenever the animation ticks, avoiding both the build and layout phases of the pipeline.

The [hitTest] method is called when the user interacts with the underlying render object, to determine if the user hit the object or missed it.

The [semanticsBuilder] is called whenever the custom object needs to rebuild its semantics information.

The [shouldRebuildSemantics] method is called when a new instance of the class is provided, to check if the new instance contains different information that affects the semantics tree.

{@tool snippet}

This sample extends the same code shown for [RadialGradient] to create a custom painter that paints a sky.

```dart
class Sky extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final Rect rect = Offset.zero & size;
    const RadialGradient gradient = RadialGradient(
      center: Alignment(0.7, -0.6),
      radius: 0.2,
      colors: <Color>[Color(0xFFFFFF00), Color(0xFF0099FF)],
      stops: <double>[0.4, 1.0],
    );
    canvas.drawRect(
      rect,
      Paint()..shader = gradient.createShader(rect),
    );
  }

  @override
  SemanticsBuilderCallback get semanticsBuilder {
    return (Size size) {
      // Annotate a rectangle containing the picture of the sun
      // with the label "Sun". When text to speech feature is enabled on the
      // device, a user will be able to locate the sun on this picture by
      // touch.
      Rect rect = Offset.zero & size;
      final double width = size.shortestSide * 0.4;
      rect = const Alignment(0.8, -0.9).inscribe(Size(width, width), rect);
      return <CustomPainterSemantics>[
        CustomPainterSemantics(
          rect: rect,
          properties: const SemanticsProperties(
            label: 'Sun',
            textDirection: TextDirection.ltr,
          ),
        ),
      ];
    };
  }

  // Since this Sky painter has no fields, it always paints
  // the same thing and semantics information is the same.
  // Therefore we return false here. If we had fields (set
  // from the constructor) then we would return true if any
  // of them differed from the same fields on the oldDelegate.
  @override
  bool shouldRepaint(Sky oldDelegate) => false;
  @override
  bool shouldRebuildSemantics(Sky oldDelegate) => false;
}
```

{@end-tool}

## Composition and the sharing of canvases

Widgets (or rather, render objects) are composited together using a minimum number of [Canvas]es, for performance reasons. As a result, a [CustomPainter]'s [Canvas] may be the same as that used by other widgets (including other [CustomPaint] widgets).

This is mostly unnoticeable, except when using unusual [BlendMode]s. For example, trying to use [BlendMode.dstOut] to "punch a hole" through a previously-drawn image may erase more than was intended, because previous widgets will have been painted onto the same canvas.

To avoid this issue, consider using [Canvas.saveLayer] and [Canvas.restore] when using such blend modes. Creating new layers is relatively expensive, however, and should be done sparingly to avoid introducing jank.

See also:

- [Canvas], the class that a custom painter uses to paint.
- [CustomPaint], the widget that uses [CustomPainter], and whose sample code shows how to use the above `Sky` class.
- [RadialGradient], whose sample code section shows a different take on the sample code above.

### CustomPainter()

```dart
CustomPainter({Listenable? repaint})
```

Creates a custom painter.

The painter will repaint whenever `repaint` notifies its listeners.

### addListener()

```dart
void addListener(VoidCallback listener)
```

Register a closure to be notified when it is time to repaint.

The [CustomPainter] implementation merely forwards to the same method on the [Listenable] provided to the constructor in the `repaint` argument, if it was not null.

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Remove a previously registered closure from the list of closures that the object notifies when it is time to repaint.

The [CustomPainter] implementation merely forwards to the same method on the [Listenable] provided to the constructor in the `repaint` argument, if it was not null.

### paint()

```dart
void paint(Canvas canvas, Size size)
```

Called whenever the object needs to paint. The given [Canvas] has its coordinate space configured such that the origin is at the top left of the box. The area of the box is the size of the [size] argument.

Paint operations should remain inside the given area. Graphical operations outside the bounds may be silently ignored, clipped, or not clipped. It may sometimes be difficult to guarantee that a certain operation is inside the bounds (e.g., drawing a rectangle whose size is determined by user inputs). In that case, consider calling [Canvas.clipRect] at the beginning of [paint] so everything that follows will be guaranteed to only draw within the clipped area.

Implementations should be wary of correctly pairing any calls to [Canvas.save]/[Canvas.saveLayer] and [Canvas.restore], otherwise all subsequent painting on this canvas may be affected, with potentially hilarious but confusing results.

To paint text on a [Canvas], use a [TextPainter].

To paint an image on a [Canvas]:

1.  Obtain an [ImageStream], for example by calling [ImageProvider.resolve] on an [AssetImage] or [NetworkImage] object.

2.  Whenever the [ImageStream]'s underlying [ImageInfo] object changes (see [ImageStream.addListener]), create a new instance of your custom paint delegate, giving it the new [ImageInfo] object.

3.  In your delegate's [paint] method, call the [Canvas.drawImage], [Canvas.drawImageRect], or [Canvas.drawImageNine] methods to paint the [ImageInfo.image] object, applying the [ImageInfo.scale] value to obtain the correct rendering size.

### semanticsBuilder

```dart
SemanticsBuilderCallback? get semanticsBuilder
```

Returns a function that builds semantic information for the picture drawn by this painter.

If the returned function is null, this painter will not contribute new [SemanticsNode]s to the semantics tree and the [CustomPaint] corresponding to this painter will not create a semantics boundary. However, if the child of a [CustomPaint] is not null, the child may contribute [SemanticsNode]s to the tree.

See also:

- [SemanticsConfiguration.isSemanticBoundary], which causes new [SemanticsNode]s to be added to the semantics tree.
- [RenderCustomPaint], which uses this getter to build semantics.

### shouldRebuildSemantics()

```dart
bool shouldRebuildSemantics(CustomPainter oldDelegate)
```

Called whenever a new instance of the custom painter delegate class is provided to the [RenderCustomPaint] object, or any time that a new [CustomPaint] object is created with a new instance of the custom painter delegate class (which amounts to the same thing, because the latter is implemented in terms of the former).

If the new instance would cause [semanticsBuilder] to create different semantics information, then this method should return true, otherwise it should return false.

If the method returns false, then the [semanticsBuilder] call might be optimized away.

It's possible that the [semanticsBuilder] will get called even if [shouldRebuildSemantics] would return false. For example, it is called when the [CustomPaint] is rendered for the very first time, or when the box changes its size.

By default this method delegates to [shouldRepaint] under the assumption that in most cases semantics change when something new is drawn.

### shouldRepaint()

```dart
bool shouldRepaint(CustomPainter oldDelegate)
```

Called whenever a new instance of the custom painter delegate class is provided to the [RenderCustomPaint] object, or any time that a new [CustomPaint] object is created with a new instance of the custom painter delegate class (which amounts to the same thing, because the latter is implemented in terms of the former).

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If the method returns false, then the [paint] call might be optimized away.

It's possible that the [paint] method will get called even if [shouldRepaint] returns false (e.g. if an ancestor or descendant needed to be repainted). It's also possible that the [paint] method will get called without [shouldRepaint] being called at all (e.g. if the box changes size).

If a custom delegate has a particularly expensive paint function such that repaints should be avoided as much as possible, a [RepaintBoundary] or [RenderRepaintBoundary] (or other render object with [RenderObject.isRepaintBoundary] set to true) might be helpful.

The `oldDelegate` argument will never be null.

### hitTest()

```dart
bool? hitTest(Offset position)
```

Called whenever a hit test is being performed on an object that is using this custom paint delegate.

The given point is relative to the same coordinate space as the last [paint] call.

The default behavior is to consider all points to be hits for background painters, and no points to be hits for foreground painters.

Return true if the given position corresponds to a point on the drawn image that should be considered a "hit", false if it corresponds to a point that should be considered outside the painted image, and null to use the default behavior.

### toString()

```dart
String toString()
```

# CustomPainterSemantics

```dart
class CustomPainterSemantics {}
```

Contains properties describing information drawn in a rectangle contained by the [Canvas] used by a [CustomPaint].

This information is used, for example, by assistive technologies to improve the accessibility of applications.

Implement [CustomPainter.semanticsBuilder] to build the semantic description of the whole picture drawn by a [CustomPaint], rather than one particular rectangle.

See also:

- [SemanticsNode], which is created using the properties of this class.
- [CustomPainter], which creates instances of this class.

### CustomPainterSemantics()

```dart
CustomPainterSemantics({Key? key, required Rect rect, required SemanticsProperties properties, Matrix4? transform, Set<SemanticsTag>? tags})
```

Creates semantics information describing a rectangle on a canvas.

### key

```dart
Key? key
```

Identifies this object in a list of siblings.

[SemanticsNode] inherits this key, so that when the list of nodes is updated, its nodes are updated from [CustomPainterSemantics] with matching keys.

If this is null, the update algorithm does not guarantee which [SemanticsNode] will be updated using this instance.

This value is assigned to [SemanticsNode.key] during update.

### rect

```dart
Rect rect
```

The location and size of the box on the canvas where this piece of semantic information applies.

This value is assigned to [SemanticsNode.rect] during update.

### transform

```dart
Matrix4? transform
```

The transform from the canvas' coordinate system to its parent's coordinate system.

This value is assigned to [SemanticsNode.transform] during update.

### properties

```dart
SemanticsProperties properties
```

Contains properties that are assigned to the [SemanticsNode] created or updated from this object.

See also:

- [Semantics], which is a widget that also uses [SemanticsProperties] to annotate.

### tags

```dart
Set<SemanticsTag>? tags
```

Tags used by the parent [SemanticsNode] to determine the layout of the semantics tree.

This value is assigned to [SemanticsNode.tags] during update.

# RenderCustomPaint

```dart
class RenderCustomPaint extends RenderProxyBox {}
```

Provides a canvas on which to draw during the paint phase.

When asked to paint, [RenderCustomPaint] first asks its [painter] to paint on the current canvas, then it paints its child, and then, after painting its child, it asks its [foregroundPainter] to paint. The coordinate system of the canvas matches the coordinate system of the [CustomPaint] object. The painters are expected to paint within a rectangle starting at the origin and encompassing a region of the given size. (If the painters paint outside those bounds, there might be insufficient memory allocated to rasterize the painting commands and the resulting behavior is undefined.)

Painters are implemented by subclassing or implementing [CustomPainter].

Because custom paint calls its painters during paint, you cannot mark the tree as needing a new layout during the callback (the layout for this frame has already happened).

Custom painters normally size themselves to their child. If they do not have a child, they attempt to size themselves to the [preferredSize], which defaults to [Size.zero].

See also:

- [CustomPainter], the class that custom painter delegates should extend.
- [Canvas], the API provided to custom painter delegates.

### RenderCustomPaint()

```dart
RenderCustomPaint({CustomPainter? painter, CustomPainter? foregroundPainter, Size preferredSize = Size.zero, bool isComplex = false, bool willChange = false, RenderBox? child})
```

Creates a render object that delegates its painting.

### painter

```dart
CustomPainter? get painter
```

The background custom paint delegate.

This painter, if non-null, is called to paint behind the children.

### painter

```dart
set painter(CustomPainter? value)
```

Set a new background custom paint delegate.

If the new delegate is the same as the previous one, this does nothing.

If the new delegate is the same class as the previous one, then the new delegate has its [CustomPainter.shouldRepaint] called; if the result is true, then the delegate will be called.

If the new delegate is a different class than the previous one, then the delegate will be called.

If the new value is null, then there is no background custom painter.

### foregroundPainter

```dart
CustomPainter? get foregroundPainter
```

The foreground custom paint delegate.

This painter, if non-null, is called to paint in front of the children.

### foregroundPainter

```dart
set foregroundPainter(CustomPainter? value)
```

Set a new foreground custom paint delegate.

If the new delegate is the same as the previous one, this does nothing.

If the new delegate is the same class as the previous one, then the new delegate has its [CustomPainter.shouldRepaint] called; if the result is true, then the delegate will be called.

If the new delegate is a different class than the previous one, then the delegate will be called.

If the new value is null, then there is no foreground custom painter.

### preferredSize

```dart
Size get preferredSize
```

The size that this [RenderCustomPaint] should aim for, given the layout constraints, if there is no child.

Defaults to [Size.zero].

If there's a child, this is ignored, and the size of the child is used instead.

### preferredSize

```dart
set preferredSize(Size value)
```

### isComplex

```dart
bool isComplex
```

Whether to hint that this layer's painting should be cached.

The compositor contains a raster cache that holds bitmaps of layers in order to avoid the cost of repeatedly rendering those layers on each frame. If this flag is not set, then the compositor will apply its own heuristics to decide whether the layer containing this render object is complex enough to benefit from caching.

### willChange

```dart
bool willChange
```

Whether the raster cache should be told that this painting is likely to change in the next frame.

This hint tells the compositor not to cache the layer containing this render object because the cache will not be used in the future. If this hint is not set, the compositor will apply its own heuristics to decide whether this layer is likely to be reused in the future.

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

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### performLayout()

```dart
void performLayout()
```

### computeSizeForNoChild()

```dart
Size computeSizeForNoChild(BoxConstraints constraints)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### assembleSemanticsNode()

```dart
void assembleSemanticsNode(SemanticsNode node, SemanticsConfiguration config, Iterable<SemanticsNode> children)
```

### clearSemantics()

```dart
void clearSemantics()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
