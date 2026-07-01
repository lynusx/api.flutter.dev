# AnimatedTransitionBuilder

```dart
typedef AnimatedTransitionBuilder = Widget Function(BuildContext context, Animation<double> animation, Widget? child)
```

Builder callback used by [DualTransitionBuilder].

The builder is expected to return a transition powered by the provided `animation` and wrapping the provided `child`.

The `animation` provided to the builder always runs forward from 0.0 to 1.0.

An optional `child` widget which represents a pre-built widget subtree that does not depend on the animation's value.

Passing a pre-built widget here and incorporating it into the returned widget tree avoids rebuilding it for every frame of the animation and can improve performance significantly in some cases.

# DualTransitionBuilder

```dart
class DualTransitionBuilder extends StatefulWidget {}
```

A transition builder that animates its [child] based on the [AnimationStatus] of the provided [animation].

This widget can be used to specify different enter and exit transitions for a [child].

While the [animation] runs forward, the [child] is animated according to [forwardBuilder] and while the [animation] is running in reverse, it is animated according to [reverseBuilder].

Using this builder allows the widget tree to maintain its shape by nesting the enter and exit transitions. This ensures that no state information of any descendant widget is lost when the transition starts or completes.

### DualTransitionBuilder()

```dart
DualTransitionBuilder({dynamic key, required Animation<double> animation, required AnimatedTransitionBuilder forwardBuilder, required AnimatedTransitionBuilder reverseBuilder, Widget? child})
```

Creates a [DualTransitionBuilder].

### animation

```dart
Animation<double> animation
```

The animation that drives the [child]'s transition.

When this animation runs forward, the [child] transitions as specified by [forwardBuilder]. When it runs in reverse, the child transitions according to [reverseBuilder].

### forwardBuilder

```dart
AnimatedTransitionBuilder forwardBuilder
```

A builder for the transition that makes [child] appear on screen.

The [child] should be fully visible when the provided `animation` reaches 1.0.

The `animation` provided to this builder is running forward from 0.0 to 1.0 when [animation] runs _forward_. When [animation] runs in reverse, the given `animation` is set to [kAlwaysCompleteAnimation].

See also:

- [reverseBuilder], which builds the transition for making the [child] disappear from the screen.

### reverseBuilder

```dart
AnimatedTransitionBuilder reverseBuilder
```

A builder for a transition that makes [child] disappear from the screen.

The [child] should be fully invisible when the provided `animation` reaches 1.0.

The `animation` provided to this builder is running forward from 0.0 to 1.0 when [animation] runs in _reverse_. When [animation] runs forward, the given `animation` is set to [kAlwaysDismissedAnimation].

See also:

- [forwardBuilder], which builds the transition for making the [child] appear on screen.

### child

```dart
Widget? child
```

The widget below this [DualTransitionBuilder] in the tree.

This child widget will be wrapped by the transitions built by [forwardBuilder] and [reverseBuilder].

If a pre-built subtree is provided as the [child], it will be passed to the [reverseBuilder], and the result of that will in turn be passed to the [forwardBuilder]. This allows the builders to incorporate the subtree without rebuilding it on every frame.

Using this pre-built child is entirely optional, but can improve performance significantly in some cases and is therefore a good practice.

### createState()

```dart
State<DualTransitionBuilder> createState()
```
