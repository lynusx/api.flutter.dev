@docImport 'package:flutter/widgets.dart';

# MaterialPointArcTween

```dart
class MaterialPointArcTween extends Tween<Offset> {}
```

A [Tween] that interpolates an [Offset] along a circular arc.

This class specializes the interpolation of [Tween<Offset>] so that instead of a straight line, the intermediate points follow the arc of a circle in a manner consistent with Material Design principles.

The arc's radius is related to the bounding box that contains the [begin] and [end] points. If the bounding box is taller than it is wide, then the center of the circle will be horizontally aligned with the end point. Otherwise the center of the circle will be aligned with the begin point. The arc's sweep is always less than or equal to 90 degrees.

See also:

- [Tween], for a discussion on how to use interpolation objects.
- [MaterialRectArcTween], which extends this concept to interpolating [Rect]s.

### MaterialPointArcTween()

```dart
MaterialPointArcTween({dynamic begin, dynamic end})
```

Creates a [Tween] for animating [Offset]s along a circular arc.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### center

```dart
Offset? get center
```

The center of the circular arc, null if [begin] and [end] are horizontally or vertically aligned, or if either is null.

### radius

```dart
double? get radius
```

The radius of the circular arc, null if [begin] and [end] are horizontally or vertically aligned, or if either is null.

### beginAngle

```dart
double? get beginAngle
```

The beginning of the arc's sweep in radians, measured from the positive x axis. Positive angles turn clockwise.

This will be null if [begin] and [end] are horizontally or vertically aligned, or if either is null.

### endAngle

```dart
double? get endAngle
```

The end of the arc's sweep in radians, measured from the positive x axis. Positive angles turn clockwise.

This will be null if [begin] and [end] are horizontally or vertically aligned, or if either is null.

### begin

```dart
set begin(Offset? value)
```

### end

```dart
set end(Offset? value)
```

### lerp()

```dart
Offset lerp(double t)
```

### toString()

```dart
String toString()
```

# MaterialRectArcTween

```dart
class MaterialRectArcTween extends RectTween {}
```

A [Tween] that interpolates a [Rect] by having its opposite corners follow circular arcs.

This class specializes the interpolation of [Tween<Rect>] so that instead of growing or shrinking linearly, opposite corners of the rectangle follow arcs in a manner consistent with Material Design principles.

Specifically, the rectangle corners whose diagonals are closest to the overall direction of the animation follow arcs defined with [MaterialPointArcTween].

See also:

- [MaterialRectCenterArcTween], which interpolates a rect along a circular arc between the begin and end [Rect]'s centers.
- [Tween], for a discussion on how to use interpolation objects.
- [MaterialPointArcTween], the analog for [Offset] interpolation.
- [RectTween], which does a linear rectangle interpolation.
- [Hero.createRectTween], which can be used to specify the tween that defines a hero's path.

### MaterialRectArcTween()

```dart
MaterialRectArcTween({dynamic begin, dynamic end})
```

Creates a [Tween] for animating [Rect]s along a circular arc.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### beginArc

```dart
MaterialPointArcTween? get beginArc
```

The path of the corresponding [begin], [end] rectangle corners that lead the animation.

### endArc

```dart
MaterialPointArcTween? get endArc
```

The path of the corresponding [begin], [end] rectangle corners that trail the animation.

### begin

```dart
set begin(Rect? value)
```

### end

```dart
set end(Rect? value)
```

### lerp()

```dart
Rect lerp(double t)
```

### toString()

```dart
String toString()
```

# MaterialRectCenterArcTween

```dart
class MaterialRectCenterArcTween extends RectTween {}
```

A [Tween] that interpolates a [Rect] by moving it along a circular arc from [begin]'s [Rect.center] to [end]'s [Rect.center] while interpolating the rectangle's width and height.

The arc that defines that center of the interpolated rectangle as it morphs from [begin] to [end] is a [MaterialPointArcTween].

See also:

- [MaterialRectArcTween], A [Tween] that interpolates a [Rect] by having its opposite corners follow circular arcs.
- [Tween], for a discussion on how to use interpolation objects.
- [MaterialPointArcTween], the analog for [Offset] interpolation.
- [RectTween], which does a linear rectangle interpolation.
- [Hero.createRectTween], which can be used to specify the tween that defines a hero's path.

### MaterialRectCenterArcTween()

```dart
MaterialRectCenterArcTween({dynamic begin, dynamic end})
```

Creates a [Tween] for animating [Rect]s along a circular arc.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### centerArc

```dart
MaterialPointArcTween? get centerArc
```

If [begin] and [end] are non-null, returns a tween that interpolates along a circular arc between [begin]'s [Rect.center] and [end]'s [Rect.center].

### begin

```dart
set begin(Rect? value)
```

### end

```dart
set end(Rect? value)
```

### lerp()

```dart
Rect lerp(double t)
```

### toString()

```dart
String toString()
```
