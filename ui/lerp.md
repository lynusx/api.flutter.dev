# lerpDouble()

```dart
double? lerpDouble(num? a, num? b, double t)
```

Linearly interpolate between two numbers, `a` and `b`, by an extrapolation factor `t`.

When `a` and `b` are equal or both NaN, `a` is returned. Otherwise, `a`, `b`, and `t` are required to be finite or null, and the result of `a + (b - a) * t` is returned, where nulls are defaulted to 0.0.
