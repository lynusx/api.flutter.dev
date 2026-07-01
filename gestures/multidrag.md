@docImport 'package:flutter/widgets.dart';

@docImport 'long_press.dart'; @docImport 'monodrag.dart';

# GestureMultiDragStartCallback

```dart
typedef GestureMultiDragStartCallback = Drag? Function(Offset position)
```

Signature for when [MultiDragGestureRecognizer] recognizes the start of a drag gesture.

# MultiDragPointerState

```dart
abstract class MultiDragPointerState {}
```

Per-pointer state for a [MultiDragGestureRecognizer].

A [MultiDragGestureRecognizer] tracks each pointer separately. The state for each pointer is a subclass of [MultiDragPointerState].

### MultiDragPointerState()

```dart
MultiDragPointerState(Offset initialPosition, PointerDeviceKind kind, DeviceGestureSettings? gestureSettings)
```

Creates per-pointer state for a [MultiDragGestureRecognizer].

### gestureSettings

```dart
DeviceGestureSettings? gestureSettings
```

Device specific gesture configuration that should be preferred over framework constants.

These settings are commonly retrieved from a [MediaQuery].

### initialPosition

```dart
Offset initialPosition
```

The global coordinates of the pointer when the pointer contacted the screen.

### kind

```dart
PointerDeviceKind kind
```

The kind of pointer performing the multi-drag gesture.

Used by subclasses to determine the appropriate hit slop, for example.

### pendingDelta

```dart
Offset? get pendingDelta
```

The offset of the pointer from the last position that was reported to the client.

After the pointer contacts the screen, the pointer might move some distance before this movement will be recognized as a drag. This field accumulates that movement so that we can report it to the client after the drag starts.

### resolve()

```dart
void resolve(GestureDisposition disposition)
```

Resolve this pointer's entry in the [GestureArenaManager] with the given disposition.

### checkForResolutionAfterMove()

```dart
void checkForResolutionAfterMove()
```

Override this to call resolve() if the drag should be accepted or rejected. This is called when a pointer movement is received, but only if the gesture has not yet been resolved.

### accepted()

```dart
void accepted(GestureMultiDragStartCallback starter)
```

Called when the gesture was accepted.

Either immediately or at some future point before the gesture is disposed, call starter(), passing it initialPosition, to start the drag.

### rejected()

```dart
void rejected()
```

Called when the gesture was rejected.

The [dispose] method will be called immediately following this.

### dispose()

```dart
void dispose()
```

Releases any resources used by the object.

# MultiDragGestureRecognizer

```dart
abstract class MultiDragGestureRecognizer extends GestureRecognizer {}
```

Recognizes movement on a per-pointer basis.

In contrast to [DragGestureRecognizer], [MultiDragGestureRecognizer] watches each pointer separately, which means multiple drags can be recognized concurrently if multiple pointers are in contact with the screen.

[MultiDragGestureRecognizer] is not intended to be used directly. Instead, consider using one of its subclasses to recognize specific types for drag gestures.

See also:

- [ImmediateMultiDragGestureRecognizer], the most straight-forward variant of multi-pointer drag gesture recognizer.
- [HorizontalMultiDragGestureRecognizer], which only recognizes drags that start horizontally.
- [VerticalMultiDragGestureRecognizer], which only recognizes drags that start vertically.
- [DelayedMultiDragGestureRecognizer], which only recognizes drags that start after a long-press gesture.

### MultiDragGestureRecognizer()

```dart
MultiDragGestureRecognizer({required Object? debugOwner, Set<InvalidType>? supportedDevices, AllowedButtonsFilter? allowedButtonsFilter})
```

Initialize the object.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### onStart

```dart
GestureMultiDragStartCallback? onStart
```

Called when this class recognizes the start of a drag gesture.

The remaining notifications for this drag gesture are delivered to the [Drag] object returned by this callback.

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### createNewPointerState()

```dart
MultiDragPointerState createNewPointerState(PointerDownEvent event)
```

Subclasses should override this method to create per-pointer state objects to track the pointer associated with the given event.

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

# ImmediateMultiDragGestureRecognizer

```dart
class ImmediateMultiDragGestureRecognizer extends MultiDragGestureRecognizer {}
```

Recognizes movement both horizontally and vertically on a per-pointer basis.

In contrast to [PanGestureRecognizer], [ImmediateMultiDragGestureRecognizer] watches each pointer separately, which means multiple drags can be recognized concurrently if multiple pointers are in contact with the screen.

See also:

- [PanGestureRecognizer], which recognizes only one drag gesture at a time, regardless of how many fingers are involved.
- [HorizontalMultiDragGestureRecognizer], which only recognizes drags that start horizontally.
- [VerticalMultiDragGestureRecognizer], which only recognizes drags that start vertically.
- [DelayedMultiDragGestureRecognizer], which only recognizes drags that start after a long-press gesture.

### ImmediateMultiDragGestureRecognizer()

```dart
ImmediateMultiDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int)? allowedButtonsFilter})
```

Create a gesture recognizer for tracking multiple pointers at once.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### createNewPointerState()

```dart
MultiDragPointerState createNewPointerState(PointerDownEvent event)
```

### debugDescription

```dart
String get debugDescription
```

# HorizontalMultiDragGestureRecognizer

```dart
class HorizontalMultiDragGestureRecognizer extends MultiDragGestureRecognizer {}
```

Recognizes movement in the horizontal direction on a per-pointer basis.

In contrast to [HorizontalDragGestureRecognizer], [HorizontalMultiDragGestureRecognizer] watches each pointer separately, which means multiple drags can be recognized concurrently if multiple pointers are in contact with the screen.

See also:

- [HorizontalDragGestureRecognizer], a gesture recognizer that just looks at horizontal movement.
- [ImmediateMultiDragGestureRecognizer], a similar recognizer, but without the limitation that the drag must start horizontally.
- [VerticalMultiDragGestureRecognizer], which only recognizes drags that start vertically.

### HorizontalMultiDragGestureRecognizer()

```dart
HorizontalMultiDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int)? allowedButtonsFilter})
```

Create a gesture recognizer for tracking multiple pointers at once but only if they first move horizontally.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### createNewPointerState()

```dart
MultiDragPointerState createNewPointerState(PointerDownEvent event)
```

### debugDescription

```dart
String get debugDescription
```

# VerticalMultiDragGestureRecognizer

```dart
class VerticalMultiDragGestureRecognizer extends MultiDragGestureRecognizer {}
```

Recognizes movement in the vertical direction on a per-pointer basis.

In contrast to [VerticalDragGestureRecognizer], [VerticalMultiDragGestureRecognizer] watches each pointer separately, which means multiple drags can be recognized concurrently if multiple pointers are in contact with the screen.

See also:

- [VerticalDragGestureRecognizer], a gesture recognizer that just looks at vertical movement.
- [ImmediateMultiDragGestureRecognizer], a similar recognizer, but without the limitation that the drag must start vertically.
- [HorizontalMultiDragGestureRecognizer], which only recognizes drags that start horizontally.

### VerticalMultiDragGestureRecognizer()

```dart
VerticalMultiDragGestureRecognizer({Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int)? allowedButtonsFilter})
```

Create a gesture recognizer for tracking multiple pointers at once but only if they first move vertically.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### createNewPointerState()

```dart
MultiDragPointerState createNewPointerState(PointerDownEvent event)
```

### debugDescription

```dart
String get debugDescription
```

# DelayedMultiDragGestureRecognizer

```dart
class DelayedMultiDragGestureRecognizer extends MultiDragGestureRecognizer {}
```

Recognizes movement both horizontally and vertically on a per-pointer basis after a delay.

In contrast to [ImmediateMultiDragGestureRecognizer], [DelayedMultiDragGestureRecognizer] waits for a [delay] before recognizing the drag. If the pointer moves more than [kTouchSlop] before the delay expires, the gesture is not recognized.

In contrast to [PanGestureRecognizer], [DelayedMultiDragGestureRecognizer] watches each pointer separately, which means multiple drags can be recognized concurrently if multiple pointers are in contact with the screen.

See also:

- [ImmediateMultiDragGestureRecognizer], a similar recognizer but without the delay.
- [PanGestureRecognizer], which recognizes only one drag gesture at a time, regardless of how many fingers are involved.

### DelayedMultiDragGestureRecognizer()

```dart
DelayedMultiDragGestureRecognizer({Duration delay = kLongPressTimeout, Object? debugOwner, Set<InvalidType>? supportedDevices, bool Function(int)? allowedButtonsFilter})
```

Creates a drag recognizer that works on a per-pointer basis after a delay.

In order for a drag to be recognized by this recognizer, the pointer must remain in the same place for [delay] (up to [kTouchSlop]). The [delay] defaults to [kLongPressTimeout] to match [LongPressGestureRecognizer] but can be changed for specific behaviors.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### delay

```dart
Duration delay
```

The amount of time the pointer must remain in the same place for the drag to be recognized.

### createNewPointerState()

```dart
MultiDragPointerState createNewPointerState(PointerDownEvent event)
```

### debugDescription

```dart
String get debugDescription
```
