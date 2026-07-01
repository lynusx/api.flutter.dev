@docImport 'package:fake_async/fake_async.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'recognizer.dart';

# SamplingClock

```dart
class SamplingClock {}
```

Class that implements clock used for sampling.

### now()

```dart
DateTime now()
```

Returns current time.

### stopwatch()

```dart
Stopwatch stopwatch()
```

Returns a new stopwatch that uses the current time as reported by `this`.

See also:

- [GestureBinding.debugSamplingClock], which is used in tests and debug builds to observe [FakeAsync].

# GestureBinding

```dart
mixin GestureBinding on BindingBase implements HitTestable, HitTestDispatcher, HitTestTarget {}
```

A binding for the gesture subsystem.

## Lifecycle of pointer events and the gesture arena

### [PointerDownEvent]

When a [PointerDownEvent] is received by the [GestureBinding] (from [dart:ui.PlatformDispatcher.onPointerDataPacket], as interpreted by the [PointerEventConverter]), a [hitTest] is performed to determine which [HitTestTarget] nodes are affected. (Other bindings are expected to implement [hitTest] to defer to [HitTestable] objects. For example, the rendering layer defers to the [RenderView] and the rest of the render object hierarchy.)

The affected nodes then are given the event to handle ([dispatchEvent] calls [HitTestTarget.handleEvent] for each affected node). If any have relevant [GestureRecognizer]s, they provide the event to them using [GestureRecognizer.addPointer]. This typically causes the recognizer to register with the [PointerRouter] to receive notifications regarding the pointer in question.

Once the hit test and dispatching logic is complete, the event is then passed to the aforementioned [PointerRouter], which passes it to any objects that have registered interest in that event.

Finally, the [gestureArena] is closed for the given pointer ([GestureArenaManager.close]), which begins the process of selecting a gesture to win that pointer.

### Other events

A pointer that is [PointerEvent.down] may send further events, such as [PointerMoveEvent], [PointerUpEvent], or [PointerCancelEvent]. These are sent to the same [HitTestTarget] nodes as were found when the [PointerDownEvent] was received (even if they have since been disposed; it is the responsibility of those objects to be aware of that possibility).

Then, the events are routed to any still-registered entrants in the [PointerRouter]'s table for that pointer.

When a [PointerUpEvent] is received, the [GestureArenaManager.sweep] method is invoked to force the gesture arena logic to terminate if necessary.

### initInstances()

```dart
void initInstances()
```

### instance

```dart
GestureBinding get instance
```

The singleton instance of this object.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### unlocked()

```dart
void unlocked()
```

### cancelPointer()

```dart
void cancelPointer(int pointer)
```

Dispatch a [PointerCancelEvent] for the given pointer soon.

The pointer event will be dispatched before the next pointer event and before the end of the microtask but not within this function call.

### pointerRouter

```dart
PointerRouter pointerRouter
```

A router that routes all pointer events received from the engine.

### gestureArena

```dart
GestureArenaManager gestureArena
```

The gesture arenas used for disambiguating the meaning of sequences of pointer events.

### pointerSignalResolver

```dart
PointerSignalResolver pointerSignalResolver
```

The resolver used for determining which widget handles a [PointerSignalEvent].

State for all pointers which are currently down.

This map caches the hit test result done when the pointer goes down ([PointerDownEvent] and [PointerPanZoomStartEvent]). This hit test result will be used throughout the entire pointer interaction; that is, the pointer is seen as pointing to the same place even if it has moved away until pointer goes up ([PointerUpEvent] and [PointerPanZoomEndEvent]). This matches the expected gesture interaction with a button, and allows devices that don't support hovering to perform as few hit tests as possible.

On the other hand, hovering requires hit testing on almost every frame. This is handled in [RendererBinding] and [MouseTracker], and will ignore the results cached here.

### handlePointerEvent()

```dart
void handlePointerEvent(PointerEvent event)
```

Dispatch an event to the targets found by a hit test on its position.

This method sends the given event to [dispatchEvent] based on event types:

- [PointerDownEvent]s and [PointerSignalEvent]s are dispatched to the result of a new [hitTest].
- [PointerUpEvent]s and [PointerMoveEvent]s are dispatched to the result of hit test of the preceding [PointerDownEvent]s.
- [PointerHoverEvent]s, [PointerAddedEvent]s, and [PointerRemovedEvent]s are dispatched without a hit test result.

### hitTestInView()

```dart
void hitTestInView(HitTestResult result, Offset position, int viewId)
```

Determine which [HitTestTarget] objects are located at a given position in the specified view.

### hitTest()

```dart
void hitTest(HitTestResult result, Offset position)
```

### dispatchEvent()

```dart
void dispatchEvent(PointerEvent event, HitTestResult? hitTestResult)
```

Dispatch an event to [pointerRouter] and the path of a hit test result.

The `event` is routed to [pointerRouter]. If the `hitTestResult` is not null, the event is also sent to every [HitTestTarget] in the entries of the given [HitTestResult]. Any exceptions from the handlers are caught.

The `hitTestResult` argument may only be null for [PointerAddedEvent]s or [PointerRemovedEvent]s.

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

### resetGestureBinding()

```dart
void resetGestureBinding()
```

Reset states of [GestureBinding].

This clears the hit test records.

This is typically called between tests.

### debugSamplingClock

```dart
SamplingClock? get debugSamplingClock
```

Overrides the sampling clock for debugging and testing.

This value is ignored in non-debug builds.

### samplingClock

```dart
SamplingClock get samplingClock
```

Provides access to the current [DateTime] and `StopWatch` objects for sampling.

Overridden by [debugSamplingClock] for debug builds and testing. Using this object under test will maintain synchronization with [FakeAsync].

### resamplingEnabled

```dart
bool resamplingEnabled
```

Enable pointer event resampling for touch devices by setting this to true.

Resampling results in smoother touch event processing at the cost of some added latency. Devices with low frequency sensors or when the frequency is not a multiple of the display frequency (e.g., 120Hz input and 90Hz display) benefit from this.

This is typically set during application initialization but can be adjusted dynamically in case the application only wants resampling for some period of time.

### samplingOffset

```dart
Duration samplingOffset
```

Offset relative to current frame time that should be used for resampling. The [samplingOffset] is expected to be negative. Non-negative [samplingOffset] is allowed but will effectively disable resampling.

# FlutterErrorDetailsForPointerEventDispatcher

```dart
class FlutterErrorDetailsForPointerEventDispatcher extends FlutterErrorDetails {}
```

Variant of [FlutterErrorDetails] with extra fields for the gesture library's binding's pointer event dispatcher ([GestureBinding.dispatchEvent]).

### FlutterErrorDetailsForPointerEventDispatcher()

```dart
FlutterErrorDetailsForPointerEventDispatcher({required dynamic exception, dynamic stack, dynamic library, dynamic context, PointerEvent? event, HitTestEntry? hitTestEntry, dynamic informationCollector, dynamic silent})
```

Creates a [FlutterErrorDetailsForPointerEventDispatcher] object with the given arguments setting the object's properties.

The gesture library calls this constructor when catching an exception that will subsequently be reported using [FlutterError.onError].

### event

```dart
PointerEvent? event
```

The pointer event that was being routed when the exception was raised.

### hitTestEntry

```dart
HitTestEntry? hitTestEntry
```

The hit test result entry for the object whose handleEvent method threw the exception. May be null if no hit test entry is associated with the event (e.g. [PointerHoverEvent]s, [PointerAddedEvent]s, and [PointerRemovedEvent]s).

The target object itself is given by the [HitTestEntry.target] property of the hitTestEntry object.
