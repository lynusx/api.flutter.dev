# PositionedGestureDetails

```dart
abstract interface class PositionedGestureDetails {}
```

An abstract interface representing gesture details that include positional information.

This class serve as a common interface for gesture details that involve positional data, such as dragging and tapping. It simplifies gesture handling by enabling the use of shared logic across multiple gesture types, users can create a method to handle a single gesture details with this position information. For example:

```dart
void handlePositionedGestures(PositionedGestureDetails details) {
  // Handle the positional information of the gesture details.
}
```

### PositionedGestureDetails()

```dart
PositionedGestureDetails({required Offset globalPosition, required Offset localPosition})
```

Creates details with positions.

### globalPosition

```dart
Offset globalPosition
```

{@template flutter.gestures.gesturedetails.PositionedGestureDetails.globalPosition} The global position at which the pointer interacts with the screen.

See also:

- [localPosition], which is the [globalPosition] transformed to the coordinate space of the event receiver. {@endtemplate}

### localPosition

```dart
Offset localPosition
```

{@template flutter.gestures.gesturedetails.PositionedGestureDetails.localPosition} The local position in the coordinate system of the event receiver at which the pointer interacts with the screen.

See also:

- [globalPosition], which is the global position at which the pointer interacts with the screen. {@endtemplate}
