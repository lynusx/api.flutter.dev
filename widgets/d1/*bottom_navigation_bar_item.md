@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'icon.dart'; @docImport 'icon_theme.dart'; @docImport 'image_icon.dart'; @docImport 'text.dart';

# BottomNavigationBarItem

```dart
class BottomNavigationBarItem {}
```

Material 的 [BottomNavigationBar](https://www.yuque.com/thyname/flutter.material/bottomnavigationbar) 或 iOS 主题的 [CupertinoTabBar](https://www.yuque.com/thyname/flutter.cupertino/cupertinotabbar) 中带有图标和标题的交互式按钮。

此类很少单独使用，通常嵌入在上述底部导航组件中。

另请参阅：

- [BottomNavigationBar](https://www.yuque.com/thyname/flutter.material/bottomnavigationbar)
- <https://material.io/design/components/bottom-navigation.html>
- [CupertinoTabBar](https://www.yuque.com/thyname/flutter.cupertino/cupertinotabbar)
- <https://developer.apple.com/design/human-interface-guidelines/tab-bars/>

### BottomNavigationBarItem()

```dart
BottomNavigationBarItem({Key? key, required Widget icon, String? label, Widget? activeIcon, Color? backgroundColor, String? tooltip, String? semanticsLabel})
```

创建一个用于 [BottomNavigationBar.items] 的条目。

在 Material Design 的 [BottomNavigationBar](https://www.yuque.com/thyname/flutter.material/bottomnavigationbar) 中使用时，参数 [icon] 不应为 null，参数 [label] 也不应为 null。

### key

```dart
Key? key
```

传递给生成组件的键。

这使得可以通过键来识别不同的 [BottomNavigationBarItem](https://www.yuque.com/thyname/flutter.widgets/bottomnavigationbaritem)。

当响应某个条目被点击而改变导航栏中条目数量时，为每个条目提供键可以使水波纹动画正确定位。

### icon

```dart
Widget icon
```

该条目的图标。

通常该图标是 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 或 [ImageIcon](https://www.yuque.com/thyname/flutter.widgets/imageicon) 组件。如果提供了其他类型的组件，则该组件应自行配置以匹配当前的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 大小和颜色。

如果提供了 [activeIcon]，则此图标仅在条目未被选中时显示。

为了使底部导航栏更易于访问，建议选择同时具有描边版和填充版的图标，例如 [Icons.cloud] 和 [Icons.cloud_queue]。[icon] 应设置为描边版本，[activeIcon] 应设置为填充版本。

如果某个图标没有对应的描边版或填充版，则不要搭配不相关的图标，而应使用 [BottomNavigationBarType.shifting]。

### activeIcon

```dart
Widget activeIcon
```

当此底部导航条目被选中时显示的替代图标。

如果未提供此图标，底部导航栏将在两种状态下都显示 [icon]。

另请参阅：

- [BottomNavigationBarItem.icon]，其中描述了如何搭配图标。

### label

```dart
String? label
```

此 [BottomNavigationBarItem](https://www.yuque.com/thyname/flutter.widgets/bottomnavigationbaritem) 的文本标签。

它将用于创建一个 [Text](https://www.yuque.com/thyname/flutter.widgets/text) 组件，放置在底部导航栏中。

### backgroundColor

```dart
Color? backgroundColor
```

Material [BottomNavigationBar](https://www.yuque.com/thyname/flutter.material/bottomnavigationbar) 中该条目背景径向动画的颜色。

如果导航栏的类型为 [BottomNavigationBarType.shifting]，则在此条目被点击时，整个导航栏都会被填充为 [backgroundColor]，这将覆盖 [BottomNavigationBar.backgroundColor]。

不适用于 [CupertinoTabBar](https://www.yuque.com/thyname/flutter.cupertino/cupertinotabbar)。若要直接控制不变的导航栏颜色，请使用 [CupertinoTabBar.backgroundColor]。

另请参阅：

- [Icon.color] 和 [ImageIcon.color]，用于控制图标本身的前景色。

### tooltip

```dart
String? tooltip
```

此 [BottomNavigationBarItem](https://www.yuque.com/thyname/flutter.widgets/bottomnavigationbaritem) 的 [Tooltip](https://www.yuque.com/thyname/flutter.material/tooltip) 中显示的文本。

只有当 [tooltip] 被设置为非空字符串时，该条目才会显示 [Tooltip](https://www.yuque.com/thyname/flutter.material/tooltip)。

默认为 null，此时不显示提示。

### semanticsLabel

```dart
String? semanticsLabel
```

此条目的语义标签。

无障碍工具使用它来描述该条目。如果提供了此值，它将覆盖无障碍工具读取的默认 [label] 字符串。

当视觉标签不能完全描述操作或目标位置，或者你想为屏幕阅读器用户提供额外的上下文信息时，此属性非常有用。

如果为 null，则使用默认的语义描述。
