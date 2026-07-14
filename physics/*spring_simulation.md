@docImport 'package:flutter/widgets.dart';

# SpringDescription

```dart
class SpringDescription {}
```

描述弹簧常数的结构体。

用于配置 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation)。

### SpringDescription()

```dart
SpringDescription({required double mass, required double stiffness, required double damping})
```

根据质量、刚度和阻尼系数创建一个弹簧。

有关这些参数的单位，请参阅 [mass]、[stiffness] 和 [damping]。

### SpringDescription.withDampingRatio()

```dart
SpringDescription.withDampingRatio({required double mass, required double stiffness, double ratio = 1.0})
```

根据质量（m）、刚度（k）和阻尼比（ζ）创建一个弹簧。阻尼比描述了弹簧振荡逐渐衰减的过程。通过使用阻尼比，可以定义振荡从一次弹跳到下一次弹跳之间的衰减速度。

在确定要创建的弹簧类型时，阻尼比尤为有用。比值为 1.0 时创建的是临界阻尼弹簧，大于 1.0 时创建的是过阻尼弹簧，小于 1.0 时创建的是欠阻尼弹簧。

有关这些参数的单位，请参阅 [mass] 和 [stiffness]。阻尼比没有单位。

### SpringDescription.withDurationAndBounce()

```dart
SpringDescription.withDurationAndBounce({Duration duration = const Duration(milliseconds: 500), double bounce = 0.0})
```

根据所需的动画时长和弹跳程度创建一个 [SpringDescription](https://www.yuque.com/thyname/flutter.physics/springdescription)。

这提供了一种基于视觉属性 [duration] 和 [bounce] 来定义弹簧的直观方式。有关这些属性的定义，请查阅其相应的文档。

这个构造函数产生的结果与 SwiftUI 的 `spring(duration:bounce:blendDuration:)` 动画相同。

{@tool snippet}

```dart
final SpringDescription spring = SpringDescription.withDurationAndBounce(
  duration: const Duration(milliseconds: 300),
  bounce: 0.3,
);
```

{@end-tool}

另请参阅：

- [SpringDescription](https://www.yuque.com/thyname/flutter.physics/springdescription)，通过显式提供物理参数来创建弹簧。
- [SpringDescription.withDampingRatio]，使用阻尼比和其他物理参数来创建弹簧。

### mass

```dart
double mass
```

弹簧的质量（m）。

单位可以任意选定，但同一系统内的所有弹簧都应使用相同的质量单位。

质量越大，振荡的振幅越大，返回平衡位置所需的时间也越长。

### stiffness

```dart
double stiffness
```

弹簧常数（k）。

刚度的单位为 M/T²，其中 M 是 [mass] 属性所使用的质量单位，T 是驱动 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation) 所使用的时间单位。

刚度定义了弹簧常数，用于衡量弹簧的强度。对于相同的偏离静止位置的程度，刚度较大的弹簧会对所连接的对象施加更大的力。

### damping

```dart
double damping
```

阻尼系数（c）。

它是一个没有物理意义的纯数值，用于描述系统受到扰动后的振荡与衰减情况。阻尼越大，弹性运动的振荡次数越少、振幅越小。

请勿将阻尼**系数**（c）与阻尼**比**（ζ）混淆。若要使用阻尼比创建 [SpringDescription](https://www.yuque.com/thyname/flutter.physics/springdescription)，请使用 [SpringDescription.withDampingRatio] 构造函数。

阻尼系数的单位为 M/T，其中 M 是 [mass] 属性所使用的质量单位，T 是驱动 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation) 所使用的时间单位。

### duration

```dart
Duration get duration
```

[SpringDescription.withDurationAndBounce] 中所使用的 duration 参数。

此值定义了弹簧在感知上的持续时间，用于控制其整体节奏。它大致等于弹簧稳定下来所需的时间，但对于弹跳程度很高的弹簧，它对应的则是振荡周期。

此时长并不代表弹簧停止运动的确切时间。例如，当 [bounce] 为 1 时，尽管 [duration] 的值是有限的，弹簧仍会无限振荡下去。若要在给定容差范围内确定运动何时已经实际停止，请使用 [SpringSimulation.isDone]。

默认为 0.5 秒。

### bounce

```dart
double get bounce
```

[SpringDescription.withDurationAndBounce] 中所使用的 bounce 参数。

此值用于控制弹簧的弹跳程度：

- 值为 0 时，会产生一个没有振荡的临界阻尼弹簧。
- 值介于 0 和 1 之间时会产生欠阻尼效果，此时弹簧会振荡若干次后才稳定下来。值为 1 时表示一个无阻尼的弹簧，将无限振荡下去。
- 负值表示过阻尼，此时的运动缓慢且具有阻力，就像在黏稠的流体中移动一样。

默认为 0。

### toString()

```dart
String toString()
```

# SpringType

```dart
enum SpringType {}
```

[SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation) 用于模拟弹簧时所采用的弹簧解的类型。

请参阅 [SpringSimulation.type]。

不产生弹跳、并以最短时间返回静止位置的弹簧。

会产生弹跳的弹簧。

不产生弹跳，但返回静止位置所需时间比 [criticallyDamped] 更长的弹簧。

# SpringSimulation

```dart
class SpringSimulation extends Simulation {}
```

弹簧模拟。

对遵循胡克定律的、附着于弹簧上的粒子进行建模。

{@tool snippet}

此方法会触发一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)（此前已构造的 `_controller` 字段），以模拟弹簧振荡效果。

```dart
void _startSpringMotion() {
  _controller.animateWith(SpringSimulation(
    const SpringDescription(
      mass: 1.0,
      stiffness: 300.0,
      damping: 15.0,
    ),
    0.0, // starting position
    1.0, // ending position
    0.0, // starting velocity
  ));
}
```

{@end-tool}

该 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 可以与 [AnimatedBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedbuilder) 搭配使用，以动画方式呈现子组件仿佛附着在弹簧上的位置变化。

### SpringSimulation()

```dart
SpringSimulation(SpringDescription spring, double start, double end, double velocity, {bool snapToEnd = false, Tolerance tolerance})
```

根据提供的弹簧描述、起始距离、结束距离和初始速度创建一个弹簧模拟。

起始距离和结束距离参数的单位可以任意选定，但必须与系统中其他长度所使用的单位保持一致。

速度的单位为 L/T，其中 L 为前述任意选定的长度单位，T 为驱动 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation) 所使用的时间单位。

如果 `snapToEnd` 为 true，那么当 [isDone] 返回 true 时，[x] 将被设置为 `end`，[dx] 将被设置为 0。这对于要求模拟必须精确停止在结束值处的过渡效果非常有用，因为弹簧本身可能无法自然地精确到达目标值。默认为 false。

### type

```dart
SpringType get type
```

所模拟弹簧的类型，用于调试目的。

此值根据传入 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation) 构造函数的 [SpringDescription](https://www.yuque.com/thyname/flutter.physics/springdescription) 推导得出。

### x()

```dart
double x(double time)
```

### dx()

```dart
double dx(double time)
```

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```

# ScrollSpringSimulation

```dart
class ScrollSpringSimulation extends SpringSimulation {}
```

一种 [SpringSimulation](https://www.yuque.com/thyname/flutter.physics/springsimulation)，当模拟 [isDone] 时，[x] 的值保证恰好等于结束值。

### ScrollSpringSimulation()

```dart
ScrollSpringSimulation(SpringDescription spring, double start, double end, double velocity, {Tolerance tolerance})
```

根据提供的弹簧描述、起始距离、结束距离和初始速度创建一个弹簧模拟。

有关这些参数单位的详细说明，请参阅父类中的 [SpringSimulation.new] 构造函数。

### x()

```dart
double x(double time)
```
