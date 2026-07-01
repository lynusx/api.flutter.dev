@docImport 'transitions.dart';

# AnimatedSize

```dart
class AnimatedSize extends StatefulWidget {}
```

Animated widget that automatically transitions its size over a given duration whenever the given child's size changes.

{@tool dartpad} This example defines a widget that uses [AnimatedSize] to change the size of the [SizedBox] on tap.

** See code in examples/api/lib/widgets/animated_size/animated_size.0.dart ** {@end-tool}

See also:

- [SizeTransition], which changes its size based on an [Animation].

### AnimatedSize()

```dart
AnimatedSize({dynamic key, Widget? child, AlignmentGeometry alignment = Alignment.center, Curve curve = Curves.linear, required Duration duration, Duration? reverseDuration, Clip clipBehavior = Clip.hardEdge, VoidCallback? onEnd})
```

Creates a widget that animates its size to match that of its child.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### alignment

```dart
AlignmentGeometry alignment
```

The alignment of the child within the parent when the parent is not yet the same size as the child.

The x and y values of the alignment control the horizontal and vertical alignment, respectively. An x value of -1.0 means that the left edge of the child is aligned with the left edge of the parent whereas an x value of 1.0 means that the right edge of the child is aligned with the right edge of the parent. Other values interpolate (and extrapolate) linearly. For example, a value of 0.0 means that the center of the child is aligned with the center of the parent.

Defaults to [Alignment.center].

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### curve

```dart
Curve curve
```

The animation curve when transitioning this widget's size to match the child's size.

### duration

```dart
Duration duration
```

The duration when transitioning this widget's size to match the child's size.

### reverseDuration

```dart
Duration? reverseDuration
```

The duration when transitioning this widget's size to match the child's size when going in reverse.

If not specified, defaults to [duration].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### onEnd

```dart
VoidCallback? onEnd
```

Called every time an animation completes.

This can be useful to trigger additional actions (e.g. another animation) at the end of the current animation.

### createState()

```dart
State<AnimatedSize> createState()
```
