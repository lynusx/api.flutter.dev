@docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'binding.dart'; @docImport 'ticker.dart';

# debugPrintBeginFrameBanner

```dart
bool debugPrintBeginFrameBanner
```

在每一帧开始时打印一条横幅。

由引擎触发、并由调度器绑定处理的帧，将带有一条给出帧编号和该帧时间戳的横幅。

由组件框架主动触发的帧（例如调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 时）将显示 "warm-up frame" 字样的标签，而非时间戳（在这种情况下，发送给帧回调的时间戳是上一帧的时间，如果是第一帧则为 0:00）。

若要在每一帧结束时也包含一条横幅，以区分帧内输出和帧间输出，请同时将 [debugPrintEndFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintendframebanner) 设为 true。

另请参阅：

- [debugProfilePaintsEnabled](https://www.yuque.com/thyname/flutter.rendering/debugprofilepaintsenabled)，它对绘制过程做了类似的事情，但使用的是时间线视图。
- [debugPrintLayouts](https://www.yuque.com/thyname/flutter.rendering/debugprintlayouts)，它对布局过程做了类似的事情，但使用控制台输出。
- [WidgetsBinding.drawFrame] 和 [SchedulerBinding.handleBeginFrame] 处的相关讨论。

# debugPrintEndFrameBanner

```dart
bool debugPrintEndFrameBanner
```

在每一帧结束时打印一条横幅。

与 [debugPrintBeginFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintbeginframebanner) 结合使用，有助于判断代码是在一帧执行期间运行，还是在帧与帧之间运行。

# debugPrintScheduleFrameStacks

```dart
bool debugPrintScheduleFrameStacks
```

记录导致一帧被调度的调用栈。

每当 [SchedulerBinding.scheduleFrame] 调度一帧时，都会调用此项。这可能由多种原因触发，例如启动了一个 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 或 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，或调用了 [RenderObject.markNeedsLayout]，或调用了 [State.setState]。

若要专门获取组件被调度构建时的调用栈，请参见 [debugPrintScheduleBuildForStacks](https://www.yuque.com/thyname/flutter.widgets/debugprintschedulebuildforstacks)。

# debugTracePostFrameCallbacks

```dart
bool debugTracePostFrameCallbacks
```

为帧后回调记录时间线追踪事件。

当此标志设为 false（默认值）时，开发者时间线会记录帧后回调运行的时间点，但不会提供关于这段时间在各个具体回调中如何分配的任何信息：

![](https://flutter.github.io/assets-for-api-docs/assets/scheduler/debug_trace_post_frame_callbacks_off.png)

当此标志设为 true 时，将为每个运行的帧后回调记录时间线事件，如下所示：

![](https://flutter.github.io/assets-for-api-docs/assets/scheduler/debug_trace_post_frame_callbacks_on.png)

# debugAssertAllSchedulerVarsUnset()

```dart
bool debugAssertAllSchedulerVarsUnset(String reason)
```

如果调度器库的调试变量均未被更改，则返回 true。

测试框架使用此函数来确保调试变量没有被无意间更改。

完整列表请参见 [调度器库](scheduler/scheduler-library.html)。
