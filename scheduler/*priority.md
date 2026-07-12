@docImport 'binding.dart';

# Priority

```dart
class Priority {}
```

任务优先级，用于传递给 [SchedulerBinding.scheduleTask]。

### value

```dart
int get value
```

描述此 Priority 值的整数。

### idle

```dart
Priority idle
```

在没有动画运行时，于所有其他任务之后运行的任务。

### animation

```dart
Priority animation
```

即使动画正在运行也会运行的任务。

### touch

```dart
Priority touch
```

即使用户正在与设备交互也会运行的任务。

### kMaxOffset

```dart
int kMaxOffset
```

用于限制相对优先级的最大偏移量。

通过反复取相对偏移量，仍然可以使优先级的偏移超过此数值，但通常不建议这样做。

### operator +()

```dart
Priority operator +(int offset)
```

返回相对于此优先级的一个优先级。

正的 [offset] 表示更高的优先级。

参数 [offset] 会被限制在 ±[kMaxOffset] 范围内。

### operator -()

```dart
Priority operator -(int offset)
```

返回相对于此优先级的一个优先级。

正的偏移量表示更低的优先级。

参数 [offset] 会被限制在 ±[kMaxOffset] 范围内。
