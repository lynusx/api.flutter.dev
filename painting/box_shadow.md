@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# BoxShadow

```dart
class BoxShadow extends ui.Shadow {}
```

A shadow cast by a box.

[BoxShadow] can cast non-rectangular shadows if the box is non-rectangular (e.g., has a border radius or a circular shape).

This class is similar to CSS box-shadow.

See also:

- [Canvas.drawShadow], which is a more efficient way to draw shadows.
- [PhysicalModel], a widget for showing shadows.
- [kElevationToShadow], for some predefined shadows used in Material Design.
- [Shadow], which is the parent class that lacks [spreadRadius].

### BoxShadow()

```dart
BoxShadow({dynamic color, dynamic offset, dynamic blurRadius, double spreadRadius = 0.0, BlurStyle blurStyle = BlurStyle.normal})
```

Creates a box shadow.

By default, the shadow is solid black with zero [offset], zero [blurRadius], zero [spreadRadius], and [BlurStyle.normal].

### spreadRadius

```dart
double spreadRadius
```

The amount the box should be inflated prior to applying the blur.

### blurStyle

```dart
BlurStyle blurStyle
```

The [BlurStyle] to use for this shadow.

Defaults to [BlurStyle.normal].

When [debugDisableShadows] is true, [toPaint] ignores the [blurStyle] and acts as if [BlurStyle.normal] was used.

### toPaint()

```dart
Paint toPaint()
```

Create the [Paint] object that corresponds to this shadow description.

The [offset] and [spreadRadius] are not represented in the [Paint] object. To honor those as well, the shape should be inflated by [spreadRadius] pixels in every direction and then translated by [offset] before being filled using this [Paint].

The [blurStyle] is ignored if [debugDisableShadows] is true. This causes an especially significant change to the rendering when [BlurStyle.outer] is used; the caller is responsible for adjusting for that case if necessary. (This only matters when using [debugDisableShadows], e.g. in tests that use [matchesGoldenFile].)

### scale()

```dart
BoxShadow scale(double factor)
```

Returns a new box shadow with its offset, blurRadius, and spreadRadius scaled by the given factor.

### copyWith()

```dart
BoxShadow copyWith({Color? color, Offset? offset, double? blurRadius, double? spreadRadius, BlurStyle? blurStyle})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
BoxShadow? lerp(BoxShadow? a, BoxShadow? b, double t)
```

Linearly interpolate between two box shadows.

If either box shadow is null, this function linearly interpolates from a box shadow that matches the other box shadow in color but has a zero offset and a zero blurRadius.

{@macro dart.ui.shadow.lerp}

### lerpList()

```dart
List<BoxShadow>? lerpList(List<BoxShadow>? a, List<BoxShadow>? b, double t)
```

Linearly interpolate between two lists of box shadows.

If the lists differ in length, excess items are lerped with null.

{@macro dart.ui.shadow.lerp}

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
