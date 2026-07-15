@docImport 'dart:ui'; @docImport 'package:flutter/animation.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'adapter.dart'; @docImport 'app_lifecycle_listener.dart'; @docImport 'basic.dart'; @docImport 'focus_scope.dart'; @docImport 'media_query.dart'; @docImport 'navigator.dart'; @docImport 'pop_scope.dart';

# WidgetsBindingObserver

```dart
abstract mixin class WidgetsBindingObserver {}
```

用于向组件（Widgets）层绑定注册的类的接口。

此接口不仅可用于组件，也可用于任何类。它提供了一个接口，[WidgetsBinding.addObserver] 和 [WidgetsBinding.removeObserver] 使用该接口来通知对象环境发生的变化，例如设备指标或无障碍设置的变化。它被用于实现诸如 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 之类的特性。

此类可以直接被继承，也可以被混入（mixin），以获得所有处理程序的默认行为。此外，也可以通过 `implements` 关键字使用它，在这种情况下必须实现所有处理程序（分析器会列出被遗漏的部分）。

要开始接收通知，请调用 `WidgetsBinding.instance.addObserver`，并传入实现 [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver) 接口的对象的引用。为避免内存泄漏，请在对象生命周期结束时调用 `WidgetsBinding.instance.removeObserver` 以取消注册该对象。

{@tool dartpad} 此示例展示了如何实现 [State](https://www.yuque.com/thyname/flutter.widgets/state) 和 [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver) 协议中必要的部分，以响应应用程序生命周期消息。参见 [didChangeAppLifecycleState]。

若要响应其他通知，请将本示例中的 [didChangeAppLifecycleState] 方法替换为此类中的其他方法。

** See code in examples/api/lib/widgets/binding/widget_binding_observer.0.dart ** {@end-tool}

### didPopRoute()

```dart
Future<bool> didPopRoute()
```

当系统告知应用弹出当前路由时调用，例如在系统返回按钮被按下或返回手势发生之后。

观察者按注册顺序被依次通知，直到某个观察者返回 true 为止。如果没有观察者返回 true，则应用程序会退出。

观察者若能够处理该通知（例如通过关闭一个活动的对话框），则应返回 true；否则返回 false。[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 组件使用此机制通知 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 组件，告知其应尽可能弹出当前路由。

此方法暴露了来自 [SystemChannels.navigation] 的 `popRoute` 通知。

{@macro flutter.widgets.AndroidPredictiveBack}

### handleStartBackGesture()

```dart
bool handleStartBackGesture(PredictiveBackEvent backEvent)
```

在预测性返回手势开始时调用。

观察者按注册顺序被依次通知，直到某个观察者返回 true 或所有观察者都已被通知。如果某个观察者返回 true，那么在同一手势的后续过程中（例如 [handleUpdateBackGestureProgress] 等），将只有该观察者会被通知。

观察者若能够处理该通知（例如通过启动一个预测性返回动画），则应返回 true；否则返回 false。[PredictiveBackPageTransitionsBuilder](https://www.yuque.com/thyname/flutter.material/predictivebackpagetransitionsbuilder) 使用此机制来监听预测性返回手势。

如果所有观察者都通过返回 false 表示不处理此返回手势，那么当 [handleCommitBackGesture] 被调用时，将会触发导航弹出操作，如同非预测性系统返回手势一样。

目前，此功能仅在支持预测性返回特性的 Android 设备上使用。

### handleUpdateBackGestureProgress()

```dart
void handleUpdateBackGestureProgress(PredictiveBackEvent backEvent)
```

当预测性返回手势移动时调用。

被通知此手势 [handleStartBackGesture] 的观察者同样会被通知此事件。

目前，此功能仅在支持预测性返回特性的 Android 设备上使用。

### handleCommitBackGesture()

```dart
void handleCommitBackGesture()
```

当预测性返回手势成功完成时调用，表示应弹出当前路由。

被通知此手势 [handleStartBackGesture] 的观察者同样会被通知此事件。如果没有这样的观察者，则会触发导航弹出操作，如同非预测性系统返回手势一样。

目前，此功能仅在支持预测性返回特性的 Android 设备上使用。

### handleCancelBackGesture()

```dart
void handleCancelBackGesture()
```

当预测性返回手势被取消时调用，表示不应发生任何导航操作。

被通知此手势 [handleStartBackGesture] 的观察者同样会被通知此事件。

目前，此功能仅在支持预测性返回特性的 Android 设备上使用。

### handleStatusBarTap()

```dart
void handleStatusBarTap()
```

当用户在 iOS 上点击状态栏时调用，用于将滚动视图滚动到顶部。

此事件通常只应由至多一个滚动视图处理，因此该回调的实现者必须协调，确定处理此事件的最合适的滚动视图。

此回调仅在 iOS 上调用。[WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver) 提供的默认实现不执行任何操作。

另请参阅：

- [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 和 [CupertinoPageScaffold](https://www.yuque.com/thyname/flutter.cupertino/cupertinopagescaffold)，它们使用此回调实现 iOS 滚动到顶部的功能。

### didPushRoute()

```dart
Future<bool> didPushRoute(String route)
```

当宿主告知应用程序将新路由推入导航器时调用。

观察者若能够处理该通知应返回 true。观察者按注册顺序被依次通知，直到某个观察者返回 true 为止。

此方法暴露了来自 [SystemChannels.navigation] 的 `pushRoute` 通知。

### didPushRouteInformation()

```dart
Future<bool> didPushRouteInformation(RouteInformation routeInformation)
```

当宿主告知应用程序将新的 [RouteInformation](https://www.yuque.com/thyname/flutter.widgets/routeinformation) 及恢复状态推入路由器时调用。

观察者若能够处理该通知应返回 true。观察者按注册顺序被依次通知，直到某个观察者返回 true 为止。

此方法暴露了来自 [SystemChannels.navigation] 的 `pushRouteInformation` 通知。

默认实现是使用由 [RouteInformation.uri] 的路径和查询参数构造的字符串直接调用 [didPushRoute]。

### didChangeMetrics()

```dart
void didChangeMetrics()
```

当应用程序的尺寸发生变化时调用。例如，当手机被旋转时。

此方法暴露了来自 [dart:ui.PlatformDispatcher.onMetricsChanged] 的通知。

{@tool snippet}

此 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 实现了 [State](https://www.yuque.com/thyname/flutter.widgets/state) 和 [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver) 协议中必要的部分，用于在设备旋转（或以其他方式改变尺寸）时作出响应。

```dart
class MetricsReactor extends StatefulWidget {
  const MetricsReactor({ super.key });

  @override
  State<MetricsReactor> createState() => _MetricsReactorState();
}

class _MetricsReactorState extends State<MetricsReactor> with WidgetsBindingObserver {
  late Size _lastSize;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    // [View.of] exposes the view from `WidgetsBinding.instance.platformDispatcher.views`
    // into which this widget is drawn.
    _lastSize = View.of(context).physicalSize;
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeMetrics() {
    setState(() { _lastSize = View.of(context).physicalSize; });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Current size: $_lastSize');
  }
}
```

{@end-tool}

一般而言，这并非必需，因为布局系统会在应用程序尺寸变化时自动重新计算应用程序的几何信息。

另请参阅：

- [MediaQuery.sizeOf]，它以更少的样板代码提供了类似的功能。

### didChangeTextScaleFactor()

```dart
void didChangeTextScaleFactor()
```

当平台的文本缩放系数发生变化时调用。

这通常是用户更改系统偏好设置的结果，它应该影响应用程序中所有文本的大小。

此方法暴露了来自 [dart:ui.PlatformDispatcher.onTextScaleFactorChanged] 的通知。

{@tool snippet}

```dart
class TextScaleFactorReactor extends StatefulWidget {
  const TextScaleFactorReactor({super.key});

  @override
  State<TextScaleFactorReactor> createState() => _TextScaleFactorReactorState();
}

class _TextScaleFactorReactorState extends State<TextScaleFactorReactor>
    with WidgetsBindingObserver {
  double _lastTextScaleFactor =
      WidgetsBinding.instance.platformDispatcher.textScaleFactor;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeTextScaleFactor() {
    setState(() {
      _lastTextScaleFactor =
          WidgetsBinding.instance.platformDispatcher.textScaleFactor;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Current scale factor: $_lastTextScaleFactor');
  }
}
```

{@end-tool}

另请参阅：

- [MediaQuery.textScaleFactorOf]，它以更少的样板代码提供了类似的功能。

### didChangePlatformBrightness()

```dart
void didChangePlatformBrightness()
```

当平台亮度发生变化时调用。

此方法暴露了来自 [dart:ui.PlatformDispatcher.onPlatformBrightnessChanged] 的通知。

另请参阅：

- [MediaQuery.platformBrightnessOf]，它以更少的样板代码提供了类似的功能。

### didChangeLocales()

```dart
void didChangeLocales(List<Locale>? locales)
```

当系统告知应用程序用户的语言区域已更改时调用。例如，当用户更改系统语言设置时。

此方法暴露了来自 [dart:ui.PlatformDispatcher.onLocaleChanged] 的通知。

### didChangeAppLifecycleState()

```dart
void didChangeAppLifecycleState(AppLifecycleState state)
```

当系统将应用置于后台或将应用恢复到前台时调用。

[WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver) 类级别的文档中提供了实现此方法的示例。

此方法暴露了来自 [SystemChannels.lifecycle] 的通知。

另请参阅：

- [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener)，一个用于响应应用程序生命周期变化的替代 API。

### didChangeViewFocus()

```dart
void didChangeViewFocus(ViewFocusEvent event)
```

每当 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 收到某个视图的焦点状态已更改的通知时调用。

[event] 包含更改了焦点状态的视图的视图 ID。

特定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 所在的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的视图 ID 可以通过 `View.of(context).viewId` 获取，从而可以将其与 `event` 中的视图 ID 进行比较，以判断该事件是否与给定的上下文相关。

### didRequestAppExit()

```dart
Future<AppExitResponse> didRequestAppExit()
```

当系统收到退出应用程序的请求时调用。

如果任何观察者以 [AppExitResponse.cancel] 响应，则会取消退出操作。所有观察者在退出前都会被询问。

{@macro flutter.services.binding.ServicesBinding.requestAppExit}

另请参阅：

- [ServicesBinding.exitApplication]，可调用该函数以请求应用程序退出。

### didHaveMemoryPressure()

```dart
void didHaveMemoryPressure()
```

当系统内存不足时调用。

此方法暴露了来自 [SystemChannels.system] 的 `memoryPressure` 通知。

### didChangeAccessibilityFeatures()

```dart
void didChangeAccessibilityFeatures()
```

当系统更改当前激活的无障碍功能集合时调用。

此方法暴露了来自 [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged] 的通知。

# WidgetsBinding

```dart
mixin WidgetsBinding on BindingBase, ServicesBinding, SchedulerBinding, GestureBinding, RendererBinding, SemanticsBinding {}
```

组件层与 Flutter 引擎之间的粘合层。

[WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 管理一棵以 [rootElement] 为根的单一 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树。调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)（间接调用 [attachRootWidget]）会引导（bootstrap）该 Element 树。

## 与渲染树的关系

多个渲染树可以与该 Element 树相关联，它们由底层的 [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding) 管理。

Element 树被划分为两种类型的区域：渲染区域和非渲染区域。

渲染区域是 Element 树中由渲染树支持的部分，它描述了在屏幕上绘制的像素。对于此区域中的元素，[Element.renderObject] 永远不会返回 null，因为这些元素都关联着 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。几乎所有组件都可以放置在渲染区域中；值得注意的例外是 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件、[ViewCollection](https://www.yuque.com/thyname/flutter.widgets/viewcollection) 组件和 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget)。

非渲染区域是 Element 树中不由渲染树支持的部分。对于此区域中的元素，[Element.renderObject] 返回 null，因为这些元素没有关联任何 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。只有不产生 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的组件才能在此区域中使用，因为没有渲染树可供渲染对象附加。换言之，[RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 不能在此区域中使用。通常，[InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)、[View](https://www.yuque.com/thyname/flutter.widgets/view) 和 [ViewCollection](https://www.yuque.com/thyname/flutter.widgets/viewcollection) 会出现在此区域中，用于在渲染区域之间注入数据，并将渲染区域（以及由此扩展的相关渲染树）组织成一棵统一的 Element 树。

位于 [rootElement] 的 Element 树的根节点开启了一个非渲染区域。在非渲染区域内，[View](https://www.yuque.com/thyname/flutter.widgets/view) 组件用于通过引导一棵渲染树来开启一个渲染区域。在渲染区域内，可以使用 [ViewAnchor](https://www.yuque.com/thyname/flutter.widgets/viewanchor) 来开启一个新的非渲染区域。

要判断某个元素是否位于渲染区域中，可以沿树向上遍历，在其祖先上调用 [Element.debugExpectsRenderObjectForSlot]。如果到达某个返回 false 的元素，则说明它位于非渲染区域中。如果到达某个 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 祖先，则说明它位于渲染区域中。

### initInstances()

```dart
void initInstances()
```

### instance

```dart
WidgetsBinding get instance
```

当前的 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding)（如果已创建）。

提供对此混入所暴露特性的访问。必须先初始化该绑定才能使用此获取器；这通常通过调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 或 [WidgetsFlutterBinding.ensureInitialized] 完成。

### debugShowWidgetInspectorOverride

```dart
bool get debugShowWidgetInspectorOverride
```

如果为 true，则强制显示组件检查器（widget inspector）。

覆盖在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中设置的 `debugShowWidgetInspector` 值。

由 `debugShowWidgetInspector` 调试扩展使用。

检查器允许在设备或模拟器上选择一个位置，并查看与之关联的组件和渲染对象。所选组件的轮廓和一些摘要信息会显示在设备上，更详细的信息则显示在 IDE 或 DevTools 中。

### debugShowWidgetInspectorOverride

```dart
set debugShowWidgetInspectorOverride(bool value)
```

### debugShowWidgetInspectorOverrideNotifier

```dart
ValueNotifier<bool> get debugShowWidgetInspectorOverrideNotifier
```

[debugShowWidgetInspectorOverride] 的通知器。

### debugWidgetInspectorSelectionOnTapEnabled

```dart
ValueNotifier<bool> get debugWidgetInspectorSelectionOnTapEnabled
```

用于指示在启用组件检查器时，设备上的点击是否被视为组件选择操作的通知器。

- 如果为 true，应用中的点击会被组件检查器拦截。
- 如果为 false，应用中的点击不会被组件检查器拦截。

### debugExcludeRootWidgetInspector

```dart
bool get debugExcludeRootWidgetInspector
```

如果为 true，则不会自动将 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 注入到组件树中。

这会覆盖以下行为：当在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中设置了 `debugShowWidgetInspector` 值，或将 [debugShowWidgetInspectorOverride] 设置为 true 时，[WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 会被添加到由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的组件树中。

供那些希望通过手动注入 [WidgetInspector](https://www.yuque.com/thyname/flutter.widgets/widgetinspector) 实例，从而更好地控制组件检查器可以选择和高亮显示哪些组件的工具使用。

### debugExcludeRootWidgetInspector

```dart
set debugExcludeRootWidgetInspector(bool value)
```

### resetInternalState()

```dart
void resetInternalState()
```

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### buildOwner

```dart
BuildOwner? get buildOwner
```

负责为此绑定根节点所在的组件树执行构建流水线的 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)。

### focusManager

```dart
FocusManager get focusManager
```

负责焦点树的对象。

很少直接使用。相反，通常使用 [FocusScope.of] 来获取给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)。

更多详情参见 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)。

### platformMenuDelegate

```dart
PlatformMenuDelegate platformMenuDelegate
```

一个用于与平台插件通信，以序列化和管理由 [PlatformMenuBar](https://www.yuque.com/thyname/flutter.widgets/platformmenubar) 创建的平台渲染菜单栏的委托。

默认情况下，此值在 [initInstances] 中被设置为一个 [DefaultPlatformMenuDelegate](https://www.yuque.com/thyname/flutter.widgets/defaultplatformmenudelegate) 实例。

### addObserver()

```dart
void addObserver(WidgetsBindingObserver observer)
```

将给定对象注册为绑定观察者。当各种应用程序事件发生时（例如系统语言区域发生变化时），绑定观察者会收到通知。通常，组件树中的某一个组件会将自身注册为绑定观察者，并将系统状态转换为继承组件（inherited widget）。

例如，[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 组件注册为绑定观察者，并在每次构建时将屏幕尺寸传递给 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 组件，这使得其他组件能够使用 [MediaQuery.sizeOf] 静态方法以及（隐式地）[InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 机制，在屏幕尺寸变化时（例如每次屏幕旋转时）收到通知。

另请参阅：

- [removeObserver]，用于释放此方法所占用的资源。
- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，其中提供了使用此方法的示例。

### removeObserver()

```dart
bool removeObserver(WidgetsBindingObserver observer)
```

取消注册给定的观察者。应谨慎使用此方法，因为其相对开销较大（在已注册观察者数量上为 O(N)）。

另请参阅：

- [addObserver]，用于最初添加观察者的方法。
- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，其中提供了使用此方法的示例。

### handleRequestAppExit()

```dart
Future<AppExitResponse> handleRequestAppExit()
```

### handleMetricsChanged()

```dart
void handleMetricsChanged()
```

### handleTextScaleFactorChanged()

```dart
void handleTextScaleFactorChanged()
```

### handlePlatformBrightnessChanged()

```dart
void handlePlatformBrightnessChanged()
```

### handleAccessibilityFeaturesChanged()

```dart
void handleAccessibilityFeaturesChanged()
```

### handleLocaleChanged()

```dart
void handleLocaleChanged()
```

当系统语言区域发生变化时调用。

调用 [dispatchLocalesChanged] 以通知绑定观察者。

参见 [dart:ui.PlatformDispatcher.onLocaleChanged]。

### dispatchLocalesChanged()

```dart
void dispatchLocalesChanged(List<Locale>? locales)
```

通知所有观察者语言区域已发生变化（使用 [WidgetsBindingObserver.didChangeLocales]），并向它们传递 `locales` 参数。

当收到 [PlatformDispatcher.onLocaleChanged] 通知时，[handleLocaleChanged] 会调用此方法。

### dispatchAccessibilityFeaturesChanged()

```dart
void dispatchAccessibilityFeaturesChanged()
```

通知所有观察者激活的 [AccessibilityFeatures](https://www.yuque.com/thyname/dart.ui/accessibilityfeatures) 集合已发生变化（使用 [WidgetsBindingObserver.didChangeAccessibilityFeatures]），并向它们传递 `features` 参数。

当收到 [PlatformDispatcher.onAccessibilityFeaturesChanged] 通知时，[handleAccessibilityFeaturesChanged] 会调用此方法。

### handlePopRoute()

```dart
Future<bool> handlePopRoute()
```

当系统弹出当前路由时调用。

此方法首先按注册顺序通知绑定观察者（使用 [WidgetsBindingObserver.didPopRoute]），直到某个观察者返回 true，表示它能够处理该请求（例如通过关闭一个对话框）。如果没有观察者返回 true，则通过调用 [SystemNavigator.pop] 关闭应用程序。

[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 将此方法与 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 结合使用，使返回按钮能够关闭对话框、从模态页面返回等。

此方法暴露了来自 [SystemChannels.navigation] 的 `popRoute` 通知。

{@template flutter.widgets.AndroidPredictiveBack}

## 提前处理返回操作

并非所有系统返回操作都会导致调用此方法。有些操作完全由系统处理，不会通知 Flutter 框架。

Android API 33+ 引入了一项名为预测性返回（predictive back）的功能，允许用户在返回手势期间窥视当前应用或路由背后的内容，然后决定取消或提交返回操作。Flutter 会提前启用或禁用此功能（在返回手势发生之前），触发预测性返回的返回手势完全由系统处理，不会在框架中触发此处的方法。

默认情况下，框架通过在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中使用 [SystemNavigator.setFrameworkHandlesBack] 来告知系统它希望处理系统返回手势。这是根据 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 堆栈的状态以及是否存在任何 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope) 组件自动完成的。开发者可以通过直接调用该方法或使用 [NavigationNotification](https://www.yuque.com/thyname/flutter.widgets/navigationnotification) 来手动设置此项。{@endtemplate}

### handlePushRoute()

```dart
Future<bool> handlePushRoute(String route)
```

当宿主告知应用程序将新路由推入导航器时调用。

此方法按注册顺序通知绑定观察者（使用 [WidgetsBindingObserver.didPushRoute]），直到某个观察者返回 true，表示它能够处理该请求（例如通过打开一个对话框）。如果没有观察者返回 true，则不执行任何操作。

此方法暴露了来自 [SystemChannels.navigation] 的 `pushRoute` 通知。

### handleAppLifecycleStateChanged()

```dart
void handleAppLifecycleStateChanged(AppLifecycleState state)
```

### handleViewFocusChanged()

```dart
void handleViewFocusChanged(ViewFocusEvent event)
```

### handleMemoryPressure()

```dart
void handleMemoryPressure()
```

### firstFrameRasterized

```dart
bool get firstFrameRasterized
```

Flutter 引擎是否已经栅格化（rasterize）第一帧。

通常，一帧被栅格化的时间与它在显示器上呈现的时间非常接近。具体来说，栅格化是仍处于 Flutter 控制范围内的一帧的最后一个耗时阶段。

另请参阅：

- [waitUntilFirstFrameRasterized]，[firstFrameRasterized] 变为 true 时完成的 Future。

### waitUntilFirstFrameRasterized

```dart
Future<void> get waitUntilFirstFrameRasterized
```

当 Flutter 引擎已栅格化第一帧时完成的 Future。

通常，一帧被栅格化的时间与它在显示器上呈现的时间非常接近。具体来说，栅格化是仍处于 Flutter 控制范围内的一帧的最后一个耗时阶段。

另请参阅：

- [firstFrameRasterized]，该 Future 是否已经完成。

### debugDidSendFirstFrameEvent

```dart
bool get debugDidSendFirstFrameEvent
```

第一帧是否已构建完成。

此值也可以通过 VM service 协议以 `ext.flutter.didSendFirstFrameEvent` 的形式获取。

另请参阅：

- [firstFrameRasterized]，第一帧是否已完成渲染。

### debugBuildingDirtyElements

```dart
bool debugBuildingDirtyElements
```

我们当前是否处于一帧之中。用于验证帧不会被重复调度。

此属性是公开的，以便测试框架可以更改它。

此标志在发布版本（release build）中不会被使用。

### drawFrame()

```dart
void drawFrame()
```

驱动构建和渲染流水线以生成一帧。

此方法由 [handleDrawFrame] 调用，而 [handleDrawFrame] 本身会在需要布局和绘制一帧时由引擎自动调用。

每一帧包括以下几个阶段：

1.  动画阶段：与 [PlatformDispatcher.onBeginFrame] 注册的 [handleBeginFrame] 方法，会按注册顺序调用通过 [scheduleFrameCallback] 注册的所有瞬时帧回调。这包括驱动 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 对象的所有 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 实例，也就是说所有活跃的 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 对象会在此时刻更新（tick）。

2.  微任务：在 [handleBeginFrame] 返回后，由瞬时帧回调调度的任何微任务都会得到运行的机会。这通常包括本帧完成的 [Ticker](https://www.yuque.com/thyname/flutter.scheduler/ticker) 和 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 所对应 Future 的回调。

在 [handleBeginFrame] 之后，与 [PlatformDispatcher.onDrawFrame] 注册的 [handleDrawFrame] 会被调用，它会调用所有持久帧回调，其中最重要的就是本方法 [drawFrame]，其流程如下：

3.  构建阶段：组件树中所有脏（dirty）的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 会被重建（参见 [State.build]）。有关如何将组件标记为需要构建的更多详情，参见 [State.setState]。有关此步骤的更多信息，参见 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)。

4.  布局阶段：系统中所有脏的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 会被布局（参见 [RenderObject.performLayout]）。有关如何将对象标记为需要布局的更多详情，参见 [RenderObject.markNeedsLayout]。

5.  合成位（compositing bits）阶段：会更新任何脏 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 对象上的合成位。参见 [RenderObject.markNeedsCompositingBitsUpdate]。

6.  绘制阶段：系统中所有脏的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 会被重新绘制（参见 [RenderObject.paint]）。这会生成 [Layer](https://www.yuque.com/thyname/flutter.rendering/layer) 树。有关如何将对象标记为需要绘制的更多详情，参见 [RenderObject.markNeedsPaint]。

7.  合成阶段：图层树会被转换为一个 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 并发送到 GPU。

8.  语义阶段：系统中所有脏的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 都会更新其语义（参见 [RenderObject.assembleSemanticsNode]）。这会生成 [SemanticsNode](https://www.yuque.com/thyname/flutter.semantics/semanticsnode) 树。有关如何将对象标记为需要语义更新的更多详情，参见 [RenderObject.markNeedsSemanticsUpdate]。

有关第 4-8 步的更多详情，参见 [PipelineOwner](https://www.yuque.com/thyname/flutter.rendering/pipelineowner)。

9. 组件层的收尾阶段：组件树被最终确定。这会导致对本帧从组件树中移除的对象调用 [State.dispose]。更多详情参见 [BuildOwner.finalizeTree]。

10. 调度器层的收尾阶段：[drawFrame] 返回后，[handleDrawFrame] 会调用帧后回调（通过 [addPostFrameCallback] 注册）。

### rootElement

```dart
Element? get rootElement
```

位于 Element 树层次结构根部的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

此值在首次调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 时初始化。

### renderViewElement

```dart
Element? get renderViewElement
```

已弃用。将在未来版本的 Flutter 中移除。

请改用 [rootElement]。

### framesEnabled

```dart
bool get framesEnabled
```

### wrapWithDefaultView()

```dart
Widget wrapWithDefaultView(Widget rootWidget)
```

由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 使用，用于将提供的 `rootWidget` 包装在默认的 [View](https://www.yuque.com/thyname/flutter.widgets/view) 中。

[View](https://www.yuque.com/thyname/flutter.widgets/view) 决定应用被渲染到哪个 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 中。目前这是来自 [platformDispatcher] 的 [PlatformDispatcher.implicitView]。如果 [PlatformDispatcher.implicitView] 为 null，此方法将抛出 [StateError](https://www.yuque.com/thyname/dart.core/stateerror)。

传递给此方法的 `rootWidget` 组件不得已经被包装在 [View](https://www.yuque.com/thyname/flutter.widgets/view) 中。

### scheduleAttachRootWidget()

```dart
void scheduleAttachRootWidget(Widget rootWidget)
```

调度一个用于附加根组件的 [Timer](https://www.yuque.com/thyname/dart.async/timer)。

由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 调用，以配置组件树。如果希望同步构建组件树，可以考虑使用 [attachRootWidget]。

### attachRootWidget()

```dart
void attachRootWidget(Widget rootWidget)
```

获取一个组件并将其附加到 [rootElement] 上，如有必要则创建它。

由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 调用，以配置组件树。

另请参阅：

- [RenderObjectToWidgetAdapter.attachToRenderTree]，用于填充（inflate）一个组件并将其附加到渲染树。

### attachToBuildOwner()

```dart
void attachToBuildOwner(RootWidget widget)
```

由 [attachRootWidget] 调用，以将提供的 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 附加到 [buildOwner]。

如有必要，此方法会创建 [rootElement]，或者复用已有的 [rootElement]。

很少直接调用此方法，但在测试中，通过提供先前版本的 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget)，将 Element 树恢复到先前版本时，此方法可能会很有用（示例用法参见 [WidgetTester.restartAndRestore]）。

### isRootWidgetAttached

```dart
bool get isRootWidgetAttached
```

[rootElement] 是否已被初始化。

在调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)（或在 [TestWidgetsFlutterBinding] 上下文中调用 [WidgetTester.pumpWidget]）之前，此值将为 false。

### performReassemble()

```dart
Future<void> performReassemble()
```

### computePlatformResolvedLocale()

```dart
Locale? computePlatformResolvedLocale(List<Locale> supportedLocales)
```

计算当前平台会解析得到的语言区域。

此方法旨在作为 [WidgetsApp.localeListResolutionCallback] 的一部分使用。由于此方法可能返回 null，因此仍应提供一个 Flutter/Dart 算法作为后备方案，以应对无法确定本机解析语言区域，或本机解析出的语言区域不理想的情况。

如果平台不支持本机语言区域解析，或解析失败，此方法可能返回 null 的 [Locale](https://www.yuque.com/thyname/dart.ui/locale)。

第一个 `supportedLocale` 被视为默认语言区域，如果找不到更好的匹配项，将返回该语言区域。

目前支持 Android 和 iOS。

在 Android 上，使用 https://developer.android.com/guide/topics/resources/multilingual-support 中描述的算法来确定解析后的语言区域。根据设备的 Android 版本，将使用现代（>= API 24）或传统（< API 24）算法。

在 iOS 上，返回 `NSBundle` 的 `preferredLocalizationsFromArray` 方法的结果。有关所用方法的详情，参见：https://developer.apple.com/documentation/foundation/nsbundle/1417249-preferredlocalizationsfromarray?language=objc 。

iOS 将脚本代码视为匹配所必需的，因此用户偏好的语言区域 `zh_Hans_CN` 不会解析为受支持的语言区域 `zh_CN`。

由于不同平台的实现可能不同，且有潜在的较大开销，如果该值会被多次使用，建议缓存此方法的结果。

应通过再次调用此方法，并从 `supportedLocales` 中省略第一次调用已匹配的语言区域，来获取次优（以及第 n 优）匹配的语言区域。

### windowingOwner

```dart
WindowingOwner get windowingOwner
```

[WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner) 负责创建和管理 [BaseWindowController](https://www.yuque.com/thyname/flutter.widgets/basewindowcontroller)。

默认的 [WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner) 支持 macOS、Linux 和 Windows。

可以通过设置器提供自定义的 [WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner)。

{@template flutter.widgets.binding.window.experimental} 请勿在生产应用程序或发布到 pub.dev 的包中使用此 API。即使在补丁版本中，Flutter 也会对此 API 进行破坏性变更。

除非通过 [isWindowingEnabled](https://www.yuque.com/thyname/flutter.foundation/iswindowingenabled) 启用了 Flutter 的窗口化特性，否则此 API 会抛出 [UnsupportedError](https://www.yuque.com/thyname/dart.core/unsupportederror) 错误。

参见：https://github.com/flutter/flutter/issues/30701 。 {@endtemplate}

### windowingOwner

```dart
set windowingOwner(WindowingOwner owner)
```

设置 [WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner)。

默认的 [WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner) 支持 macOS、Linux 和 Windows。

此设置器可用于提供自定义的 [WindowingOwner](https://www.yuque.com/thyname/flutter.widgets/windowingowner)。

{@macro flutter.widgets.binding.window.experimental}

# runApp()

```dart
void runApp(Widget app)
```

填充（inflate）给定的组件并将其附加到视图上。

[runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 方法通过将提供的 `app` 组件包装在一个 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件中，将其渲染到 [PlatformDispatcher.implicitView] 中，该 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件将引导应用程序的渲染树。想要控制应用渲染到哪个 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的应用，可以改用 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget)。

在布局期间，会给该组件施加约束，强制其填满整个视图。如果希望将组件对齐到视图的某一侧（例如顶部），可以考虑使用 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 组件。如果希望将组件居中，也可以使用 [Center](https://www.yuque.com/thyname/flutter.widgets/center) 组件。

再次调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 会将先前的根组件从视图上分离，并将给定的组件附加到其位置。新的组件树会与先前的组件树进行比较，任何差异都会应用到底层渲染树，这与 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 在调用 [State.setState] 后重建时发生的情况类似。

如有必要，使用 [WidgetsFlutterBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsflutterbinding) 初始化绑定。

{@template flutter.widgets.runApp.shutdown}

## 应用程序关闭

由于无法预测应用程序何时会关闭，因此在应用程序关闭时，此组件树不会被拆除。例如，用户可能会物理断开设备电源，应用程序可能会意外崩溃，或者设备上的恶意软件可能会强制终止该进程。

应用程序应负责确保即使面对快速的、计划外的终止，也能保持良好的行为。

要监听平台关闭消息（以及其他生命周期变化），可以考虑使用 [AppLifecycleListener](https://www.yuque.com/thyname/flutter.widgets/applifecyclelistener) API。 {@endtemplate}

若要人为地使整个组件树被释放，可以考虑使用诸如 [SizedBox.shrink] 之类的组件调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)。

{@template flutter.widgets.runApp.dismissal}

## 通过平台原生方法关闭 Flutter UI

一个应用程序中可能同时包含 Flutter 和非 Flutter UI。如果应用程序调用非 Flutter 方法来移除基于 Flutter 的 UI，例如使用平台原生 API 来操作平台原生导航栈，框架无法知道开发者是否打算尽早释放资源。组件树仍会保持挂载状态，随时准备在再次显示时进行渲染。{@endtemplate}

若要更早地释放资源，可以建立一个[平台通道](https://flutter.dev/to/platform-channels)，并在框架应释放活动组件树时使用它调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)，传入诸如 [SizedBox.shrink] 之类的组件。

另请参阅：

- [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget)，它引导一棵组件树，而无需假定其将被渲染到哪个 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 中。
- [WidgetsBinding.attachRootWidget]，它为组件层次结构创建根组件。
- [RenderObjectToWidgetAdapter.attachToRenderTree]，它为 Element 层次结构创建根 Element。
- [WidgetsBinding.handleBeginFrame]，它驱动组件流水线，以确保组件树、Element 树和渲染树都已构建完成。

# runWidget()

```dart
void runWidget(Widget app)
```

填充（inflate）给定的组件并引导组件树。

与 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 不同，此方法不定义所提供的 `app` 组件将被渲染到的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。调用者需要在提供的 `app` 组件中至少包含一个 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件，用于引导一棵渲染树并定义渲染内容所使用的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。没有祖先 [View](https://www.yuque.com/thyname/flutter.widgets/view) 组件的 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 会导致异常。想要在无需处理视图管理的情况下渲染到默认视图的应用，可以考虑改为调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)。

{@tool snippet} 该示例展示了如何利用 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget) 指定要将 `MyApp` 组件绘制到哪个 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 中：

```dart
runWidget(
  View(
    view: myFlutterView,
    child: const MyApp(),
  ),
);
```

{@end-tool}

再次调用 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget) 会分离先前的根组件，并将给定的组件附加到其位置。新的组件树会与先前的组件树进行比较，任何差异都会应用到底层渲染树，这与 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 在调用 [State.setState] 后重建时发生的情况类似。

如有必要，使用 [WidgetsFlutterBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsflutterbinding) 初始化绑定。

{@macro flutter.widgets.runApp.shutdown}

若要人为地使整个组件树被释放，可以考虑使用未指定任何 [ViewCollection.views] 的 [ViewCollection](https://www.yuque.com/thyname/flutter.widgets/viewcollection) 调用 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget)。

{@macro flutter.widgets.runApp.dismissal}

若要更早地释放资源，可以建立一个[平台通道](https://flutter.dev/to/platform-channels)，用于从提供给 [runWidget](https://www.yuque.com/thyname/flutter.widgets/runwidget) 的 `app` 组件树中移除应释放其组件资源的 [View](https://www.yuque.com/thyname/flutter.widgets/view)。

另请参阅：

- [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp)，它引导一棵组件树并将其渲染到默认的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 中。
- [WidgetsBinding.attachRootWidget]，它为组件层次结构创建根组件。
- [RenderObjectToWidgetAdapter.attachToRenderTree]，它为 Element 层次结构创建根 Element。
- [WidgetsBinding.handleBeginFrame]，它驱动组件流水线，以确保组件树、Element 树和渲染树都已构建完成。

# debugDumpApp()

```dart
void debugDumpApp()
```

打印当前正在运行的应用程序的字符串表示形式。

# RootWidget

```dart
class RootWidget extends Widget {}
```

用于组件树根部的组件。

暴露了一个 [attach] 方法，用于将组件树附加到 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)。该方法还会引导 Element 树。

由 [WidgetsBinding.attachRootWidget]（间接由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 调用）使用，以引导应用程序。

### RootWidget()

```dart
RootWidget({dynamic key, Widget? child, String? debugShortDescription})
```

创建一个 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget)。

### child

```dart
Widget? child
```

此组件下方组件树中的组件。

{@macro flutter.widgets.ProxyWidget.child}

### debugShortDescription

```dart
String? debugShortDescription
```

调试辅助工具使用的该组件的简短描述。

### createElement()

```dart
RootElement createElement()
```

### attach()

```dart
RootElement attach(BuildOwner owner, [RootElement? element])
```

填充此组件并将其附加到提供的 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner)。

如果 `element` 为 null，此函数会创建一个新的 Element。否则，将为给定的 Element 调度一次更新，以切换到此组件。

由 [WidgetsBinding.attachToBuildOwner]（间接由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 调用）使用，以引导应用程序。

### toStringShort()

```dart
String toStringShort()
```

# RootElement

```dart
class RootElement extends Element with RootElementMixin {}
```

Element 树的根节点。

此 Element 类是 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 的实例化结果。它只能用作 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树的根节点（不能被挂载到另一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 中；其父节点必须为 null）。

在典型用法中，它会通过调用 [RootWidget.attach] 为某个 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 实例化。在此用法中，它通常由 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 创建的 [WidgetsFlutterBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsflutterbinding) 单例中的引导逻辑实例化。

### RootElement()

```dart
RootElement(RootWidget widget)
```

为提供的 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 创建一个 [RootElement](https://www.yuque.com/thyname/flutter.widgets/rootelement)。

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(RootWidget newWidget)
```

### performRebuild()

```dart
void performRebuild()
```

### debugDoingBuild

```dart
bool get debugDoingBuild
```

### debugExpectsRenderObjectForSlot()

```dart
bool debugExpectsRenderObjectForSlot(Object? slot)
```

# WidgetsFlutterBinding

```dart
class WidgetsFlutterBinding extends BindingBase with GestureBinding, SchedulerBinding, ServicesBinding, PaintingBinding, SemanticsBinding, RendererBinding, WidgetsBinding {}
```

基于组件框架的应用程序所使用的具体绑定。

这是将框架绑定到 Flutter 引擎的粘合层。

使用组件框架时，必须使用此绑定，或实现相同接口的绑定。以下混入用于实现此绑定：

- [GestureBinding](https://www.yuque.com/thyname/flutter.gestures/gesturebinding)，实现命中测试（hit testing）的基础功能。
- [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)，引入了帧的概念。
- [ServicesBinding](https://www.yuque.com/thyname/flutter.services/servicesbinding)，提供对插件子系统的访问。
- [PaintingBinding](https://www.yuque.com/thyname/flutter.painting/paintingbinding)，支持图像解码。
- [SemanticsBinding](https://www.yuque.com/thyname/flutter.semantics/semanticsbinding)，支持无障碍功能。
- [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding)，处理渲染树。
- [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding)，处理组件树。

### ensureInitialized()

```dart
WidgetsBinding ensureInitialized()
```

返回一个实现了 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 的绑定实例。如果尚未初始化任何绑定，则使用 [WidgetsFlutterBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsflutterbinding) 类来创建并初始化一个绑定实例。

只有在需要绑定于调用 [runApp](https://www.yuque.com/thyname/flutter.widgets/runapp) 之前完成初始化时，才需要调用此方法。

在 `flutter_test` 框架中，[testWidgets] 会将绑定实例初始化为 [TestWidgetsFlutterBinding]，而非 [WidgetsFlutterBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsflutterbinding)。参见 [TestWidgetsFlutterBinding.ensureInitialized]。
