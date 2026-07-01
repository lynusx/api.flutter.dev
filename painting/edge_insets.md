@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart';

# EdgeInsetsGeometry

```dart
abstract class EdgeInsetsGeometry {}
```

Base class for [EdgeInsets] that allows for text-direction aware resolution.

A property or argument of this type accepts classes created either with [ EdgeInsets.fromLTRB] and its variants, or [ EdgeInsetsDirectional.fromSTEB] and its variants.

To convert an [EdgeInsetsGeometry] object of indeterminate type into a [EdgeInsets] object, call the [resolve] method.

See also:

- [Padding], a widget that describes margins using [EdgeInsetsGeometry].

### EdgeInsetsGeometry()

```dart
EdgeInsetsGeometry()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### EdgeInsetsGeometry.all()

```dart
EdgeInsetsGeometry.all(double value)
```

Creates insets where all the offsets are `value`.

### EdgeInsetsGeometry.only()

```dart
EdgeInsetsGeometry.only({double left, double right, double top, double bottom})
```

Creates [EdgeInsets] with only the given values non-zero.

### EdgeInsetsGeometry.directional()

```dart
EdgeInsetsGeometry.directional({double start, double end, double top, double bottom})
```

Creates [EdgeInsetsDirectional] with only the given values non-zero.

### EdgeInsetsGeometry.symmetric()

```dart
EdgeInsetsGeometry.symmetric({double vertical, double horizontal})
```

Creates [EdgeInsets] with symmetrical vertical and horizontal offsets.

### EdgeInsetsGeometry.fromLTRB()

```dart
EdgeInsetsGeometry.fromLTRB(double left, double top, double right, double bottom)
```

Creates [EdgeInsets] from offsets from the left, top, right, and bottom.

### EdgeInsetsGeometry.fromViewPadding()

```dart
EdgeInsetsGeometry.fromViewPadding(ui.ViewPadding padding, double devicePixelRatio)
```

Creates [EdgeInsets] that match the given view padding.

If you need the current system padding or view insets in the context of a widget, consider using [MediaQuery.paddingOf] to obtain these values rather than using the value from a [FlutterView] directly, so that you get notified of changes.

### EdgeInsetsGeometry.fromSTEB()

```dart
EdgeInsetsGeometry.fromSTEB(double start, double top, double end, double bottom)
```

Creates [EdgeInsetsDirectional] from offsets from the start, top, end, and bottom.

### zero

```dart
EdgeInsetsGeometry zero
```

An [EdgeInsets] with zero offsets in each direction.

### infinity

```dart
EdgeInsetsGeometry infinity
```

An [EdgeInsetsGeometry] with infinite offsets in each direction.

Can be used as an infinite upper bound for [clamp].

### isNonNegative

```dart
bool get isNonNegative
```

Whether every dimension is non-negative.

### horizontal

```dart
double get horizontal
```

The total offset in the horizontal direction.

### vertical

```dart
double get vertical
```

The total offset in the vertical direction.

### along()

```dart
double along(Axis axis)
```

The total offset in the given direction.

### collapsedSize

```dart
Size get collapsedSize
```

The size that this [EdgeInsets] would occupy with an empty interior.

### flipped

```dart
EdgeInsetsGeometry get flipped
```

An [EdgeInsetsGeometry] with top and bottom, left and right, and start and end flipped.

### inflateSize()

```dart
Size inflateSize(Size size)
```

Returns a new size that is bigger than the given size by the amount of inset in the horizontal and vertical directions.

See also:

- [EdgeInsets.inflateRect], to inflate a [Rect] rather than a [Size] (for [EdgeInsetsDirectional], requires first calling [resolve] to establish how the start and end map to the left or right).
- [deflateSize], to deflate a [Size] rather than inflating it.

### deflateSize()

```dart
Size deflateSize(Size size)
```

Returns a new size that is smaller than the given size by the amount of inset in the horizontal and vertical directions.

If the argument is smaller than [collapsedSize], then the resulting size will have negative dimensions.

See also:

- [EdgeInsets.deflateRect], to deflate a [Rect] rather than a [Size]. (for [EdgeInsetsDirectional], requires first calling [resolve] to establish how the start and end map to the left or right).
- [inflateSize], to inflate a [Size] rather than deflating it.

### subtract()

```dart
EdgeInsetsGeometry subtract(EdgeInsetsGeometry other)
```

Returns the difference between two [EdgeInsetsGeometry] objects.

If you know you are applying this to two [EdgeInsets] or two [EdgeInsetsDirectional] objects, consider using the binary infix `-` operator instead, which always returns an object of the same type as the operands, and is typed accordingly.

If [subtract] is applied to two objects of the same type ([EdgeInsets] or [EdgeInsetsDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [EdgeInsets] using [resolve].

This method returns the same result as [add] applied to the result of negating the argument (using the prefix unary `-` operator or multiplying the argument by -1.0 using the `*` operator).

### add()

```dart
EdgeInsetsGeometry add(EdgeInsetsGeometry other)
```

Returns the sum of two [EdgeInsetsGeometry] objects.

If you know you are adding two [EdgeInsets] or two [EdgeInsetsDirectional] objects, consider using the `+` operator instead, which always returns an object of the same type as the operands, and is typed accordingly.

If [add] is applied to two objects of the same type ([EdgeInsets] or [EdgeInsetsDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [EdgeInsets] using [resolve].

### clamp()

```dart
EdgeInsetsGeometry clamp(EdgeInsetsGeometry min, EdgeInsetsGeometry max)
```

Returns a new [EdgeInsetsGeometry] object with all values greater than or equal to `min`, and less than or equal to `max`.

### operator -()

```dart
EdgeInsetsGeometry operator -()
```

Returns the [EdgeInsetsGeometry] object with each dimension negated.

This is the same as multiplying the object by -1.0.

This operator returns an object of the same type as the operand.

### operator *()

```dart
EdgeInsetsGeometry operator *(double other)
```

Scales the [EdgeInsetsGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### operator /()

```dart
EdgeInsetsGeometry operator /(double other)
```

Divides the [EdgeInsetsGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### operator ~/()

```dart
EdgeInsetsGeometry operator ~/(double other)
```

Integer divides the [EdgeInsetsGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

This operator may have unexpected results when applied to a mixture of [EdgeInsets] and [EdgeInsetsDirectional] objects.

### operator %()

```dart
EdgeInsetsGeometry operator %(double other)
```

Computes the remainder in each dimension by the given factor.

This operator returns an object of the same type as the operand.

This operator may have unexpected results when applied to a mixture of [EdgeInsets] and [EdgeInsetsDirectional] objects.

### lerp()

```dart
EdgeInsetsGeometry? lerp(EdgeInsetsGeometry? a, EdgeInsetsGeometry? b, double t)
```

Linearly interpolate between two [EdgeInsetsGeometry] objects.

If either is null, this function interpolates from [EdgeInsets.zero], and the result is an object of the same type as the non-null argument.

If [lerp] is applied to two objects of the same type ([EdgeInsets] or [EdgeInsetsDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [EdgeInsets] using [resolve].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
EdgeInsets resolve(TextDirection? direction)
```

Convert this instance into an [EdgeInsets], which uses literal coordinates (i.e. the `left` coordinate being explicitly a distance from the left, and the `right` coordinate being explicitly a distance from the right).

See also:

- [EdgeInsets], for which this is a no-op (returns itself).
- [EdgeInsetsDirectional], which flips the horizontal direction based on the `direction` argument.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# EdgeInsets

```dart
class EdgeInsets extends EdgeInsetsGeometry {}
```

An immutable set of offsets in each of the four cardinal directions.

Typically used for an offset from each of the four sides of a box. For example, the padding inside a box can be represented using this class.

The [EdgeInsets] class specifies offsets in terms of visual edges, left, top, right, and bottom. These values are not affected by the [TextDirection]. To support both left-to-right and right-to-left layouts, consider using [EdgeInsetsDirectional], which is expressed in terms of _start_, top, _end_, and bottom, where start and end are resolved in terms of a [TextDirection] (typically obtained from the ambient [Directionality]).

{@tool snippet}

Here are some examples of how to create [EdgeInsets] instances:

Typical eight-pixel margin on all sides:

```dart
const EdgeInsets.all(8.0)
```

{@end-tool} {@tool snippet}

Eight pixel margin above and below, no horizontal margins:

```dart
const EdgeInsets.symmetric(vertical: 8.0)
```

{@end-tool} {@tool snippet}

Left margin indent of 40 pixels:

```dart
const EdgeInsets.only(left: 40.0)
```

{@end-tool}

See also:

- [Padding], a widget that accepts [EdgeInsets] to describe its margins.
- [EdgeInsetsDirectional], which (for properties and arguments that accept the type [EdgeInsetsGeometry]) allows the horizontal insets to be specified in a [TextDirection]-aware manner.

### EdgeInsets.fromLTRB()

```dart
EdgeInsets.fromLTRB(double left, double top, double right, double bottom)
```

Creates insets from offsets from the left, top, right, and bottom.

### EdgeInsets.all()

```dart
EdgeInsets.all(double value)
```

Creates insets where all the offsets are `value`.

{@tool snippet}

Typical eight-pixel margin on all sides:

```dart
const EdgeInsets.all(8.0)
```

{@end-tool}

### EdgeInsets.only()

```dart
EdgeInsets.only({double left = 0.0, double top = 0.0, double right = 0.0, double bottom = 0.0})
```

Creates insets with only the given values non-zero.

{@tool snippet}

Left margin indent of 40 pixels:

```dart
const EdgeInsets.only(left: 40.0)
```

{@end-tool}

### EdgeInsets.symmetric()

```dart
EdgeInsets.symmetric({double vertical = 0.0, double horizontal = 0.0})
```

Creates insets with symmetrical vertical and horizontal offsets.

{@tool snippet}

Eight pixel margin above and below, no horizontal margins:

```dart
const EdgeInsets.symmetric(vertical: 8.0)
```

{@end-tool}

### EdgeInsets.fromViewPadding()

```dart
EdgeInsets.fromViewPadding(ui.ViewPadding padding, double devicePixelRatio)
```

Creates insets that match the given view padding.

If you need the current system padding or view insets in the context of a widget, consider using [MediaQuery.paddingOf] to obtain these values rather than using the value from a [FlutterView] directly, so that you get notified of changes.

### EdgeInsets.fromWindowPadding()

```dart
EdgeInsets.fromWindowPadding(ui.ViewPadding padding, double devicePixelRatio)
```

Deprecated. Will be removed in a future version of Flutter.

Use [EdgeInsets.fromViewPadding] instead.

### zero

```dart
EdgeInsets zero
```

An [EdgeInsets] with zero offsets in each direction.

### left

```dart
double left
```

The offset from the left.

### top

```dart
double top
```

The offset from the top.

### right

```dart
double right
```

The offset from the right.

### bottom

```dart
double bottom
```

The offset from the bottom.

### topLeft

```dart
Offset get topLeft
```

An Offset describing the vector from the top left of a rectangle to the top left of that rectangle inset by this object.

### topRight

```dart
Offset get topRight
```

An Offset describing the vector from the top right of a rectangle to the top right of that rectangle inset by this object.

### bottomLeft

```dart
Offset get bottomLeft
```

An Offset describing the vector from the bottom left of a rectangle to the bottom left of that rectangle inset by this object.

### bottomRight

```dart
Offset get bottomRight
```

An Offset describing the vector from the bottom right of a rectangle to the bottom right of that rectangle inset by this object.

### flipped

```dart
EdgeInsets get flipped
```

An [EdgeInsets] with top and bottom as well as left and right flipped.

### inflateRect()

```dart
Rect inflateRect(Rect rect)
```

Returns a new rect that is bigger than the given rect in each direction by the amount of inset in each direction. Specifically, the left edge of the rect is moved left by [left], the top edge of the rect is moved up by [top], the right edge of the rect is moved right by [right], and the bottom edge of the rect is moved down by [bottom].

See also:

- [inflateSize], to inflate a [Size] rather than a [Rect].
- [deflateRect], to deflate a [Rect] rather than inflating it.

### deflateRect()

```dart
Rect deflateRect(Rect rect)
```

Returns a new rect that is smaller than the given rect in each direction by the amount of inset in each direction. Specifically, the left edge of the rect is moved right by [left], the top edge of the rect is moved down by [top], the right edge of the rect is moved left by [right], and the bottom edge of the rect is moved up by [bottom].

If the argument's [Rect.size] is smaller than [collapsedSize], then the resulting rectangle will have negative dimensions.

See also:

- [deflateSize], to deflate a [Size] rather than a [Rect].
- [inflateRect], to inflate a [Rect] rather than deflating it.

### inflateRRect()

```dart
RRect inflateRRect(RRect rect)
```

Returns a new [RRect] expanded by this [EdgeInsets], increasing each corner's radius by the corresponding per-axis inset amounts (clamped at zero).

The resulting rectangle's left, top, right, and bottom edges are moved outward by the corresponding inset values. Each corner radius is also expanded by the corresponding inset values on both axes, ensuring that the corner shape is preserved while scaling appropriately.

Corner radii are adjusted per-axis and clamped to be non-negative. For example, the top-left corner radius is expanded by [left] horizontally and [top] vertically.

See also:

- [deflateRRect], to deflate an [RRect] rather than inflating it.
- [inflateRect], to inflate a [Rect] rather than an [RRect].
- [BorderRadius], which is used to define the corner radii of an [RRect].

### deflateRRect()

```dart
RRect deflateRRect(RRect rect)
```

Returns a new [RRect] shrunk by this [EdgeInsets], decreasing each corner's radius by the corresponding per-axis inset amounts (clamped at zero).

The resulting rectangle's left, top, right, and bottom edges are moved inward by the corresponding inset values. Each corner radius is also reduced by the corresponding inset values on both axes, maintaining the corner shape while scaling appropriately to the new size.

Corner radii are adjusted per-axis and clamped to be non-negative. For example, the top-left corner radius is reduced by [left] horizontally and [top] vertically. If either resulting dimension would be negative, the radius is clamped to zero in that direction.

See also:

- [inflateRRect], to inflate an [RRect] rather than deflating it.
- [deflateRect], to deflate a [Rect] rather than an [RRect].
- [BorderRadius], which is used to define the corner radii of an [RRect].

### subtract()

```dart
EdgeInsetsGeometry subtract(EdgeInsetsGeometry other)
```

### add()

```dart
EdgeInsetsGeometry add(EdgeInsetsGeometry other)
```

### clamp()

```dart
EdgeInsetsGeometry clamp(EdgeInsetsGeometry min, EdgeInsetsGeometry max)
```

### operator -()

```dart
EdgeInsets operator -(EdgeInsets other)
```

Returns the difference between two [EdgeInsets].

### operator +()

```dart
EdgeInsets operator +(EdgeInsets other)
```

Returns the sum of two [EdgeInsets].

### operator -()

```dart
EdgeInsets operator -()
```

Returns the [EdgeInsets] object with each dimension negated.

This is the same as multiplying the object by -1.0.

### operator *()

```dart
EdgeInsets operator *(double other)
```

Scales the [EdgeInsets] in each dimension by the given factor.

### operator /()

```dart
EdgeInsets operator /(double other)
```

Divides the [EdgeInsets] in each dimension by the given factor.

### operator ~/()

```dart
EdgeInsets operator ~/(double other)
```

Integer divides the [EdgeInsets] in each dimension by the given factor.

### operator %()

```dart
EdgeInsets operator %(double other)
```

Computes the remainder in each dimension by the given factor.

### lerp()

```dart
EdgeInsets? lerp(EdgeInsets? a, EdgeInsets? b, double t)
```

Linearly interpolate between two [EdgeInsets].

If either is null, this function interpolates from [EdgeInsets.zero].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
EdgeInsets resolve(TextDirection? direction)
```

### copyWith()

```dart
EdgeInsets copyWith({double? left, double? top, double? right, double? bottom})
```

Creates a copy of this EdgeInsets but with the given fields replaced with the new values.

# EdgeInsetsDirectional

```dart
class EdgeInsetsDirectional extends EdgeInsetsGeometry {}
```

An immutable set of offsets in each of the four cardinal directions, but whose horizontal components are dependent on the writing direction.

This can be used to indicate padding from the left in [TextDirection.ltr] text and padding from the right in [TextDirection.rtl] text without having to be aware of the current text direction.

See also:

- [EdgeInsets], a variant that uses physical labels (left and right instead of start and end).

### EdgeInsetsDirectional.fromSTEB()

```dart
EdgeInsetsDirectional.fromSTEB(double start, double top, double end, double bottom)
```

Creates insets from offsets from the start, top, end, and bottom.

### EdgeInsetsDirectional.only()

```dart
EdgeInsetsDirectional.only({double start = 0.0, double top = 0.0, double end = 0.0, double bottom = 0.0})
```

Creates insets with only the given values non-zero.

{@tool snippet}

A margin indent of 40 pixels on the leading side:

```dart
const EdgeInsetsDirectional.only(start: 40.0)
```

{@end-tool}

### EdgeInsetsDirectional.symmetric()

```dart
EdgeInsetsDirectional.symmetric({double horizontal = 0.0, double vertical = 0.0})
```

Creates insets with symmetric vertical and horizontal offsets.

This is equivalent to [EdgeInsets.symmetric], since the inset is the same with either [TextDirection]. This constructor is just a convenience for type compatibility.

{@tool snippet} Eight pixel margin above and below, no horizontal margins:

```dart
const EdgeInsetsDirectional.symmetric(vertical: 8.0)
```

{@end-tool}

### EdgeInsetsDirectional.all()

```dart
EdgeInsetsDirectional.all(double value)
```

Creates insets where all the offsets are `value`.

{@tool snippet}

Typical eight-pixel margin on all sides:

```dart
const EdgeInsetsDirectional.all(8.0)
```

{@end-tool}

### zero

```dart
EdgeInsetsDirectional zero
```

An [EdgeInsetsDirectional] with zero offsets in each direction.

Consider using [EdgeInsets.zero] instead, since that object has the same effect, but will be cheaper to [resolve].

### start

```dart
double start
```

The offset from the start side, the side from which the user will start reading text.

This value is normalized into an [EdgeInsets.left] or [EdgeInsets.right] value by the [resolve] method.

### top

```dart
double top
```

The offset from the top.

This value is passed through to [EdgeInsets.top] unmodified by the [resolve] method.

### end

```dart
double end
```

The offset from the end side, the side on which the user ends reading text.

This value is normalized into an [EdgeInsets.left] or [EdgeInsets.right] value by the [resolve] method.

### bottom

```dart
double bottom
```

The offset from the bottom.

This value is passed through to [EdgeInsets.bottom] unmodified by the [resolve] method.

### isNonNegative

```dart
bool get isNonNegative
```

### flipped

```dart
EdgeInsetsDirectional get flipped
```

An [EdgeInsetsDirectional] with [top] and [bottom] as well as [start] and [end] flipped.

### subtract()

```dart
EdgeInsetsGeometry subtract(EdgeInsetsGeometry other)
```

### add()

```dart
EdgeInsetsGeometry add(EdgeInsetsGeometry other)
```

### operator -()

```dart
EdgeInsetsDirectional operator -(EdgeInsetsDirectional other)
```

Returns the difference between two [EdgeInsetsDirectional] objects.

### operator +()

```dart
EdgeInsetsDirectional operator +(EdgeInsetsDirectional other)
```

Returns the sum of two [EdgeInsetsDirectional] objects.

### operator -()

```dart
EdgeInsetsDirectional operator -()
```

Returns the [EdgeInsetsDirectional] object with each dimension negated.

This is the same as multiplying the object by -1.0.

### operator *()

```dart
EdgeInsetsDirectional operator *(double other)
```

Scales the [EdgeInsetsDirectional] object in each dimension by the given factor.

### operator /()

```dart
EdgeInsetsDirectional operator /(double other)
```

Divides the [EdgeInsetsDirectional] object in each dimension by the given factor.

### operator ~/()

```dart
EdgeInsetsDirectional operator ~/(double other)
```

Integer divides the [EdgeInsetsDirectional] object in each dimension by the given factor.

### operator %()

```dart
EdgeInsetsDirectional operator %(double other)
```

Computes the remainder in each dimension by the given factor.

### lerp()

```dart
EdgeInsetsDirectional? lerp(EdgeInsetsDirectional? a, EdgeInsetsDirectional? b, double t)
```

Linearly interpolate between two [EdgeInsetsDirectional].

If either is null, this function interpolates from [EdgeInsetsDirectional.zero].

To interpolate between two [EdgeInsetsGeometry] objects of arbitrary type (either [EdgeInsets] or [EdgeInsetsDirectional]), consider the [EdgeInsetsGeometry.lerp] static method.

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
EdgeInsets resolve(TextDirection? direction)
```

### copyWith()

```dart
EdgeInsetsDirectional copyWith({double? start, double? top, double? end, double? bottom})
```

Creates a copy of this EdgeInsetsDirectional but with the given fields replaced with the new values.
