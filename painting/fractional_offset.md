# FractionalOffset

```dart
class FractionalOffset extends Alignment {}
```

An offset that's expressed as a fraction of a [Size].

`FractionalOffset(1.0, 0.0)` represents the top right of the [Size].

`FractionalOffset(0.0, 1.0)` represents the bottom left of the [Size].

`FractionalOffset(0.5, 2.0)` represents a point half way across the [Size], below the bottom of the rectangle by the height of the [Size].

The [FractionalOffset] class specifies offsets in terms of a distance from the top left, regardless of the [TextDirection].

## Design discussion

[FractionalOffset] and [Alignment] are two different representations of the same information: the location within a rectangle relative to the size of the rectangle. The difference between the two classes is in the coordinate system they use to represent the location.

[FractionalOffset] uses a coordinate system with an origin in the top-left corner of the rectangle whereas [Alignment] uses a coordinate system with an origin in the center of the rectangle.

Historically, [FractionalOffset] predates [Alignment]. When we attempted to make a version of [FractionalOffset] that adapted to the [TextDirection], we ran into difficulty because placing the origin in the top-left corner introduced a left-to-right bias that was hard to remove.

By placing the origin in the center, [Alignment] and [AlignmentDirectional] are able to use the same origin, which means we can use a linear function to resolve an [AlignmentDirectional] into an [Alignment] in both [TextDirection.rtl] and [TextDirection.ltr].

[Alignment] is better for most purposes than [FractionalOffset] and should be used instead of [FractionalOffset]. We continue to implement [FractionalOffset] to support code that predates [Alignment].

See also:

- [Alignment], which uses a coordinate system based on the center of the rectangle instead of the top left corner of the rectangle.

### FractionalOffset()

```dart
FractionalOffset(double dx, double dy)
```

Creates a fractional offset.

### FractionalOffset.fromOffsetAndSize()

```dart
FractionalOffset.fromOffsetAndSize(Offset offset, Size size)
```

Creates a fractional offset from a specific offset and size.

The returned [FractionalOffset] describes the position of the [Offset] in the [Size], as a fraction of the [Size].

### FractionalOffset.fromOffsetAndRect()

```dart
FractionalOffset.fromOffsetAndRect(Offset offset, Rect rect)
```

Creates a fractional offset from a specific offset and rectangle.

The offset is assumed to be relative to the same origin as the rectangle.

If the offset is relative to the top left of the rectangle, use [ FractionalOffset.fromOffsetAndSize] instead, passing `rect.size`.

The returned [FractionalOffset] describes the position of the [Offset] in the [Rect], as a fraction of the [Rect].

### dx

```dart
double get dx
```

The distance fraction in the horizontal direction.

A value of 0.0 corresponds to the leftmost edge. A value of 1.0 corresponds to the rightmost edge. Values are not limited to that range; negative values represent positions to the left of the left edge, and values greater than 1.0 represent positions to the right of the right edge.

### dy

```dart
double get dy
```

The distance fraction in the vertical direction.

A value of 0.0 corresponds to the topmost edge. A value of 1.0 corresponds to the bottommost edge. Values are not limited to that range; negative values represent positions above the top, and values greater than 1.0 represent positions below the bottom.

### topLeft

```dart
FractionalOffset topLeft
```

The top left corner.

### topCenter

```dart
FractionalOffset topCenter
```

The center point along the top edge.

### topRight

```dart
FractionalOffset topRight
```

The top right corner.

### centerLeft

```dart
FractionalOffset centerLeft
```

The center point along the left edge.

### center

```dart
FractionalOffset center
```

The center point, both horizontally and vertically.

### centerRight

```dart
FractionalOffset centerRight
```

The center point along the right edge.

### bottomLeft

```dart
FractionalOffset bottomLeft
```

The bottom left corner.

### bottomCenter

```dart
FractionalOffset bottomCenter
```

The center point along the bottom edge.

### bottomRight

```dart
FractionalOffset bottomRight
```

The bottom right corner.

### operator -()

```dart
Alignment operator -(Alignment other)
```

### operator +()

```dart
Alignment operator +(Alignment other)
```

### operator -()

```dart
FractionalOffset operator -()
```

### operator *()

```dart
FractionalOffset operator *(double other)
```

### operator /()

```dart
FractionalOffset operator /(double other)
```

### operator ~/()

```dart
FractionalOffset operator ~/(double other)
```

### operator %()

```dart
FractionalOffset operator %(double other)
```

### lerp()

```dart
FractionalOffset? lerp(FractionalOffset? a, FractionalOffset? b, double t)
```

Linearly interpolate between two [FractionalOffset]s.

If either is null, this function interpolates from [FractionalOffset.center].

{@macro dart.ui.shadow.lerp}

### toString()

```dart
String toString()
```
