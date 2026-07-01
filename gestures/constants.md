@docImport 'recognizer.dart'; @docImport 'tap.dart';

# kPressTimeout

```dart
Duration kPressTimeout
```

The time that must elapse before a tap gesture sends onTapDown, if there's any doubt that the gesture is a tap.

# kHoverTapTimeout

```dart
Duration kHoverTapTimeout
```

Maximum length of time between a tap down and a tap up for the gesture to be considered a tap. (Currently not honored by the TapGestureRecognizer.)

# kHoverTapSlop

```dart
double kHoverTapSlop
```

Maximum distance between the down and up pointers for a tap. (Currently not honored by the [TapGestureRecognizer]; [PrimaryPointerGestureRecognizer], which TapGestureRecognizer inherits from, uses [kTouchSlop].)

# kLongPressTimeout

```dart
Duration kLongPressTimeout
```

The time before a long press gesture attempts to win.

# kDoubleTapTimeout

```dart
Duration kDoubleTapTimeout
```

The maximum time from the start of the first tap to the start of the second tap in a double-tap gesture.

# kDoubleTapMinTime

```dart
Duration kDoubleTapMinTime
```

The minimum time from the end of the first tap to the start of the second tap in a double-tap gesture.

# kDoubleTapTouchSlop

```dart
double kDoubleTapTouchSlop
```

The maximum distance that the first touch in a double-tap gesture can travel before deciding that it is not part of a double-tap gesture. DoubleTapGestureRecognizer also restricts the second touch to this distance.

# kDoubleTapSlop

```dart
double kDoubleTapSlop
```

Distance between the initial position of the first touch and the start position of a potential second touch for the second touch to be considered the second touch of a double-tap gesture.

# kZoomControlsTimeout

```dart
Duration kZoomControlsTimeout
```

The time for which zoom controls (e.g. in a map interface) are to be displayed on the screen, from the moment they were last requested.

# kTouchSlop

```dart
double kTouchSlop
```

The distance a touch has to travel for the framework to be confident that the gesture is a scroll gesture, or, inversely, the maximum distance that a touch can travel before the framework becomes confident that it is not a tap.

A total delta less than or equal to [kTouchSlop] is not considered to be a drag, whereas if the delta is greater than [kTouchSlop] it is considered to be a drag.

# kPagingTouchSlop

```dart
double kPagingTouchSlop
```

The distance a touch has to travel for the framework to be confident that the gesture is a paging gesture. (Currently not used, because paging uses a regular drag gesture, which uses kTouchSlop.)

# kPanSlop

```dart
double kPanSlop
```

The distance a touch has to travel for the framework to be confident that the gesture is a panning gesture.

# kScaleSlop

```dart
double kScaleSlop
```

The distance a touch has to travel for the framework to be confident that the gesture is a scale gesture.

# kWindowTouchSlop

```dart
double kWindowTouchSlop
```

The margin around a dialog, popup menu, or other window-like widget inside which we do not consider a tap to dismiss the widget. (Not currently used.)

# kMinFlingVelocity

```dart
double kMinFlingVelocity
```

The minimum velocity for a touch to consider that touch to trigger a fling gesture.

# kMaxFlingVelocity

```dart
double kMaxFlingVelocity
```

Drag gesture fling velocities are clipped to this value.

# kJumpTapTimeout

```dart
Duration kJumpTapTimeout
```

The maximum time from the start of the first tap to the start of the second tap in a jump-tap gesture.

# kPrecisePointerHitSlop

```dart
double kPrecisePointerHitSlop
```

Like [kTouchSlop], but for more precise pointers like mice and trackpads.

# kPrecisePointerPanSlop

```dart
double kPrecisePointerPanSlop
```

Like [kPanSlop], but for more precise pointers like mice and trackpads.

# kPrecisePointerScaleSlop

```dart
double kPrecisePointerScaleSlop
```

Like [kScaleSlop], but for more precise pointers like mice and trackpads.
