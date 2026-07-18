@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# NavigationToolbar

```dart
class NavigationToolbar extends StatelessWidget {}
```

[NavigationToolbar](https://www.yuque.com/thyname/flutter.widgets/navigationtoolbar) 是一个布局辅助 Widget，用于沿水平轴排布 3 个 Widget 或 Widget 组，这种排布方式适用于应用程序的导航栏，例如 Material Design 和 iOS 中的导航栏。

[leading] 和 [trailing] Widget 占据该 Widget 两端的位置，并具有合理的尺寸约束，而 [middle] Widget 则以居中对齐或起始对齐的方式占据剩余空间。

可以直接使用带主题的应用栏，例如 Material 的 [AppBar](https://www.yuque.com/thyname/flutter.material/appbar) 或 iOS 的 [CupertinoNavigationBar](https://www.yuque.com/thyname/flutter.cupertino/cupertinonavigationbar)，也可以用更多主题规范包装此 Widget 以构建自定义应用栏。

### NavigationToolbar()

```dart
NavigationToolbar({dynamic key, Widget? leading, Widget? middle, Widget? trailing, bool centerMiddle = true, double middleSpacing = kMiddleSpacing})
```

创建一个以适合工具栏的方式排布其子级的 Widget。

### kMiddleSpacing

```dart
double kMiddleSpacing
```

[middle] Widget 周围的默认间距，单位为 dp。

### leading

```dart
Widget? leading
```

放置在水平工具栏起始位置的 Widget。

### middle

```dart
Widget? middle
```

放置在水平工具栏中间位置的 Widget，占据尽可能多的剩余空间。

### trailing

```dart
Widget? trailing
```

放置在水平工具栏末尾位置的 Widget。

### centerMiddle

```dart
bool centerMiddle
```

是否将 [middle] Widget 对齐到该 Widget 的中心；若为 false，则对齐到 [leading] 旁边。

### middleSpacing

```dart
double middleSpacing
```

[middle] Widget 在水平轴方向上的间距。

默认为 [kMiddleSpacing]。
