@docImport 'package:flutter/material.dart';

# AnimatableCallback

```dart
typedef AnimatableCallback<T> = T Function(double value)
```

A typedef used by [Animatable.fromCallback] to create an [Animatable] from a callback.

# Animatable

```dart
abstract class Animatable<T> {}
```

An object that can produce a value of type [T] given an [Animation<double>] as input.

Typically, the values of the input animation are nominally in the range 0.0 to 1.0. In principle, however, any value could be provided.

The main subclass of [Animatable] is [Tween].

### Animatable()

```dart
Animatable()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### Animatable.fromCallback()

```dart
Animatable.fromCallback(AnimatableCallback<T> callback)
```

Create a new [Animatable] from the provided [callback].

See also:

- [Animation.drive], which provides an example for how this can be used.

### transform()

```dart
T transform(double t)
```

Returns the value of the object at point `t`.

The value of `t` is nominally a fraction in the range 0.0 to 1.0, though in practice it may extend outside this range.

See also:

- [evaluate], which is a shorthand for applying [transform] to the value of an [Animation].
- [Curve.transform], a similar method for easing curves.

### evaluate()

```dart
T evaluate(Animation<double> animation)
```

The current value of this object for the given [Animation].

This function is implemented by deferring to [transform]. Subclasses that want to provide custom behavior should override [transform], not [evaluate].

See also:

- [transform], which is similar but takes a `t` value directly instead of an [Animation].
- [animate], which creates an [Animation] out of this object, continually applying [evaluate].

### animate()

```dart
Animation<T> animate(Animation<double> parent)
```

Returns a new [Animation] that is driven by the given animation but that takes on values determined by this object.

Essentially this returns an [Animation] that automatically applies the [evaluate] method to the parent's value.

See also:

- [AnimationController.drive], which does the same thing from the opposite starting point.

### chain()

```dart
Animatable<T> chain(Animatable<double> parent)
```

Returns a new [Animatable] whose value is determined by first evaluating the given parent and then evaluating this object at the result.

This method represents function composition on [transform]: the [transform] method of the returned [Animatable] is the result of composing this object's [transform] method with the given parent's [transform] method.

This allows [Tween]s to be chained before obtaining an [Animation], without allocating an [Animation] for the intermediate result.

# Tween

```dart
class Tween<T extends Object?> extends Animatable<T> {}
```

A linear interpolation between a beginning and ending value.

[Tween] is useful if you want to interpolate across a range.

To use a [Tween] object with an animation, call the [Tween] object's [animate] method and pass it the [Animation] object that you want to modify.

You can chain [Tween] objects together using the [chain] method, producing the function composition of their [transform] methods. Configuring a single [Animation] object by calling [animate] on the resulting [Tween] produces the same result as calling the [animate] method on each [Tween] separately in succession, but more efficiently because it avoids creating [Animation] objects for the intermediate results.

{@tool snippet}

Suppose `_controller` is an [AnimationController], and we want to create an [Animation<Offset>] that is controlled by that controller, and save it in `_animation`. Here are two possible ways of expressing this:

```dart
_animation = _controller.drive(
  Tween<Offset>(
    begin: const Offset(100.0, 50.0),
    end: const Offset(200.0, 300.0),
  ),
);
```

{@end-tool} {@tool snippet}

```dart
_animation = Tween<Offset>(
  begin: const Offset(100.0, 50.0),
  end: const Offset(200.0, 300.0),
).animate(_controller);
```

{@end-tool}

In both cases, the `_animation` variable holds an object that, over the lifetime of the `_controller`'s animation, returns a value (`_animation.value`) that depicts a point along the line between the two offsets above. If we used a [MaterialPointArcTween] instead of a [Tween<Offset>] in the code above, the points would follow a pleasing curve instead of a straight line, with no other changes necessary.

## Performance optimizations

Tweens are mutable; specifically, their [begin] and [end] values can be changed at runtime. An object created with [Animation.drive] using a [Tween] will immediately honor changes to that underlying [Tween] (though the listeners will only be triggered if the [Animation] is actively animating). This can be used to change an animation on the fly without having to recreate all the objects in the chain from the [AnimationController] to the final [Tween].

If a [Tween]'s values are never changed, however, a further optimization can be applied: the object can be stored in a `static final` variable, so that the exact same instance is used whenever the [Tween] is needed. This is preferable to creating an identical [Tween] afresh each time a [State.build] method is called, for example.

## Types with special considerations

Classes with [lerp] static methods typically have corresponding dedicated [Tween] subclasses that call that method. For example, [ColorTween] uses [Color.lerp] to implement the [ColorTween.lerp] method.

Types that define `+` and `-` operators to combine values (`T + T → T` and `T - T → T`) and an `*` operator to scale by multiplying with a double (`T * double → T`) can be directly used with `Tween<T>`.

This does not extend to any type with `+`, `-`, and `*` operators. In particular, [int] does not satisfy this precise contract (`int * double` actually returns [num], not [int]). There are therefore two specific classes that can be used to interpolate integers:

- [IntTween], which is an approximation of a linear interpolation (using [double.round]).
- [StepTween], which uses [double.floor] to ensure that the result is never greater than it would be using if a `Tween<double>`.

The relevant operators on [Size] also don't fulfill this contract, so [SizeTween] uses [Size.lerp].

In addition, some of the types that _do_ have suitable `+`, `-`, and `*` operators still have dedicated [Tween] subclasses that perform the interpolation in a more specialized manner. One such class is [MaterialPointArcTween], which is mentioned above. The [AlignmentTween], and [AlignmentGeometryTween], and [FractionalOffsetTween] are another group of [Tween]s that use dedicated `lerp` methods instead of merely relying on the operators (in particular, this allows them to handle null values in a more useful manner).

## Nullability

The [begin] and [end] fields are nullable; a [Tween] does not have to have non-null values specified when it is created.

If `T` is nullable, then [lerp] and [transform] may return null. This is typically seen in the case where [begin] is null and `t` is 0.0, or [end] is null and `t` is 1.0, or both are null (at any `t` value).

If `T` is not nullable, then [begin] and [end] must both be set to non-null values before using [lerp] or [transform], otherwise they will throw.

## Implementing a Tween

To specialize this class for a new type, the subclass should implement the [lerp] method (and a constructor). The other methods of this class are all defined in terms of [lerp].

### Tween()

```dart
Tween({T? begin, T? end})
```

Creates a tween.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### begin

```dart
T? begin
```

The value this variable has at the beginning of the animation.

See the constructor for details about whether this property may be null (it varies from subclass to subclass).

### end

```dart
T? end
```

The value this variable has at the end of the animation.

See the constructor for details about whether this property may be null (it varies from subclass to subclass).

### lerp()

```dart
T lerp(double t)
```

Returns the value this variable has at the given animation clock value.

The default implementation of this method uses the `+`, `-`, and `*` operators on `T`. The [begin] and [end] properties must therefore be non-null by the time this method is called.

In general, however, it is possible for this to return null, especially when `t`=0.0 and [begin] is null, or `t`=1.0 and [end] is null.

### transform()

```dart
T transform(double t)
```

Returns the interpolated value for the current value of the given animation.

This method returns `begin` and `end` when the animation values are 0.0 or 1.0, respectively.

This function is implemented by deferring to [lerp]. Subclasses that want to provide custom behavior should override [lerp], not [transform] (nor [evaluate]).

See the constructor for details about whether the [begin] and [end] properties may be null when this is called. It varies from subclass to subclass.

### toString()

```dart
String toString()
```

# ReverseTween

```dart
class ReverseTween<T extends Object?> extends Tween<T> {}
```

A [Tween] that evaluates its [parent] in reverse.

### ReverseTween()

```dart
ReverseTween(Tween<T> parent)
```

Construct a [Tween] that evaluates its [parent] in reverse.

### parent

```dart
Tween<T> parent
```

This tween's value is the same as the parent's value evaluated in reverse.

This tween's [begin] is the parent's [end] and its [end] is the parent's [begin]. The [lerp] method returns `parent.lerp(1.0 - t)` and its [evaluate] method is similar.

### lerp()

```dart
T lerp(double t)
```

# ColorTween

```dart
class ColorTween extends Tween<Color?> {}
```

An interpolation between two colors.

This class specializes the interpolation of [Tween<Color>] to use [Color.lerp].

The values can be null, representing no color (which is distinct to transparent black, as represented by [Colors.transparent]).

See [Tween] for a discussion on how to use interpolation objects.

### ColorTween()

```dart
ColorTween({dynamic begin, dynamic end})
```

Creates a [Color] tween.

The [begin] and [end] properties may be null; the null value is treated as transparent.

We recommend that you do not pass [Colors.transparent] as [begin] or [end] if you want the effect of fading in or out of transparent. Instead prefer null. [Colors.transparent] refers to black transparent and thus will fade out of or into black which is likely unwanted.

### lerp()

```dart
Color? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# SizeTween

```dart
class SizeTween extends Tween<Size?> {}
```

An interpolation between two sizes.

This class specializes the interpolation of [Tween<Size>] to use [Size.lerp].

The values can be null, representing [Size.zero].

See [Tween] for a discussion on how to use interpolation objects.

### SizeTween()

```dart
SizeTween({dynamic begin, dynamic end})
```

Creates a [Size] tween.

The [begin] and [end] properties may be null; the null value is treated as an empty size.

### lerp()

```dart
Size? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# RectTween

```dart
class RectTween extends Tween<Rect?> {}
```

An interpolation between two rectangles.

This class specializes the interpolation of [Tween<Rect>] to use [Rect.lerp].

The values can be null, representing a zero-sized rectangle at the origin ([Rect.zero]).

See [Tween] for a discussion on how to use interpolation objects.

### RectTween()

```dart
RectTween({dynamic begin, dynamic end})
```

Creates a [Rect] tween.

The [begin] and [end] properties may be null; the null value is treated as an empty rect at the top left corner.

### lerp()

```dart
Rect? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# IntTween

```dart
class IntTween extends Tween<int> {}
```

An interpolation between two integers that rounds.

This class specializes the interpolation of [Tween<int>] to be appropriate for integers by interpolating between the given begin and end values and then rounding the result to the nearest integer.

This is the closest approximation to a linear tween that is possible with an integer. Compare to [StepTween] and [Tween<double>].

The [begin] and [end] values must be set to non-null values before calling [lerp] or [transform].

See [Tween] for a discussion on how to use interpolation objects.

### IntTween()

```dart
IntTween({int? begin, int? end})
```

Creates an int tween.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### lerp()

```dart
int lerp(double t)
```

# StepTween

```dart
class StepTween extends Tween<int> {}
```

An interpolation between two integers that floors.

This class specializes the interpolation of [Tween<int>] to be appropriate for integers by interpolating between the given begin and end values and then using [double.floor] to return the current integer component, dropping the fractional component.

This results in a value that is never greater than the equivalent value from a linear double interpolation. Compare to [IntTween].

The [begin] and [end] values must be set to non-null values before calling [lerp] or [transform].

See [Tween] for a discussion on how to use interpolation objects.

### StepTween()

```dart
StepTween({int? begin, int? end})
```

Creates an [int] tween that floors.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### lerp()

```dart
int lerp(double t)
```

# ConstantTween

```dart
class ConstantTween<T> extends Tween<T> {}
```

A tween with a constant value.

### ConstantTween()

```dart
ConstantTween(T value)
```

Create a tween whose [begin] and [end] values equal [value].

### lerp()

```dart
T lerp(double t)
```

This tween doesn't interpolate, it always returns the same value.

### toString()

```dart
String toString()
```

# CurveTween

```dart
class CurveTween extends Animatable<double> {}
```

Transforms the value of the given animation by the given curve.

This class differs from [CurvedAnimation] in that [CurvedAnimation] applies a curve to an existing [Animation] object whereas [CurveTween] can be chained with another [Tween] prior to receiving the underlying [Animation]. Unlike [CurvedAnimation], a [CurveTween] does not add listeners or hold state, so it does not need to be disposed.

([CurvedAnimation] also has the additional ability of having different curves when the animation is going forward vs when it is going backward, which can be useful in some scenarios.)

{@tool snippet}

The following code snippet shows how you can apply a curve to a linear animation produced by an [AnimationController] `controller`:

```dart
final Animation<double> animation = _controller.drive(
  CurveTween(curve: Curves.ease),
);
```

{@end-tool}

See also:

- [CurvedAnimation], for an alternative way of expressing the sample above.
- [AnimationController], for examples of creating and disposing of an [AnimationController].

### CurveTween()

```dart
CurveTween({required Curve curve})
```

Creates a curve tween.

### curve

```dart
Curve curve
```

The curve to use when transforming the value of the animation.

### transform()

```dart
double transform(double t)
```

### toString()

```dart
String toString()
```
