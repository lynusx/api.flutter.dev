@docImport 'package:flutter/widgets.dart';

# SemanticsService

```dart
abstract final class SemanticsService {}
```

允许访问平台的辅助功能服务。

此服务发送的事件由 Flutter 引擎中特定于平台的辅助功能桥接层处理。

如果可能，请优先使用像 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 这样的机制隐式触发播报，而不是使用此事件。

### announce()

```dart
Future<void> announce(String message, TextDirection textDirection, {Assertiveness assertiveness = Assertiveness.polite})
```

发送语义播报。

此方法已弃用。请优先使用 [sendAnnouncement]。

{@template flutter.semantics.service.announce} 此方法应用于播报那些不会因 UI 状态变化而被系统无缝播报的内容。

例如，相机应用可以使用此方法对取景器中的物体进行辅助功能播报。

播报的紧急程度由 [assertiveness] 决定。目前，这仅在 Web 引擎上受支持，对其他平台没有影响。默认模式为 [Assertiveness.polite]。

并非所有平台都支持播报。在调用此方法之前，请使用 [MediaQuery.supportsAnnounceOf] 检查是否支持。

### Android

由于其对 TalkBack 的干扰性行为——会强制清空其语音队列并朗读所提供的文本——Android 已经[弃用了播报事件][1]。请改用像 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 这样的机制隐式触发播报。

[1]: https://developer.android.com/reference/android/view/View#announceForAccessibility(java.lang.CharSequence) {@endtemplate}

### sendAnnouncement()

```dart
Future<void> sendAnnouncement(FlutterView view, String message, TextDirection textDirection, {Assertiveness assertiveness = Assertiveness.polite})
```

为特定视图发送语义播报。

可以使用 [View.of] 获取当前的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。

{@macro flutter.semantics.service.announce}

### tooltip()

```dart
Future<void> tooltip(String message)
```

发送工具提示的语义播报。

目前仅在 Android 上生效。[message] 的内容将由 TalkBack 朗读。
