@docImport 'shape_decoration.dart';

# StadiumBorder

```dart
class StadiumBorder extends OutlinedBorder {}
```

A border that fits a stadium-shaped border (a box with semicircles on the ends) within the rectangle of the widget it is applied to.

Typically used with [ShapeDecoration] to draw a stadium border.

If the rectangle is taller than it is wide, then the semicircles will be on the top and bottom, and on the left and right otherwise.

See also:

- [BorderSide], which is used to describe the border of the stadium.

### StadiumBorder()

```dart
StadiumBorder({BorderSide side})
```

Create a stadium border.

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
StadiumBorder copyWith({BorderSide? side})
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
