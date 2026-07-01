@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# AlignmentGeometry

```dart
abstract class AlignmentGeometry {}
```

Base class for [Alignment] that allows for text-direction aware resolution.

A property or argument of this type accepts classes created either with [Alignment] and its variants, or [AlignmentDirectional.new].

To convert an [AlignmentGeometry] object of indeterminate type into an [Alignment] object, call the [resolve] method.

### AlignmentGeometry()

```dart
AlignmentGeometry()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### AlignmentGeometry.xy()

```dart
AlignmentGeometry.xy(double x, double y)
```

Creates an [Alignment].

### AlignmentGeometry.directional()

```dart
AlignmentGeometry.directional(double start, double y)
```

Creates a directional alignment, or [AlignmentDirectional].

### topLeft

```dart
AlignmentGeometry topLeft
```

The top left corner.

See also:

- [Alignment.topLeft], which is the same thing.

### topCenter

```dart
AlignmentGeometry topCenter
```

The center point along the top edge.

See also:

- [Alignment.topCenter], which is the same thing.

### topRight

```dart
AlignmentGeometry topRight
```

The top right corner.

See also:

- [Alignment.topRight], which is the same thing.

### topStart

```dart
AlignmentGeometry topStart
```

The top corner on the "start" edge.

{@template flutter.painting.alignment.directional.start} This can be used to indicate an offset from the left in [TextDirection.ltr] text and an offset from the right in [TextDirection.rtl] text without having to be aware of the current text direction. {@endtemplate}

See also:

- [AlignmentDirectional.topStart], which is the same thing.

### topEnd

```dart
AlignmentGeometry topEnd
```

The top corner on the "end" edge.

{@template flutter.painting.alignment.directional.end} This can be used to indicate an offset from the right in [TextDirection.ltr] text and an offset from the left in [TextDirection.rtl] text without having to be aware of the current text direction. {@endtemplate}

See also:

- [AlignmentDirectional.topEnd], which is the same thing.

### centerLeft

```dart
AlignmentGeometry centerLeft
```

The center point along the left edge.

See also:

- [Alignment.centerLeft], which is the same thing.

### center

```dart
AlignmentGeometry center
```

The center point, both horizontally and vertically.

See also:

- [Alignment.center], which is the same thing.

### centerRight

```dart
AlignmentGeometry centerRight
```

The center point along the right edge.

See also:

- [Alignment.centerRight], which is the same thing.

### centerStart

```dart
AlignmentGeometry centerStart
```

The center point along the "start" edge.

{@macro flutter.painting.alignment.directional.start}

See also:

- [AlignmentDirectional.centerStart], which is the same thing.

### centerEnd

```dart
AlignmentGeometry centerEnd
```

The center point along the "end" edge.

{@macro flutter.painting.alignment.directional.end}

See also:

- [AlignmentDirectional.centerEnd], which is the same thing.

### bottomLeft

```dart
AlignmentGeometry bottomLeft
```

The bottom left corner.

See also:

- [Alignment.bottomLeft], which is the same thing.

### bottomCenter

```dart
AlignmentGeometry bottomCenter
```

The center point along the bottom edge.

See also:

- [Alignment.bottomCenter], which is the same thing.

### bottomRight

```dart
AlignmentGeometry bottomRight
```

The bottom right corner.

See also:

- [Alignment.bottomRight], which is the same thing.

### bottomStart

```dart
AlignmentGeometry bottomStart
```

The bottom corner on the "start" edge.

{@macro flutter.painting.alignment.directional.start}

See also:

- [AlignmentDirectional.bottomStart], which is the same thing.

### bottomEnd

```dart
AlignmentGeometry bottomEnd
```

The bottom corner on the "end" edge.

{@macro flutter.painting.alignment.directional.end}

See also:

- [AlignmentDirectional.bottomEnd], which is the same thing.

### add()

```dart
AlignmentGeometry add(AlignmentGeometry other)
```

Returns the sum of two [AlignmentGeometry] objects.

If you know you are adding two [Alignment] or two [AlignmentDirectional] objects, consider using the `+` operator instead, which always returns an object of the same type as the operands, and is typed accordingly.

If [add] is applied to two objects of the same type ([Alignment] or [AlignmentDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [Alignment] using [resolve].

### operator -()

```dart
AlignmentGeometry operator -()
```

Returns the negation of the given [AlignmentGeometry] object.

This is the same as multiplying the object by -1.0.

This operator returns an object of the same type as the operand.

### operator \*()

```dart
AlignmentGeometry operator *(double other)
```

Scales the [AlignmentGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### operator /()

```dart
AlignmentGeometry operator /(double other)
```

Divides the [AlignmentGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### operator ~/()

```dart
AlignmentGeometry operator ~/(double other)
```

Integer divides the [AlignmentGeometry] object in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### operator %()

```dart
AlignmentGeometry operator %(double other)
```

Computes the remainder in each dimension by the given factor.

This operator returns an object of the same type as the operand.

### lerp()

```dart
AlignmentGeometry? lerp(AlignmentGeometry? a, AlignmentGeometry? b, double t)
```

Linearly interpolate between two [AlignmentGeometry] objects.

If either is null, this function interpolates from [Alignment.center], and the result is an object of the same type as the non-null argument.

If [lerp] is applied to two objects of the same type ([Alignment] or [AlignmentDirectional]), an object of that type will be returned (though this is not reflected in the type system). Otherwise, an object representing a combination of both is returned. That object can be turned into a concrete [Alignment] using [resolve].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
Alignment resolve(TextDirection? direction)
```

Convert this instance into an [Alignment], which uses literal coordinates (the `x` coordinate being explicitly a distance from the left).

See also:

- [Alignment], for which this is a no-op (returns itself).
- [AlignmentDirectional], which flips the horizontal direction based on the `direction` argument.

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

# Alignment

```dart
class Alignment extends AlignmentGeometry {}
```

A point within a rectangle.

`Alignment(0.0, 0.0)` represents the center of the rectangle. The distance from -1.0 to +1.0 is the distance from one side of the rectangle to the other side of the rectangle. Therefore, 2.0 units horizontally (or vertically) is equivalent to the width (or height) of the rectangle.

`Alignment(-1.0, -1.0)` represents the top left of the rectangle.

`Alignment(1.0, 1.0)` represents the bottom right of the rectangle.

`Alignment(0.0, 3.0)` represents a point that is horizontally centered with respect to the rectangle and vertically below the bottom of the rectangle by the height of the rectangle.

`Alignment(0.0, -0.5)` represents a point that is horizontally centered with respect to the rectangle and vertically half way between the top edge and the center.

`Alignment(x, y)` in a rectangle with height h and width w describes the point (x _ w/2 + w/2, y _ h/2 + h/2) in the coordinate system of the rectangle.

[Alignment] uses visual coordinates, which means increasing [x] moves the point from left to right. To support layouts with a right-to-left [TextDirection], consider using [AlignmentDirectional], in which the direction the point moves when increasing the horizontal value depends on the [TextDirection].

A variety of widgets use [Alignment] in their configuration, most notably:

- [Align] positions a child according to an [Alignment].

See also:

- [AlignmentDirectional], which has a horizontal coordinate orientation that depends on the [TextDirection].
- [AlignmentGeometry], which is an abstract type that is agnostic as to whether the horizontal direction depends on the [TextDirection].

### Alignment()

```dart
Alignment(double x, double y)
```

Creates an alignment.

### x

```dart
double x
```

The distance fraction in the horizontal direction.

A value of -1.0 corresponds to the leftmost edge. A value of 1.0 corresponds to the rightmost edge. Values are not limited to that range; values less than -1.0 represent positions to the left of the left edge, and values greater than 1.0 represent positions to the right of the right edge.

### y

```dart
double y
```

The distance fraction in the vertical direction.

A value of -1.0 corresponds to the topmost edge. A value of 1.0 corresponds to the bottommost edge. Values are not limited to that range; values less than -1.0 represent positions above the top, and values greater than 1.0 represent positions below the bottom.

### topLeft

```dart
Alignment topLeft
```

The top left corner.

### topCenter

```dart
Alignment topCenter
```

The center point along the top edge.

### topRight

```dart
Alignment topRight
```

The top right corner.

### centerLeft

```dart
Alignment centerLeft
```

The center point along the left edge.

### center

```dart
Alignment center
```

The center point, both horizontally and vertically.

### centerRight

```dart
Alignment centerRight
```

The center point along the right edge.

### bottomLeft

```dart
Alignment bottomLeft
```

The bottom left corner.

### bottomCenter

```dart
Alignment bottomCenter
```

The center point along the bottom edge.

### bottomRight

```dart
Alignment bottomRight
```

The bottom right corner.

### add()

```dart
AlignmentGeometry add(AlignmentGeometry other)
```

### operator -()

```dart
Alignment operator -(Alignment other)
```

Returns the difference between two [Alignment]s.

### operator +()

```dart
Alignment operator +(Alignment other)
```

Returns the sum of two [Alignment]s.

### operator -()

```dart
Alignment operator -()
```

Returns the negation of the given [Alignment].

### operator \*()

```dart
Alignment operator *(double other)
```

Scales the [Alignment] in each dimension by the given factor.

### operator /()

```dart
Alignment operator /(double other)
```

Divides the [Alignment] in each dimension by the given factor.

### operator ~/()

```dart
Alignment operator ~/(double other)
```

Integer divides the [Alignment] in each dimension by the given factor.

### operator %()

```dart
Alignment operator %(double other)
```

Computes the remainder in each dimension by the given factor.

### alongOffset()

```dart
Offset alongOffset(Offset other)
```

Returns the offset that is this fraction in the direction of the given offset.

### alongSize()

```dart
Offset alongSize(Size other)
```

Returns the offset that is this fraction within the given size.

### withinRect()

```dart
Offset withinRect(Rect rect)
```

Returns the point that is this fraction within the given rect.

### inscribe()

```dart
Rect inscribe(Size size, Rect rect)
```

Returns a rect of the given size, aligned within given rect as specified by this alignment.

For example, a 100×100 size inscribed on a 200×200 rect using [Alignment.topLeft] would be the 100×100 rect at the top left of the 200×200 rect.

### lerp()

```dart
Alignment? lerp(Alignment? a, Alignment? b, double t)
```

Linearly interpolate between two [Alignment]s.

If either is null, this function interpolates from [Alignment.center].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
Alignment resolve(TextDirection? direction)
```

### toString()

```dart
String toString()
```

# AlignmentDirectional

```dart
class AlignmentDirectional extends AlignmentGeometry {}
```

An offset that's expressed as a fraction of a [Size], but whose horizontal component is dependent on the writing direction.

This can be used to indicate an offset from the left in [TextDirection.ltr] text and an offset from the right in [TextDirection.rtl] text without having to be aware of the current text direction.

See also:

- [Alignment], a variant that is defined in physical terms (i.e. whose horizontal component does not depend on the text direction).

### AlignmentDirectional()

```dart
AlignmentDirectional(double start, double y)
```

Creates a directional alignment.

### start

```dart
double start
```

The distance fraction in the horizontal direction.

A value of -1.0 corresponds to the edge on the "start" side, which is the left side in [TextDirection.ltr] contexts and the right side in [TextDirection.rtl] contexts. A value of 1.0 corresponds to the opposite edge, the "end" side. Values are not limited to that range; values less than -1.0 represent positions beyond the start edge, and values greater than 1.0 represent positions beyond the end edge.

This value is normalized into an [Alignment.x] value by the [resolve] method.

### y

```dart
double y
```

The distance fraction in the vertical direction.

A value of -1.0 corresponds to the topmost edge. A value of 1.0 corresponds to the bottommost edge. Values are not limited to that range; values less than -1.0 represent positions above the top, and values greater than 1.0 represent positions below the bottom.

This value is passed through to [Alignment.y] unmodified by the [resolve] method.

### topStart

```dart
AlignmentDirectional topStart
```

The top corner on the "start" side.

### topCenter

```dart
AlignmentDirectional topCenter
```

The center point along the top edge.

Consider using [Alignment.topCenter] instead, as it does not need to be [resolve]d to be used.

### topEnd

```dart
AlignmentDirectional topEnd
```

The top corner on the "end" side.

### centerStart

```dart
AlignmentDirectional centerStart
```

The center point along the "start" edge.

### center

```dart
AlignmentDirectional center
```

The center point, both horizontally and vertically.

Consider using [Alignment.center] instead, as it does not need to be [resolve]d to be used.

### centerEnd

```dart
AlignmentDirectional centerEnd
```

The center point along the "end" edge.

### bottomStart

```dart
AlignmentDirectional bottomStart
```

The bottom corner on the "start" side.

### bottomCenter

```dart
AlignmentDirectional bottomCenter
```

The center point along the bottom edge.

Consider using [Alignment.bottomCenter] instead, as it does not need to be [resolve]d to be used.

### bottomEnd

```dart
AlignmentDirectional bottomEnd
```

The bottom corner on the "end" side.

### add()

```dart
AlignmentGeometry add(AlignmentGeometry other)
```

### operator -()

```dart
AlignmentDirectional operator -(AlignmentDirectional other)
```

Returns the difference between two [AlignmentDirectional]s.

### operator +()

```dart
AlignmentDirectional operator +(AlignmentDirectional other)
```

Returns the sum of two [AlignmentDirectional]s.

### operator -()

```dart
AlignmentDirectional operator -()
```

Returns the negation of the given [AlignmentDirectional].

### operator \*()

```dart
AlignmentDirectional operator *(double other)
```

Scales the [AlignmentDirectional] in each dimension by the given factor.

### operator /()

```dart
AlignmentDirectional operator /(double other)
```

Divides the [AlignmentDirectional] in each dimension by the given factor.

### operator ~/()

```dart
AlignmentDirectional operator ~/(double other)
```

Integer divides the [AlignmentDirectional] in each dimension by the given factor.

### operator %()

```dart
AlignmentDirectional operator %(double other)
```

Computes the remainder in each dimension by the given factor.

### lerp()

```dart
AlignmentDirectional? lerp(AlignmentDirectional? a, AlignmentDirectional? b, double t)
```

Linearly interpolate between two [AlignmentDirectional]s.

If either is null, this function interpolates from [AlignmentDirectional.center].

{@macro dart.ui.shadow.lerp}

### resolve()

```dart
Alignment resolve(TextDirection? direction)
```

### toString()

```dart
String toString()
```

# TextAlignVertical

```dart
class TextAlignVertical {}
```

The vertical alignment of text within an input box.

A single [y] value that can range from -1.0 to 1.0. -1.0 aligns to the top of an input box so that the top of the first line of text fits within the box and its padding. 0.0 aligns to the center of the box. 1.0 aligns so that the bottom of the last line of text aligns with the bottom interior edge of the input box.

See also:

- [TextField.textAlignVertical], which is passed on to the [InputDecorator].
- [CupertinoTextField.textAlignVertical], which behaves in the same way as the parameter in TextField.
- [InputDecorator.textAlignVertical], which defines the alignment of prefix, input, and suffix within an [InputDecorator].

### TextAlignVertical()

```dart
TextAlignVertical({required double y})
```

Creates a TextAlignVertical from any y value between -1.0 and 1.0.

### y

```dart
double y
```

A value ranging from -1.0 to 1.0 that defines the topmost and bottommost locations of the top and bottom of the input box.

### top

```dart
TextAlignVertical top
```

Aligns a TextField's input Text with the topmost location within a TextField's input box.

### center

```dart
TextAlignVertical center
```

Aligns a TextField's input Text to the center of the TextField.

### bottom

```dart
TextAlignVertical bottom
```

Aligns a TextField's input Text with the bottommost location within a TextField.

### toString()

```dart
String toString()
```
