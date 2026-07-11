# clampDouble()

```dart
double clampDouble(double x, double min, double max)
```

Same as [num.clamp] but optimized for a non-null [double].

This is faster because it avoids polymorphism, boxing, and special cases for floating point numbers.
