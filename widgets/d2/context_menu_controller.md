@docImport 'package:flutter/services.dart';

# ContextMenuController

```dart
class ContextMenuController {}
```

在指定位置构建并管理上下文菜单。

整个应用中同一时刻只能显示一个上下文菜单。对某个实例调用 [show] 方法，将会隐藏其他已显示的实例。

{@tool dartpad} 此示例展示了如何使用 GestureDetector，在部件子树中的任意位置响应右键点击或长按操作以显示上下文菜单。

** See code in examples/api/lib/material/context_menu/context_menu_controller.0.dart ** {@end-tool}

另请参阅：

- [BrowserContextMenu](https://www.yuque.com/thyname/flutter.services/browsercontextmenu)，用于在 Web 平台上禁用浏览器自带的上下文菜单，从而显示 Flutter 渲染的上下文菜单。

### ContextMenuController()

```dart
ContextMenuController({VoidCallback? onRemove})
```

创建一个可通过 [show] 显示的上下文菜单。

### onRemove

```dart
VoidCallback? onRemove
```

当此菜单被移除时调用。

### show()

```dart
void show({required BuildContext context, required WidgetBuilder contextMenuBuilder, Widget? debugRequiredFor})
```

显示指定的上下文菜单。

由于同一时刻只能显示一个上下文菜单，调用此方法也会移除其他已显示的上下文菜单。

### removeAny()

```dart
void removeAny()
```

从 UI 中移除当前显示的上下文菜单。

如果当前没有显示任何上下文菜单，则不执行任何操作。

如果某个菜单被移除，并且该菜单在创建时提供了 [onRemove] 回调，则会调用该回调。

另请参阅：

- [remove]，仅移除当前实例。

### isShown

```dart
bool get isShown
```

当且仅当此菜单当前正在显示时为 true。

### markNeedsBuild()

```dart
void markNeedsBuild()
```

使底层 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 在下一次管线刷新（pipeline flush）时重新构建。

如果 `contextMenuBuilder` 的输出发生了变化，则必须调用此函数。

如果上下文菜单当前未显示，则会报错。

另请参阅：

- [OverlayEntry.markNeedsBuild]

### remove()

```dart
void remove()
```

从 UI 中移除此菜单。

如果此实例当前未显示，则不执行任何操作。换言之，如果当前显示的是另一个上下文菜单，则该菜单不会被移除。

此方法只能调用一次。此实例被移除后不能再次显示，需创建一个新实例。

如果创建此实例时提供了 [onRemove] 方法，则会调用该方法。

另请参阅：

- [removeAny]，移除任何已显示的上下文菜单实例。
