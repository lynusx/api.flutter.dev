@docImport 'binding.dart';

# MouseTrackerHitTest

```dart
typedef MouseTrackerHitTest = HitTestResult Function(Offset offset, int viewId)
```

Signature for hit testing at the given offset for the specified view.

It is used by the [MouseTracker] to fetch annotations for the mouse position.

# MouseTracker

```dart
class MouseTracker extends ChangeNotifier {}
```

Tracks the relationship between mouse devices and annotations, and triggers mouse events and cursor changes accordingly.

The [MouseTracker] tracks the relationship between mouse devices and [MouseTrackerAnnotation], notified by [updateWithEvent] and [updateAllDevices]. At every update, [MouseTracker] triggers the following changes if applicable:

- Dispatches mouse-related pointer events (pointer enter, hover, and exit).
- Changes mouse cursors.
- Notifies when [mouseIsConnected] changes.

This class is a [ChangeNotifier] that notifies its listeners if the value of [mouseIsConnected] changes.

An instance of [MouseTracker] is owned by the global singleton [RendererBinding].

### MouseTracker()

```dart
MouseTracker(MouseTrackerHitTest hitTestInView)
```

Create a mouse tracker.

The `hitTestInView` is used to find the render objects on a given position in the specific view. It is typically provided by the [RendererBinding].

### mouseIsConnected

```dart
bool get mouseIsConnected
```

Whether or not at least one mouse is connected and has produced events.

### updateWithEvent()

```dart
void updateWithEvent(PointerEvent event, HitTestResult? hitTestResult)
```

Perform a device update for one device according to the given new event.

The [updateWithEvent] is typically called by [RendererBinding] during the handler of a pointer event. All pointer events should call this method, and let [MouseTracker] filter which to react to.

The `hitTestResult` serves as an optional optimization, and is the hit test result already performed by [RendererBinding] for other gestures. It can be null, but when it's not null, it should be identical to the result from directly calling `hitTestInView` given in the constructor (which means that it should not use the cached result for [PointerMoveEvent]).

The [updateWithEvent] is one of the two ways of updating mouse states, the other one being [updateAllDevices].

### updateAllDevices()

```dart
void updateAllDevices()
```

Perform a device update for all detected devices.

The [updateAllDevices] is typically called during the post frame phase, indicating a frame has passed and all objects have potentially moved. For each connected device, the [updateAllDevices] will make a hit test on the device's last seen position, and check if necessary changes need to be made.

The [updateAllDevices] is one of the two ways of updating mouse states, the other one being [updateWithEvent].

### debugDeviceActiveCursor()

```dart
MouseCursor? debugDeviceActiveCursor(int device)
```

Returns the active mouse cursor for a device.

The return value is the last [MouseCursor] activated onto this device, even if the activation failed.

This function is only active when asserts are enabled. In release builds, it always returns null.
