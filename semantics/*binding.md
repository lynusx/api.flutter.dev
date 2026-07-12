@docImport 'package:flutter/widgets.dart';

@docImport 'semantics.dart';

# SemanticsBinding

```dart
mixin SemanticsBinding on BindingBase {}
```

语义层与 Flutter 引擎之间的粘合层。

### initInstances()

```dart
void initInstances()
```

### instance

```dart
SemanticsBinding get instance
```

当前的 [SemanticsBinding]（如果已创建）。

提供对此 mixin 所公开功能的访问。必须先初始化该绑定才能使用此 getter；这通常通过调用 [runApp] 或 [WidgetsFlutterBinding.ensureInitialized] 完成。

### semanticsEnabled

```dart
bool get semanticsEnabled
```

是否必须收集语义信息。

如果平台已请求生成语义信息，或者已调用 [ensureSemantics]，则返回 true。

要在此值发生变化时收到通知，请使用 [addSemanticsEnabledListener] 注册监听器。

### addSemanticsEnabledListener()

```dart
void addSemanticsEnabledListener(VoidCallback listener)
```

添加一个在 [semanticsEnabled] 变化时调用的 `listener`。

另请参阅：

- [removeSemanticsEnabledListener]，用于再次移除该监听器。
- [ValueNotifier.addListener]，记录了监听器如何以及何时被调用。

### removeSemanticsEnabledListener()

```dart
void removeSemanticsEnabledListener(VoidCallback listener)
```

移除通过 [addSemanticsEnabledListener] 添加的 `listener`。

另请参阅：

- [ValueNotifier.removeListener]，记录了如何移除监听器。

### addSemanticsActionListener()

```dart
void addSemanticsActionListener(ValueSetter<ui.SemanticsActionEvent> listener)
```

添加一个监听器，每当接收到 [ui.SemanticsActionEvent] 时都会调用它。

这些监听器会在调用 [performSemanticsAction] 之前被调用。

要移除该监听器，请调用 [removeSemanticsActionListener]。

### removeSemanticsActionListener()

```dart
void removeSemanticsActionListener(ValueSetter<ui.SemanticsActionEvent> listener)
```

移除之前通过 [addSemanticsActionListener] 添加的监听器。

### getRectOfSemanticsNodeInViewCoordinates()

```dart
ui.Rect? getRectOfSemanticsNodeInViewCoordinates(int viewId, int nodeId)
```

返回具有给定 [viewId] 的视图中，具有给定 [nodeId] 的语义节点的全局矩形区域。

该矩形位于该视图渲染树的全局坐标系中，以逻辑像素表示。这对于需要响应语义操作并需要获取接收到该操作的语义节点在屏幕上位置的 widget 很有用。

在非 release 构建中，如果视图未知、视图没有语义所有者或找不到该节点，则会触发断言并返回 null。调用方应仅在响应语义操作时调用此方法，在这种情况下三项查找均应成功。

### debugOutstandingSemanticsHandles

```dart
int get debugOutstandingSemanticsHandles
```

已注册以监听语义信息的客户端数量。

每次调用 [ensureSemantics] 时该数量增加，每次调用 [SemanticsHandle.dispose] 时该数量减少。

### ensureSemantics()

```dart
SemanticsHandle ensureSemantics()
```

创建一个新的 [SemanticsHandle] 并请求收集语义信息。

只有当存在对语义信息感兴趣的客户端时，才会收集语义信息。这些客户端通过持有一个 [SemanticsHandle] 来表达其兴趣。

客户端可以通过调用 [SemanticsHandle.dispose] 来关闭其 [SemanticsHandle]。一旦所有未完成的 [SemanticsHandle] 对象都被关闭，将不再收集语义信息。

### performSemanticsAction()

```dart
void performSemanticsAction(ui.SemanticsActionEvent action)
```

每当平台请求对某个 [SemanticsNode] 执行操作时调用。

当用户通过辅助功能服务（例如 TalkBack 和 VoiceOver）与应用交互，并在获得焦点的节点上发起某个操作时，会调用此回调。

混入 [SemanticsBinding] 的绑定必须实现此方法，并对由 [ui.SemanticsActionEvent.nodeId] 指定的 [SemanticsNode] 执行给定的 `action`。

参见 [dart:ui.PlatformDispatcher.onSemanticsActionEvent]。

### accessibilityFeatures

```dart
ui.AccessibilityFeatures get accessibilityFeatures
```

当前生效的一组 [ui.AccessibilityFeatures]。

此值在绑定首次初始化时设置，并在标志发生变化时更新。

要监听辅助功能特性的变化，请创建一个 [WidgetsBindingObserver] 并监听 [WidgetsBindingObserver.didChangeAccessibilityFeatures]。

### handleAccessibilityFeaturesChanged()

```dart
void handleAccessibilityFeaturesChanged()
```

当平台辅助功能特性发生变化时调用。

参见 [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged]。

### createSemanticsUpdateBuilder()

```dart
ui.SemanticsUpdateBuilder createSemanticsUpdateBuilder()
```

创建一个空的语义更新构建器。

调用方负责填写语义节点的更新内容。

[SemanticsOwner] 使用此方法为其所有语义更新创建构建器。

### disableAnimations

```dart
bool get disableAnimations
```

平台正在请求禁用或简化动画。

可以通过设置 [debugSemanticsDisableAnimations] 在测试或调试时覆盖此设置。

# SemanticsHandle

```dart
class SemanticsHandle {}
```

对框架生成的语义信息的引用。

只有当存在对语义信息感兴趣的客户端时，才会收集语义信息。这些客户端通过持有一个 [SemanticsHandle] 来表达其兴趣。当客户端不再需要语义信息时，必须在 [SemanticsHandle] 上调用 [dispose] 以将其关闭。当所有已打开的 [SemanticsHandle] 都被释放后，框架将停止更新语义信息。

要获取 [SemanticsHandle]，请调用 [SemanticsBinding.ensureSemantics]。

### dispose()

```dart
void dispose()
```

关闭语义句柄。

当所有未完成的 [SemanticsHandle] 对象都被关闭后，框架将停止生成语义信息。
