@docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# TickerCallback

```dart
typedef TickerCallback = void Function(Duration elapsed)
```

Signature for the callback passed to the [Ticker] class's constructor.

The argument is the time elapsed from the frame timestamp when the ticker was last started to the current frame timestamp.

# TickerProvider

```dart
abstract class TickerProvider {}
```

An interface implemented by classes that can vend [Ticker] objects.

To obtain a [TickerProvider], consider mixing in either [TickerProviderStateMixin] (which always works) or [SingleTickerProviderStateMixin] (which is more efficient when it works) to make a [State] subclass implement [TickerProvider]. That [State] can then be passed to lower-level widgets or other related objects. This ensures the resulting [Ticker]s will only tick when that [State]'s subtree is enabled, as defined by [TickerMode].

In widget tests, the [WidgetTester] object is also a [TickerProvider].

Tickers can be used by any object that wants to be notified whenever a frame triggers, but are most commonly used indirectly via an [AnimationController]. [AnimationController]s need a [TickerProvider] to obtain their [Ticker].

### TickerProvider()

```dart
TickerProvider()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### createTicker()

```dart
Ticker createTicker(TickerCallback onTick)
```

Creates a ticker with the given callback.

The kind of ticker provided depends on the kind of ticker provider.

# Ticker

```dart
class Ticker {}
```

Calls its callback once per animation frame, when enabled.

To obtain a ticker, consider [TickerProvider].

When created, a ticker is initially disabled. Call [start] to enable the ticker.

A [Ticker] can be silenced by setting [muted] to true. While silenced, time still elapses, and [start] and [stop] can still be called, but no callbacks are called.

By convention, the [start] and [stop] methods are used by the ticker's consumer (for example, an [AnimationController]), and the [muted] property is controlled by the [TickerProvider] that created the ticker (for example, a [State] that uses [TickerProviderStateMixin] to silence the ticker when the state's subtree is disabled as defined by [TickerMode]).

See also:

- [TickerProvider], for obtaining a ticker.
- [SchedulerBinding.scheduleFrameCallback], which drives tickers.

### Ticker()

```dart
Ticker(TickerCallback _onTick, {String? debugLabel})
```

Creates a ticker that will call the provided callback once per frame while running.

An optional label can be provided for debugging purposes. That label will appear in the [toString] output in debug builds.

### forceFrames

```dart
bool forceFrames
```

If true, this ticker will request frames using [SchedulerBinding.scheduleForcedFrame] instead of [SchedulerBinding.scheduleFrame].

This allows granular control to advance frames even when frames are typically disabled (e.g. when the app is in the background). This should be used sparingly as it can increase battery usage.

### muted

```dart
bool get muted
```

Whether this ticker has been silenced.

While silenced, a ticker's clock can still run, but the callback will not be called.

### muted

```dart
set muted(bool value)
```

When set to true, silences the ticker, so that it is no longer ticking. If a tick is already scheduled, it will unschedule it. This will not unschedule the next frame, though.

When set to false, unsilences the ticker, potentially scheduling a frame to handle the next tick.

By convention, the [muted] property is controlled by the object that created the [Ticker] (typically a [TickerProvider]), not the object that listens to the ticker's ticks.

### isTicking

```dart
bool get isTicking
```

Whether this [Ticker] has scheduled a call to call its callback on the next frame.

A ticker that is [muted] can be active (see [isActive]) yet not be ticking. In that case, the ticker will not call its callback, and [isTicking] will be false, but time will still be progressing.

This will return false if the [SchedulerBinding.lifecycleState] is one that indicates the application is not currently visible (e.g. if the device's screen is turned off).

### isActive

```dart
bool get isActive
```

Whether time is elapsing for this [Ticker]. Becomes true when [start] is called and false when [stop] is called.

A ticker can be active yet not be actually ticking (i.e. not be calling the callback). To determine if a ticker is actually ticking, use [isTicking].

### start()

```dart
TickerFuture start()
```

Starts the clock for this [Ticker]. If the ticker is not [muted], then this also starts calling the ticker's callback once per animation frame.

The returned future resolves once the ticker [stop]s ticking. If the ticker is disposed, the future does not resolve. A derivative future is available from the returned [TickerFuture] object that resolves with an error in that case, via [TickerFuture.orCancel].

Calling this sets [isActive] to true.

This method cannot be called while the ticker is active. To restart the ticker, first [stop] it.

By convention, this method is used by the object that receives the ticks (as opposed to the [TickerProvider] which created the ticker).

### describeForError()

```dart
DiagnosticsNode describeForError(String name)
```

Adds a debug representation of a [Ticker] optimized for including in error messages.

### stop()

```dart
void stop({bool canceled = false})
```

Stops calling this [Ticker]'s callback.

If called with the `canceled` argument set to false (the default), causes the future returned by [start] to resolve. If called with the `canceled` argument set to true, the future does not resolve, and the future obtained from [TickerFuture.orCancel], if any, resolves with a [TickerCanceled] error.

Calling this sets [isActive] to false.

This method does nothing if called when the ticker is inactive.

By convention, this method is used by the object that receives the ticks (as opposed to the [TickerProvider] which created the ticker).

### scheduled

```dart
bool get scheduled
```

Whether this [Ticker] has already scheduled a frame callback.

### shouldScheduleTick

```dart
bool get shouldScheduleTick
```

Whether a tick should be scheduled.

If this is true, then calling [scheduleTick] should succeed.

Reasons why a tick should not be scheduled include:

- A tick has already been scheduled for the coming frame.
- The ticker is not active ([start] has not been called).
- The ticker is not ticking, e.g. because it is [muted] (see [isTicking]).

### scheduleTick()

```dart
void scheduleTick({bool rescheduling = false})
```

Schedules a tick for the next frame.

This should only be called if [shouldScheduleTick] is true.

### unscheduleTick()

```dart
void unscheduleTick()
```

Cancels the frame callback that was requested by [scheduleTick], if any.

Calling this method when no tick is [scheduled] is harmless.

This method should not be called when [shouldScheduleTick] would return true if no tick was scheduled.

### absorbTicker()

```dart
void absorbTicker(Ticker originalTicker)
```

Makes this [Ticker] take the state of another ticker, and disposes the other ticker.

This is useful if an object with a [Ticker] is given a new [TickerProvider] but needs to maintain continuity. In particular, this maintains the identity of the [TickerFuture] returned by the [start] function of the original [Ticker] if the original ticker is active.

This ticker must not be active when this method is called.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

It is legal to call this method while [isActive] is true, in which case:

- The frame callback that was requested by [scheduleTick], if any, is canceled.
- The future that was returned by [start] does not resolve.
- The future obtained from [TickerFuture.orCancel], if any, resolves with a [TickerCanceled] error.

### debugLabel

```dart
String? debugLabel
```

An optional label can be provided for debugging purposes.

This label will appear in the [toString] output in debug builds.

### toString()

```dart
String toString({bool debugIncludeStack = false})
```

# TickerFuture

```dart
class TickerFuture implements Future<void> {}
```

An object representing an ongoing [Ticker] sequence.

The [Ticker.start] method returns a [TickerFuture]. The [TickerFuture] will complete successfully if the [Ticker] is stopped using [Ticker.stop] with the `canceled` argument set to false (the default).

If the [Ticker] is disposed without being stopped, or if it is stopped with `canceled` set to true, then this Future will never complete. For this reason, [TickerFuture]s should generally not be awaited, as they risk hanging indefinitely if the [Ticker] is canceled or muted before the animation completes.

Methods returning a [TickerFuture] are typically marked with `@awaitNotRequired` (or similar annotations) to signal that ignoring the Future is the intended pattern. Callers who need to react to completion should use [whenComplete] to handle both success and cancellation safely.

This class works like a normal [Future], but has an additional property, [orCancel], which returns a derivative [Future] that completes with an error if the [Ticker] that returned the [TickerFuture] was stopped with `canceled` set to true, or if it was disposed without being stopped.

To run a callback when either this future resolves or when the ticker is canceled, use [whenCompleteOrCancel].

### TickerFuture.complete()

```dart
TickerFuture.complete()
```

Creates a [TickerFuture] instance that represents an already-complete [Ticker] sequence.

This is useful for implementing objects that normally defer to a [Ticker] but sometimes can skip the ticker because the animation is of zero duration, but which still need to represent the completed animation in the form of a [TickerFuture].

### whenCompleteOrCancel()

```dart
void whenCompleteOrCancel(VoidCallback callback)
```

Calls `callback` either when this future resolves or when the ticker is canceled.

Calling this method registers an exception handler for the [orCancel] future, so even if the [orCancel] property is accessed, canceling the ticker will not cause an uncaught exception in the current zone.

### orCancel

```dart
Future<void> get orCancel
```

A future that resolves when this future resolves or throws when the ticker is canceled.

If this property is never accessed, then canceling the ticker does not throw any exceptions. Once this property is accessed, though, if the corresponding ticker is canceled, then the [Future] returned by this getter will complete with an error, and if that error is not caught, there will be an uncaught exception in the current zone.

### asStream()

```dart
Stream<void> asStream()
```

### catchError()

```dart
Future<void> catchError(Function onError, {bool Function(Object)? test})
```

### then()

```dart
Future<R> then<R>(FutureOr<R> Function(void value) onValue, {Function? onError})
```

### timeout()

```dart
Future<void> timeout(Duration timeLimit, {FutureOr<void> Function()? onTimeout})
```

### whenComplete()

```dart
Future<void> whenComplete(dynamic Function() action)
```

### toString()

```dart
String toString()
```

# TickerCanceled

```dart
class TickerCanceled implements Exception {}
```

Exception thrown by [Ticker] objects on the [TickerFuture.orCancel] future when the ticker is canceled.

### TickerCanceled()

```dart
TickerCanceled([Ticker? ticker])
```

Creates a canceled-ticker exception.

### ticker

```dart
Ticker? ticker
```

Reference to the [Ticker] object that was canceled.

This may be null in the case that the [Future] created for [TickerFuture.orCancel] was created after the ticker was canceled.

### toString()

```dart
String toString()
```
