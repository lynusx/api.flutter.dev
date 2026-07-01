@docImport 'scroll_activity.dart';

# BouncingScrollSimulation

```dart
class BouncingScrollSimulation extends Simulation {}
```

An implementation of scroll physics that matches iOS.

See also:

- [ClampingScrollSimulation], which implements Android scroll physics.

### BouncingScrollSimulation()

```dart
BouncingScrollSimulation({required double position, required double velocity, required double leadingExtent, required double trailingExtent, required SpringDescription spring, double constantDeceleration = 0, dynamic tolerance})
```

Creates a simulation group for scrolling on iOS, with the given parameters.

The position and velocity arguments must use the same units as will be expected from the [x] and [dx] methods respectively (typically logical pixels and logical pixels per second respectively).

The leading and trailing extents must use the unit of length, the same unit as used for the position argument and as expected from the [x] method (typically logical pixels).

The units used with the provided [SpringDescription] must similarly be consistent with the other arguments. A default set of constants is used for the `spring` description if it is omitted; these defaults assume that the unit of length is the logical pixel.

### maxSpringTransferVelocity

```dart
double maxSpringTransferVelocity
```

The maximum velocity that can be transferred from the inertia of a ballistic scroll into overscroll.

### leadingExtent

```dart
double leadingExtent
```

When [x] falls below this value the simulation switches from an internal friction model to a spring model which causes [x] to "spring" back to [leadingExtent].

### trailingExtent

```dart
double trailingExtent
```

When [x] exceeds this value the simulation switches from an internal friction model to a spring model which causes [x] to "spring" back to [trailingExtent].

### spring

```dart
SpringDescription spring
```

The spring used to return [x] to either [leadingExtent] or [trailingExtent].

### x()

```dart
double x(double time)
```

### dx()

```dart
double dx(double time)
```

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```

# ClampingScrollSimulation

```dart
class ClampingScrollSimulation extends Simulation {}
```

An implementation of scroll physics that aligns with Android.

For any value of [velocity], this travels the same total distance as the Android scroll physics.

This scroll physics has been adjusted relative to Android's in order to make it ballistic, meaning that the deceleration at any moment is a function only of the current velocity [dx] and does not depend on how long ago the simulation was started. (This is required by Flutter's scrolling protocol, where [ScrollActivityDelegate.goBallistic] may restart a scroll activity using only its current velocity and the scroll position's own state.) Compared to this scroll physics, Android's moves faster at the very beginning, then slower, and it ends at the same place but a little later.

Times are measured in seconds, and positions in logical pixels.

See also:

- [BouncingScrollSimulation], which implements iOS scroll physics.

### ClampingScrollSimulation()

```dart
ClampingScrollSimulation({required double position, required double velocity, double friction = 0.015, dynamic tolerance})
```

Creates a scroll physics simulation that aligns with Android scrolling.

### position

```dart
double position
```

The position of the particle at the beginning of the simulation, in logical pixels.

### velocity

```dart
double velocity
```

The velocity at which the particle is traveling at the beginning of the simulation, in logical pixels per second.

### friction

```dart
double friction
```

The amount of friction the particle experiences as it travels.

The more friction the particle experiences, the sooner it stops and the less far it travels.

The default value causes the particle to travel the same total distance as in the Android scroll physics.

### x()

```dart
double x(double time)
```

### dx()

```dart
double dx(double time)
```

### isDone()

```dart
bool isDone(double time)
```
