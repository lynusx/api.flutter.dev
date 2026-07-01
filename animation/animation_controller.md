@docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# AnimationBehavior

```dart
enum AnimationBehavior {}
```

Configures how an [AnimationController] behaves when animations are disabled.

When [AccessibilityFeatures.disableAnimations] is true, the device is asking Flutter to reduce or disable animations as much as possible. To honor this, we reduce the duration and the corresponding number of frames for animations. This enum is used to allow certain [AnimationController]s to opt out of this behavior.

For example, the [AnimationController] which controls the physics simulation for a scrollable list will have [AnimationBehavior.preserve], so that when a user attempts to scroll it does not jump to the end/beginning too quickly.

The [AnimationController] will reduce its duration when [AccessibilityFeatures.disableAnimations] is true.

The [AnimationController] will preserve its behavior.

This is the default for repeating animations in order to prevent them from flashing rapidly on the screen if the widget does not take the [AccessibilityFeatures.disableAnimations] flag into account.

Whether animations should be enabled, based on the configured behavior and the [AccessibilityFeatures.disableAnimations] flag.

# AnimationController

```dart
class AnimationController extends Animation<double> with AnimationEagerListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

A controller for an animation.

This class lets you perform tasks such as:

- Play an animation [forward] or in [reverse], or [stop] an animation.
- Set the animation to a specific [value].
- Define the [upperBound] and [lowerBound] values of an animation.
- Create a [fling] animation effect using a physics simulation.

By default, an [AnimationController] linearly produces values that range from 0.0 to 1.0, during a given duration.

When the animation is actively animating, the animation controller generates a new value each time the device running your app is ready to display a new frame (typically, this rate is around 60–120 values per second). If the animation controller is associated with a [State] through a [TickerProvider], then its updates will be silenced when that [State]'s subtree is disabled as defined by [TickerMode]; time will still elapse, and methods like [forward] and [stop] can still be called and will change the value, but the controller will not generate new values on its own.

## Ticker providers

An [AnimationController] needs a [TickerProvider], which is configured using the `vsync` argument on the constructor. The constructor uses the [TickerProvider] to create a [Ticker], which the [AnimationController] uses to step through the animation it controls.

For advice on obtaining a ticker provider, see [TickerProvider]. Typically the relevant [State] serves as the ticker provider, after applying a suitable mixin (like [SingleTickerProviderStateMixin]) to cause the [State] subclass to implement [TickerProvider].

## Life cycle

An [AnimationController] should be [dispose]d when it is no longer needed. This reduces the likelihood of leaks. When used with a [StatefulWidget], it is common for an [AnimationController] to be created in the [State.initState] method and then disposed in the [State.dispose] method.

## Using [Future]s with [AnimationController]

The methods that start animations return a [TickerFuture] object which completes when the animation completes successfully, and never throws an error; if the animation is canceled, the future never completes. This object also has a [TickerFuture.orCancel] property which returns a future that completes when the animation completes successfully, and completes with an error when the animation is aborted.

This can be used to write code such as the `fadeOutAndUpdateState` method below.

{@tool snippet}

Here is a stateful `Foo` widget. Its [State] uses the [SingleTickerProviderStateMixin] to implement the necessary [TickerProvider], creating its controller in the [State.initState] method and disposing of it in the [State.dispose] method. The duration of the controller is configured from a property in the `Foo` widget; as that changes, the [State.didUpdateWidget] method is used to update the controller.

```dart
class Foo extends StatefulWidget {
  const Foo({ super.key, required this.duration });

  final Duration duration;

  @override
  State<Foo> createState() => _FooState();
}

class _FooState extends State<Foo> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      vsync: this, // the SingleTickerProviderStateMixin
      duration: widget.duration,
    );
  }

  @override
  void didUpdateWidget(Foo oldWidget) {
    super.didUpdateWidget(oldWidget);
    _controller.duration = widget.duration;
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(); // ...
  }
}
```

{@end-tool} {@tool snippet}

The following method (for a [State] subclass) drives two animation controllers using Dart's asynchronous syntax for awaiting [Future] objects:

```dart
Future<void> fadeOutAndUpdateState() async {
  try {
    await fadeAnimationController.forward().orCancel;
    await sizeAnimationController.forward().orCancel;
    setState(() {
      dismissed = true;
    });
  } on TickerCanceled {
    // the animation got canceled, probably because we were disposed
  }
}
```

{@end-tool}

The assumption in the code above is that the animation controllers are being disposed in the [State] subclass' override of the [State.dispose] method. Since disposing the controller cancels the animation (raising a [TickerCanceled] exception), the code here can skip verifying whether [State.mounted] is still true at each step. (Again, this assumes that the controllers are created in [State.initState] and disposed in [State.dispose], as described in the previous section.)

{@tool dartpad} This example shows how to use [AnimationController] and [SlideTransition] to create an animated digit like you might find on an old pinball machine our your car's odometer. New digit values slide into place from below, as the old value slides upwards and out of view. Taps that occur while the controller is already animating cause the controller's [AnimationController.duration] to be reduced so that the visuals don't fall behind.

** See code in examples/api/lib/animation/animation_controller/animated_digit.0.dart ** {@end-tool}

See also:

- [Tween], the base class for converting an [AnimationController] to a range of values of other types.

### AnimationController()

```dart
AnimationController({double? value, Duration? duration, Duration? reverseDuration, String? debugLabel, double lowerBound = 0.0, double upperBound = 1.0, AnimationBehavior animationBehavior = AnimationBehavior.normal, required TickerProvider vsync})
```

Creates an animation controller.

- `value` is the initial value of the animation. If defaults to the lower bound.

- [duration] is the length of time this animation should last.

- [debugLabel] is a string to help identify this animation during debugging (used by [toString]).

- [lowerBound] is the smallest value this animation can obtain and the value at which this animation is deemed to be dismissed.

- [upperBound] is the largest value this animation can obtain and the value at which this animation is deemed to be completed.

- `vsync` is the required [TickerProvider] for the current context. It can be changed by calling [resync]. See [TickerProvider] for advice on obtaining a ticker provider.

### AnimationController.unbounded()

```dart
AnimationController.unbounded({double value = 0.0, Duration? duration, Duration? reverseDuration, String? debugLabel, required TickerProvider vsync, AnimationBehavior animationBehavior = AnimationBehavior.preserve})
```

Creates an animation controller with no upper or lower bound for its value.

- [value] is the initial value of the animation.

- [duration] is the length of time this animation should last.

- [debugLabel] is a string to help identify this animation during debugging (used by [toString]).

- `vsync` is the required [TickerProvider] for the current context. It can be changed by calling [resync]. See [TickerProvider] for advice on obtaining a ticker provider.

This constructor is most useful for animations that will be driven using a physics simulation, especially when the physics simulation has no pre-determined bounds.

### lowerBound

```dart
double lowerBound
```

The value at which this animation is deemed to be dismissed.

### upperBound

```dart
double upperBound
```

The value at which this animation is deemed to be completed.

### debugLabel

```dart
String? debugLabel
```

A label that is used in the [toString] output. Intended to aid with identifying animation controller instances in debug output.

### animationBehavior

```dart
AnimationBehavior animationBehavior
```

The behavior of the controller when [AccessibilityFeatures.disableAnimations] is true.

Defaults to [AnimationBehavior.normal] for the [AnimationController.new] constructor, and [AnimationBehavior.preserve] for the [AnimationController.unbounded] constructor.

### view

```dart
Animation<double> get view
```

Returns an [Animation<double>] for this animation controller, so that a pointer to this object can be passed around without allowing users of that pointer to mutate the [AnimationController] state.

### duration

```dart
Duration? duration
```

The length of time this animation should last.

If [reverseDuration] is specified, then [duration] is only used when going [forward]. Otherwise, it specifies the duration going in both directions.

### reverseDuration

```dart
Duration? reverseDuration
```

The length of time this animation should last when going in [reverse].

The value of [duration] is used if [reverseDuration] is not specified or set to null.

### resync()

```dart
void resync(TickerProvider vsync)
```

Recreates the [Ticker] with the new [TickerProvider].

### value

```dart
double get value
```

The current value of the animation.

Setting this value notifies all the listeners that the value changed.

Setting this value also stops the controller if it is currently running; if this happens, it also notifies all the status listeners.

### value

```dart
set value(double newValue)
```

Stops the animation controller and sets the current value of the animation.

The new value is clamped to the range set by [lowerBound] and [upperBound].

Value listeners are notified even if this does not change the value. Status listeners are notified if the animation was previously playing.

{@template flutter.animation.AnimationController.ticker_canceled} The most recently returned [TickerFuture], if any, is marked as having been canceled, meaning the future never completes and its [TickerFuture.orCancel] derivative future completes with a [TickerCanceled] error. {@endtemplate}

See also:

- [reset], which is equivalent to setting [value] to [lowerBound].
- [stop], which aborts the animation without changing its value or status and without dispatching any notifications other than completing or canceling the [TickerFuture].
- [forward], [reverse], [animateTo], [animateWith], [animateBackWith], [fling], and [repeat], which start the animation controller.

### reset()

```dart
void reset()
```

Sets the controller's value to [lowerBound], stopping the animation (if in progress), and resetting to its beginning point, or dismissed state.

{@macro flutter.animation.AnimationController.ticker_canceled}

See also:

- [value], which can be explicitly set to a specific value as desired.
- [forward], which starts the animation in the forward direction.
- [stop], which aborts the animation without changing its value or status and without dispatching any notifications other than completing or canceling the [TickerFuture].

### velocity

```dart
double get velocity
```

The rate of change of [value] per second.

If [isAnimating] is false, then [value] is not changing and the rate of change is zero.

### lastElapsedDuration

```dart
Duration? get lastElapsedDuration
```

The amount of time that has passed between the time the animation started and the most recent tick of the animation.

If the controller is not animating, the last elapsed duration is null.

### isAnimating

```dart
bool get isAnimating
```

Whether this animation is currently animating in either the forward or reverse direction.

This is separate from whether it is actively ticking. An animation controller's ticker might get muted, in which case the animation controller's callbacks will no longer fire even though time is continuing to pass. See [Ticker.muted] and [TickerMode].

If the animation was stopped (e.g. with [stop] or by setting a new [value]), [isAnimating] will return `false` but the [status] will not change, so the value of [AnimationStatus.isAnimating] might still be `true`.

### status

```dart
AnimationStatus get status
```

### forward()

```dart
TickerFuture forward({double? from})
```

Starts running this animation forwards (towards the end).

Returns a [TickerFuture] that completes when the animation is complete.

If [from] is non-null, it will be set as the current [value] before running the animation.

{@macro flutter.animation.AnimationController.ticker_canceled}

During the animation, [status] is reported as [AnimationStatus.forward], which switches to [AnimationStatus.completed] when [upperBound] is reached at the end of the animation.

### reverse()

```dart
TickerFuture reverse({double? from})
```

Starts running this animation in reverse (towards the beginning).

Returns a [TickerFuture] that completes when the animation is dismissed.

If [from] is non-null, it will be set as the current [value] before running the animation.

{@macro flutter.animation.AnimationController.ticker_canceled}

During the animation, [status] is reported as [AnimationStatus.reverse], which switches to [AnimationStatus.dismissed] when [lowerBound] is reached at the end of the animation.

### toggle()

```dart
TickerFuture toggle({double? from})
```

Toggles the direction of this animation, based on whether it [isForwardOrCompleted].

Specifically, this function acts the same way as [reverse] if the [status] is either [AnimationStatus.forward] or [AnimationStatus.completed], and acts as [forward] for [AnimationStatus.reverse] or [AnimationStatus.dismissed].

If [from] is non-null, it will be set as the current [value] before running the animation.

{@macro flutter.animation.AnimationController.ticker_canceled}

### animateTo()

```dart
TickerFuture animateTo(double target, {Duration? duration, Curve curve = Curves.linear})
```

Drives the animation from its current value to the given target, "forward".

Returns a [TickerFuture] that completes when the animation is complete.

{@macro flutter.animation.AnimationController.ticker_canceled}

During the animation, [status] is reported as [AnimationStatus.forward] regardless of whether `target` > [value] or not. At the end of the animation, when `target` is reached, [status] is reported as [AnimationStatus.completed].

If the `target` argument is the same as the current [value] of the animation, then this won't animate, and the returned [TickerFuture] will be already complete.

### animateBack()

```dart
TickerFuture animateBack(double target, {Duration? duration, Curve curve = Curves.linear})
```

Drives the animation from its current value to the given target, "backward".

Returns a [TickerFuture] that completes when the animation is complete.

{@macro flutter.animation.AnimationController.ticker_canceled}

During the animation, [status] is reported as [AnimationStatus.reverse] regardless of whether `target` < [value] or not. At the end of the animation, when `target` is reached, [status] is reported as [AnimationStatus.dismissed].

If the `target` argument is the same as the current [value] of the animation, then this won't animate, and the returned [TickerFuture] will be already complete.

### repeat()

```dart
TickerFuture repeat({double? min, double? max, bool reverse = false, Duration? period, int? count})
```

Starts running this animation in the forward direction, and restarts the animation when it completes.

Defaults to repeating between the [lowerBound] and [upperBound] of the [AnimationController] when no explicit value is set for [min] and [max].

With [reverse] set to true, instead of always starting over at [min] the starting value will alternate between [min] and [max] values on each repeat. The [status] will be reported as [AnimationStatus.reverse] when the animation runs from [max] to [min].

Each run of the animation will have a duration of `period`. If `period` is not provided, [duration] will be used instead, which has to be set before [repeat] is called either in the constructor or later by using the [duration] setter.

If a value is passed to [count], the animation will perform that many iterations before stopping. Otherwise, the animation repeats indefinitely.

Returns a [TickerFuture] that never completes, unless a [count] is specified. The [TickerFuture.orCancel] future completes with an error when the animation is stopped (e.g. with [stop]).

{@macro flutter.animation.AnimationController.ticker_canceled}

### fling()

```dart
TickerFuture fling({double velocity = 1.0, SpringDescription? springDescription, AnimationBehavior? animationBehavior})
```

Drives the animation with a spring (within [lowerBound] and [upperBound]) and initial velocity.

If velocity is positive, the animation will complete, otherwise it will dismiss. The velocity is specified in units per second. If the [SemanticsBinding.disableAnimations] flag is set, the velocity is somewhat arbitrarily multiplied by 200.

The [springDescription] parameter can be used to specify a custom [SpringType.criticallyDamped] or [SpringType.overDamped] spring with which to drive the animation. By default, a [SpringType.criticallyDamped] spring is used. See [SpringDescription.withDampingRatio] for how to create a suitable [SpringDescription].

The resulting spring simulation cannot be of type [SpringType.underDamped]; such a spring would oscillate rather than fling.

Returns a [TickerFuture] that completes when the animation is complete.

{@macro flutter.animation.AnimationController.ticker_canceled}

### animateWith()

```dart
TickerFuture animateWith(Simulation simulation)
```

Drives the animation according to the given simulation.

{@template flutter.animation.AnimationController.animateWith} The values from the simulation are clamped to the [lowerBound] and [upperBound]. To avoid this, consider creating the [AnimationController] using the [AnimationController.unbounded] constructor.

Returns a [TickerFuture] that completes when the animation is complete.

The most recently returned [TickerFuture], if any, is marked as having been canceled, meaning the future never completes and its [TickerFuture.orCancel] derivative future completes with a [TickerCanceled] error. {@endtemplate}

The [status] is always [AnimationStatus.forward] for the entire duration of the simulation.

See also:

- [animateBackWith], which is like this method but the status is always [AnimationStatus.reverse].

### animateBackWith()

```dart
TickerFuture animateBackWith(Simulation simulation)
```

Drives the animation according to the given simulation with a [status] of [AnimationStatus.reverse].

{@macro flutter.animation.AnimationController.animateWith}

The [status] is always [AnimationStatus.reverse] for the entire duration of the simulation.

See also:

- [animateWith], which is like this method but the status is always [AnimationStatus.forward].

### stop()

```dart
void stop({bool canceled = true})
```

Stops running this animation.

This does not trigger any notifications. The animation stops in its current state.

By default, the most recently returned [TickerFuture] is marked as having been canceled, meaning the future never completes and its [TickerFuture.orCancel] derivative future completes with a [TickerCanceled] error. By passing the `canceled` argument with the value false, this is reversed, and the futures complete successfully.

See also:

- [reset], which stops the animation and resets it to the [lowerBound], and which does send notifications.
- [forward], [reverse], [animateTo], [animateWith], [fling], and [repeat], which restart the animation controller.

### dispose()

```dart
void dispose()
```

Release the resources used by this object. The object is no longer usable after this method is called.

{@macro flutter.animation.AnimationController.ticker_canceled}

### toStringDetails()

```dart
String toStringDetails()
```
