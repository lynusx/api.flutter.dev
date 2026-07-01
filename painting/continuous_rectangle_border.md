@docImport 'rounded_rectangle_border.dart';

# ContinuousRectangleBorder

```dart
class ContinuousRectangleBorder extends OutlinedBorder {}
```

A rectangular border with smooth continuous transitions between the straight sides and the rounded corners.

{@tool snippet}

```dart
Widget build(BuildContext context) {
  return Material(
    shape: ContinuousRectangleBorder(
      borderRadius: BorderRadius.circular(28.0),
    ),
  );
}
```

{@end-tool}

See also:

- [RoundedRectangleBorder] Which creates rectangles with rounded corners, however its straight sides change into a rounded corner with a circular radius in a step function instead of gradually like the [ContinuousRectangleBorder].

### ContinuousRectangleBorder()

```dart
ContinuousRectangleBorder({BorderSide side, BorderRadiusGeometry borderRadius = BorderRadius.zero})
```

Creates a [ContinuousRectangleBorder].

### borderRadius

```dart
BorderRadiusGeometry borderRadius
```

The radius for each corner.

Negative radius values are clamped to 0.0 by [getInnerPath] and [getOuterPath].

### dimensions

```dart
EdgeInsetsGeometry get dimensions
```

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

### copyWith()

```dart
ContinuousRectangleBorder copyWith({BorderSide? side, BorderRadiusGeometry? borderRadius})
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
