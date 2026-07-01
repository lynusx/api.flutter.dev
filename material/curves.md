# standardEasing

```dart
Curve standardEasing
```

The standard easing curve in the Material 2 specification.

Elements that begin and end at rest use standard easing. They speed up quickly and slow down gradually, in order to emphasize the end of the transition.

See also:

- <https://material.io/design/motion/speed.html#easing>

# accelerateEasing

```dart
Curve accelerateEasing
```

The accelerate easing curve in the Material 2 specification.

Elements exiting a screen use acceleration easing, where they start at rest and end at peak velocity.

See also:

- <https://material.io/design/motion/speed.html#easing>

# decelerateEasing

```dart
Curve decelerateEasing
```

The decelerate easing curve in the Material 2 specification.

Incoming elements are animated using deceleration easing, which starts a transition at peak velocity (the fastest point of an element’s movement) and ends at rest.

See also:

- <https://material.io/design/motion/speed.html#easing>
