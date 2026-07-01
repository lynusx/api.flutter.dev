@docImport 'package:flutter/material.dart';

# ParametricCurve

```dart
abstract class ParametricCurve<T> {}
```

An abstract class providing an interface for evaluating a parametric curve.

A parametric curve transforms a parameter (hence the name) `t` along a curve to the value of the curve at that value of `t`. The curve can be of arbitrary dimension, but is typically a 1D, 2D, or 3D curve.

See also:

- [Curve], a 1D animation easing curve that starts at 0.0 and ends at 1.0.
- [Curve2D], a parametric curve that transforms the parameter to a 2D point.

### ParametricCurve()

```dart
ParametricCurve()
```

Abstract const constructor to enable subclasses to provide const constructors so that they can be used in const expressions.

### transform()

```dart
T transform(double t)
```

Returns the value of the curve at point `t`.

This method asserts that t is between 0 and 1 before delegating to [transformInternal].

It is recommended that subclasses override [transformInternal] instead of this function, as the above case is already handled in the default implementation of [transform], which delegates the remaining logic to [transformInternal].

### transformInternal()

```dart
T transformInternal(double t)
```

Returns the value of the curve at point `t`.

The given parametric value `t` will be between 0.0 and 1.0, inclusive.

### toString()

```dart
String toString()
```

# Curve

```dart
abstract class Curve extends ParametricCurve<double> {}
```

An parametric animation easing curve, i.e. a mapping of the unit interval to the unit interval.

Easing curves are used to adjust the rate of change of an animation over time, allowing them to speed up and slow down, rather than moving at a constant rate.

A [Curve] must map t=0.0 to 0.0 and t=1.0 to 1.0.

See also:

- [Curves], a collection of common animation easing curves.
- [CurveTween], which can be used to apply a [Curve] to an [Animation].
- [Canvas.drawArc], which draws an arc, and has nothing to do with easing curves.
- [Animatable], for a more flexible interface that maps fractions to arbitrary values.

### Curve()

```dart
Curve()
```

Abstract const constructor to enable subclasses to provide const constructors so that they can be used in const expressions.

### transform()

```dart
double transform(double t)
```

Returns the value of the curve at point `t`.

This function must ensure the following:

- The value of `t` must be between 0.0 and 1.0
- Values of `t`=0.0 and `t`=1.0 must be mapped to 0.0 and 1.0, respectively.

It is recommended that subclasses override [transformInternal] instead of this function, as the above cases are already handled in the default implementation of [transform], which delegates the remaining logic to [transformInternal].

### flipped

```dart
Curve get flipped
```

Returns a new curve that is the reversed inversion of this one.

This is often useful with [CurvedAnimation.reverseCurve].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_flipped.mp4}

See also:

- [FlippedCurve], the class that is used to implement this getter.
- [ReverseAnimation], which reverses an [Animation] rather than a [Curve].
- [CurvedAnimation], which can take a separate curve and reverse curve.

# SawTooth

```dart
class SawTooth extends Curve {}
```

A sawtooth curve that repeats a given number of times over the unit interval.

The curve rises linearly from 0.0 to 1.0 and then falls discontinuously back to 0.0 each iteration.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_sawtooth.mp4}

### SawTooth()

```dart
SawTooth(int count)
```

Creates a sawtooth curve.

### count

```dart
int count
```

The number of repetitions of the sawtooth pattern in the unit interval.

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Interval

```dart
class Interval extends Curve {}
```

A curve that is 0.0 until [begin], then curved (according to [curve]) from 0.0 at [begin] to 1.0 at [end], then remains 1.0 past [end].

An [Interval] can be used to delay an animation. For example, a six second animation that uses an [Interval] with its [begin] set to 0.5 and its [end] set to 1.0 will essentially become a three-second animation that starts three seconds later.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_interval.mp4}

### Interval()

```dart
Interval(double begin, double end, {Curve curve = Curves.linear})
```

Creates an interval curve.

### begin

```dart
double begin
```

The largest value for which this interval is 0.0.

From t=0.0 to t=[begin], the interval's value is 0.0.

### end

```dart
double end
```

The smallest value for which this interval is 1.0.

From t=[end] to t=1.0, the interval's value is 1.0.

### curve

```dart
Curve curve
```

The curve to apply between [begin] and [end].

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Split

```dart
class Split extends Curve {}
```

A curve that progresses according to [beginCurve] until [split], then according to [endCurve].

Split curves are useful in situations where a widget must track the user's finger (which requires a linear animation), but can also be flung using a curve specified with the [endCurve] argument, after the finger is released. In such a case, the value of [split] would be the progress of the animation at the time when the finger was released.

For example, if [split] is set to 0.5, [beginCurve] is [Curves.linear], and [endCurve] is [Curves.easeOutCubic], then the bottom-left quarter of the curve will be a straight line, and the top-right quarter will contain the entire [Curves.easeOutCubic] curve.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_split.mp4}

### Split()

```dart
Split(double split, {Curve beginCurve = Curves.linear, Curve endCurve = Curves.easeOutCubic})
```

Creates a split curve.

### split

```dart
double split
```

The progress value separating [beginCurve] from [endCurve].

The value before which the curve progresses according to [beginCurve] and after which the curve progresses according to [endCurve].

When t is exactly `split`, the curve has the value `split`.

Must be between 0 and 1.0, inclusively.

### beginCurve

```dart
Curve beginCurve
```

The curve to use before [split] is reached.

Defaults to [Curves.linear].

### endCurve

```dart
Curve endCurve
```

The curve to use after [split] is reached.

Defaults to [Curves.easeOutCubic].

### transform()

```dart
double transform(double t)
```

### toString()

```dart
String toString()
```

# Threshold

```dart
class Threshold extends Curve {}
```

A curve that is 0.0 until it hits the threshold, then it jumps to 1.0.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_threshold.mp4}

### Threshold()

```dart
Threshold(double threshold)
```

Creates a threshold curve.

### threshold

```dart
double threshold
```

The value before which the curve is 0.0 and after which the curve is 1.0.

When t is exactly [threshold], the curve has the value 1.0.

### transformInternal()

```dart
double transformInternal(double t)
```

# Cubic

```dart
class Cubic extends Curve {}
```

A cubic polynomial mapping of the unit interval.

The [Curves] class contains some commonly used cubic curves:

- [Curves.fastLinearToSlowEaseIn]
- [Curves.ease]
- [Curves.easeIn]
- [Curves.easeInToLinear]
- [Curves.easeInSine]
- [Curves.easeInQuad]
- [Curves.easeInCubic]
- [Curves.easeInQuart]
- [Curves.easeInQuint]
- [Curves.easeInExpo]
- [Curves.easeInCirc]
- [Curves.easeInBack]
- [Curves.easeOut]
- [Curves.linearToEaseOut]
- [Curves.easeOutSine]
- [Curves.easeOutQuad]
- [Curves.easeOutCubic]
- [Curves.easeOutQuart]
- [Curves.easeOutQuint]
- [Curves.easeOutExpo]
- [Curves.easeOutCirc]
- [Curves.easeOutBack]
- [Curves.easeInOut]
- [Curves.easeInOutSine]
- [Curves.easeInOutQuad]
- [Curves.easeInOutCubic]
- [Curves.easeInOutQuart]
- [Curves.easeInOutQuint]
- [Curves.easeInOutExpo]
- [Curves.easeInOutCirc]
- [Curves.easeInOutBack]
- [Curves.fastOutSlowIn]
- [Curves.slowMiddle]

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_linear_to_slow_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_to_linear.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear_to_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4}

The [Cubic] class implements third-order Bézier curves.

See also:

- [Curves], where many more predefined curves are available.
- [CatmullRomCurve], a curve which passes through specific values.

### Cubic()

```dart
Cubic(double a, double b, double c, double d)
```

Creates a cubic curve.

Rather than creating a new instance, consider using one of the common cubic curves in [Curves].

### a

```dart
double a
```

The x coordinate of the first control point.

The line through the point (0, 0) and the first control point is tangent to the curve at the point (0, 0).

### b

```dart
double b
```

The y coordinate of the first control point.

The line through the point (0, 0) and the first control point is tangent to the curve at the point (0, 0).

### c

```dart
double c
```

The x coordinate of the second control point.

The line through the point (1, 1) and the second control point is tangent to the curve at the point (1, 1).

### d

```dart
double d
```

The y coordinate of the second control point.

The line through the point (1, 1) and the second control point is tangent to the curve at the point (1, 1).

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ThreePointCubic

```dart
class ThreePointCubic extends Curve {}
```

A cubic polynomial composed of two curves that share a common center point.

The curve runs through three points: (0,0), the [midpoint], and (1,1).

The [Curves] class contains a curve defined with this class: [Curves.easeInOutCubicEmphasized].

The [ThreePointCubic] class implements third-order Bézier curves, where two curves share an interior [midpoint] that the curve passes through. If the control points surrounding the middle point ([b1], and [a2]) are not collinear with the middle point, then the curve's derivative will have a discontinuity (a cusp) at the shared middle point.

See also:

- [Curves], where many more predefined curves are available.
- [Cubic], which defines a single cubic polynomial.
- [CatmullRomCurve], a curve which passes through specific values.

### ThreePointCubic()

```dart
ThreePointCubic(Offset a1, Offset b1, Offset midpoint, Offset a2, Offset b2)
```

Creates two cubic curves that share a common control point.

Rather than creating a new instance, consider using one of the common three-point cubic curves in [Curves].

The arguments correspond to the control points for the two curves, including the [midpoint], but do not include the two implied end points at (0,0) and (1,1), which are fixed.

### a1

```dart
Offset a1
```

The coordinates of the first control point of the first curve.

The line through the point (0, 0) and this control point is tangent to the curve at the point (0, 0).

### b1

```dart
Offset b1
```

The coordinates of the second control point of the first curve.

The line through the [midpoint] and this control point is tangent to the curve approaching the [midpoint].

### midpoint

```dart
Offset midpoint
```

The coordinates of the middle shared point.

The curve will go through this point. If the control points surrounding this middle point ([b1], and [a2]) are not colinear with this point, then the curve's derivative will have a discontinuity (a cusp) at this point.

### a2

```dart
Offset a2
```

The coordinates of the first control point of the second curve.

The line through the [midpoint] and this control point is tangent to the curve approaching the [midpoint].

### b2

```dart
Offset b2
```

The coordinates of the second control point of the second curve.

The line through the point (1, 1) and this control point is tangent to the curve at (1, 1).

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Curve2D

```dart
abstract class Curve2D extends ParametricCurve<Offset> {}
```

Abstract class that defines an API for evaluating 2D parametric curves.

[Curve2D] differs from [Curve] in that the values interpolated are [Offset] values instead of [double] values, hence the "2D" in the name. They both take a single double `t` that has a range of 0.0 to 1.0, inclusive, as input to the [transform] function . Unlike [Curve], [Curve2D] is not required to map `t=0.0` and `t=1.0` to specific output values.

The interpolated `t` value given to [transform] represents the progression along the curve, but it doesn't necessarily progress at a constant velocity, so incrementing `t` by, say, 0.1 might move along the curve by quite a lot at one part of the curve, or hardly at all in another part of the curve, depending on the definition of the curve.

{@tool dartpad} This example shows how to use a [Curve2D] to modify the position of a widget so that it can follow an arbitrary path.

** See code in examples/api/lib/animation/curves/curve2_d.0.dart ** {@end-tool}

### Curve2D()

```dart
Curve2D()
```

Abstract const constructor to enable subclasses to provide const constructors so that they can be used in const expressions.

### generateSamples()

```dart
Iterable<Curve2DSample> generateSamples({double start = 0.0, double end = 1.0, double tolerance = 1e-10})
```

Generates a list of samples with a recursive subdivision until a tolerance of `tolerance` is reached.

Samples are generated in order.

Samples can be used to render a curve efficiently, since the samples constitute line segments which vary in size with the curvature of the curve. They can also be used to quickly approximate the value of the curve by searching for the desired range in X and linearly interpolating between samples to obtain an approximation of Y at the desired X value. The implementation of [CatmullRomCurve] uses samples for this purpose internally.

The tolerance is computed as the area of a triangle formed by a new point and the preceding and following point.

See also:

- Luiz Henrique de Figueire's Graphics Gem on [the algorithm](http://ariel.chronotext.org/dd/defigueiredo93adaptive.pdf).

### samplingSeed

```dart
int get samplingSeed
```

Returns a seed value used by [generateSamples] to seed a random number generator to avoid sample aliasing.

Subclasses should override this and provide a custom seed.

The value returned should be the same each time it is called, unless the curve definition changes.

### findInverse()

```dart
double findInverse(double x)
```

Returns the parameter `t` that corresponds to the given x value of the spline.

This will only work properly for curves which are single-valued in x (where every value of `x` maps to only one value in 'y', i.e. the curve does not loop or curve back over itself). For curves that are not single-valued, it will return the parameter for only one of the values at the given `x` location.

# Curve2DSample

```dart
class Curve2DSample {}
```

A class that holds a sample of a 2D parametric curve, containing the [value] (the X, Y coordinates) of the curve at the parametric value [t].

See also:

- [Curve2D.generateSamples], which generates samples of this type.
- [Curve2D], a parametric curve that maps a double parameter to a 2D location.

### Curve2DSample()

```dart
Curve2DSample(double t, Offset value)
```

Creates an object that holds a sample; used with [Curve2D] subclasses.

### t

```dart
double t
```

The parametric location of this sample point along the curve.

### value

```dart
Offset value
```

The value (the X, Y coordinates) of the curve at parametric value [t].

### toString()

```dart
String toString()
```

# CatmullRomSpline

```dart
class CatmullRomSpline extends Curve2D {}
```

A 2D spline that passes smoothly through the given control points using a centripetal Catmull-Rom spline.

When the curve is evaluated with [transform], the output values will move smoothly from one control point to the next, passing through the control points.

{@template flutter.animation.CatmullRomSpline} Unlike most cubic splines, Catmull-Rom splines have the advantage that their curves pass through the control points given to them. They are cubic polynomial representations, and, in fact, Catmull-Rom splines can be converted mathematically into cubic splines. This class implements a "centripetal" Catmull-Rom spline. The term centripetal implies that it won't form loops or self-intersections within a single segment. {@endtemplate}

See also:

- [Centripetal Catmull–Rom splines](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline) on Wikipedia.
- [Parameterization and Applications of Catmull-Rom Curves](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf), a paper on using Catmull-Rom splines.
- [CatmullRomCurve], an animation curve that uses a [CatmullRomSpline] as its internal representation.

### CatmullRomSpline()

```dart
CatmullRomSpline(List<Offset> controlPoints, {double tension = 0.0, Offset? startHandle, Offset? endHandle})
```

Constructs a centripetal Catmull-Rom spline curve.

The `controlPoints` argument is a list of four or more points that describe the points that the curve must pass through.

The optional `tension` argument controls how tightly the curve approaches the given `controlPoints`. It must be in the range 0.0 to 1.0, inclusive. It defaults to 0.0, which provides the smoothest curve. A value of 1.0 produces a linear interpolation between points.

The optional `endHandle` and `startHandle` points are the beginning and ending handle positions. If not specified, they are created automatically by extending the line formed by the first and/or last line segment in the `controlPoints`, respectively. The spline will not go through these handle points, but they will affect the slope of the line at the beginning and end of the spline. The spline will attempt to match the slope of the line formed by the start or end handle and the neighboring first or last control point. The default is chosen so that the slope of the line at the ends matches that of the first or last line segment in the control points.

The `controlPoints` list must contain at least four control points to interpolate.

The internal curve data structures are lazily computed the first time [transform] is called. If you would rather pre-compute the structures, use [CatmullRomSpline.precompute] instead.

### CatmullRomSpline.precompute()

```dart
CatmullRomSpline.precompute(List<Offset> controlPoints, {double tension = 0.0, Offset? startHandle, Offset? endHandle})
```

Constructs a centripetal Catmull-Rom spline curve.

The same as [CatmullRomSpline.new], except that the internal data structures are precomputed instead of being computed lazily.

### samplingSeed

```dart
int get samplingSeed
```

### transformInternal()

```dart
Offset transformInternal(double t)
```

# CatmullRomCurve

```dart
class CatmullRomCurve extends Curve {}
```

An animation easing curve that passes smoothly through the given control points using a centripetal Catmull-Rom spline.

When this curve is evaluated with [transform], the values will interpolate smoothly from one control point to the next, passing through (0.0, 0.0), the given points, and then (1.0, 1.0).

{@macro flutter.animation.CatmullRomSpline}

This class uses a centripetal Catmull-Rom curve (a [CatmullRomSpline]) as its internal representation. The term centripetal implies that it won't form loops or self-intersections within a single segment, and corresponds to a Catmull-Rom α (alpha) value of 0.5.

See also:

- [CatmullRomSpline], the 2D spline that this curve uses to generate its values.
- A Wikipedia article on [centripetal Catmull-Rom splines](https://en.wikipedia.org/wiki/Centripetal_Catmull%E2%80%93Rom_spline).
- [CatmullRomCurve.new] for a description of the constraints put on the input control points.
- This [paper on using Catmull-Rom splines](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf).

### CatmullRomCurve()

```dart
CatmullRomCurve(List<Offset> controlPoints, {double tension = 0.0})
```

Constructs a centripetal [CatmullRomCurve].

It takes a list of two or more points that describe the points that the curve must pass through. See [controlPoints] for a description of the restrictions placed on control points. In addition to the given [controlPoints], the curve will begin with an implicit control point at (0.0, 0.0) and end with an implicit control point at (1.0, 1.0), so that the curve begins and ends at those points.

The optional [tension] argument controls how tightly the curve approaches the given `controlPoints`. It must be in the range 0.0 to 1.0, inclusive. It defaults to 0.0, which provides the smoothest curve. A value of 1.0 is equivalent to a linear interpolation between points.

The internal curve data structures are lazily computed the first time [transform] is called. If you would rather pre-compute the curve, use [CatmullRomCurve.precompute] instead.

See also:

- This [paper on using Catmull-Rom splines](http://faculty.cs.tamu.edu/schaefer/research/cr_cad.pdf).

### CatmullRomCurve.precompute()

```dart
CatmullRomCurve.precompute(List<Offset> controlPoints, {double tension = 0.0})
```

Constructs a centripetal [CatmullRomCurve].

Same as [CatmullRomCurve.new], but it precomputes the internal curve data structures for a more predictable computation load.

### controlPoints

```dart
List<Offset> controlPoints
```

The control points used to create this curve.

The `dx` value of each [Offset] in [controlPoints] represents the animation value at which the curve should pass through the `dy` value of the same control point.

The [controlPoints] list must meet the following criteria:

- The list must contain at least two points.
- The X value of each point must be greater than 0.0 and less then 1.0.
- The X values of each point must be greater than the previous point's X value (i.e. monotonically increasing). The Y values are not constrained.
- The resulting spline must be single-valued in X. That is, for each X value, there must be exactly one Y value. This means that the control points must not generated a spline that loops or overlaps itself.

The static function [validateControlPoints] can be used to check that these conditions are met, and will return true if they are. In debug mode, it will also optionally return a list of reasons in text form. In debug mode, the constructor will assert that these conditions are met and print the reasons if the assert fires.

When the curve is evaluated with [transform], the values will interpolate smoothly from one control point to the next, passing through (0.0, 0.0), the given control points, and (1.0, 1.0).

### tension

```dart
double tension
```

The "tension" of the curve.

The [tension] attribute controls how tightly the curve approaches the given [controlPoints]. It must be in the range 0.0 to 1.0, inclusive. It is optional, and defaults to 0.0, which provides the smoothest curve. A value of 1.0 is equivalent to a linear interpolation between control points.

### validateControlPoints()

```dart
bool validateControlPoints(List<Offset>? controlPoints, {double tension = 0.0, List<String>? reasons})
```

Validates that a given set of control points for a [CatmullRomCurve] is well-formed and will not produce a spline that self-intersects.

This method is also used in debug mode to validate a curve to make sure that it won't violate the contract for the [CatmullRomCurve.new] constructor.

If in debug mode, and `reasons` is non-null, this function will fill in `reasons` with descriptions of the problems encountered. The `reasons` argument is ignored in release mode.

In release mode, this function can be used to decide if a proposed modification to the curve will result in a valid curve.

If the first and last points in the samples aren't at (0,0) or (1,1) respectively, then the curve is multi-valued at the ends.

### transformInternal()

```dart
double transformInternal(double t)
```

# FlippedCurve

```dart
class FlippedCurve extends Curve {}
```

A curve that is the reversed inversion of its given curve.

This curve evaluates the given curve in reverse (i.e., from 1.0 to 0.0 as t increases from 0.0 to 1.0) and returns the inverse of the given curve's value (i.e., 1.0 minus the given curve's value).

This is the class used to implement the [flipped] getter on curves.

This is often useful with [CurvedAnimation.reverseCurve].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_flipped.mp4}

See also:

- [Curve.flipped], which provides the [FlippedCurve] of a [Curve].
- [ReverseAnimation], which reverses an [Animation] rather than a [Curve].
- [CurvedAnimation], which can take a separate curve and reverse curve.

### FlippedCurve()

```dart
FlippedCurve(Curve curve)
```

Creates a flipped curve.

### curve

```dart
Curve curve
```

The curve that is being flipped.

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticInCurve

```dart
class ElasticInCurve extends Curve {}
```

An oscillating curve that grows in magnitude while overshooting its bounds.

An instance of this class using the default period of 0.4 is available as [Curves.elasticIn].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4}

### ElasticInCurve()

```dart
ElasticInCurve([double period = 0.4])
```

Creates an elastic-in curve.

Rather than creating a new instance, consider using [Curves.elasticIn].

### period

```dart
double period
```

The duration of the oscillation.

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticOutCurve

```dart
class ElasticOutCurve extends Curve {}
```

An oscillating curve that shrinks in magnitude while overshooting its bounds.

An instance of this class using the default period of 0.4 is available as [Curves.elasticOut].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4}

### ElasticOutCurve()

```dart
ElasticOutCurve([double period = 0.4])
```

Creates an elastic-out curve.

Rather than creating a new instance, consider using [Curves.elasticOut].

### period

```dart
double period
```

The duration of the oscillation.

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# ElasticInOutCurve

```dart
class ElasticInOutCurve extends Curve {}
```

An oscillating curve that grows and then shrinks in magnitude while overshooting its bounds.

An instance of this class using the default period of 0.4 is available as [Curves.elasticInOut].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4}

### ElasticInOutCurve()

```dart
ElasticInOutCurve([double period = 0.4])
```

Creates an elastic-in-out curve.

Rather than creating a new instance, consider using [Curves.elasticInOut].

### period

```dart
double period
```

The duration of the oscillation.

### transformInternal()

```dart
double transformInternal(double t)
```

### toString()

```dart
String toString()
```

# Curves

```dart
abstract final class Curves {}
```

A collection of common animation curves.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_decelerate.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4} {@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear.mp4}

See also:

- [Curve], the interface implemented by the constants available from the [Curves] class.
- [Easing], for the Material animation curves.

### linear

```dart
Curve linear
```

A linear animation curve.

This is the identity map over the unit interval: its [Curve.transform] method returns its input unmodified. This is useful as a default curve for cases where a [Curve] is required but no actual curve is desired.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear.mp4}

### decelerate

```dart
Curve decelerate
```

A curve where the rate of change starts out quickly and then decelerates; an upside-down `f(t) = t²` parabola.

This is equivalent to the Android `DecelerateInterpolator` class with a unit factor (the default factor).

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_decelerate.mp4}

### fastLinearToSlowEaseIn

```dart
Cubic fastLinearToSlowEaseIn
```

A curve that is very steep and linear at the beginning, but quickly flattens out and very slowly eases in.

By default is the curve used to animate pages on iOS back to their original position if a swipe gesture is ended midway through a swipe.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_linear_to_slow_ease_in.mp4}

### fastEaseInToSlowEaseOut

```dart
ThreePointCubic fastEaseInToSlowEaseOut
```

A curve that starts slowly, speeds up very quickly, and then ends slowly.

This curve is used by default to animate page transitions used by [CupertinoPageRoute].

It has been derived from plots of native iOS 16.3 animation frames on iPhone 14 Pro Max. Specifically, transition animation positions were measured every frame and plotted against time. Then, a cubic curve was strictly fit to the measured data points.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_ease_in_to_slow_ease_out.mp4}

### ease

```dart
Cubic ease
```

A cubic animation curve that speeds up quickly and ends slowly.

This is the same as the CSS easing function `ease`.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease.mp4}

### easeIn

```dart
Cubic easeIn
```

A cubic animation curve that starts slowly and ends quickly.

This is the same as the CSS easing function `ease-in`.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in.mp4}

### easeInToLinear

```dart
Cubic easeInToLinear
```

A cubic animation curve that starts slowly and ends linearly.

The symmetric animation to [linearToEaseOut].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_to_linear.mp4}

### easeInSine

```dart
Cubic easeInSine
```

A cubic animation curve that starts slowly and ends quickly. This is similar to [Curves.easeIn], but with sinusoidal easing for a slightly less abrupt beginning and end. Nonetheless, the result is quite gentle and is hard to distinguish from [Curves.linear] at a glance.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_sine.mp4}

### easeInQuad

```dart
Cubic easeInQuad
```

A cubic animation curve that starts slowly and ends quickly. Based on a quadratic equation where `f(t) = t²`, this is effectively the inverse of [Curves.decelerate].

Compared to [Curves.easeInSine], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quad.mp4}

### easeInCubic

```dart
Cubic easeInCubic
```

A cubic animation curve that starts slowly and ends quickly. This curve is based on a cubic equation where `f(t) = t³`. The result is a safe sweet spot when choosing a curve for widgets animating off the viewport.

Compared to [Curves.easeInQuad], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_cubic.mp4}

### easeInQuart

```dart
Cubic easeInQuart
```

A cubic animation curve that starts slowly and ends quickly. This curve is based on a quartic equation where `f(t) = t⁴`.

Animations using this curve or steeper curves will benefit from a longer duration to avoid motion feeling unnatural.

Compared to [Curves.easeInCubic], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quart.mp4}

### easeInQuint

```dart
Cubic easeInQuint
```

A cubic animation curve that starts slowly and ends quickly. This curve is based on a quintic equation where `f(t) = t⁵`.

Compared to [Curves.easeInQuart], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_quint.mp4}

### easeInExpo

```dart
Cubic easeInExpo
```

A cubic animation curve that starts slowly and ends quickly. This curve is based on an exponential equation where `f(t) = 2¹⁰⁽ᵗ⁻¹⁾`.

Using this curve can give your animations extra flare, but a longer duration may need to be used to compensate for the steepness of the curve.

Compared to [Curves.easeInQuint], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_expo.mp4}

### easeInCirc

```dart
Cubic easeInCirc
```

A cubic animation curve that starts slowly and ends quickly. This curve is effectively the bottom-right quarter of a circle.

Like [Curves.easeInExpo], this curve is fairly dramatic and will reduce the clarity of an animation if not given a longer duration.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_circ.mp4}

### easeInBack

```dart
Cubic easeInBack
```

A cubic animation curve that starts slowly and ends quickly. This curve is similar to [Curves.elasticIn] in that it overshoots its bounds before reaching its end. Instead of repeated swinging motions before ascending, though, this curve overshoots once, then continues to ascend.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_back.mp4}

### easeOut

```dart
Cubic easeOut
```

A cubic animation curve that starts quickly and ends slowly.

This is the same as the CSS easing function `ease-out`.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out.mp4}

### linearToEaseOut

```dart
Cubic linearToEaseOut
```

A cubic animation curve that starts linearly and ends slowly.

A symmetric animation to [easeInToLinear].

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_linear_to_ease_out.mp4}

### easeOutSine

```dart
Cubic easeOutSine
```

A cubic animation curve that starts quickly and ends slowly. This is similar to [Curves.easeOut], but with sinusoidal easing for a slightly less abrupt beginning and end. Nonetheless, the result is quite gentle and is hard to distinguish from [Curves.linear] at a glance.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_sine.mp4}

### easeOutQuad

```dart
Cubic easeOutQuad
```

A cubic animation curve that starts quickly and ends slowly. This is effectively the same as [Curves.decelerate], only simulated using a cubic bezier function.

Compared to [Curves.easeOutSine], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quad.mp4}

### easeOutCubic

```dart
Cubic easeOutCubic
```

A cubic animation curve that starts quickly and ends slowly. This curve is a flipped version of [Curves.easeInCubic].

The result is a safe sweet spot when choosing a curve for animating a widget's position entering or already inside the viewport.

Compared to [Curves.easeOutQuad], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4}

### easeOutQuart

```dart
Cubic easeOutQuart
```

A cubic animation curve that starts quickly and ends slowly. This curve is a flipped version of [Curves.easeInQuart].

Animations using this curve or steeper curves will benefit from a longer duration to avoid motion feeling unnatural.

Compared to [Curves.easeOutCubic], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quart.mp4}

### easeOutQuint

```dart
Cubic easeOutQuint
```

A cubic animation curve that starts quickly and ends slowly. This curve is a flipped version of [Curves.easeInQuint].

Compared to [Curves.easeOutQuart], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_quint.mp4}

### easeOutExpo

```dart
Cubic easeOutExpo
```

A cubic animation curve that starts quickly and ends slowly. This curve is a flipped version of [Curves.easeInExpo]. Using this curve can give your animations extra flare, but a longer duration may need to be used to compensate for the steepness of the curve.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_expo.mp4}

### easeOutCirc

```dart
Cubic easeOutCirc
```

A cubic animation curve that starts quickly and ends slowly. This curve is effectively the top-left quarter of a circle.

Like [Curves.easeOutExpo], this curve is fairly dramatic and will reduce the clarity of an animation if not given a longer duration.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_circ.mp4}

### easeOutBack

```dart
Cubic easeOutBack
```

A cubic animation curve that starts quickly and ends slowly. This curve is similar to [Curves.elasticOut] in that it overshoots its bounds before reaching its end. Instead of repeated swinging motions after ascending, though, this curve only overshoots once.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_back.mp4}

### easeInOut

```dart
Cubic easeInOut
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly.

This is the same as the CSS easing function `ease-in-out`.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out.mp4}

### easeInOutSine

```dart
Cubic easeInOutSine
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This is similar to [Curves.easeInOut], but with sinusoidal easing for a slightly less abrupt beginning and end.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_sine.mp4}

### easeInOutQuad

```dart
Cubic easeInOutQuad
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInQuad] as the first half, and [Curves.easeOutQuad] as the second.

Compared to [Curves.easeInOutSine], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quad.mp4}

### easeInOutCubic

```dart
Cubic easeInOutCubic
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInCubic] as the first half, and [Curves.easeOutCubic] as the second.

The result is a safe sweet spot when choosing a curve for a widget whose initial and final positions are both within the viewport.

Compared to [Curves.easeInOutQuad], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic.mp4}

### easeInOutCubicEmphasized

```dart
ThreePointCubic easeInOutCubicEmphasized
```

A cubic animation curve that starts slowly, speeds up shortly thereafter, and then ends slowly. This curve can be imagined as a steeper version of [easeInOutCubic].

The result is a more emphasized eased curve when choosing a curve for a widget whose initial and final positions are both within the viewport.

Compared to [Curves.easeInOutCubic], this curve is slightly steeper.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_cubic_emphasized.mp4}

### easeInOutQuart

```dart
Cubic easeInOutQuart
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInQuart] as the first half, and [Curves.easeOutQuart] as the second.

Animations using this curve or steeper curves will benefit from a longer duration to avoid motion feeling unnatural.

Compared to [Curves.easeInOutCubic], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quart.mp4}

### easeInOutQuint

```dart
Cubic easeInOutQuint
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInQuint] as the first half, and [Curves.easeOutQuint] as the second.

Compared to [Curves.easeInOutQuart], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_quint.mp4}

### easeInOutExpo

```dart
Cubic easeInOutExpo
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly.

Since this curve is arrived at with an exponential function, the midpoint is exceptionally steep. Extra consideration should be taken when designing an animation using this.

Compared to [Curves.easeInOutQuint], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_expo.mp4}

### easeInOutCirc

```dart
Cubic easeInOutCirc
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInCirc] as the first half, and [Curves.easeOutCirc] as the second.

Like [Curves.easeInOutExpo], this curve is fairly dramatic and will reduce the clarity of an animation if not given a longer duration.

Compared to [Curves.easeInOutExpo], this curve is slightly steeper.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_circ.mp4}

### easeInOutBack

```dart
Cubic easeInOutBack
```

A cubic animation curve that starts slowly, speeds up, and then ends slowly. This curve can be imagined as [Curves.easeInBack] as the first half, and [Curves.easeOutBack] as the second.

Since two curves are used as a basis for this curve, the resulting animation will overshoot its bounds twice before reaching its end - first by exceeding its lower bound, then exceeding its upper bound and finally descending to its final position.

Derived from Robert Penner’s easing functions.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_in_out_back.mp4}

### fastOutSlowIn

```dart
Cubic fastOutSlowIn
```

A curve that starts quickly and eases into its final position.

Over the course of the animation, the object spends more time near its final destination. As a result, the user isn’t left waiting for the animation to finish, and the negative effects of motion are minimized.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_fast_out_slow_in.mp4}

See also:

- [Easing.legacy], the name for this curve in the Material specification.

### slowMiddle

```dart
Cubic slowMiddle
```

A cubic animation curve that starts quickly, slows down, and then ends quickly.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_slow_middle.mp4}

### bounceIn

```dart
Curve bounceIn
```

An oscillating curve that grows in magnitude.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in.mp4}

### bounceOut

```dart
Curve bounceOut
```

An oscillating curve that first grows and then shrink in magnitude.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_out.mp4}

### bounceInOut

```dart
Curve bounceInOut
```

An oscillating curve that first grows and then shrink in magnitude.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_bounce_in_out.mp4}

### elasticIn

```dart
ElasticInCurve elasticIn
```

An oscillating curve that grows in magnitude while overshooting its bounds.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in.mp4}

### elasticOut

```dart
ElasticOutCurve elasticOut
```

An oscillating curve that shrinks in magnitude while overshooting its bounds.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_out.mp4}

### elasticInOut

```dart
ElasticInOutCurve elasticInOut
```

An oscillating curve that grows and then shrinks in magnitude while overshooting its bounds.

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_elastic_in_out.mp4}
