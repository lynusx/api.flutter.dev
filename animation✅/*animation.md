@docImport 'package:flutter/scheduler.dart'; @docImport 'package:flutter/widgets.dart';

# AnimationStatus

```dart
enum AnimationStatus {}
```

动画的状态。

动画停止在起始点。

动画正在从起始点运行到结束点。

动画正在反向运行，从结束点运行到起始点。

动画停止在结束点。

### isDismissed

```dart
bool get isDismissed
```

是否动画停止在起始点。

### isCompleted

```dart
bool get isCompleted
```

是否动画停止在结束点。

### isAnimating

```dart
bool get isAnimating
```

是否动画正在任一方向上运行。

### isForwardOrCompleted

```dart
bool get isForwardOrCompleted
```

{@template flutter.animation.AnimationStatus.isForwardOrCompleted} 动画当前的目标方向是否为朝向完成状态。

具体而言，当状态为 [AnimationStatus.forward] 或 [AnimationStatus.completed] 时返回 `true`；当状态为 [AnimationStatus.reverse] 或 [AnimationStatus.dismissed] 时返回 `false`。{@endtemplate}

# AnimationStatusListener

```dart
typedef AnimationStatusListener = void Function(AnimationStatus status)
```

使用 [Animation.addStatusListener] 添加的监听器的函数签名。

# ValueListenableTransformer

```dart
typedef ValueListenableTransformer<T> = T Function(T)
```

用于在 [Animation.fromValueListenable] 中转换值的方法签名。

# Animation

```dart
abstract class Animation<T> extends Listenable implements ValueListenable<T> {}
```

一个可能随时间变化的值，可正向或反向移动。

动画拥有一个（类型为 [T] 的）[value] 和一个 [status]。从概念上讲，该值位于某条路径上，而状态表示该值当前沿路径移动的方式：正向移动、反向移动，或停止在结束点或起始点。该路径可能会自我折返（例如，当动画使用具有回弹效果的曲线时），因此即使动画在概念上是正向移动的，其值也可能不是单调变化的。

动画的使用者可以通过 [addListener] 和 [addStatusListener] 监听值或状态的变化。监听器回调会在渲染管线的“动画”阶段被调用，即在重建 Widget 之前。

动画可能会随着时间的推移自行正向或反向移动（例如，用户触摸按钮后，按钮的不透明度会在固定时长内渐隐）；也可能由用户驱动（例如，用户可以来回拖动滑块的位置）；还可能两者兼有（例如，开关在释放时会自动归位到相应位置，或 [Dismissible](https://www.yuque.com/thyname/flutter.widgets/dismissible) 会响应拖动和快速滑动手势等）。这种行为通常由底层某个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 上的方法调用来控制。当动画正在活跃地运行时，通常会在每一帧由 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 驱动进行更新。

## Using animations

对于简单的动画效果，可以考虑使用 [ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget) 的某个子类，如 [AnimatedScale](https://www.yuque.com/thyname/flutter.widgets/animatedscale)、[AnimatedOpacity](https://www.yuque.com/thyname/flutter.widgets/animatedopacity) 等。当 [ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget) 足以满足需求时，就不需要使用 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 及本节中讨论的其他类。

否则，动画通常起源于由实现了 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider) 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 所创建的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)（其本身就是一个 [Animation<double>]）。可以进一步使用例如 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 或 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 从该动画派生出其他动画。这些动画可用于配置 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget)（使用其众多子类之一，如 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)），也可以直接使用其值。

例如，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 可以表示动画从 0.0 到 1.0 的抽象进度；然后 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 可以对其应用缓动曲线；接着 [SizeTween](https://www.yuque.com/thyname/flutter.animation/sizetween) 和 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween) 可以分别应用于该曲线动画，从而生成 [Animation<Size>] 和 [Animation<Color>]，用于控制 Widget 在动画进行过程中收缩并改变颜色。

## Performance considerations

由于 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 在动画进行过程中保持相同的标识，因此对于编排复杂动画的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 而言，它提供了一种便捷的方式，可以将动画的进度传达给各个子 Widget。建议让树中较高层级的 Widget 将 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象本身（而非其值）传递给较低层级的 Widget，这样即使动画处于活跃状态，也可以避免在每一帧都重建较高层级的 Widget。如果叶子 Widget 同样忽略 [value]，而是将整个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象传递给渲染对象（就像 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition) 所做的那样），那么它们也有可能避免重建，甚至避免重新布局，从而使动画每一帧所需的唯一工作就是重绘。

另请参阅：

- [ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget) 及其子类，它们无需手动使用 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)、[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 甚至 [State](https://www.yuque.com/thyname/flutter.widgets/state) 即可提供动画效果。
- [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，一种可以正向和反向运行、停止，或设置为特定值的动画。
- [Tween](https://www.yuque.com/thyname/flutter.animation/tween)，可用于将 [Animation<double>] 转换为其他类型的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。
- [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 及其子类，它们提供可由 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 控制的动画效果。

### Animation()

```dart
Animation()
```

抽象 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可以在 const 表达式中使用。

### Animation.fromValueListenable()

```dart
Animation.fromValueListenable(ValueListenable<T> listenable, {ValueListenableTransformer<T>? transformer})
```

根据 [ValueListenable](https://www.yuque.com/thyname/flutter.foundation/valuelistenable) 创建一个新的动画。

返回的动画的状态始终为 [AnimationStatus.forward]。所提供的 listenable 的值可以选择性地使用 [transformer] 函数进行转换。

{@tool snippet}

此构造函数可用于将 [ValueListenableBuilder](https://www.yuque.com/thyname/flutter.widgets/valuelistenablebuilder) Widget 实例替换为相应的动画 Widget，如 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition)。

之前：

```dart
Widget build(BuildContext context) {
  return ValueListenableBuilder<double>(
    valueListenable: _scrollPosition,
    builder: (BuildContext context, double value, Widget? child) {
      final double opacity = (value / 1000).clamp(0, 1);
      return Opacity(opacity: opacity, child: child);
    },
    child: const ColoredBox(
      color: Colors.red,
      child: Text('Hello, Animation'),
    ),
  );
}
```

{@end-tool} {@tool snippet}

之后：

```dart
Widget build2(BuildContext context) {
  return FadeTransition(
    opacity: Animation<double>.fromValueListenable(_scrollPosition, transformer: (double value) {
      return (value / 1000).clamp(0, 1);
    }),
    child: const ColoredBox(
      color: Colors.red,
      child: Text('Hello, Animation'),
    ),
  );
}
```

{@end-tool}

### addListener()

```dart
void addListener(VoidCallback listener)
```

每当动画的值发生变化时，调用该监听器。

可以使用 [removeListener] 移除监听器。

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

停止在动画值每次变化时调用该监听器。

如果 `listener` 当前未注册为监听器，则此方法不执行任何操作。

可以使用 [addListener] 添加监听器。

### addStatusListener()

```dart
void addStatusListener(AnimationStatusListener listener)
```

每当动画的状态发生变化时，调用该监听器。

可以使用 [removeStatusListener] 移除监听器。

### removeStatusListener()

```dart
void removeStatusListener(AnimationStatusListener listener)
```

停止在动画状态每次变化时调用该监听器。

如果 `listener` 当前未注册为状态监听器，则此方法不执行任何操作。

可以使用 [addStatusListener] 添加监听器。

### status

```dart
AnimationStatus get status
```

此动画的当前状态。

### value

```dart
T get value
```

动画的当前值。

### isDismissed

```dart
bool get isDismissed
```

此动画是否停止在起始点。

### isCompleted

```dart
bool get isCompleted
```

此动画是否停止在结束点。

### isAnimating

```dart
bool get isAnimating
```

此动画是否正在任一方向上运行。

默认情况下，此值等于 `status.isAnimating`，但 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 重写了此方法，使其输出取决于控制器是否正在活跃地计时（ticking）。

### isForwardOrCompleted

```dart
bool get isForwardOrCompleted
```

{@macro flutter.animation.AnimationStatus.isForwardOrCompleted}

### drive()

```dart
Animation<U> drive<U>(Animatable<U> child)
```

将一个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)（或 [CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween)）链接到此 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

此方法仅对 `Animation<double>` 实例有效（即当 `T` 为 `double` 时）。这意味着，例如，可以在 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 对象上调用此方法，也可以在 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)、[ProxyAnimation](https://www.yuque.com/thyname/flutter.animation/proxyanimation)、[ReverseAnimation](https://www.yuque.com/thyname/flutter.animation/reverseanimation)、[TrainHoppingAnimation](https://www.yuque.com/thyname/flutter.animation/trainhoppinganimation) 等对象上调用。

它返回一个专用于与该方法参数（`child`）相同类型 `U` 的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，其值是通过将给定的 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 应用于此 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的值而派生得到的。

{@tool snippet}

给定一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) `_controller`，以下代码创建了一个 `Animation<Alignment>`，随着控制器从 0.0 变化到 1.0，它会从左上角摆动到右上角：

```dart
Animation<Alignment> alignment1 = _controller.drive(
  AlignmentTween(
    begin: Alignment.topLeft,
    end: Alignment.topRight,
  ),
);
```

{@end-tool} {@tool snippet}

随后可以在 Widget 的 build 方法中使用 `alignment1.value`，例如，通过 [Align](https://www.yuque.com/thyname/flutter.widgets/align) Widget 来定位子 Widget，使子 Widget 的位置随时间从左上角移动到右上角。

通常会对这类曲线进行缓动处理，例如使过渡在开始时较慢、在结束时较快。以下代码片段展示了一种将上例中的 alignment tween 链接到缓动曲线（本例中为 [Curves.easeIn]）的方法。在此示例中，由于该 tween 的参数不会发生变化，因此它被创建为一个可在别处复用的变量。

```dart
final Animatable<Alignment> tween = AlignmentTween(begin: Alignment.topLeft, end: Alignment.topRight)
  .chain(CurveTween(curve: Curves.easeIn));
// ...
final Animation<Alignment> alignment2 = _controller.drive(tween);
```

{@end-tool} {@tool snippet}

以下代码与之完全等价，当 tween 内联创建时通常更清晰易懂，这在 tween 的值取决于其他变量时可能是更好的选择：

```dart
Animation<Alignment> alignment3 = _controller
  .drive(CurveTween(curve: Curves.easeIn))
  .drive(AlignmentTween(
    begin: Alignment.topLeft,
    end: Alignment.topRight,
  ));
```

{@end-tool} {@tool snippet}

此方法可以与通过 [Animatable.fromCallback] 创建的 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable) 搭配使用，以便使用回调函数对动画进行转换。这对于执行没有明确起点或终点的动画非常有用。此示例将当前滚动位置转换为在红色数值之间循环变化的颜色。

```dart
Animation<Color> color = Animation<double>.fromValueListenable(_scrollPosition)
  .drive(Animatable<Color>.fromCallback((double value) {
    return Color.fromRGBO(value.round() % 255, 0, 0, 1);
  }));
```

{@end-tool}

另请参阅：

- [Animatable.animate]，其作用相同。
- [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，通常用于驱动动画。
- [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation)，[CurveTween](https://www.yuque.com/thyname/flutter.animation/curvetween) 的替代方案，用于应用缓动曲线，它支持在正向和反向上使用不同的曲线。
- [Animatable.fromCallback]，允许通过任意转换创建 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)。

### toString()

```dart
String toString()
```

### toStringDetails()

```dart
String toStringDetails()
```

提供一个描述此对象状态的字符串，但不包括有关该对象本身的信息。

[Animation.toString] 使用此函数，以便 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的子类可以提供额外的详细信息，同时确保所有 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 子类都具有一致的 [toString] 风格。

此函数的结果包含一个描述此 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象状态的图标：

- “&#x25B6;”：[AnimationStatus.forward]（[value] 递增）
- “&#x25C0;”：[AnimationStatus.reverse]（[value] 递减）
- “&#x23ED;”：[AnimationStatus.completed]（[value] == 1.0）
- “&#x23EE;”：[AnimationStatus.dismissed]（[value] == 0.0）
