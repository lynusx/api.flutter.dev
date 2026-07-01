@docImport 'package:flutter/material.dart';

@docImport 'box_border.dart';

# BorderStyle

```dart
enum BorderStyle {}
```

The style of line to draw for a [BorderSide] in a [Border].

Skip the border.

Draw the border as a solid line.

# BorderSide

```dart
class BorderSide with Diagnosticable {}
```

A side of a border of a box.

A [Border] consists of four [BorderSide] objects: [Border.top], [Border.left], [Border.right], and [Border.bottom].

Setting [BorderSide.width] to 0.0 will result in hairline rendering; see [BorderSide.width] for a more involved explanation.

{@tool snippet} This sample shows how [BorderSide] objects can be used in a [Container], via a [BoxDecoration] and a [Border], to decorate some [Text]. In this example, the text has a thick bar above it that is light blue, and a thick bar below it that is a darker shade of blue.

```dart
Container(
  padding: const EdgeInsets.all(8.0),
  decoration: BoxDecoration(
    border: Border(
      top: BorderSide(width: 16.0, color: Colors.lightBlue.shade50),
      bottom: BorderSide(width: 16.0, color: Colors.lightBlue.shade900),
    ),
  ),
  child: const Text('Flutter in the sky', textAlign: TextAlign.center),
)
```

{@end-tool}

See also:

- [Border], which uses [BorderSide] objects to represent its sides.
- [BoxDecoration], which optionally takes a [Border] object.
- [TableBorder], which is similar to [Border] but has two more sides ([TableBorder.horizontalInside] and [TableBorder.verticalInside]), both of which are also [BorderSide] objects.

### BorderSide()

```dart
BorderSide({Color color = const Color(0xFF000000), double width = 1.0, BorderStyle style = BorderStyle.solid, double strokeAlign = strokeAlignInside})
```

Creates the side of a border.

By default, the border is 1.0 logical pixels wide and solid black.

### merge()

```dart
BorderSide merge(BorderSide a, BorderSide b)
```

Creates a [BorderSide] that represents the addition of the two given [BorderSide]s.

It is only valid to call this if [canMerge] returns true for the two sides.

If one of the sides is zero-width with [BorderStyle.none], then the other side is return as-is. If both of the sides are zero-width with [BorderStyle.none], then [BorderSide.none] is returned.

### color

```dart
Color color
```

The color of this side of the border.

### width

```dart
double width
```

The width of this side of the border, in logical pixels.

Setting width to 0.0 will result in a hairline border. This means that the border will have the width of one physical pixel. Hairline rendering takes shortcuts when the path overlaps a pixel more than once. This means that it will render faster than otherwise, but it might double-hit pixels, giving it a slightly darker/lighter result.

To omit the border entirely, set the [style] to [BorderStyle.none].

### style

```dart
BorderStyle style
```

The style of this side of the border.

To omit a side, set [style] to [BorderStyle.none]. This skips painting the border, but the border still has a [width].

### none

```dart
BorderSide none
```

A hairline black border that is not rendered.

### strokeAlign

```dart
double strokeAlign
```

The relative position of the stroke on a [BorderSide] in an [OutlinedBorder] or [Border].

Values typically range from -1.0 ([strokeAlignInside], inside border, default) to 1.0 ([strokeAlignOutside], outside border), without any bound constraints (e.g., a value of -2.0 is not typical, but allowed). A value of 0 ([strokeAlignCenter]) will center the border on the edge of the widget.

When set to [strokeAlignInside], the stroke is drawn completely inside the widget. For [strokeAlignCenter] and [strokeAlignOutside], a property such as [Container.clipBehavior] can be used in an outside widget to clip it. If [Container.decoration] has a border, the container may incorporate [width] as additional padding:

- [strokeAlignInside] provides padding with full [width].
- [strokeAlignCenter] provides padding with half [width].
- [strokeAlignOutside] provides zero padding, as stroke is drawn entirely outside.

This property is not honored by [toPaint] (because the [Paint] object cannot represent it); it is intended that classes that use [BorderSide] objects implement this property when painting borders by suitably inflating or deflating their regions.

{@tool dartpad} This example shows an animation of how [strokeAlign] affects the drawing when applied to borders of various shapes.

** See code in examples/api/lib/painting/borders/border_side.stroke_align.0.dart ** {@end-tool}

### strokeAlignInside

```dart
double strokeAlignInside
```

The border is drawn fully inside of the border path.

This is a constant for use with [strokeAlign].

This is the default value for [strokeAlign].

### strokeAlignCenter

```dart
double strokeAlignCenter
```

The border is drawn on the center of the border path, with half of the [BorderSide.width] on the inside, and the other half on the outside of the path.

This is a constant for use with [strokeAlign].

### strokeAlignOutside

```dart
double strokeAlignOutside
```

The border is drawn on the outside of the border path.

This is a constant for use with [strokeAlign].

### copyWith()

```dart
BorderSide copyWith({Color? color, double? width, BorderStyle? style, double? strokeAlign})
```

Creates a copy of this border but with the given fields replaced with the new values.

### scale()

```dart
BorderSide scale(double t)
```

Creates a copy of this border side description but with the width scaled by the factor `t`.

The `t` argument represents the multiplicand, or the position on the timeline for an interpolation from nothing to `this`, with 0.0 meaning that the object returned should be the nil variant of this object, 1.0 meaning that no change should be applied, returning `this` (or something equivalent to `this`), and other values meaning that the object should be multiplied by `t`. Negative values are treated like zero.

Since a zero width is normally painted as a hairline width rather than no border at all, the zero factor is special-cased to instead change the style to [BorderStyle.none].

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### toPaint()

```dart
Paint toPaint()
```

Create a [Paint] object that, if used to stroke a line, will draw the line in this border's style.

The [strokeAlign] property is not reflected in the [Paint]; consumers must implement that directly by inflating or deflating their region appropriately.

Not all borders use this method to paint their border sides. For example, non-uniform rectangular [Border]s have beveled edges and so paint their border sides as filled shapes rather than using a stroke.

### canMerge()

```dart
bool canMerge(BorderSide a, BorderSide b)
```

Whether the two given [BorderSide]s can be merged using [BorderSide.merge].

Two sides can be merged if one or both are zero-width with [BorderStyle.none], or if they both have the same color and style.

### lerp()

```dart
BorderSide lerp(BorderSide a, BorderSide b, double t)
```

Linearly interpolate between two border sides.

{@macro dart.ui.shadow.lerp}

### strokeInset

```dart
double get strokeInset
```

Get the amount of the stroke width that lies inside of the [BorderSide].

For example, this will return the [width] for a [strokeAlign] of -1, half the [width] for a [strokeAlign] of 0, and 0 for a [strokeAlign] of 1.

### strokeOutset

```dart
double get strokeOutset
```

Get the amount of the stroke width that lies outside of the [BorderSide].

For example, this will return 0 for a [strokeAlign] of -1, half the [width] for a [strokeAlign] of 0, and the [width] for a [strokeAlign] of 1.

### strokeOffset

```dart
double get strokeOffset
```

The offset of the stroke, taking into account the stroke alignment.

For example, this will return the negative [width] of the stroke for a [strokeAlign] of -1, 0 for a [strokeAlign] of 0, and the [width] for a [strokeAlign] of -1.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ShapeBorder

```dart
abstract class ShapeBorder {}
```

Base class for shape outlines.

This class handles how to add multiple borders together. Subclasses define various shapes, like circles ([CircleBorder]), rounded rectangles ([RoundedRectangleBorder]), continuous rectangles ([ContinuousRectangleBorder]), or beveled rectangles ([BeveledRectangleBorder]).

See also:

- [ShapeDecoration], which can be used with [DecoratedBox] to show a shape.
- [Material] (and many other widgets in the Material library), which takes a [ShapeBorder] to define its shape.
- [NotchedShape], which describes a shape with a hole in it.

### ShapeBorder()

```dart
ShapeBorder()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

The widths of the sides of this border represented as an [EdgeInsets].

Specifically, this is the amount by which a rectangle should be inset so as to avoid painting over any important part of the border. It is the amount by which additional borders will be inset before they are drawn.

This can be used, for example, with a [Padding] widget to inset a box by the size of these borders.

Shapes that have a fixed ratio regardless of the area on which they are painted, or that change their rendering based on the size they are given when painting (for instance [CircleBorder]), will not return valid [dimensions] information because they cannot know their eventual size when computing their [dimensions].

### add()

```dart
ShapeBorder? add(ShapeBorder other, {bool reversed = false})
```

Attempts to create a new object that represents the amalgamation of `this` border and the `other` border.

If the type of the other border isn't known, or the given instance cannot be reasonably added to this instance, then this should return null.

This method is used by the [operator +] implementation.

The `reversed` argument is true if this object was the right operand of the `+` operator, and false if it was the left operand.

### operator +()

```dart
ShapeBorder operator +(ShapeBorder other)
```

Creates a new border consisting of the two borders on either side of the operator.

If the borders belong to classes that know how to add themselves, then this results in a new border that represents the intelligent addition of those two borders (see [add]). Otherwise, an object is returned that merely paints the two borders sequentially, with the left hand operand on the inside and the right hand operand on the outside.

### scale()

```dart
ShapeBorder scale(double t)
```

Creates a copy of this border, scaled by the factor `t`.

Typically this means scaling the width of the border's side, but it can also include scaling other artifacts of the border, e.g. the border radius of a [RoundedRectangleBorder].

The `t` argument represents the multiplicand, or the position on the timeline for an interpolation from nothing to `this`, with 0.0 meaning that the object returned should be the nil variant of this object, 1.0 meaning that no change should be applied, returning `this` (or something equivalent to `this`), and other values meaning that the object should be multiplied by `t`. Negative values are allowed but may be meaningless (they correspond to extrapolating the interpolation from this object to nothing, and going beyond nothing)

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

See also:

- [BorderSide.scale], which most [ShapeBorder] subclasses defer to for the actual computation.

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

Linearly interpolates from another [ShapeBorder] (possibly of another class) to `this`.

When implementing this method in subclasses, return null if this class cannot interpolate from `a`. In that case, [lerp] will try other ways to interpolate between the two borders before applying a default behavior. If `a` is null, this must not return null.

The base class implementation handles the case of `a` being null by deferring to [scale].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `this` (or something equivalent to `this`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `this`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

Instead of calling this directly, use [ShapeBorder.lerp].

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

Linearly interpolates from `this` to another [ShapeBorder] (possibly of another class).

When implementing this method in subclasses, return null if this class cannot interpolate to `b`. In that case, [lerp] will try other ways to interpolate between the two borders before applying a default behavior. If `b` is null, this must not return null.

The base class implementation handles the case of `b` being null by deferring to [scale].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `this` (or something equivalent to `this`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `this` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

Instead of calling this directly, use [ShapeBorder.lerp].

### lerp()

```dart
ShapeBorder? lerp(ShapeBorder? a, ShapeBorder? b, double t)
```

Linearly interpolates between two [ShapeBorder]s.

This first tries the forward interpolation, by calling `b.lerpFrom(a, t)` and then `a.lerpTo(b, t)`. If both return null, this tries the same interpolation on the reversed timeline, by calling `b.lerpTo(a, 1.0 - t)` and then `a.lerpFrom(b, 1.0 - t)`. If all of these methods return null, this returns `a` before `t=0.5` and `b` after `t=0.5`.

{@macro dart.ui.shadow.lerp}

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
```

Create a [Path] that describes the outer edge of the border.

This path must not cross the path given by [getInnerPath] for the same [Rect].

To obtain a [Path] that describes the area of the border itself, set the [Path.fillType] of the returned object to [PathFillType.evenOdd], and add to this object the path returned from [getInnerPath] (using [Path.addPath]).

The `textDirection` argument must be provided non-null if the border has a text direction dependency (for example if it is expressed in terms of "start" and "end" instead of "left" and "right"). It may be null if the border will not need the text direction to paint itself.

See also:

- [getInnerPath], which creates the path for the inner edge.
- [Path.contains], which can tell if an [Offset] is within a [Path].

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

Create a [Path] that describes the inner edge of the border.

This path must not cross the path given by [getOuterPath] for the same [Rect].

To obtain a [Path] that describes the area of the border itself, set the [Path.fillType] of the returned object to [PathFillType.evenOdd], and add to this object the path returned from [getOuterPath] (using [Path.addPath]).

The `textDirection` argument must be provided and non-null if the border has a text direction dependency (for example if it is expressed in terms of "start" and "end" instead of "left" and "right"). It may be null if the border will not need the text direction to paint itself.

See also:

- [getOuterPath], which creates the path for the outer edge.
- [Path.contains], which can tell if an [Offset] is within a [Path].

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

Paint a canvas with the appropriate shape.

On [ShapeBorder] subclasses whose [preferPaintInterior] method returns true, this should be faster than using [Canvas.drawPath] with the path provided by [getOuterPath]. (If [preferPaintInterior] returns false, then this method asserts in debug mode and does nothing in release mode.)

Subclasses are expected to implement this method when the [Canvas] API has a dedicated method to draw the relevant shape. For example, [CircleBorder] uses this to call [Canvas.drawCircle], and [RoundedRectangleBorder] uses this to call [Canvas.drawRRect].

Subclasses that implement this must ensure that calling [paintInterior] is semantically equivalent to (i.e. renders the same pixels as) calling [Canvas.drawPath] with the same [Paint] and the [Path] returned from [getOuterPath], and must also override [preferPaintInterior] to return true.

For example, a shape that draws a rectangle might implement [getOuterPath], [paintInterior], and [preferPaintInterior] as follows:

```dart
class RectangleBorder extends OutlinedBorder {
  // ...

  @override
  Path getOuterPath(Rect rect, { TextDirection? textDirection }) {
   return Path()
     ..addRect(rect);
  }

  @override
  void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection}) {
   canvas.drawRect(rect, paint);
  }

  @override
  bool get preferPaintInterior => true;

  // ...
}
```

When a shape can only be drawn using path, [preferPaintInterior] must return false. In that case, classes such as [ShapeDecoration] will cache the path from [getOuterPath] and call [Canvas.drawPath] directly.

### preferPaintInterior

```dart
bool get preferPaintInterior
```

Reports whether [paintInterior] is implemented.

Classes such as [ShapeDecoration] prefer to use [paintInterior] if this getter returns true. This is intended to enable faster painting; instead of computing a shape using [getOuterPath] and then drawing it using [Canvas.drawPath], the path can be drawn directly to the [Canvas] using dedicated methods such as [Canvas.drawRect] or [Canvas.drawCircle].

By default, this getter returns false.

Subclasses that implement [paintInterior] should override this to return true. Subclasses should only override [paintInterior] if doing so enables faster rendering than is possible with [Canvas.drawPath] (so, in particular, subclasses should not call [Canvas.drawPath] in [paintInterior]).

See also:

- [paintInterior], whose API documentation has an example implementation.

### paint()

```dart
void paint(Canvas canvas, Rect rect, {TextDirection? textDirection})
```

Paints the border within the given [Rect] on the given [Canvas].

The `textDirection` argument must be provided and non-null if the border has a text direction dependency (for example if it is expressed in terms of "start" and "end" instead of "left" and "right"). It may be null if the border will not need the text direction to paint itself.

### toString()

```dart
String toString()
```

# OutlinedBorder

```dart
abstract class OutlinedBorder extends ShapeBorder {}
```

A ShapeBorder that draws an outline with the width and color specified by [side].

### OutlinedBorder()

```dart
OutlinedBorder({BorderSide side = BorderSide.none})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

### side

```dart
BorderSide side
```

The border outline's color and weight.

If [side] is [BorderSide.none], which is the default, an outline is not drawn. Otherwise the outline is centered over the shape's boundary.

### copyWith()

```dart
OutlinedBorder copyWith({BorderSide? side})
```

Returns a copy of this OutlinedBorder that draws its outline with the specified [side], if [side] is non-null.

### scale()

```dart
ShapeBorder scale(double t)
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
OutlinedBorder? lerp(OutlinedBorder? a, OutlinedBorder? b, double t)
```

Linearly interpolates between two [OutlinedBorder]s.

This first tries the forward interpolation, by calling `b.lerpFrom(a, t)` and then `a.lerpTo(b, t)`. If both return null, this tries the same interpolation on the reversed timeline, by calling `b.lerpTo(a, 1.0 - t)` and then `a.lerpFrom(b, 1.0 - t)`. If all of these methods return null, this returns `a` before `t=0.5` and `b` after `t=0.5`.

{@macro dart.ui.shadow.lerp}

# paintBorder()

```dart
void paintBorder(Canvas canvas, Rect rect, {BorderSide top = BorderSide.none, BorderSide right = BorderSide.none, BorderSide bottom = BorderSide.none, BorderSide left = BorderSide.none})
```

Paints a border around the given rectangle on the canvas.

The four sides can be independently specified. They are painted in the order top, right, bottom, left. This is only notable if the widths of the borders and the size of the given rectangle are such that the border sides will overlap each other. No effort is made to optimize the rendering of uniform borders (where all the borders have the same configuration); to render a uniform border, consider using [Canvas.drawRect] directly.

See also:

- [paintImage], which paints an image in a rectangle on a canvas.
- [Border], which uses this function to paint its border when the border is not uniform.
- [BoxDecoration], which describes its border using the [Border] class.
