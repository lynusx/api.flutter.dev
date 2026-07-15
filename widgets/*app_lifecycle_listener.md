@docImport 'package:flutter/services.dart';

# AppExitRequestCallback

```dart
typedef AppExitRequestCallback = Future<AppExitResponse> Function()
```

一种回调类型，[AppLifecycleListener.onExitRequested] 使用它来询问应用程序是否要取消应用程序终止。

# AppLifecycleListener

```dart
class AppLifecycleListener with WidgetsBindingObserver, Diagnosticable {}
```

一个可用于监听应用程序生命周期变化的监听器。

要监听应用程序退出请求，并决定在请求退出时应用程序是否应该退出，可创建一个 [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener) 并设置 [onExitRequested] 回调。

要监听应用程序生命周期状态的变化，可定义 [onStateChange] 回调。有关各种状态的详细信息，请参阅 [AppLifecycleState](https://www.yuque.com/thyname/dart.ui/applifecyclestate) 枚举。

每次状态变化时都会调用 [onStateChange] 回调；如果发生的状态转换与某个具体的状态转换回调（如 [onResume]、[onInactive] 等）相对应，那么这些回调也会被调用。

状态变化将按照下图所描述的状态机进行：

![应用程序生命周期图示，由 AppLifecycleState 枚举定义](https://flutter.github.io/assets-for-api-docs/assets/dart-ui/app_lifecycle.png)

该状态机的初始状态为 [AppLifecycleState.detached] 状态，图中的箭头描述了有效的状态转换。蓝色的转换仅在 iOS 和 Android 上发生。

{@tool dartpad} 此示例展示了应用程序如何监听应用程序状态的变化。

** 请参阅 examples/api/lib/widgets/app_lifecycle_listener/app_lifecycle_listener.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 此示例展示了应用程序如何在退出请求发生时选择性地中止请求，而不是遵从该请求。

** 请参阅 examples/api/lib/widgets/app_lifecycle_listener/app_lifecycle_listener.1.dart 中的代码 ** {@end-tool}

另请参阅：

- [ServicesBinding.exitApplication]，一个可调用以请求应用程序退出的函数。
- [WidgetsBindingObserver.didRequestAppExit]，此类用于接收退出请求所使用的处理程序。
- [WidgetsBindingObserver.didChangeAppLifecycleState]，此类用于接收生命周期状态变化所使用的处理程序。

### AppLifecycleListener()

```dart
AppLifecycleListener({WidgetsBinding? binding, VoidCallback? onResume, VoidCallback? onInactive, VoidCallback? onHide, VoidCallback? onShow, VoidCallback? onPause, VoidCallback? onRestart, VoidCallback? onDetach, AppExitRequestCallback? onExitRequested, ValueChanged<AppLifecycleState>? onStateChange})
```

创建一个 [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener)。

### binding

```dart
WidgetsBinding binding
```

用于监听应用程序生命周期事件的 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding)。

通常情况下，该值设为 [WidgetsBinding.instance]，但也可以替换为其他值用于测试或其他特殊用途的绑定。

默认为 [WidgetsBinding.instance]。

### onStateChange

```dart
ValueChanged<AppLifecycleState>? onStateChange
```

在状态发生任何变化时被调用，并传入新状态。

### onInactive

```dart
VoidCallback? onInactive
```

当应用程序失去输入焦点时调用的回调。

在移动平台上，这可能发生在通话期间或系统对话框可见时。

在桌面平台上，这是指应用程序的所有视图都已失去输入焦点，但应用程序至少还有一个视图可见的情况。

在 Web 上，这是指窗口（或标签页）失去输入焦点的情况。

### onResume

```dart
VoidCallback? onResume
```

当应用程序中的某个视图获得输入焦点时调用的回调。

调用此回调表明应用程序正进入可见、活动并接受用户输入的状态。

### onHide

```dart
VoidCallback? onHide
```

当应用程序被隐藏时调用的回调。

在移动平台上，这通常发生在应用程序即将被前台的另一个应用程序替换之前。

在桌面平台上，这发生在应用程序即将因被最小化或以其他方式隐藏所有视图而被隐藏之前。

在 Web 上，这发生在窗口（或标签页）即将被隐藏之前。

### onShow

```dart
VoidCallback? onShow
```

当应用程序显示时调用的回调。

在移动平台上，这通常发生在应用程序即将替换前台的另一个应用程序之前。

在桌面平台上，这发生在应用程序即将因被取消最小化或以其他方式显示至少一个视图而显示之前。

在 Web 上，这发生在窗口（或标签页）即将显示之前。

### onPause

```dart
VoidCallback? onPause
```

当应用程序暂停时调用的回调。

在移动平台上，这发生在应用程序即将被另一个应用程序替换之前。

在桌面平台和 Web 上，此函数不会被调用。

### onRestart

```dart
VoidCallback? onRestart
```

当应用程序在暂停后恢复时调用的回调。

在移动平台上，这发生在此应用程序即将成为活动应用程序之前。

在桌面平台和 Web 上，此函数不会被调用。

### onExitRequested

```dart
AppExitRequestCallback? onExitRequested
```

用于在退出可取消的情况下询问应用程序是否允许退出的回调。

应用程序的退出并非总是可取消的，但当退出可取消时，此函数将在退出发生之前被调用。

返回 [AppExitResponse.exit] 将继续终止流程，而返回 [AppExitResponse.cancel] 将取消终止流程。如果终止未被取消，应用程序将立即退出。

### onDetach

```dart
VoidCallback? onDetach
```

当应用程序已退出，并且已将所有宿主视图从引擎中分离时调用的回调。

此回调仅在 iOS 和 Android 上调用。

### dispose()

```dart
void dispose()
```

在不再使用此监听器时调用。

调用 [dispose] 后请勿再使用该对象。

如果子类重写了 [dispose]，则必须在其中调用此方法。
