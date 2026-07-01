@docImport 'rounded_rectangle_border.dart';

# BeveledRectangleBorder

```dart
class BeveledRectangleBorder extends OutlinedBorder {}
```

A rectangular border with flattened or "beveled" corners.

The line segments that connect the rectangle's four sides will begin and at locations offset by the corresponding border radius, but not farther than the side's center. If all the border radii exceed the sides' half widths/heights the resulting shape is diamond made by connecting the centers of the sides.

### BeveledRectangleBorder()

```dart
BeveledRectangleBorder({BorderSide side, BorderRadiusGeometry borderRadius = BorderRadius.zero})
```

Creates a border like a [RoundedRectangleBorder] except that the corners are joined by straight lines instead of arcs.

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

The radii for each corner.

Each corner [Radius] defines the endpoints of a line segment that spans the corner. The endpoints are located in the same place as they would be for [RoundedRectangleBorder], but they're connected by a straight line instead of an arc.

Negative radius values are clamped to 0.0 by [getInnerPath] and [getOuterPath].

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

### copyWith()

```dart
BeveledRectangleBorder copyWith({BorderSide? side, BorderRadiusGeometry? borderRadius})
```

Returns a copy of this RoundedRectangleBorder with the given fields replaced with the new values.

### getInnerPath()

```dart
Path getInnerPath(Rect rect, {TextDirection? textDirection})
```

### getOuterPath()

```dart
Path getOuterPath(Rect rect, {TextDirection? textDirection})
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
