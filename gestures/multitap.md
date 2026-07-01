@docImport 'package:flutter/widgets.dart';

# GestureDoubleTapCallback

```dart
typedef GestureDoubleTapCallback = void Function()
```

Signature for callback when the user has tapped the screen at the same location twice in quick succession.

See also:

- [GestureDetector.onDoubleTap], which matches this signature.

# GestureMultiTapDownCallback

```dart
typedef GestureMultiTapDownCallback = void Function(int pointer, TapDownDetails details)
```

Signature used by [MultiTapGestureRecognizer] for when a pointer that might cause a tap has contacted the screen at a particular location.

# GestureMultiTapUpCallback

```dart
typedef GestureMultiTapUpCallback = void Function(int pointer, TapUpDetails details)
```

Signature used by [MultiTapGestureRecognizer] for when a pointer that will trigger a tap has stopped contacting the screen at a particular location.

# GestureMultiTapCallback

```dart
typedef GestureMultiTapCallback = void Function(int pointer)
```

Signature used by [MultiTapGestureRecognizer] for when a tap has occurred.

# GestureMultiTapCancelCallback

```dart
typedef GestureMultiTapCancelCallback = void Function(int pointer)
```

Signature for when the pointer that previously triggered a [GestureMultiTapDownCallback] will not end up causing a tap.

# DoubleTapGestureRecognizer

```dart
class DoubleTapGestureRecognizer extends GestureRecognizer {}
```

Recognizes when the user has tapped the screen at the same location twice in quick succession.

[DoubleTapGestureRecognizer] competes on pointer events when it has a non-null callback. If it has no callbacks, it is a no-op.

### DoubleTapGestureRecognizer()

```dart
DoubleTapGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter = _defaultButtonAcceptBehavior})
```

Create a gesture recognizer for double taps.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### onDoubleTapDown

```dart
GestureTapDownCallback? onDoubleTapDown
```

A pointer has contacted the screen with a primary button at the same location twice in quick succession, which might be the start of a double tap.

This triggers immediately after the down event of the second tap.

If this recognizer doesn't win the arena, [onDoubleTapCancel] is called next. Otherwise, [onDoubleTap] is called next.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [TapDownDetails], which is passed as an argument to this callback.
- [GestureDetector.onDoubleTapDown], which exposes this callback.

### onDoubleTap

```dart
GestureDoubleTapCallback? onDoubleTap
```

Called when the user has tapped the screen with a primary button at the same location twice in quick succession.

This triggers when the pointer stops contacting the device after the second tap.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [GestureDetector.onDoubleTap], which exposes this callback.

### onDoubleTapCancel

```dart
GestureTapCancelCallback? onDoubleTapCancel
```

A pointer that previously triggered [onDoubleTapDown] will not end up causing a double tap.

This triggers once the gesture loses the arena if [onDoubleTapDown] has previously been triggered.

If this recognizer wins the arena, [onDoubleTap] is called instead.

See also:

- [allowedButtonsFilter], which decides which button will be allowed.
- [GestureDetector.onDoubleTapCancel], which exposes this callback.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerDownEvent event)
```

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
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

# MultiTapGestureRecognizer

```dart
class MultiTapGestureRecognizer extends GestureRecognizer {}
```

Recognizes taps on a per-pointer basis.

[MultiTapGestureRecognizer] considers each sequence of pointer events that could constitute a tap independently of other pointers: For example, down-1, down-2, up-1, up-2 produces two taps, on up-1 and up-2.

See also:

- [TapGestureRecognizer]

### MultiTapGestureRecognizer()

```dart
MultiTapGestureRecognizer({Duration longTapDelay = Duration.zero, Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Creates a multi-tap gesture recognizer.

The [longTapDelay] defaults to [Duration.zero], which means [onLongTapDown] is called immediately after [onTapDown].

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### onTapDown

```dart
GestureMultiTapDownCallback? onTapDown
```

A pointer that might cause a tap has contacted the screen at a particular location.

### onTapUp

```dart
GestureMultiTapUpCallback? onTapUp
```

A pointer that will trigger a tap has stopped contacting the screen at a particular location.

### onTap

```dart
GestureMultiTapCallback? onTap
```

A tap has occurred.

### onTapCancel

```dart
GestureMultiTapCancelCallback? onTapCancel
```

The pointer that previously triggered [onTapDown] will not end up causing a tap.

### longTapDelay

```dart
Duration longTapDelay
```

The amount of time between [onTapDown] and [onLongTapDown].

### onLongTapDown

```dart
GestureMultiTapDownCallback? onLongTapDown
```

A pointer that might cause a tap is still in contact with the screen at a particular location after [longTapDelay].

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
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

# GestureSerialTapDownCallback

```dart
typedef GestureSerialTapDownCallback = void Function(SerialTapDownDetails details)
```

Signature used by [SerialTapGestureRecognizer.onSerialTapDown] for when a pointer that might cause a serial tap has contacted the screen at a particular location.

# SerialTapDownDetails

```dart
class SerialTapDownDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureSerialTapDownCallback], such as the tap count within the series.

See also:

- [SerialTapGestureRecognizer], which passes this information to its [SerialTapGestureRecognizer.onSerialTapDown] callback.

### SerialTapDownDetails()

```dart
SerialTapDownDetails({Offset globalPosition = Offset.zero, Offset? localPosition, required PointerDeviceKind kind, int buttons = 0, int count = 1})
```

Creates details for a [GestureSerialTapDownCallback].

The `count` argument must be greater than zero.

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

### buttons

```dart
int buttons
```

Which buttons were pressed when the pointer contacted the screen.

See also:

- [PointerEvent.buttons], which this field reflects.

### count

```dart
int count
```

The number of consecutive taps that this "tap down" represents.

This value will always be greater than zero. When the first pointer in a possible series contacts the screen, this value will be `1`, the second tap in a double-tap will be `2`, and so on.

If a tap is determined to not be in the same series as the tap that preceded it (e.g. because too much time elapsed between the two taps or the two taps had too much distance between them), then this count will reset back to `1`, and a new series will have begun.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureSerialTapCancelCallback

```dart
typedef GestureSerialTapCancelCallback = void Function(SerialTapCancelDetails details)
```

Signature used by [SerialTapGestureRecognizer.onSerialTapCancel] for when a pointer that previously triggered a [GestureSerialTapDownCallback] will not end up completing the serial tap.

# SerialTapCancelDetails

```dart
class SerialTapCancelDetails with Diagnosticable {}
```

Details for [GestureSerialTapCancelCallback], such as the tap count within the series.

See also:

- [SerialTapGestureRecognizer], which passes this information to its [SerialTapGestureRecognizer.onSerialTapCancel] callback.

### SerialTapCancelDetails()

```dart
SerialTapCancelDetails({int count = 1})
```

Creates details for a [GestureSerialTapCancelCallback].

The `count` argument must be greater than zero.

### count

```dart
int count
```

The number of consecutive taps that were in progress when the gesture was interrupted.

This number will match the corresponding count that was specified in [SerialTapDownDetails.count] for the tap that is being canceled. See that field for more information on how this count is reported.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# GestureSerialTapUpCallback

```dart
typedef GestureSerialTapUpCallback = void Function(SerialTapUpDetails details)
```

Signature used by [SerialTapGestureRecognizer.onSerialTapUp] for when a pointer that will trigger a serial tap has stopped contacting the screen.

# SerialTapUpDetails

```dart
class SerialTapUpDetails with Diagnosticable implements PositionedGestureDetails {}
```

Details for [GestureSerialTapUpCallback], such as the tap count within the series.

See also:

- [SerialTapGestureRecognizer], which passes this information to its [SerialTapGestureRecognizer.onSerialTapUp] callback.

### SerialTapUpDetails()

```dart
SerialTapUpDetails({Offset globalPosition = Offset.zero, Offset? localPosition, PointerDeviceKind? kind, int count = 1})
```

Creates details for a [GestureSerialTapUpCallback].

The `count` argument must be greater than zero.

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

### count

```dart
int count
```

The number of consecutive taps that this tap represents.

This value will always be greater than zero. When the first pointer in a possible series completes its tap, this value will be `1`, the second tap in a double-tap will be `2`, and so on.

If a tap is determined to not be in the same series as the tap that preceded it (e.g. because too much time elapsed between the two taps or the two taps had too much distance between them), then this count will reset back to `1`, and a new series will have begun.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SerialTapGestureRecognizer

```dart
class SerialTapGestureRecognizer extends GestureRecognizer {}
```

Recognizes serial taps (taps in a series).

A collection of taps are considered to be _in a series_ if they occur in rapid succession in the same location (within a tolerance). The number of taps in the series is its count. A double-tap, for instance, is a special case of a tap series with a count of two.

### Gesture arena behavior

[SerialTapGestureRecognizer] competes on all pointer events (regardless of button). It will declare defeat if it determines that a gesture is not a tap (e.g. if the pointer is dragged too far while it's contacting the screen). It will immediately declare victory for every tap that it recognizes.

Each time a pointer contacts the screen, this recognizer will enter that gesture into the arena. This means that this recognizer will yield multiple winning entries in the arena for a single tap series as the series progresses.

If this recognizer loses the arena (either by declaring defeat or by another recognizer declaring victory) while the pointer is contacting the screen, it will fire [onSerialTapCancel], and [onSerialTapUp] will not be fired.

### Button behavior

A tap series is defined to have the same buttons across all taps. If a tap with a different combination of buttons is delivered in the middle of a series, it will "steal" the series and begin a new series, starting the count over.

### Interleaving tap behavior

A tap must be _completed_ in order for a subsequent tap to be considered "in the same series" as that tap. Thus, if tap A is in-progress (the down event has been received, but the corresponding up event has not yet been received), and tap B begins (another pointer contacts the screen), tap A will fire [onSerialTapCancel], and tap B will begin a new series (tap B's [SerialTapDownDetails.count] will be 1).

### Relation to `TapGestureRecognizer` and `DoubleTapGestureRecognizer`

[SerialTapGestureRecognizer] fires [onSerialTapDown] and [onSerialTapUp] for every tap that it recognizes (passing the count in the details), regardless of whether that tap is a single-tap, double-tap, etc. This makes it especially useful when you want to respond to every tap in a series. Contrast this with [DoubleTapGestureRecognizer], which only fires if the user completes a double-tap, and [TapGestureRecognizer], which _doesn't_ fire if the recognizer is competing with a `DoubleTapGestureRecognizer`, and the user double-taps.

For example, consider a list item that should be _selected_ on the first tap and _cause an edit dialog to open_ on a double-tap. If you use both [TapGestureRecognizer] and [DoubleTapGestureRecognizer], there are a few problems:

1.  If the user single-taps the list item, it will not select the list item until after enough time has passed to rule out a double-tap.
2.  If the user double-taps the list item, it will not select the list item at all.

The solution is to use [SerialTapGestureRecognizer] and use the tap count to either select the list item or open the edit dialog.

### When competing with `TapGestureRecognizer` and `DoubleTapGestureRecognizer`

Unlike [TapGestureRecognizer] and [DoubleTapGestureRecognizer], [SerialTapGestureRecognizer] aggressively declares victory when it detects a tap, so when it is competing with those gesture recognizers, it will beat them in the arena, regardless of which recognizer entered the arena first.

### SerialTapGestureRecognizer()

```dart
SerialTapGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Creates a serial tap gesture recognizer.

### onSerialTapDown

```dart
GestureSerialTapDownCallback? onSerialTapDown
```

A pointer has contacted the screen at a particular location, which might be the start of a serial tap.

If this recognizer loses the arena before the serial tap is completed (either because the gesture does not end up being a tap or because another recognizer wins the arena), [onSerialTapCancel] is called next. Otherwise, [onSerialTapUp] is called next.

The [SerialTapDownDetails.count] that is passed to this callback specifies the series tap count.

### onSerialTapCancel

```dart
GestureSerialTapCancelCallback? onSerialTapCancel
```

A pointer that previously triggered [onSerialTapDown] will not end up triggering the corresponding [onSerialTapUp].

If the user completes the serial tap, [onSerialTapUp] is called instead.

The [SerialTapCancelDetails.count] that is passed to this callback will match the [SerialTapDownDetails.count] that was passed to the [onSerialTapDown] callback.

### onSerialTapUp

```dart
GestureSerialTapUpCallback? onSerialTapUp
```

A pointer has stopped contacting the screen at a particular location, representing a serial tap.

If the user didn't complete the tap, or if another recognizer won the arena, then [onSerialTapCancel] is called instead.

The [SerialTapUpDetails.count] that is passed to this callback specifies the series tap count and will match the [SerialTapDownDetails.count] that was passed to the [onSerialTapDown] callback.

### isTrackingPointer

```dart
bool get isTrackingPointer
```

Indicates whether this recognizer is currently tracking a pointer that's in contact with the screen.

If this is true, it implies that [onSerialTapDown] has fired, but neither [onSerialTapCancel] nor [onSerialTapUp] have yet fired.

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerDownEvent event)
```

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### acceptGesture()

```dart
void acceptGesture(int pointer)
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
