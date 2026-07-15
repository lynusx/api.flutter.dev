@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'ticker.dart';

# timeDilation

```dart
double get timeDilation
```

按此系数减慢动画速度，以便于开发调试。

# timeDilation

```dart
set timeDilation(double value)
```

如果 [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding) 已初始化，设置时间膨胀系数会自动调用 [SchedulerBinding.resetEpoch]，以确保调度器绑定的使用者所看到的时间戳始终是递增的。

在初始化绑定之前设置此值是安全的。

# FrameCallback

```dart
typedef FrameCallback = void Function(Duration timeStamp)
```

调度器发出的与帧相关的回调的签名。

`timeStamp` 是自调度器纪元开始以来经过的毫秒数。可使用 timeStamp 来确定动画时间线应推进多少，从而使系统中所有的动画都同步到一个共同的时间基准。

# TaskCallback

```dart
typedef TaskCallback<T> = FutureOr<T> Function()
```

[SchedulerBinding.scheduleTask] 回调的签名。

类型参数 `T` 是任务的返回值。如果任务不返回值，可以考虑使用 `void`。

# SchedulingStrategy

```dart
typedef SchedulingStrategy = bool Function({required int priority, required SchedulerBinding scheduler})
```

[SchedulerBinding.schedulingStrategy] 回调的签名。每当系统需要判断给定优先级的任务是否需要运行时，都会调用它。

如果当前应当执行给定优先级的任务，则返回 true，否则返回 false。

另请参阅：

- [defaultSchedulingStrategy](https://www.yuque.com/thyname/flutter.scheduler/defaultschedulingstrategy)，[SchedulerBinding.schedulingStrategy] 的默认 [SchedulingStrategy](https://www.yuque.com/thyname/flutter.scheduler/schedulingstrategy)。

# SchedulerPhase

```dart
enum SchedulerPhase {}
```

[SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding) 在 [SchedulerBinding.handleBeginFrame] 期间所经历的各个阶段。

该枚举通过 [SchedulerBinding.schedulerPhase] 暴露出来。

此枚举的值按照阶段发生的顺序排列，因此可以比较它们相对的索引值。

另请参阅：

- [WidgetsBinding.drawFrame]，它驱动构建和渲染管线以生成一帧。

当前没有帧正在被处理。此时可能正在执行的有：任务（由 [SchedulerBinding.scheduleTask] 调度）、微任务（由 [scheduleMicrotask](https://www.yuque.com/thyname/dart.async/schedulemicrotask) 调度）、[Timer](https://www.yuque.com/thyname/dart.async/timer) 回调、事件处理程序（例如来自用户输入的事件），以及其他回调（例如来自 [Future](https://www.yuque.com/thyname/dart.async/future)、[Stream](https://www.yuque.com/thyname/dart.async/stream) 等）。

瞬态回调（由 [SchedulerBinding.scheduleFrameCallback] 调度）正在执行。

通常，这些回调用于将对象更新为新的动画状态。

参见 [SchedulerBinding.handleBeginFrame]。

在处理瞬态回调期间调度的微任务正在执行。

例如，这可能包括在 [transientCallbacks] 阶段解析的 Future 所触发的回调。

持久性回调（由 [SchedulerBinding.addPersistentFrameCallback] 调度）正在执行。

通常，这是构建/布局/绘制管线。参见 [WidgetsBinding.drawFrame] 和 [SchedulerBinding.handleDrawFrame]。

帧后回调（由 [SchedulerBinding.addPostFrameCallback] 调度）正在执行。

通常，这些回调用于清理工作以及为下一帧调度任务。

参见 [SchedulerBinding.handleDrawFrame]。

# PerformanceModeRequestHandle

```dart
class PerformanceModeRequestHandle {}
```

一个不透明的句柄，用于使对 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode) 的请求保持有效，直至被释放。

要创建 [PerformanceModeRequestHandle](https://www.yuque.com/thyname/flutter.scheduler/performancemoderequesthandle)，请使用 [SchedulerBinding.requestPerformanceMode]。发起请求的组件负责释放该句柄。

### dispose()

```dart
void dispose()
```

调用此方法以向 [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding) 表明不再需要对 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode) 的请求。

每个对象只能调用此方法一次。

# SchedulerBinding

```dart
mixin SchedulerBinding on BindingBase {}
```

用于运行以下内容的调度器：

- **瞬态回调（Transient callbacks）**，由系统的 [dart:ui.PlatformDispatcher.onBeginFrame] 回调触发，用于将应用程序的行为与系统显示同步。例如，[Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 和 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 便由此触发。

- **持久性回调（Persistent callbacks）**，由系统的 [dart:ui.PlatformDispatcher.onDrawFrame] 回调触发，用于在瞬态回调执行完毕后更新系统显示。例如，渲染层使用它来驱动其渲染管线。

- **帧后回调（Post-frame callbacks）**，在持久性回调之后运行，恰好在 [dart:ui.PlatformDispatcher.onDrawFrame] 回调返回之前执行。

- 非渲染任务，在帧与帧之间运行。这些任务被赋予优先级，并根据 [schedulingStrategy] 按优先级顺序执行。

### initInstances()

```dart
void initInstances()
```

### instance

```dart
SchedulerBinding get instance
```

当前的 [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)（如果已创建）。

提供对此 mixin 所暴露功能的访问。必须先初始化绑定才能使用此获取器；通常通过调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 或 [WidgetsFlutterBinding.ensureInitialized] 来完成初始化。

### addTimingsCallback()

```dart
void addTimingsCallback(TimingsCallback callback)
```

添加一个 [TimingsCallback](https://www.yuque.com/thyname/dart.ui/timingscallback)，用于接收引擎发送的 [FrameTiming](https://www.yuque.com/thyname/dart.ui/frametiming)。

此 API 使应用程序能够监控其图形性能。来自引擎的数据会被批量组织成 [FrameTiming](https://www.yuque.com/thyname/dart.ui/frametiming) 对象列表，在 release 模式下约每秒报告一次，在 debug 和 profile 构建中约每 100ms 报告一次。该列表按时间先后升序排列（最早的帧在前）。第一帧的时序信息会立即发送，不会被批量处理。

返回的数据可用于捕获丢帧情况（通过查看 [FrameTiming.buildDuration] 或 [FrameTiming.rasterDuration] 是否超出帧预算，例如在 60Hz 下为 16ms），以及捕获高延迟情况（通过查看 [FrameTiming.totalSpan] 是否超出帧预算）。在 Flutter 引擎对图形更新进行流水线处理的情况下，即使没有丢帧，延迟也可能超过一帧，例如因为 [FrameTiming.buildDuration] 与 [FrameTiming.rasterDuration] 之和超出了帧预算。在这些情况下，动画会保持流畅，但触摸输入会显得更加迟滞。

优先使用 [addTimingsCallback] 而非直接使用 [dart:ui.PlatformDispatcher.onReportTimings]，因为 [dart:ui.PlatformDispatcher.onReportTimings] API 只允许设置一个回调，这会阻止多个库同时注册监听器，而此 API 允许独立注册多个回调。

此 API 基于 [dart:ui.PlatformDispatcher.onReportTimings] 实现。在 release 构建中，当没有任何库注册此 API 时，[dart:ui.PlatformDispatcher.onReportTimings] 回调不会被设置，从而禁用性能跟踪，并将运行时开销降至几乎为零。当注册了一个或多个回调时（即启用性能跟踪时），性能跟踪本身带来的开销约为每秒 0.01% 的 CPU 占用（在 iPhone 6s 上测得）。

在 debug 和 profile 构建中，[SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding) 自身会注册一个 timings 回调以更新 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline)。

如果同一个回调被添加两次，它将被执行两次。

另请参阅：

- [removeTimingsCallback]，可用于移除通过此方法添加的回调。

### removeTimingsCallback()

```dart
void removeTimingsCallback(TimingsCallback callback)
```

移除此前通过 [addTimingsCallback] 添加的回调。

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### lifecycleState

```dart
AppLifecycleState? get lifecycleState
```

应用程序当前是否可见，如果可见，是否当前处于可交互状态。

当 [SystemChannels.lifecycle] 通知被分发时，此值由 [handleAppLifecycleStateChanged] 设置。

监听此值变化的推荐方式是使用 [WidgetsBindingObserver.didChangeAppLifecycleState]，或通过 [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener) 对象。

### resetInternalState()

```dart
void resetInternalState()
```

允许测试框架将生命周期状态和 framesEnabled 重置为其初始值。

### handleAppLifecycleStateChanged()

```dart
void handleAppLifecycleStateChanged(AppLifecycleState state)
```

在应用程序生命周期状态发生变化时调用。

使用 [WidgetsBindingObserver.didChangeAppLifecycleState] 通知所有观察者。

此方法暴露了来自 [SystemChannels.lifecycle] 的通知。

### schedulingStrategy

```dart
SchedulingStrategy schedulingStrategy
```

用于决定是否运行任务的策略。

默认为 [defaultSchedulingStrategy](https://www.yuque.com/thyname/flutter.scheduler/defaultschedulingstrategy)。

### scheduleTask()

```dart
Future<T> scheduleTask<T>(TaskCallback<T> task, Priority priority, {String? debugLabel, Flow? flow})
```

以给定的 `priority` 调度给定的 `task`。

如果 `task` 返回一个 future，则 [scheduleTask] 返回的 future 将在前者被调度完成之后才完成。否则，[scheduleTask] 返回的 future 将在 `task` 被调度之后，以 `task` 返回的相同值完成。

`debugLabel` 和 `flow` 用于向 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 报告该任务，以便在性能分析时使用。

## Processing model

任务将在帧与帧之间按优先级顺序执行，当前 [schedulingStrategy] 跳过的任务除外。任务应当简短（例如最多一毫秒），以免导致常规的帧回调被延迟。

如果动画正在运行（例如，一个用于指示存在待处理任务的 [ProgressIndicator](https://www.yuque.com/thyname/flutter.material/progressindicator)），那么优先级低于 [Priority.animation] 的任务将不会运行（至少在使用 [defaultSchedulingStrategy](https://www.yuque.com/thyname/flutter.scheduler/defaultschedulingstrategy) 的情况下如此；可以通过 [schedulingStrategy] 对此进行配置）。

### unlocked()

```dart
void unlocked()
```

### handleEventLoopCallback()

```dart
bool handleEventLoopCallback()
```

执行优先级最高的任务（如果其优先级足够高）。

如果调度器处于 [locked] 状态，或没有剩余任务，则返回 false。

否则返回 true，包括因为优先级过低而未执行任何任务的情况。

### transientCallbackCount

```dart
int get transientCallbackCount
```

当前已调度的瞬态帧回调数量。

在一帧开始、所有当前已调度的瞬态回调即将被调用之前，此值会被重置为零。

暴露此数字主要是为了让测试能够验证：在测试资源被妥善释放之后，不再有意外的瞬态回调仍处于注册状态。

### scheduleFrameCallback()

```dart
int scheduleFrameCallback(FrameCallback callback, {bool rescheduling = false, bool scheduleNewFrame = true})
```

调度给定的瞬态帧回调。

将给定的回调添加到帧回调列表中，并在 `scheduleNewFrame` 参数为 true 时确保调度一帧。

`scheduleNewFrame` 参数决定是否应调用 [scheduleFrame] 以确保产生新的一帧。默认为 true。

如果在帧的动画阶段（瞬态帧回调仍在被调用时）调用此方法，`callback` 将在下一帧被调用，而不是在当前帧中调用。

如果这是一次性注册，可忽略 `rescheduling` 参数。

如果这是一个每次触发后都会重新注册的回调，那么在重新注册该回调时，应将 `rescheduling` 参数设为 true。这在 release 构建中没有任何效果，但在 debug 构建中，它可以确保为此回调保存的调用栈是该回调**首次**注册时的原始调用栈，而不是重新注册时的调用栈。这样便于追溯某个回调最初被调用的原因。如果 `rescheduling` 为 true，此调用必须发生在帧回调的上下文中。

通过此方法注册的回调可以使用 [cancelFrameCallbackWithId] 取消。

另请参阅：

- [WidgetsBinding.drawFrame]，其中解释了使用 Flutter widgets 的应用中每一帧的各个阶段（以及瞬态帧回调在这些阶段中所处的位置）。

### cancelFrameCallbackWithId()

```dart
void cancelFrameCallbackWithId(int id)
```

取消具有给定 [id] 的瞬态帧回调。

将给定的回调从帧回调列表中移除。如果已经请求了一帧，此操作并不会同时取消该请求。

瞬态帧回调是指通过 [scheduleFrameCallback] 注册的回调。

### debugAssertNoTransientCallbacks()

```dart
bool debugAssertNoTransientCallbacks(String reason)
```

断言当前没有已注册的瞬态回调；如果有，则打印它们的位置并抛出异常。

瞬态帧回调是指通过 [scheduleFrameCallback] 注册的回调。

预期在测试结束时调用此方法（flutter_test 框架在正常情况下会自动执行此操作）。

当你期望不存在已注册的瞬态回调时，可在 assert 语句中调用此方法，并附上希望在检测到瞬态回调时打印的消息：

```dart
assert(SchedulerBinding.instance.debugAssertNoTransientCallbacks(
  'A leak of transient callbacks was detected while doing foo.'
));
```

如果断言被禁用，则不执行任何操作。始终返回 true。

### debugAssertNoPendingPerformanceModeRequests()

```dart
bool debugAssertNoPendingPerformanceModeRequests(String reason)
```

在 debug 模式下断言不存在待处理的性能模式请求。

如果存在待处理的性能模式请求，则抛出 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)，因为这表明可能存在内存泄漏。

### debugAssertNoTimeDilation()

```dart
bool debugAssertNoTimeDilation(String reason)
```

在 debug 模式下断言不存在人为的时间膨胀。

如果存在这种膨胀，则抛出 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)，因为这会使后续测试也受到时间膨胀的影响，从而变得不稳定。

### debugPrintTransientCallbackRegistrationStack()

```dart
void debugPrintTransientCallbackRegistrationStack()
```

打印当前瞬态回调被注册处的调用栈。

瞬态帧回调是指通过 [scheduleFrameCallback] 注册的回调。

在 debug 模式下、且处于瞬态回调上下文中调用此函数时，会打印出当前瞬态回调被注册处的调用栈（即它首次调用 [scheduleFrameCallback] 的位置）。

在 debug 模式下的其他上下文中调用此函数时，会打印一条消息，说明此函数并非在瞬态回调的上下文中被调用。

在 release 模式下，此函数不执行任何操作。

要调用此函数，请使用以下代码：

```dart
SchedulerBinding.debugPrintTransientCallbackRegistrationStack();
```

### addPersistentFrameCallback()

```dart
void addPersistentFrameCallback(FrameCallback callback)
```

添加一个持久性帧回调。

持久性回调会在瞬态（非持久性）帧回调之后被调用。

**不会**请求新的一帧。从概念上讲，持久性帧回调是"开始帧"事件的观察者。由于它们在瞬态帧回调之后执行，因此可以驱动渲染管线。

持久性帧回调无法被取消注册。一旦注册，它们将在应用程序的整个生命周期中的每一帧都被调用。

另请参阅：

- [WidgetsBinding.drawFrame]，其中解释了使用 Flutter widgets 的应用中每一帧的各个阶段（以及持久性帧回调在这些阶段中所处的位置）。

### addPostFrameCallback()

```dart
void addPostFrameCallback(FrameCallback callback, {String debugLabel = 'callback'})
```

为此帧的结束调度一个回调。

所提供的回调会在一帧结束后立即运行，紧接在持久性帧回调之后（此时主渲染管线已被刷新）。

此方法**不会**请求新的一帧。如果已有一帧正在进行中，且帧后回调的执行尚未开始，则已注册的回调会在当前帧结束时执行。否则，已注册的回调会在下一帧之后执行（无论那是何时，如果确实会发生的话）。

这些回调按照被添加的顺序执行。

帧后回调无法被取消注册。它们只会被调用一次。

在 debug 模式下，如果 [debugTracePostFrameCallbacks](https://www.yuque.com/thyname/flutter.scheduler/debugtracepostframecallbacks) 被设为 true，则已注册的回调将显示在时间线事件图表中，可在 [DevTools](https://docs.flutter.dev/tools/devtools) 中查看。在这种情况下，`debugLabel` 参数指定了该回调在时间线中显示的名称。在 profile 和 release 构建中，帧后回调永远不会被追踪，`debugLabel` 参数会被忽略。

另请参阅：

- [scheduleFrameCallback]，用于为下一帧的开始注册回调。
- [WidgetsBinding.drawFrame]，其中解释了使用 Flutter widgets 的应用中每一帧的各个阶段（以及帧后回调在这些阶段中所处的位置）。

### endOfFrame

```dart
Future<void> get endOfFrame
```

返回一个在帧完成之后才完成的 Future。

如果在帧与帧之间调用此方法，必要时会立即调度一帧。如果在帧执行期间调用此方法，该 Future 将在当前帧完成之后完成。

如果设备屏幕当前处于关闭状态，此操作可能会等待很长时间，因为在设备屏幕关闭期间不会调度帧。

### hasScheduledFrame

```dart
bool get hasScheduledFrame
```

此调度器是否已请求尽快调用 [handleBeginFrame]。

### schedulerPhase

```dart
SchedulerPhase get schedulerPhase
```

调度器当前所处的阶段。

### framesEnabled

```dart
bool get framesEnabled
```

当调用 [scheduleFrame] 时，当前是否会调度帧。

此值取决于 [lifecycleState] 的值。

### ensureFrameCallbacksRegistered()

```dart
void ensureFrameCallbacksRegistered()
```

确保 [PlatformDispatcher.onBeginFrame] 和 [PlatformDispatcher.onDrawFrame] 的回调已被注册。

### ensureVisualUpdate()

```dart
void ensureVisualUpdate()
```

如果此对象当前未在生成帧，则使用 [scheduleFrame] 调度新的一帧。

调用此方法可确保 [handleDrawFrame] 最终会被调用，除非它已经在进行中。

如果 [schedulerPhase] 为 [SchedulerPhase.transientCallbacks] 或 [SchedulerPhase.midFrameMicrotasks]（因为此时已经在准备一帧），或为 [SchedulerPhase.persistentCallbacks]（因为此时正在积极渲染一帧），则此操作不起作用。如果 [schedulerPhase] 为 [SchedulerPhase.idle]（帧与帧之间）或 [SchedulerPhase.postFrameCallbacks]（帧完成之后），则会调度一帧。

### scheduleFrame()

```dart
void scheduleFrame()
```

如有必要，通过调用 [dart:ui.PlatformDispatcher.scheduleFrame] 调度新的一帧。

调用此方法后，引擎最终会调用 [handleBeginFrame]（此调用可能会被延迟，例如如果设备屏幕已关闭，通常会延迟到屏幕开启且应用程序可见为止）。在一帧期间调用此方法会强制调度另一帧，即使当前帧尚未完成。

已调度的帧会在操作系统提供的 "Vsync" 信号触发时得到处理。"Vsync" 信号，即垂直同步信号，历史上与显示刷新有关，那时硬件通过物理方式在两次显示更新之间垂直移动电子束。当代硬件的运作方式更为精细复杂，但概念上的 "Vsync" 刷新信号仍被用来指示应用程序何时应更新其渲染内容。

要在此函数每次调度一帧时都向控制台打印调用栈，请将 [debugPrintScheduleFrameStacks](https://www.yuque.com/thyname/flutter.scheduler/debugprintscheduleframestacks) 设为 true。

另请参阅：

- [scheduleForcedFrame]，在调度帧时会忽略 [lifecycleState]。
- [scheduleWarmUpFrame]，完全忽略 "Vsync" 信号并立即触发一帧。

### scheduleForcedFrame()

```dart
void scheduleForcedFrame()
```

通过调用 [dart:ui.PlatformDispatcher.scheduleFrame] 调度新的一帧。

调用此方法后，即使正常情况下 [scheduleFrame] 不会调度帧（例如设备屏幕已关闭），引擎仍会调用 [handleBeginFrame]。

框架使用此方法，在手机旋转时强制以正确的尺寸渲染一帧，以便屏幕重新开启时能够提供尺寸正确的渲染内容。

要在此函数每次调度一帧时都向控制台打印调用栈，请将 [debugPrintScheduleFrameStacks](https://www.yuque.com/thyname/flutter.scheduler/debugprintscheduleframestacks) 设为 true。

除非必须立即调度一帧，否则应优先使用 [scheduleFrame]，因为在设备本应处于空闲状态时使用 [scheduleForcedFrame] 会显著增加电量消耗。

如果目标是尽快更新渲染内容（例如在应用程序启动时），可考虑改用 [scheduleWarmUpFrame]。

### scheduleWarmUpFrame()

```dart
void scheduleWarmUpFrame()
```

调度一帧尽快运行，而不是等待引擎响应系统 "Vsync" 信号来请求一帧。

这在应用程序启动期间使用，以便第一帧（其开销通常相当大）能获得额外的几毫秒来运行。

在已调度的帧完成之前，会锁定事件分发。

如果已经通过 [scheduleFrame] 或 [scheduleForcedFrame] 调度了一帧，此调用可能会延迟该帧。

如果已调度的帧已经开始，或者已经调用过另一次 [scheduleWarmUpFrame]，则此调用将被忽略。

在正常操作中，应优先使用 [scheduleFrame] 来更新显示内容。

## Design discussion

当 Flutter 引擎收到来自操作系统的请求时（由于历史原因称为 vsync），会提示框架生成帧。然而，这可能在应用启动后（或热重载后）的若干毫秒内都不会发生。为了利用组件树首次配置完成到引擎请求更新之间的这段时间，框架会调度一个**预热帧（warm-up frame）**。

预热帧可能实际上从不真正渲染（因为引擎并未请求它，因此没有有效的绘制上下文），但它会促使框架经历构建、布局和绘制的各个步骤，这些步骤合计可能需要几毫秒。因此，当引擎请求真正的一帧时，大部分工作已经完成，框架便可以以最小的额外开销生成该帧。

预热帧在启动时由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 调度，在热重载期间由 [RendererBinding.performReassemble] 调度。

当框架因调用 [RendererBinding.allowFirstFrame] 而被解除阻塞时（对应于此前调用 [RendererBinding.deferFirstFrame] 阻塞了渲染），也会调度预热帧。

### resetEpoch()

```dart
void resetEpoch()
```

为时间戳计算方式的一次非单调变化做好准备。

从调度器接收到的回调都假定其时间戳是单调递增的。传递给 [handleBeginFrame] 的原始时间戳是单调的，但调度器可能会调整这些时间戳以提供 [timeDilation](https://www.yuque.com/thyname/flutter.scheduler/timedilation) 效果。如果不加以妥善处理，这些调整可能导致时间看起来在倒退。

[resetEpoch] 函数通过将用于未来时间戳调整的基准时间戳重置为当前值，来确保时间戳保持单调。例如，如果 [timeDilation](https://www.yuque.com/thyname/flutter.scheduler/timedilation) 减小，[resetEpoch] 不会缩放自纪元开始以来的整个 [Duration](https://www.yuque.com/thyname/dart.core/duration)，而是确保仅缩放自 [resetEpoch] 被调用以来的时长。

设置 [timeDilation](https://www.yuque.com/thyname/flutter.scheduler/timedilation) 会自动调用 [resetEpoch]。你无需自行调用 [resetEpoch]。

将给定的时间戳调整到当前纪元。

这既会根据纪元的开始时间（无论是原始时间还是纪元自身的时间线）对时间戳进行偏移，也会根据当前纪元中的时间膨胀系数对时间戳进行缩放。

这些机制共同确保了我们在帧回调期间给出的时长是单调递增的。

### currentFrameTimeStamp

```dart
Duration get currentFrameTimeStamp
```

当前正在处理的帧的时间戳。

此值仅在 [handleBeginFrame] 开始到对应的 [handleDrawFrame] 结束之间有效，即在一帧正在被生成的期间有效。

### currentSystemFrameTimeStamp

```dart
Duration get currentSystemFrameTimeStamp
```

引擎为当前正在处理的帧提供给 [dart:ui.PlatformDispatcher.onBeginFrame] 的原始时间戳。

与 [currentFrameTimeStamp] 不同，此时间戳既不会因纪元开始时间而被偏移，也不会根据当前纪元的 [timeDilation](https://www.yuque.com/thyname/flutter.scheduler/timedilation) 而被缩放。

在大多数平台上，此值或多或少是任意的，通常应予以忽略。在 Fuchsia 上，此值对应于系统提供的呈现时间，可用于确保在不同进程中运行的动画保持同步。

### handleBeginFrame()

```dart
void handleBeginFrame(Duration? rawTimeStamp)
```

由引擎调用，以使框架准备好生成新的一帧。

此函数调用所有通过 [scheduleFrameCallback] 注册的瞬态帧回调。随后返回，运行任何已调度的微任务（例如由瞬态帧回调解析的 [Future](https://www.yuque.com/thyname/dart.async/future) 所对应的处理程序），并调用 [handleDrawFrame] 以继续该帧的处理。

如果给定的时间戳为 null，则会复用上一帧的时间戳。

要在 debug 模式下于每一帧开始时显示横幅，请将 [debugPrintBeginFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintbeginframebanner) 设为 true。该横幅会使用 [debugPrint](https://www.yuque.com/thyname/flutter.foundation/debugprint) 打印到控制台，内容包含帧编号（每帧递增一）和该帧的时间戳。如果给定的时间戳为 null，则会显示字符串 "warm-up frame" 而非时间戳。这样便可将框架主动推送的帧与引擎响应操作系统 "Vsync" 信号所请求的帧区分开来。

你也可以通过将 [debugPrintEndFrameBanner](https://www.yuque.com/thyname/flutter.scheduler/debugprintendframebanner) 设为 true，在每一帧结束时显示横幅。这样便可将一帧执行期间打印的日志语句与帧与帧之间打印的日志语句（例如响应事件或定时器时打印的日志）区分开来。

### requestPerformanceMode()

```dart
PerformanceModeRequestHandle? requestPerformanceMode(DartPerformanceMode mode)
```

请求特定的 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode)。

如果由于性能模式请求存在冲突而请求失败，则返回 `null`。当两个请求的 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode) 类型不同、且此前已存在对某个性能模式的显式请求时，即视为存在冲突。

请求方在不再需要该性能模式时，负责调用 [PerformanceModeRequestHandle.dispose]。

移除对特定 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode) 的请求。

如果所有待处理的请求都已被释放，引擎将恢复为 [DartPerformanceMode.balanced] 性能模式。

### debugGetRequestedPerformanceMode()

```dart
DartPerformanceMode? debugGetRequestedPerformanceMode()
```

返回当前请求的 [DartPerformanceMode](https://www.yuque.com/thyname/dart.ui/dartperformancemode)；如果尚未发出任何请求，则返回 `null`。

此功能仅在 debug 和 profile 模式下受支持，在 release 模式下返回 `null`。

### handleDrawFrame()

```dart
void handleDrawFrame()
```

由引擎调用，以生成新的一帧。

此方法紧接在 [handleBeginFrame] 之后被调用。它会调用所有通过 [addPersistentFrameCallback] 注册的回调（这些回调通常驱动渲染管线），然后调用通过 [addPostFrameCallback] 注册的回调。

有关处理帧回调时可能有用的调试钩子的讨论，请参见 [handleBeginFrame]。

# defaultSchedulingStrategy()

```dart
bool defaultSchedulingStrategy({required int priority, required SchedulerBinding scheduler})
```

[SchedulerBinding.schedulingStrategy] 的默认 [SchedulingStrategy](https://www.yuque.com/thyname/flutter.scheduler/schedulingstrategy)。

如果存在任何已注册的帧回调，则仅运行 [Priority](https://www.yuque.com/thyname/flutter.scheduler/priority) 为 [Priority.animation] 或更高的任务。否则，运行所有任务。
