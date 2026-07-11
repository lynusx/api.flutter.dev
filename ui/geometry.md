# OffsetBase

```dart
abstract class OffsetBase {}
```

Base class for [Size] and [Offset], which are both ways to describe a distance as a two-dimensional axis-aligned vector.

### OffsetBase()

```dart
OffsetBase(double _dx, double _dy)
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

The first argument sets the horizontal component, and the second the vertical component.

### isInfinite

```dart
bool get isInfinite
```

Returns true if either component is [double.infinity], and false if both are finite (or negative infinity, or NaN).

This is different than comparing for equality with an instance that has _both_ components set to [double.infinity].

See also:

- [isFinite], which is true if both components are finite (and not NaN).

### isFinite

```dart
bool get isFinite
```

Whether both components are finite (neither infinite nor NaN).

See also:

- [isInfinite], which returns true if either component is equal to positive infinity.

### operator <()

```dart
bool operator <(OffsetBase other)
```

Less-than operator. Compares an [Offset] or [Size] to another [Offset] or [Size], and returns true if both the horizontal and vertical values of the left-hand-side operand are smaller than the horizontal and vertical values of the right-hand-side operand respectively. Returns false otherwise.

This is a partial ordering. It is possible for two values to be neither less, nor greater than, nor equal to, another.

### operator <=()

```dart
bool operator <=(OffsetBase other)
```

Less-than-or-equal-to operator. Compares an [Offset] or [Size] to another [Offset] or [Size], and returns true if both the horizontal and vertical values of the left-hand-side operand are smaller than or equal to the horizontal and vertical values of the right-hand-side operand respectively. Returns false otherwise.

This is a partial ordering. It is possible for two values to be neither less, nor greater than, nor equal to, another.

### operator >()

```dart
bool operator >(OffsetBase other)
```

Greater-than operator. Compares an [Offset] or [Size] to another [Offset] or [Size], and returns true if both the horizontal and vertical values of the left-hand-side operand are bigger than the horizontal and vertical values of the right-hand-side operand respectively. Returns false otherwise.

This is a partial ordering. It is possible for two values to be neither less, nor greater than, nor equal to, another.

### operator >=()

```dart
bool operator >=(OffsetBase other)
```

Greater-than-or-equal-to operator. Compares an [Offset] or [Size] to another [Offset] or [Size], and returns true if both the horizontal and vertical values of the left-hand-side operand are bigger than or equal to the horizontal and vertical values of the right-hand-side operand respectively. Returns false otherwise.

This is a partial ordering. It is possible for two values to be neither less, nor greater than, nor equal to, another.

### operator ==()

```dart
bool operator ==(Object other)
```

Equality operator. Compares an [Offset] or [Size] to another [Offset] or [Size], and returns true if the horizontal and vertical values of the left-hand-side operand are equal to the horizontal and vertical values of the right-hand-side operand respectively. Returns false otherwise.

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Offset

```dart
class Offset extends OffsetBase {}
```

An immutable 2D floating-point offset.

Generally speaking, Offsets can be interpreted in two ways:

1.  As representing a point in Cartesian space a specified distance from a separately-maintained origin. For example, the top-left position of children in the [RenderBox] protocol is typically represented as an [Offset] from the top left of the parent box.

2.  As a vector that can be applied to coordinates. For example, when painting a [RenderObject], the parent is passed an [Offset] from the screen's origin which it can add to the offsets of its children to find the [Offset] from the screen's origin to each of the children.

Because a particular [Offset] can be interpreted as one sense at one time then as the other sense at a later time, the same class is used for both senses.

See also:

- [Size], which represents a vector describing the size of a rectangle.

### Offset()

```dart
Offset(double dx, double dy)
```

Creates an offset. The first argument sets [dx], the horizontal component, and the second sets [dy], the vertical component.

### Offset.fromDirection()

```dart
Offset.fromDirection(double direction, [double distance = 1.0])
```

Creates an offset from its [direction] and [distance].

The direction is in radians clockwise from the positive x-axis.

The distance can be omitted, to create a unit vector (distance = 1.0).

### dx

```dart
double get dx
```

The x component of the offset.

The y component is given by [dy].

### dy

```dart
double get dy
```

The y component of the offset.

The x component is given by [dx].

### distance

```dart
double get distance
```

The magnitude of the offset.

If you need this value to compare it to another [Offset]'s distance, consider using [distanceSquared] instead, since it is cheaper to compute.

### distanceSquared

```dart
double get distanceSquared
```

The square of the magnitude of the offset.

This is cheaper than computing the [distance] itself.

### direction

```dart
double get direction
```

The angle of this offset as radians clockwise from the positive x-axis, in the range -[pi] to [pi], assuming positive values of the x-axis go to the right and positive values of the y-axis go down.

Zero means that [dy] is zero and [dx] is zero or positive.

Values from zero to [pi]/2 indicate positive values of [dx] and [dy], the bottom-right quadrant.

Values from [pi]/2 to [pi] indicate negative values of [dx] and positive values of [dy], the bottom-left quadrant.

Values from zero to -[pi]/2 indicate positive values of [dx] and negative values of [dy], the top-right quadrant.

Values from -[pi]/2 to -[pi] indicate negative values of [dx] and [dy], the top-left quadrant.

When [dy] is zero and [dx] is negative, the [direction] is [pi].

When [dx] is zero, [direction] is [pi]/2 if [dy] is positive and -[pi]/2 if [dy] is negative.

See also:

- [distance], to compute the magnitude of the vector.
- [Canvas.rotate], which uses the same convention for its angle.

### zero

```dart
Offset zero
```

An offset with zero magnitude.

This can be used to represent the origin of a coordinate space.

### infinite

```dart
Offset infinite
```

An offset with infinite x and y components.

See also:

- [isInfinite], which checks whether either component is infinite.
- [isFinite], which checks whether both components are finite.

### scale()

```dart
Offset scale(double scaleX, double scaleY)
```

Returns a new offset with the x component scaled by `scaleX` and the y component scaled by `scaleY`.

If the two scale arguments are the same, consider using the `*` operator instead:

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = a * 2.0; // same as: a.scale(2.0, 2.0)
```

If the two arguments are -1, consider using the unary `-` operator instead:

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = -a; // same as: a.scale(-1.0, -1.0)
```

### translate()

```dart
Offset translate(double translateX, double translateY)
```

Returns a new offset with translateX added to the x component and translateY added to the y component.

If the arguments come from another [Offset], consider using the `+` or `-` operators instead:

```dart
Offset a = const Offset(10.0, 10.0);
Offset b = const Offset(10.0, 10.0);
Offset c = a + b; // same as: a.translate(b.dx, b.dy)
Offset d = a - b; // same as: a.translate(-b.dx, -b.dy)
```

### operator -()

```dart
Offset operator -()
```

Unary negation operator.

Returns an offset with the coordinates negated.

If the [Offset] represents an arrow on a plane, this operator returns the same arrow but pointing in the reverse direction.

### operator -()

```dart
Offset operator -(Offset other)
```

Binary subtraction operator.

Returns an offset whose [dx] value is the left-hand-side operand's [dx] minus the right-hand-side operand's [dx] and whose [dy] value is the left-hand-side operand's [dy] minus the right-hand-side operand's [dy].

See also [translate].

### operator +()

```dart
Offset operator +(Offset other)
```

Binary addition operator.

Returns an offset whose [dx] value is the sum of the [dx] values of the two operands, and whose [dy] value is the sum of the [dy] values of the two operands.

See also [translate].

### operator \*()

```dart
Offset operator *(double operand)
```

Multiplication operator.

Returns an offset whose coordinates are the coordinates of the left-hand-side operand (an Offset) multiplied by the scalar right-hand-side operand (a double).

See also [scale].

### operator /()

```dart
Offset operator /(double operand)
```

Division operator.

Returns an offset whose coordinates are the coordinates of the left-hand-side operand (an Offset) divided by the scalar right-hand-side operand (a double).

See also [scale].

### operator ~/()

```dart
Offset operator ~/(double operand)
```

Integer (truncating) division operator.

Returns an offset whose coordinates are the coordinates of the left-hand-side operand (an Offset) divided by the scalar right-hand-side operand (a double), rounded towards zero.

### operator %()

```dart
Offset operator %(double operand)
```

Modulo (remainder) operator.

Returns an offset whose coordinates are the remainder of dividing the coordinates of the left-hand-side operand (an Offset) by the scalar right-hand-side operand (a double).

### operator &()

```dart
Rect operator &(Size other)
```

Rectangle constructor operator.

Combines an [Offset] and a [Size] to form a [Rect] whose top-left coordinate is the point given by adding this offset, the left-hand-side operand, to the origin, and whose size is the right-hand-side operand.

```dart
Rect myRect = Offset.zero & const Size(100.0, 100.0);
// same as: Rect.fromLTWH(0.0, 0.0, 100.0, 100.0)
```

### lerp()

```dart
Offset? lerp(Offset? a, Offset? b, double t)
```

Linearly interpolate between two offsets.

If either offset is null, this function interpolates from [Offset.zero].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

Compares two Offsets for equality.

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Size

```dart
class Size extends OffsetBase {}
```

Holds a 2D floating-point size.

You can think of this as an [Offset] from the origin.

### Size()

```dart
Size(double width, double height)
```

Creates a [Size] with the given [width] and [height].

### Size.copy()

```dart
Size.copy(Size source)
```

Creates an instance of [Size] that has the same values as another.

### Size.square()

```dart
Size.square(double dimension)
```

Creates a square [Size] whose [width] and [height] are the given dimension.

See also:

- [Size.fromRadius], which is more convenient when the available size is the radius of a circle.

### Size.fromWidth()

```dart
Size.fromWidth(double width)
```

Creates a [Size] with the given [width] and an infinite [height].

### Size.fromHeight()

```dart
Size.fromHeight(double height)
```

Creates a [Size] with the given [height] and an infinite [width].

### Size.fromRadius()

```dart
Size.fromRadius(double radius)
```

Creates a square [Size] whose [width] and [height] are twice the given dimension.

This is a square that contains a circle with the given radius.

See also:

- [Size.square], which creates a square with the given dimension.

### width

```dart
double get width
```

The horizontal extent of this size.

### height

```dart
double get height
```

The vertical extent of this size.

### aspectRatio

```dart
double get aspectRatio
```

The aspect ratio of this size.

This returns the [width] divided by the [height].

If the [width] is zero, the result will be zero. If the [height] is zero (and the [width] is not), the result will be [double.infinity] or [double.negativeInfinity] as determined by the sign of [width].

See also:

- [AspectRatio], a widget for giving a child widget a specific aspect ratio.
- [FittedBox], a widget that (in most modes) attempts to maintain a child widget's aspect ratio while changing its size.

### zero

```dart
Size zero
```

An empty size, one with a zero width and a zero height.

### infinite

```dart
Size infinite
```

A size whose [width] and [height] are infinite.

See also:

- [isInfinite], which checks whether either dimension is infinite.
- [isFinite], which checks whether both dimensions are finite.

### isEmpty

```dart
bool get isEmpty
```

Whether this size encloses a zero area.

Negative areas are considered empty.

### operator -()

```dart
OffsetBase operator -(OffsetBase other)
```

Binary subtraction operator for [Size].

Subtracting a [Size] from a [Size] returns the [Offset] that describes how much bigger the left-hand-side operand is than the right-hand-side operand. Adding that resulting [Offset] to the [Size] that was the right-hand-side operand would return a [Size] equal to the [Size] that was the left-hand-side operand. (i.e. if `sizeA - sizeB -> offsetA`, then `offsetA + sizeB -> sizeA`)

Subtracting an [Offset] from a [Size] returns the [Size] that is smaller than the [Size] operand by the difference given by the [Offset] operand. In other words, the returned [Size] has a [width] consisting of the [width] of the left-hand-side operand minus the [Offset.dx] dimension of the right-hand-side operand, and a [height] consisting of the [height] of the left-hand-side operand minus the [Offset.dy] dimension of the right-hand-side operand.

### operator +()

```dart
Size operator +(Offset other)
```

Binary addition operator for adding an [Offset] to a [Size].

Returns a [Size] whose [width] is the sum of the [width] of the left-hand-side operand, a [Size], and the [Offset.dx] dimension of the right-hand-side operand, an [Offset], and whose [height] is the sum of the [height] of the left-hand-side operand and the [Offset.dy] dimension of the right-hand-side operand.

### operator \*()

```dart
Size operator *(double operand)
```

Multiplication operator.

Returns a [Size] whose dimensions are the dimensions of the left-hand-side operand (a [Size]) multiplied by the scalar right-hand-side operand (a [double]).

### operator /()

```dart
Size operator /(double operand)
```

Division operator.

Returns a [Size] whose dimensions are the dimensions of the left-hand-side operand (a [Size]) divided by the scalar right-hand-side operand (a [double]).

### operator ~/()

```dart
Size operator ~/(double operand)
```

Integer (truncating) division operator.

Returns a [Size] whose dimensions are the dimensions of the left-hand-side operand (a [Size]) divided by the scalar right-hand-side operand (a [double]), rounded towards zero.

### operator %()

```dart
Size operator %(double operand)
```

Modulo (remainder) operator.

Returns a [Size] whose dimensions are the remainder of dividing the left-hand-side operand (a [Size]) by the scalar right-hand-side operand (a [double]).

### shortestSide

```dart
double get shortestSide
```

The lesser of the magnitudes of the [width] and the [height].

### longestSide

```dart
double get longestSide
```

The greater of the magnitudes of the [width] and the [height].

### topLeft()

```dart
Offset topLeft(Offset origin)
```

The offset to the intersection of the top and left edges of the rectangle described by the given [Offset] (which is interpreted as the top-left corner) and this [Size].

See also [Rect.topLeft].

### topCenter()

```dart
Offset topCenter(Offset origin)
```

The offset to the center of the top edge of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.topCenter].

### topRight()

```dart
Offset topRight(Offset origin)
```

The offset to the intersection of the top and right edges of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.topRight].

### centerLeft()

```dart
Offset centerLeft(Offset origin)
```

The offset to the center of the left edge of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.centerLeft].

### center()

```dart
Offset center(Offset origin)
```

The offset to the point halfway between the left and right and the top and bottom edges of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.center].

### centerRight()

```dart
Offset centerRight(Offset origin)
```

The offset to the center of the right edge of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.centerRight].

### bottomLeft()

```dart
Offset bottomLeft(Offset origin)
```

The offset to the intersection of the bottom and left edges of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.bottomLeft].

### bottomCenter()

```dart
Offset bottomCenter(Offset origin)
```

The offset to the center of the bottom edge of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.bottomCenter].

### bottomRight()

```dart
Offset bottomRight(Offset origin)
```

The offset to the intersection of the bottom and right edges of the rectangle described by the given offset (which is interpreted as the top-left corner) and this size.

See also [Rect.bottomRight].

### contains()

```dart
bool contains(Offset offset)
```

Whether the point specified by the given offset (which is assumed to be relative to the top left of the size) lies between the left and right and the top and bottom edges of a rectangle of this size.

Rectangles include their top and left edges but exclude their bottom and right edges.

### flipped

```dart
Size get flipped
```

A [Size] with the [width] and [height] swapped.

### lerp()

```dart
Size? lerp(Size? a, Size? b, double t)
```

Linearly interpolate between two sizes

If either size is null, this function interpolates from [Size.zero].

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### operator ==()

```dart
bool operator ==(Object other)
```

Compares two Sizes for equality.

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Rect

```dart
class Rect {}
```

An immutable, 2D, axis-aligned, floating-point rectangle whose coordinates are relative to a given origin.

A Rect can be created with one of its constructors or from an [Offset] and a [Size] using the `&` operator:

```dart
Rect myRect = const Offset(1.0, 2.0) & const Size(3.0, 4.0);
```

### Rect.fromLTRB()

```dart
Rect.fromLTRB(double left, double top, double right, double bottom)
```

Construct a rectangle from its left, top, right, and bottom edges.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltrb.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltrb_dark.png#gh-dark-mode-only)

### Rect.fromLTWH()

```dart
Rect.fromLTWH(double left, double top, double width, double height)
```

Construct a rectangle from its left and top edges, its width, and its height.

To construct a [Rect] from an [Offset] and a [Size], you can use the rectangle constructor operator `&`. See [Offset.&].

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltwh.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_ltwh_dark.png#gh-dark-mode-only)

### Rect.fromCircle()

```dart
Rect.fromCircle({required Offset center, required double radius})
```

Construct a rectangle that bounds the given circle.

The `center` argument is assumed to be an offset from the origin.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_circle.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_circle_dark.png#gh-dark-mode-only)

### Rect.fromCenter()

```dart
Rect.fromCenter({required Offset center, required double width, required double height})
```

Constructs a rectangle from its center point, width, and height.

The `center` argument is assumed to be an offset from the origin.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_center.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_center_dark.png#gh-dark-mode-only)

### Rect.fromPoints()

```dart
Rect.fromPoints(Offset a, Offset b)
```

Construct the smallest rectangle that encloses the given offsets, treating them as vectors from the origin.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_points.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/rect_from_points_dark.png#gh-dark-mode-only)

### left

```dart
double left
```

The offset of the left edge of this rectangle from the x axis.

### top

```dart
double top
```

The offset of the top edge of this rectangle from the y axis.

### right

```dart
double right
```

The offset of the right edge of this rectangle from the x axis.

### bottom

```dart
double bottom
```

The offset of the bottom edge of this rectangle from the y axis.

### width

```dart
double get width
```

The distance between the left and right edges of this rectangle.

### height

```dart
double get height
```

The distance between the top and bottom edges of this rectangle.

### size

```dart
Size get size
```

The distance between the upper-left corner and the lower-right corner of this rectangle.

### hasNaN

```dart
bool get hasNaN
```

Whether any of the dimensions are `NaN`.

### zero

```dart
Rect zero
```

A rectangle with left, top, right, and bottom edges all at zero.

### largest

```dart
Rect largest
```

A rectangle that covers the entire coordinate space.

This covers the space from -1e9,-1e9 to 1e9,1e9. This is the space over which graphics operations are valid.

### isInfinite

```dart
bool get isInfinite
```

Whether any of the coordinates of this rectangle are equal to positive infinity.

### isFinite

```dart
bool get isFinite
```

Whether all coordinates of this rectangle are finite.

### isEmpty

```dart
bool get isEmpty
```

Whether this rectangle encloses a non-zero area. Negative areas are considered empty.

### shift()

```dart
Rect shift(Offset offset)
```

Returns a new rectangle translated by the given offset.

To translate a rectangle by separate x and y components rather than by an [Offset], consider [translate].

### translate()

```dart
Rect translate(double translateX, double translateY)
```

Returns a new rectangle with translateX added to the x components and translateY added to the y components.

To translate a rectangle by an [Offset] rather than by separate x and y components, consider [shift].

### inflate()

```dart
Rect inflate(double delta)
```

Returns a new rectangle with edges moved outwards by the given delta.

### deflate()

```dart
Rect deflate(double delta)
```

Returns a new rectangle with edges moved inwards by the given delta.

### intersect()

```dart
Rect intersect(Rect other)
```

Returns a new rectangle that is the intersection of the given rectangle and this rectangle. The two rectangles must overlap for this to be meaningful. If the two rectangles do not overlap, then the resulting Rect will have a negative width or height.

### expandToInclude()

```dart
Rect expandToInclude(Rect other)
```

Returns a new rectangle which is the bounding box containing this rectangle and the given rectangle.

### overlaps()

```dart
bool overlaps(Rect other)
```

Whether `other` has a nonzero area of overlap with this rectangle.

### shortestSide

```dart
double get shortestSide
```

The lesser of the magnitudes of the [width] and the [height] of this rectangle.

### longestSide

```dart
double get longestSide
```

The greater of the magnitudes of the [width] and the [height] of this rectangle.

### topLeft

```dart
Offset get topLeft
```

The offset to the intersection of the top and left edges of this rectangle.

See also [Size.topLeft].

### topCenter

```dart
Offset get topCenter
```

The offset to the center of the top edge of this rectangle.

See also [Size.topCenter].

### topRight

```dart
Offset get topRight
```

The offset to the intersection of the top and right edges of this rectangle.

See also [Size.topRight].

### centerLeft

```dart
Offset get centerLeft
```

The offset to the center of the left edge of this rectangle.

See also [Size.centerLeft].

### center

```dart
Offset get center
```

The offset to the point halfway between the left and right and the top and bottom edges of this rectangle.

See also [Size.center].

### centerRight

```dart
Offset get centerRight
```

The offset to the center of the right edge of this rectangle.

See also [Size.centerRight].

### bottomLeft

```dart
Offset get bottomLeft
```

The offset to the intersection of the bottom and left edges of this rectangle.

See also [Size.bottomLeft].

### bottomCenter

```dart
Offset get bottomCenter
```

The offset to the center of the bottom edge of this rectangle.

See also [Size.bottomCenter].

### bottomRight

```dart
Offset get bottomRight
```

The offset to the intersection of the bottom and right edges of this rectangle.

See also [Size.bottomRight].

### contains()

```dart
bool contains(Offset offset)
```

Whether the point specified by the given offset (which is assumed to be relative to the origin) lies between the left and right and the top and bottom edges of this rectangle.

Rectangles include their top and left edges but exclude their bottom and right edges.

### lerp()

```dart
Rect? lerp(Rect? a, Rect? b, double t)
```

Linearly interpolate between two rectangles.

If either rect is null, [Rect.zero] is used as a substitute.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

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

# Radius

```dart
class Radius {}
```

A radius for either circular or elliptical shapes.

### Radius.circular()

```dart
Radius.circular(double radius)
```

Constructs a circular radius. [x] and [y] will have the same radius value.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_circular.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_circular_dark.png#gh-dark-mode-only)

### Radius.elliptical()

```dart
Radius.elliptical(double x, double y)
```

Constructs an elliptical radius with the given radii.

![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_elliptical.png#gh-light-mode-only) ![](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/radius_elliptical_dark.png#gh-dark-mode-only)

### x

```dart
double x
```

The radius value on the horizontal axis.

### y

```dart
double y
```

The radius value on the vertical axis.

### zero

```dart
Radius zero
```

A radius with [x] and [y] values set to zero.

You can use [Radius.zero] with [RRect] or [RSuperellipse] to have right-angle corners.

### clamp()

```dart
Radius clamp({Radius? minimum, Radius? maximum})
```

Returns this [Radius], with values clamped to the given min and max [Radius] values.

The `min` value defaults to `Radius.circular(-double.infinity)`, and the `max` value defaults to `Radius.circular(double.infinity)`.

### clampValues()

```dart
Radius clampValues({double? minimumX, double? minimumY, double? maximumX, double? maximumY})
```

Returns this [Radius], with values clamped to the given min and max values in each dimension

The `minimumX` and `minimumY` values default to `-double.infinity`, and the `maximumX` and `maximumY` values default to `double.infinity`.

### operator -()

```dart
Radius operator -()
```

Unary negation operator.

Returns a Radius with the distances negated.

Radiuses with negative values aren't geometrically meaningful, but could occur as part of expressions. For example, negating a radius of one pixel and then adding the result to another radius is equivalent to subtracting a radius of one pixel from the other.

### operator -()

```dart
Radius operator -(Radius other)
```

Binary subtraction operator.

Returns a radius whose [x] value is the left-hand-side operand's [x] minus the right-hand-side operand's [x] and whose [y] value is the left-hand-side operand's [y] minus the right-hand-side operand's [y].

### operator +()

```dart
Radius operator +(Radius other)
```

Binary addition operator.

Returns a radius whose [x] value is the sum of the [x] values of the two operands, and whose [y] value is the sum of the [y] values of the two operands.

### operator \*()

```dart
Radius operator *(double operand)
```

Multiplication operator.

Returns a radius whose coordinates are the coordinates of the left-hand-side operand (a radius) multiplied by the scalar right-hand-side operand (a double).

### operator /()

```dart
Radius operator /(double operand)
```

Division operator.

Returns a radius whose coordinates are the coordinates of the left-hand-side operand (a radius) divided by the scalar right-hand-side operand (a double).

### operator ~/()

```dart
Radius operator ~/(double operand)
```

Integer (truncating) division operator.

Returns a radius whose coordinates are the coordinates of the left-hand-side operand (a radius) divided by the scalar right-hand-side operand (a double), rounded towards zero.

### operator %()

```dart
Radius operator %(double operand)
```

Modulo (remainder) operator.

Returns a radius whose coordinates are the remainder of dividing the coordinates of the left-hand-side operand (a radius) by the scalar right-hand-side operand (a double).

### lerp()

```dart
Radius? lerp(Radius? a, Radius? b, double t)
```

Linearly interpolate between two radii.

If either is null, this function substitutes [Radius.zero] instead.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

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

# RRect

```dart
class RRect extends _RRectLike<RRect> {}
```

An immutable rounded rectangle with the custom radii for all four corners.

### RRect.fromLTRBXY()

```dart
RRect.fromLTRBXY(double left, double top, double right, double bottom, double radiusX, double radiusY)
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and the same radii along its horizontal axis and its vertical axis.

Will assert in debug mode if `radiusX` or `radiusY` are negative.

### RRect.fromLTRBR()

```dart
RRect.fromLTRBR(double left, double top, double right, double bottom, Radius radius)
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and the same radius in each corner.

Will assert in debug mode if the `radius` is negative in either x or y.

### RRect.fromRectXY()

```dart
RRect.fromRectXY(Rect rect, double radiusX, double radiusY)
```

Construct a rounded rectangle from its bounding box and the same radii along its horizontal axis and its vertical axis.

Will assert in debug mode if `radiusX` or `radiusY` are negative.

### RRect.fromRectAndRadius()

```dart
RRect.fromRectAndRadius(Rect rect, Radius radius)
```

Construct a rounded rectangle from its bounding box and a radius that is the same in each corner.

Will assert in debug mode if the `radius` is negative in either x or y.

### RRect.fromLTRBAndCorners()

```dart
RRect.fromLTRBAndCorners(double left, double top, double right, double bottom, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and topLeft, topRight, bottomRight, and bottomLeft radii.

The corner radii default to [Radius.zero], i.e. right-angled corners. Will assert in debug mode if any of the radii are negative in either x or y.

### RRect.fromRectAndCorners()

```dart
RRect.fromRectAndCorners(Rect rect, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

Construct a rounded rectangle from its bounding box and topLeft, topRight, bottomRight, and bottomLeft radii.

The corner radii default to [Radius.zero], i.e. right-angled corners. Will assert in debug mode if any of the radii are negative in either x or y.

### zero

```dart
RRect zero
```

A rounded rectangle with all the values set to zero.

### contains()

```dart
bool contains(Offset point)
```

Whether the point specified by the given offset (which is assumed to be relative to the origin) lies inside the rounded rectangle.

This method may allocate (and cache) a copy of the object with normalized radii the first time it is called on a particular [RRect] instance. When using this method, prefer to reuse existing [RRect]s rather than recreating the object each time.

### lerp()

```dart
RRect? lerp(RRect? a, RRect? b, double t)
```

Linearly interpolate between two rounded rectangles.

If either is null, this function substitutes [RRect.zero] instead.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### toString()

```dart
String toString()
```

# RSuperellipse

```dart
class RSuperellipse extends _RRectLike<RSuperellipse> {}
```

An immutable rounded superellipse.

A rounded superellipse (not to be confused with a standard superellipse) is a shape formed by replacing the four curved corners of a superellipse with circular arcs. A (standard) superellipse follows the formula x^n + y^n = a^n, and while n > 2 gives it rounded corners, they tend to be too sharp and pronounced. Replacing them with circular arcs makes the shape feel softer and more natural.

Visually, a rounded superellipse looks similar to a typical rounded rectangle ([RRect]) but with smoother transitions between the straight edges and corners. It closely matches the `RoundedRectangle` shape in SwiftUI with the `.continuous` corner style.

### RSuperellipse.fromLTRBXY()

```dart
RSuperellipse.fromLTRBXY(double left, double top, double right, double bottom, double radiusX, double radiusY)
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and the same radii along its horizontal axis and its vertical axis.

Will assert in debug mode if `radiusX` or `radiusY` are negative.

### RSuperellipse.fromLTRBR()

```dart
RSuperellipse.fromLTRBR(double left, double top, double right, double bottom, Radius radius)
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and the same radius in each corner.

Will assert in debug mode if the `radius` is negative in either x or y.

### RSuperellipse.fromRectXY()

```dart
RSuperellipse.fromRectXY(Rect rect, double radiusX, double radiusY)
```

Construct a rounded rectangle from its bounding box and the same radii along its horizontal axis and its vertical axis.

Will assert in debug mode if `radiusX` or `radiusY` are negative.

### RSuperellipse.fromRectAndRadius()

```dart
RSuperellipse.fromRectAndRadius(Rect rect, Radius radius)
```

Construct a rounded rectangle from its bounding box and a radius that is the same in each corner.

Will assert in debug mode if the `radius` is negative in either x or y.

### RSuperellipse.fromLTRBAndCorners()

```dart
RSuperellipse.fromLTRBAndCorners(double left, double top, double right, double bottom, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

Construct a rounded rectangle from its left, top, right, and bottom edges, and topLeft, topRight, bottomRight, and bottomLeft radii.

The corner radii default to [Radius.zero], i.e. right-angled corners. Will assert in debug mode if any of the radii are negative in either x or y.

### RSuperellipse.fromRectAndCorners()

```dart
RSuperellipse.fromRectAndCorners(Rect rect, {Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomRight = Radius.zero, Radius bottomLeft = Radius.zero})
```

Construct a rounded rectangle from its bounding box and topLeft, topRight, bottomRight, and bottomLeft radii.

The corner radii default to [Radius.zero], i.e. right-angled corners. Will assert in debug mode if any of the radii are negative in either x or y.

### contains()

```dart
bool contains(Offset point)
```

Whether the point specified by the given offset (which is assumed to be relative to the origin) lies inside the rounded superellipse.

### zero

```dart
RSuperellipse zero
```

A rounded rectangle with all the values set to zero.

### lerp()

```dart
RSuperellipse? lerp(RSuperellipse? a, RSuperellipse? b, double t)
```

Linearly interpolate between two rounded superellipses.

If either is null, this function substitutes [RSuperellipse.zero] instead.

The `t` argument represents position on the timeline, with 0.0 meaning that the interpolation has not started, returning `a` (or something equivalent to `a`), 1.0 meaning that the interpolation has finished, returning `b` (or something equivalent to `b`), and values in between meaning that the interpolation is at the relevant point on the timeline between `a` and `b`. The interpolation can be extrapolated beyond 0.0 and 1.0, so negative values and values greater than 1.0 are valid (and can easily be generated by curves such as [Curves.elasticInOut]).

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

### toString()

```dart
String toString()
```

# RSTransform

```dart
class RSTransform {}
```

A transform consisting of a translation, a rotation, and a uniform scale.

Used by [Canvas.drawAtlas]. This is a more efficient way to represent these simple transformations than a full matrix.

### RSTransform()

```dart
RSTransform(double scos, double ssin, double tx, double ty)
```

Creates an RSTransform.

An [RSTransform] expresses the combination of a translation, a rotation around a particular point, and a scale factor.

The first argument, `scos`, is the cosine of the rotation, multiplied by the scale factor.

The second argument, `ssin`, is the sine of the rotation, multiplied by that same scale factor.

The third argument is the x coordinate of the translation, minus the `scos` argument multiplied by the x-coordinate of the rotation point, plus the `ssin` argument multiplied by the y-coordinate of the rotation point.

The fourth argument is the y coordinate of the translation, minus the `ssin` argument multiplied by the x-coordinate of the rotation point, minus the `scos` argument multiplied by the y-coordinate of the rotation point.

The [RSTransform.fromComponents] method may be a simpler way to construct these values. However, if there is a way to factor out the computations of the sine and cosine of the rotation so that they can be reused over multiple calls to this constructor, it may be more efficient to directly use this constructor instead.

### RSTransform.fromComponents()

```dart
RSTransform.fromComponents({required double rotation, required double scale, required double anchorX, required double anchorY, required double translateX, required double translateY})
```

Creates an RSTransform from its individual components.

The `rotation` parameter gives the rotation in radians.

The `scale` parameter describes the uniform scale factor.

The `anchorX` and `anchorY` parameters give the coordinate of the point around which to rotate.

The `translateX` and `translateY` parameters give the coordinate of the offset by which to translate.

This constructor computes the arguments of the [RSTransform.new] constructor and then defers to that constructor to actually create the object. If many [RSTransform] objects are being created and there is a way to factor out the computations of the sine and cosine of the rotation (which are computed each time this constructor is called) and reuse them over multiple [RSTransform] objects, it may be more efficient to directly use the more direct [RSTransform.new] constructor instead.

### scos

```dart
double get scos
```

The cosine of the rotation multiplied by the scale factor.

### ssin

```dart
double get ssin
```

The sine of the rotation multiplied by that same scale factor.

### tx

```dart
double get tx
```

The x coordinate of the translation, minus [scos] multiplied by the x-coordinate of the rotation point, plus [ssin] multiplied by the y-coordinate of the rotation point.

### ty

```dart
double get ty
```

The y coordinate of the translation, minus [ssin] multiplied by the x-coordinate of the rotation point, minus [scos] multiplied by the y-coordinate of the rotation point.
