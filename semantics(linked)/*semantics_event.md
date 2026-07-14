@docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart';

# Assertiveness

```dart
enum Assertiveness {}
```

确定无障碍播报的紧急程度级别。

[AnnounceSemanticsEvent](https://www.yuque.com/thyname/flutter.semantics/announcesemanticsevent) 使用它来确定辅助技术处理播报的优先级。

辅助技术会在用户空闲时朗读变更内容。

辅助技术会中断当前正在进行的任何播报，以将变更通知用户。

此选项应仅用于时间敏感/关键的通知。

# SemanticsEvent

```dart
abstract class SemanticsEvent {}
```

应用程序发送的事件，用于通知感兴趣的监听者用户界面发生了某些变化（例如某个视图发生了滚动）。

这些事件通常由辅助技术解读，以便为用户提供有关当前 UI 状态的额外线索。

### SemanticsEvent()

```dart
SemanticsEvent(String type)
```

初始化内部字段。

[type] 是用于标识该类 [SemanticsEvent](https://www.yuque.com/thyname/flutter.semantics/semanticsevent) 的字符串。

### type

```dart
String type
```

此事件的类型。

引擎使用该类型将此事件转换为相应的原生事件（iOS 上的 `UIAccessibility*Notification`，Android 上的 `AccessibilityEvent`）。

### toMap()

```dart
Map<String, dynamic> toMap({int? nodeId})
```

将此事件转换为可使用 [StandardMessageCodec](https://www.yuque.com/thyname/flutter.services/standardmessagecodec) 编码的 Map。

[nodeId] 是与该事件关联的语义节点的唯一标识符；如果该事件未关联任何语义节点，则为 null。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

返回该事件的数据对象。

### toString()

```dart
String toString()
```

# AnnounceSemanticsEvent

```dart
class AnnounceSemanticsEvent extends SemanticsEvent {}
```

用于语义播报的事件。

此事件应用于那些系统无法因 UI 状态变化而无缝播报的公告。

例如，相机应用程序可以使用此方法针对取景器中的对象发出无障碍播报。

在可能的情况下，应优先使用 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 等机制隐式触发播报，而不是使用此事件。

### Android

Android 已[弃用播报事件][1]，因为它会带来干扰性行为，迫使 TalkBack 清空其语音队列并朗读所提供的文本。请改用 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 等机制隐式触发播报。

[1]: https://developer.android.com/reference/android/view/View#announceForAccessibility(java.lang.CharSequence)

### AnnounceSemanticsEvent()

```dart
AnnounceSemanticsEvent(String message, TextDirection textDirection, int viewId, {Assertiveness assertiveness = Assertiveness.polite})
```

构造一个事件，用于触发平台针对指定视图发出播报。

### viewId

```dart
int viewId
```

此播报所对应的视图。

### message

```dart
String message
```

要播报的消息。

### textDirection

```dart
TextDirection textDirection
```

[message] 的文本方向。

### assertiveness

```dart
Assertiveness assertiveness
```

确定该播报应中断现有播报，还是在其后排队等待。

在 Web 上，此选项使用 aria-live 级别来设置播报的紧急程度。在 iOS、Android、Windows、Linux、macOS 和 Fuchsia 上，此选项目前没有任何效果。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# TooltipSemanticsEvent

```dart
class TooltipSemanticsEvent extends SemanticsEvent {}
```

用于工具提示语义播报的事件。

此事件仅由 Android 用于播报工具提示的值。

### TooltipSemanticsEvent()

```dart
TooltipSemanticsEvent(String message)
```

构造一个事件，用于触发平台发出工具提示播报。

### message

```dart
String message
```

工具提示的文本内容。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# LongPressSemanticsEvent

```dart
class LongPressSemanticsEvent extends SemanticsEvent {}
```

触发长按语义反馈的事件。

目前仅在 Android 上受支持。当 TalkBack 启用时，会触发特定的长按提示音。

### LongPressSemanticsEvent()

```dart
LongPressSemanticsEvent()
```

构造一个事件，用于触发平台发出长按语义反馈。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# TapSemanticEvent

```dart
class TapSemanticEvent extends SemanticsEvent {}
```

触发点击语义反馈的事件。

目前仅在 Android 上受支持。当 TalkBack 启用时，会触发特定的点击提示音。

### TapSemanticEvent()

```dart
TapSemanticEvent()
```

构造一个事件，用于触发平台发出长按语义反馈。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```

# FocusSemanticEvent

```dart
class FocusSemanticEvent extends SemanticsEvent {}
```

用于移动无障碍焦点的事件。

通常不建议使用此 API，因为它可能打破用户对无障碍焦点工作方式的预期，因此使用时应格外谨慎。

一个可能的使用场景：例如，当前获得焦点的渲染对象被另一个渲染对象替换。一般来说，应尽可能避免此类设计。如果无法避免，则可能需要将焦点重新移动到新添加的渲染对象上。

一个不推荐的示例：当新的弹出框或下拉菜单打开时，在这种情况下移动焦点可能会使用户感到困惑，并降低可访问性。

{@tool snippet}

以下代码片段展示了如何在某个 Widget 上请求焦点。

```dart
class MyWidget extends StatefulWidget {
  const MyWidget({super.key});

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  final GlobalKey mykey = GlobalKey();

  @override
  void initState() {
    super.initState();
    // Using addPostFrameCallback because changing focus need to wait for the widget to finish rendering.
    WidgetsBinding.instance.addPostFrameCallback((_) {
      mykey.currentContext?.findRenderObject()?.sendSemanticsEvent(const FocusSemanticEvent());
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('example'),
      ),
      body: Column(
        children: <Widget>[
          const Text('Hello World'),
          const SizedBox(height: 50),
          Text('set focus here', key: mykey),
        ],
      ),
    );
  }
}
```

{@end-tool}

此功能目前仅支持 Android 和 iOS。

### FocusSemanticEvent()

```dart
FocusSemanticEvent()
```

构造一个事件，用于触发平台发出焦点变更。

### getDataMap()

```dart
Map<String, dynamic> getDataMap()
```
