@docImport 'package:flutter/widgets.dart';

# GestureLongPressDownCallback

```dart
typedef GestureLongPressDownCallback = void Function(LongPressDownDetails details)
```

Callback signature for [LongPressGestureRecognizer.onLongPressDown].

Called when a pointer that might cause a long-press has contacted the screen. The position at which the pointer contacted the screen is available in the `details`.

See also:

- [GestureDetector.onLongPressDown], which matches this signature.
- [GestureLongPressStartCallback], the signature that gets called when the pointer has been in contact with the screen long enough to be considered a long-press.

# GestureLongPressCancelCallback

```dart
typedef GestureLongPressCancelCallback = void Function()
```

Callback signature for [LongPressGestureRecognizer.onLongPressCancel].

Called when the pointer that previously triggered a [GestureLongPressDownCallback] will not end up causing a long-press.

See also:

- [GestureDetector.onLongPressCancel], which matches this signature.

# GestureLongPressCallback

```dart
typedef GestureLongPressCallback = void Function()
```

Callback signature for [LongPressGestureRecognizer.onLongPress].

Called when a pointer has remained in contact with the screen at the same location for a long period of time.

See also:

- [GestureDetector.onLongPress], which matches this signature.
- [GestureLongPressStartCallback], which is the same signature but with details of where the long press occurred.

# GestureLongPressUpCallback

```dart
typedef GestureLongPressUpCallback = void Function()
```

Callback signature for [LongPressGestureRecognizer.onLongPressUp].

Called when a pointer stops contacting the screen after a long press gesture was detected.

See also:

- [GestureDetector.onLongPressUp], which matches this signature.

# GestureLongPressStartCallback

```dart
typedef GestureLongPressStartCallback = void Function(LongPressStartDetails details)
```

Callback signature for [LongPressGestureRecognizer.onLongPressStart].

Called when a pointer has remained in contact with the screen at the same location for a long period of time. Also reports the long press down position.

See also:

- [GestureDetector.onLongPressStart], which matches this signature.
- [GestureLongPressCallback], which is the same signature without the details.

# GestureLongPressMoveUpdateCallback

```dart
typedef GestureLongPressMoveUpdateCallback = void Function(LongPressMoveUpdateDetails details)
```

Callback signature for [LongPressGestureRecognizer.onLongPressMoveUpdate].

Called when a pointer is moving after being held in contact at the same location for a long period of time. Reports the new position and its offset from the original down position.

See also:

- [GestureDetector.onLongPressMoveUpdate], which matches this signature.

# GestureLongPressEndCallback

```dart
typedef GestureLongPressEndCallback = void Function(LongPressEndDetails details)
```

Callback signature for [LongPressGestureRecognizer.onLongPressEnd].

Called when a pointer stops contacting the screen after a long press gesture was detected. Also reports the position where the pointer stopped contacting the screen.

See also:

- [GestureDetector.onLongPressEnd], which matches this signature.

# LongPressDownDetails

```dart
class LongPressDownDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for callbacks that use [GestureLongPressDownCallback].

See also:

- [LongPressGestureRecognizer.onLongPressDown], whose callback passes these details.
- [LongPressGestureRecognizer.onSecondaryLongPressDown], whose callback passes these details.
- [LongPressGestureRecognizer.onTertiaryLongPressDown], whose callback passes these details.

### LongPressDownDetails()

```dart
LongPressDownDetails({Offset globalPosition = Offset.zero, Offset? localPosition, PointerDeviceKind? kind})
```

Creates the details for a [GestureLongPressDownCallback].

If the `localPosition` argument is not specified, it will default to the global position.

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

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LongPressStartDetails

```dart
class LongPressStartDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for callbacks that use [GestureLongPressStartCallback].

See also:

- [LongPressGestureRecognizer.onLongPressStart], which uses [GestureLongPressStartCallback].
- [LongPressMoveUpdateDetails], the details for [GestureLongPressMoveUpdateCallback]
- [LongPressEndDetails], the details for [GestureLongPressEndCallback].

### LongPressStartDetails()

```dart
LongPressStartDetails({Offset globalPosition = Offset.zero, Offset? localPosition})
```

Creates the details for a [GestureLongPressStartCallback].

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

# LongPressMoveUpdateDetails

```dart
class LongPressMoveUpdateDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for callbacks that use [GestureLongPressMoveUpdateCallback].

See also:

- [LongPressGestureRecognizer.onLongPressMoveUpdate], which uses [GestureLongPressMoveUpdateCallback].
- [LongPressEndDetails], the details for [GestureLongPressEndCallback]
- [LongPressStartDetails], the details for [GestureLongPressStartCallback].

### LongPressMoveUpdateDetails()

```dart
LongPressMoveUpdateDetails({Offset globalPosition = Offset.zero, Offset? localPosition, Offset offsetFromOrigin = Offset.zero, Offset? localOffsetFromOrigin})
```

Creates the details for a [GestureLongPressMoveUpdateCallback].

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

### offsetFromOrigin

```dart
Offset offsetFromOrigin
```

A delta offset from the point where the long press drag initially contacted the screen to the point where the pointer is currently located (the present [globalPosition]) when this callback is triggered.

### localOffsetFromOrigin

```dart
Offset localOffsetFromOrigin
```

A local delta offset from the point where the long press drag initially contacted the screen to the point where the pointer is currently located (the present [localPosition]) when this callback is triggered.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LongPressEndDetails

```dart
class LongPressEndDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for callbacks that use [GestureLongPressEndCallback].

See also:

- [LongPressGestureRecognizer.onLongPressEnd], which uses [GestureLongPressEndCallback].
- [LongPressMoveUpdateDetails], the details for [GestureLongPressMoveUpdateCallback].
- [LongPressStartDetails], the details for [GestureLongPressStartCallback].

### LongPressEndDetails()

```dart
LongPressEndDetails({Offset globalPosition = Offset.zero, Offset? localPosition, Velocity velocity = Velocity.zero})
```

Creates the details for a [GestureLongPressEndCallback].

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

The pointer's velocity when it stopped contacting the screen.

Defaults to zero if not specified in the constructor.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LongPressGestureRecognizer

```dart
class LongPressGestureRecognizer extends PrimaryPointerGestureRecognizer {}
```

Recognizes when the user has pressed down at the same location for a long period of time.

The gesture must not deviate in position from its touch down point for 500ms until it's recognized. Once the gesture is accepted, the finger can be moved, triggering [onLongPressMoveUpdate] callbacks, unless the [postAcceptSlopTolerance] constructor argument is specified.

[LongPressGestureRecognizer] may compete on pointer events of [kPrimaryButton], [kSecondaryButton], and/or [kTertiaryButton] if at least one corresponding callback is non-null. If it has no callbacks, it is a no-op.

### LongPressGestureRecognizer()

```dart
LongPressGestureRecognizer({Duration? duration, double? postAcceptSlopTolerance = null, Set<InvalidType>? supportedDevices, Object? debugOwner, AllowedButtonsFilter? allowedButtonsFilter})
```

Creates a long-press gesture recognizer.

Consider assigning the [onLongPressStart] callback after creating this object.

The [postAcceptSlopTolerance] argument can be used to specify a maximum allowed distance for the gesture to deviate from the starting point once the long press has triggered. If the gesture deviates past that point, subsequent callbacks ([onLongPressMoveUpdate], [onLongPressUp], [onLongPressEnd]) will stop. Defaults to null, which means the gesture can be moved without limit once the long press is accepted.

The [duration] argument can be used to overwrite the default duration after which the long press will be recognized.

{@macro flutter.gestures.tap.TapGestureRecognizer.allowedButtonsFilter}

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### onLongPressDown

```dart
GestureLongPressDownCallback? onLongPressDown
```

Called when a pointer has contacted the screen at a particular location with a primary button, which might be the start of a long-press.

This triggers after the pointer down event.

If this recognizer doesn't win the arena, [onLongPressCancel] is called next. Otherwise, [onLongPressStart] is called next.

See also:

- [kPrimaryButton], the button this callback responds to.
- [onSecondaryLongPressDown], a similar callback but for a secondary button.
- [onTertiaryLongPressDown], a similar callback but for a tertiary button.
- [LongPressDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onLongPressDown], which exposes this callback in a widget.

### onLongPressCancel

```dart
GestureLongPressCancelCallback? onLongPressCancel
```

Called when a pointer that previously triggered [onLongPressDown] will not end up causing a long-press.

This triggers once the gesture loses the arena if [onLongPressDown] has previously been triggered.

If this recognizer wins the arena, [onLongPressStart] and [onLongPress] are called instead.

If the gesture is deactivated due to [postAcceptSlopTolerance] having been exceeded, this callback will not be called, since the gesture will have already won the arena at that point.

See also:

- [kPrimaryButton], the button this callback responds to.

### onLongPress

```dart
GestureLongPressCallback? onLongPress
```

Called when a long press gesture by a primary button has been recognized.

This is equivalent to (and is called immediately after) [onLongPressStart]. The only difference between the two is that this callback does not contain details of the position at which the pointer initially contacted the screen.

See also:

- [kPrimaryButton], the button this callback responds to.

### onLongPressStart

```dart
GestureLongPressStartCallback? onLongPressStart
```

Called when a long press gesture by a primary button has been recognized.

This is equivalent to (and is called immediately before) [onLongPress]. The only difference between the two is that this callback contains details of the position at which the pointer initially contacted the screen, whereas [onLongPress] does not.

See also:

- [kPrimaryButton], the button this callback responds to.
- [LongPressStartDetails], which is passed as an argument to this callback.

### onLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onLongPressMoveUpdate
```

Called when moving after the long press by a primary button is recognized.

See also:

- [kPrimaryButton], the button this callback responds to.
- [LongPressMoveUpdateDetails], which is passed as an argument to this callback.

### onLongPressUp

```dart
GestureLongPressUpCallback? onLongPressUp
```

Called when the pointer stops contacting the screen after a long-press by a primary button.

This is equivalent to (and is called immediately after) [onLongPressEnd]. The only difference between the two is that this callback does not contain details of the state of the pointer when it stopped contacting the screen.

See also:

- [kPrimaryButton], the button this callback responds to.

### onLongPressEnd

```dart
GestureLongPressEndCallback? onLongPressEnd
```

Called when the pointer stops contacting the screen after a long-press by a primary button.

This is equivalent to (and is called immediately before) [onLongPressUp]. The only difference between the two is that this callback contains details of the state of the pointer when it stopped contacting the screen, whereas [onLongPressUp] does not.

See also:

- [kPrimaryButton], the button this callback responds to.
- [LongPressEndDetails], which is passed as an argument to this callback.

### onSecondaryLongPressDown

```dart
GestureLongPressDownCallback? onSecondaryLongPressDown
```

Called when a pointer has contacted the screen at a particular location with a secondary button, which might be the start of a long-press.

This triggers after the pointer down event.

If this recognizer doesn't win the arena, [onSecondaryLongPressCancel] is called next. Otherwise, [onSecondaryLongPressStart] is called next.

See also:

- [kSecondaryButton], the button this callback responds to.
- [onLongPressDown], a similar callback but for a primary button.
- [onTertiaryLongPressDown], a similar callback but for a tertiary button.
- [LongPressDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onSecondaryLongPressDown], which exposes this callback in a widget.

### onSecondaryLongPressCancel

```dart
GestureLongPressCancelCallback? onSecondaryLongPressCancel
```

Called when a pointer that previously triggered [onSecondaryLongPressDown] will not end up causing a long-press.

This triggers once the gesture loses the arena if [onSecondaryLongPressDown] has previously been triggered.

If this recognizer wins the arena, [onSecondaryLongPressStart] and [onSecondaryLongPress] are called instead.

If the gesture is deactivated due to [postAcceptSlopTolerance] having been exceeded, this callback will not be called, since the gesture will have already won the arena at that point.

See also:

- [kSecondaryButton], the button this callback responds to.

### onSecondaryLongPress

```dart
GestureLongPressCallback? onSecondaryLongPress
```

Called when a long press gesture by a secondary button has been recognized.

This is equivalent to (and is called immediately after) [onSecondaryLongPressStart]. The only difference between the two is that this callback does not contain details of the position at which the pointer initially contacted the screen.

See also:

- [kSecondaryButton], the button this callback responds to.

### onSecondaryLongPressStart

```dart
GestureLongPressStartCallback? onSecondaryLongPressStart
```

Called when a long press gesture by a secondary button has been recognized.

This is equivalent to (and is called immediately before) [onSecondaryLongPress]. The only difference between the two is that this callback contains details of the position at which the pointer initially contacted the screen, whereas [onSecondaryLongPress] does not.

See also:

- [kSecondaryButton], the button this callback responds to.
- [LongPressStartDetails], which is passed as an argument to this callback.

### onSecondaryLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onSecondaryLongPressMoveUpdate
```

Called when moving after the long press by a secondary button is recognized.

See also:

- [kSecondaryButton], the button this callback responds to.
- [LongPressMoveUpdateDetails], which is passed as an argument to this callback.

### onSecondaryLongPressUp

```dart
GestureLongPressUpCallback? onSecondaryLongPressUp
```

Called when the pointer stops contacting the screen after a long-press by a secondary button.

This is equivalent to (and is called immediately after) [onSecondaryLongPressEnd]. The only difference between the two is that this callback does not contain details of the state of the pointer when it stopped contacting the screen.

See also:

- [kSecondaryButton], the button this callback responds to.

### onSecondaryLongPressEnd

```dart
GestureLongPressEndCallback? onSecondaryLongPressEnd
```

Called when the pointer stops contacting the screen after a long-press by a secondary button.

This is equivalent to (and is called immediately before) [onSecondaryLongPressUp]. The only difference between the two is that this callback contains details of the state of the pointer when it stopped contacting the screen, whereas [onSecondaryLongPressUp] does not.

See also:

- [kSecondaryButton], the button this callback responds to.
- [LongPressEndDetails], which is passed as an argument to this callback.

### onTertiaryLongPressDown

```dart
GestureLongPressDownCallback? onTertiaryLongPressDown
```

Called when a pointer has contacted the screen at a particular location with a tertiary button, which might be the start of a long-press.

This triggers after the pointer down event.

If this recognizer doesn't win the arena, [onTertiaryLongPressCancel] is called next. Otherwise, [onTertiaryLongPressStart] is called next.

See also:

- [kTertiaryButton], the button this callback responds to.
- [onLongPressDown], a similar callback but for a primary button.
- [onSecondaryLongPressDown], a similar callback but for a secondary button.
- [LongPressDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onTertiaryLongPressDown], which exposes this callback in a widget.

### onTertiaryLongPressCancel

```dart
GestureLongPressCancelCallback? onTertiaryLongPressCancel
```

Called when a pointer that previously triggered [onTertiaryLongPressDown] will not end up causing a long-press.

This triggers once the gesture loses the arena if [onTertiaryLongPressDown] has previously been triggered.

If this recognizer wins the arena, [onTertiaryLongPressStart] and [onTertiaryLongPress] are called instead.

If the gesture is deactivated due to [postAcceptSlopTolerance] having been exceeded, this callback will not be called, since the gesture will have already won the arena at that point.

See also:

- [kTertiaryButton], the button this callback responds to.

### onTertiaryLongPress

```dart
GestureLongPressCallback? onTertiaryLongPress
```

Called when a long press gesture by a tertiary button has been recognized.

This is equivalent to (and is called immediately after) [onTertiaryLongPressStart]. The only difference between the two is that this callback does not contain details of the position at which the pointer initially contacted the screen.

See also:

- [kTertiaryButton], the button this callback responds to.

### onTertiaryLongPressStart

```dart
GestureLongPressStartCallback? onTertiaryLongPressStart
```

Called when a long press gesture by a tertiary button has been recognized.

This is equivalent to (and is called immediately before) [onTertiaryLongPress]. The only difference between the two is that this callback contains details of the position at which the pointer initially contacted the screen, whereas [onTertiaryLongPress] does not.

See also:

- [kTertiaryButton], the button this callback responds to.
- [LongPressStartDetails], which is passed as an argument to this callback.

### onTertiaryLongPressMoveUpdate

```dart
GestureLongPressMoveUpdateCallback? onTertiaryLongPressMoveUpdate
```

Called when moving after the long press by a tertiary button is recognized.

See also:

- [kTertiaryButton], the button this callback responds to.
- [LongPressMoveUpdateDetails], which is passed as an argument to this callback.

### onTertiaryLongPressUp

```dart
GestureLongPressUpCallback? onTertiaryLongPressUp
```

Called when the pointer stops contacting the screen after a long-press by a tertiary button.

This is equivalent to (and is called immediately after) [onTertiaryLongPressEnd]. The only difference between the two is that this callback does not contain details of the state of the pointer when it stopped contacting the screen.

See also:

- [kTertiaryButton], the button this callback responds to.

### onTertiaryLongPressEnd

```dart
GestureLongPressEndCallback? onTertiaryLongPressEnd
```

Called when the pointer stops contacting the screen after a long-press by a tertiary button.

This is equivalent to (and is called immediately before) [onTertiaryLongPressUp]. The only difference between the two is that this callback contains details of the state of the pointer when it stopped contacting the screen, whereas [onTertiaryLongPressUp] does not.

See also:

- [kTertiaryButton], the button this callback responds to.
- [LongPressEndDetails], which is passed as an argument to this callback.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerDownEvent event)
```

### didExceedDeadline()

```dart
void didExceedDeadline()
```

### handlePrimaryPointer()

```dart
void handlePrimaryPointer(PointerEvent event)
```

### resolve()

```dart
void resolve(GestureDisposition disposition)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

### debugDescription

```dart
String get debugDescription
```
