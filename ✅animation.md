Flutter 动画系统。

要使用此库，请导入 `package:flutter/animation.dart`。

此库提供了在 Flutter 中实现动画的基本构建模块。框架的其他层使用这些构建模块为应用程序提供高级动画支持。例如，widgets 库包含 [ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget) 和 [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget)，它们可以轻松地为 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的某些属性设置动画。如果这些动画组件不能满足特定用例的需求，则可以使用此库提供的基本构建模块来实现自定义动画效果。

此库仅依赖 Dart 核心库和 `physics.dart` 库。

### 基础：Animation 类

Flutter 将动画表示为在给定时长内变化的值，该值可以是任意类型。例如，它可以是一个 [double](https://www.yuque.com/thyname/dart.core/double)，表示 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 淡出时的当前不透明度；也可以是组件在两种颜色之间平滑过渡时的当前背景 [Color](https://www.yuque.com/thyname/dart.ui/color)。动画的当前值由一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象表示，它是动画库的核心类。除了当前动画值之外，[Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象还存储当前的 [AnimationStatus](https://www.yuque.com/thyname/flutter.animation/animationstatus)。该状态表示动画在概念上是从起点运行到终点，还是反向运行；它也可能表示动画当前停止在起点或终点。

其他对象可以在 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 上注册监听器，以便在动画值和/或动画状态发生变化时收到通知。[Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 可以通过 [Animation.addListener] 注册这样的 _值_ 监听器，以便每当该值变化时使用当前动画值重建自身。例如，一个组件可能会监听某个动画，以便在其值每次变化时更新自身的不透明度。同样，通过 [Animation.addStatusListener] 注册 _状态_ 监听器，在当前动画结束时触发其他操作也很有用。

作为示例，以下视频展示了某个组件的不透明度动画中，当前动画状态和动画值随时间的变化情况。此 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 由一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)（见下一节）驱动。动画触发之前，动画状态为 "dismissed"，值为 0.0。当值从 0.0 变化到 1.0 以使组件淡入时，状态变为 "forward"。当组件在动画值为 1.0 时完全淡入后，状态变为 "completed"。当动画再次触发以将组件淡出时，动画状态变为 "reverse"，动画值回到 0.0。此时组件完全淡出，动画状态切回 "dismissed"，直到动画再次被触发。

{@animation 420 100 https://flutter.github.io/assets-for-api-docs/assets/animation/animation_status_value.mp4}

尽管你不能直接实例化 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)（它是一个抽象类），但你可以使用 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 来创建一个。

### 驱动动画：AnimationController

[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 是一种特殊的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，每当运行应用程序的设备准备好显示新的一帧时，它就会推进其动画值（通常这个速率约为每秒 60 个值）。凡是需要 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的地方都可以使用 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)。顾名思义，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 还提供了对其 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的控制：它实现了在任意时刻停止动画、以及正向和反向运行动画的方法。

默认情况下，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 在正向运行时，会在给定时长内将其动画值从 0.0 到 1.0 线性递增。在许多用例中，你可能希望值是不同的类型、改变动画值的范围，或者改变动画在各个值之间移动的方式。这可以通过包装动画来实现：将其包装在 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)（见下文）中可以将动画值的范围改变为不同的范围或类型（例如对 [Color](https://www.yuque.com/thyname/dart.ui/color) 或 [Rect](https://www.yuque.com/thyname/dart.ui/rect) 进行动画处理）。此外，通过将动画包装在 [CurvedAnimation](https://www.yuque.com/thyname/flutter.animation/curvedanimation) 中，还可以为其应用 [Curve](https://www.yuque.com/thyname/flutter.animation/curve)。曲线动画不是线性递增动画值，而是根据提供的曲线来改变其值。框架内置了许多曲线（见 [Curves](https://www.yuque.com/thyname/flutter.animation/curves)）。例如，[Curves.easeOutCubic] 会在动画开始时快速增加动画值，然后减速，直到到达目标值：

{@animation 464 192 https://flutter.github.io/assets-for-api-docs/assets/animation/curve_ease_out_cubic.mp4}

### 对不同类型进行动画处理：Animatable

`Animatable<T>` 是一个以 `Animation<double>` 作为输入并生成类型为 `T` 的值的对象。此类对象可用于将 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)（或任何其他类型为 [double](https://www.yuque.com/thyname/dart.core/double) 的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)）的动画值范围转换为不同的范围，而这个新范围甚至不必再是 double 类型。借助 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 或 [TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence)（见下文各节）这样的 [Animatable](https://www.yuque.com/thyname/flutter.animation/animatable)，[AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 可以在给定时长内，将 [Color](https://www.yuque.com/thyname/dart.ui/color)、[Rect](https://www.yuque.com/thyname/dart.ui/rect)、[Size](https://www.yuque.com/thyname/dart.ffi/size) 等多种类型从一个值平滑过渡到另一个值。

### 插值：Tween

[Tween](https://www.yuque.com/thyname/flutter.animation/tween) 应用于类型为 [double](https://www.yuque.com/thyname/dart.core/double) 的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，以改变动画值的范围和类型。例如，要使 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 的背景在两种 [Color](https://www.yuque.com/thyname/dart.ui/color) 之间平滑过渡，可以使用 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween)。每个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 都指定一个起始值和一个结束值。当驱动该 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的动画值从 0.0 变化到 1.0 时，它会在起始值和结束值之间产生插值。随着驱动 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的动画值接近 1.0，[Tween](https://www.yuque.com/thyname/flutter.animation/tween) 产生的值通常会越来越接近其结束值。

以下视频展示了当动画值从 0.0 变化到 1.0 再变回 0.0 时，[IntTween](https://www.yuque.com/thyname/flutter.animation/inttween)、`Tween<double>` 和 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween) 所产生的示例值：

{@animation 530 150 https://flutter.github.io/assets-for-api-docs/assets/animation/tweens.mp4}

一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 或 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 可以驱动多个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween)。例如，要并行地对某个组件的大小和颜色进行动画处理，可以创建一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 来同时驱动 [SizeTween](https://www.yuque.com/thyname/flutter.animation/sizetween) 和 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween)。

框架内置了许多 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 子类（如 [IntTween](https://www.yuque.com/thyname/flutter.animation/inttween)、[SizeTween](https://www.yuque.com/thyname/flutter.animation/sizetween)、[RectTween](https://www.yuque.com/thyname/flutter.animation/recttween) 等），用于对常见属性进行动画处理。

### 分阶段动画：TweenSequence

[TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 可以帮助按阶段平滑地对给定属性进行动画处理。序列中的每个 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 负责一个不同的阶段，并具有相关联的权重。动画运行时，各阶段依次执行。例如，假设你想让某个组件的背景从黄色动画过渡到绿色，短暂停留后再过渡到红色。为此，你可以在一个 tween 序列中指定三个 tween：一个从黄色到绿色的 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween)，一个仅保持绿色的 [ConstantTween](https://www.yuque.com/thyname/flutter.animation/constanttween)，以及另一个从绿色到红色的 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween)。对于每个 tween，你需要选择一个权重，表示该 tween 相对于所有其他 tween 所占用的时间比例。如果我们为两个 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween) 都分配权重 2，为 [ConstantTween](https://www.yuque.com/thyname/flutter.animation/constanttween) 分配权重 1，那么 [ColorTween](https://www.yuque.com/thyname/flutter.animation/colortween) 所描述的过渡所花费的时间将是 [ConstantTween](https://www.yuque.com/thyname/flutter.animation/constanttween) 的两倍。与常规 [Tween](https://www.yuque.com/thyname/flutter.animation/tween) 一样，[TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 也由 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 驱动：当驱动的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 从 0.0 运行到 1.0 时，[TweenSequence](https://www.yuque.com/thyname/flutter.animation/tweensequence) 会依次运行完它的所有阶段。

以下视频展示了上一段中描述的动画：

{@animation 646 250 https://flutter.github.io/assets-for-api-docs/assets/animation/tween_sequence.mp4}

另请参阅：

- flutter.dev 上的 [动画简介](https://docs.flutter.dev/ui/animations)。
- flutter.dev 上的 [动画教程](https://docs.flutter.dev/ui/animations/tutorial)。
- [示例应用](https://github.com/flutter/samples/tree/main/animations)，展示了 Flutter 的动画特性。
- [ImplicitlyAnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/implicitlyanimatedwidget) 及其子类，它们是能够隐式地为自身属性变化添加动画效果的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。
- [AnimatedWidget](https://www.yuque.com/thyname/flutter.widgets/animatedwidget) 及其子类，它们是接受显式 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 以对自身属性进行动画处理的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。
