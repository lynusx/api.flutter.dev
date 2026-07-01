@docImport 'package:flutter/widgets.dart';

# SpringDescription

```dart
class SpringDescription {}
```

Structure that describes a spring's constants.

Used to configure a [SpringSimulation].

### SpringDescription()

```dart
SpringDescription({required double mass, required double stiffness, required double damping})
```

Creates a spring given the mass, stiffness, and the damping coefficient.

See [mass], [stiffness], and [damping] for the units of the arguments.

### SpringDescription.withDampingRatio()

```dart
SpringDescription.withDampingRatio({required double mass, required double stiffness, double ratio = 1.0})
```

Creates a spring given the mass (m), stiffness (k), and damping ratio (ζ). The damping ratio describes a gradual reduction in a spring oscillation. By using the damping ratio, you can define how rapidly the oscillations decay from one bounce to the next.

The damping ratio is especially useful when trying to determining the type of spring to create. A ratio of 1.0 creates a critically damped spring, > 1.0 creates an overdamped spring and < 1.0 an underdamped one.

See [mass] and [stiffness] for the units for those arguments. The damping ratio is unitless.

### SpringDescription.withDurationAndBounce()

```dart
SpringDescription.withDurationAndBounce({Duration duration = const Duration(milliseconds: 500), double bounce = 0.0})
```

Creates a [SpringDescription] based on a desired animation duration and bounce.

This provides an intuitive way to define a spring based on its visual properties, [duration] and [bounce]. Check the properties' documentation for their definition.

This constructor produces the same result as SwiftUI's `spring(duration:bounce:blendDuration:)` animation.

{@tool snippet}

```dart
final SpringDescription spring = SpringDescription.withDurationAndBounce(
  duration: const Duration(milliseconds: 300),
  bounce: 0.3,
);
```

{@end-tool}

See also:

- [SpringDescription], which creates a spring by explicitly providing physical parameters.
- [SpringDescription.withDampingRatio], which creates a spring with a damping ratio and other physical parameters.

### mass

```dart
double mass
```

The mass of the spring (m).

The units are arbitrary, but all springs within a system should use the same mass units.

The greater the mass, the larger the amplitude of oscillation, and the longer the time to return to the equilibrium position.

### stiffness

```dart
double stiffness
```

The spring constant (k).

The units of stiffness are M/T², where M is the mass unit used for the value of the [mass] property, and T is the time unit used for driving the [SpringSimulation].

Stiffness defines the spring constant, which measures the strength of the spring. A stiff spring applies more force to the object that is attached for some deviation from the rest position.

### damping

```dart
double damping
```

The damping coefficient (c).

It is a pure number without physical meaning and describes the oscillation and decay of a system after being disturbed. The larger the damping, the fewer oscillations and smaller the amplitude of the elastic motion.

Do not confuse the damping _coefficient_ (c) with the damping _ratio_ (ζ). To create a [SpringDescription] with a damping ratio, use the [ SpringDescription.withDampingRatio] constructor.

The units of the damping coefficient are M/T, where M is the mass unit used for the value of the [mass] property, and T is the time unit used for driving the [SpringSimulation].

### duration

```dart
Duration get duration
```

The duration parameter used in [SpringDescription.withDurationAndBounce].

This value defines the perceptual duration of the spring, controlling its overall pace. It is approximately equal to the time it takes for the spring to settle, but for highly bouncy springs, it instead corresponds to the oscillation period.

This duration does not represent the exact time for the spring to stop moving. For example, when [bounce] is 1, the spring oscillates indefinitely, even though [duration] has a finite value. To determine when the motion has effectively stopped within a certain tolerance, use [SpringSimulation.isDone].

Defaults to 0.5 seconds.

### bounce

```dart
double get bounce
```

The bounce parameter used in [SpringDescription.withDurationAndBounce].

This value controls how bouncy the spring is:

- A value of 0 results in a critically damped spring with no oscillation.
- Values between 0 and 1 produce underdamping, where the spring oscillates a few times before settling. A value of 1 represents an undamped spring that oscillates indefinitely.
- Negative values indicate overdamping, where the motion is slow and resistive, like moving through a thick fluid.

Defaults to 0.

### toString()

```dart
String toString()
```

# SpringType

```dart
enum SpringType {}
```

The kind of spring solution that the [SpringSimulation] is using to simulate the spring.

See [SpringSimulation.type].

A spring that does not bounce and returns to its rest position in the shortest possible time.

A spring that bounces.

A spring that does not bounce but takes longer to return to its rest position than a [criticallyDamped] one.

# SpringSimulation

```dart
class SpringSimulation extends Simulation {}
```

A spring simulation.

Models a particle attached to a spring that follows Hooke's law.

{@tool snippet}

This method triggers an [AnimationController] (a previously constructed `_controller` field) to simulate a spring oscillation.

```dart
void _startSpringMotion() {
  _controller.animateWith(SpringSimulation(
    const SpringDescription(
      mass: 1.0,
      stiffness: 300.0,
      damping: 15.0,
    ),
    0.0, // starting position
    1.0, // ending position
    0.0, // starting velocity
  ));
}
```

{@end-tool}

This [AnimationController] could be used with an [AnimatedBuilder] to animate the position of a child as if it were attached to a spring.

### SpringSimulation()

```dart
SpringSimulation(SpringDescription spring, double start, double end, double velocity, {bool snapToEnd = false, Tolerance tolerance})
```

Creates a spring simulation from the provided spring description, start distance, end distance, and initial velocity.

The units for the start and end distance arguments are arbitrary, but must be consistent with the units used for other lengths in the system.

The units for the velocity are L/T, where L is the aforementioned arbitrary unit of length, and T is the time unit used for driving the [SpringSimulation].

If `snapToEnd` is true, [x] will be set to `end` and [dx] to 0 when [isDone] returns true. This is useful for transitions that require the simulation to stop exactly at the end value, since the spring may not naturally reach the target precisely. Defaults to false.

### type

```dart
SpringType get type
```

The kind of spring being simulated, for debugging purposes.

This is derived from the [SpringDescription] provided to the [ SpringSimulation] constructor.

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

# ScrollSpringSimulation

```dart
class ScrollSpringSimulation extends SpringSimulation {}
```

A [SpringSimulation] where the value of [x] is guaranteed to have exactly the end value when the simulation [isDone].

### ScrollSpringSimulation()

```dart
ScrollSpringSimulation(SpringDescription spring, double start, double end, double velocity, {Tolerance tolerance})
```

Creates a spring simulation from the provided spring description, start distance, end distance, and initial velocity.

See the [SpringSimulation.new] constructor on the superclass for a discussion of the arguments' units.

### x()

```dart
double x(double time)
```
