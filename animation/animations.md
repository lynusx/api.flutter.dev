@docImport 'package:flutter/widgets.dart';

# kAlwaysCompleteAnimation

```dart
Animation<double> kAlwaysCompleteAnimation
```

An animation that is always complete.

Using this constant involves less overhead than building an [AnimationController] with an initial value of 1.0. This is useful when an API expects an animation but you don't actually want to animate anything.

# kAlwaysDismissedAnimation

```dart
Animation<double> kAlwaysDismissedAnimation
```

An animation that is always dismissed.

Using this constant involves less overhead than building an [AnimationController] with an initial value of 0.0. This is useful when an API expects an animation but you don't actually want to animate anything.

# AlwaysStoppedAnimation

```dart
class AlwaysStoppedAnimation<T> extends Animation<T> {}
```

An animation that is always stopped at a given value.

The [status] is always [AnimationStatus.forward].

### AlwaysStoppedAnimation()

```dart
AlwaysStoppedAnimation(T value)
```

Creates an [AlwaysStoppedAnimation] with the given value.

Since the [value] and [status] of an [AlwaysStoppedAnimation] can never change, the listeners can never be called. It is therefore safe to reuse an [AlwaysStoppedAnimation] instance in multiple places. If the [value] to be used is known at compile time, the constructor should be called as a `const` constructor.

### value

```dart
T value
```

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

### status

```dart
AnimationStatus get status
```

### toStringDetails()

```dart
String toStringDetails()
```

# AnimationWithParentMixin

```dart
mixin AnimationWithParentMixin<T> {}
```

Implements most of the [Animation] interface by deferring its behavior to a given [parent] Animation.

To implement an [Animation] that is driven by a parent, it is only necessary to mix in this class, implement [parent], and implement `T get value`.

To define a mapping from values in the range 0..1, consider subclassing [Tween] instead.

### parent

```dart
Animation<T> get parent
```

The animation whose value this animation will proxy.

This animation must remain the same for the lifetime of this object. If you wish to proxy a different animation at different times, consider using [ProxyAnimation].

### addListener()

```dart
void addListener(VoidCallback listener)
```

Calls the listener every time the value of the animation changes.

Listeners can be removed with [removeListener].

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Stop calling the listener every time the value of the animation changes.

Listeners can be added with [addListener].

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

Calls listener every time the status of the animation changes.

Listeners can be removed with [removeStatusListener].

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

Stops calling the listener every time the status of the animation changes.

Listeners can be added with [addStatusListener].

### status

```dart
AnimationStatus get status
```

The current status of this animation.

# ProxyAnimation

```dart
class ProxyAnimation extends Animation<double> with AnimationLazyListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

An animation that is a proxy for another animation.

A proxy animation is useful because the parent animation can be mutated. For example, one object can create a proxy animation, hand the proxy to another object, and then later change the animation from which the proxy receives its value.

### ProxyAnimation()

```dart
ProxyAnimation([Animation<double>? animation])
```

Creates a proxy animation.

If the animation argument is omitted, the proxy animation will have the status [AnimationStatus.dismissed] and a value of 0.0.

### parent

```dart
Animation<double>? get parent
```

The animation whose value this animation will proxy.

This value is mutable. When mutated, the listeners on the proxy animation will be transparently updated to be listening to the new parent animation.

### parent

```dart
set parent(Animation<double>? value)
```

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# ReverseAnimation

```dart
class ReverseAnimation extends Animation<double> with AnimationLazyListenerMixin, AnimationLocalStatusListenersMixin {}
```

An animation that is the reverse of another animation.

If the parent animation is running forward from 0.0 to 1.0, this animation is running in reverse from 1.0 to 0.0.

Using a [ReverseAnimation] is different from using a [Tween] with a `begin` of 1.0 and an `end` of 0.0 because the tween does not change the status or direction of the animation.

See also:

- [Curve.flipped] and [FlippedCurve], which provide a similar effect but on [Curve]s.
- [CurvedAnimation], which can take separate curves for when the animation is going forward than for when it is going in reverse.

### ReverseAnimation()

```dart
ReverseAnimation(Animation<double> parent)
```

Creates a reverse animation.

### parent

```dart
Animation<double> parent
```

The animation whose value and direction this animation is reversing.

### addListener()

```dart
void addListener(VoidCallback listener)
```

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# CurvedAnimation

```dart
class CurvedAnimation extends Animation<double> with AnimationWithParentMixin<double> {}
```

An animation that applies a curve to another animation.

[CurvedAnimation] is useful when you want to apply a non-linear [Curve] to an animation object, especially if you want different curves when the animation is going forward vs when it is going backward.

Depending on the given curve, the output of the [CurvedAnimation] could have a wider range than its input. For example, elastic curves such as [Curves.elasticIn] will significantly overshoot or undershoot the default range of 0.0 to 1.0.

If you want to apply a [Curve] to a [Tween], consider using [CurveTween].

A [CurvedAnimation] should be disposed when no longer needed to clean up any listeners that it may have added. Disposing the parent animation (typically the [AnimationController]) will also clean up this object. Do not create a [CurvedAnimation] inside a `build` method because it would leak any added listeners on every rebuild. If [reverseCurve] is not needed, prefer `parent.drive(CurveTween(curve: curve))` which does not require separate disposal.

{@tool snippet}

The following code snippet shows how you can apply a curve to a linear animation produced by an [AnimationController] `controller`.

```dart
final Animation<double> animation = CurvedAnimation(
  parent: controller,
  curve: Curves.ease,
);
```

{@end-tool} {@tool snippet}

This second code snippet shows how to apply a different curve in the forward direction than in the reverse direction. This can't be done using a [CurveTween] (since [Tween]s are not aware of the animation direction when they are applied).

```dart
final Animation<double> animation = CurvedAnimation(
  parent: controller,
  curve: Curves.easeIn,
  reverseCurve: Curves.easeOut,
);
```

{@end-tool}

By default, the [reverseCurve] matches the forward [curve].

See also:

- [CurveTween], for an alternative way of expressing the first sample above.
- [AnimationController], for examples of creating and disposing of an [AnimationController].
- [Curve.flipped] and [FlippedCurve], which provide the reverse of a [Curve].

### CurvedAnimation()

```dart
CurvedAnimation({required Animation<double> parent, required Curve curve, Curve? reverseCurve})
```

Creates a curved animation.

### parent

```dart
Animation<double> parent
```

The animation to which this animation applies a curve.

### curve

```dart
Curve curve
```

The curve to use in the forward direction.

### reverseCurve

```dart
Curve? reverseCurve
```

The curve to use in the reverse direction.

If the parent animation changes direction without first reaching the [AnimationStatus.completed] or [AnimationStatus.dismissed] status, the [CurvedAnimation] stays on the same curve (albeit in the opposite direction) to avoid visual discontinuities.

Because [CurvedAnimation] may add listeners to its parent, it must be created once (for example in [State.initState]) and disposed in [State.dispose]. Do not recreate it on every build as it would leak any added listeners on every rebuild. If [reverseCurve] is not needed, prefer `parent.drive(CurveTween(curve: curve))` which does not require separate disposal.

If this field is null, uses [curve] in both directions.

### isDisposed

```dart
bool isDisposed
```

True if this CurvedAnimation has been disposed.

### dispose()

```dart
void dispose()
```

Cleans up any listeners added by this CurvedAnimation.

### value

```dart
double get value
```

### toString()

```dart
String toString()
```

# TrainHoppingAnimation

```dart
class TrainHoppingAnimation extends Animation<double> with AnimationEagerListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

This animation starts by proxying one animation, but when the value of that animation crosses the value of the second (either because the second is going in the opposite direction, or because the one overtakes the other), the animation hops over to proxying the second animation.

When the [TrainHoppingAnimation] starts proxying the second animation instead of the first, the [onSwitchedTrain] callback is called.

If the two animations start at the same value, then the [TrainHoppingAnimation] immediately hops to the second animation, and the [onSwitchedTrain] callback is not called. If only one animation is provided (i.e. if the second is null), then the [TrainHoppingAnimation] just proxies the first animation.

Since this object must track the two animations even when it has no listeners of its own, instead of shutting down when all its listeners are removed, it exposes a [dispose()] method. Call this method to shut this object down.

### TrainHoppingAnimation()

```dart
TrainHoppingAnimation(Animation<double>? _currentTrain, Animation<double>? _nextTrain, {VoidCallback? onSwitchedTrain})
```

Creates a train-hopping animation.

The current train argument must not be null but the next train argument can be null. If the next train is null, then this object will just proxy the first animation and never hop.

### currentTrain

```dart
Animation<double>? get currentTrain
```

The animation that is currently driving this animation.

The identity of this object will change from the first animation to the second animation when [onSwitchedTrain] is called.

### onSwitchedTrain

```dart
VoidCallback? onSwitchedTrain
```

Called when this animation switches to be driven by the second animation.

This is not called if the two animations provided to the constructor have the same value at the time of the call to the constructor. In that case, the second animation is used from the start, and the first is ignored.

### status

```dart
AnimationStatus get status
```

### value

```dart
double get value
```

### dispose()

```dart
void dispose()
```

Frees all the resources used by this performance. After this is called, this object is no longer usable.

### toString()

```dart
String toString()
```

# CompoundAnimation

```dart
abstract class CompoundAnimation<T> extends Animation<T> with AnimationLazyListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

An interface for combining multiple Animations. Subclasses need only implement the `value` getter to control how the child animations are combined. Can be chained to combine more than 2 animations.

For example, to create an animation that is the sum of two others, subclass this class and define `T get value = first.value + second.value;`

By default, the [status] of a [CompoundAnimation] is the status of the [next] animation if [next] is moving, and the status of the [first] animation otherwise.

### CompoundAnimation()

```dart
CompoundAnimation({required Animation<T> first, required Animation<T> next})
```

Creates a [CompoundAnimation].

Either argument can be a [CompoundAnimation] itself to combine multiple animations.

### first

```dart
Animation<T> first
```

The first sub-animation. Its status takes precedence if neither are animating.

### next

```dart
Animation<T> next
```

The second sub-animation.

### didStartListening()

```dart
void didStartListening()
```

### didStopListening()

```dart
void didStopListening()
```

### status

```dart
AnimationStatus get status
```

Gets the status of this animation based on the [first] and [next] status.

The default is that if the [next] animation is moving, use its status. Otherwise, default to [first].

### toString()

```dart
String toString()
```

# AnimationMean

```dart
class AnimationMean extends CompoundAnimation<double> {}
```

An animation of [double]s that tracks the mean of two other animations.

The [status] of this animation is the status of the `right` animation if it is moving, and the `left` animation otherwise.

The [value] of this animation is the [double] that represents the mean value of the values of the `left` and `right` animations.

### AnimationMean()

```dart
AnimationMean({required Animation<double> left, required Animation<double> right})
```

Creates an animation that tracks the mean of two other animations.

### value

```dart
double get value
```

# AnimationMax

```dart
class AnimationMax<T extends num> extends CompoundAnimation<T> {}
```

An animation that tracks the maximum of two other animations.

The [value] of this animation is the maximum of the values of [first] and [next].

### AnimationMax()

```dart
AnimationMax(Animation<T> first, Animation<T> next)
```

Creates an [AnimationMax].

Either argument can be an [AnimationMax] itself to combine multiple animations.

### value

```dart
T get value
```

# AnimationMin

```dart
class AnimationMin<T extends num> extends CompoundAnimation<T> {}
```

An animation that tracks the minimum of two other animations.

The [value] of this animation is the minimum of the values of [first] and [next].

### AnimationMin()

```dart
AnimationMin(Animation<T> first, Animation<T> next)
```

Creates an [AnimationMin].

Either argument can be an [AnimationMin] itself to combine multiple animations.

### value

```dart
T get value
```
