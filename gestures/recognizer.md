@docImport 'package:flutter/widgets.dart';

@docImport 'drag_details.dart'; @docImport 'monodrag.dart'; @docImport 'multitap.dart'; @docImport 'tap.dart';

# RecognizerCallback

```dart
typedef RecognizerCallback<T> = T Function()
```

Generic signature for callbacks passed to [GestureRecognizer.invokeCallback]. This allows the [GestureRecognizer.invokeCallback] mechanism to be generically used with anonymous functions that return objects of particular types.

# DragStartBehavior

```dart
enum DragStartBehavior {}
```

Configuration of offset passed to [DragStartDetails].

See also:

- [DragGestureRecognizer.dragStartBehavior], which gives an example for the different behaviors.

Set the initial offset at the position where the first down event was detected.

Set the initial position at the position where this gesture recognizer won the arena.

# MultitouchDragStrategy

```dart
enum MultitouchDragStrategy {}
```

Configuration of multi-finger drag strategy on multi-touch devices.

When dragging with only one finger, there's no difference in behavior between all the settings.

Used by [DragGestureRecognizer.multitouchDragStrategy].

Only the latest active pointer is tracked by the recognizer.

If the tracked pointer is released, the first accepted of the remaining active pointers will continue to be tracked.

This is the behavior typically seen on Android.

All active pointers will be tracked, and the result is computed from the boundary pointers.

The scrolling offset is determined by the maximum deltas of both directions.

If the user is dragging with 3 pointers at the same time, each having \[+10, +20, +33\] pixels of offset, the recognizer will report a delta of 33 pixels.

If the user is dragging with 5 pointers at the same time, each having \[+10, +20, +33, -1, -12\] pixels of offset, the recognizer will report a delta of (+33) + (-12) = 21 pixels.

The panning [PanGestureRecognizer] offset is the average of all pointers.

If the user is dragging with 3 pointers at the same time, each having \[+10, +50, -30\] pixels of offset in one direction (horizontal or vertical), the recognizer will report a delta of (10 + 50 -30) / 3 = 10 pixels in this direction.

This is the behavior typically seen on iOS.

All active pointers will be tracked together. The scrolling offset is the sum of the offsets of all active pointers.

When a [Scrollable] drives scrolling by this drag strategy, the scrolling speed will double or triple, depending on how many fingers are dragging at the same time.

If the user is dragging with 3 pointers at the same time, each having \[+10, +20, +33\] pixels of offset, the recognizer will report a delta of 10 + 20 + 33 = 63 pixels.

If the user is dragging with 5 pointers at the same time, each having \[+10, +20, +33, -1, -12\] pixels of offset, the recognizer will report a delta of 10 + 20 + 33 - 1 - 12 = 50 pixels.

# AllowedButtonsFilter

```dart
typedef AllowedButtonsFilter = bool Function(int buttons)
```

Signature for [GestureRecognizer.allowedButtonsFilter].

Used to filter the input buttons of incoming pointer events. The parameter `buttons` comes from [PointerEvent.buttons].

# GestureRecognizer

```dart
abstract class GestureRecognizer extends GestureArenaMember with DiagnosticableTreeMixin {}
```

The base class that all gesture recognizers inherit from.

Provides a basic API that can be used by classes that work with gesture recognizers but don't care about the specific details of the gestures recognizers themselves.

See also:

- [GestureDetector], the widget that is used to detect built-in gestures.
- [RawGestureDetector], the widget that is used to detect custom gestures.
- [debugPrintRecognizerCallbacksTrace], a flag that can be set to help debug issues with gesture recognizers.

### GestureRecognizer()

```dart
GestureRecognizer({Object? debugOwner, Set<PointerDeviceKind>? supportedDevices, AllowedButtonsFilter allowedButtonsFilter = _defaultButtonAcceptBehavior})
```

Initializes the gesture recognizer.

The argument is optional and is only used for debug purposes (e.g. in the [toString] serialization).

{@template flutter.gestures.GestureRecognizer.supportedDevices} It's possible to limit this recognizer to a specific set of [PointerDeviceKind]s by providing the optional [supportedDevices] argument. If [supportedDevices] is null, the recognizer will accept pointer events from all device kinds. {@endtemplate}

### debugOwner

```dart
Object? debugOwner
```

The recognizer's owner.

This is used in the [toString] serialization to report the object for which this gesture recognizer was created, to aid in debugging.

### gestureSettings

```dart
DeviceGestureSettings? gestureSettings
```

Optional device specific configuration for device gestures that will take precedence over framework defaults.

### supportedDevices

```dart
Set<PointerDeviceKind>? supportedDevices
```

The kind of devices that are allowed to be recognized as provided by `supportedDevices` in the constructor, or the currently deprecated `kind`. These cannot both be set. If both are null, events from all device kinds will be tracked and recognized.

### allowedButtonsFilter

```dart
AllowedButtonsFilter allowedButtonsFilter
```

{@template flutter.gestures.multidrag._allowedButtonsFilter} Called when interaction starts. This limits the dragging behavior for custom clicks (such as scroll click). Its parameter comes from [PointerEvent.buttons].

Due to how [kPrimaryButton], [kSecondaryButton], etc., use integers, bitwise operations can help filter how buttons are pressed. For example, if someone simultaneously presses the primary and secondary buttons, the default behavior will return false. The following code accepts any button press with primary: `(int buttons) => buttons & kPrimaryButton != 0`.

When value is `(int buttons) => false`, allow no interactions. When value is `(int buttons) => true`, allow all interactions.

Defaults to all buttons. {@endtemplate}

### addPointerPanZoom()

```dart
void addPointerPanZoom(PointerPanZoomStartEvent event)
```

Registers a new pointer pan/zoom that might be relevant to this gesture detector.

A pointer pan/zoom is a stream of events that conveys data covering pan, zoom, and rotate data from a multi-finger trackpad gesture.

The owner of this gesture recognizer calls addPointerPanZoom() with the PointerPanZoomStartEvent of each pointer that should be considered for this gesture.

It's the GestureRecognizer's responsibility to then add itself to the global pointer router (see [PointerRouter]) to receive subsequent events for this pointer, and to add the pointer to the global gesture arena manager (see [GestureArenaManager]) to track that pointer.

This method is called for each and all pointers being added. In most cases, you want to override [addAllowedPointerPanZoom] instead.

### addAllowedPointerPanZoom()

```dart
void addAllowedPointerPanZoom(PointerPanZoomStartEvent event)
```

Registers a new pointer pan/zoom that's been checked to be allowed by this gesture recognizer.

Subclasses of [GestureRecognizer] are supposed to override this method instead of [addPointerPanZoom] because [addPointerPanZoom] will be called for each pointer being added while [addAllowedPointerPanZoom] is only called for pointers that are allowed by this recognizer.

### addPointer()

```dart
void addPointer(PointerDownEvent event)
```

Registers a new pointer that might be relevant to this gesture detector.

The owner of this gesture recognizer calls addPointer() with the PointerDownEvent of each pointer that should be considered for this gesture.

It's the GestureRecognizer's responsibility to then add itself to the global pointer router (see [PointerRouter]) to receive subsequent events for this pointer, and to add the pointer to the global gesture arena manager (see [GestureArenaManager]) to track that pointer.

This method is called for each and all pointers being added. In most cases, you want to override [addAllowedPointer] instead.

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

Registers a new pointer that's been checked to be allowed by this gesture recognizer.

Subclasses of [GestureRecognizer] are supposed to override this method instead of [addPointer] because [addPointer] will be called for each pointer being added while [addAllowedPointer] is only called for pointers that are allowed by this recognizer.

### handleNonAllowedPointer()

```dart
void handleNonAllowedPointer(PointerDownEvent event)
```

Handles a pointer being added that's not allowed by this recognizer.

Subclasses can override this method and reject the gesture.

See:

- [OneSequenceGestureRecognizer.handleNonAllowedPointer].

### isPointerAllowed()

```dart
bool isPointerAllowed(PointerDownEvent event)
```

Checks whether or not a pointer is allowed to be tracked by this recognizer.

### handleNonAllowedPointerPanZoom()

```dart
void handleNonAllowedPointerPanZoom(PointerPanZoomStartEvent event)
```

Handles a pointer pan/zoom being added that's not allowed by this recognizer.

Subclasses can override this method and reject the gesture.

### isPointerPanZoomAllowed()

```dart
bool isPointerPanZoomAllowed(PointerPanZoomStartEvent event)
```

Checks whether or not a pointer pan/zoom is allowed to be tracked by this recognizer.

### getKindForPointer()

```dart
PointerDeviceKind getKindForPointer(int pointer)
```

For a given pointer ID, returns the device kind associated with it.

The pointer ID is expected to be a valid one i.e. an event was received with that pointer ID.

### getButtonsForPointer()

```dart
int getButtonsForPointer(int pointer)
```

For a given pointer ID, returns the buttons associated with it.

The pointer ID is expected to be valid, meaning an event related to it has been received.

### dispose()

```dart
void dispose()
```

Releases any resources used by the object.

This method is called by the owner of this gesture recognizer when the object is no longer needed (e.g. when a gesture recognizer is being unregistered from a [GestureDetector], the GestureDetector widget calls this method).

### debugDescription

```dart
String get debugDescription
```

Returns a very short pretty description of the gesture that the recognizer looks for, like 'tap' or 'horizontal drag'.

### invokeCallback()

```dart
T? invokeCallback<T>(String name, RecognizerCallback<T> callback, {String Function()? debugReport})
```

Invoke a callback provided by the application, catching and logging any exceptions.

The `name` argument is ignored except when reporting exceptions.

The `debugReport` argument is optional and is used when [debugPrintRecognizerCallbacksTrace] is true. If specified, it must be a callback that returns a string describing useful debugging information, e.g. the arguments passed to the callback.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OneSequenceGestureRecognizer

```dart
abstract class OneSequenceGestureRecognizer extends GestureRecognizer {}
```

Base class for gesture recognizers that can only recognize one gesture at a time. For example, a single [TapGestureRecognizer] can never recognize two taps happening simultaneously, even if multiple pointers are placed on the same widget.

This is in contrast to, for instance, [MultiTapGestureRecognizer], which manages each pointer independently and can consider multiple simultaneous touches to each result in a separate tap.

### OneSequenceGestureRecognizer()

```dart
OneSequenceGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Initialize the object.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### handleNonAllowedPointer()

```dart
void handleNonAllowedPointer(PointerDownEvent event)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```

Called when a pointer event is routed to this recognizer.

This will be called for every pointer event while the pointer is being tracked. Typically, this recognizer will start tracking the pointer in [addAllowedPointer], which means that [handleEvent] will be called starting with the [PointerDownEvent] that was passed to [addAllowedPointer].

See also:

- [startTrackingPointer], which causes pointer events to be routed to this recognizer.
- [stopTrackingPointer], which stops events from being routed to this recognizer.
- [stopTrackingIfPointerNoLongerDown], which conditionally stops events from being routed to this recognizer.

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

Called when the number of pointers this recognizer is tracking changes from one to zero.

The given pointer ID is the ID of the last pointer this recognizer was tracking.

### resolve()

```dart
void resolve(GestureDisposition disposition)
```

Resolves this recognizer's participation in each gesture arena with the given disposition.

### resolvePointer()

```dart
void resolvePointer(int pointer, GestureDisposition disposition)
```

Resolves this recognizer's participation in the given gesture arena with the given disposition.

### dispose()

```dart
void dispose()
```

### team

```dart
GestureArenaTeam? get team
```

The team that this recognizer belongs to, if any.

If [team] is null, this recognizer competes directly in the [GestureArenaManager] to recognize a sequence of pointer events as a gesture. If [team] is non-null, this recognizer competes in the arena in a group with other recognizers on the same team.

A recognizer can be assigned to a team only when it is not participating in the arena. For example, a common time to assign a recognizer to a team is shortly after creating the recognizer.

### team

```dart
set team(GestureArenaTeam? value)
```

The [team] can only be set once.

### startTrackingPointer()

```dart
void startTrackingPointer(int pointer, [Matrix4? transform])
```

Causes events related to the given pointer ID to be routed to this recognizer.

The pointer events are transformed according to `transform` and then delivered to [handleEvent]. The value for the `transform` argument is usually obtained from [PointerDownEvent.transform] to transform the events from the global coordinate space into the coordinate space of the event receiver. It may be null if no transformation is necessary.

Use [stopTrackingPointer] to remove the route added by this function.

This method also adds this recognizer (or its [team] if it's non-null) to the gesture arena for the specified pointer.

This is called by [OneSequenceGestureRecognizer.addAllowedPointer].

### stopTrackingPointer()

```dart
void stopTrackingPointer(int pointer)
```

Stops events related to the given pointer ID from being routed to this recognizer.

If this function reduces the number of tracked pointers to zero, it will call [didStopTrackingLastPointer] synchronously.

Use [startTrackingPointer] to add the routes in the first place.

### stopTrackingIfPointerNoLongerDown()

```dart
void stopTrackingIfPointerNoLongerDown(PointerEvent event)
```

Stops tracking the pointer associated with the given event if the event is a [PointerUpEvent] or a [PointerCancelEvent] event.

# GestureRecognizerState

```dart
enum GestureRecognizerState {}
```

The possible states of a [PrimaryPointerGestureRecognizer].

The recognizer advances from [ready] to [possible] when it starts tracking a primary pointer. Where it advances from there depends on how the gesture is resolved for that pointer:

- If the primary pointer is resolved by the gesture winning the arena, the recognizer stays in the [possible] state as long as it continues to track a pointer.
- If the primary pointer is resolved by the gesture being rejected and losing the arena, the recognizer's state advances to [defunct].

Once the recognizer has stopped tracking any remaining pointers, the recognizer returns to [ready].

The recognizer is ready to start recognizing a gesture.

The sequence of pointer events seen thus far is consistent with the gesture the recognizer is attempting to recognize but the gesture has not been accepted definitively.

Further pointer events cannot cause this recognizer to recognize the gesture until the recognizer returns to the [ready] state (typically when all the pointers the recognizer is tracking are removed from the screen).

# PrimaryPointerGestureRecognizer

```dart
abstract class PrimaryPointerGestureRecognizer extends OneSequenceGestureRecognizer {}
```

A base class for gesture recognizers that track a single primary pointer.

Gestures based on this class will stop tracking the gesture if the primary pointer travels beyond [preAcceptSlopTolerance] or [postAcceptSlopTolerance] pixels from the original contact point of the gesture.

If the [preAcceptSlopTolerance] was breached before the gesture was accepted in the gesture arena, the gesture will be rejected.

### PrimaryPointerGestureRecognizer()

```dart
PrimaryPointerGestureRecognizer({Duration? deadline, double? preAcceptSlopTolerance = _unsetTouchSlop, double? postAcceptSlopTolerance = _unsetTouchSlop, Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Initializes the [deadline] field during construction of subclasses.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### deadline

```dart
Duration? deadline
```

If non-null, the recognizer will call [didExceedDeadline] after this amount of time has elapsed since starting to track the primary pointer.

The [didExceedDeadline] will not be called if the primary pointer is accepted, rejected, or all pointers are up or canceled before [deadline].

### preAcceptSlopTolerance

```dart
double? get preAcceptSlopTolerance
```

The maximum distance in logical pixels the gesture is allowed to drift from the initial touch down position before the gesture is accepted.

Drifting past the allowed slop amount causes the gesture to be rejected.

Can be null to indicate that the gesture can drift for any distance. Defaults to gestureSettings.touchSlop with a fallback of 18 logical pixels.

### postAcceptSlopTolerance

```dart
double? get postAcceptSlopTolerance
```

The maximum distance in logical pixels the gesture is allowed to drift after the gesture has been accepted.

Drifting past the allowed slop amount causes the gesture to stop tracking and signaling subsequent callbacks.

Can be null to indicate that the gesture can drift for any distance. Defaults to gestureSettings.touchSlop with a fallback of 18 logical pixels.

### state

```dart
GestureRecognizerState get state
```

The current state of the recognizer.

See [GestureRecognizerState] for a description of the states.

### primaryPointer

```dart
int? get primaryPointer
```

The ID of the primary pointer this recognizer is tracking.

If this recognizer is no longer tracking any pointers, this field holds the ID of the primary pointer this recognizer was most recently tracking. This enables the recognizer to know which pointer it was most recently tracking when [acceptGesture] or [rejectGesture] is called (which may be called after the recognizer is no longer tracking a pointer if, e.g. [GestureArenaManager.hold] has been called, or if there are other recognizers keeping the arena open).

### initialPosition

```dart
OffsetPair? get initialPosition
```

The location at which the primary pointer contacted the screen.

This will only be non-null while this recognizer is tracking at least one pointer.

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### handleNonAllowedPointer()

```dart
void handleNonAllowedPointer(PointerDownEvent event)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```

### handlePrimaryPointer()

```dart
void handlePrimaryPointer(PointerEvent event)
```

Override to provide behavior for the primary pointer when the gesture is still possible.

### didExceedDeadline()

```dart
void didExceedDeadline()
```

Override to be notified when [deadline] is exceeded.

You must override this method or [didExceedDeadlineWithEvent] if you supply a [deadline]. Subclasses that override this method must _not_ call `super.didExceedDeadline()`.

### didExceedDeadlineWithEvent()

```dart
void didExceedDeadlineWithEvent(PointerDownEvent event)
```

Same as [didExceedDeadline] but receives the [event] that initiated the gesture.

You must override this method or [didExceedDeadline] if you supply a [deadline]. Subclasses that override this method must _not_ call `super.didExceedDeadlineWithEvent(event)`.

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

# OffsetPair

```dart
class OffsetPair {}
```

A container for a [local] and [global] [Offset] pair.

Usually, the [global] [Offset] is in the coordinate space of the screen after conversion to logical pixels and the [local] offset is the same [Offset], but transformed to a local coordinate space.

### OffsetPair()

```dart
OffsetPair({required Offset local, required Offset global})
```

Creates a [OffsetPair] combining a [local] and [global] [Offset].

### OffsetPair.fromEventPosition()

```dart
OffsetPair.fromEventPosition(PointerEvent event)
```

Creates a [OffsetPair] from [PointerEvent.localPosition] and [PointerEvent.position].

### OffsetPair.fromEventDelta()

```dart
OffsetPair.fromEventDelta(PointerEvent event)
```

Creates a [OffsetPair] from [PointerEvent.localDelta] and [PointerEvent.delta].

### zero

```dart
OffsetPair zero
```

A [OffsetPair] where both [Offset]s are [Offset.zero].

### local

```dart
Offset local
```

The [Offset] in the local coordinate space.

### global

```dart
Offset global
```

The [Offset] in the global coordinate space after conversion to logical pixels.

### operator +()

```dart
OffsetPair operator +(OffsetPair other)
```

Adds the `other.global` to [global] and `other.local` to [local].

### operator -()

```dart
OffsetPair operator -(OffsetPair other)
```

Subtracts the `other.global` from [global] and `other.local` from [local].

### toString()

```dart
String toString()
```
