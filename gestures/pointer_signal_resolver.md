@docImport 'package:flutter/widgets.dart';

@docImport 'binding.dart';

# PointerSignalResolvedCallback

```dart
typedef PointerSignalResolvedCallback = void Function(PointerSignalEvent event)
```

The callback to register with a [PointerSignalResolver] to express interest in a pointer signal event.

# PointerSignalResolver

```dart
class PointerSignalResolver {}
```

Mediates disputes over which listener should handle pointer signal events when multiple listeners wish to handle those events.

Pointer signals (such as [PointerScrollEvent]) are immediate, so unlike events that participate in the gesture arena, pointer signals always resolve at the end of event dispatch. Yet if objects interested in handling these signal events were to handle them directly, it would cause issues such as multiple [Scrollable] widgets in the widget hierarchy responding to the same mouse wheel event. Using this class, these events will only be dispatched to the first registered handler, which will in turn correspond to the widget that's deepest in the widget hierarchy.

To use this class, objects should register their event handler like so:

```dart
void handleSignalEvent(PointerSignalEvent event) {
  GestureBinding.instance.pointerSignalResolver.register(event, (PointerSignalEvent event) {
    // handle the event...
  });
}
```

{@tool dartpad} Here is an example that demonstrates the effect of not using the resolver versus using it.

When this example is set to _not_ use the resolver, then triggering the mouse wheel over the outer box will cause only the outer box to change color, but triggering the mouse wheel over the inner box will cause _both_ the outer and the inner boxes to change color (because they're both receiving the event).

When this example is set to _use_ the resolver, then only the box located directly under the cursor will change color when the mouse wheel is triggered.

** See code in examples/api/lib/gestures/pointer_signal_resolver/pointer_signal_resolver.0.dart ** {@end-tool}

### register()

```dart
void register(PointerSignalEvent event, PointerSignalResolvedCallback callback)
```

Registers interest in handling [event].

This method may be called multiple times (typically from different parts of the widget hierarchy) for the same `event`, with different `callback`s, as the event is being dispatched across the tree. Once the dispatching is complete, the [GestureBinding] calls [resolve], and the first registered callback is called.

The `callback` is invoked with one argument, the `event`.

Once the [register] method has been called with a particular `event`, it must not be called for other `event`s until after [resolve] has been called. Only one event disambiguation can be in flight at a time. In normal use this is achieved by only registering callbacks for an event as it is actively being dispatched (for example, in [Listener.onPointerSignal]).

See the documentation for the [PointerSignalResolver] class for an example of using this method.

### resolve()

```dart
void resolve(PointerSignalEvent event)
```

Resolves the event, calling the first registered callback if there was one.

This is called by the [GestureBinding] after the framework has finished dispatching the pointer signal event.
