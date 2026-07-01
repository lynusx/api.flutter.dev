@docImport 'package:flutter/material.dart';

# TableBorder

```dart
class TableBorder {}
```

Border specification for [Table] widgets.

This is like [Border], with the addition of two sides: the inner horizontal borders between rows and the inner vertical borders between columns.

The sides are represented by [BorderSide] objects.

### TableBorder()

```dart
TableBorder({BorderSide top = BorderSide.none, BorderSide right = BorderSide.none, BorderSide bottom = BorderSide.none, BorderSide left = BorderSide.none, BorderSide horizontalInside = BorderSide.none, BorderSide verticalInside = BorderSide.none, BorderRadius borderRadius = BorderRadius.zero})
```

Creates a border for a table.

All the sides of the border default to [BorderSide.none].

### TableBorder.all()

```dart
TableBorder.all({Color color = const Color(0xFF000000), double width = 1.0, BorderStyle style = BorderStyle.solid, BorderRadius borderRadius = BorderRadius.zero})
```

A uniform border with all sides the same color and width.

The sides default to black solid borders, one logical pixel wide.

### TableBorder.symmetric()

```dart
TableBorder.symmetric({BorderSide inside = BorderSide.none, BorderSide outside = BorderSide.none, BorderRadius borderRadius = BorderRadius.zero})
```

Creates a border for a table where all the interior sides use the same styling and all the exterior sides use the same styling.

### top

```dart
BorderSide top
```

The top side of this border.

### right

```dart
BorderSide right
```

The right side of this border.

### bottom

```dart
BorderSide bottom
```

The bottom side of this border.

### left

```dart
BorderSide left
```

The left side of this border.

### horizontalInside

```dart
BorderSide horizontalInside
```

The horizontal interior sides of this border.

### verticalInside

```dart
BorderSide verticalInside
```

The vertical interior sides of this border.

### borderRadius

```dart
BorderRadius borderRadius
```

The [BorderRadius] to use when painting the corners of this border.

It is also applied to [DataTable]'s [Material].

### dimensions

```dart
EdgeInsets get dimensions
```

The widths of the sides of this border represented as an [EdgeInsets].

This can be used, for example, with a [Padding] widget to inset a box by the size of these borders.

### isUniform

```dart
bool get isUniform
```

Whether all the sides of the border (outside and inside) are identical. Uniform borders are typically more efficient to paint.

### scale()

```dart
TableBorder scale(double t)
```

Creates a copy of this border but with the widths scaled by the factor `t`.

The `t` argument represents the multiplicand, or the position on the timeline for an interpolation from nothing to `this`, with 0.0 meaning that the object returned should be the nil variant of this object, 1.0 meaning that no change should be applied, returning `this` (or something equivalent to `this`), and other values meaning that the object should be multiplied by `t`. Negative values are treated like zero.

Values for `t` are usually obtained from an [Animation<double>], such as an [AnimationController].

See also:

- [BorderSide.scale], which is used to implement this method.

### lerp()

```dart
TableBorder? lerp(TableBorder? a, TableBorder? b, double t)
```

Linearly interpolate between two table borders.

If a border is null, it is treated as having only [BorderSide.none] borders.

{@macro dart.ui.shadow.lerp}

### paint()

```dart
void paint(Canvas canvas, Rect rect, {required Iterable<double> rows, required Iterable<double> columns})
```

Paints the border around the given [Rect] on the given [Canvas], with the given rows and columns.

Uniform borders are more efficient to paint than more complex borders.

The `rows` argument specifies the vertical positions between the rows, relative to the given rectangle. For example, if the table contained two rows of height 100.0 each, then `rows` would contain a single value, 100.0, which is the vertical position between the two rows (relative to the top edge of `rect`).

The `columns` argument specifies the horizontal positions between the columns, relative to the given rectangle. For example, if the table contained two columns of height 100.0 each, then `columns` would contain a single value, 100.0, which is the vertical position between the two columns (relative to the left edge of `rect`).

The [verticalInside] border is only drawn if there are at least two columns. The [horizontalInside] border is only drawn if there are at least two rows. The horizontal borders are drawn after the vertical borders.

The outer borders (in the order [top], [right], [bottom], [left], with [left] above the others) are painted after the inner borders.

The paint order is particularly notable in the case of partially-transparent borders.

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
