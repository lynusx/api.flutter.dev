@docImport 'package:flutter/widgets.dart';

@docImport 'box_border.dart'; @docImport 'box_decoration.dart';

# BorderRadiusGeometry

```dart
abstract class BorderRadiusGeometry {}
```

Base class for [BorderRadius] that allows for text-direction aware resolution.

A property or argument of this type accepts classes created either with [ BorderRadius.only] and its variants, or [BorderRadiusDirectional.only] and its variants.

To convert a [BorderRadiusGeometry] object of indeterminate type into a [BorderRadius] object, call the [resolve] method.

### BorderRadiusGeometry()

```dart
BorderRadiusGeometry()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### BorderRadiusGeometry.all()

```dart
BorderRadiusGeometry.all(Radius radius)
```

Creates a [BorderRadius] where all radii are `radius`.

### BorderRadiusGeometry.circular()

```dart
BorderRadiusGeometry.circular(double radius)
```

Creates a [BorderRadius] where all radii are [Radius.circular(radius)].

Consider using the `const` [BorderRadiusGeometry.all] constructor for better performance.

### BorderRadiusGeometry.horizontal()

```dart
BorderRadiusGeometry.horizontal({Radius? left, Radius? right, Radius? start, Radius? end})
```

Creates a horizontally symmetrical border radius.

Utilizing the `left` and `right` properties will return a [BorderRadius], while `start` and `end` will yield a [BorderRadiusDirectional]. These properties cannot be used interchangeably.

### BorderRadiusGeometry.only()

```dart
BorderRadiusGeometry.only({Radius topLeft, Radius topRight, Radius bottomLeft, Radius bottomRight})
```

Creates a [BorderRadius] with only the given non-zero values.

The other corners will be right angles.

### BorderRadiusGeometry.directional()

```dart
BorderRadiusGeometry.directional({Radius topStart, Radius topEnd, Radius bottomStart, Radius bottomEnd})
```

Creates a [BorderRadiusDirectional] with only the given non-zero values.

The other corners will be right angles.

### BorderRadiusGeometry.vertical()

```dart
BorderRadiusGeometry.vertical({Radius top, Radius bottom})
```

Creates a vertically symmetric [BorderRadius] where the top and bottom sides of the rectangle have the same radii.

### zero

```dart
BorderRadiusGeometry zero
```

A [BorderRadius] with all zero radii.

### subtract()

```dart
BorderRadiusGeometry subtract(BorderRadiusGeometry other)
```

Returns the difference between two [BorderRadiusGeometry] objects.

If you know you are applying this to two [BorderRadius] or two [BorderRadiusDirectional] objects, consider using the binary infix `-` operator instead, which always returns an object of the same type as the operands, and is typed accordingly.

If [subtract] is applied to two objects of the same type ([BorderRadius] or [BorderRadiusDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [BorderRadius] using [resolve].

This method returns the same result as [add] applied to the result of negating the argument (using the prefix unary `-` operator or multiplying the argument by -1.0 using the `*` operator).

### add()

```dart
BorderRadiusGeometry add(BorderRadiusGeometry other)
```

Returns the sum of two [BorderRadiusGeometry] objects.

If you know you are adding two [BorderRadius] or two [BorderRadiusDirectional] objects, consider using the `+` operator instead, which always returns an object of the same type as the operands, and is typed accordingly.

If [add] is applied to two objects of the same type ([BorderRadius] or [BorderRadiusDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [BorderRadius] using [resolve].

### operator -()

```dart
BorderRadiusGeometry operator -()
```

Returns the [BorderRadiusGeometry] object with each corner radius negated.

This is the same as multiplying the object by -1.0.

This operator returns an object of the same type as the operand.

### operator \*()

```dart
BorderRadiusGeometry operator *(double other)
```

Scales the [BorderRadiusGeometry] object's corners by the given factor.

This operator returns an object of the same type as the operand.

### operator /()

```dart
BorderRadiusGeometry operator /(double other)
```

Divides the [BorderRadiusGeometry] object's corners by the given factor.

This operator returns an object of the same type as the operand.

### operator ~/()

```dart
BorderRadiusGeometry operator ~/(double other)
```

Integer divides the [BorderRadiusGeometry] object's corners by the given factor.

This operator returns an object of the same type as the operand.

This operator may have unexpected results when applied to a mixture of [BorderRadius] and [BorderRadiusDirectional] objects.

### operator %()

```dart
BorderRadiusGeometry operator %(double other)
```

Computes the remainder of each corner by the given factor.

This operator returns an object of the same type as the operand.

This operator may have unexpected results when applied to a mixture of [BorderRadius] and [BorderRadiusDirectional] objects.

### lerp()

```dart
BorderRadiusGeometry? lerp(BorderRadiusGeometry? a, BorderRadiusGeometry? b, double t)
```

Linearly interpolate between two [BorderRadiusGeometry] objects.

If either is null, this function interpolates from [BorderRadius.zero], and the result is an object of the same type as the non-null argument. (If both are null, this returns null.)

If [lerp] is applied to two objects of the same type ([BorderRadius] or [BorderRadiusDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [BorderRadius] using [resolve].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
BorderRadius resolve(TextDirection? direction)
```

Convert this instance into a [BorderRadius], so that the radii are expressed for specific physical corners (top-left, top-right, etc) rather than in a direction-dependent manner.

See also:

- [BorderRadius], for which this is a no-op (returns itself).
- [BorderRadiusDirectional], which flips the horizontal direction based on the `direction` argument.

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

# BorderRadius

```dart
class BorderRadius extends BorderRadiusGeometry {}
```

An immutable set of radii for each corner of a rectangle.

Used by [BoxDecoration] when the shape is a [BoxShape.rectangle].

The [BorderRadius] class specifies offsets in terms of visual corners, e.g. [topLeft]. These values are not affected by the [TextDirection]. To support both left-to-right and right-to-left layouts, consider using [BorderRadiusDirectional], which is expressed in terms that are relative to a [TextDirection] (typically obtained from the ambient [Directionality]).

### BorderRadius.all()

```dart
BorderRadius.all(Radius radius)
```

Creates a border radius where all radii are [radius].

### BorderRadius.circular()

```dart
BorderRadius.circular(double radius)
```

Creates a border radius where all radii are [Radius.circular(radius)].

Consider using the `const` [BorderRadius.all] constructor for better performance.

### BorderRadius.vertical()

```dart
BorderRadius.vertical({Radius top = Radius.zero, Radius bottom = Radius.zero})
```

Creates a vertically symmetric border radius where the top and bottom sides of the rectangle have the same radii.

### BorderRadius.horizontal()

```dart
BorderRadius.horizontal({Radius left = Radius.zero, Radius right = Radius.zero})
```

Creates a horizontally symmetrical border radius where the left and right sides of the rectangle have the same radii.

### BorderRadius.only()

```dart
BorderRadius.only({Radius topLeft = Radius.zero, Radius topRight = Radius.zero, Radius bottomLeft = Radius.zero, Radius bottomRight = Radius.zero})
```

Creates a border radius with only the given non-zero values. The other corners will be right angles.

### copyWith()

```dart
BorderRadius copyWith({Radius? topLeft, Radius? topRight, Radius? bottomLeft, Radius? bottomRight})
```

Returns a copy of this BorderRadius with the given fields replaced with the new values.

### zero

```dart
BorderRadius zero
```

A border radius with all zero radii.

### topLeft

```dart
Radius topLeft
```

The top-left [Radius].

### topRight

```dart
Radius topRight
```

The top-right [Radius].

### bottomLeft

```dart
Radius bottomLeft
```

The bottom-left [Radius].

### bottomRight

```dart
Radius bottomRight
```

The bottom-right [Radius].

### toRRect()

```dart
RRect toRRect(Rect rect)
```

Creates an [RRect] from the current border radius and a [Rect].

If any of the radii have negative values in x or y, those values will be clamped to zero in order to produce a valid [RRect].

### toRSuperellipse()

```dart
RSuperellipse toRSuperellipse(Rect rect)
```

Creates an [RSuperellipse] from the current border radius and a [Rect].

If any of the radii have negative values in x or y, those values will be clamped to zero in order to produce a valid [RRect].

### subtract()

```dart
BorderRadiusGeometry subtract(BorderRadiusGeometry other)
```

### add()

```dart
BorderRadiusGeometry add(BorderRadiusGeometry other)
```

### operator -()

```dart
BorderRadius operator -(BorderRadius other)
```

Returns the difference between two [BorderRadius] objects.

### operator +()

```dart
BorderRadius operator +(BorderRadius other)
```

Returns the sum of two [BorderRadius] objects.

### operator -()

```dart
BorderRadius operator -()
```

Returns the [BorderRadius] object with each corner negated.

This is the same as multiplying the object by -1.0.

### operator \*()

```dart
BorderRadius operator *(double other)
```

Scales each corner of the [BorderRadius] by the given factor.

### operator /()

```dart
BorderRadius operator /(double other)
```

Divides each corner of the [BorderRadius] by the given factor.

### operator ~/()

```dart
BorderRadius operator ~/(double other)
```

Integer divides each corner of the [BorderRadius] by the given factor.

### operator %()

```dart
BorderRadius operator %(double other)
```

Computes the remainder of each corner by the given factor.

### lerp()

```dart
BorderRadius? lerp(BorderRadius? a, BorderRadius? b, double t)
```

Linearly interpolate between two [BorderRadius] objects.

If either is null, this function interpolates from [BorderRadius.zero].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
BorderRadius resolve(TextDirection? direction)
```

# BorderRadiusDirectional

```dart
class BorderRadiusDirectional extends BorderRadiusGeometry {}
```

An immutable set of radii for each corner of a rectangle, but with the corners specified in a manner dependent on the writing direction.

This can be used to specify a corner radius on the leading or trailing edge of a box, so that it flips to the other side when the text alignment flips (e.g. being on the top right in English text but the top left in Arabic text).

See also:

- [BorderRadius], a variant that uses physical labels (`topLeft` and `topRight` instead of `topStart` and `topEnd`).

### BorderRadiusDirectional.all()

```dart
BorderRadiusDirectional.all(Radius radius)
```

Creates a border radius where all radii are [radius].

### BorderRadiusDirectional.circular()

```dart
BorderRadiusDirectional.circular(double radius)
```

Creates a border radius where all radii are [Radius.circular(radius)].

Consider using the `const` [BorderRadiusDirectional.all] constructor for better performance.

### BorderRadiusDirectional.vertical()

```dart
BorderRadiusDirectional.vertical({Radius top = Radius.zero, Radius bottom = Radius.zero})
```

Creates a vertically symmetric border radius where the top and bottom sides of the rectangle have the same radii.

### BorderRadiusDirectional.horizontal()

```dart
BorderRadiusDirectional.horizontal({Radius start = Radius.zero, Radius end = Radius.zero})
```

Creates a horizontally symmetrical border radius where the start and end sides of the rectangle have the same radii.

### BorderRadiusDirectional.only()

```dart
BorderRadiusDirectional.only({Radius topStart = Radius.zero, Radius topEnd = Radius.zero, Radius bottomStart = Radius.zero, Radius bottomEnd = Radius.zero})
```

Creates a border radius with only the given non-zero values. The other corners will be right angles.

### zero

```dart
BorderRadiusDirectional zero
```

A border radius with all zero radii.

Consider using [BorderRadius.zero] instead, since that object has the same effect, but will be cheaper to [resolve].

### topStart

```dart
Radius topStart
```

The top-start [Radius].

### topEnd

```dart
Radius topEnd
```

The top-end [Radius].

### bottomStart

```dart
Radius bottomStart
```

The bottom-start [Radius].

### bottomEnd

```dart
Radius bottomEnd
```

The bottom-end [Radius].

### subtract()

```dart
BorderRadiusGeometry subtract(BorderRadiusGeometry other)
```

### add()

```dart
BorderRadiusGeometry add(BorderRadiusGeometry other)
```

### operator -()

```dart
BorderRadiusDirectional operator -(BorderRadiusDirectional other)
```

Returns the difference between two [BorderRadiusDirectional] objects.

### operator +()

```dart
BorderRadiusDirectional operator +(BorderRadiusDirectional other)
```

Returns the sum of two [BorderRadiusDirectional] objects.

### operator -()

```dart
BorderRadiusDirectional operator -()
```

Returns the [BorderRadiusDirectional] object with each corner negated.

This is the same as multiplying the object by -1.0.

### operator \*()

```dart
BorderRadiusDirectional operator *(double other)
```

Scales each corner of the [BorderRadiusDirectional] by the given factor.

### operator /()

```dart
BorderRadiusDirectional operator /(double other)
```

Divides each corner of the [BorderRadiusDirectional] by the given factor.

### operator ~/()

```dart
BorderRadiusDirectional operator ~/(double other)
```

Integer divides each corner of the [BorderRadiusDirectional] by the given factor.

### operator %()

```dart
BorderRadiusDirectional operator %(double other)
```

Computes the remainder of each corner by the given factor.

### lerp()

```dart
BorderRadiusDirectional? lerp(BorderRadiusDirectional? a, BorderRadiusDirectional? b, double t)
```

Linearly interpolate between two [BorderRadiusDirectional] objects.

If either is null, this function interpolates from [BorderRadiusDirectional.zero].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
BorderRadius resolve(TextDirection? direction)
```
