# Tolerance

```dart
class Tolerance {}
```

用于指定被视为相等时，距离、时长与速度差异所允许的最大幅度的结构体。

### Tolerance()

```dart
Tolerance({double distance = _epsilonDefault, double time = _epsilonDefault, double velocity = _epsilonDefault})
```

创建一个 [Tolerance] 对象。默认情况下，距离、时间和速度的容差均为 ±0.001；构造函数的参数可以覆盖此默认值。

### defaultTolerance

```dart
Tolerance defaultTolerance
```

三个值均为 0.001 的默认容差。

### distance

```dart
double distance
```

两点之间被视为在容差范围内时，所允许的最大距离幅度。

距离容差所使用的单位，必须与将与该容差进行比较的距离所使用的单位相同。

### time

```dart
double time
```

两个时间点之间被视为在容差范围内时，所允许的最大时长幅度。

时间容差所使用的单位，必须与将与该容差进行比较的时间所使用的单位相同。

### velocity

```dart
double velocity
```

两个速度之间被视为在容差范围内时，所允许的最大差异幅度。

速度容差所使用的单位，必须与将与该容差进行比较的速度所使用的单位相同。

### toString()

```dart
String toString()
```
