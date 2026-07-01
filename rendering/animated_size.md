# RenderAnimatedSizeState

```dart
enum RenderAnimatedSizeState {}
```

A [RenderAnimatedSize] can be in exactly one of these states.

The initial state, when we do not yet know what the starting and target sizes are to animate.

The next state is [stable].

At this state the child's size is assumed to be stable and we are either animating, or waiting for the child's size to change.

If the child's size changes, the state will become [changed]. Otherwise, it remains [stable].

At this state we know that the child has changed once after being assumed [stable].

The next state will be one of:

- [stable] if the child's size stabilized immediately. This is a signal for the render object to begin animating the size towards the child's new size.

- [unstable] if the child's size continues to change.

At this state the child's size is assumed to be unstable (changing each frame).

Instead of chasing the child's size in this state, the render object tightly tracks the child's size until it stabilizes.

The render object remains in this state until a frame where the child's size remains the same as the previous frame. At that time, the next state is [stable].

# RenderAnimatedSize

```dart
class RenderAnimatedSize extends RenderAligningShiftedBox {}
```

A render object that animates its size to its child's size over a given [duration] and with a given [curve]. If the child's size itself animates (i.e. if it changes size two frames in a row, as opposed to abruptly changing size in one frame then remaining that size in subsequent frames), this render object sizes itself to fit the child instead of animating itself.

When the child overflows the current animated size of this render object, it is clipped.

### RenderAnimatedSize()

```dart
RenderAnimatedSize({required TickerProvider vsync, required Duration duration, Duration? reverseDuration, Curve curve = Curves.linear, dynamic alignment, dynamic textDirection, RenderBox? child, Clip clipBehavior = Clip.hardEdge, VoidCallback? onEnd})
```

Creates a render object that animates its size to match its child. The [duration] and [curve] arguments define the animation.

The [alignment] argument is used to align the child when the parent is not (yet) the same size as the child.

The [duration] is required.

The [vsync] should specify a [TickerProvider] for the animation controller.

The arguments [duration], [curve], [alignment], and [vsync] must not be null.

### debugController

```dart
AnimationController? get debugController
```

When asserts are enabled, returns the animation controller that is used to drive the resizing.

Otherwise, returns null.

This getter is intended for use in framework unit tests. Applications must not depend on its value.

### debugAnimation

```dart
CurvedAnimation? get debugAnimation
```

When asserts are enabled, returns the animation that drives the resizing.

Otherwise, returns null.

This getter is intended for use in framework unit tests. Applications must not depend on its value.

### state

```dart
RenderAnimatedSizeState get state
```

The state this size animation is in.

See [RenderAnimatedSizeState] for possible states.

### duration

```dart
Duration get duration
```

The duration of the animation.

### duration

```dart
set duration(Duration value)
```

### reverseDuration

```dart
Duration? get reverseDuration
```

The duration of the animation when running in reverse.

### reverseDuration

```dart
set reverseDuration(Duration? value)
```

### curve

```dart
Curve get curve
```

The curve of the animation.

### curve

```dart
set curve(Curve value)
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### isAnimating

```dart
bool get isAnimating
```

Whether the size is being currently animated towards the child's size.

See [RenderAnimatedSizeState] for situations when we may not be animating the size.

### vsync

```dart
TickerProvider get vsync
```

The [TickerProvider] for the [AnimationController] that runs the animation.

### vsync

```dart
set vsync(TickerProvider value)
```

### onEnd

```dart
VoidCallback? get onEnd
```

Called every time an animation completes.

This can be useful to trigger additional actions (e.g. another animation) at the end of the current animation.

### onEnd

```dart
set onEnd(VoidCallback? value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### performLayout()

```dart
void performLayout()
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### dispose()

```dart
void dispose()
```
