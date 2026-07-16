@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'safe_area.dart';

# DisplayFeatureSubScreen

```dart
class DisplayFeatureSubScreen extends StatelessWidget {}
```

定位 [child]，使其避免与任何将屏幕分割为多个子屏幕的 [DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature) 重叠。

当同时满足以下两个条件时，[DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature) 会将屏幕分割为多个子屏幕：

- 它遮挡了屏幕，即它所占据的区域不为 0，或者其 `state` 为 [DisplayFeatureState.postureHalfOpened]。
- 它的高度至少与屏幕相同（从而产生左右两个子屏幕），或者它的宽度至少与屏幕相同（从而产生上下两个子屏幕）。

在确定子屏幕后，会使用离 [anchorPoint] 最近的那个子屏幕来渲染内容。

如果未提供 [anchorPoint]，则使用 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)：

- 对于 [TextDirection.ltr]，[anchorPoint] 为 `Offset.zero`，这会使内容显示在左上方的子屏幕中。
- 对于 [TextDirection.rtl]，[anchorPoint] 为 `Offset(double.maxFinite, 0)`，这会使内容显示在右上方的子屏幕中。

如果未提供 [anchorPoint]，且树中没有 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 祖先 Widget，则此 Widget 会在调试模式下的构建过程中触发断言。

与 [SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea) 类似，此 Widget 假定它与最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先之间没有额外的内边距。[child] 会被包裹在一个新的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 实例中，该实例仅包含所选子屏幕中存在的 [DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature)，其坐标相对于该子屏幕。内边距也会被相应调整，将此 Widget 所避开的各边归零。

另请参阅：

- [showDialog](https://www.yuque.com/thyname/flutter.material/showdialog)，一种显示 [DialogRoute](https://www.yuque.com/thyname/flutter.material/dialogroute) 的方式。
- [showCupertinoDialog](https://www.yuque.com/thyname/flutter.cupertino/showcupertinodialog)，显示 iOS 风格对话框。

### DisplayFeatureSubScreen()

```dart
DisplayFeatureSubScreen({dynamic key, Offset? anchorPoint, required Widget child})
```

创建一个定位其子组件以避开显示特性（display features）的 Widget。

### anchorPoint

```dart
Offset? anchorPoint
```

{@template flutter.widgets.DisplayFeatureSubScreen.anchorPoint} 用于选择最近子屏幕的锚点。

如果锚点位于其中一个子屏幕内，则选择该子屏幕。否则，使用边缘距该点最近的子屏幕。

[Offset.zero] 是可用屏幕空间的左上角。对于垂直分割的双屏设备，这是左侧屏幕的左上角。

当此值为空时，使用 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)：

- 对于 [TextDirection.ltr]，[anchorPoint] 为 [Offset.zero]，这会使左上方的子屏幕被选中。
- 对于 [TextDirection.rtl]，[anchorPoint] 为 `Offset(double.maxFinite, 0)`，这会使右上方的子屏幕被选中。 {@endtemplate}

### child

```dart
Widget child
```

此 Widget 树中位于此 Widget 下方的 Widget。

为 [child] 提供的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的内边距将被适当调整，以将此 Widget 所避开的各边归零。为 [child] 提供的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 将不再包含任何将屏幕分割为多个子屏幕的显示特性。

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### avoidBounds()

```dart
Iterable<Rect> avoidBounds(MediaQueryData mediaQuery)
```

返回被显示特性遮挡的屏幕区域。

当 [DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature) 所占据的区域不为 0，或者其 `state` 为 [DisplayFeatureState.postureHalfOpened] 时，该 [DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature) 会遮挡屏幕。

### subScreensInBounds()

```dart
Iterable<Rect> subScreensInBounds(Rect wantedBounds, Iterable<Rect> avoidBounds)
```

返回沿 [avoidBounds] 中至少与 [wantedBounds] 同高或同宽的项对 [wantedBounds] 进行分割所得到的子屏幕。
