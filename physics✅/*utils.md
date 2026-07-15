# nearEqual()

```dart
bool nearEqual(double? a, double? b, double epsilon)
```

判断两个 double 值是否彼此处于给定的距离范围内。

`epsilon` 参数必须为正数且不能为空。`a` 和 `b` 参数可以为空。空值仅会被视为与另一个空值"近似相等"。

# nearZero()

```dart
bool nearZero(double a, double epsilon)
```

判断一个 double 值是否处于与零的给定距离范围内。

epsilon 参数必须为正数。
