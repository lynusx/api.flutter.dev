@docImport 'box_border.dart'; @docImport 'box_decoration.dart'; @docImport 'shape_decoration.dart';

# RoundedRectangleBorder

```dart
class RoundedRectangleBorder extends OutlinedBorder with _RRectLikeBorder {}
```

A rectangular border with rounded corners.

Typically used with [ShapeDecoration] to draw a box with a rounded rectangle.

This shape can interpolate to and from [CircleBorder].

See also:

- [BorderSide], which is used to describe each side of the box.
- [Border], which, when used with [BoxDecoration], can also describe a rounded rectangle.
- [RoundedSuperellipseBorder], which uses a smoother shape similar to the one used in iOS design.

### RoundedRectangleBorder()

```dart
RoundedRectangleBorder({BorderSide side, BorderRadiusGeometry borderRadius = BorderRadius.zero})
```

Creates a rounded rectangle border.

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

The radii for each corner.

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
RoundedRectangleBorder copyWith({BorderSide? side, BorderRadiusGeometry? borderRadius})
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

### paintInterior()

```dart
void paintInterior(Canvas canvas, Rect rect, Paint paint, {TextDirection? textDirection})
```

### preferPaintInterior

```dart
bool get preferPaintInterior
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

# RoundedSuperellipseBorder

```dart
class RoundedSuperellipseBorder extends OutlinedBorder with _RRectLikeBorder {}
```

A rectangular border with rounded corners following the shape of an [RSuperellipse].

Typically used with [ShapeDecoration] to draw a box that mimics the rounded rectangle style commonly seen in iOS design.

{@tool dartpad} This interactive example demonstrates the use of [RoundedSuperellipseBorder].

Toggle the switch at the top to compare [RoundedSuperellipseBorder] with the traditional [RoundedRectangleBorder] and observe their subtle visual differences.

Use the sliders below to adjust the border's thickness and radius to explore its behavior in real-time.

** See code in examples/api/lib/painting/rounded_superellipse_border/rounded_superellipse_border.0.dart ** {@end-tool}

See also:

- [RSuperellipse], which defines the shape.
- [RoundedRectangleBorder], which uses the traditional [RRect] shape.

### RoundedSuperellipseBorder()

```dart
RoundedSuperellipseBorder({BorderSide side, BorderRadiusGeometry? borderRadius})
```

Creates a rounded rectangle border.

If `borderRadius` is not specified or null, it defaults to [BorderRadius.zero].

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

The radii for each corner.

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
RoundedSuperellipseBorder copyWith({BorderSide? side, BorderRadiusGeometry? borderRadius})
```

Returns a copy of this RoundedSuperellipseBorder with the given fields replaced with the new values.

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
