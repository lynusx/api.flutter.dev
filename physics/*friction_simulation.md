# FrictionSimulation

```dart
class FrictionSimulation extends Simulation {}
```

对粒子施加阻力使其减速的模拟。

对受到流体阻力（例如空气阻力）影响的粒子进行建模。

当粒子的速度降至零（在当前速度 [tolerance] 范围内）时，模拟结束。

### FrictionSimulation()

```dart
FrictionSimulation(double drag, double position, double velocity, {Tolerance tolerance, double constantDeceleration = 0})
```

使用给定的参数创建一个 [FrictionSimulation]，这些参数分别为：流体阻力系数 _cₓ_（一个无单位的数值）；初始位置 _x₀_（其长度单位与 [x] 所使用的单位相同）；以及初始速度 _dx₀_（其速度单位与 [dx] 所使用的单位相同）。

### FrictionSimulation.through()

```dart
FrictionSimulation.through(double startPosition, double endPosition, double startVelocity, double endVelocity)
```

创建一个新的摩擦模拟，其流体阻力系数（_cₓ_）经过设定，以确保模拟能够在指定的起始和结束位置及速度处开始和结束。

位置必须使用 [x] 所要求的单位，速度必须使用 [dx] 所要求的单位。

起始速度与结束速度的符号必须相同，起始速度的幅值必须大于结束速度的幅值，并且速度的方向必须与粒子从起始位置到达结束位置所需的方向相符。

### x()

```dart
double x(double time)
```

### dx()

```dart
double dx(double time)
```

### finalX

```dart
double get finalX
```

[x] 在 `double.infinity` 处的值。

### timeAtX()

```dart
double timeAtX(double x)
```

`x(time)` 的值等于 [x] 时所对应的时间。

如果模拟永远不会到达 [x]，则返回 `double.infinity`。

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```

# BoundedFrictionSimulation

```dart
class BoundedFrictionSimulation extends FrictionSimulation {}
```

一种 [FrictionSimulation]，会将所建模的粒子限制在特定的取值范围内。

仅位置会被限制。一旦粒子到达边界，速度 [dx] 仍会继续报告未经限制的模拟速度。

### BoundedFrictionSimulation()

```dart
BoundedFrictionSimulation(double drag, double position, double velocity, double _minX, double _maxX)
```

使用给定的参数创建一个 [BoundedFrictionSimulation]，这些参数分别为：流体阻力系数 _cₓ_（一个无单位的数值）；初始位置 _x₀_（其长度单位与 [x] 所使用的单位相同）；初始速度 _dx₀_（其速度单位与 [dx] 所使用的单位相同）；位置的最小值；以及位置的最大值。最小值和最大值必须与初始位置使用相同的单位，并且初始位置必须处于给定的范围之内。

### x()

```dart
double x(double time)
```

### isDone()

```dart
bool isDone(double time)
```

### toString()

```dart
String toString()
```
