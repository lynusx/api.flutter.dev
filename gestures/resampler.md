# HandleEventCallback

```dart
typedef HandleEventCallback = void Function(PointerEvent event)
```

A callback used by [PointerEventResampler.sample] and [PointerEventResampler.stop] to process a resampled `event`.

# PointerEventResampler

```dart
class PointerEventResampler {}
```

Class for pointer event resampling.

An instance of this class can be used to resample one sequence of pointer events. Multiple instances are expected to be used for multi-touch support. The sampling frequency and the sampling offset is determined by the caller.

This can be used to get smooth touch event processing at the cost of adding some latency. Devices with low frequency sensors or when the frequency is not a multiple of the display frequency (e.g., 120Hz input and 90Hz display) benefit from this.

The following pointer event types are supported: [PointerAddedEvent], [PointerHoverEvent], [PointerDownEvent], [PointerMoveEvent], [PointerCancelEvent], [PointerUpEvent], [PointerRemovedEvent].

Resampling is currently limited to event position and delta. All pointer event types except [PointerAddedEvent] will be resampled. [PointerHoverEvent] and [PointerMoveEvent] will only be generated when the position has changed.

### addEvent()

```dart
void addEvent(PointerEvent event)
```

Enqueue pointer `event` for resampling.

### sample()

```dart
void sample(Duration sampleTime, Duration nextSampleTime, HandleEventCallback callback)
```

Dispatch resampled pointer events for the specified `sampleTime` by calling [callback].

This may dispatch multiple events if position is not the only state that has changed since last sample.

Calling [callback] must not add or sample events.

Positive value for `nextSampleTime` allow early processing of up and removed events. This improves resampling of these events, which is important for fling animations.

### stop()

```dart
void stop(HandleEventCallback callback)
```

Stop resampling.

This will dispatch pending events by calling [callback] and reset internal state.

### hasPendingEvents

```dart
bool get hasPendingEvents
```

Returns `true` if a call to [sample] can dispatch more events.

### isTracked

```dart
bool get isTracked
```

Returns `true` if pointer is currently tracked.

### isDown

```dart
bool get isDown
```

Returns `true` if pointer is currently down.
