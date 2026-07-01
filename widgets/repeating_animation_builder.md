# RepeatMode

```dart
enum RepeatMode {}
```

Configures how [RepeatingAnimationBuilder] loops its animation.

Each iteration starts over from the beginning once 1.0 is reached.

Each iteration runs forward, then reverses back to the beginning.

# RepeatingAnimationBuilder

```dart
class RepeatingAnimationBuilder<T extends Object> extends StatefulWidget {}
```

Widget that animates an [Animatable] value and repeats indefinitely.

The animation continuously cycles from the value produced by the [Animatable] at 0.0 to the value at 1.0. The [builder] receives the current value produced by this [Animatable] and builds the child from it. When the animation reaches 1.0, it either restarts from 0.0 or reverses direction, based on the configured [repeatMode]. When [paused] is true, the animation stops at its current value.

{@tool dartpad} This example shows a continuously rotating square that can be paused and resumed.

** See code in examples/api/lib/widgets/repeating_animation_builder/repeating_animation_builder.0.dart ** {@end-tool}

For more complex, stateful, or coordinated animations, consider managing an [AnimationController] directly and composing it with [AnimatedBuilder] or an [AnimatedWidget].

See also:

- [TweenAnimationBuilder], which animates a tween value once.
- [AnimationController.repeat], the underlying mechanism.

### RepeatingAnimationBuilder()

```dart
RepeatingAnimationBuilder({dynamic key, required Animatable<T> animatable, required Duration duration, Curve curve = Curves.linear, RepeatMode repeatMode = RepeatMode.restart, bool paused = false, required ValueWidgetBuilder<T> builder, Widget? child})
```

Creates a widget that repeats an animation.

### animatable

```dart
Animatable<T> animatable
```

The animatable to drive repeatedly.

Typically this is a [Tween] or a [TweenSequence], but any [Animatable] that produces values of type [T] is accepted.

### duration

```dart
Duration duration
```

The duration of the animation.

If [repeatMode] is [RepeatMode.restart], this is the duration of the entire animation sequence from 0.0 to 1.0.

If [repeatMode] is [RepeatMode.reverse], both the forward segment (0.0 to 1.0) and the backward segment (1.0 to 0.0) will each take this duration separately. The total time for one complete forward-and-reverse cycle will be twice this value.

### curve

```dart
Curve curve
```

The curve applied to the animation input before it is passed to the [animatable].

In other words, the curve transforms the controller's 0.0..1.0 timeline and the resulting value is then fed into the [animatable].

Defaults to [Curves.linear].

### builder

```dart
ValueWidgetBuilder<T> builder
```

A builder that creates the animated widget subtree.

The builder is called every time the animation value changes. The optional child can be used to avoid unnecessary rebuilds if a part of the subtree does not depend on the animation.

### child

```dart
Widget? child
```

An optional widget to pass to the builder.

If a builder callback's return value contains a subtree that does not depend on the animation, it's more efficient to build that subtree once instead of rebuilding it on every animation tick.

If the pre-built subtree is passed as the child parameter, the [RepeatingAnimationBuilder] will pass it back to the [builder] function so that it can be incorporated into the build.

Using this pre-built child is entirely optional, but can improve performance significantly in some cases and is therefore a good practice.

### repeatMode

```dart
RepeatMode repeatMode
```

How the animation behaves after reaching 1.0.

When set to [RepeatMode.reverse], the animation plays forward and then backward. Defaults to [RepeatMode.restart], which jumps back to 0.0 and resumes from there.

### paused

```dart
bool paused
```

Whether the animation is currently paused.

When true, the animation stops at its current value. When changed to false, the animation resumes from that value. Defaults to false.

### createState()

```dart
State<RepeatingAnimationBuilder<T>> createState()
```
