# AnimatedTransitionBuilder

```dart
typedef AnimatedTransitionBuilder = Widget Function(BuildContext context, Animation<double> animation, Widget? child)
```

[DualTransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/dualtransitionbuilder) 使用的 builder 回调。

该 builder 应返回一个由所提供的 `animation` 驱动、并包裹所提供 `child` 的过渡效果。

传递给 builder 的 `animation` 始终从 0.0 正向运行到 1.0。

可选的 `child` 组件表示一个不依赖于该动画值的预构建组件子树。

在此传入一个预构建的组件，并将其纳入返回的组件树中，可以避免在动画的每一帧都重新构建该组件，在某些情况下可以显著提升性能。

# DualTransitionBuilder

```dart
class DualTransitionBuilder extends StatefulWidget {}
```

一个根据所提供 `animation` 的 [AnimationStatus](https://www.yuque.com/thyname/flutter.animation/animationstatus)（动画状态）为其 [child] 添加动画效果的过渡 builder。

此组件可用于为 [child] 指定不同的进入和退出过渡效果。

当 [animation](https://www.yuque.com/thyname/flutter.animation) 正向运行时，[child] 将根据 [forwardBuilder] 添加动画；当 [animation](https://www.yuque.com/thyname/flutter.animation) 反向运行时，则根据 [reverseBuilder] 添加动画。

使用此 builder 可使组件树保持其结构，确保在过渡开始或完成时，任何后代组件的状态信息都不会丢失。

### DualTransitionBuilder()

```dart
DualTransitionBuilder({dynamic key, required Animation<double> animation, required AnimatedTransitionBuilder forwardBuilder, required AnimatedTransitionBuilder reverseBuilder, Widget? child})
```

创建一个 [DualTransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/dualtransitionbuilder)。

### animation

```dart
Animation<double> animation
```

驱动 [child] 过渡效果的动画。

当此动画正向运行时，[child] 将按照 [forwardBuilder] 指定的方式过渡。当其反向运行时，child 将按照 [reverseBuilder] 指定的方式过渡。

### forwardBuilder

```dart
AnimatedTransitionBuilder forwardBuilder
```

用于使 [child] 在屏幕上出现的过渡效果的 builder。

当所提供的 `animation` 达到 1.0 时，[child] 应完全可见。

当 [animation](https://www.yuque.com/thyname/flutter.animation) 正向运行时，传递给此 builder 的 `animation` 会从 0.0 正向运行到 1.0。当 [animation](https://www.yuque.com/thyname/flutter.animation) 反向运行时，传递给此 builder 的 animation 将被设置为 [kAlwaysCompleteAnimation](https://www.yuque.com/thyname/flutter.animation/kalwayscompleteanimation)。

另请参阅：

- [reverseBuilder]，用于构建使 [child] 从屏幕上消失的过渡效果。

### reverseBuilder

```dart
AnimatedTransitionBuilder reverseBuilder
```

用于使 [child] 从屏幕上消失的过渡效果的 builder。

当所提供的 `animation` 达到 1.0 时，[child] 应完全不可见。

当 [animation](https://www.yuque.com/thyname/flutter.animation) 反向运行时，传递给此 builder 的 `animation` 会从 0.0 正向运行到 1.0。当 [animation](https://www.yuque.com/thyname/flutter.animation) 正向运行时，传递给此 builder 的 animation 将被设置为 [kAlwaysDismissedAnimation](https://www.yuque.com/thyname/flutter.animation/kalwaysdismissedanimation)。

另请参阅：

- [forwardBuilder]，用于构建使 [child] 在屏幕上出现的过渡效果。

### child

```dart
Widget? child
```

此 [DualTransitionBuilder](https://www.yuque.com/thyname/flutter.widgets/dualtransitionbuilder) 在组件树中的下级组件。

此 child 组件将被 [forwardBuilder] 和 [reverseBuilder] 构建的过渡效果所包裹。

如果提供了预构建的子树作为 [child]，它将被传递给 [reverseBuilder]，该 builder 的构建结果又会被传递给 [forwardBuilder]。这使得这些 builder 能够在不必每帧都重新构建该子树的情况下，将其纳入构建结果中。

使用此预构建的 child 完全是可选的，但在某些情况下可以显著提升性能，因此是一种值得推荐的良好实践。
