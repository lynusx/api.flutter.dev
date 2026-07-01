@docImport 'package:flutter/material.dart';

# LinearBorderEdge

```dart
class LinearBorderEdge {}
```

Defines the relative size and alignment of one [LinearBorder] edge.

A [LinearBorder] defines a box outline as zero to four edges, each of which is rendered as a single line. The width and color of the lines is defined by [LinearBorder.side].

Each line's length is defined by [size], a value between 0.0 and 1.0 (the default) which defines the length as a percentage of the length of a box edge.

When [size] is less than 1.0, the line is aligned within the available space according to [alignment], a value between -1.0 and 1.0. The default is 0.0, which means centered, -1.0 means align on the "start" side, and 1.0 means align on the "end" side. The meaning of start and end depend on the current [TextDirection], see [Directionality].

### LinearBorderEdge()

```dart
LinearBorderEdge({double size = 1.0, double alignment = 0.0})
```

Defines one side of a [LinearBorder].

The values of [size] and [alignment] must be between 0.0 and 1.0, and -1.0 and 1.0 respectively.

### size

```dart
double size
```

A value between 0.0 and 1.0 that defines the length of the edge as a percentage of the length of the corresponding box edge. Default is 1.0.

### alignment

```dart
double alignment
```

A value between -1.0 and 1.0 that defines how edges for which [size] is less than 1.0 are aligned relative to the corresponding box edge.

- -1.0, aligned in the "start" direction. That's left for [TextDirection.ltr] and right for [TextDirection.rtl].
- 0.0, centered.
- 1.0, aligned in the "end" direction. That's right for [TextDirection.ltr] and left for [TextDirection.rtl].

### lerp()

```dart
LinearBorderEdge? lerp(LinearBorderEdge? a, LinearBorderEdge? b, double t)
```

Linearly interpolates between two [LinearBorder]s.

If both `a` and `b` are null then null is returned. If `a` is null then we interpolate to `b` varying [size] from 0.0 to `b.size`. If `b` is null then we interpolate from `a` varying size from `a.size` to zero. Otherwise both values are interpolated.

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

# LinearBorder

```dart
class LinearBorder extends OutlinedBorder {}
```

An [OutlinedBorder] like [BoxBorder] that allows one to define a rectangular (box) border in terms of zero to four [LinearBorderEdge]s, each of which is rendered as a single line.

The color and width of each line are defined by [side]. When [LinearBorder] is used with a class whose border sides and shape are defined by a [ButtonStyle], then a non-null [ButtonStyle.side] will override the one specified here. For example the [LinearBorder] in the [TextButton] example below adds a red underline to the button. This is because TextButton's `side` parameter overrides the `side` property of its [ButtonStyle.shape].

```dart
 TextButton(
   style: TextButton.styleFrom(
     side: const BorderSide(color: Colors.red),
     shape: const LinearBorder(
       side: BorderSide(color: Colors.blue),
       bottom: LinearBorderEdge(),
     ),
   ),
   onPressed: () { },
   child: const Text('Red LinearBorder'),
 )
```

This class resolves itself against the current [TextDirection] (see [Directionality]). Start and end values resolve to left and right for [TextDirection.ltr] and to right and left for [TextDirection.rtl].

Convenience constructors are included for the common case where just one edge is specified: [LinearBorder.start], [LinearBorder.end], [LinearBorder.top], [LinearBorder.bottom].

{@tool dartpad} This example shows how to draw different kinds of [LinearBorder]s.

** See code in examples/api/lib/painting/linear_border/linear_border.0.dart ** {@end-tool}

### LinearBorder()

```dart
LinearBorder({BorderSide side, LinearBorderEdge? start, LinearBorderEdge? end, LinearBorderEdge? top, LinearBorderEdge? bottom})
```

Creates a rectangular box border that's rendered as zero to four lines.

### LinearBorder.start()

```dart
LinearBorder.start({BorderSide side, double alignment = 0.0, double size = 1.0})
```

Creates a rectangular box border with an edge on the left for [TextDirection.ltr] or on the right for [TextDirection.rtl].

### LinearBorder.end()

```dart
LinearBorder.end({BorderSide side, double alignment = 0.0, double size = 1.0})
```

Creates a rectangular box border with an edge on the right for [TextDirection.ltr] or on the left for [TextDirection.rtl].

### LinearBorder.top()

```dart
LinearBorder.top({BorderSide side, double alignment = 0.0, double size = 1.0})
```

Creates a rectangular box border with an edge on the top.

### LinearBorder.bottom()

```dart
LinearBorder.bottom({BorderSide side, double alignment = 0.0, double size = 1.0})
```

Creates a rectangular box border with an edge on the bottom.

### none

```dart
LinearBorder none
```

No border.

### start

```dart
LinearBorderEdge? start
```

Defines the left edge for [TextDirection.ltr] or the right for [TextDirection.rtl].

### end

```dart
LinearBorderEdge? end
```

Defines the right edge for [TextDirection.ltr] or the left for [TextDirection.rtl].

### top

```dart
LinearBorderEdge? top
```

Defines the top edge.

### bottom

```dart
LinearBorderEdge? bottom
```

Defines the bottom edge.

### scale()

```dart
LinearBorder scale(double t)
```

### dimensions

```dart
EdgeInsetsGeometry get dimensions
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
LinearBorder copyWith({BorderSide? side, LinearBorderEdge? start, LinearBorderEdge? end, LinearBorderEdge? top, LinearBorderEdge? bottom})
```

Returns a copy of this LinearBorder with the given fields replaced with the new values.

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
