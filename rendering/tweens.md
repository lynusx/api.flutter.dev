# FractionalOffsetTween

```dart
class FractionalOffsetTween extends Tween<FractionalOffset?> {}
```

An interpolation between two fractional offsets.

This class specializes the interpolation of [Tween<FractionalOffset>] to be appropriate for fractional offsets.

See [Tween] for a discussion on how to use interpolation objects.

See also:

- [AlignmentTween], which interpolates between to [Alignment] objects.

### FractionalOffsetTween()

```dart
FractionalOffsetTween({dynamic begin, dynamic end})
```

Creates a fractional offset tween.

The [begin] and [end] properties may be null; the null value is treated as meaning the center.

### lerp()

```dart
FractionalOffset? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# AlignmentTween

```dart
class AlignmentTween extends Tween<Alignment> {}
```

An interpolation between two alignments.

This class specializes the interpolation of [Tween<Alignment>] to be appropriate for alignments.

See [Tween] for a discussion on how to use interpolation objects.

See also:

- [AlignmentGeometryTween], which interpolates between two [AlignmentGeometry] objects.

### AlignmentTween()

```dart
AlignmentTween({dynamic begin, dynamic end})
```

Creates a fractional offset tween.

The [begin] and [end] properties may be null; the null value is treated as meaning the center.

### lerp()

```dart
Alignment lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# AlignmentGeometryTween

```dart
class AlignmentGeometryTween extends Tween<AlignmentGeometry?> {}
```

An interpolation between two [AlignmentGeometry].

This class specializes the interpolation of [Tween<AlignmentGeometry>] to be appropriate for alignments.

See [Tween] for a discussion on how to use interpolation objects.

See also:

- [AlignmentTween], which interpolates between two [Alignment] objects.

### AlignmentGeometryTween()

```dart
AlignmentGeometryTween({dynamic begin, dynamic end})
```

Creates a fractional offset geometry tween.

The [begin] and [end] properties may be null; the null value is treated as meaning the center.

### lerp()

```dart
AlignmentGeometry? lerp(double t)
```

Returns the value this variable has at the given animation clock value.
