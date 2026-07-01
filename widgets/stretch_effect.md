# StretchEffect

```dart
class StretchEffect extends StatelessWidget {}
```

A widget that applies a stretching visual effect to its child.

When shader-based effects are supported, this effect replicates the native Android stretch overscroll effect. Otherwise, a matrix transform provides an approximation.

Used by [StretchingOverscrollIndicator] widget.

### StretchEffect()

```dart
StretchEffect({dynamic key, double stretchStrength = 0.0, required Axis axis, required Widget child})
```

Creates a [StretchEffect] widget that applies a stretch effect when the user overscrolls horizontally or vertically.

The [stretchStrength] controls the intensity of the stretch effect and must be between -1.0 and 1.0.

### stretchStrength

```dart
double stretchStrength
```

The overscroll strength applied for the stretching effect.

The value should be between -1.0 and 1.0 inclusive.

For the horizontal axis:

- Positive values apply a pull/stretch from left to right, where 1.0 represents the maximum stretch to the right.
- Negative values apply a pull/stretch from right to left, where -1.0 represents the maximum stretch to the left.

For the vertical axis:

- Positive values apply a pull/stretch from top to bottom, where 1.0 represents the maximum stretch downward.
- Negative values apply a pull/stretch from bottom to top, where -1.0 represents the maximum stretch upward.

{@tool snippet} This example shows how to set the horizontal stretch strength to pull right.

```dart
const StretchEffect(
  stretchStrength: 0.5,
  axis: Axis.horizontal,
  child: Text('Hello, World!'),
);
```

{@end-tool}

### axis

```dart
Axis axis
```

The axis along which the stretching overscroll effect is applied.

Determines the direction of the stretch, either horizontal or vertical.

### child

```dart
Widget child
```

The child widget that the stretching overscroll effect applies to.

### build()

```dart
Widget build(BuildContext context)
```
