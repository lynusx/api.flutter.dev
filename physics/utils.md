# nearEqual()

```dart
bool nearEqual(double? a, double? b, double epsilon)
```

Whether two doubles are within a given distance of each other.

The `epsilon` argument must be positive and not null. The `a` and `b` arguments may be null. A null value is only considered near-equal to another null value.

# nearZero()

```dart
bool nearZero(double a, double epsilon)
```

Whether a double is within a given distance of zero.

The epsilon argument must be positive.
