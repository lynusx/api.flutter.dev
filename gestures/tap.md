@docImport 'package:flutter/widgets.dart';

@docImport 'multitap.dart';

# TapDownDetails

```dart
class TapDownDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapDownCallback], such as position.

See also:

- [GestureDetector.onTapDown], which receives this information.
- [TapGestureRecognizer], which passes this information to one of its callbacks.

### TapDownDetails()

```dart
TapDownDetails({Offset globalPosition = Offset.zero, Offset? localPosition, PointerDeviceKind? kind})
```

Creates details for a [GestureTapDownCallback].

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

# GestureTapDownCallback

```dart
typedef GestureTapDownCallback = void Function(TapDownDetails details)
```

{@template flutter.gestures.tap.GestureTapDownCallback} Signature for when a pointer that might cause a tap has contacted the screen.

The position at which the pointer contacted the screen is available in the `details`. {@endtemplate}

See also:

- [GestureDetector.onTapDown], which matches this signature.
- [TapGestureRecognizer], which uses this signature in one of its callbacks.

# TapUpDetails

```dart
class TapUpDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureTapUpCallback], such as position.

See also:

- [GestureDetector.onTapUp], which receives this information.
- [TapGestureRecognizer], which passes this information to one of its callbacks.

### TapUpDetails()

```dart
TapUpDetails({Offset globalPosition = Offset.zero, Offset? localPosition, required PointerDeviceKind kind})
```

Creates a [TapUpDetails] data object.

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

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TapMoveDetails

```dart
class TapMoveDetails {}
```

Details object for callbacks that use [GestureTapMoveCallback].

See also:

- [GestureDetector.onTapMove], which receives this information.
- [TapGestureRecognizer], which passes this information to one of its callbacks.

### TapMoveDetails()

```dart
TapMoveDetails({required PointerDeviceKind kind, Offset globalPosition = Offset.zero, Offset delta = Offset.zero, Offset? localPosition})
```

Creates a [TapMoveDetails] data object.

### globalPosition

```dart
Offset globalPosition
```

The global position at which the pointer contacted the screen.

### localPosition

```dart
Offset localPosition
```

The local position at which the pointer contacted the screen.

### kind

```dart
PointerDeviceKind kind
```

The kind of the device that initiated the event.

### delta

```dart
Offset delta
```

The amount the pointer has moved in the coordinate space of the event receiver since the previous update.

# GestureTapUpCallback

```dart
typedef GestureTapUpCallback = void Function(TapUpDetails details)
```

{@template flutter.gestures.tap.GestureTapUpCallback} Signature for when a pointer that will trigger a tap has stopped contacting the screen.

The position at which the pointer stopped contacting the screen is available in the `details`. {@endtemplate}

See also:

- [GestureDetector.onTapUp], which matches this signature.
- [TapGestureRecognizer], which uses this signature in one of its callbacks.

# GestureTapCallback

```dart
typedef GestureTapCallback = void Function()
```

Signature for when a tap has occurred.

See also:

- [GestureDetector.onTap], which matches this signature.
- [TapGestureRecognizer], which uses this signature in one of its callbacks.

# GestureTapMoveCallback

```dart
typedef GestureTapMoveCallback = void Function(TapMoveDetails details)
```

Signature for when a pointer that triggered a tap has moved.

The position at which the pointer moved is available in the `details`.

See also:

- [GestureDetector.onTapMove], which matches this signature.
- [TapGestureRecognizer], which uses this signature in one of its callbacks.

# GestureTapCancelCallback

```dart
typedef GestureTapCancelCallback = void Function()
```

Signature for when the pointer that previously triggered a [GestureTapDownCallback] will not end up causing a tap.

See also:

- [GestureDetector.onTapCancel], which matches this signature.
- [TapGestureRecognizer], which uses this signature in one of its callbacks.

# BaseTapGestureRecognizer

```dart
abstract class BaseTapGestureRecognizer extends PrimaryPointerGestureRecognizer {}
```

A base class for gesture recognizers that recognize taps.

Gesture recognizers take part in gesture arenas to enable potential gestures to be disambiguated from each other. This process is managed by a [GestureArenaManager].

A tap is defined as a sequence of events that starts with a down, followed by optional moves, then ends with an up. All move events must contain the same `buttons` as the down event, and must not be too far from the initial position. The gesture is rejected on any violation, a cancel event, or if any other recognizers wins the arena. It is accepted only when it is the last member of the arena.

The [BaseTapGestureRecognizer] considers all the pointers involved in the pointer event sequence as contributing to one gesture. For this reason, extra pointer interactions during a tap sequence are not recognized as additional taps. For example, down-1, down-2, up-1, up-2 produces only one tap on up-1.

The [BaseTapGestureRecognizer] can not be directly used, since it does not define which buttons to accept, or what to do when a tap happens. If you want to build a custom tap recognizer, extend this class by overriding [isPointerAllowed] and the handler methods.

See also:

- [TapGestureRecognizer], a ready-to-use tap recognizer that recognizes taps of the primary button and taps of the secondary button.
- [ModalBarrier], a widget that uses a custom tap recognizer that accepts any buttons.

### BaseTapGestureRecognizer()

```dart
BaseTapGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter, double? preAcceptSlopTolerance, double? postAcceptSlopTolerance})
```

Creates a tap gesture recognizer.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### handleTapDown()

```dart
void handleTapDown({required PointerDownEvent down})
```

A pointer has contacted the screen, which might be the start of a tap.

This triggers after the down event, once a short timeout ([deadline]) has elapsed, or once the gesture has won the arena, whichever comes first.

The parameter `down` is the down event of the primary pointer that started the tap sequence.

If this recognizer doesn't win the arena, [handleTapCancel] is called next. Otherwise, [handleTapUp] is called next.

### handleTapUp()

```dart
void handleTapUp({required PointerDownEvent down, required PointerUpEvent up})
```

A pointer has stopped contacting the screen, which is recognized as a tap.

This triggers on the up event if the recognizer wins the arena with it or has previously won.

The parameter `down` is the down event of the primary pointer that started the tap sequence, and `up` is the up event that ended the tap sequence.

If this recognizer doesn't win the arena, [handleTapCancel] is called instead.

### handleTapMove()

```dart
void handleTapMove({required PointerMoveEvent move})
```

A pointer that triggered a tap has moved.

This triggers on the move event if the recognizer has recognized the tap gesture.

The parameter `move` is the move event of the primary pointer that started the tap sequence.

### handleTapCancel()

```dart
void handleTapCancel({required PointerDownEvent down, PointerCancelEvent? cancel, required String reason})
```

A pointer that previously triggered [handleTapDown] will not end up causing a tap.

This triggers once the gesture loses the arena if [handleTapDown] has been previously triggered.

The parameter `down` is the down event of the primary pointer that started the tap sequence; `cancel` is the cancel event, which might be null; `reason` is a short description of the cause if `cancel` is null, which can be "forced" if other gestures won the arena, or "spontaneous" otherwise.

If this recognizer wins the arena, [handleTapUp] is called instead.

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### startTrackingPointer()

```dart
void startTrackingPointer(int pointer, [Matrix4? transform])
```

### handlePrimaryPointer()

```dart
void handlePrimaryPointer(PointerEvent event)
```

### resolve()

```dart
void resolve(GestureDisposition disposition)
```

### didExceedDeadline()

```dart
void didExceedDeadline()
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
```

### rejectGesture()

```dart
void rejectGesture(int pointer)
```

### debugDescription

```dart
String get debugDescription
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TapGestureRecognizer

```dart
class TapGestureRecognizer extends BaseTapGestureRecognizer {}
```

Recognizes taps.

Gesture recognizers take part in gesture arenas to enable potential gestures to be disambiguated from each other. This process is managed by a [GestureArenaManager].

[TapGestureRecognizer] considers all the pointers involved in the pointer event sequence as contributing to one gesture. For this reason, extra pointer interactions during a tap sequence are not recognized as additional taps. For example, down-1, down-2, up-1, up-2 produces only one tap on up-1.

[TapGestureRecognizer] competes on pointer events of [kPrimaryButton] only when it has at least one non-null `onTap*` callback, on events of [kSecondaryButton] only when it has at least one non-null `onSecondaryTap*` callback, and on events of [kTertiaryButton] only when it has at least one non-null `onTertiaryTap*` callback. If it has no callbacks, it is a no-op.

{@template flutter.gestures.tap.TapGestureRecognizer.allowedButtonsFilter} The [allowedButtonsFilter] argument only gives this recognizer the ability to limit the buttons it accepts. It does not provide the ability to recognize any buttons beyond the ones it already accepts: kPrimaryButton, kSecondaryButton or kTertiaryButton. Therefore, a combined value of `kPrimaryButton & kSecondaryButton` would be ignored, but `kPrimaryButton | kSecondaryButton` would be allowed, as long as only one of them is selected at a time. {@endtemplate}

See also:

- [GestureDetector.onTap], which uses this recognizer.
- [MultiTapGestureRecognizer]

### TapGestureRecognizer()

```dart
TapGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter, double? preAcceptSlopTolerance, double? postAcceptSlopTolerance})
```

Creates a tap gesture recognizer.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### onTapDown

```dart
GestureTapDownCallback? onTapDown
```

{@template flutter.gestures.tap.TapGestureRecognizer.onTapDown} A pointer has contacted the screen at a particular location with a primary button, which might be the start of a tap. {@endtemplate}

This triggers after the down event, once a short timeout ([deadline]) has elapsed, or once the gestures has won the arena, whichever comes first.

If this recognizer doesn't win the arena, [onTapCancel] is called next. Otherwise, [onTapUp] is called next.

See also:

- [kPrimaryButton], the button this callback responds to.
- [onSecondaryTapDown], a similar callback but for a secondary button.
- [onTertiaryTapDown], a similar callback but for a tertiary button.
- [TapDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onTapDown], which exposes this callback.

### onTapUp

```dart
GestureTapUpCallback? onTapUp
```

{@template flutter.gestures.tap.TapGestureRecognizer.onTapUp} A pointer has stopped contacting the screen at a particular location, which is recognized as a tap of a primary button. {@endtemplate}

This triggers on the up event, if the recognizer wins the arena with it or has previously won, immediately followed by [onTap].

If this recognizer doesn't win the arena, [onTapCancel] is called instead.

See also:

- [kPrimaryButton], the button this callback responds to.
- [onSecondaryTapUp], a similar callback but for a secondary button.
- [onTertiaryTapUp], a similar callback but for a tertiary button.
- [TapUpDetails], which is passed as an argument to this callback.
- [GestureDetector.onTapUp], which exposes this callback.

### onTap

```dart
GestureTapCallback? onTap
```

A pointer has stopped contacting the screen, which is recognized as a tap of a primary button.

This triggers on the up event, if the recognizer wins the arena with it or has previously won, immediately following [onTapUp].

If this recognizer doesn't win the arena, [onTapCancel] is called instead.

See also:

- [kPrimaryButton], the button this callback responds to.
- [onSecondaryTap], a similar callback but for a secondary button.
- [onTapUp], which has the same timing but with details.
- [GestureDetector.onTap], which exposes this callback.

### onTapMove

```dart
GestureTapMoveCallback? onTapMove
```

A pointer that triggered a tap has moved.

This callback is triggered after the tap gesture has been recognized and the pointer starts to move.

If the pointer moves beyond the `postAcceptSlopTolerance` distance, the tap will be canceled. To make `onTapMove` more useful, consider setting `postAcceptSlopTolerance` to a larger value, or to `null` for no limit on movement.

See also:

- [kPrimaryButton], the button this callback responds to.
- [GestureDetector.onTapMove], which exposes this callback.

### onTapCancel

```dart
GestureTapCancelCallback? onTapCancel
```

{@template flutter.gestures.tap.TapGestureRecognizer.onTapCancel} A pointer that previously triggered [onTapDown] will not end up causing a tap. {@endtemplate}

This triggers once the gesture loses the arena if [onTapDown] has previously been triggered.

If this recognizer wins the arena, [onTapUp] and [onTap] are called instead.

See also:

- [kPrimaryButton], the button this callback responds to.
- [onSecondaryTapCancel], a similar callback but for a secondary button.
- [onTertiaryTapCancel], a similar callback but for a tertiary button.
- [GestureDetector.onTapCancel], which exposes this callback.

### onSecondaryTap

```dart
GestureTapCallback? onSecondaryTap
```

{@template flutter.gestures.tap.TapGestureRecognizer.onSecondaryTap} A pointer has stopped contacting the screen, which is recognized as a tap of a secondary button. {@endtemplate}

This triggers on the up event, if the recognizer wins the arena with it or has previously won, immediately following [onSecondaryTapUp].

If this recognizer doesn't win the arena, [onSecondaryTapCancel] is called instead.

See also:

- [kSecondaryButton], the button this callback responds to.
- [onSecondaryTapUp], which has the same timing but with details.
- [GestureDetector.onSecondaryTap], which exposes this callback.

### onSecondaryTapDown

```dart
GestureTapDownCallback? onSecondaryTapDown
```

{@template flutter.gestures.tap.TapGestureRecognizer.onSecondaryTapDown} A pointer has contacted the screen at a particular location with a secondary button, which might be the start of a secondary tap. {@endtemplate}

This triggers after the down event, once a short timeout ([deadline]) has elapsed, or once the gestures has won the arena, whichever comes first.

If this recognizer doesn't win the arena, [onSecondaryTapCancel] is called next. Otherwise, [onSecondaryTapUp] is called next.

See also:

- [kSecondaryButton], the button this callback responds to.
- [onTapDown], a similar callback but for a primary button.
- [onTertiaryTapDown], a similar callback but for a tertiary button.
- [TapDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onSecondaryTapDown], which exposes this callback.

### onSecondaryTapUp

```dart
GestureTapUpCallback? onSecondaryTapUp
```

{@template flutter.gestures.tap.TapGestureRecognizer.onSecondaryTapUp} A pointer has stopped contacting the screen at a particular location, which is recognized as a tap of a secondary button. {@endtemplate}

This triggers on the up event if the recognizer wins the arena with it or has previously won.

If this recognizer doesn't win the arena, [onSecondaryTapCancel] is called instead.

See also:

- [onSecondaryTap], a handler triggered right after this one that doesn't pass any details about the tap.
- [kSecondaryButton], the button this callback responds to.
- [onTapUp], a similar callback but for a primary button.
- [onTertiaryTapUp], a similar callback but for a tertiary button.
- [TapUpDetails], which is passed as an argument to this callback.
- [GestureDetector.onSecondaryTapUp], which exposes this callback.

### onSecondaryTapCancel

```dart
GestureTapCancelCallback? onSecondaryTapCancel
```

{@template flutter.gestures.tap.TapGestureRecognizer.onSecondaryTapCancel} A pointer that previously triggered [onSecondaryTapDown] will not end up causing a tap. {@endtemplate}

This triggers once the gesture loses the arena if [onSecondaryTapDown] has previously been triggered.

If this recognizer wins the arena, [onSecondaryTapUp] is called instead.

See also:

- [kSecondaryButton], the button this callback responds to.
- [onTapCancel], a similar callback but for a primary button.
- [onTertiaryTapCancel], a similar callback but for a tertiary button.
- [GestureDetector.onSecondaryTapCancel], which exposes this callback.

### onTertiaryTapDown

```dart
GestureTapDownCallback? onTertiaryTapDown
```

A pointer has contacted the screen at a particular location with a tertiary button, which might be the start of a tertiary tap.

This triggers after the down event, once a short timeout ([deadline]) has elapsed, or once the gestures has won the arena, whichever comes first.

If this recognizer doesn't win the arena, [onTertiaryTapCancel] is called next. Otherwise, [onTertiaryTapUp] is called next.

See also:

- [kTertiaryButton], the button this callback responds to.
- [onTapDown], a similar callback but for a primary button.
- [onSecondaryTapDown], a similar callback but for a secondary button.
- [TapDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onTertiaryTapDown], which exposes this callback.

### onTertiaryTapUp

```dart
GestureTapUpCallback? onTertiaryTapUp
```

A pointer has stopped contacting the screen at a particular location, which is recognized as a tap of a tertiary button.

This triggers on the up event if the recognizer wins the arena with it or has previously won.

If this recognizer doesn't win the arena, [onTertiaryTapCancel] is called instead.

See also:

- [kTertiaryButton], the button this callback responds to.
- [onTapUp], a similar callback but for a primary button.
- [onSecondaryTapUp], a similar callback but for a secondary button.
- [TapUpDetails], which is passed as an argument to this callback.
- [GestureDetector.onTertiaryTapUp], which exposes this callback.

### onTertiaryTapCancel

```dart
GestureTapCancelCallback? onTertiaryTapCancel
```

A pointer that previously triggered [onTertiaryTapDown] will not end up causing a tap.

This triggers once the gesture loses the arena if [onTertiaryTapDown] has previously been triggered.

If this recognizer wins the arena, [onTertiaryTapUp] is called instead.

See also:

- [kSecondaryButton], the button this callback responds to.
- [onTapCancel], a similar callback but for a primary button.
- [onSecondaryTapCancel], a similar callback but for a secondary button.
- [GestureDetector.onTertiaryTapCancel], which exposes this callback.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerDownEvent event)
```

### handleTapDown()

```dart
void handleTapDown({required PointerDownEvent down})
```

### handleTapUp()

```dart
void handleTapUp({required PointerDownEvent down, required PointerUpEvent up})
```

### handleTapMove()

```dart
void handleTapMove({required PointerMoveEvent move})
```

### handleTapCancel()

```dart
void handleTapCancel({required PointerDownEvent down, PointerCancelEvent? cancel, required String reason})
```

### debugDescription

```dart
String get debugDescription
```
