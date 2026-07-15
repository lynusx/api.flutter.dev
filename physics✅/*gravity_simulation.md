@docImport 'package:flutter/widgets.dart';

# GravitySimulation

```dart
class GravitySimulation extends Simulation {}
```

施加恒定加速力的模拟。

对遵循牛顿第二运动定律的粒子进行建模。当位置超过所定义的阈值时，模拟结束。

{@tool snippet}

此方法会触发一个 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)（此前已构造的 `_controller` 字段），以模拟下落 300 像素的效果。

```dart
void _startFall() {
  _controller.animateWith(GravitySimulation(
    10.0, // acceleration, pixels per second per second
    0.0, // starting position, pixels
    300.0, // ending position, pixels
    0.0, // starting velocity, pixels per second
  ));
}
```

{@end-tool}

该 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 可以与 [AnimatedBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedbuilder) 搭配使用，以动画方式呈现子组件仿佛正在下落的位置变化。

结束距离阈值（构造函数的第三个参数）必须指定为正数，但可以在正方向或负方向上达到该阈值。举例来说（假设负数所代表的物理位置高于正数，正如常见的 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 坐标系那样），如果加速度为正（即"向下"），起始速度为负（即"向上"），且起始距离为零，那么粒子将从原点向上攀升，到达一个平台期，随后回落并越过原点。如果结束距离阈值小于该平台期的高度，模拟将在攀升过程中结束；否则，模拟将在下落过程中、粒子越过原点达到该距离之后结束。

另请参阅：

- [Curves.bounceOut]，一个具有相似效果但包含弹跳效果的 [Curve](https://www.yuque.com/thyname/flutter.animation/curve)。

### GravitySimulation()

```dart
GravitySimulation(double acceleration, double distance, double endDistance, double velocity)
```

使用给定的参数创建一个 [GravitySimulation](https://www.yuque.com/thyname/flutter.physics/gravitysimulation)，这些参数分别为：随时间持续施加的加速度；相对于原点的初始位置；与该原点之间的距离幅值（在任一方向上超过该距离即视为模拟"结束"，此值必须为正数）；以及初始速度。

初始位置和最大距离均以任意长度单位 L、相对于任意原点进行度量。该单位将与 [x] 所使用的单位相匹配。

用于 [x]、[dx] 和 [isDone] 参数的时间单位 T，与前述长度单位相结合，共同决定了速度和加速度参数所必须使用的单位：分别为 L/T 和 L/T²。从 [dx] 获得的速度也使用相同的速度单位。

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
