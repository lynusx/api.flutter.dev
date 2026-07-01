@docImport 'package:flutter/material.dart';

@docImport 'box_decoration.dart';

# BoxShape

```dart
enum BoxShape {}
```

The shape to use when rendering a [Border] or [BoxDecoration].

Consider using [ShapeBorder] subclasses directly (with [ShapeDecoration]), instead of using [BoxShape] and [Border], if the shapes will need to be interpolated or animated. The [Border] class cannot interpolate between different shapes.

An axis-aligned rectangle, optionally with rounded corners.

The amount of corner rounding, if any, is determined by the border radius specified by classes such as [BoxDecoration] or [Border]. The rectangle's edges match those of the box in which it is painted.

See also:

- [RoundedRectangleBorder], the equivalent [ShapeBorder].

A circle centered in the middle of the box into which the [Border] or [BoxDecoration] is painted. The diameter of the circle is the shortest dimension of the box, either the width or the height, such that the circle touches the edges of the box.

See also:

- [CircleBorder], the equivalent [ShapeBorder].

# BoxBorder

```dart
abstract class BoxBorder extends ShapeBorder {}
```

Base class for box borders that can paint as rectangles, circles, or rounded rectangles.

This class is extended by [Border] and [BorderDirectional] to provide concrete versions of four-sided borders using different conventions for specifying the sides.

The only API difference that this class introduces over [ShapeBorder] is that its [paint] method takes additional arguments.

See also:

- [BorderSide], which is used to describe each side of the box.
- [RoundedRectangleBorder], another way of describing a box's border.
- [CircleBorder], another way of describing a circle border.
- [BoxDecoration], which uses a [BoxBorder] to describe its borders.

### BoxBorder()

```dart
BoxBorder()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### BoxBorder.fromLTRB()

```dart
BoxBorder.fromLTRB({BorderSide top = BorderSide.none, BorderSide right = BorderSide.none, BorderSide bottom = BorderSide.none, BorderSide left = BorderSide.none})
```

Creates a [Border].

All the sides of the border default to [BorderSide.none].

### BoxBorder.all()

```dart
BoxBorder.all({Color color, double width, BorderStyle style, double strokeAlign})
```

A uniform [Border] with all sides the same color and width.

The sides default to black solid borders, one logical pixel wide.

### BoxBorder.fromBorderSide()

```dart
BoxBorder.fromBorderSide(BorderSide side)
```

Creates a [Border] whose sides are all the same.

### BoxBorder.symmetric()

```dart
BoxBorder.symmetric({BorderSide vertical, BorderSide horizontal})
```

Creates a [Border] with symmetrical vertical and horizontal sides.

The `vertical` argument applies to the [left] and [right] sides, and the `horizontal` argument applies to the [top] and [bottom] sides.

All arguments default to [BorderSide.none].

### BoxBorder.fromSTEB()

```dart
BoxBorder.fromSTEB({BorderSide top = BorderSide.none, BorderSide start = BorderSide.none, BorderSide end = BorderSide.none, BorderSide bottom = BorderSide.none})
```

Creates a [BorderDirectional].

The [start] and [end] sides represent the horizontal sides; the start side is on the leading edge given the reading direction, and the end side is on the trailing edge. They are resolved during [paint].

All the sides of the border default to [BorderSide.none].

### top

```dart
BorderSide get top
```

The top side of this border.

This getter is available on both [Border] and [BorderDirectional]. If [isUniform] is true, then this is the same style as all the other sides.

### bottom

```dart
BorderSide get bottom
```

The bottom side of this border.

### isUniform

```dart
bool get isUniform
```

Whether all four sides of the border are identical. Uniform borders are typically more efficient to paint.

A uniform border by definition has no text direction dependency and therefore could be expressed as a [Border], even if it is currently a [BorderDirectional]. A uniform border can also be expressed as a [RoundedRectangleBorder].

### add()

```dart
BoxBorder? add(ShapeBorder other, {bool reversed = false})
```

### lerp()

```dart
BoxBorder? lerp(BoxBorder? a, BoxBorder? b, double t)
```

Linearly interpolate between two borders.

If a border is null, it is treated as having four [BorderSide.none] borders.

This supports interpolating between [Border] and [BorderDirectional] objects. If both objects are different types but both have sides on one or both of their lateral edges (the two sides that aren't the top and bottom) other than [BorderSide.none], then the sides are interpolated by reducing `a`'s lateral edges to [BorderSide.none] over the first half of the animation, and then bringing `b`'s lateral edges _from_ [BorderSide.none] over the second half of the animation.

For a more flexible approach, consider [ShapeBorder.lerp], which would instead [add] the two sets of sides and interpolate them simultaneously.

{@macro dart.ui.shadow.lerp}

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
```

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

### preferPaintInterior

```dart
bool get preferPaintInterior
```

### paint()

```dart
void paint(Canvas canvas, Rect rect, {TextDirection? textDirection, BoxShape shape = BoxShape.rectangle, BorderRadius? borderRadius})
```

Paints the border within the given [Rect] on the given [Canvas].

This is an extension of the [ShapeBorder.paint] method. It allows [BoxBorder] borders to be applied to different [BoxShape]s and with different [borderRadius] parameters, without changing the [BoxBorder] object itself.

The `shape` argument specifies the [BoxShape] to draw the border on.

If the `shape` is specifies a rectangular box shape ([BoxShape.rectangle]), then the `borderRadius` argument describes the corners of the rectangle.

The [getInnerPath] and [getOuterPath] methods do not know about the `shape` and `borderRadius` arguments.

See also:

- [paintBorder], which is used if the border has non-uniform colors or styles and no borderRadius.
- [Border.paint], similar to this method, includes additional comments and provides more details on each parameter than described here.

### paintNonUniformBorder()

```dart
void paintNonUniformBorder(Canvas canvas, Rect rect, {required BorderRadius? borderRadius, required TextDirection? textDirection, BoxShape shape = BoxShape.rectangle, BorderSide top = BorderSide.none, BorderSide right = BorderSide.none, BorderSide bottom = BorderSide.none, BorderSide left = BorderSide.none, required Color color})
```

Paints a Border with different widths, styles and strokeAligns, on any borderRadius while using a single color.

See also:

- [paintBorder], which supports multiple colors but not borderRadius.
- [paint], which calls this method.

# Border

```dart
class Border extends BoxBorder {}
```

A border of a box, comprised of four sides: top, right, bottom, left.

The sides are represented by [BorderSide] objects.

{@tool snippet}

All four borders the same, two-pixel wide solid white:

```dart
Border.all(width: 2.0, color: const Color(0xFFFFFFFF))
```

{@end-tool} {@tool snippet}

The border for a Material Design divider:

```dart
Border(bottom: BorderSide(color: Theme.of(context).dividerColor))
```

{@end-tool} {@tool snippet}

A 1990s-era "OK" button:

```dart
Container(
  decoration: const BoxDecoration(
    border: Border(
      top: BorderSide(color: Color(0xFFFFFFFF)),
      left: BorderSide(color: Color(0xFFFFFFFF)),
      right: BorderSide(),
      bottom: BorderSide(),
    ),
  ),
  child: Container(
    padding: const EdgeInsets.symmetric(horizontal: 20.0, vertical: 2.0),
    decoration: const BoxDecoration(
      border: Border(
        top: BorderSide(color: Color(0xFFDFDFDF)),
        left: BorderSide(color: Color(0xFFDFDFDF)),
        right: BorderSide(color: Color(0xFF7F7F7F)),
        bottom: BorderSide(color: Color(0xFF7F7F7F)),
      ),
      color: Color(0xFFBFBFBF),
    ),
    child: const Text(
      'OK',
      textAlign: TextAlign.center,
      style: TextStyle(color: Color(0xFF000000))
    ),
  ),
)
```

{@end-tool}

See also:

- [BoxDecoration], which uses this class to describe its edge decoration.
- [BorderSide], which is used to describe each side of the box.
- [Theme], from the material layer, which can be queried to obtain appropriate colors to use for borders in a [MaterialApp], as shown in the "divider" sample above.
- [paint], which explains the behavior of [BoxDecoration] parameters.
- <https://pub.dev/packages/non_uniform_border>, a package that implements a Non-Uniform Border on ShapeBorder, which is used by Material Design buttons and other widgets, under the "shape" field.

### Border()

```dart
Border({BorderSide top = BorderSide.none, BorderSide right = BorderSide.none, BorderSide bottom = BorderSide.none, BorderSide left = BorderSide.none})
```

Creates a border.

All the sides of the border default to [BorderSide.none].

### Border.fromBorderSide()

```dart
Border.fromBorderSide(BorderSide side)
```

Creates a border whose sides are all the same.

### Border.symmetric()

```dart
Border.symmetric({BorderSide vertical = BorderSide.none, BorderSide horizontal = BorderSide.none})
```

Creates a border with symmetrical vertical and horizontal sides.

The `vertical` argument applies to the [left] and [right] sides, and the `horizontal` argument applies to the [top] and [bottom] sides.

All arguments default to [BorderSide.none].

### Border.all()

```dart
Border.all({Color color = const Color(0xFF000000), double width = 1.0, BorderStyle style = BorderStyle.solid, double strokeAlign = BorderSide.strokeAlignInside})
```

A uniform border with all sides the same color and width.

The sides default to black solid borders, one logical pixel wide.

### merge()

```dart
Border merge(Border a, Border b)
```

Creates a [Border] that represents the addition of the two given [Border]s.

It is only valid to call this if [BorderSide.canMerge] returns true for the pairwise combination of each side on both [Border]s.

### top

```dart
BorderSide top
```

### right

```dart
BorderSide right
```

The right side of this border.

### bottom

```dart
BorderSide bottom
```

### left

```dart
BorderSide left
```

The left side of this border.

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### isUniform

```dart
bool get isUniform
```

### add()

```dart
Border? add(ShapeBorder other, {bool reversed = false})
```

### scale()

```dart
Border scale(double t)
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### lerp()

```dart
Border? lerp(Border? a, Border? b, double t)
```

Linearly interpolate between two borders.

If a border is null, it is treated as having four [BorderSide.none] borders.

{@macro dart.ui.shadow.lerp}

### paint()

```dart
void paint(Canvas canvas, Rect rect, {TextDirection? textDirection, BoxShape shape = BoxShape.rectangle, BorderRadius? borderRadius})
```

Paints the border within the given [Rect] on the given [Canvas].

Uniform borders and non-uniform borders with similar colors and styles are more efficient to paint than more complex borders.

You can provide a [BoxShape] to draw the border on. If the `shape` in [BoxShape.circle], there is the requirement that the border has uniform color and style.

If you specify a rectangular box shape ([BoxShape.rectangle]), then you may specify a [BorderRadius]. If a `borderRadius` is specified, there is the requirement that the border has uniform color and style.

The [getInnerPath] and [getOuterPath] methods do not know about the `shape` and `borderRadius` arguments.

The `textDirection` argument is not used by this paint method.

See also:

- [paintBorder], which is used if the border has non-uniform colors or styles and no borderRadius.
- <https://pub.dev/packages/non_uniform_border>, a package that implements a Non-Uniform Border on ShapeBorder, which is used by Material Design buttons and other widgets, under the "shape" field.

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

# BorderDirectional

```dart
class BorderDirectional extends BoxBorder {}
```

A border of a box, comprised of four sides, the lateral sides of which flip over based on the reading direction.

The lateral sides are called [start] and [end]. When painted in left-to-right environments, the [start] side will be painted on the left and the [end] side on the right; in right-to-left environments, it is the reverse. The other two sides are [top] and [bottom].

The sides are represented by [BorderSide] objects.

If the [start] and [end] sides are the same, then it is slightly more efficient to use a [Border] object rather than a [BorderDirectional] object.

See also:

- [BoxDecoration], which uses this class to describe its edge decoration.
- [BorderSide], which is used to describe each side of the box.
- [Theme], from the material layer, which can be queried to obtain appropriate colors to use for borders in a [MaterialApp], as shown in the "divider" sample above.
- <https://pub.dev/packages/non_uniform_border>, a package that implements a Non-Uniform Border on ShapeBorder, which is used by Material Design buttons and other widgets, under the "shape" field.

### BorderDirectional()

```dart
BorderDirectional({BorderSide top = BorderSide.none, BorderSide start = BorderSide.none, BorderSide end = BorderSide.none, BorderSide bottom = BorderSide.none})
```

Creates a border.

The [start] and [end] sides represent the horizontal sides; the start side is on the leading edge given the reading direction, and the end side is on the trailing edge. They are resolved during [paint].

All the sides of the border default to [BorderSide.none].

### merge()

```dart
BorderDirectional merge(BorderDirectional a, BorderDirectional b)
```

Creates a [BorderDirectional] that represents the addition of the two given [BorderDirectional]s.

It is only valid to call this if [BorderSide.canMerge] returns true for the pairwise combination of each side on both [BorderDirectional]s.

### top

```dart
BorderSide top
```

### start

```dart
BorderSide start
```

The start side of this border.

This is the side on the left in left-to-right text and on the right in right-to-left text.

See also:

- [TextDirection], which is used to describe the reading direction.

### end

```dart
BorderSide end
```

The end side of this border.

This is the side on the right in left-to-right text and on the left in right-to-left text.

See also:

- [TextDirection], which is used to describe the reading direction.

### bottom

```dart
BorderSide bottom
```

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### isUniform

```dart
bool get isUniform
```

### add()

```dart
BoxBorder? add(ShapeBorder other, {bool reversed = false})
```

### scale()

```dart
BorderDirectional scale(double t)
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### lerp()

```dart
BorderDirectional? lerp(BorderDirectional? a, BorderDirectional? b, double t)
```

Linearly interpolate between two borders.

If a border is null, it is treated as having four [BorderSide.none] borders.

{@macro dart.ui.shadow.lerp}

### paint()

```dart
void paint(Canvas canvas, Rect rect, {TextDirection? textDirection, BoxShape shape = BoxShape.rectangle, BorderRadius? borderRadius})
```

Paints the border within the given [Rect] on the given [Canvas].

Uniform borders are more efficient to paint than more complex borders.

You can provide a [BoxShape] to draw the border on. If the `shape` in [BoxShape.circle], there is the requirement that the border [isUniform].

If you specify a rectangular box shape ([BoxShape.rectangle]), then you may specify a [BorderRadius]. If a `borderRadius` is specified, there is the requirement that the border [isUniform].

The [getInnerPath] and [getOuterPath] methods do not know about the `shape` and `borderRadius` arguments.

The `textDirection` argument is used to determine which of [start] and [end] map to the left and right. For [TextDirection.ltr], the [start] is the left and the [end] is the right; for [TextDirection.rtl], it is the reverse.

See also:

- [paintBorder], which is used if the border has non-uniform colors or styles and no borderRadius.

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
