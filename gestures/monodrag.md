@docImport 'package:flutter/widgets.dart';

@docImport 'multidrag.dart';

# GestureDragEndCallback

```dart
typedef GestureDragEndCallback = void Function(DragEndDetails details)
```

{@template flutter.gestures.monodrag.GestureDragEndCallback} Signature for when a pointer that was previously in contact with the screen and moving is no longer in contact with the screen.

The velocity at which the pointer was moving when it stopped contacting the screen is available in the `details`. {@endtemplate}

Used by [DragGestureRecognizer.onEnd].

# GestureDragCancelCallback

```dart
typedef GestureDragCancelCallback = void Function()
```

Signature for when the pointer that previously triggered a [GestureDragDownCallback] did not complete.

Used by [DragGestureRecognizer.onCancel].

# GestureVelocityTrackerBuilder

```dart
typedef GestureVelocityTrackerBuilder = VelocityTracker Function(PointerEvent event)
```

Signature for a function that builds a [VelocityTracker].

Used by [DragGestureRecognizer.velocityTrackerBuilder].

# DragGestureRecognizer

```dart
sealed class DragGestureRecognizer extends OneSequenceGestureRecognizer {}
```

Recognizes movement.

In contrast to [MultiDragGestureRecognizer], [DragGestureRecognizer] recognizes a single gesture sequence for all the pointers it watches, which means that the recognizer has at most one drag sequence active at any given time regardless of how many pointers are in contact with the screen.

[DragGestureRecognizer] is not intended to be used directly. Instead, consider using one of its subclasses to recognize specific types for drag gestures.

[DragGestureRecognizer] competes on pointer events only when it has at least one non-null callback. If it has no callbacks, it is a no-op.

See also:

- [HorizontalDragGestureRecognizer], for left and right drags.
- [VerticalDragGestureRecognizer], for up and down drags.
- [PanGestureRecognizer], for drags that are not locked to a single axis.

### DragGestureRecognizer()

```dart
DragGestureRecognizer({Object? debugOwner, DragStartBehavior dragStartBehavior = DragStartBehavior.start, MultitouchDragStrategy multitouchDragStrategy = MultitouchDragStrategy.latestPointer, GestureVelocityTrackerBuilder velocityTrackerBuilder = _defaultBuilder, bool onlyAcceptDragOnThreshold = false, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter = _defaultButtonAcceptBehavior})
```

Initialize the object.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

Configure the behavior of offsets passed to [onStart].

If set to [DragStartBehavior.start], the [onStart] callback will be called with the position of the pointer at the time this gesture recognizer won the arena. If [DragStartBehavior.down], [onStart] will be called with the position of the first detected down event for the pointer. When there are no other gestures competing with this gesture in the arena, there's no difference in behavior between the two settings.

For more information about the gesture arena: https://flutter.dev/to/gesture-disambiguation

By default, the drag start behavior is [DragStartBehavior.start].

## Example:

A [HorizontalDragGestureRecognizer] and a [VerticalDragGestureRecognizer] compete with each other. A finger presses down on the screen with offset (500.0, 500.0), and then moves to position (510.0, 500.0) before the [HorizontalDragGestureRecognizer] wins the arena. With [dragStartBehavior] set to [DragStartBehavior.down], the [onStart] callback will be called with position (500.0, 500.0). If it is instead set to [DragStartBehavior.start], [onStart] will be called with position (510.0, 500.0).

### multitouchDragStrategy

```dart
MultitouchDragStrategy multitouchDragStrategy
```

{@template flutter.gestures.monodrag.DragGestureRecognizer.multitouchDragStrategy} Configure the multi-finger drag strategy on multi-touch devices.

If set to [MultitouchDragStrategy.latestPointer], the drag gesture recognizer will only track the latest active (accepted by this recognizer) pointer, which appears to be only one finger dragging.

If set to [MultitouchDragStrategy.averageBoundaryPointers], all active pointers will be tracked, and the result is computed from the boundary pointers.

If set to [MultitouchDragStrategy.sumAllPointers], all active pointers will be tracked together and the scrolling offset is the sum of the offsets of all active pointers {@endtemplate}

By default, the strategy is [MultitouchDragStrategy.latestPointer].

See also:

- [MultitouchDragStrategy], which defines several different drag strategies for multi-finger drag.

### onDown

```dart
GestureDragDownCallback? onDown
```

A pointer has contacted the screen with a primary button and might begin to move.

The position of the pointer is provided in the callback's `details` argument, which is a [DragDownDetails] object.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [DragDownDetails], which is passed as an argument to this callback.

### onStart

```dart
GestureDragStartCallback? onStart
```

{@template flutter.gestures.monodrag.DragGestureRecognizer.onStart} A pointer has contacted the screen with a primary button and has begun to move. {@endtemplate}

The position of the pointer is provided in the callback's `details` argument, which is a [DragStartDetails] object. The [dragStartBehavior] determines this position.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [DragStartDetails], which is passed as an argument to this callback.

### onUpdate

```dart
GestureDragUpdateCallback? onUpdate
```

{@template flutter.gestures.monodrag.DragGestureRecognizer.onUpdate} A pointer that is in contact with the screen with a primary button and moving has moved again. {@endtemplate}

The distance traveled by the pointer since the last update is provided in the callback's `details` argument, which is a [DragUpdateDetails] object.

If this gesture recognizer recognizes movement on a single axis (a [VerticalDragGestureRecognizer] or [HorizontalDragGestureRecognizer]), then `details` will reflect movement only on that axis and its [DragUpdateDetails.primaryDelta] will be non-null. If this gesture recognizer recognizes movement in all directions (a [PanGestureRecognizer]), then `details` will reflect movement on both axes and its [DragUpdateDetails.primaryDelta] will be null.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [DragUpdateDetails], which is passed as an argument to this callback.

### onEnd

```dart
GestureDragEndCallback? onEnd
```

{@template flutter.gestures.monodrag.DragGestureRecognizer.onEnd} A pointer that was previously in contact with the screen with a primary button and moving is no longer in contact with the screen and was moving at a specific velocity when it stopped contacting the screen. {@endtemplate}

The velocity is provided in the callback's `details` argument, which is a [DragEndDetails] object.

If this gesture recognizer recognizes movement on a single axis (a [VerticalDragGestureRecognizer] or [HorizontalDragGestureRecognizer]), then `details` will reflect movement only on that axis and its [DragEndDetails.primaryVelocity] will be non-null. If this gesture recognizer recognizes movement in all directions (a [PanGestureRecognizer]), then `details` will reflect movement on both axes and its [DragEndDetails.primaryVelocity] will be null.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [DragEndDetails], which is passed as an argument to this callback.

### onCancel

```dart
GestureDragCancelCallback? onCancel
```

The pointer that previously triggered [onDown] did not complete.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.

### minFlingDistance

```dart
double? minFlingDistance
```

The minimum distance an input pointer drag must have moved to be considered a fling gesture.

This value is typically compared with the distance traveled along the scrolling axis. If null then [kTouchSlop] is used.

### minFlingVelocity

```dart
double? minFlingVelocity
```

The minimum velocity for an input pointer drag to be considered fling.

This value is typically compared with the magnitude of fling gesture's velocity along the scrolling axis. If null then [kMinFlingVelocity] is used.

### maxFlingVelocity

```dart
double? maxFlingVelocity
```

Fling velocity magnitudes will be clamped to this value.

If null then [kMaxFlingVelocity] is used.

### onlyAcceptDragOnThreshold

```dart
bool onlyAcceptDragOnThreshold
```

Whether the drag threshold should be met before dispatching any drag callbacks.

The drag threshold is met when the global distance traveled by a pointer has exceeded the defined threshold on the relevant axis, i.e. y-axis for the [VerticalDragGestureRecognizer], x-axis for the [HorizontalDragGestureRecognizer], and the entire plane for [PanGestureRecognizer]. The threshold for both [VerticalDragGestureRecognizer] and [HorizontalDragGestureRecognizer] are calculated by [computeHitSlop], while [computePanSlop] is used for [PanGestureRecognizer].

If true, the drag callbacks will only be dispatched when this recognizer has won the arena and the drag threshold has been met.

If false, the drag callbacks will be dispatched immediately when this recognizer has won the arena.

This value defaults to false.

### velocityTrackerBuilder

```dart
GestureVelocityTrackerBuilder velocityTrackerBuilder
```

Determines the type of velocity estimation method to use for a potential drag gesture, when a new pointer is added.

To estimate the velocity of a gesture, [DragGestureRecognizer] calls [velocityTrackerBuilder] when it starts to track a new pointer in [addAllowedPointer], and add subsequent updates on the pointer to the resulting velocity tracker, until the gesture recognizer stops tracking the pointer. This allows you to specify a different velocity estimation strategy for each allowed pointer added, by changing the type of velocity tracker this [GestureVelocityTrackerBuilder] returns.

If left unspecified the default [velocityTrackerBuilder] creates a new [VelocityTracker] for every pointer added.

See also:

- [VelocityTracker], a velocity tracker that uses least squares estimation on the 20 most recent pointer data samples. It's a well-rounded velocity tracker and is used by default.
- [IOSScrollViewFlingVelocityTracker], a specialized velocity tracker for determining the initial fling velocity for a [Scrollable] on iOS, to match the native behavior on that platform.

### lastPosition

```dart
OffsetPair get lastPosition
```

The local and global offsets of the last pointer event received.

It is used to create the [DragEndDetails], which provides information about the end of a drag gesture.

### debugLastPendingEventTimestamp

```dart
Duration? get debugLastPendingEventTimestamp
```

When asserts are enabled, returns the last tracked pending event timestamp for this recognizer.

Otherwise, returns null.

This getter is intended for use in framework unit tests. Applications must not depend on its value.

### globalDistanceMoved

```dart
double get globalDistanceMoved
```

Distance moved in the global coordinate space of the screen in drag direction.

If drag is only allowed along a defined axis, this value may be negative to differentiate the direction of the drag.

### isFlingGesture()

```dart
bool isFlingGesture(VelocityEstimate estimate, PointerDeviceKind kind)
```

Determines if a gesture is a fling or not based on velocity.

A fling calls its gesture end callback with a velocity, allowing the provider of the callback to respond by carrying the gesture forward with inertia, for example.

### considerFling()

```dart
DragEndDetails? considerFling(VelocityEstimate estimate, PointerDeviceKind kind)
```

Determines if a gesture is a fling or not, and if so its effective velocity.

A fling calls its gesture end callback with a velocity, allowing the provider of the callback to respond by carrying the gesture forward with inertia, for example.

### hasSufficientGlobalDistanceToAccept()

```dart
bool hasSufficientGlobalDistanceToAccept(PointerDeviceKind pointerDeviceKind, double? deviceTouchSlop)
```

Whether the [globalDistanceMoved] is big enough to accept the gesture.

If this method returns `true`, it means this recognizer should declare win in the gesture arena.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerEvent event)
```

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### addAllowedPointerPanZoom()

```dart
void addAllowedPointerPanZoom(PointerPanZoomStartEvent event)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

### rejectGesture()

```dart
void rejectGesture(int pointer)
```

### didStopTrackingLastPointer()

```dart
void didStopTrackingLastPointer(int pointer)
```

### dispose()

```dart
void dispose()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# VerticalDragGestureRecognizer

```dart
class VerticalDragGestureRecognizer extends DragGestureRecognizer {}
```

Recognizes movement in the vertical direction.

Used for vertical scrolling.

See also:

- [HorizontalDragGestureRecognizer], for a similar recognizer but for horizontal movement.
- [MultiDragGestureRecognizer], for a family of gesture recognizers that track each touch point independently.

### VerticalDragGestureRecognizer()

```dart
VerticalDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Create a gesture recognizer for interactions in the vertical axis.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### isFlingGesture()

```dart
bool isFlingGesture(VelocityEstimate estimate, PointerDeviceKind kind)
```

### considerFling()

```dart
DragEndDetails? considerFling(VelocityEstimate estimate, PointerDeviceKind kind)
```

### hasSufficientGlobalDistanceToAccept()

```dart
bool hasSufficientGlobalDistanceToAccept(PointerDeviceKind pointerDeviceKind, double? deviceTouchSlop)
```

### debugDescription

```dart
String get debugDescription
```

# HorizontalDragGestureRecognizer

```dart
class HorizontalDragGestureRecognizer extends DragGestureRecognizer {}
```

Recognizes movement in the horizontal direction.

Used for horizontal scrolling.

See also:

- [VerticalDragGestureRecognizer], for a similar recognizer but for vertical movement.
- [MultiDragGestureRecognizer], for a family of gesture recognizers that track each touch point independently.

### HorizontalDragGestureRecognizer()

```dart
HorizontalDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Create a gesture recognizer for interactions in the horizontal axis.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### isFlingGesture()

```dart
bool isFlingGesture(VelocityEstimate estimate, PointerDeviceKind kind)
```

### considerFling()

```dart
DragEndDetails? considerFling(VelocityEstimate estimate, PointerDeviceKind kind)
```

### hasSufficientGlobalDistanceToAccept()

```dart
bool hasSufficientGlobalDistanceToAccept(PointerDeviceKind pointerDeviceKind, double? deviceTouchSlop)
```

### debugDescription

```dart
String get debugDescription
```

# PanGestureRecognizer

```dart
class PanGestureRecognizer extends DragGestureRecognizer {}
```

Recognizes movement both horizontally and vertically.

See also:

- [ImmediateMultiDragGestureRecognizer], for a similar recognizer that tracks each touch point independently.
- [DelayedMultiDragGestureRecognizer], for a similar recognizer that tracks each touch point independently, but that doesn't start until some time has passed.

### PanGestureRecognizer()

```dart
PanGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Create a gesture recognizer for tracking movement on a plane.

### isFlingGesture()

```dart
bool isFlingGesture(VelocityEstimate estimate, PointerDeviceKind kind)
```

### considerFling()

```dart
DragEndDetails? considerFling(VelocityEstimate estimate, PointerDeviceKind kind)
```

### hasSufficientGlobalDistanceToAccept()

```dart
bool hasSufficientGlobalDistanceToAccept(PointerDeviceKind pointerDeviceKind, double? deviceTouchSlop)
```

### debugDescription

```dart
String get debugDescription
```
