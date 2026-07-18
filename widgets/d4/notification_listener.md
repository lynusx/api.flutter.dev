@docImport 'layout_builder.dart'; @docImport 'nested_scroll_view.dart'; @docImport 'scroll_notification.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'size_changed_layout_notifier.dart';

# NotificationListenerCallback

```dart
typedef NotificationListenerCallback<T extends Notification> = bool Function(T notification)
```

[Notification](https://www.yuque.com/thyname/flutter.widgets/notification) 监听器的函数签名。

返回 true 以取消通知的冒泡；返回 false 则允许通知继续向上传递给更上层的祖先节点。

[NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 适用于监听 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)、[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)、[GridView](https://www.yuque.com/thyname/flutter.widgets/gridview) 或任何滚动组件中的滚动事件。由 [NotificationListener.onNotification] 使用。

# Notification

```dart
abstract class Notification {}
```

一种可以在组件树中向上冒泡的通知。

可以使用 `is` 运算符检查通知的 [runtimeType]，从而判断通知的类型。

若要在某个子树中监听通知，请使用 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)。

若要发送通知，请在希望发送的通知对象上调用 [dispatch]。该通知将被传递给给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的所有祖先节点中、具有匹配类型参数的 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 组件。

{@tool dartpad} 此示例展示了一个监听 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 通知的 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 组件。当 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中发生滚动事件时，该组件会收到通知。这些事件可能是 [ScrollStartNotification](https://www.yuque.com/thyname/flutter.widgets/scrollstartnotification) 或 [ScrollEndNotification](https://www.yuque.com/thyname/flutter.widgets/scrollendnotification)。

** 代码见 examples/api/lib/widgets/notification_listener/notification.0.dart ** {@end-tool}

另请参阅：

- [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification)，描述了通知的生命周期。
- [ScrollStartNotification](https://www.yuque.com/thyname/flutter.widgets/scrollstartnotification)，返回滚动的起始位置。
- [ScrollEndNotification](https://www.yuque.com/thyname/flutter.widgets/scrollendnotification)，返回滚动的结束位置。
- [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)，用于创建嵌套滚动视图。

### Notification()

```dart
Notification()
```

抽象的 const 构造函数。此构造函数使子类能够提供 const 构造函数，从而可以在 const 表达式中使用。

### dispatch()

```dart
void dispatch(BuildContext? target)
```

从给定的构建上下文（build context）开始，使此通知开始冒泡。

该通知将被传递给给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的所有祖先节点中、具有匹配类型参数的 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 组件。如果 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 为 null，则不会分发该通知。

### toString()

```dart
String toString()
```

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

向给定的描述列表中添加附加信息，供 [toString] 使用。

此方法便于子类协同提供高质量的 [toString] 实现。[Notification](https://www.yuque.com/thyname/flutter.widgets/notification) 基类的 [toString] 实现会调用 [debugFillDescription] 来收集子类提供的有用信息，并将其纳入返回值中。

[debugFillDescription] 的实现应当以调用 `super.debugFillDescription(description)` 开始。

# NotificationListener

```dart
class NotificationListener<T extends Notification> extends ProxyWidget {}
```

一个监听在组件树中向上冒泡的 [Notification](https://www.yuque.com/thyname/flutter.widgets/notification) 的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=cAnFbFoGM50}

只有当通知的 [runtimeType] 是 `T` 的子类型时，通知才会触发 [onNotification] 回调。

若要分发通知，请使用 [Notification.dispatch] 方法。

### NotificationListener()

```dart
NotificationListener({dynamic key, required Widget child, NotificationListenerCallback<T>? onNotification})
```

创建一个监听通知的组件。

### onNotification

```dart
NotificationListenerCallback<T>? onNotification
```

当适当类型的通知到达组件树中的此位置时调用。

返回 true 以取消通知的冒泡；返回 false 则允许通知继续向上传递给更上层的祖先节点。

不同的通知在分发时机上有所不同，主要有两种情况：在帧与帧之间分发，以及在布局过程中分发。

对于在布局过程中分发的通知（例如继承自 [LayoutChangedNotification](https://www.yuque.com/thyname/flutter.widgets/layoutchangednotification) 的通知），此时调用 [State.setState] 来响应通知已为时过晚（因为布局此时正发生在某个后代节点上，根据定义，这是由于通知是向上冒泡的）。对于依赖布局的组件，可以考虑改用 [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder)。

### createElement()

```dart
Element createElement()
```

# LayoutChangedNotification

```dart
class LayoutChangedNotification extends Notification {}
```

表明接收此通知的对象的某个后代节点的布局已发生某种变化，因此任何关于该布局的既有假设都已不再有效。

例如，当你试图对齐多个后代节点时，此通知会很有用。

若要在某个子树中监听通知，请使用 [NotificationListener<LayoutChangedNotification>]。

若要发送通知，请在希望发送的通知对象上调用 [dispatch]。该通知将被传递给给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的所有祖先节点中、具有匹配类型参数的 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener) 组件。

在 widgets 库中，只有 [SizeChangedLayoutNotifier](https://www.yuque.com/thyname/flutter.widgets/sizechangedlayoutnotifier) 类和 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 类会分发此通知（具体而言，它们分别分发 [SizeChangedLayoutNotification](https://www.yuque.com/thyname/flutter.widgets/sizechangedlayoutnotification) 和 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification)）。过渡动画（Transitions）则不会分发此通知。在 build 函数中改变自身的布局，并不会自动触发此通知的分发。如果某个祖先节点期望在任何布局变化时都能收到通知，则必须确保：要么只使用布局永不改变的组件，要么使用会在适当时机通知其祖先节点的组件，或者在适当的时候自行分发该通知。

此外，由于此通知是在布局发生变化时发送的，它仅适用于依赖布局的绘制效果。如果试图利用此通知来改变 build 过程，那么显示效果将总是落后一帧，这会显得非常难看且卡顿。

### LayoutChangedNotification()

```dart
LayoutChangedNotification()
```

创建一个新的 [LayoutChangedNotification](https://www.yuque.com/thyname/flutter.widgets/layoutchangednotification)。
