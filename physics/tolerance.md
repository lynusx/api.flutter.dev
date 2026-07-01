# Tolerance

```dart
class Tolerance {}
```

Structure that specifies maximum allowable magnitudes for distances, durations, and velocity differences to be considered equal.

### Tolerance()

```dart
Tolerance({double distance = _epsilonDefault, double time = _epsilonDefault, double velocity = _epsilonDefault})
```

Creates a [Tolerance] object. By default, the distance, time, and velocity tolerances are all ±0.001; the constructor arguments override this.

The arguments should all be positive values.

### defaultTolerance

```dart
Tolerance defaultTolerance
```

A default tolerance of 0.001 for all three values.

### distance

```dart
double distance
```

The magnitude of the maximum distance between two points for them to be considered within tolerance.

The units for the distance tolerance must be the same as the units used for the distances that are to be compared to this tolerance.

### time

```dart
double time
```

The magnitude of the maximum duration between two times for them to be considered within tolerance.

The units for the time tolerance must be the same as the units used for the times that are to be compared to this tolerance.

### velocity

```dart
double velocity
```

The magnitude of the maximum difference between two velocities for them to be considered within tolerance.

The units for the velocity tolerance must be the same as the units used for the velocities that are to be compared to this tolerance.

### toString()

```dart
String toString()
```
