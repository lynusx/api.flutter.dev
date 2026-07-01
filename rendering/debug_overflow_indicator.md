@docImport 'flex.dart'; @docImport 'shifted_box.dart';

# DebugOverflowIndicatorMixin

```dart
mixin DebugOverflowIndicatorMixin on RenderObject {}
```

An mixin indicator that is drawn when a [RenderObject] overflows its container.

This is used by some RenderObjects that are containers to show where, and by how much, their children overflow their containers. These indicators are typically only shown in a debug build (where the call to [paintOverflowIndicator] is surrounded by an assert).

This class will also print a debug message to the console when the container overflows. It will print on the first occurrence, and once after each time that [reassemble] is called.

{@tool snippet}

```dart
class MyRenderObject extends RenderAligningShiftedBox with DebugOverflowIndicatorMixin {
  MyRenderObject({
    super.alignment = Alignment.center,
    required super.textDirection,
    super.child,
  });

  late Rect _containerRect;
  late Rect _childRect;

  @override
  void performLayout() {
    // ...
    final BoxParentData childParentData = child!.parentData! as BoxParentData;
    _containerRect = Offset.zero & size;
    _childRect = childParentData.offset & child!.size;
  }

  @override
  void paint(PaintingContext context, Offset offset) {
    // Do normal painting here...
    // ...

    assert(() {
      paintOverflowIndicator(context, offset, _containerRect, _childRect);
      return true;
    }());
  }
}
```

{@end-tool}

See also:

- [RenderConstraintsTransformBox] and [RenderFlex] for examples of classes that use this indicator mixin.

### dispose()

```dart
void dispose()
```

### paintOverflowIndicator()

```dart
void paintOverflowIndicator(PaintingContext context, Offset offset, Rect containerRect, Rect childRect, {List<DiagnosticsNode>? overflowHints})
```

To be called when the overflow indicators should be painted.

Typically only called if there is an overflow, and only from within a debug build.

See example code in [DebugOverflowIndicatorMixin] documentation.

### reassemble()

```dart
void reassemble()
```
