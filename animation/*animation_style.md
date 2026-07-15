@docImport 'package:flutter/material.dart';

# AnimationStyle

```dart
class AnimationStyle with Diagnosticable {}
```

用于覆盖动画的默认参数。

目前，此类被以下 Widget 使用：

- [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)
- [ExpansionTile](https://www.yuque.com/thyname/flutter.material/expansiontile)
- [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)
- [PopupMenuButton](https://www.yuque.com/thyname/flutter.material/popupmenubutton)
- [ScaffoldMessengerState.showSnackBar]
- [showBottomSheet](https://www.yuque.com/thyname/flutter.material/showbottomsheet)
- [showModalBottomSheet](https://www.yuque.com/thyname/flutter.material/showmodalbottomsheet)

如果将 [duration] 和 [reverseDuration] 设置为 [Duration.zero]，则相应的动画将被禁用。

所有参数都是可选的。如果未指定任何参数，则会使用默认动画。

### AnimationStyle()

```dart
AnimationStyle({Curve? curve, Duration? duration, Curve? reverseCurve, Duration? reverseDuration})
```

创建 Animation Style 类的一个实例。

### noAnimation

```dart
AnimationStyle noAnimation
```

创建一个不带动画的 Animation Style 类实例。

### curve

```dart
Curve? curve
```

如果指定了此参数，动画将使用此曲线。

### duration

```dart
Duration? duration
```

如果指定了此参数，动画将使用此时长。

### reverseCurve

```dart
Curve? reverseCurve
```

如果指定了此参数，反向动画将使用此曲线。

### reverseDuration

```dart
Duration? reverseDuration
```

如果指定了此参数，反向动画将使用此时长。

### copyWith()

```dart
AnimationStyle copyWith({Curve? curve, Duration? duration, Curve? reverseCurve, Duration? reverseDuration})
```

基于当前选择创建一个新的 [AnimationStyle](https://www.yuque.com/thyname/flutter.animation/animationstyle)，并覆盖所提供的参数。

### merge()

```dart
AnimationStyle merge(AnimationStyle? other)
```

创建一个新的 [AnimationStyle](https://www.yuque.com/thyname/flutter.animation/animationstyle)，它是此动画样式与给定的 `other` 动画样式的组合。

如果 `other` 不为 null，则使用其非空属性来覆盖此样式中相应的属性。

如果 `other` 为 null，则返回此动画样式。

### lerp()

```dart
AnimationStyle? lerp(AnimationStyle? a, AnimationStyle? b, double t)
```

在两种动画样式之间进行线性插值。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
