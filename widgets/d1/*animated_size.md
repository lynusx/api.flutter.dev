@docImport 'transitions.dart';

# AnimatedSize

```dart
class AnimatedSize extends StatefulWidget {}
```

当子组件（child）的大小发生变化时，此动画组件会在给定的时长内自动过渡到新的大小。

{@tool dartpad} 此示例定义了一个使用 [AnimatedSize](https://www.yuque.com/thyname/flutter.widgets/animatedsize) 在点击时改变 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 大小的组件。

** 代码参见 examples/api/lib/widgets/animated_size/animated_size.0.dart ** {@end-tool}

另请参阅：

- [SizeTransition](https://www.yuque.com/thyname/flutter.widgets/sizetransition)，根据 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 改变其大小。

### AnimatedSize()

```dart
AnimatedSize({dynamic key, Widget? child, AlignmentGeometry alignment = Alignment.center, Curve curve = Curves.linear, required Duration duration, Duration? reverseDuration, Clip clipBehavior = Clip.hardEdge, VoidCallback? onEnd})
```

创建一个动画组件，使其大小与子组件的大小相匹配。

### child

```dart
Widget? child
```

此组件在组件树中的下一级子组件。

{@macro flutter.widgets.ProxyWidget.child}

### alignment

```dart
AlignmentGeometry alignment
```

当父组件的大小尚未与子组件相同时，子组件在父组件内的对齐方式。

对齐方式的 x 值和 y 值分别控制水平和垂直方向的对齐。x 值为 -1.0 表示子组件的左边缘与父组件的左边缘对齐，而 x 值为 1.0 表示子组件的右边缘与父组件的右边缘对齐。其他数值将进行线性插值（或外插）。例如，值为 0.0 表示子组件的中心与父组件的中心对齐。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含常用常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，用于指定相对于文本方向的对齐方式。

### curve

```dart
Curve curve
```

此组件的大小过渡到与子组件大小匹配时所使用的动画曲线。

### duration

```dart
Duration duration
```

此组件的大小过渡到与子组件大小匹配所需的时长。

### reverseDuration

```dart
Duration? reverseDuration
```

反向过渡时，此组件的大小过渡到与子组件大小匹配所需的时长。

如果未指定，默认为 [duration]。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### onEnd

```dart
VoidCallback? onEnd
```

每次动画完成时调用。

这在当前动画结束时触发其他操作（例如另一个动画）时非常有用。

### createState()

```dart
State<AnimatedSize> createState()
```
