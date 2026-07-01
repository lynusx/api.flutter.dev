# DragBoundaryDelegate

```dart
abstract class DragBoundaryDelegate<T> {}
```

The interface for defining the algorithm for a boundary that a specified shape is dragged within.

See also:

- [DragBoundary], an [InheritedWidget] that provides a [DragBoundaryDelegate] to its descendants.

`T` is a data class that defines the shape being dragged. For example, when dragging a rectangle within the boundary, `T` should be a `Rect`.

### isWithinBoundary()

```dart
bool isWithinBoundary(T draggedObject)
```

Returns whether the specified dragged object is within the boundary.

### nearestPositionWithinBoundary()

```dart
T nearestPositionWithinBoundary(T draggedObject)
```

Returns the given dragged object after moving it fully inside the boundary with the shortest distance.

If the bounds cannot contain the dragged object, an exception is thrown.

# DragBoundary

```dart
class DragBoundary extends InheritedWidget {}
```

Provides a [DragBoundaryDelegate] for its descendants whose bounds are those defined by this widget.

[forRectOf] and [forRectMaybeOf] returns a delegate for a drag object of type [Rect].

{@tool dartpad} This example demonstrates dragging a red box, constrained within the bounds of a green box.

** See code in examples/api/lib/widgets/gesture_detector/gesture_detector.3.dart ** {@end-tool}

### DragBoundary()

```dart
DragBoundary({required Widget child, dynamic key})
```

Creates a widget that provides a boundary to its descendants.

### forRectOf()

```dart
DragBoundaryDelegate<Rect> forRectOf(BuildContext context, {bool useGlobalPosition = true})
```

{@template flutter.widgets.DragBoundary.forRectOf} Retrieve the [DragBoundary] from the nearest ancestor to get its [DragBoundaryDelegate] of [Rect].

The [useGlobalPosition] specifies whether to retrieve the [DragBoundaryDelegate] of type [Rect] in global coordinates. If false, the local coordinates of the boundary are used. Defaults to true. {@endtemplate}

If no [DragBoundary] ancestor is found, the delegate will return a delegate that allows the drag object to move freely.

### forRectMaybeOf()

```dart
DragBoundaryDelegate<Rect>? forRectMaybeOf(BuildContext context, {bool useGlobalPosition = true})
```

{@macro flutter.widgets.DragBoundary.forRectOf}

returns null if not ancestor is found.

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedWidget oldWidget)
```
