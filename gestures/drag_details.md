@docImport 'monodrag.dart';

# DragDownDetails

```dart
class DragDownDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details object for callbacks that use [GestureDragDownCallback].

See also:

- [DragGestureRecognizer.onDown], which uses [GestureDragDownCallback].
- [DragStartDetails], the details for [GestureDragStartCallback].
- [DragUpdateDetails], the details for [GestureDragUpdateCallback].
- [DragEndDetails], the details for [GestureDragEndCallback].

### DragDownDetails()

```dart
DragDownDetails({Offset globalPosition = Offset.zero, Offset? localPosition})
```

Creates details for a [GestureDragDownCallback].

### globalPosition

```dart
Offset globalPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.globalPosition}

### localPosition

```dart
Offset localPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.localPosition}

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureDragDownCallback

```dart
typedef GestureDragDownCallback = void Function(DragDownDetails details)
```

Signature for when a pointer has contacted the screen and might begin to move.

The `details` object provides the position of the touch.

See [DragGestureRecognizer.onDown].

# DragStartDetails

```dart
class DragStartDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details object for callbacks that use [GestureDragStartCallback].

See also:

- [DragGestureRecognizer.onStart], which uses [GestureDragStartCallback].
- [DragDownDetails], the details for [GestureDragDownCallback].
- [DragUpdateDetails], the details for [GestureDragUpdateCallback].
- [DragEndDetails], the details for [GestureDragEndCallback].

### DragStartDetails()

```dart
DragStartDetails({Offset globalPosition = Offset.zero, Offset? localPosition, Duration? sourceTimeStamp, PointerDeviceKind? kind})
```

Creates details for a [GestureDragStartCallback].

### globalPosition

```dart
Offset globalPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.globalPosition}

### localPosition

```dart
Offset localPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.localPosition}

### sourceTimeStamp

```dart
Duration? sourceTimeStamp
```

Recorded timestamp of the source pointer event that triggered the drag event.

Could be null if triggered from proxied events such as accessibility.

### kind

```dart
PointerDeviceKind? kind
```

The kind of the device that initiated the event.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureDragStartCallback

```dart
typedef GestureDragStartCallback = void Function(DragStartDetails details)
```

{@template flutter.gestures.dragdetails.GestureDragStartCallback} Signature for when a pointer has contacted the screen and has begun to move.

The `details` object provides the position of the touch when it first touched the surface. {@endtemplate}

See [DragGestureRecognizer.onStart].

# DragUpdateDetails

```dart
class DragUpdateDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details object for callbacks that use [GestureDragUpdateCallback].

See also:

- [DragGestureRecognizer.onUpdate], which uses [GestureDragUpdateCallback].
- [DragDownDetails], the details for [GestureDragDownCallback].
- [DragStartDetails], the details for [GestureDragStartCallback].
- [DragEndDetails], the details for [GestureDragEndCallback].

### DragUpdateDetails()

```dart
DragUpdateDetails({required Offset globalPosition, Offset? localPosition, Duration? sourceTimeStamp, Offset delta = Offset.zero, double? primaryDelta, PointerDeviceKind? kind})
```

Creates details for a [GestureDragUpdateCallback].

If [primaryDelta] is non-null, then its value must match one of the coordinates of [delta] and the other coordinate must be zero.

### globalPosition

```dart
Offset globalPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.globalPosition}

### localPosition

```dart
Offset localPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.localPosition}

### sourceTimeStamp

```dart
Duration? sourceTimeStamp
```

Recorded timestamp of the source pointer event that triggered the drag event.

Could be null if triggered from proxied events such as accessibility.

### delta

```dart
Offset delta
```

The amount the pointer has moved in the coordinate space of the event receiver since the previous update.

If the [GestureDragUpdateCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this offset contains only the delta in that direction (i.e., the coordinate in the other direction is zero).

Defaults to zero if not specified in the constructor.

### primaryDelta

```dart
double? primaryDelta
```

The amount the pointer has moved along the primary axis in the coordinate space of the event receiver since the previous update.

If the [GestureDragUpdateCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this value contains the component of [delta] along the primary axis (e.g., horizontal or vertical, respectively). Otherwise, if the [GestureDragUpdateCallback] is for a two-dimensional drag (e.g., a pan), then this value is null.

Defaults to null if not specified in the constructor.

### kind

```dart
PointerDeviceKind? kind
```

The kind of the device that initiated the event.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureDragUpdateCallback

```dart
typedef GestureDragUpdateCallback = void Function(DragUpdateDetails details)
```

{@template flutter.gestures.dragdetails.GestureDragUpdateCallback} Signature for when a pointer that is in contact with the screen and moving has moved again.

The `details` object provides the position of the touch and the distance it has traveled since the last update. {@endtemplate}

See [DragGestureRecognizer.onUpdate].

# DragEndDetails

```dart
class DragEndDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details object for callbacks that use [GestureDragEndCallback].

See also:

- [DragGestureRecognizer.onEnd], which uses [GestureDragEndCallback].
- [DragDownDetails], the details for [GestureDragDownCallback].
- [DragStartDetails], the details for [GestureDragStartCallback].
- [DragUpdateDetails], the details for [GestureDragUpdateCallback].

### DragEndDetails()

```dart
DragEndDetails({Offset globalPosition = Offset.zero, Offset? localPosition, Velocity velocity = Velocity.zero, double? primaryVelocity})
```

Creates details for a [GestureDragEndCallback].

If [primaryVelocity] is non-null, its value must match one of the coordinates of `velocity.pixelsPerSecond` and the other coordinate must be zero.

### globalPosition

```dart
Offset globalPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.globalPosition}

### localPosition

```dart
Offset localPosition
```

{@macro flutter.gestures.gesturedetails.PositionedGestureDetails.localPosition}

### velocity

```dart
Velocity velocity
```

The velocity the pointer was moving when it stopped contacting the screen.

Defaults to zero if not specified in the constructor.

### primaryVelocity

```dart
double? primaryVelocity
```

The velocity the pointer was moving along the primary axis when it stopped contacting the screen, in logical pixels per second.

If the [GestureDragEndCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this value contains the component of [velocity] along the primary axis (e.g., horizontal or vertical, respectively). Otherwise, if the [GestureDragEndCallback] is for a two-dimensional drag (e.g., a pan), then this value is null.

Defaults to null if not specified in the constructor.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
