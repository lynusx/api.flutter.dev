@docImport 'box_border.dart'; @docImport 'box_decoration.dart'; @docImport 'oval_border.dart'; @docImport 'shape_decoration.dart';

# CircleBorder

```dart
class CircleBorder extends OutlinedBorder {}
```

A border that fits a circle within the available space.

Typically used with [ShapeDecoration] to draw a circle.

The [dimensions] assume that the border is being used in a square space. When applied to a rectangular space, the border paints in the center of the rectangle.

The [eccentricity] parameter describes how much a circle will deform to fit the rectangle it is a border for. A value of zero implies no deformation (a circle touching at least two sides of the rectangle), a value of one implies full deformation (an oval touching all sides of the rectangle).

See also:

- [OvalBorder], which draws a Circle touching all the edges of the box.
- [BorderSide], which is used to describe each side of the box.
- [Border], which, when used with [BoxDecoration], can also describe a circle.

### CircleBorder()

```dart
CircleBorder({BorderSide side, double eccentricity = 0.0})
```

Create a circle border.

### eccentricity

```dart
double eccentricity
```

Defines the ratio (0.0-1.0) from which the border will deform to fit a rectangle. When 0.0, it draws a circle touching at least two sides of the rectangle. When 1.0, it draws an oval touching all sides of the rectangle.

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

### copyWith()

```dart
CircleBorder copyWith({BorderSide? side, double? eccentricity})
```

### paint()

```dart
void paint(Canvas canvas, Rect rect, {TextDirection? textDirection})
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
