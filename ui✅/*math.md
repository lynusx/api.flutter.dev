# clampDouble()

```dart
double clampDouble(double x, double min, double max)
```

与 [num.clamp] 相同，但针对非空的 [double](https://www.yuque.com/thyname/dart.core/double) 做了优化。

由于避免了多态性、装箱以及浮点数的特殊情况处理，此方法速度更快。
