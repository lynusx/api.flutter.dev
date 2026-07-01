@docImport 'package:flutter/widgets.dart';

@docImport 'arena.dart';

# GestureTapDragDownCallback

```dart
typedef GestureTapDragDownCallback = void Function(TapDragDownDetails details)
```

{@macro flutter.gestures.tap.GestureTapDownCallback}

The consecutive tap count at the time the pointer contacted the screen is given by [TapDragDownDetails.consecutiveTapCount].

Used by [BaseTapAndDragGestureRecognizer.onTapDown].

# TapDragDownDetails

```dart
class TapDragDownDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDragDownCallback], such as the number of consecutive taps.

See also:

- [BaseTapAndDragGestureRecognizer], which passes this information to its [BaseTapAndDragGestureRecognizer.onTapDown] callback.
- [TapDragUpDetails], the details for [GestureTapDragUpCallback].
- [TapDragStartDetails], the details for [GestureTapDragStartCallback].
- [TapDragUpdateDetails], the details for [GestureTapDragUpdateCallback].
- [TapDragEndDetails], the details for [GestureTapDragEndCallback].

### TapDragDownDetails()

```dart
TapDragDownDetails({required Offset globalPosition, required Offset localPosition, PointerDeviceKind? kind, required int consecutiveTapCount})
```

Creates details for a [GestureTapDragDownCallback].

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

### kind

```dart
PointerDeviceKind? kind
```

The kind of the device that initiated the event.

### consecutiveTapCount

```dart
int consecutiveTapCount
```

If this tap is in a series of taps, then this value represents the number in the series this tap is.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureTapDragUpCallback

```dart
typedef GestureTapDragUpCallback = void Function(TapDragUpDetails details)
```

{@macro flutter.gestures.tap.GestureTapUpCallback}

The consecutive tap count at the time the pointer contacted the screen is given by [TapDragUpDetails.consecutiveTapCount].

Used by [BaseTapAndDragGestureRecognizer.onTapUp].

# TapDragUpDetails

```dart
class TapDragUpDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDragUpCallback], such as the number of consecutive taps.

See also:

- [BaseTapAndDragGestureRecognizer], which passes this information to its [BaseTapAndDragGestureRecognizer.onTapUp] callback.
- [TapDragDownDetails], the details for [GestureTapDragDownCallback].
- [TapDragStartDetails], the details for [GestureTapDragStartCallback].
- [TapDragUpdateDetails], the details for [GestureTapDragUpdateCallback].
- [TapDragEndDetails], the details for [GestureTapDragEndCallback].

### TapDragUpDetails()

```dart
TapDragUpDetails({required Offset globalPosition, required Offset localPosition, required PointerDeviceKind kind, required int consecutiveTapCount})
```

Creates details for a [GestureTapDragUpCallback].

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

### kind

```dart
PointerDeviceKind kind
```

The kind of the device that initiated the event.

### consecutiveTapCount

```dart
int consecutiveTapCount
```

If this tap is in a series of taps, then this value represents the number in the series this tap is.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureTapDragStartCallback

```dart
typedef GestureTapDragStartCallback = void Function(TapDragStartDetails details)
```

{@macro flutter.gestures.dragdetails.GestureDragStartCallback}

The consecutive tap count at the time the pointer contacted the screen is given by [TapDragStartDetails.consecutiveTapCount].

Used by [BaseTapAndDragGestureRecognizer.onDragStart].

# TapDragStartDetails

```dart
class TapDragStartDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDragStartCallback], such as the number of consecutive taps.

See also:

- [BaseTapAndDragGestureRecognizer], which passes this information to its [BaseTapAndDragGestureRecognizer.onDragStart] callback.
- [TapDragDownDetails], the details for [GestureTapDragDownCallback].
- [TapDragUpDetails], the details for [GestureTapDragUpCallback].
- [TapDragUpdateDetails], the details for [GestureTapDragUpdateCallback].
- [TapDragEndDetails], the details for [GestureTapDragEndCallback].

### TapDragStartDetails()

```dart
TapDragStartDetails({required Offset globalPosition, required Offset localPosition, Duration? sourceTimeStamp, PointerDeviceKind? kind, required int consecutiveTapCount})
```

Creates details for a [GestureTapDragStartCallback].

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

### consecutiveTapCount

```dart
int consecutiveTapCount
```

If this tap is in a series of taps, then this value represents the number in the series this tap is.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureTapDragUpdateCallback

```dart
typedef GestureTapDragUpdateCallback = void Function(TapDragUpdateDetails details)
```

{@macro flutter.gestures.dragdetails.GestureDragUpdateCallback}

The consecutive tap count at the time the pointer contacted the screen is given by [TapDragUpdateDetails.consecutiveTapCount].

Used by [BaseTapAndDragGestureRecognizer.onDragUpdate].

# TapDragUpdateDetails

```dart
class TapDragUpdateDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDragUpdateCallback], such as the number of consecutive taps.

See also:

- [BaseTapAndDragGestureRecognizer], which passes this information to its [BaseTapAndDragGestureRecognizer.onDragUpdate] callback.
- [TapDragDownDetails], the details for [GestureTapDragDownCallback].
- [TapDragUpDetails], the details for [GestureTapDragUpCallback].
- [TapDragStartDetails], the details for [GestureTapDragStartCallback].
- [TapDragEndDetails], the details for [GestureTapDragEndCallback].

### TapDragUpdateDetails()

```dart
TapDragUpdateDetails({required Offset globalPosition, required Offset localPosition, Duration? sourceTimeStamp, Offset delta = Offset.zero, double? primaryDelta, PointerDeviceKind? kind, required Offset offsetFromOrigin, required Offset localOffsetFromOrigin, required int consecutiveTapCount})
```

Creates details for a [GestureTapDragUpdateCallback].

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

If the [GestureTapDragUpdateCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this offset contains only the delta in that direction (i.e., the coordinate in the other direction is zero).

Defaults to zero if not specified in the constructor.

### primaryDelta

```dart
double? primaryDelta
```

The amount the pointer has moved along the primary axis in the coordinate space of the event receiver since the previous update.

If the [GestureTapDragUpdateCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this value contains the component of [delta] along the primary axis (e.g., horizontal or vertical, respectively). Otherwise, if the [GestureTapDragUpdateCallback] is for a two-dimensional drag (e.g., a pan), then this value is null.

Defaults to null if not specified in the constructor.

### kind

```dart
PointerDeviceKind? kind
```

The kind of the device that initiated the event.

### offsetFromOrigin

```dart
Offset offsetFromOrigin
```

A delta offset from the point where the drag initially contacted the screen to the point where the pointer is currently located in global coordinates (the present [globalPosition]) when this callback is triggered.

When considering a [GestureRecognizer] that tracks the number of consecutive taps, this offset is associated with the most recent [PointerDownEvent] that occurred.

### localOffsetFromOrigin

```dart
Offset localOffsetFromOrigin
```

A local delta offset from the point where the drag initially contacted the screen to the point where the pointer is currently located in local coordinates (the present [localPosition]) when this callback is triggered.

When considering a [GestureRecognizer] that tracks the number of consecutive taps, this offset is associated with the most recent [PointerDownEvent] that occurred.

### consecutiveTapCount

```dart
int consecutiveTapCount
```

If this tap is in a series of taps, then this value represents the number in the series this tap is.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureTapDragEndCallback

```dart
typedef GestureTapDragEndCallback = void Function(TapDragEndDetails endDetails)
```

{@macro flutter.gestures.monodrag.GestureDragEndCallback}

The consecutive tap count at the time the pointer contacted the screen is given by [TapDragEndDetails.consecutiveTapCount].

Used by [BaseTapAndDragGestureRecognizer.onDragEnd].

# TapDragEndDetails

```dart
class TapDragEndDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDragEndCallback], such as the number of consecutive taps.

See also:

- [BaseTapAndDragGestureRecognizer], which passes this information to its [BaseTapAndDragGestureRecognizer.onDragEnd] callback.
- [TapDragDownDetails], the details for [GestureTapDragDownCallback].
- [TapDragUpDetails], the details for [GestureTapDragUpCallback].
- [TapDragStartDetails], the details for [GestureTapDragStartCallback].
- [TapDragUpdateDetails], the details for [GestureTapDragUpdateCallback].

### TapDragEndDetails()

```dart
TapDragEndDetails({Offset globalPosition = Offset.zero, Offset? localPosition, Velocity velocity = Velocity.zero, double? primaryVelocity, required int consecutiveTapCount})
```

Creates details for a [GestureTapDragEndCallback].

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

If the [GestureTapDragEndCallback] is for a one-dimensional drag (e.g., a horizontal or vertical drag), then this value contains the component of [velocity] along the primary axis (e.g., horizontal or vertical, respectively). Otherwise, if the [GestureTapDragEndCallback] is for a two-dimensional drag (e.g., a pan), then this value is null.

Defaults to null if not specified in the constructor.

### consecutiveTapCount

```dart
int consecutiveTapCount
```

If this tap is in a series of taps, then this value represents the number in the series this tap is.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureCancelCallback

```dart
typedef GestureCancelCallback = void Function()
```

Signature for when the pointer that previously triggered a [GestureTapDragDownCallback] did not complete.

Used by [BaseTapAndDragGestureRecognizer.onCancel].

# BaseTapAndDragGestureRecognizer

```dart
sealed class BaseTapAndDragGestureRecognizer extends OneSequenceGestureRecognizer with _TapStatusTrackerMixin {}
```

A base class for gesture recognizers that recognize taps and movements.

Takes on the responsibilities of [TapGestureRecognizer] and [DragGestureRecognizer] in one [GestureRecognizer].

### Gesture arena behavior

[BaseTapAndDragGestureRecognizer] competes on the pointer events of [kPrimaryButton] only when it has at least one non-null `onTap*` or `onDrag*` callback.

It will declare defeat if it determines that a gesture is not a tap (e.g. if the pointer is dragged too far while it's contacting the screen) or a drag (e.g. if the pointer was not dragged far enough to be considered a drag.

This recognizer will not immediately declare victory for every tap that it recognizes, but it declares victory for every drag.

The recognizer will declare victory when all other recognizer's in the arena have lost, if the timer of [kPressTimeout] elapses and a tap series greater than 1 is being tracked, or until the pointer has moved a sufficient global distance from the origin to be considered a drag.

If this recognizer loses the arena (either by declaring defeat or by another recognizer declaring victory) while the pointer is contacting the screen, it will fire [onCancel] instead of [onTapUp] or [onDragEnd].

### When competing with `TapGestureRecognizer` and `DragGestureRecognizer`

Similar to [TapGestureRecognizer] and [DragGestureRecognizer], [BaseTapAndDragGestureRecognizer] will not aggressively declare victory when it detects a tap, so when it is competing with those gesture recognizers and others it has a chance of losing. Similarly, when `eagerVictoryOnDrag` is set to `false`, this recognizer will not aggressively declare victory when it detects a drag. By default, `eagerVictoryOnDrag` is set to `true`, so this recognizer will aggressively declare victory when it detects a drag.

When competing against [TapGestureRecognizer], if the pointer does not move past the tap tolerance, then the recognizer that entered the arena first will win. In this case the gesture detected is a tap. If the pointer does travel past the tap tolerance then this recognizer will be declared winner by default. The gesture detected in this case is a drag.

When competing against [DragGestureRecognizer], if the pointer does not move a sufficient global distance to be considered a drag, the recognizers will tie in the arena. If the pointer does travel enough distance then the recognizer that entered the arena first will win. The gesture detected in this case is a drag.

{@tool dartpad} This example shows how to use the [TapAndPanGestureRecognizer] along with a [RawGestureDetector] to scale a Widget.

** See code in examples/api/lib/gestures/tap_and_drag/tap_and_drag.0.dart ** {@end-tool}

{@tool snippet}

This example shows how to hook up [TapAndPanGestureRecognizer]s' to nested [RawGestureDetector]s'. It assumes that the code is being used inside a [State] object with a `_last` field that is then displayed as the child of the gesture detector.

In this example, if the pointer has moved past the drag threshold, then the the first [TapAndPanGestureRecognizer] instance to receive the [PointerEvent] will win the arena because the recognizer will immediately declare victory.

The first one to receive the event in the example will depend on where on both containers the pointer lands first. If your pointer begins in the overlapping area of both containers, then the inner-most widget will receive the event first. If your pointer begins in the yellow container then it will be the first to receive the event.

If the pointer has not moved past the drag threshold, then the first recognizer to enter the arena will win (i.e. they both tie and the gesture arena will call [GestureArenaManager.sweep] so the first member of the arena will win).

```dart
RawGestureDetector(
  gestures: <Type, GestureRecognizerFactory>{
    TapAndPanGestureRecognizer: GestureRecognizerFactoryWithHandlers<TapAndPanGestureRecognizer>(
      () => TapAndPanGestureRecognizer(),
      (TapAndPanGestureRecognizer instance) {
        instance
          ..onTapDown = (TapDragDownDetails details) { setState(() { _last = 'down_a'; }); }
          ..onDragStart = (TapDragStartDetails details) { setState(() { _last = 'drag_start_a'; }); }
          ..onDragUpdate = (TapDragUpdateDetails details) { setState(() { _last = 'drag_update_a'; }); }
          ..onDragEnd = (TapDragEndDetails details) { setState(() { _last = 'drag_end_a'; }); }
          ..onTapUp = (TapDragUpDetails details) { setState(() { _last = 'up_a'; }); }
          ..onCancel = () { setState(() { _last = 'cancel_a'; }); };
      },
    ),
  },
  child: Container(
    width: 300.0,
    height: 300.0,
    color: Colors.yellow,
    alignment: Alignment.center,
    child: RawGestureDetector(
      gestures: <Type, GestureRecognizerFactory>{
        TapAndPanGestureRecognizer: GestureRecognizerFactoryWithHandlers<TapAndPanGestureRecognizer>(
          () => TapAndPanGestureRecognizer(),
          (TapAndPanGestureRecognizer instance) {
            instance
              ..onTapDown = (TapDragDownDetails details) { setState(() { _last = 'down_b'; }); }
              ..onDragStart = (TapDragStartDetails details) { setState(() { _last = 'drag_start_b'; }); }
              ..onDragUpdate = (TapDragUpdateDetails details) { setState(() { _last = 'drag_update_b'; }); }
              ..onDragEnd = (TapDragEndDetails details) { setState(() { _last = 'drag_end_b'; }); }
              ..onTapUp = (TapDragUpDetails details) { setState(() { _last = 'up_b'; }); }
              ..onCancel = () { setState(() { _last = 'cancel_b'; }); };
          },
        ),
      },
      child: Container(
        width: 150.0,
        height: 150.0,
        color: Colors.blue,
        child: Text(_last),
      ),
    ),
  ),
)
```

{@end-tool}

### BaseTapAndDragGestureRecognizer()

```dart
BaseTapAndDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter, bool eagerVictoryOnDrag = true})
```

Creates a tap and drag gesture recognizer.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

Configure the behavior of offsets passed to [onDragStart].

If set to [DragStartBehavior.start], the [onDragStart] callback will be called with the position of the pointer at the time this gesture recognizer won the arena. If [DragStartBehavior.down], [onDragStart] will be called with the position of the first detected down event for the pointer. When there are no other gestures competing with this gesture in the arena, there's no difference in behavior between the two settings.

For more information about the gesture arena: https://flutter.dev/to/gesture-disambiguation

By default, the drag start behavior is [DragStartBehavior.start].

See also:

- [DragGestureRecognizer.dragStartBehavior], which includes more details and an example.

### dragUpdateThrottleFrequency

```dart
Duration? dragUpdateThrottleFrequency
```

The frequency at which the [onDragUpdate] callback is called.

The value defaults to null, meaning there is no delay for [onDragUpdate] callback.

### maxConsecutiveTap

```dart
int? maxConsecutiveTap
```

An upper bound for the amount of taps that can belong to one tap series.

When this limit is reached the series of taps being tracked by this recognizer will be reset.

### eagerVictoryOnDrag

```dart
bool eagerVictoryOnDrag
```

Whether this recognizer eagerly declares victory when it has detected a drag.

When this value is `false`, this recognizer will wait until it is the last recognizer in the gesture arena before declaring victory on a drag.

Defaults to `true`.

### onTapDown

```dart
GestureTapDragDownCallback? onTapDown
```

{@macro flutter.gestures.tap.TapGestureRecognizer.onTapDown}

This triggers after the down event, once a short timeout ([kPressTimeout]) has elapsed, or once the gestures has won the arena, whichever comes first.

The position of the pointer is provided in the callback's `details` argument, which is a [TapDragDownDetails] object.

{@template flutter.gestures.selectionrecognizers.BaseTapAndDragGestureRecognizer.tapStatusTrackerData} The number of consecutive taps, and the keys that were pressed on tap down are also provided in the callback's `details` argument. {@endtemplate}

See also:

- [kPrimaryButton], the button this callback responds to.
- [TapDragDownDetails], which is passed as an argument to this callback.

### onTapUp

```dart
GestureTapDragUpCallback? onTapUp
```

{@macro flutter.gestures.tap.TapGestureRecognizer.onTapUp}

This triggers on the up event, if the recognizer wins the arena with it or has previously won.

The position of the pointer is provided in the callback's `details` argument, which is a [TapDragUpDetails] object.

{@macro flutter.gestures.selectionrecognizers.BaseTapAndDragGestureRecognizer.tapStatusTrackerData}

See also:

- [kPrimaryButton], the button this callback responds to.
- [TapDragUpDetails], which is passed as an argument to this callback.

### onDragStart

```dart
GestureTapDragStartCallback? onDragStart
```

{@macro flutter.gestures.monodrag.DragGestureRecognizer.onStart}

The position of the pointer is provided in the callback's `details` argument, which is a [TapDragStartDetails] object. The [dragStartBehavior] determines this position.

{@macro flutter.gestures.selectionrecognizers.BaseTapAndDragGestureRecognizer.tapStatusTrackerData}

See also:

- [kPrimaryButton], the button this callback responds to.
- [TapDragStartDetails], which is passed as an argument to this callback.

### onDragUpdate

```dart
GestureTapDragUpdateCallback? onDragUpdate
```

{@macro flutter.gestures.monodrag.DragGestureRecognizer.onUpdate}

The distance traveled by the pointer since the last update is provided in the callback's `details` argument, which is a [TapDragUpdateDetails] object.

{@macro flutter.gestures.selectionrecognizers.BaseTapAndDragGestureRecognizer.tapStatusTrackerData}

See also:

- [kPrimaryButton], the button this callback responds to.
- [TapDragUpdateDetails], which is passed as an argument to this callback.

### onDragEnd

```dart
GestureTapDragEndCallback? onDragEnd
```

{@macro flutter.gestures.monodrag.DragGestureRecognizer.onEnd}

The velocity is provided in the callback's `details` argument, which is a [TapDragEndDetails] object.

{@macro flutter.gestures.selectionrecognizers.BaseTapAndDragGestureRecognizer.tapStatusTrackerData}

See also:

- [kPrimaryButton], the button this callback responds to.
- [TapDragEndDetails], which is passed as an argument to this callback.

### onCancel

```dart
GestureCancelCallback? onCancel
```

The pointer that previously triggered [onTapDown] did not complete.

This is called when a [PointerCancelEvent] is tracked when the [onTapDown] callback was previously called.

It may also be called if a [PointerUpEvent] is tracked after the pointer has moved past the tap tolerance but not past the drag tolerance, and the recognizer has not yet won the arena.

See also:

- [kPrimaryButton], the button this callback responds to.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerEvent event)
```

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### handleNonAllowedPointer()

```dart
void handleNonAllowedPointer(PointerDownEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

### didStopTrackingLastPointer()

```dart
void didStopTrackingLastPointer(int pointer)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```

### rejectGesture()

```dart
void rejectGesture(int pointer)
```

### dispose()

```dart
void dispose()
```

### debugDescription

```dart
String get debugDescription
```

# TapAndHorizontalDragGestureRecognizer

```dart
class TapAndHorizontalDragGestureRecognizer extends BaseTapAndDragGestureRecognizer {}
```

Recognizes taps along with movement in the horizontal direction.

Before this recognizer has won the arena for the primary pointer being tracked, it will only accept a drag on the horizontal axis. If a drag is detected after this recognizer has won the arena then it will accept a drag on any axis.

See also:

- [BaseTapAndDragGestureRecognizer], for the class that provides the main implementation details of this recognizer.
- [TapAndPanGestureRecognizer], for a similar recognizer that accepts a drag on any axis regardless if the recognizer has won the arena for the primary pointer being tracked.
- [HorizontalDragGestureRecognizer], for a similar recognizer that only recognizes horizontal movement.

### TapAndHorizontalDragGestureRecognizer()

```dart
TapAndHorizontalDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices})
```

Create a gesture recognizer for interactions in the horizontal axis.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### debugDescription

```dart
String get debugDescription
```

# TapAndPanGestureRecognizer

```dart
class TapAndPanGestureRecognizer extends BaseTapAndDragGestureRecognizer {}
```

{@template flutter.gestures.selectionrecognizers.TapAndPanGestureRecognizer} Recognizes taps along with both horizontal and vertical movement.

This recognizer will accept a drag on any axis, regardless if it has won the arena for the primary pointer being tracked.

See also:

- [BaseTapAndDragGestureRecognizer], for the class that provides the main implementation details of this recognizer.
- [TapAndHorizontalDragGestureRecognizer], for a similar recognizer that only accepts horizontal drags before it has won the arena for the primary pointer being tracked.
- [PanGestureRecognizer], for a similar recognizer that only recognizes movement. {@endtemplate}

### TapAndPanGestureRecognizer()

```dart
TapAndPanGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices})
```

Create a gesture recognizer for interactions on a plane.

### debugDescription

```dart
String get debugDescription
```

# TapAndDragGestureRecognizer

```dart
class TapAndDragGestureRecognizer extends BaseTapAndDragGestureRecognizer {}
```

{@macro flutter.gestures.selectionrecognizers.TapAndPanGestureRecognizer}

### TapAndDragGestureRecognizer()

```dart
TapAndDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices})
```

Create a gesture recognizer for interactions on a plane.

### debugDescription

```dart
String get debugDescription
```
