# Simulation

```dart
abstract class Simulation {}
```

所有模拟（simulation）的基类。

模拟用于在一维空间中对某个受到特定力作用的对象进行建模，并暴露以下内容：

- 对象的位置 [x]
- 对象的速度 [dx]
- 模拟是否已经"结束" [isDone]

如果对象在给定的 [tolerance]（容差）范围内已经完全静止，则通常认为该模拟已经"结束"。

[x]、[dx] 和 [isDone] 函数都接受一个时间参数，用于指定需要在哪个时间点进行求值。原则上，模拟可以是无状态的，因此可以使用任意时间进行查询。但在实践中，某些模拟并非如此，调用这些函数中的任意一个都会使模拟推进到指定的时间。

因此，通常应遵循这样一条规则：对同一个模拟进行查询时，所使用的时间应等于或大于此前该模拟所使用过的所有时间。

模拟不规定距离、速度和时间的单位。客户端应当自行建立一套约定，并在所有相关对象中保持一致地使用该约定。

### Simulation()

```dart
Simulation({Tolerance tolerance = Tolerance.defaultTolerance})
```

为子类初始化 [tolerance] 字段。

### x()

```dart
double x(double time)
```

对象在模拟中于给定时间的位置。

### dx()

```dart
double dx(double time)
```

对象在模拟中于给定时间的速度。

### isDone()

```dart
bool isDone(double time)
```

模拟在给定时间是否已经"结束"。

### tolerance

```dart
Tolerance tolerance
```

在 [isDone] 判定模拟为"结束"之前，某一特定时间点的值与模拟实际终点之间必须达到的接近程度。

具有渐近曲线的模拟在技术上永远不会真正"结束"，但一旦某一特定时间点的值与渐近线之间的差异已经无法被察觉，继续进行模拟就没有意义了。容差正是用来确定这种差异是否已经无法被察觉的标准。

### toString()

```dart
String toString()
```
