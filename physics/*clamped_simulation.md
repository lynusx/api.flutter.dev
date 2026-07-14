# ClampedSimulation

```dart
class ClampedSimulation extends Simulation {}
```

对另一个模拟施加限制的模拟。

这些限制仅作用于另一个模拟的输出结果。例如，若对一个重力模拟施加最大位置限制，且粒子的初始速度向上、加速度向下，而最大位置介于初始位置与曲线顶点之间，那么粒子返回其初始位置所需的时间将与未施加该最大值限制时相同；唯一的区别在于，在那些原本会报告更高位置的时间段内，位置将被报告为固定于该最大值。

同样地，这意味着当 [x] 或 [dx] 其中之一被限制时，[x] 值的变化速率将与所报告的 [dx] 值不一致。

[isDone] 的逻辑不受限制的影响，它反映的是底层模拟本身的逻辑。

### ClampedSimulation()

```dart
ClampedSimulation(Simulation simulation, {double xMin = double.negativeInfinity, double xMax = double.infinity, double dxMin = double.negativeInfinity, double dxMax = double.infinity})
```

创建一个 [ClampedSimulation](https://www.yuque.com/thyname/flutter.physics/clampedsimulation)，用于限制给定的模拟。

命名参数指定了应用于 [x] 和 [dx] 的限制行为的取值范围。

### simulation

```dart
Simulation simulation
```

被限制的模拟。对 [x]、[dx] 和 [isDone] 的调用都会转发给该模拟。

### xMin

```dart
double xMin
```

应用于 [x] 的最小值。

### xMax

```dart
double xMax
```

应用于 [x] 的最大值。

### dxMin

```dart
double dxMin
```

应用于 [dx] 的最小值。

### dxMax

```dart
double dxMax
```

应用于 [dx] 的最大值。

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
