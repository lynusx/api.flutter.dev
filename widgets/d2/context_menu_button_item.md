# ContextMenuButtonType

```dart
enum ContextMenuButtonType {}
```

上下文菜单中默认可能出现的按钮类型。

另请参阅：

- [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem)，使用此枚举描述上下文菜单中的按钮。

剪切当前文本选区的按钮。

复制当前文本选区的按钮。

将剪贴板内容粘贴到当前获得焦点的文本字段中的按钮。

选中当前获得焦点的文本字段全部内容的按钮。

删除当前文本选区的按钮。

查找当前文本选区的按钮。

为当前文本选区启动网络搜索的按钮。

显示当前文本选区分享界面的按钮。

用于启动 Live Text 输入的按钮。

另请参阅：

- [LiveText](https://www.yuque.com/thyname/flutter.services/livetext)，可从中获取 Live Text 输入的可用性。
- [LiveTextInputStatusNotifier](https://www.yuque.com/thyname/flutter.widgets/livetextinputstatusnotifier)，可从中监听 Live Text 的状态。

除默认按钮类型之外的其他类型。

# ContextMenuButtonItem

```dart
class ContextMenuButtonItem {}
```

上下文菜单按钮的类型和回调。

另请参阅：

- [AdaptiveTextSelectionToolbar](https://www.yuque.com/thyname/flutter.material/adaptivetextselectiontoolbar)，可接收一组 ContextMenuButtonItem，并创建包含指定按钮的平台特定上下文菜单。
- [IOSSystemContextMenuItem](https://www.yuque.com/thyname/flutter.widgets/iossystemcontextmenuitem)，作用类似，但用于 iOS 上系统绘制的上下文菜单项。

### ContextMenuButtonItem()

```dart
ContextMenuButtonItem({required VoidCallback? onPressed, ContextMenuButtonType type = ContextMenuButtonType.custom, String? label})
```

创建一个 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 的 const 实例。

### onPressed

```dart
VoidCallback? onPressed
```

按钮被按下时调用的回调。

### type

```dart
ContextMenuButtonType type
```

此按钮所代表的按钮类型。

### label

```dart
String? label
```

按钮上显示的标签。

如果给定了 [ContextMenuButtonType.custom] 以外的 [type]，且未提供标签，则会查找该平台上该类型的默认标签。

### copyWith()

```dart
ContextMenuButtonItem copyWith({VoidCallback? onPressed, ContextMenuButtonType? type, String? label})
```

创建一个新的 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem)，并覆盖所提供的参数。
