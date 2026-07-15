@docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# AnimationBehavior

```dart
enum AnimationBehavior {}
```

配置当动画被禁用时 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的行为方式。

当 [AccessibilityFeatures.disableAnimations] 为 true 时，表示设备要求 Flutter 尽可能减少或禁用动画。为了遵循这一要求，我们会缩短动画的时长以及相应的帧数。此枚举用于允许某些 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 选择不采用此行为。

例如，控制可滚动列表物理模拟的 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 将使用 [AnimationBehavior.preserve]，这样当用户尝试滚动时，列表就不会过快地跳转到结尾/开头。

当 [AccessibilityFeatures.disableAnimations] 为 true 时，该 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 将缩短其时长。

该 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 将保持其行为不变。

这是循环动画的默认行为，以防止在 Widget 未考虑 [AccessibilityFeatures.disableAnimations] 标志的情况下，动画在屏幕上快速闪烁。

根据所配置的行为以及 [AccessibilityFeatures.disableAnimations] 标志，判断是否应启用动画。

# AnimationController

```dart
class AnimationController extends Animation<double> with AnimationEagerListenerMixin, AnimationLocalListenersMixin, AnimationLocalStatusListenersMixin {}
```

动画的控制器。

此类允许你执行以下任务：

- 使动画 [forward]（正向播放）或 [reverse]（反向播放），或 [stop]（停止）动画。
- 将动画设置为特定的 [value]。
- 定义动画的 [upperBound] 和 [lowerBound] 值。
- 使用物理模拟创建 [fling]（快速滑动）动画效果。

默认情况下，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 会在给定的时长内线性地生成范围从 0.0 到 1.0 的值。

当动画正在活跃运行时，动画控制器会在运行你的应用的设备每次准备好显示新一帧时生成一个新值（通常，此速率约为每秒 60 到 120 个值）。如果动画控制器通过 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider) 与某个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 相关联，那么当该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的子树按照 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode) 的定义被禁用时，其更新将被静默；此时时间仍会流逝，[forward] 和 [stop] 等方法仍然可以被调用并会改变值，但控制器不会再自行生成新值。

## Ticker providers

[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 需要一个 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)，它通过构造函数上的 `vsync` 参数进行配置。构造函数使用该 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider) 创建一个 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker)，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 使用此 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 来逐步推进它所控制的动画。

关于如何获取 ticker provider 的建议，请参阅 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)。通常，在应用了合适的 mixin（如 [SingleTickerProviderStateMixin](https://www.yuque.com/thyname/flutter.widgets/singletickerproviderstatemixin)）使 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类实现 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider) 之后，相关的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 便可充当 ticker provider。

## Life cycle

当不再需要 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 时，应当对其调用 [dispose]。这可以降低发生内存泄漏的可能性。当与 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 一起使用时，通常会在 [State.initState] 方法中创建 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，然后在 [State.dispose] 方法中将其释放。

## Using [Future](https://www.yuque.com/thyname/dart.async/future)s with [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)

启动动画的方法会返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 对象，该对象会在动画成功完成时完成（complete），并且永远不会抛出错误；如果动画被取消，该 future 将永远不会完成。此对象还具有一个 [TickerFuture.orCancel] 属性，它返回一个 future，该 future 会在动画成功完成时完成，并在动画被中止时以错误的形式完成。

这可用于编写如下面的 `fadeOutAndUpdateState` 方法这样的代码。

{@tool snippet}

下面是一个有状态的 `Foo` Widget。它的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 使用 [SingleTickerProviderStateMixin](https://www.yuque.com/thyname/flutter.widgets/singletickerproviderstatemixin) 来实现所需的 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)，在 [State.initState] 方法中创建其控制器，并在 [State.dispose] 方法中将其释放。控制器的时长根据 `Foo` Widget 中的一个属性进行配置；当该属性发生变化时，会使用 [State.didUpdateWidget] 方法来更新控制器。

```dart
class Foo extends StatefulWidget {
  const Foo({ super.key, required this.duration });

  final Duration duration;

  @override
  State<Foo> createState() => _FooState();
}

class _FooState extends State<Foo> with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      vsync: this, // the SingleTickerProviderStateMixin
      duration: widget.duration,
    );
  }

  @override
  void didUpdateWidget(Foo oldWidget) {
    super.didUpdateWidget(oldWidget);
    _controller.duration = widget.duration;
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(); // ...
  }
}
```

{@end-tool} {@tool snippet}

以下方法（用于某个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类）使用 Dart 中等待 [Future](https://www.yuque.com/thyname/dart.async/future) 对象的异步语法来驱动两个动画控制器：

```dart
Future<void> fadeOutAndUpdateState() async {
  try {
    await fadeAnimationController.forward().orCancel;
    await sizeAnimationController.forward().orCancel;
    setState(() {
      dismissed = true;
    });
  } on TickerCanceled {
    // the animation got canceled, probably because we were disposed
  }
}
```

{@end-tool}

上面代码中的假设是，动画控制器会在 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类对 [State.dispose] 方法的重写中被释放。由于释放控制器会取消动画（引发 [TickerCanceled](https://www.yuque.com/thyname/flutter.scheduler/tickercanceled) 异常），因此此处的代码可以跳过在每一步验证 [State.mounted] 是否仍为 true 的操作。（同样，这里假设控制器是在 [State.initState] 中创建、在 [State.dispose] 中释放的，如前一节所述。）

{@tool dartpad} 此示例展示了如何使用 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 和 [SlideTransition](https://www.yuque.com/thyname/flutter.widgets/slidetransition) 来创建一个动画数字效果，类似于老式弹球机或汽车里程表上的数字效果。新的数字值会从下方滑入到位，而旧的值则会向上滑出视野。当控制器已经在运行动画时发生的点击，会使控制器的 [AnimationController.duration] 缩短，以避免视觉效果滞后。

** See code in examples/api/lib/animation/animation_controller/animated_digit.0.dart ** {@end-tool}

另请参阅：

- [Tween](https://www.yuque.com/thyname/flutter.animation/tween)，用于将 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 转换为其他类型的值范围的基类。

### AnimationController()

```dart
AnimationController({double? value, Duration? duration, Duration? reverseDuration, String? debugLabel, double lowerBound = 0.0, double upperBound = 1.0, AnimationBehavior animationBehavior = AnimationBehavior.normal, required TickerProvider vsync})
```

创建一个动画控制器。

- `value` 是动画的初始值。默认为下界（lower bound）。

- [duration] 是此动画应持续的时长。

- [debugLabel] 是一个字符串，用于在调试期间帮助识别此动画（由 [toString] 使用）。

- [lowerBound] 是此动画可以取得的最小值，也是此动画被视为处于 dismissed（已消失）状态时的值。

- [upperBound] 是此动画可以取得的最大值，也是此动画被视为处于 completed（已完成）状态时的值。

- `vsync` 是当前上下文所需的 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)。可以通过调用 [resync] 来更改它。有关如何获取 ticker provider 的建议，请参阅 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)。

### AnimationController.unbounded()

```dart
AnimationController.unbounded({double value = 0.0, Duration? duration, Duration? reverseDuration, String? debugLabel, required TickerProvider vsync, AnimationBehavior animationBehavior = AnimationBehavior.preserve})
```

创建一个值没有上界或下界的动画控制器。

- [value] 是动画的初始值。

- [duration] 是此动画应持续的时长。

- [debugLabel] 是一个字符串，用于在调试期间帮助识别此动画（由 [toString] 使用）。

- `vsync` 是当前上下文所需的 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)。可以通过调用 [resync] 来更改它。有关如何获取 ticker provider 的建议，请参阅 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider)。

此构造函数最适用于将通过物理模拟驱动的动画，尤其是当该物理模拟没有预先确定的边界时。

### lowerBound

```dart
double lowerBound
```

此动画被视为处于 dismissed（已消失）状态时的值。

### upperBound

```dart
double upperBound
```

此动画被视为处于 completed（已完成）状态时的值。

### debugLabel

```dart
String? debugLabel
```

在 [toString] 输出中使用的标签，旨在帮助在调试输出中识别动画控制器实例。

### animationBehavior

```dart
AnimationBehavior animationBehavior
```

当 [AccessibilityFeatures.disableAnimations] 为 true 时控制器的行为。

对于 [AnimationController.new] 构造函数，默认值为 [AnimationBehavior.normal]；对于 [AnimationController.unbounded] 构造函数，默认值为 [AnimationBehavior.preserve]。

### view

```dart
Animation<double> get view
```

返回此动画控制器对应的 [Animation<double>]，这样便可以传递指向此对象的引用，而不允许该引用的使用者修改 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的状态。

### duration

```dart
Duration? duration
```

此动画应持续的时长。

如果指定了 [reverseDuration]，则 [duration] 仅在 [forward]（正向播放）时使用。否则，它将指定两个方向上的时长。

### reverseDuration

```dart
Duration? reverseDuration
```

此动画在 [reverse]（反向播放）时应持续的时长。

如果未指定 [reverseDuration] 或将其设置为 null，则会使用 [duration] 的值。

### resync()

```dart
void resync(TickerProvider vsync)
```

使用新的 [TickerProvider](https://www.yuque.com/thyname/flutter.scheduler/tickerprovider) 重新创建 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker)。

### value

```dart
double get value
```

动画的当前值。

设置此值会通知所有监听器该值已发生变化。

如果控制器当前正在运行，设置此值也会停止控制器；如果发生这种情况，还会通知所有状态监听器。

### value

```dart
set value(double newValue)
```

停止动画控制器，并设置动画的当前值。

新值会被限制在 [lowerBound] 和 [upperBound] 所设定的范围内。

即使此操作未改变值，值监听器也会收到通知。如果动画此前正在播放，则状态监听器也会收到通知。

{@template flutter.animation.AnimationController.ticker_canceled} 最近一次返回的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)（如果有的话）会被标记为已取消，这意味着该 future 永远不会完成，而其派生的 [TickerFuture.orCancel] future 将以 [TickerCanceled](https://www.yuque.com/thyname/flutter.scheduler/tickercanceled) 错误完成。{@endtemplate}

另请参阅：

- [reset]，相当于将 [value] 设置为 [lowerBound]。
- [stop]，用于中止动画，而不改变其值或状态，也不发出除了完成或取消 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 之外的任何通知。
- [forward]、[reverse]、[animateTo]、[animateWith]、[animateBackWith]、[fling] 和 [repeat]，用于启动动画控制器。

### reset()

```dart
void reset()
```

将控制器的值设置为 [lowerBound]，停止动画（如果正在进行中），并将其重置到起始点，即 dismissed（已消失）状态。

{@macro flutter.animation.AnimationController.ticker_canceled}

另请参阅：

- [value]，可根据需要显式设置为特定值。
- [forward]，用于在正向上启动动画。
- [stop]，用于中止动画，而不改变其值或状态，也不发出除了完成或取消 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 之外的任何通知。

### velocity

```dart
double get velocity
```

[value] 每秒的变化速率。

如果 [isAnimating] 为 false，则 [value] 不会发生变化，且变化速率为零。

### lastElapsedDuration

```dart
Duration? get lastElapsedDuration
```

自动画开始起，到动画最近一次 tick 之间经过的时长。

如果控制器未在运行动画，则最近经过的时长为 null。

### isAnimating

```dart
bool get isAnimating
```

此动画当前是否正在正向或反向上运行。

这与该动画是否正在活跃地计时（ticking）是两回事。动画控制器的 ticker 可能会被静音（muted），在这种情况下，即使时间仍在继续流逝，动画控制器的回调也不会再被触发。请参阅 [Ticker.muted] 和 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode)。

如果动画被停止（例如通过 [stop] 或设置新的 [value]），[isAnimating] 将返回 `false`，但 [status] 不会改变，因此 [AnimationStatus.isAnimating] 的值可能仍为 `true`。

### status

```dart
AnimationStatus get status
```

### forward()

```dart
TickerFuture forward({double? from})
```

开始正向（朝向结束点）运行此动画。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画完成时完成。

如果 [from] 不为 null，则在运行动画之前，会将其设置为当前的 [value]。

{@macro flutter.animation.AnimationController.ticker_canceled}

在动画进行过程中，[status] 会报告为 [AnimationStatus.forward]，当动画结束时到达 [upperBound]，[status] 将切换为 [AnimationStatus.completed]。

### reverse()

```dart
TickerFuture reverse({double? from})
```

开始反向（朝向起始点）运行此动画。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画进入 dismissed（已消失）状态时完成。

如果 [from] 不为 null，则在运行动画之前，会将其设置为当前的 [value]。

{@macro flutter.animation.AnimationController.ticker_canceled}

在动画进行过程中，[status] 会报告为 [AnimationStatus.reverse]，当动画结束时到达 [lowerBound]，[status] 将切换为 [AnimationStatus.dismissed]。

### toggle()

```dart
TickerFuture toggle({double? from})
```

根据此动画是否 [isForwardOrCompleted]，切换此动画的方向。

具体而言，如果 [status] 为 [AnimationStatus.forward] 或 [AnimationStatus.completed]，则此函数的行为与 [reverse] 相同；如果为 [AnimationStatus.reverse] 或 [AnimationStatus.dismissed]，则其行为与 [forward] 相同。

如果 [from] 不为 null，则在运行动画之前，会将其设置为当前的 [value]。

{@macro flutter.animation.AnimationController.ticker_canceled}

### animateTo()

```dart
TickerFuture animateTo(double target, {Duration? duration, Curve curve = Curves.linear})
```

将动画从其当前值“正向”驱动到给定的目标值。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画完成时完成。

{@macro flutter.animation.AnimationController.ticker_canceled}

在动画进行过程中，无论 `target` 是否大于 [value]，[status] 都会报告为 [AnimationStatus.forward]。在动画结束时，当到达 `target` 时，[status] 会报告为 [AnimationStatus.completed]。

如果 `target` 参数与动画的当前 [value] 相同，则不会执行动画，并且返回的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 将已经处于完成状态。

### animateBack()

```dart
TickerFuture animateBack(double target, {Duration? duration, Curve curve = Curves.linear})
```

将动画从其当前值“反向”驱动到给定的目标值。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画完成时完成。

{@macro flutter.animation.AnimationController.ticker_canceled}

在动画进行过程中，无论 `target` 是否小于 [value]，[status] 都会报告为 [AnimationStatus.reverse]。在动画结束时，当到达 `target` 时，[status] 会报告为 [AnimationStatus.dismissed]。

如果 `target` 参数与动画的当前 [value] 相同，则不会执行动画，并且返回的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 将已经处于完成状态。

### repeat()

```dart
TickerFuture repeat({double? min, double? max, bool reverse = false, Duration? period, int? count})
```

开始沿正向运行此动画，并在动画完成时重新开始运行。

当未为 [min] 和 [max] 显式设置值时，默认在 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 的 [lowerBound] 和 [upperBound] 之间循环。

将 [reverse] 设置为 true 后，动画不再总是从 [min] 重新开始，而是每次循环时起始值都会在 [min] 和 [max] 值之间交替。当动画从 [max] 运行到 [min] 时，[status] 会报告为 [AnimationStatus.reverse]。

动画的每一次运行都将持续 `period` 时长。如果未提供 `period`，则会改用 [duration]，该值必须在调用 [repeat] 之前设置——可以在构造函数中设置，也可以之后使用 [duration] 的 setter 进行设置。

如果为 [count] 传入了一个值，则动画将执行相应次数的迭代后停止。否则，动画将无限循环。

返回一个永远不会完成的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，除非指定了 [count]。当动画被停止时（例如通过 [stop]），[TickerFuture.orCancel] future 会以错误的形式完成。

{@macro flutter.animation.AnimationController.ticker_canceled}

### fling()

```dart
TickerFuture fling({double velocity = 1.0, SpringDescription? springDescription, AnimationBehavior? animationBehavior})
```

使用弹簧效果（在 [lowerBound] 和 [upperBound] 范围内）和初始速度来驱动动画。

如果速度为正，动画将完成；否则将 dismiss（消失）。速度以每秒的单位数指定。如果设置了 [SemanticsBinding.disableAnimations] 标志，则速度会被相对随意地乘以 200。

[springDescription] 参数可用于指定一个自定义的 [SpringType.criticallyDamped] 或 [SpringType.overDamped] 弹簧，以此来驱动动画。默认情况下，会使用 [SpringType.criticallyDamped] 弹簧。有关如何创建合适的 [SpringDescription](https://www.yuque.com/thyname/flutter.physics/springdescription)，请参阅 [SpringDescription.withDampingRatio]。

生成的弹簧模拟不能是 [SpringType.underDamped] 类型；这种弹簧会振荡而不是快速滑动（fling）。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画完成时完成。

{@macro flutter.animation.AnimationController.ticker_canceled}

### animateWith()

```dart
TickerFuture animateWith(Simulation simulation)
```

根据给定的模拟（simulation）来驱动动画。

{@template flutter.animation.AnimationController.animateWith} 来自模拟的值会被限制在 [lowerBound] 和 [upperBound] 范围内。若要避免这种情况，可以考虑使用 [AnimationController.unbounded] 构造函数来创建 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。

返回一个 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)，它会在动画完成时完成。

最近一次返回的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture)（如果有的话）会被标记为已取消，这意味着该 future 永远不会完成，而其派生的 [TickerFuture.orCancel] future 将以 [TickerCanceled](https://www.yuque.com/thyname/flutter.scheduler/tickercanceled) 错误完成。{@endtemplate}

在整个模拟持续期间，[status] 始终为 [AnimationStatus.forward]。

另请参阅：

- [animateBackWith]，与此方法类似，但其状态始终为 [AnimationStatus.reverse]。

### animateBackWith()

```dart
TickerFuture animateBackWith(Simulation simulation)
```

根据给定的模拟来驱动动画，其 [status] 为 [AnimationStatus.reverse]。

{@macro flutter.animation.AnimationController.animateWith}

在整个模拟持续期间，[status] 始终为 [AnimationStatus.reverse]。

另请参阅：

- [animateWith]，与此方法类似，但其状态始终为 [AnimationStatus.forward]。

### stop()

```dart
void stop({bool canceled = true})
```

停止运行此动画。

此操作不会触发任何通知。动画将停止在其当前状态。

默认情况下，最近一次返回的 [TickerFuture](https://www.yuque.com/thyname/flutter.scheduler/tickerfuture) 会被标记为已取消，这意味着该 future 永远不会完成，而其派生的 [TickerFuture.orCancel] future 将以 [TickerCanceled](https://www.yuque.com/thyname/flutter.scheduler/tickercanceled) 错误完成。通过为 `canceled` 参数传入值 false，可以反转这一行为，使这些 future 成功完成。

另请参阅：

- [reset]，用于停止动画并将其重置为 [lowerBound]，并且会发送通知。
- [forward]、[reverse]、[animateTo]、[animateWith]、[fling] 和 [repeat]，用于重新启动动画控制器。

### dispose()

```dart
void dispose()
```

释放此对象所使用的资源。调用此方法后，该对象将不再可用。

{@macro flutter.animation.AnimationController.ticker_canceled}

### toStringDetails()

```dart
String toStringDetails()
```
