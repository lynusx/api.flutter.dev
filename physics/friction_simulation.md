# FrictionSimulation

```dart
class FrictionSimulation extends Simulation {}
```

A simulation that applies a drag to slow a particle down.

Models a particle affected by fluid drag, e.g. air resistance.

The simulation ends when the velocity of the particle drops to zero (within the current velocity [tolerance]).

### FrictionSimulation()

```dart
FrictionSimulation(double drag, double position, double velocity, {Tolerance tolerance, double constantDeceleration = 0})
```

Creates a [FrictionSimulation] with the given arguments, namely: the fluid drag coefficient _cₓ_, a unitless value; the initial position _x₀_, in the same length units as used for [x]; and the initial velocity _dx₀_, in the same velocity units as used for [dx].

### FrictionSimulation.through()

```dart
FrictionSimulation.through(double startPosition, double endPosition, double startVelocity, double endVelocity)
```

Creates a new friction simulation with its fluid drag coefficient (_cₓ_) set so as to ensure that the simulation starts and ends at the specified positions and velocities.

The positions must use the same units as expected from [x], and the velocities must use the same units as expected from [dx].

The sign of the start and end velocities must be the same, the magnitude of the start velocity must be greater than the magnitude of the end velocity, and the velocities must be in the direction appropriate for the particle to start from the start position and reach the end position.

### x()

```dart
double x(double time)
```

### dx()

```dart
double dx(double time)
```

### finalX

```dart
double get finalX
```

The value of [x] at `double.infinity`.

### timeAtX()

```dart
double timeAtX(double x)
```

The time at which the value of `x(time)` will equal [x].

Returns `double.infinity` if the simulation will never reach [x].

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```

# BoundedFrictionSimulation

```dart
class BoundedFrictionSimulation extends FrictionSimulation {}
```

A [FrictionSimulation] that clamps the modeled particle to a specific range of values.

Only the position is clamped. The velocity [dx] will continue to report unbounded simulated velocities once the particle has reached the bounds.

### BoundedFrictionSimulation()

```dart
BoundedFrictionSimulation(double drag, double position, double velocity, double _minX, double _maxX)
```

Creates a [BoundedFrictionSimulation] with the given arguments, namely: the fluid drag coefficient _cₓ_, a unitless value; the initial position _x₀_, in the same length units as used for [x]; the initial velocity _dx₀_, in the same velocity units as used for [dx], the minimum value for the position, and the maximum value for the position. The minimum and maximum values must be in the same units as the initial position, and the initial position must be within the given range.

### x()

```dart
double x(double time)
```

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```
