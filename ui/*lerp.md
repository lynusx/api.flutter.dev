# lerpDouble()

```dart
double? lerpDouble(num? a, num? b, double t)
```

在两个数字 `a` 和 `b` 之间按外推系数 `t` 进行线性插值。

当 `a` 和 `b` 相等，或两者都是 NaN 时，返回 `a`。否则，`a`、`b` 和 `t` 必须为有限值或 `null`，并返回 `a + (b - a) * t` 的计算结果，其中 `null` 默认按 `0.0` 处理。
