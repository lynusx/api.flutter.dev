@docImport 'package:flutter/material.dart';

@docImport 'box_decoration.dart';

# GradientTransform

```dart
abstract class GradientTransform {}
```

Base class for transforming gradient shaders without applying the same transform to the entire canvas.

For example, a [SweepGradient] normally starts its gradation at 3 o'clock and draws clockwise. To have the sweep appear to start at 6 o'clock, supply a [GradientRotation] of `pi/4` radians (i.e. 45 degrees).

### GradientTransform()

```dart
GradientTransform()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### transform()

```dart
Matrix4? transform(Rect bounds, {TextDirection? textDirection})
```

When a [Gradient] creates its [Shader], it will call this method to determine what transform to apply to the shader for the given [Rect] and [TextDirection].

Implementers may return null from this method, which achieves the same final effect as returning [Matrix4.identity].

# GradientRotation

```dart
class GradientRotation extends GradientTransform {}
```

A [GradientTransform] that rotates the gradient around the center-point of its bounding box.

{@tool snippet}

This sample would rotate a sweep gradient by a quarter turn clockwise:

```dart
const SweepGradient gradient = SweepGradient(
  colors: <Color>[Color(0xFFFFFFFF), Color(0xFF009900)],
  transform: GradientRotation(math.pi/4),
);
```

{@end-tool}

### GradientRotation()

```dart
GradientRotation(double radians)
```

Constructs a [GradientRotation] for the specified angle.

The angle is in radians in the clockwise direction.

### radians

```dart
double radians
```

The angle of rotation in radians in the clockwise direction.

### transform()

```dart
Matrix4 transform(Rect bounds, {TextDirection? textDirection})
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Gradient

```dart
abstract class Gradient {}
```

A 2D gradient.

This is an interface that allows [LinearGradient], [RadialGradient], and [SweepGradient] classes to be used interchangeably in [BoxDecoration]s.

See also:

- [Gradient](dart-ui/Gradient-class.html), the class in the [dart:ui] library.

### Gradient()

```dart
Gradient({required List<Color> colors, List<double>? stops, GradientTransform? transform})
```

Initialize the gradient's colors and stops.

The [colors] argument must have at least two colors (the length is not verified until the [createShader] method is called).

If specified, the [stops] argument must have the same number of entries as [colors] (this is also not verified until the [createShader] method is called).

The [transform] argument can be applied to transform _only_ the gradient, without rotating the canvas itself or other geometry on the canvas. For example, a `GradientRotation(math.pi/4)` will result in a [SweepGradient] that starts from a position of 6 o'clock instead of 3 o'clock, assuming no other rotation or perspective transformations have been applied to the [Canvas]. If null, no transformation is applied.

### colors

```dart
List<Color> colors
```

The colors the gradient should obtain at each of the stops.

If [stops] is non-null, this list must have the same length as [stops].

This list must have at least two colors in it (otherwise, it's not a gradient!).

### stops

```dart
List<double>? stops
```

A list of values from 0.0 to 1.0 that denote fractions along the gradient.

If non-null, this list must have the same length as [colors].

If the first value is not 0.0, then a stop with position 0.0 and a color equal to the first color in [colors] is implied.

If the last value is not 1.0, then a stop with position 1.0 and a color equal to the last color in [colors] is implied.

The values in the [stops] list must be in ascending order. If a value in the [stops] list is less than an earlier value in the list, then its value is assumed to equal the previous value.

If stops is null, then a set of uniformly distributed stops is implied, with the first stop at 0.0 and the last stop at 1.0.

### transform

```dart
GradientTransform? transform
```

The transform, if any, to apply to the gradient.

This transform is in addition to any other transformations applied to the canvas, but does not add any transformations to the canvas.

### createShader()

```dart
Shader createShader(Rect rect, {TextDirection? textDirection})
```

Creates a [Shader] for this gradient to fill the given rect.

If the gradient's configuration is text-direction-dependent, for example it uses [AlignmentDirectional] objects instead of [Alignment] objects, then the `textDirection` argument must not be null.

The shader's transform will be resolved from the [transform] of this gradient.

### scale()

```dart
Gradient scale(double factor)
```

Returns a new gradient with its properties scaled by the given factor.

A factor of 0.0 (or less) should result in a variant of the gradient that is invisible; any two factors epsilon apart should be unnoticeably different from each other at first glance. From this it follows that scaling a gradient with values from 1.0 to 0.0 over time should cause the gradient to smoothly disappear.

Typically this is the same as interpolating from null (with [lerp]).

### withOpacity()

```dart
Gradient withOpacity(double opacity)
```

Returns a new [Gradient] with each color set to the given opacity.

### fromColor()

```dart
Gradient fromColor(Color color)
```

Returns a copy of this gradient with all of its [colors] replaced by the given `color`.

The geometry of the gradient (such as its [stops] and the subclass-specific positioning) is preserved, so the result paints as a uniform `color`. This is useful to represent a solid color as a gradient, for example when interpolating between a color and a gradient with [lerp].

Subclasses should override this method to preserve their own geometry. The base implementation returns a [LinearGradient]; this is sufficient because a gradient with uniform colors paints as a solid color regardless of its geometry.

### lerpFrom()

```dart
Gradient? lerpFrom(Gradient? a, double t)
```

Linearly interpolates from another [Gradient] to `this`.

When implementing this method in subclasses, return null if this class cannot interpolate from `a`. In that case, [lerp] will try `a`'s [lerpTo] method instead.

If `a` is null, this must not return null. The base class implements this by deferring to [scale].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `this` (or something equivalent to `this`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `this`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

Instead of calling this directly, use [Gradient.lerp].

### lerpTo()

```dart
Gradient? lerpTo(Gradient? b, double t)
```

Linearly interpolates from `this` to another [Gradient].

This is called if `b`'s [lerpTo] did not know how to handle this class.

When implementing this method in subclasses, return null if this class cannot interpolate from `b`. In that case, [lerp] will apply a default behavior instead.

If `b` is null, this must not return null. The base class implements this by deferring to [scale].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `this` (or something equivalent to `this`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `this` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

Instead of calling this directly, use [Gradient.lerp].

### lerp()

```dart
Gradient? lerp(Gradient? a, Gradient? b, double t)
```

Linearly interpolates between two [Gradient]s.

This defers to `b`'s [lerpTo] function if `b` is not null. If `b` is null or if its [lerpTo] returns null, it uses `a`'s [lerpFrom] function instead. If both return null, it returns `a` before `t == 0.5` and `b` after `t == 0.5`.

{@macro dart.ui.shadow.lerp}

# LinearGradient

```dart
class LinearGradient extends Gradient {}
```

A 2D linear gradient.

{@youtube 560 315 https://www.youtube.com/watch?v=gYNTcgZVcWw}

This class is used by [BoxDecoration] to represent linear gradients. This abstracts out the arguments to the [ui.Gradient.linear] constructor from the `dart:ui` library.

A gradient has two anchor points, [begin] and [end]. The [begin] point corresponds to 0.0, and the [end] point corresponds to 1.0. These points are expressed in fractions, so that the same gradient can be reused with varying sized boxes without changing the parameters. (This contrasts with [ ui.Gradient.linear], whose arguments are expressed in logical pixels.)

The [colors] are described by a list of [Color] objects. There must be at least two colors. The [stops] list, if specified, must have the same length as [colors]. It specifies fractions of the vector from start to end, between 0.0 and 1.0, for each color. If it is null, a uniform distribution is assumed.

The region of the canvas before [begin] and after [end] is colored according to [tileMode].

Typically this class is used with [BoxDecoration], which does the painting. To use a [LinearGradient] to paint on a canvas directly, see [createShader].

{@tool dartpad} This sample draws a picture with a gradient sweeping through different colors, by having a [Container] display a [BoxDecoration] with a [LinearGradient].

** See code in examples/api/lib/painting/gradient/linear_gradient.0.dart ** {@end-tool}

See also:

- [RadialGradient], which displays a gradient in concentric circles, and has an example which shows a different way to use [Gradient] objects.
- [SweepGradient], which displays a gradient in a sweeping arc around a center point.
- [BoxDecoration], which can take a [LinearGradient] in its [BoxDecoration.gradient] property.

### LinearGradient()

```dart
LinearGradient({AlignmentGeometry begin = Alignment.centerLeft, AlignmentGeometry end = Alignment.centerRight, required List<InvalidType> colors, List<double>? stops, TileMode tileMode = TileMode.clamp, GradientTransform? transform})
```

Creates a linear gradient.

If [stops] is non-null, it must have the same length as [colors].

### begin

```dart
AlignmentGeometry begin
```

The offset at which stop 0.0 of the gradient is placed.

If this is an [Alignment], then it is expressed as a vector from coordinate (0.0, 0.0), in a coordinate space that maps the center of the paint box at (0.0, 0.0) and the bottom right at (1.0, 1.0).

For example, a begin offset of (-1.0, 0.0) is half way down the left side of the box.

It can also be an [AlignmentDirectional], where the start is the left in left-to-right contexts and the right in right-to-left contexts. If a text-direction-dependent value is provided here, then the [createShader] method will need to be given a [TextDirection].

### end

```dart
AlignmentGeometry end
```

The offset at which stop 1.0 of the gradient is placed.

If this is an [Alignment], then it is expressed as a vector from coordinate (0.0, 0.0), in a coordinate space that maps the center of the paint box at (0.0, 0.0) and the bottom right at (1.0, 1.0).

For example, a begin offset of (1.0, 0.0) is half way down the right side of the box.

It can also be an [AlignmentDirectional], where the start is the left in left-to-right contexts and the right in right-to-left contexts. If a text-direction-dependent value is provided here, then the [createShader] method will need to be given a [TextDirection].

### tileMode

```dart
TileMode tileMode
```

How this gradient should tile the plane beyond in the region before [begin] and after [end].

For details, see [TileMode].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_linear.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_linear.png)

### createShader()

```dart
Shader createShader(Rect rect, {TextDirection? textDirection})
```

### scale()

```dart
LinearGradient scale(double factor)
```

Returns a new [LinearGradient] with its colors scaled by the given factor.

Since the alpha component of the Color is what is scaled, a factor of 0.0 or less results in a gradient that is fully transparent.

### fromColor()

```dart
LinearGradient fromColor(Color color)
```

### lerpFrom()

```dart
Gradient? lerpFrom(Gradient? a, double t)
```

### lerpTo()

```dart
Gradient? lerpTo(Gradient? b, double t)
```

### lerp()

```dart
LinearGradient? lerp(LinearGradient? a, LinearGradient? b, double t)
```

Linearly interpolate between two [LinearGradient]s.

If either gradient is null, this function linearly interpolates from a gradient that matches the other gradient in [begin], [end], [stops] and [tileMode] and with the same [colors] but transparent (using [scale]).

If neither gradient is null, they must have the same number of [colors].

The `t` argument represents a position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

### withOpacity()

```dart
LinearGradient withOpacity(double opacity)
```

# RadialGradient

```dart
class RadialGradient extends Gradient {}
```

A 2D radial gradient.

This class is used by [BoxDecoration] to represent radial gradients. This abstracts out the arguments to the [ui.Gradient.radial] constructor from the `dart:ui` library.

A normal radial gradient has a [center] and a [radius]. The [center] point corresponds to 0.0, and the ring at [radius] from the center corresponds to 1.0. These lengths are expressed in fractions, so that the same gradient can be reused with varying sized boxes without changing the parameters. (This contrasts with [ui.Gradient.radial], whose arguments are expressed in logical pixels.)

It is also possible to create a two-point (or focal pointed) radial gradient (which is sometimes referred to as a two point conic gradient, but is not the same as a CSS conic gradient which corresponds to a [SweepGradient]). A [focal] point and [focalRadius] can be specified similarly to [center] and [radius], which will make the rendered gradient appear to be pointed or directed in the direction of the [focal] point. This is only important if [focal] and [center] are not equal or [focalRadius] > 0.0 (as this case is visually identical to a normal radial gradient). One important case to avoid is having [focal] and [center] both resolve to [Offset.zero] when [focalRadius] > 0.0. In such a case, a valid shader cannot be created by the framework.

The [colors] are described by a list of [Color] objects. There must be at least two colors. The [stops] list, if specified, must have the same length as [colors]. It specifies fractions of the radius between 0.0 and 1.0, giving concentric rings for each color stop. If it is null, a uniform distribution is assumed.

The region of the canvas beyond [radius] from the [center] is colored according to [tileMode].

Typically this class is used with [BoxDecoration], which does the painting. To use a [RadialGradient] to paint on a canvas directly, see [createShader].

{@tool snippet}

This function draws a gradient that looks like a sun in a blue sky.

```dart
void paintSky(Canvas canvas, Rect rect) {
  const RadialGradient gradient = RadialGradient(
    center: Alignment(0.7, -0.6), // near the top right
    radius: 0.2,
    colors: <Color>[
      Color(0xFFFFFF00), // yellow sun
      Color(0xFF0099FF), // blue sky
    ],
    stops: <double>[0.4, 1.0],
  );
  // rect is the area we are painting over
  final Paint paint = Paint()
    ..shader = gradient.createShader(rect);
  canvas.drawRect(rect, paint);
}
```

{@end-tool}

See also:

- [LinearGradient], which displays a gradient in parallel lines, and has an example which shows a different way to use [Gradient] objects.
- [SweepGradient], which displays a gradient in a sweeping arc around a center point.
- [BoxDecoration], which can take a [RadialGradient] in its [BoxDecoration.gradient] property.
- [CustomPainter], which shows how to use the above sample code in a custom painter.

### RadialGradient()

```dart
RadialGradient({AlignmentGeometry center = Alignment.center, double radius = 0.5, required List<InvalidType> colors, List<double>? stops, TileMode tileMode = TileMode.clamp, AlignmentGeometry? focal, double focalRadius = 0.0, GradientTransform? transform})
```

Creates a radial gradient.

If [stops] is non-null, it must have the same length as [colors].

### center

```dart
AlignmentGeometry center
```

The center of the gradient, as an offset into the (-1.0, -1.0) x (1.0, 1.0) square describing the gradient which will be mapped onto the paint box.

For example, an alignment of (0.0, 0.0) will place the radial gradient in the center of the box.

If this is an [Alignment], then it is expressed as a vector from coordinate (0.0, 0.0), in a coordinate space that maps the center of the paint box at (0.0, 0.0) and the bottom right at (1.0, 1.0).

It can also be an [AlignmentDirectional], where the start is the left in left-to-right contexts and the right in right-to-left contexts. If a text-direction-dependent value is provided here, then the [createShader] method will need to be given a [TextDirection].

### radius

```dart
double radius
```

The radius of the gradient, as a fraction of the shortest side of the paint box.

For example, if a radial gradient is painted on a box that is 100.0 pixels wide and 200.0 pixels tall, then a radius of 1.0 will place the 1.0 stop at 100.0 pixels from the [center].

### tileMode

```dart
TileMode tileMode
```

How this gradient should tile the plane beyond the outer ring at [radius] pixels from the [center].

For details, see [TileMode].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radial.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radial.png)

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_radialWithFocal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_radialWithFocal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_radialWithFocal.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_radialWithFocal.png)

### focal

```dart
AlignmentGeometry? focal
```

The focal point of the gradient. If specified, the gradient will appear to be focused along the vector from [center] to focal.

See [center] for a description of how the coordinates are mapped.

If this value is specified and [focalRadius] > 0.0, care should be taken to ensure that either this value or [center] will not both resolve to [Offset.zero], which would fail to create a valid gradient.

### focalRadius

```dart
double focalRadius
```

The radius of the focal point of gradient, as a fraction of the shortest side of the paint box.

For example, if a radial gradient is painted on a box that is 100.0 pixels wide and 200.0 pixels tall, then a radius of 1.0 will place the 1.0 stop at 100.0 pixels from the [focal] point.

If this value is specified and is greater than 0.0, either [focal] or [center] must not resolve to [Offset.zero], which would fail to create a valid gradient.

### createShader()

```dart
Shader createShader(Rect rect, {TextDirection? textDirection})
```

### scale()

```dart
RadialGradient scale(double factor)
```

Returns a new [RadialGradient] with its colors scaled by the given factor.

Since the alpha component of the Color is what is scaled, a factor of 0.0 or less results in a gradient that is fully transparent.

### fromColor()

```dart
RadialGradient fromColor(Color color)
```

### lerpFrom()

```dart
Gradient? lerpFrom(Gradient? a, double t)
```

### lerpTo()

```dart
Gradient? lerpTo(Gradient? b, double t)
```

### lerp()

```dart
RadialGradient? lerp(RadialGradient? a, RadialGradient? b, double t)
```

Linearly interpolate between two [RadialGradient]s.

If either gradient is null, this function linearly interpolates from a gradient that matches the other gradient in [center], [radius], [stops] and [tileMode] and with the same [colors] but transparent (using [scale]).

If neither gradient is null, they must have the same number of [colors].

The `t` argument represents a position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

### withOpacity()

```dart
RadialGradient withOpacity(double opacity)
```

# SweepGradient

```dart
class SweepGradient extends Gradient {}
```

A 2D sweep gradient.

This class is used by [BoxDecoration] to represent sweep gradients. This abstracts out the arguments to the [ui.Gradient.sweep] constructor from the `dart:ui` library.

A gradient has a [center], a [startAngle], and an [endAngle]. The [startAngle] corresponds to 0.0, and the [endAngle] corresponds to 1.0. These angles are expressed in radians.

The [colors] are described by a list of [Color] objects. There must be at least two colors. The [stops] list, if specified, must have the same length as [colors]. It specifies fractions of the vector from start to end, between 0.0 and 1.0, for each color. If it is null, a uniform distribution is assumed.

The region of the canvas before [startAngle] and after [endAngle] is colored according to [tileMode].

Typically this class is used with [BoxDecoration], which does the painting. To use a [SweepGradient] to paint on a canvas directly, see [createShader].

{@tool snippet}

This sample draws a different color in each quadrant.

```dart
Container(
  decoration: const BoxDecoration(
    gradient: SweepGradient(
      center: FractionalOffset.center,
      colors: <Color>[
        Color(0xFF4285F4), // blue
        Color(0xFF34A853), // green
        Color(0xFFFBBC05), // yellow
        Color(0xFFEA4335), // red
        Color(0xFF4285F4), // blue again to seamlessly transition to the start
      ],
      stops: <double>[0.0, 0.25, 0.5, 0.75, 1.0],
    ),
  )
)
```

{@end-tool}

{@tool snippet}

This sample takes the above gradient and rotates it by `math.pi/4` radians, i.e. 45 degrees.

```dart
Container(
  decoration: const BoxDecoration(
    gradient: SweepGradient(
      center: FractionalOffset.center,
      colors: <Color>[
        Color(0xFF4285F4), // blue
        Color(0xFF34A853), // green
        Color(0xFFFBBC05), // yellow
        Color(0xFFEA4335), // red
        Color(0xFF4285F4), // blue again to seamlessly transition to the start
      ],
      stops: <double>[0.0, 0.25, 0.5, 0.75, 1.0],
      transform: GradientRotation(math.pi/4),
    ),
  ),
)
```

{@end-tool}

See also:

- [LinearGradient], which displays a gradient in parallel lines, and has an example which shows a different way to use [Gradient] objects.
- [RadialGradient], which displays a gradient in concentric circles, and has an example which shows a different way to use [Gradient] objects.
- [BoxDecoration], which can take a [SweepGradient] in its [BoxDecoration.gradient] property.

### SweepGradient()

```dart
SweepGradient({AlignmentGeometry center = Alignment.center, double startAngle = 0.0, double endAngle = math.pi * 2, required List<InvalidType> colors, List<double>? stops, TileMode tileMode = TileMode.clamp, GradientTransform? transform})
```

Creates a sweep gradient.

If [stops] is non-null, it must have the same length as [colors].

### center

```dart
AlignmentGeometry center
```

The center of the gradient, as an offset into the (-1.0, -1.0) x (1.0, 1.0) square describing the gradient which will be mapped onto the paint box.

For example, an alignment of (0.0, 0.0) will place the sweep gradient in the center of the box.

If this is an [Alignment], then it is expressed as a vector from coordinate (0.0, 0.0), in a coordinate space that maps the center of the paint box at (0.0, 0.0) and the bottom right at (1.0, 1.0).

It can also be an [AlignmentDirectional], where the start is the left in left-to-right contexts and the right in right-to-left contexts. If a text-direction-dependent value is provided here, then the [createShader] method will need to be given a [TextDirection].

### startAngle

```dart
double startAngle
```

The angle in radians at which stop 0.0 of the gradient is placed.

The angle is measured in radians clockwise from the positive x-axis.

Values outside the range `[0, 2π]` are normalized to the equivalent angle within this range using modulo arithmetic.

The gradient will be painted in the sector between [startAngle] and [endAngle]. The behavior outside this sector is determined by [tileMode].

Defaults to 0.0.

### endAngle

```dart
double endAngle
```

The angle in radians at which stop 1.0 of the gradient is placed.

The angle is measured in radians clockwise from the positive x-axis.

Values outside the range `[0, 2π]` are normalized to the equivalent angle within this range using modulo arithmetic.

The gradient will be painted in the sector between [startAngle] and [endAngle]. The behavior outside this sector is determined by [tileMode].

Defaults to math.pi * 2 (2π = a full circle).

### tileMode

```dart
TileMode tileMode
```

How this gradient should tile the plane in the region before [startAngle] and after [endAngle].

The gradient will be painted in the sector between [startAngle] and [endAngle]. The [tileMode] determines what happens in the remaining area:

- [TileMode.clamp]: The edge colors are extended to fill the remaining area.
- [TileMode.repeated]: The gradient is repeated in the angular direction.
- [TileMode.mirror]: The gradient is mirrored in the angular direction.
- [TileMode.decal]: Only the gradient is drawn, leaving the remaining area transparent.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_clamp_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_decal_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_mirror_sweep.png) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/tile_mode_repeated_sweep.png)

### createShader()

```dart
Shader createShader(Rect rect, {TextDirection? textDirection})
```

### scale()

```dart
SweepGradient scale(double factor)
```

Returns a new [SweepGradient] with its colors scaled by the given factor.

Since the alpha component of the Color is what is scaled, a factor of 0.0 or less results in a gradient that is fully transparent.

### fromColor()

```dart
SweepGradient fromColor(Color color)
```

### lerpFrom()

```dart
Gradient? lerpFrom(Gradient? a, double t)
```

### lerpTo()

```dart
Gradient? lerpTo(Gradient? b, double t)
```

### lerp()

```dart
SweepGradient? lerp(SweepGradient? a, SweepGradient? b, double t)
```

Linearly interpolate between two [SweepGradient]s.

If either gradient is null, then the non-null gradient is returned with its color scaled in the same way as the [scale] function.

If neither gradient is null, they must have the same number of [colors].

The `t` argument represents a position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

### withOpacity()

```dart
SweepGradient withOpacity(double opacity)
```
