@docImport 'box_border.dart'; @docImport 'box_decoration.dart'; @docImport 'shape_decoration.dart';

# OvalBorder

```dart
class OvalBorder extends CircleBorder {}
```

A border that fits an elliptical shape.

Typically used with [ShapeDecoration] to draw an oval. Instead of centering the [Border] to a square, like [CircleBorder], it fills the available space, such that it touches the edges of the box. There is no difference between `CircleBorder(eccentricity = 1.0)` and `OvalBorder()`. [OvalBorder] works as an alias for users to discover this feature.

See also:

- [CircleBorder], which draws a circle, centering when the box is rectangular.
- [Border], which, when used with [BoxDecoration], can also describe an oval.

### OvalBorder()

```dart
OvalBorder({BorderSide side, double eccentricity = 1.0})
```

Create an oval border.

### scale()

```dart
ShapeBorder scale(double t)
```

### copyWith()

```dart
OvalBorder copyWith({BorderSide? side, double? eccentricity})
```

### lerpFrom()

```dart
ShapeBorder? lerpFrom(ShapeBorder? a, double t)
```

### lerpTo()

```dart
ShapeBorder? lerpTo(ShapeBorder? b, double t)
```

### toString()

```dart
String toString()
```
