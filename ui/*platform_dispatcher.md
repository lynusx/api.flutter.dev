# VoidCallback

```dart
typedef VoidCallback = void Function()
```

无参数且不返回数据的回调函数签名。

# FrameCallback

```dart
typedef FrameCallback = void Function(Duration duration)
```

[PlatformDispatcher.onBeginFrame] 的回调函数签名。

`duration` 参数表示当前帧间隔开始的时间点，以自某个纪元以来的时长表示。所有帧的纪元都相同，但可能与 [DateTime] 的纪元不一致。

对于满足帧号 `a` 小于帧号 `b` 的任意两帧 `a` 和 `b`，`a` 的 duration 参数将小于或等于 `b` 的 duration 参数。

# TimingsCallback

```dart
typedef TimingsCallback = void Function(List<FrameTiming> timings)
```

[PlatformDispatcher.onReportTimings] 的回调函数签名。

{@template dart.ui.TimingsCallback.list} 该回调接收一个 [FrameTiming] 列表，因为它可能不会在每一帧后立即触发。相反，Flutter 会尝试将多帧批量处理，一次性发送它们的时间信息以降低开销（因为这在发布模式下也可用）。该列表按时间升序排列（最早的帧排在最前）。即使没有后续帧可供批处理，任何一帧的时间信息也会在大约 1 秒内发送（在 profile/debug 模式下为 100ms）。第一帧的时间信息会立即发送，不进行批处理。{@endtemplate}

# PointerDataPacketCallback

```dart
typedef PointerDataPacketCallback = void Function(PointerDataPacket packet)
```

[PlatformDispatcher.onPointerDataPacket] 的回调函数签名。

# KeyDataCallback

```dart
typedef KeyDataCallback = bool Function(KeyData data)
```

[PlatformDispatcher.onKeyData] 的回调函数签名。

如果按键事件已被框架处理且不应继续传播，该回调应返回 true。

# SemanticsActionEventCallback

```dart
typedef SemanticsActionEventCallback = void Function(SemanticsActionEvent action)
```

[PlatformDispatcher.onSemanticsActionEvent] 的回调函数签名。

# HitTestCallback

```dart
typedef HitTestCallback = HitTestResponse Function(HitTestRequest request)
```

[PlatformDispatcher.onHitTest] 的回调函数签名。

# PlatformMessageResponseCallback

```dart
typedef PlatformMessageResponseCallback = void Function(ByteData? data)
```

平台消息响应的回调函数签名。

用作 [PlatformDispatcher.sendPlatformMessage] 和 [PlatformDispatcher.onPlatformMessage] 的参数。

# PlatformMessageCallback

```dart
typedef PlatformMessageCallback = void Function(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

已弃用。请迁移到 [ChannelBuffers.setListener]。

[PlatformDispatcher.onPlatformMessage] 的回调函数签名。

# ErrorCallback

```dart
typedef ErrorCallback = bool Function(Object exception, StackTrace stackTrace)
```

[PlatformDispatcher.onError] 的回调函数签名。

如果此方法返回 false，引擎可能会使用某种后备机制来提供有关错误的信息。

调用此方法后，进程或 VM 可能会终止。某些严重的未处理错误可能也无法调用此方法，例如 Dart 编译错误或进程终止错误。

# RootIsolateToken

```dart
class RootIsolateToken {}
```

表示根 isolate 的令牌。

### instance

```dart
RootIsolateToken? instance
```

执行此 Dart 代码的根 isolate 的令牌。如果此 Dart 代码未在根 isolate 上执行，[instance] 将为 null。

# PlatformDispatcher

```dart
class PlatformDispatcher {}
```

平台事件分发器单例。

与宿主操作系统交互的最基础接口。

这是来自平台的平台消息和配置事件的中心入口点。

它暴露了核心调度 API、输入事件回调、图形绘制 API 以及其他此类核心服务。

它管理应用程序的 [views] 列表以及各种平台属性的 [configuration]。

请考虑避免通过 [PlatformDispatcher.instance] 静态引用此单例，而是优先使用绑定进行依赖解析，例如 `WidgetsBinding.instance.platformDispatcher`。有关为何推荐此做法的更多信息，请参阅 [PlatformDispatcher.instance]。

### instance

```dart
PlatformDispatcher get instance
```

[PlatformDispatcher] 单例。

请考虑避免通过 [PlatformDispatcher.instance] 静态引用此单例，而是优先使用绑定进行依赖解析，例如 `WidgetsBinding.instance.platformDispatcher`。

静态访问此对象意味着 Flutter 在测试中几乎没有（如果有的话）伪造或模拟该对象的选项。即使 Dart 提供了特殊的语言结构来强制遮蔽此类属性，这些机制也只对测试合理，而对于 Flutter 未来希望在运行时选择合适实现的场景来说并不合理。

唯一适合静态使用 [PlatformDispatcher.instance] 对象的场景是：在调用 `runApp()` 或 `WidgetsFlutterBinding.instance.ensureInitialized()` 初始化绑定之前就需要访问这些 API。在这种情况下，虽然不太理想，但有必要静态使用该对象。

### onPlatformConfigurationChanged

```dart
VoidCallback? get onPlatformConfigurationChanged
```

当平台配置发生变化时调用。

引擎在设置该回调时所处的相同 zone 中调用此回调。

### onPlatformConfigurationChanged

```dart
set onPlatformConfigurationChanged(VoidCallback? callback)
```

### displays

```dart
Iterable<Display> get displays
```

当前的显示器列表。

如果其中任何一个的配置发生变化，将调用 [onMetricsChanged]。

要获取某个 [FlutterView] 所在的显示器，请使用 [FlutterView.display]。

平台可能会限制应用程序可获取的关于次要显示器和/或没有活动应用窗口的显示器的信息。

目前，在 Android 和 Web 上，此集合仅包含当前窗口所在的显示器。在 iOS 上，它仅包含手机或平板上的主显示器。在 Linux 以外的桌面平台上，它仅包含一个具有有效刷新率但尺寸和设备像素比无效的主显示器。

### views

```dart
Iterable<FlutterView> get views
```

当前的视图列表，包括应用程序使用的顶级平台窗口。

如果其中任何一个的配置发生变化，将调用 [onMetricsChanged]。

### view()

```dart
FlutterView? view({required int id})
```

如果存在具有给定 ID 的 [FlutterView]，则返回该视图，否则返回 null。

### implicitView

```dart
FlutterView? get implicitView
```

当平台无法创建窗口时，由引擎提供的 [FlutterView]；或者出于向后兼容性考虑而提供。

如果平台提供了隐式视图，可用它来引导框架启动。这在为单视图应用程序设计的平台（如具有单一显示器的移动设备）上很常见。

应用程序和库不应依赖此属性一定被设置，因为它可能因引擎配置而为 null。请考虑使用 [View.of] 来查找当前 [BuildContext] 所绘制的 [FlutterView]。

虽然所引用的 [FlutterView] 上的属性可能会变化，但该引用本身在应用程序的生命周期内保证不会改变：如果此属性在启动时为 null，则它将在应用程序的整个生命周期内保持为 null。如果它指向某个特定的 [FlutterView]，它将一直指向同一个视图，直到应用程序关闭（尽管引擎可能会自行决定替换或移除该视图的底层支持表面）。

另请参阅：

- [View.of]，用于访问当前视图。
- [PlatformDispatcher.views]，获取平台提供的所有 [FlutterView] 的列表。

### onMetricsChanged

```dart
VoidCallback? get onMetricsChanged
```

每当任何 [views] 的 [ViewConfiguration] 发生变化时被调用的回调。

例如，当设备旋转或应用程序被调整大小时（例如在 Android 上以分屏方式显示应用程序），会调用 `onMetricsChanged`。

引擎在设置该回调时所处的相同 zone 中调用此回调。

框架会注册此回调并相应地更新布局。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层注册此回调调用通知的机制。
- [MediaQuery.of]，实现相同功能的更简单机制。

### onMetricsChanged

```dart
set onMetricsChanged(VoidCallback? callback)
```

### engineId

```dart
int? get engineId
```

运行当前 isolate 的引擎的不透明引擎标识符。可在原生代码中用于检索引擎实例。该标识符在 isolate 运行期间有效。

### onViewFocusChange

```dart
ViewFocusChangeCallback? get onViewFocusChange
```

在焦点跨 [FlutterView] 转移后立即调用的回调。

当平台将焦点从一个 [FlutterView] 移动到另一个时，会调用此回调，指示获得焦点的新视图以及焦点接收的方向。例如，如果焦点以前向方向（可能是按 Tab 键的结果）移动到 ID 为 2 的 [FlutterView]，该回调会收到一个带有 [ViewFocusState.focused] 和 [ViewFocusDirection.forward] 的 [ViewFocusEvent]。

通常，该事件的接收者会将焦点移动到 ID 为 2 的 [FlutterView] 内的第一个可获得焦点的组件来响应。如果某个视图在反向方向上获得焦点（可能是按 Shift + Tab 键的结果），通常会聚焦该视图内的最后一个可获得焦点的组件。

平台可能会移除某个 [FlutterView] 的焦点。例如，在 Web 上，浏览器可以将焦点移动到另一个元素，或移动到浏览器的内置 UI。在桌面上，操作系统可以切换到另一个窗口（例如在 Windows 上使用 Alt + Tab）。在这些场景中，将调用 [onViewFocusChange]，并传入 [ViewFocusState.unfocused] 和 [ViewFocusDirection.undefined]。

接收者通常通过移除应用中的所有焦点指示来响应此事件。

应用程序也可以通过调用 [requestViewFocusChange] 以编程方式请求将焦点移动到指定的 [FlutterView]。

该回调在设置该回调时所处的相同 zone 中调用。

另请参阅：

- [requestViewFocusChange]，以编程方式指示平台将焦点移动到不同的 [FlutterView]。
- [ViewFocusState]，列出了允许的焦点转换状态。
- [ViewFocusDirection]，列出了允许的焦点方向。
- [ViewFocusEvent]，提供给该回调的事件对象。

### onViewFocusChange

```dart
set onViewFocusChange(ViewFocusChangeCallback? callback)
```

### requestViewFocusChange()

```dart
void requestViewFocusChange({required int viewId, required ViewFocusState state, required ViewFocusDirection direction})
```

请求更改 ID 为 [viewId] 的 [FlutterView] 的焦点。

如果应用程序希望请求引擎以前向方向将焦点移动到 ID 为 1 的 [FlutterView]，应使用 [ViewFocusState.focused] 和 [ViewFocusDirection.forward] 调用此方法。

如果相关视图已经拥有焦点，则无需调用此方法，因为这不会产生任何效果。

调用此方法后，如果请求成功完成，引擎将调用 [onViewFocusChange]。

另请参阅：

- [onViewFocusChange]，用于订阅视图焦点变化事件的回调。

### onBeginFrame

```dart
FrameCallback? get onBeginFrame
```

当任意视图开始一帧时调用的回调。

用于通知应用程序现在是使用 [SceneBuilder] API 和 [FlutterView.render] 方法提供场景的适当时机的回调。

在可能的情况下，此回调由所连接屏幕中 VSync 速率最高的硬件 VSync 信号驱动。仅当自上次调用此回调以来已调用过 [PlatformDispatcher.scheduleFrame] 时才会调用它。

### onBeginFrame

```dart
set onBeginFrame(FrameCallback? callback)
```

### onDrawFrame

```dart
VoidCallback? get onDrawFrame
```

在每一帧中，[onBeginFrame] 完成且微任务队列清空后调用的回调。

可用于实现帧渲染的第二阶段，该阶段在 [onBeginFrame] 阶段排队的任何延迟工作之后进行。

### onDrawFrame

```dart
set onDrawFrame(VoidCallback? callback)
```

### onPointerDataPacket

```dart
PointerDataPacketCallback? get onPointerDataPacket
```

当指针数据可用时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

另请参阅：

- [GestureBinding]，Flutter 框架中管理指针事件的类。

### onPointerDataPacket

```dart
set onPointerDataPacket(PointerDataPacketCallback? callback)
```

### onKeyData

```dart
KeyDataCallback? get onKeyData
```

当按键数据可用时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

如果按键事件已被框架处理且不应继续传播，该回调应返回 true。

### onKeyData

```dart
set onKeyData(KeyDataCallback? callback)
```

### onReportTimings

```dart
TimingsCallback? get onReportTimings
```

用于报告最近光栅化帧的 [FrameTiming] 的回调。

相比直接使用 [onReportTimings]，更推荐使用 [SchedulerBinding.addTimingsCallback]，因为 [SchedulerBinding.addTimingsCallback] 允许注册多个回调。

可用于查看应用程序是否丢帧（通过 [FrameTiming.buildDuration] 和 [FrameTiming.rasterDuration]），或是否存在高延迟（通过 [FrameTiming.totalSpan]）。

与 [Timeline] 不同，此处的时间信息在发布模式下也可用（此外还包括 profile 和 debug 模式）。因此可用它来监控应用程序在实际使用中的性能。

{@macro dart.ui.TimingsCallback.list}

如果此值为 null，则不会执行额外的工作。如果此值不为 null，Flutter 每 1 秒花费不到 0.1ms 来报告时间信息（在 iPhone6S 上测得）。0.1ms 大约是 16ms（60fps 的帧预算）的 0.6%，或者说每秒约 0.01% 的 CPU 使用率。

### onReportTimings

```dart
set onReportTimings(TimingsCallback? callback)
```

### sendPlatformMessage()

```dart
void sendPlatformMessage(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

向特定平台的插件发送消息。

`name` 参数决定哪个插件接收该消息。`data` 参数包含消息负载，通常为 UTF-8 编码的 JSON，但也可以是任意数据。如果插件回复了该消息，将调用 `callback` 并传入响应内容。

框架在调用此方法时所处的相同 zone 中调用 [callback]。

### sendPortPlatformMessage()

```dart
void sendPortPlatformMessage(String name, ByteData? data, int identifier, SendPort port)
```

通过 [SendPort] 向特定平台的插件发送消息。

此操作与 [sendPlatformMessage] 类似，但用于从后台 isolate 发送消息。[port] 参数使 Flutter 能够知道应将结果发送到哪个 isolate。[name] 参数是通信所在通道的名称。[data] 参数是消息的负载。[identifier] 参数是分配给该消息的唯一整数。

### registerBackgroundIsolate()

```dart
void registerBackgroundIsolate(RootIsolateToken token)
```

将当前 isolate 注册到由 [token] 标识的 isolate。如果要在后台 isolate 上使用平台通道，则必须执行此操作。

### setSemanticsTreeEnabled()

```dart
void setSemanticsTreeEnabled(bool enabled)
```

通知引擎框架是否正在生成语义树。

只有框架知道何时应该生成语义树。它使用此方法通知引擎框架是否将生成语义树。

在平台希望启用语义功能的场景中（例如启用了辅助功能技术时），它会通过 [onSemanticsEnabledChanged] 通知框架。

将此值设置为 true 后，平台应准备好接受通过 [FlutterView.updateSemantics] 发送的语义更新。将此值设置为 false 时，平台可以释放与处理语义相关的任何资源，因为不会再通过 [FlutterView.updateSemantics] 发送进一步的语义更新。

在通过 [updateSemantics] 发送更新之前，必须先以 true 调用此方法。

### onPlatformMessage

```dart
PlatformMessageCallback? get onPlatformMessage
```

已弃用。请迁移到 [ChannelBuffers.setListener]。

每当此平台分发器收到来自特定平台插件的消息时调用。

`name` 参数决定发送该消息的插件。`data` 参数是消息负载，通常为 UTF-8 编码的 JSON，但也可以是任意数据。

消息处理程序必须调用 `callback` 参数中提供的函数。如果处理程序不需要响应，应向该回调传入 null。

框架在设置该回调时所处的相同 zone 中调用此回调。

### onPlatformMessage

```dart
set onPlatformMessage(PlatformMessageCallback? callback)
```

### setIsolateDebugName()

```dart
void setIsolateDebugName(String name)
```

设置与此平台分发器的根 isolate 关联的调试名称。

通常，调试名称是根据 Dart 端口、入口点和源文件自动生成的。例如：`main.dart$main-1234`。

可结合使用 flutter tools 的 `--isolate-filter` 标志来调试特定的根 isolate。例如：`flutter attach --isolate-filter=[name]`。请注意，这不会重命名该根 isolate 的任何子 isolate。

### requestDartPerformanceMode()

```dart
void requestDartPerformanceMode(DartPerformanceMode mode)
```

请求 Dart VM 根据请求的 `performance_mode` 调整 GC 启发式策略。

此操作在 Web 上为空操作（no-op）。引擎可能会忽略性能模式更改请求，或者不会以可预测的方式响应。

有关各性能模式的更多信息，请参阅 [DartPerformanceMode]。

### getPersistentIsolateData()

```dart
ByteData? getPersistentIsolateData()
```

嵌入器可以指定 isolate 在启动时可以同步请求的数据。此访问器用于获取该数据。

该数据在 Flutter 应用程序的整个生命周期内持续存在，即使在 isolate 重启后也可用。由于这种生命周期特性，此数据的大小必须保持最小。

对于嵌入器和 isolate 之间的异步通信，可以使用平台通道。

### scheduleFrame()

```dart
void scheduleFrame()
```

请求在下一个适当的时机调用 [onBeginFrame] 和 [onDrawFrame] 回调。

另请参阅：

- [SchedulerBinding]，Flutter 框架中管理帧调度的类。
- [scheduleWarmUpFrame]，该方法仅应用于调度预热帧。

### scheduleWarmUpFrame()

```dart
void scheduleWarmUpFrame({required VoidCallback beginFrame, required VoidCallback drawFrame})
```

尽快调度一帧运行，而不是等待引擎响应系统的“Vsync”信号来请求一帧。

应用程序可以在启动后立即调用此方法，以便第一帧（通常开销较大）能够提前几毫秒开始。在其他情况下使用它可能会导致意外结果，例如屏幕撕裂。根据平台和场景的不同，预热帧可能会也可能不会真正渲染到屏幕上。

有关预热帧的更多介绍，请参阅 [SchedulerBinding.scheduleWarmUpFrame]。

此方法使用提供的回调作为开始帧回调和绘制帧回调，而不是 [onBeginFrame] 和 [onDrawFrame]。

另请参阅：

- [SchedulerBinding.scheduleWarmUpFrame]，使用此方法并更详细地介绍了预热帧。
- [scheduleFrame]，在下一个适当的时机调度帧，应用于渲染常规帧。

### accessibilityFeatures

```dart
AccessibilityFeatures get accessibilityFeatures
```

平台可能启用的其他无障碍功能。

### onAccessibilityFeaturesChanged

```dart
VoidCallback? get onAccessibilityFeaturesChanged
```

当 [accessibilityFeatures] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

### onAccessibilityFeaturesChanged

```dart
set onAccessibilityFeaturesChanged(VoidCallback? callback)
```

### updateSemantics()

```dart
void updateSemantics(SemanticsUpdate update)
```

更改此平台分发器所保留的语义数据。

如果 [semanticsEnabled] 为 true，则表示用户已请求在此平台分发器的语义内容发生变化时调用此函数。

无论哪种情况，此函数都会释放给定的更新数据，这意味着该语义更新之后将无法再使用。

### locale

```dart
Locale get locale
```

设备的系统报告的默认语言区域。

它确定了应用程序应尽可能用于渲染其用户界面的语言和格式约定。

这是用户选择的第一个语言区域，是用户的主要语言区域（即设备 UI 显示所使用的语言区域）。

这等价于 `locales.first`，不同之处在于，如果 [locales] 列表尚未设置或为空，它将提供一个非 null 的“未定义”语言区域（使用语言标签 "und"）。

### setApplicationLocale()

```dart
void setApplicationLocale(Locale locale)
```

在引擎中设置应用程序的语言区域。

通常由框架调用，根据 Flutter 应用实际使用的语言区域进行设置。

### locales

```dart
List<Locale> get locales
```

设备完整的系统报告支持的语言区域列表。

它确定了应用程序应尽可能用于渲染其用户界面的语言和格式约定。

该列表按优先级排序，索引较小的语言区域优先于索引较大的语言区域。第一个元素是主要的 [locale]。

每当此值发生变化时，都会调用 [onLocaleChanged] 回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此值变化的机制。

### computePlatformResolvedLocale()

```dart
Locale? computePlatformResolvedLocale(List<Locale> supportedLocales)
```

执行平台原生的语言区域解析。

不同平台可能返回不同的结果。

如果平台无法解析语言区域，则此方法将返回 null。

此方法同步返回，是对特定平台 API 的直接调用，不涉及方法通道。

### onLocaleChanged

```dart
VoidCallback? get onLocaleChanged
```

每当 [locale] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此回调何时被调用的机制。

### onLocaleChanged

```dart
set onLocaleChanged(VoidCallback? callback)
```

### initialLifecycleState

```dart
String get initialLifecycleState
```

Dart isolate 初始化后立即生效的生命周期状态。

此属性不会随着生命周期的变化而更新。

它用于在启动时利用任何已缓冲的生命周期状态事件初始化 [SchedulerBinding.lifecycleState]。

### alwaysUse24HourFormat

```dart
bool get alwaysUse24HourFormat
```

指示时间是否应始终以 24 小时制显示的设置。

此选项由 [showTimePicker] 使用。

### lineHeightScaleFactorOverride

```dart
double? get lineHeightScaleFactorOverride
```

系统建议的文本高度，以字体大小的倍数表示。

此值优先于应用层指定的任何文本高度。例如，在框架层，[Text]、[SelectableText] 和 [EditableText] 组件的 [TextStyle] 中，此值会覆盖 [TextStyle.height] 和 [StrutStyle.height] 的现有值。

如果系统未设置覆盖值，则返回 null。

如果此值发生变化，将调用 [onMetricsChanged]。

### letterSpacingOverride

```dart
double? get letterSpacingOverride
```

系统建议的每个字母之间要添加的额外间距量（以逻辑像素为单位）。

可使用负值使字母间距更紧凑。

此值优先于应用层指定的任何文本字母间距。例如，在框架层，[Text]、[SelectableText] 和 [EditableText] 组件的 [TextStyle] 中，此值会覆盖 [TextStyle.letterSpacing] 的现有值。

如果系统未设置覆盖值，则返回 null。

如果此值发生变化，将调用 [onMetricsChanged]。

### wordSpacingOverride

```dart
double? get wordSpacingOverride
```

系统建议的每个空白序列（即每个单词）之间要添加的额外间距量（以逻辑像素为单位）。

可使用负值使单词间距更紧凑。

此值优先于应用层指定的任何文本单词间距。例如，在框架层，[Text]、[SelectableText] 和 [EditableText] 组件的 [TextStyle] 中，此值会覆盖 [TextStyle.wordSpacing] 的现有值。

如果系统未设置覆盖值，则返回 null。

如果此值发生变化，将调用 [onMetricsChanged]。

### paragraphSpacingOverride

```dart
double? get paragraphSpacingOverride
```

系统建议的文本中每个段落之后要添加的额外间距量（以逻辑像素为单位）。

此值优先于应用层指定的任何文本段落间距。

如果系统未设置覆盖值，则返回 null。

如果此值发生变化，将调用 [onMetricsChanged]。

### textScaleFactor

```dart
double get textScaleFactor
```

系统报告的文本缩放比例。

它根据用户的平台偏好设置确定渲染文本时使用的文本缩放系数。

每当此值发生变化时，都会调用 [onTextScaleFactorChanged] 回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此值变化的机制。

### onTextScaleFactorChanged

```dart
VoidCallback? get onTextScaleFactorChanged
```

每当 [textScaleFactor] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此回调何时被调用的机制。

### onTextScaleFactorChanged

```dart
set onTextScaleFactorChanged(VoidCallback? callback)
```

### nativeSpellCheckServiceDefined

```dart
bool get nativeSpellCheckServiceDefined
```

当前平台是否支持拼写检查服务。

当请求默认拼写检查服务时，[EditableTextState] 使用此选项来定义其 [SpellCheckConfiguration]。

### supportsShowingSystemContextMenu

```dart
bool get supportsShowingSystemContextMenu
```

当前平台是否支持显示系统上下文菜单。

[AdaptiveTextSelectionToolbar] 使用此选项来决定是显示系统上下文菜单，还是回退到默认的 Flutter 上下文菜单。

### brieflyShowPassword

```dart
bool get brieflyShowPassword
```

系统设置中是否已启用在模糊文本字段中输入时短暂显示字符的功能。

另请参阅：

- [EditableText.obscureText]，设置为 true 时会隐藏文本字段中的文本。

### platformBrightness

```dart
Brightness get platformBrightness
```

表示宿主平台当前亮度模式的设置。如果平台没有偏好设置，[platformBrightness] 默认为 [Brightness.light]。

### onPlatformBrightnessChanged

```dart
VoidCallback? get onPlatformBrightnessChanged
```

每当 [platformBrightness] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此回调何时被调用的机制。

### onPlatformBrightnessChanged

```dart
set onPlatformBrightnessChanged(VoidCallback? callback)
```

### systemFontFamily

```dart
String? get systemFontFamily
```

表示宿主平台当前系统字体的设置。

### onSystemFontFamilyChanged

```dart
VoidCallback? get onSystemFontFamilyChanged
```

每当 [systemFontFamily] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver]，一种在 widgets 层观察此回调何时被调用的机制。

### onSystemFontFamilyChanged

```dart
set onSystemFontFamilyChanged(VoidCallback? callback)
```

### semanticsEnabled

```dart
bool get semanticsEnabled
```

用户是否已请求在视图的语义内容发生变化时调用 updateSemantics。

每当此值发生变化时，都会调用 [onSemanticsEnabledChanged] 回调。

### onSemanticsEnabledChanged

```dart
VoidCallback? get onSemanticsEnabledChanged
```

当 [semanticsEnabled] 的值发生变化时调用的回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

### onSemanticsEnabledChanged

```dart
set onSemanticsEnabledChanged(VoidCallback? callback)
```

### onSemanticsActionEvent

```dart
SemanticsActionEventCallback? get onSemanticsActionEvent
```

每当用户请求对某个语义节点执行操作时调用的回调。

当用户根据 updateSemantics 提供的语义节点表达他们希望执行的操作时，使用此回调。

框架在设置该回调时所处的相同 zone 中调用此回调。

### onSemanticsActionEvent

```dart
set onSemanticsActionEvent(SemanticsActionEventCallback? callback)
```

### onHitTest

```dart
HitTestCallback? get onHitTest
```

当平台希望对某个 [FlutterView] 进行命中测试时调用的回调。

例如，iOS 使用此功能来判断某个手势是否命中了 [UIKitView]。

### onHitTest

```dart
set onHitTest(HitTestCallback? callback)
```

### frameData

```dart
FrameData get frameData
```

当前帧的 [FrameData] 对象。

### onFrameDataChanged

```dart
VoidCallback? get onFrameDataChanged
```

当窗口更新 [FrameData] 时调用的回调。

### onFrameDataChanged

```dart
set onFrameDataChanged(VoidCallback? callback)
```

### onError

```dart
ErrorCallback? get onError
```

当根 isolate 中发生未处理的错误时调用的回调。

如果此回调已处理该错误，则必须返回 `true`。否则，必须返回 `false`，此时将使用后备机制（例如打印到 stderr），具体取决于特定平台嵌入器通过 `Settings::unhandled_exception_callback` 所做的配置。

调用此回调后，VM 或进程可能会退出或变得无响应。对于在此回调被调用之前就导致 VM 或进程终止或变得无响应的异常，该回调将不会被调用。

此回调不会由根 isolate 的子 isolate 中的错误直接触发。创建新 isolate 的程序必须监听这些 isolate 上的错误并将其转发给根 isolate。

### onError

```dart
set onError(ErrorCallback? callback)
```

### defaultRouteName

```dart
String get defaultRouteName
```

应用程序启动时嵌入器所请求的路由或路径。

如果没有请求特定的路由，该值将为字符串 "`/`"。

## Android

在 Android 上，调用 [`FlutterView.setInitialRoute`](/javadoc/io/flutter/view/FlutterView.html#setInitialRoute-java.lang.String-) 将设置此值。该值必须足够早地设置，即在 Dart 中执行 [runApp] 调用之前，此设置才会对框架产生任何影响。在你的 `FlutterActivity` 子类中，`createFlutterView` 方法是设置该值的合适时机。应用程序的 `AndroidManifest.xml` 文件也必须相应更新，添加合适的 [`<intent-filter>`](https://developer.android.com/guide/topics/manifest/intent-filter-element.html)。

## iOS

在 iOS 上，调用 [`FlutterViewController.setInitialRoute`](/ios-embedder/interface_flutter_view_controller.html#a7f269c2da73312f856d42611cc12a33f) 将设置此值。该值必须足够早地设置，即在 Dart 中执行 [runApp] 调用之前，此设置才会对框架产生任何影响。`application:didFinishLaunchingWithOptions:` 方法是设置此值的合适时机。

另请参阅：

- [Navigator]，处理路由的组件。
- [SystemChannels.navigation]，处理来自嵌入器的后续导航请求。

### scaleFontSize()

```dart
double scaleFontSize(double unscaledFontSize)
```

根据用户的平台偏好设置，根据给定的 `unscaledFontSize` 计算缩放后的字体大小。

许多平台允许用户全局缩放文本以提高可读性。给定应用开发者以逻辑像素指定的字体大小，此方法将其转换为考虑了平台范围文本缩放的首选字体大小（同样以逻辑像素表示）。返回值始终为非负数。

如果用户更改了文本缩放偏好设置（例如在系统设置中），相同字体大小输入的缩放值可能会发生变化。可以使用 [onTextScaleFactorChanged] 回调来监控此类变化。

应用程序通常应使用 [MediaQuery.textScalerOf] 在组件树中获取缩放后的字体大小，而不是直接调用此方法，这样当文本缩放偏好设置发生变化时，应用中的文本会正确调整大小。

# SystemColor

```dart
final class SystemColor {}
```

操作系统 UI 调色板中指定的颜色。

目前，系统颜色仅在 Web 上受支持。要检查当前平台是否支持系统颜色，请使用静态字段 [platformProvidesSystemColors]。如果该字段为 `false`，此类中的其他函数将抛出 [UnsupportedError]。

此类通常与 [AccessibilityFeatures.highContrast] 结合使用。具体来说，在 Windows 上，当用户启用高对比度模式时，他们可能还会选择应用程序用户界面应使用的特定颜色。虽然应用程序通常使用自定义配色方案和设计语言很常见，但在高对比度模式下，建议组件使用系统指定的颜色，以使内容对用户更清晰易读。

“浅色”系统颜色可通过 [SystemColor.light] 获取，“深色”系统颜色可通过 [SystemColor.dark] 获取。

示例：

```dart
import 'dart:ui';

Color getSystemAccentColor() {
  Color? systemAccentColor;
  if (SystemColor.platformProvidesSystemColors) {
    if (PlatformDispatcher.instance.platformBrightness == Brightness.light) {
      systemAccentColor = SystemColor.light.accentColor.value;
    } else {
      systemAccentColor = SystemColor.dark.accentColor.value;
    }
  }

  return systemAccentColor ?? const Color(0xFF007AFF);
}
```

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors
- https://developer.mozilla.org/en-US/docs/Web/CSS/system-color
- https://developer.mozilla.org/en-US/docs/Web/CSS/@media/forced-colors

### SystemColor()

```dart
SystemColor({required String name, Color? value})
```

创建系统颜色的实例。

[name] 是颜色的名称。由 [SystemColorPalette] 提供的系统颜色（例如 [SystemColorPalette.accentColor] 和 [SystemColorPalette.buttonText]）使用 [W3C CSS 规范](https://drafts.csswg.org/css-color/#css-system-colors) 中定义的标准名称。

[value] 是该颜色的值（如果支持此颜色名称），若不支持则为 null。

### name

```dart
String name
```

标准系统颜色名称，由 W3C CSS 规范定义。

Flutter 中的系统颜色名称是大小写敏感的。这是为了使颜色名称可以方便地用作 [Map] 的键。这与 CSS 不同，在 CSS 中系统颜色名称不区分大小写。也就是说，指定 `background-color: aCcEnTcOlOr` 等价于指定 `background-color: AccentColor`。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### value

```dart
Color? value
```

名为 [name] 的颜色所使用的颜色值（如果支持）。

如果 [isSupported] 为 false，则 [value] 为 null。如果 [isSupported] 为 true，则 [value] 不为 null。

### isSupported

```dart
bool get isSupported
```

如果当前平台提供了具有给定 [name] 的系统颜色，则返回 true。

另请参阅：

- [platformProvidesSystemColors]，返回当前平台是否提供系统颜色。

### platformProvidesSystemColors

```dart
bool get platformProvidesSystemColors
```

如果当前平台提供系统颜色，则返回 true。

目前，系统颜色仅在 Web 上受支持。

另请参阅：

- [isSupported]，返回是否支持特定颜色。

### light

```dart
SystemColorPalette light
```

浅色模式的系统调色板。

### dark

```dart
SystemColorPalette dark
```

深色模式的系统调色板。

# SystemColorPalette

```dart
final class SystemColorPalette {}
```

操作系统中为给定 [brightness] 指定的系统颜色调色板。

此类中的获取器，例如 [accentColor] 和 [buttonText]，提供了 [W3C CSS 规范](https://drafts.csswg.org/css-color/#css-system-colors) 定义的标准系统颜色。

### brightness

```dart
Brightness brightness
```

定义此调色板的亮度模式。

### accentColor

```dart
SystemColor get accentColor
```

返回名为 "AccentColor" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### accentColorText

```dart
SystemColor get accentColorText
```

返回名为 "AccentColorText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### activeText

```dart
SystemColor get activeText
```

返回名为 "ActiveText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonBorder

```dart
SystemColor get buttonBorder
```

返回名为 "ButtonBorder" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonFace

```dart
SystemColor get buttonFace
```

返回名为 "ButtonFace" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonText

```dart
SystemColor get buttonText
```

返回名为 "ButtonText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### canvas

```dart
SystemColor get canvas
```

返回名为 "Canvas" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### canvasText

```dart
SystemColor get canvasText
```

返回名为 "CanvasText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### field

```dart
SystemColor get field
```

返回名为 "Field" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### fieldText

```dart
SystemColor get fieldText
```

返回名为 "FieldText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### grayText

```dart
SystemColor get grayText
```

返回名为 "GrayText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### highlight

```dart
SystemColor get highlight
```

返回名为 "Highlight" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### highlightText

```dart
SystemColor get highlightText
```

返回名为 "HighlightText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### linkText

```dart
SystemColor get linkText
```

返回名为 "LinkText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### mark

```dart
SystemColor get mark
```

返回名为 "Mark" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### markText

```dart
SystemColor get markText
```

返回名为 "MarkText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### selectedItem

```dart
SystemColor get selectedItem
```

返回名为 "SelectedItem" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### selectedItemText

```dart
SystemColor get selectedItemText
```

返回名为 "SelectedItemText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

### visitedText

```dart
SystemColor get visitedText
```

返回名为 "VisitedText" 的系统颜色。

另请参阅：

- https://drafts.csswg.org/css-color/#css-system-colors

# FramePhase

```dart
enum FramePhase {}
```

帧生命周期中的各个重要时间点。

[FrameTiming] 记录每个阶段的时间戳，用于性能分析。

操作系统给出的 vsync 信号的时间戳。

另请参阅 [FrameTiming.vsyncOverhead]。

UI 线程开始构建一帧的时间点。

另请参阅 [FrameTiming.buildDuration]。

UI 线程完成一帧构建的时间点。

另请参阅 [FrameTiming.buildDuration]。

光栅线程开始光栅化一帧的时间点。

另请参阅 [FrameTiming.rasterDuration]。

光栅线程完成一帧光栅化的时间点。

另请参阅 [FrameTiming.rasterDuration]。

光栅线程以墙钟时间完成一帧光栅化的时间点。

这对于将光栅完成时间与系统时钟相关联、与其他性能分析工具集成非常有用。

# FrameTiming

```dart
class FrameTiming {}
```

一帧的时间相关性能指标。

如果你使用完整的 Flutter 框架，请使用 [SchedulerBinding.addTimingsCallback] 来获取此对象。相比直接使用 [PlatformDispatcher.onReportTimings]，更推荐使用它，因为 [SchedulerBinding.addTimingsCallback] 允许注册多个回调。如果 [SchedulerBinding] 不可用，请参阅 [PlatformDispatcher.onReportTimings] 了解如何获取此对象。

调试模式（不带任何标志运行 `flutter run`）下的指标可能与 profile 和 release 模式下的指标有很大差异，这是由于调试开销所致。因此建议仅在 profile 和 release 模式下监控和分析性能指标。

### FrameTiming()

```dart
FrameTiming({required int vsyncStart, required int buildStart, required int buildFinish, required int rasterStart, required int rasterFinish, required int rasterFinishWallTime, int layerCacheCount = 0, int layerCacheBytes = 0, int pictureCacheCount = 0, int pictureCacheBytes = 0, int frameNumber = -1})
```

使用微秒为单位的原始时间戳构造 [FrameTiming]。

此构造函数仅用于单元测试。真实的 [FrameTiming] 应从 [PlatformDispatcher.onReportTimings] 获取。

如果未提供 [frameNumber]，则默认为 `-1`。

### timestampInMicroseconds()

```dart
int timestampInMicroseconds(FramePhase phase)
```

这是自某个纪元以来以微秒为单位的原始时间戳。所有 [FrameTiming] 中的纪元都相同，但可能与 [DateTime] 的纪元不一致。

### buildDuration

```dart
Duration get buildDuration
```

在 UI 线程上构建该帧所用的时长。

构建大约在调用 [PlatformDispatcher.onBeginFrame] 时开始。[PlatformDispatcher.onBeginFrame] 回调中的 [Duration] 恰好等于 `Duration(microseconds: timestampInMicroseconds(FramePhase.buildStart))`。

构建在调用 [FlutterView.render] 时完成。

{@template dart.ui.FrameTiming.fps_smoothness_milliseconds} 为确保 X fps 的流畅动画，此值不应超过 1000/X 毫秒。{@endtemplate} {@template dart.ui.FrameTiming.fps_milliseconds} 对于 60fps 大约是 16ms，对于 120fps 大约是 8ms。{@endtemplate}

### rasterDuration

```dart
Duration get rasterDuration
```

在光栅线程上光栅化该帧所用的时长。

{@macro dart.ui.FrameTiming.fps_smoothness_milliseconds} {@macro dart.ui.FrameTiming.fps_milliseconds}

### vsyncOverhead

```dart
Duration get vsyncOverhead
```

从收到 vsync 信号到开始构建该帧之间的时长。

### totalSpan

```dart
Duration get totalSpan
```

从 vsync 开始到光栅完成之间的时间跨度。

为在 X fps 的显示器上实现最低延迟，此值不应超过 1000/X 毫秒。{@macro dart.ui.FrameTiming.fps_milliseconds}

另请参阅 [vsyncOverhead]、[buildDuration] 和 [rasterDuration]。

### layerCacheCount

```dart
int get layerCacheCount
```

该帧期间存储在光栅缓存中的图层数量。

另请参阅 [layerCacheBytes]、[pictureCacheCount] 和 [pictureCacheBytes]。

### layerCacheBytes

```dart
int get layerCacheBytes
```

该帧期间用于缓存图层的图像数据字节数。

另请参阅 [layerCacheCount]、[layerCacheMegabytes]、[pictureCacheCount] 和 [pictureCacheBytes]。

### layerCacheMegabytes

```dart
double get layerCacheMegabytes
```

该帧期间用于缓存图层的图像数据兆字节数。

另请参阅 [layerCacheCount]、[layerCacheBytes]、[pictureCacheCount] 和 [pictureCacheBytes]。

### pictureCacheCount

```dart
int get pictureCacheCount
```

该帧期间存储在光栅缓存中的图片（picture）数量。

另请参阅 [layerCacheCount]、[layerCacheBytes] 和 [pictureCacheBytes]。

### pictureCacheBytes

```dart
int get pictureCacheBytes
```

该帧期间用于缓存图片的图像数据字节数。

另请参阅 [layerCacheCount]、[layerCacheBytes]、[pictureCacheCount] 和 [pictureCacheMegabytes]。

### pictureCacheMegabytes

```dart
double get pictureCacheMegabytes
```

该帧期间用于缓存图片的图像数据兆字节数。

另请参阅 [layerCacheCount]、[layerCacheBytes]、[pictureCacheCount] 和 [pictureCacheBytes]。

### frameNumber

```dart
int get frameNumber
```

与此帧测量相关联的帧键。

### toString()

```dart
String toString()
```

# AppLifecycleState

```dart
enum AppLifecycleState {}
```

应用程序在运行期间可能处于的状态。

平台不支持的状态将由框架在受支持的状态之间转换时合成，以便所有实现共享相同的状态机。

该状态的初始值为 [detached] 状态，一旦从平台收到第一个生命周期更新（通常是 [resumed]），就会更新为当前状态。

由于历史原因和名称冲突，Flutter 的应用状态名称与所有平台上的状态名称并非一一对应。例如在 Android 上，当操作系统调用 [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>) 时，Flutter 将进入 [inactive] 状态，但当 Android 调用 [`Activity.onStop`](<https://developer.android.com/reference/android/app/Activity#onStop()>) 时，Flutter 将进入 [paused] 状态。有关每个状态在各平台上含义的说明，请参阅各个状态的相关文档。

当前的应用状态可以从 [SchedulerBinding.instance.lifecycleState] 获取，可以通过创建 [AppLifecycleListener]，或者通过重写 [WidgetsBindingObserver.didChangeAppLifecycleState] 方法使用 [WidgetsBindingObserver] 来观察状态的变化。

应用程序不应依赖于总是能收到所有可能的通知。

例如，如果应用程序被任务管理器杀死、被 kill 信号终止、用户直接拔掉设备电源，或者设备发生了突发性物理损坏，在应用程序被突然终止之前不会发送任何通知，并且可能会跳过某些状态。

另请参阅：

- [AppLifecycleListener]，一个用于观察生命周期状态并提供状态转换回调的对象。
- [WidgetsBindingObserver]，一种在 widgets 层观察生命周期状态的机制。
- iOS 的 [UIKit 活动生命周期](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle?language=objc) 文档。
- Android 的[活动生命周期](https://developer.android.com/guide/components/activities/activity-lifecycle)文档。
- macOS 的 [AppKit 活动生命周期](https://developer.apple.com/documentation/appkit/nsapplicationdelegate?language=objc) 文档。

应用程序仍由 Flutter 引擎托管，但与任何宿主视图分离。

应用程序在初始化之前默认处于此状态，并且（适用于 Android、iOS 和 Web）在所有视图都已分离后可能处于此状态。

当应用程序处于此状态时，引擎在没有视图的情况下运行。

此状态仅在 iOS、Android 和 Web 上进入，尽管在所有平台上它都是应用程序开始运行之前的默认状态。

在所有平台上，此状态表示应用程序处于默认的运行模式，拥有输入焦点并且可见。

在 Android 上，此状态对应于 Flutter 宿主视图在 Android 处于“resumed”状态时拥有焦点（调用了 [`Activity.onWindowFocusChanged`](<https://developer.android.com/reference/android/app/Activity#onWindowFocusChanged(boolean)>) 且参数为 true）。如果应用失去焦点（调用了 [`Activity.onWindowFocusChanged`](<https://developer.android.com/reference/android/app/Activity#onWindowFocusChanged(boolean)>) 且参数为 false），但尚未调用 [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>)，则 Flutter 应用可能处于 [inactive] 状态，即使仍处于 Android 的["onResume"](https://developer.android.com/guide/components/activities/activity-lifecycle) 状态。

在 iOS 和 macOS 上，这对应于应用在前台活动状态下运行。

应用程序至少有一个视图可见，但没有任何视图拥有输入焦点。应用程序在其他方面正常运行。

在非 Web 桌面平台上，这对应于一个不在前台但仍有可见窗口的应用程序。

在 Web 上，这对应于运行在没有输入焦点的窗口或标签页中的应用程序。

在 iOS 和 macOS 上，此状态对应于 Flutter 宿主视图在前台非活动状态下运行。当应用处于电话通话中、响应 TouchID 请求、进入应用切换器或控制中心，或者托管 Flutter 应用的 UIViewController 正在过渡时，应用会转换到此状态。

在 Android 上，这对应于 Flutter 宿主视图处于 Android 的暂停状态（即已调用 [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>)），或处于 Android 的“resumed”状态（即已调用 [`Activity.onResume`](<https://developer.android.com/reference/android/app/Activity#onResume()>)）但没有窗口焦点。应用转换到此状态的例子包括：应用被部分遮挡或另一个 activity 获得焦点、在分屏中运行但不是当前应用、被电话呼叫打断的应用、画中画应用、系统对话框、另一个视图。当通知栏下拉或应用切换器可见时，应用也会处于非活动状态。

在 Android 和 iOS 上，处于此状态的应用应假定它们随时可能被 [hidden] 和 [paused]。

应用程序的所有视图都已隐藏，可能是因为应用程序即将暂停（在 iOS 和 Android 上），或者因为它已被最小化或放置在不再可见的桌面上（在非 Web 桌面上），或者运行在不再可见的窗口或标签页中（在 Web 上）。

在 iOS 和 Android 上，为了在所有平台上保持相同的状态机，在从 [inactive] 进入 [paused] 状态之前，会先合成一次转换到此状态；同样，在从 [paused] 进入 [inactive] 状态之前也是如此。这使得希望知道应用何时在概念上“隐藏”的跨平台实现只需编写一个处理程序即可。

应用程序当前对用户不可见，且不响应用户输入。

当应用程序处于此状态时，引擎不会调用 [PlatformDispatcher.onBeginFrame] 和 [PlatformDispatcher.onDrawFrame] 回调。

此状态仅在 iOS 和 Android 上进入。

# AppExitResponse

```dart
enum AppExitResponse {}
```

对退出应用程序请求的可能响应。

该请求通常通过创建 [AppLifecycleListener] 并提供 [AppLifecycleListener.onExitRequested] 回调来响应，或者通过重写 [WidgetsBindingObserver.didRequestAppExit] 来响应。

可以继续退出应用程序。

取消退出：不退出应用程序。

# AppExitType

```dart
enum AppExitType {}
```

调用 [ServicesBinding.exitApplication] 时要执行的应用程序退出类型。

请求应用程序开始有序退出，通过 [WidgetsBinding] 将请求发送回框架。如果框架响应 [AppExitResponse.exit]，则按照与 [required] 退出相同的步骤继续。如果框架响应 [AppExitResponse.cancel]，则取消退出请求，应用程序继续正常执行。

不可取消的有序退出请求。引擎将关闭引擎并调用原生 UI 工具包的退出 API。

如果你需要更快、更危险的退出方式，可以直接调用 `dart:io` 的 `exit()`，这样甚至不会调用原生工具包的退出 API。不过这相当危险，因为引擎可能会因未被正确关闭而崩溃，导致应用在退出时崩溃。

# ViewPadding

```dart
class ViewPadding {}
```

表示矩形四条边各自距离的类，用于编码应用程序应在其用户界面周围放置的视图内边距（view insets）和内边距（padding），分别由 [FlutterView.viewInsets] 和 [FlutterView.padding] 暴露。视图内边距（insets）和内边距（padding）最好通过 [MediaQuery.of] 读取。

有关表示矩形周围距离的通用类，请参阅 [EdgeInsets] 类。

另请参阅：

- [WidgetsBindingObserver]，在 widgets 层接收内边距变化通知的机制。
- [MediaQuery.of]，访问这些值的首选机制。
- [Scaffold]，在 material design 应用程序中自动应用内边距。

### left

```dart
double left
```

从左边缘到第一个未被遮挡像素的距离，以物理像素为单位。

### top

```dart
double top
```

从上边缘到第一个未被遮挡像素的距离，以物理像素为单位。

### right

```dart
double right
```

从右边缘到第一个未被遮挡像素的距离，以物理像素为单位。

### bottom

```dart
double bottom
```

从下边缘到第一个未被遮挡像素的距离，以物理像素为单位。

### zero

```dart
ViewPadding zero
```

每条边的值均为零的视图内边距。

### toString()

```dart
String toString()
```

# WindowPadding

```dart
typedef WindowPadding = ViewPadding
```

已弃用。将在 Flutter 未来版本中移除。

请使用 [ViewPadding] 代替。

# ViewConstraints

```dart
class ViewConstraints {}
```

[FlutterView] 的不可变布局约束。

与 [BoxConstraints] 类似，当且仅当以下所有关系均成立时，[Size] 才满足 [ViewConstraints]：

- [minWidth] <= [Size.width] <= [maxWidth]
- [minHeight] <= [Size.height] <= [maxHeight]

约束本身必须满足以下关系：

- 0.0 <= [minWidth] <= [maxWidth] <= [double.infinity]
- 0.0 <= [minHeight] <= [maxHeight] <= [double.infinity]

对于每个约束，[double.infinity] 都是合法值。

有关表示此类约束的通用类，请参阅 [BoxConstraints] 类。

### ViewConstraints()

```dart
ViewConstraints({double minWidth = 0.0, double maxWidth = double.infinity, double minHeight = 0.0, double maxHeight = double.infinity})
```

使用给定约束创建视图约束。

### ViewConstraints.tight()

```dart
ViewConstraints.tight(Size size)
```

创建仅被给定尺寸满足的视图约束。

### minWidth

```dart
double minWidth
```

满足约束的最小宽度。

### maxWidth

```dart
double maxWidth
```

满足约束的最大宽度。

可能为 [double.infinity]。

### minHeight

```dart
double minHeight
```

满足约束的最小高度。

### maxHeight

```dart
double maxHeight
```

满足约束的最大高度。

可能为 [double.infinity]。

### isSatisfiedBy()

```dart
bool isSatisfiedBy(Size size)
```

给定尺寸是否满足此约束。

### isTight

```dart
bool get isTight
```

是否只有一个尺寸满足此约束。

### operator /()

```dart
ViewConstraints operator /(double factor)
```

将每个约束参数按给定因子的倒数进行缩放。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# DisplayFeature

```dart
class DisplayFeature {}
```

显示器上可能被硬件特征遮挡的区域。

此项仅在 Android 上填充。

[bounds] 以逻辑像素为单位度量。在具有两块屏幕的设备上，坐标系以左侧或顶部屏幕的左上角为 (0,0)，并扩展以包括两块屏幕及其间的视觉空间。

[type] 描述了 [DisplayFeature] 的行为，以及它是否会遮挡显示。例如，[DisplayFeatureType.hinge] 和 [DisplayFeatureType.cutout] 都会遮挡显示，而 [DisplayFeatureType.fold] 则不会。

![带铰链显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_hinge.png)

![带折叠显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_fold.png)

![带凹口显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_cutout.png)

[state] 包含可折叠特征（[DisplayFeatureType.hinge] 和 [DisplayFeatureType.fold]）的姿态信息。姿态是显示屏的形状，例如 [DisplayFeatureState.postureFlat] 或 [DisplayFeatureState.postureHalfOpened]。对于 [DisplayFeatureType.cutout]，不使用 state，其值为 [DisplayFeatureState.unknown]。

### DisplayFeature()

```dart
DisplayFeature({required Rect bounds, required DisplayFeatureType type, required DisplayFeatureState state})
```

### bounds

```dart
Rect bounds
```

Flutter 视图中被此显示特征占据的区域，以逻辑像素为单位度量。

在具有两块屏幕的设备上，Flutter 视图从左侧或顶部屏幕的左上角延伸到右侧或底部屏幕的右下角，包括任何显示特征所占据的视觉区域。显示特征的边界即按此坐标系报告。

例如，在竖屏模式的双屏设备上：

- [Rect.left] 给出左侧屏幕的尺寸（以逻辑像素为单位）。
- [Rect.right] 给出左侧屏幕的尺寸加上铰链宽度。

### type

```dart
DisplayFeatureType type
```

显示特征的类型，例如铰链、折叠、凹口。

### state

```dart
DisplayFeatureState state
```

显示特征的姿态，仅在折叠和铰链情况下填充。

对于凹口，此值为 [DisplayFeatureState.unknown]

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# DisplayFeatureType

```dart
enum DisplayFeatureType {}
```

[DisplayFeature] 的类型，描述了 [DisplayFeature] 的行为以及它是否会遮挡显示。

某些类型的 [DisplayFeature]，例如 [DisplayFeatureType.fold]，可以在不实际影响屏幕绘制的情况下被报告。它们对于了解显示屏的弯曲或折痕位置很有用。在这种情况下，[DisplayFeature.bounds] 的宽度可以为 0。

[DisplayFeatureType.fold] 和 [DisplayFeatureType.hinge] 类型的屏幕所形成的形状称为姿态（posture），并通过 [DisplayFeature.state] 暴露。例如，[DisplayFeatureState.postureFlat] 姿态表示屏幕形成了一个平面。

![带铰链显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_hinge.png)

![带折叠显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_fold.png)

![带凹口显示特征的设备](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_cutout.png)

[DisplayFeature] 类型是新出现的，Flutter 尚不识别。

柔性屏幕上没有物理间隙的折叠。

此显示特征类型的边界表示显示屏产生折痕的位置。

具有铰链的物理分隔，允许两个显示面板折叠。

屏幕上不显示内容的区域，通常用于放置摄像头或传感器。

# DisplayFeatureState

```dart
enum DisplayFeatureState {}
```

显示特征的状态，包含可折叠特征姿态的相关信息。

姿态是柔性屏幕各部分或物理屏幕面板所形成的形状。它们的灵感来源于并类似于 [Android 姿态](https://developer.android.com/guide/topics/ui/foldables#postures)。

- 对于 [DisplayFeatureType.fold] 和 [DisplayFeatureType.hinge]，该状态即为姿态。
- 对于 [DisplayFeatureType.cutout]，不使用该状态，其值为 [DisplayFeatureState.unknown]。

该显示特征为 [DisplayFeatureType.cutout]，或此状态是新出现的，Flutter 尚不识别。

可折叠设备完全展开。

呈现给用户的屏幕空间是平坦的。

折叠角度处于展开和闭合状态之间的中间位置。

柔性屏幕各部分之间或物理屏幕面板之间存在非平坦角度，使得屏幕开始彼此面对。

# DisplayCornerRadii

```dart
class DisplayCornerRadii {}
```

显示器四个角的圆角半径集合。

此类表示显示器圆角的曲率。半径值以物理像素定义。

如果某个角是直角（未圆化），则其半径为 0.0。

目前仅在 Android API 31+ 上填充。

### DisplayCornerRadii()

```dart
DisplayCornerRadii({required double topLeft, required double topRight, required double bottomRight, required double bottomLeft})
```

创建一个 [DisplayCornerRadii]。

### topLeft

```dart
double topLeft
```

显示器左上角的半径，以物理像素为单位。

### topRight

```dart
double topRight
```

显示器右上角的半径，以物理像素为单位。

### bottomRight

```dart
double bottomRight
```

显示器右下角的半径，以物理像素为单位。

### bottomLeft

```dart
double bottomLeft
```

显示器左下角的半径，以物理像素为单位。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# Locale

```dart
class Locale {}
```

用于选择用户语言和格式偏好设置的标识符。

它表示一个 [Unicode 语言标识符](https://www.unicode.org/reports/tr35/#Unicode_language_identifier)（即不含 Locale 扩展），但不支持变体（variant）。

语言区域根据 [IANA 语言子标签注册表](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) 中的“首选值”条目进行规范化。例如，`const Locale('he')` 和 `const Locale('iw')` 是相等的，且它们的 [languageCode] 都是 `he`，因为 `iw` 是一个已弃用的语言子标签，已被子标签 `he` 取代。

另请参阅：

- [PlatformDispatcher.locale]，指定系统当前选择的 [Locale]。

### Locale()

```dart
Locale(String _languageCode, [String? _countryCode])
```

创建一个新的 Locale 对象。第一个参数是主要语言子标签，第二个参数是地区（也称为“国家”）子标签。

例如：

```dart
const Locale swissFrench = Locale('fr', 'CH');
const Locale canadianFrench = Locale('fr', 'CA');
```

主要语言子标签不能为 null。地区子标签是可选的。当没有地区/国家子标签时，该参数应省略，或传入 `null` 而不是空字符串。

子标签值是**大小写敏感**的，且必须是根据 CLDR 补充数据校验有效的子标签：[language](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml)、[region](https://github.com/unicode-org/cldr/blob/master/common/validity/region.xml)。主要语言子标签必须是至少两个、最多八个小写字母，但不能是四个字母。地区子标签必须是两个大写字母或三个数字。请参阅 [Unicode 语言标识符](https://www.unicode.org/reports/tr35/#Unicode_language_identifier)规范。

默认情况下不会检查有效性，但某些方法可能会丢弃无效数据。

另请参阅：

- [Locale.fromSubtags]，也允许指定 [scriptCode]。

### Locale.fromSubtags()

```dart
Locale.fromSubtags({String languageCode = 'und', String? scriptCode, String? countryCode})
```

创建一个新的 Locale 对象。

关键字参数指定 Locale 的子标签。

子标签值是**大小写敏感**的，且必须是根据 CLDR 补充数据校验有效的子标签，分别对应 languageCode、scriptCode 和 countryCode 的 [language](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml)、[script](https://github.com/unicode-org/cldr/blob/master/common/validity/script.xml) 和 [region](https://github.com/unicode-org/cldr/blob/master/common/validity/region.xml)。

[languageCode] 子标签是可选的。当没有语言子标签时，该参数应省略或设置为 "und"。如果未提供，[languageCode] 默认为 "und"，即未定义的语言代码。

[countryCode] 子标签是可选的。当没有国家子标签时，该参数应省略，或传入 `null` 而不是空字符串。

默认情况下不会检查有效性，但某些方法可能会丢弃无效数据。

### languageCode

```dart
String get languageCode
```

语言区域的主要语言子标签。

此值不能为 null。它可以是 'und'，表示“未定义”。

此值应为在 [IANA 语言子标签注册表](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) 中类型为 "language" 的已注册字符串。指定的字符串必须与注册表中字符串的大小写一致。

已在注册表中弃用且有首选代码的语言子标签会被更改为其首选代码。例如，`const Locale('he')` 和 `const Locale('iw')` 是相等的，且它们的 [languageCode] 都是 `he`，因为 `iw` 是一个已弃用的语言子标签，已被子标签 `he` 取代。

此值必须是 [Unicode CLDR 补充数据](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml) 中列出的有效 Unicode 语言子标签。

另请参阅：

- [Locale.fromSubtags]，描述了创建 [Locale] 对象的约定。

### scriptCode

```dart
String? scriptCode
```

语言区域的文字（script）子标签。

此值可以为 null，表示未指定文字子标签。

此值必须是 [Unicode CLDR 补充数据](https://github.com/unicode-org/cldr/blob/master/common/validity/script.xml) 中列出的有效 Unicode 语言标识符文字子标签。

另请参阅：

- [Locale.fromSubtags]，描述了创建 [Locale] 对象的约定。

### countryCode

```dart
String? get countryCode
```

语言区域的地区子标签。

此值可以为 null，表示未指定地区子标签。

此值应为在 [IANA 语言子标签注册表](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) 中类型为 "region" 的已注册字符串。指定的字符串必须与注册表中字符串的大小写一致。

已在注册表中弃用且有首选代码的地区子标签会被更改为其首选代码。例如，`const Locale('de', 'DE')` 和 `const Locale('de', 'DD')` 是相等的，且它们的 [countryCode] 都是 `DE`，因为 `DD` 是一个已弃用的语言子标签，已被子标签 `DE` 取代。

另请参阅：

- [Locale.fromSubtags]，描述了创建 [Locale] 对象的约定。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

返回表示该语言区域的字符串。

这个标识符恰好是一个使用下划线作为分隔符的有效 Unicode 语言区域标识符，但仅用于调试目的。如需可解析的结果，请改用 [toLanguageTag]。

### toLanguageTag()

```dart
String toLanguageTag()
```

返回一个语法上有效的 Unicode BCP47 语言区域标识符。

此类标识符的一些示例："en"、"es-419"、"hi-Deva-IN" 和 "zh-Hans-CN"。有关技术细节，请参阅 http://www.unicode.org/reports/tr35/ 。

# DartPerformanceMode

```dart
enum DartPerformanceMode {}
```

用于调优 Dart VM 垃圾回收性能的各种性能模式。

编辑此枚举时，请保持顺序与 [dart_api.h](https://github.com/dart-lang/sdk/blob/main/runtime/include/dart_api.h#L1302) 中的 `Dart_PerformanceMode` 同步。

这是 Dart VM 的默认模式。

以更小的批次执行工作（需要更多开销）或延迟执行工作（需要更多内存）为代价，优化以实现低延迟，牺牲吞吐量和内存开销。嵌入器不应无限期地保持在此模式下。

以更大批次执行工作并伴随更多的间歇性内存增长为代价，优化以实现高吞吐量，牺牲延迟和内存开销。

以更频繁地执行工作为代价，优化以实现低内存占用，牺牲吞吐量和延迟。

# SemanticsActionEvent

```dart
class SemanticsActionEvent {}
```

请求对由 ID 为 [viewId] 的 [FlutterView] 所拥有、ID 为 [nodeId] 的 [SemanticsNode] 执行类型为 [type] 的 [SemanticsAction] 的事件。

由 [SemanticsBinding.performSemanticsAction] 使用。

### SemanticsActionEvent()

```dart
SemanticsActionEvent({required SemanticsAction type, required int viewId, required int nodeId, Object? arguments})
```

创建一个 [SemanticsActionEvent]。

### type

```dart
SemanticsAction type
```

要执行的操作类型。

### viewId

```dart
int viewId
```

与 ID 为 [nodeId] 的 [SemanticsNode] 关联的 [FlutterView] 的 ID。

### nodeId

```dart
int nodeId
```

要在其上执行操作的 [SemanticsNode] 的 ID。

### arguments

```dart
Object? arguments
```

该操作的可选参数。

### copyWith()

```dart
SemanticsActionEvent copyWith({SemanticsAction? type, int? viewId, int? nodeId, Object? arguments = _noArgumentPlaceholder})
```

创建 [SemanticsActionEvent] 的克隆，并替换所提供的参数。

# ViewFocusChangeCallback

```dart
typedef ViewFocusChangeCallback = void Function(ViewFocusEvent viewFocusEvent)
```

[PlatformDispatcher.onViewFocusChange] 的回调函数签名。

# ViewFocusEvent

```dart
final class ViewFocusEvent {}
```

用于引擎向应用传达视图焦点变化的事件。

此值通常会传递给 [PlatformDispatcher.onViewFocusChange] 回调。

### ViewFocusEvent()

```dart
ViewFocusEvent({required int viewId, required ViewFocusState state, required ViewFocusDirection direction})
```

创建一个 [ViewFocusChange]。

### viewId

```dart
int viewId
```

发生焦点变化的 [FlutterView] 的 ID。

### state

```dart
ViewFocusState state
```

焦点变化后的状态。

### direction

```dart
ViewFocusDirection direction
```

焦点变化的方向。

### toString()

```dart
String toString()
```

# ViewFocusState

```dart
enum ViewFocusState {}
```

表示给定 [FlutterView] 的焦点状态。

失去焦点时，视图的焦点状态变为 [ViewFocusState.unfocused]。

获得焦点时，视图的焦点状态变为 [ViewFocusState.focused]。

视图内有效的转换为：

- [ViewFocusState.focused] 到 [ViewFocusState.unfocused]。
- [ViewFocusState.unfocused] 到 [ViewFocusState.focused]。

另请参阅：

- [ViewFocusDirection]，指定焦点方向。
- [ViewFocusEvent]，传达 [FlutterView] 焦点变化的相关信息。

指定视图没有平台焦点。

指定视图拥有平台焦点。

# ViewFocusDirection

```dart
enum ViewFocusDirection {}
```

表示焦点在 [FlutterView] 之间转移的方向。

另请参阅：

- [ViewFocusState]，指定 [FlutterView] 的当前焦点状态。
- [ViewFocusEvent]，传达 [FlutterView] 焦点变化的相关信息。

表示焦点转移没有方向。

这通常与以编程方式请求焦点或焦点丢失相关联。

表示焦点转移是以前向方向执行的。

这通常是用户按下 Tab 键的结果。

表示焦点转移是以反向方向执行的。

这通常是用户按下 Shift + Tab 键的结果。

# HitTestRequest

```dart
class HitTestRequest {}
```

在特定位置评估视图内容的请求。

另请参阅：

- [PlatformDispatcher.onHitTest]，平台调用以在特定位置对视图进行命中测试的回调。
- [HitTestResponse]，命中测试请求的结果。

### HitTestRequest()

```dart
HitTestRequest({required FlutterView view, required Offset offset})
```

创建一个命中测试请求。

### view

```dart
FlutterView view
```

应进行命中测试的视图。

### offset

```dart
Offset offset
```

应在 [view] 中进行命中测试的位置。

# HitTestResponse

```dart
class HitTestResponse {}
```

在特定位置对视图进行命中测试的结果。

另请参阅：

- [PlatformDispatcher.onHitTest]，平台调用以在特定位置对视图进行命中测试的回调。
- [HitTestRequest]，在特定位置对视图进行命中测试的请求。

### HitTestResponse()

```dart
HitTestResponse({required bool hasPlatformView})
```

创建一个命中测试响应。

### empty

```dart
HitTestResponse empty
```

没有命中条目的响应。

### hasPlatformView

```dart
bool hasPlatformView
```

命中测试结果是否包含平台视图。

另请参阅：

- [NativeHitTestTarget]，表示由平台视图支持的命中测试目标的 Flutter 框架 mixin。
