@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'form.dart'; @docImport 'pages.dart'; @docImport 'pop_scope.dart'; @docImport 'router.dart'; @docImport 'will_pop_scope.dart';

# RouteFactory

```dart
typedef RouteFactory = Route<dynamic>? Function(RouteSettings settings)
```

根据给定的路由设置创建一个路由。

由 [Navigator.onGenerateRoute] 使用。

另请参阅：

- [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，所有的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 最终都会归属于它。

# RouteListFactory

```dart
typedef RouteListFactory = List<Route<dynamic>> Function(NavigatorState navigator, String initialRoute)
```

创建一个或多个路由组成的序列。

由 [Navigator.onGenerateInitialRoutes] 使用。

# RestorableRouteBuilder

```dart
typedef RestorableRouteBuilder<T> = Route<T> Function(BuildContext context, Object? arguments)
```

创建一个待添加到 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)。

可以使用提供的 `arguments` 对路由进行配置。提供的 `context` 是该路由将被添加到的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 `BuildContext`。

由 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中用于添加匿名路由的可恢复方法使用（例如 [NavigatorState.restorablePush]）。在这种用例下，[RestorableRouteBuilder](https://www.yuque.com/thyname/flutter.widgets/restorableroutebuilder) 必须是一个使用 `@pragma('vm:entry-point')` 注解的静态函数。[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会在状态恢复期间再次调用它，以重新创建该路由。

# RoutePredicate

```dart
typedef RoutePredicate = bool Function(Route<dynamic> route)
```

[Navigator.popUntil] 谓词参数的签名。

# WillPopCallback

```dart
typedef WillPopCallback = Future<bool> Function()
```

用于验证是否可以调用 [Navigator.pop] 的回调的签名。

由 [Form.onWillPop]、[ModalRoute.addScopedWillPopCallback]、[ModalRoute.removeScopedWillPopCallback] 和 [WillPopScope](https://www.yuque.com/thyname/flutter.widgets/willpopscope) 使用。

# PopPageCallback

```dart
typedef PopPageCallback = bool Function(Route<dynamic> route, dynamic result)
```

[Navigator.onPopPage] 回调的签名。

此回调必须对指定的路由调用 [Route.didPop]，并且必须在下次传入 [Navigator.pages] 时正确更新页面列表，使其不再包含对应的 [Page](https://www.yuque.com/thyname/flutter.widgets/page)。（否则，当 [Navigator.pages] 列表下次更新时，该页面将被视为一个需要显示的新页面。）

# DidRemovePageCallback

```dart
typedef DidRemovePageCallback = void Function(Page<Object?> page)
```

[Navigator.onDidRemovePage] 回调的签名。

此回调必须在下次传入 [Navigator.pages] 时正确更新页面列表，使其不再包含输入的 `page`。（否则，当 [Navigator.pages] 列表下次更新时，该页面将被视为一个需要显示的新页面。）

# RoutePopDisposition

```dart
enum RoutePopDisposition {}
```

指示当前路由是否应该被弹出。

用作 [Route.willPop] 的返回值。

另请参阅：

- [WillPopScope](https://www.yuque.com/thyname/flutter.widgets/willpopscope)，一个接入路由 [Route.willPop] 机制的组件。

弹出该路由。

如果 [Route.willPop] 或 [Route.popDisposition] 返回 [pop]，返回按钮将会真正弹出当前路由。

不弹出该路由。

如果 [Route.willPop] 或 [Route.popDisposition] 返回 [doNotPop]，返回按钮将被忽略。

将其委托给下一级导航处理。

如果 [Route.willPop] 或 [Route.popDisposition] 返回 [bubble]，返回按钮将由 [SystemNavigator](https://www.yuque.com/thyname/flutter.services/systemnavigator) 处理，这通常会关闭应用程序。

# Route

```dart
abstract class Route<T> extends _RoutePlaceholder {}
```

由 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 管理的条目的一种抽象。

该类定义了导航器与被压入及弹出导航器的“路由”之间的抽象接口。大多数路由都具有可视化的表现形式，它们会使用一个或多个 [OverlayEntry](https://www.yuque.com/thyname/flutter.widgets/overlayentry) 对象将其放置在导航器的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中。

有关如何在导航中使用 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的更多说明（包括代码示例），请参阅 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。

有关使用平台自适应过渡效果替换整个屏幕的路由，请参阅 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute)。

如果 [settings] 是 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的子类，则该路由可以归属于某个页面。与无页面路由相对，基于页面的路由是在 [Navigator.pages] 更新期间通过 [Page.createRoute] 创建的。与此路由关联的页面可能会在路由的生命周期内发生变化。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 更新了此路由的页面，它会调用 [changedInternalState] 来通知路由该页面已被更新。

类型参数 `T` 是路由的返回类型，被 [currentResult]、[popped] 和 [didPop] 使用。如果该路由不返回任何值，可以使用 `void` 类型。

### Route()

```dart
Route({RouteSettings? settings, bool? requestFocus})
```

初始化 [Route](https://www.yuque.com/thyname/flutter.widgets/route)。

如果未提供 [settings]，则会改用一个空的 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings) 对象。

{@template flutter.widgets.navigator.Route.requestFocus} 如果未提供 [requestFocus]，则会改用 [Navigator.requestFocus] 的值。{@endtemplate}

### requestFocus

```dart
bool get requestFocus
```

当路由状态更新时，如果当前路由处于顶部，则请求获得焦点。

如果在构造函数中未提供该值，则会改用 [Navigator.requestFocus]。

### navigator

```dart
NavigatorState? get navigator
```

该路由所在的导航器（如果存在的话）。

### settings

```dart
RouteSettings get settings
```

此路由的设置。

详见 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings)。

设置可以在路由的生命周期内发生变化。如果设置发生变化，路由的覆盖层将被标记为脏（见 [changedInternalState]）。

如果该路由是根据 [Navigator.pages] 列表中的某个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 创建的，那么此值将是一个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 子类，并且每当 [Navigator.pages] 中对应的 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 发生变化时，它都会被更新。一旦该 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 从历史记录中移除，此值将停止更新（并保留其最后的值）。

### restorationScopeId

```dart
ValueListenable<String?> get restorationScopeId
```

用于包围此路由的 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope) 的恢复作用域 ID。

如果此路由当前禁用了恢复功能，则恢复作用域 ID 为 null。

如果恢复作用域 ID 在路由的生命周期内发生变化（例如因为启用或禁用了恢复功能），[ValueListenable](https://www.yuque.com/thyname/flutter.foundation/valuelistenable) 会通知其监听器。例如，当路由正在过渡离开屏幕时，该 ID 会变为 null，这将触发此字段上的通知。此时，出于恢复目的，该路由被视为已不再存在，其状态将不会被恢复。

### overlayEntries

```dart
List<OverlayEntry> get overlayEntries
```

此路由的覆盖层条目。

这些条目通常由 [install] 填充。[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 负责将它们添加到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中或从中移除。

在调用 [install] 之后，此列表中必须至少有一个条目。

如果路由在历史记录中被移动，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会负责将这些条目保持在一起。

### install()

```dart
void install()
```

当路由被插入导航器时调用。

利用此方法来填充 [overlayEntries]。调用 [install] 之后，此列表中必须至少有一个条目。[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 将负责通过调用 [OverlayEntry.remove] 把它们添加到 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中或从中移除。

### didPush()

```dart
TickerFuture didPush()
```

当路由被压入导航器时，在 [install] 之后调用。

返回值会在压入过渡完成时解析完成。

当路由无需任何压入过渡而立即出现在屏幕上时，将调用 [didAdd] 方法而非 [didPush]。

通常在调用此方法之后会立即调用 [didChangeNext] 和 [didChangePrevious] 方法。

### didAdd()

```dart
void didAdd()
```

当路由被添加到导航器时，在 [install] 之后调用。

当路由无需任何压入过渡而立即出现在屏幕上时，将调用此方法而非 [didPush]。

通常在调用此方法之后会立即调用 [didChangeNext] 和 [didChangePrevious] 方法。

### didReplace()

```dart
void didReplace(Route<dynamic>? oldRoute)
```

当路由在导航器中替换了另一个路由时，在 [install] 之后调用。

通常在调用此方法之后会立即调用 [didChangeNext] 和 [didChangePrevious] 方法。

### willPop()

```dart
Future<RoutePopDisposition> willPop()
```

返回当此 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 为当前路由（[isCurrent]）时，调用 [Navigator.maybePop] 是否应该产生任何效果。

[Navigator.maybePop] 通常用于替代 [Navigator.pop] 来处理系统返回按钮。

默认情况下，如果某个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 是历史记录中的第一个路由（即 [isFirst] 为真），它会报告弹出操作应该被冒泡（[RoutePopDisposition.bubble]）。这一行为可以防止用户将历史记录中的第一个路由弹出而滞留在空白屏幕上；取而代之的是弹出更大的作用域（例如应用程序退出，使用户返回到上一个应用程序）。

在其他情况下，默认行为是接受弹出操作（[RoutePopDisposition.pop]）。

第三种可能的值是 [RoutePopDisposition.doNotPop]，它会导致弹出请求被完全忽略。

另请参阅：

- [Form](https://www.yuque.com/thyname/flutter.widgets/form)，它提供了一个使用此机制的 [Form.onWillPop] 回调。
- [WillPopScope](https://www.yuque.com/thyname/flutter.widgets/willpopscope)，另一个提供拦截返回按钮方式的组件。

### popDisposition

```dart
RoutePopDisposition get popDisposition
```

返回当此 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 为当前路由（[isCurrent]）时，调用 [Navigator.maybePop] 是否应该产生任何效果。

在尚未通过 [SystemNavigator.setFrameworkHandlesBack] 禁用的情况下，[Navigator.maybePop] 通常用于替代 [Navigator.pop] 来处理系统返回按钮。

默认情况下，如果某个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 是历史记录中的第一个路由（即 [isFirst] 为真），它会报告弹出操作应该被冒泡（[RoutePopDisposition.bubble]）。这一行为可以防止用户将历史记录中的第一个路由弹出而滞留在空白屏幕上；取而代之的是弹出更大的作用域（例如应用程序退出，使用户返回到上一个应用程序）。

在其他情况下，默认行为是接受弹出操作（[RoutePopDisposition.pop]）。

第三种可能的值是 [RoutePopDisposition.doNotPop]，它会导致弹出请求被完全忽略。

另请参阅：

- [Form](https://www.yuque.com/thyname/flutter.widgets/form)，它提供了一个类似的 [Form.canPop] 布尔值。
- [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope)，一个提供拦截返回按钮方式的组件。
- [Page.canPop]，[Page](https://www.yuque.com/thyname/flutter.widgets/page) 影响此属性的一种方式。

### onPopInvoked()

```dart
void onPopInvoked(bool didPop)
```

在路由弹出被处理之后调用。

即使弹出操作被取消（例如被 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope) 组件取消），此方法仍然会被调用。`didPop` 参数指示返回导航是否真正成功发生。

### onPopInvokedWithResult()

```dart
void onPopInvokedWithResult(bool didPop, T? result)
```

{@template flutter.widgets.navigator.onPopInvokedWithResult} 在路由弹出被处理之后调用。

即使弹出操作被取消（例如被 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope) 组件取消），此方法仍然会被调用。`didPop` 参数指示返回导航是否真正成功发生。{@endtemplate}

### willHandlePopInternally

```dart
bool get willHandlePopInternally
```

调用 [didPop] 是否会返回 false。

### currentResult

```dart
T? get currentResult
```

当此路由被弹出时（见 [Navigator.pop]），如果未指定结果或结果为 null，则会改用此值。

这一后备机制由 [didComplete] 实现。如果传给该方法的参数为 null，则会使用此值。

### popped

```dart
Future<T?> get popped
```

一个在此路由从导航器弹出时完成的 future。

该 future 会以传给 [Navigator.pop] 的值（如果有的话）完成，否则以 [currentResult] 的值完成。有关此主题的更多讨论，请参阅 [didComplete]。

### didPop()

```dart
bool didPop(T? result)
```

发起了一个弹出此路由的请求。如果该路由可以在内部处理此请求（例如因为它拥有自己的内部状态堆栈），则返回 false，否则返回 true（通过返回调用 `super.didPop` 的值）。返回 false 将阻止 [NavigatorState.pop] 的默认行为。

当此函数返回 true 时，导航器会将此路由从历史记录中移除，但尚不会调用 [dispose]。相反，由该路由自己负责调用 [NavigatorState.finalizeRoute]，后者会转而对该路由调用 [dispose]。这一顺序使得路由能够在被弹出之后、被释放之前执行退出动画（或其他一些视觉效果）。

此方法应调用 [didComplete] 来解析 [popped] future（默认实现也仅执行此操作）；路由不应等待其退出动画完成后再执行此操作。

有关 `result` 参数的讨论，请参阅 [popped]、[didComplete] 和 [currentResult]。

### didComplete()

```dart
void didComplete(T? result)
```

该路由已被弹出，或者以某种较为平和的方式被移除。

此方法由 [didPop] 调用，也会在响应 [NavigatorState.pushReplacement] 时被调用。如果没有调用 [didPop]，那么必须立即调用 [NavigatorState.finalizeRoute] 方法，并且不会运行退出动画。

此方法会完成 [popped] future。`result` 参数指定了该 future 完成时使用的值，除非该值为 null，此时会改用 [currentResult]。

此方法应在弹出动画（如果有的话）发生之前被调用，尽管在某些情况下，动画可能会在路由被确定弹出之前由用户驱动；这种情况尤其可能发生在 iOS 风格的返回手势中。请参阅 [NavigatorState.didStartUserGesture]。

### didPopNext()

```dart
void didPopNext(Route<dynamic> nextRoute)
```

位于此路由之上的给定路由已从导航器中弹出。

此路由现在是当前路由（[isCurrent] 现在为真），并且不存在下一个路由。

### didChangeNext()

```dart
void didChangeNext(Route<dynamic>? nextRoute)
```

此路由的下一个路由已变更为给定的新路由。

只要路由处于历史记录中，无论出于何种原因，只要下一个路由发生变化，就会在该路由上调用此方法，包括路由首次被添加到 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 时（例如通过 [Navigator.push]），但会调用 [didPopNext] 的情况除外。

如果不存在新的下一个路由（即 [isCurrent] 为真），则 `nextRoute` 参数将为 null。

### didChangePrevious()

```dart
void didChangePrevious(Route<dynamic>? previousRoute)
```

此路由的上一个路由已变更为给定的新路由。

只要路由处于历史记录中，无论出于何种原因，只要上一个路由发生变化，就会在该路由上调用此方法，但该路由自身刚被压入之后的情况除外（此时会改为调用 [didPush] 或 [didReplace]）。

如果不存在上一个路由（即 [isFirst] 为真），则 `previousRoute` 参数将为 null。

### changedInternalState()

```dart
void changedInternalState()
```

每当路由的内部状态发生变化时调用。

每当 [willHandlePopInternally]、[didPop]、[ModalRoute.offstage] 或路由的其他内部状态改变了值时，都应调用此方法。例如，[ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 会使用此方法，通过其继承组件将新信息报告给该路由的任何子组件。

另请参阅：

- [changedExternalState]，当 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 以某种可能影响路由的方式更新时被调用。

### changedExternalState()

```dart
void changedExternalState()
```

每当 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 以某种可能影响路由的方式更新时调用，以表明该路由可能也需要重建。

每当 [NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate) 的 [State.widget] 发生变化时（如同 [State.didUpdateWidget] 中那样），例如因为 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 已被重建，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 就会调用此方法。这确保了直接引用构建 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 的组件状态的路由，会在该组件重建时收到通知，因为否则很难通知这些路由它们所依赖的状态可能已经改变。

每当 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的依赖项发生变化时（如同 [State.didChangeDependencies] 中那样），也会调用此方法。这使得路由能够使用 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的上下文（[NavigatorState.context]），例如在 [ModalRoute.barrierColor] 中，并相应地进行更新。

[ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 子类重写了此方法，以强制屏障覆盖层重建。

另请参阅：

- [changedInternalState]，与此等效，但针对路由内部状态的变化。

### dispose()

```dart
void dispose()
```

释放该对象所使用的任何资源。

此方法不应将其 [overlayEntries] 从 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中移除。这项工作由该对象的所有者负责。

调用此方法之后，该对象将不再处于可用状态，应当被丢弃。

此方法只应由该对象的所有者调用；通常 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有某个路由，因此会在该路由被移除时调用此方法，此后该路由将不再被导航器引用。

### isCurrent

```dart
bool get isCurrent
```

此路由是否为导航器上的最顶层路由。

如果此值为真，则 [isActive] 也为真。

### isFirst

```dart
bool get isFirst
```

此路由是否为导航器上最底层的活动路由。

如果 [isFirst] 和 [isCurrent] 均为真，则此路由是导航器上唯一的路由（并且 [isActive] 也将为真）。

### hasActiveRouteBelow

```dart
bool get hasActiveRouteBelow
```

此路由之下是否存在至少一个活动路由。

### isActive

```dart
bool get isActive
```

此路由是否位于导航器上。

如果该路由不仅是活动的，而且还是当前路由（最顶层的路由），则 [isCurrent] 也将为真。如果它是第一个路由（最底层的路由），则 [isFirst] 也将为真。

如果位于其上方的某个路由完全不透明，那么此路由虽然处于活动状态，但不会被渲染。甚至有可能出现路由处于活动状态、但其内部的有状态组件尚未被实例化的情况。请参阅 [ModalRoute.maintainState]。

# RouteSettings

```dart
class RouteSettings {}
```

在构造 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 时可能有用的数据。

### RouteSettings()

```dart
RouteSettings({String? name, Object? arguments})
```

创建用于构造路由的数据。

### name

```dart
String? name
```

路由的名称（例如 "/settings"）。

如果为 null，则该路由是匿名的。

### arguments

```dart
Object? arguments
```

传递给此路由的参数。

可以在构建路由时使用，例如在 [Navigator.onGenerateRoute] 中。

### toString()

```dart
String toString()
```

# Page

```dart
abstract class Page<T> extends RouteSettings {}
```

描述 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的配置。

类型参数 `T` 是对应 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的返回类型，被 [Route.currentResult]、[Route.popped] 和 [Route.didPop] 使用。

[canPop] 和 [onPopInvoked] 用于拦截弹出操作。

{@tool dartpad} 此示例演示了如何使用 [canPop] 和 [onPopInvoked] 来拦截弹出操作。

** See code in examples/api/lib/widgets/page/page_can_pop.0.dart ** {@end-tool}

另请参阅：

- [Navigator.pages]，它接受一个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 列表并更新其路由历史记录。

### Page()

```dart
Page({LocalKey? key, String? name, Object? arguments, String? restorationId, bool canPop = true, PopInvokedWithResultCallback<T> onPopInvoked = _defaultPopInvokedHandler})
```

创建一个页面，并为子类初始化 [key]。

### key

```dart
LocalKey? key
```

与此页面关联的键。

此键将用于在 [canUpdate] 中比较页面。

### restorationId

```dart
String? restorationId
```

用于保存和恢复由此页面配置的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的状态的恢复 ID。

如果未提供恢复 ID，则该 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不会恢复其状态。

另请参阅：

- [RestorationManager](https://www.yuque.com/thyname/flutter.services/restorationmanager)，其中解释了状态恢复在 Flutter 中的工作原理。

### onPopInvoked

```dart
PopInvokedWithResultCallback<T> onPopInvoked
```

在关联路由上的弹出操作被处理之后调用。

在调用此方法时，已经无法阻止弹出操作的发生；弹出操作已经发生了。请使用 [canPop] 来提前禁用弹出操作。

即使弹出操作被取消，此方法仍然会被调用。当关联的 [Route.popDisposition] 返回 false，或者 [canPop] 被设为 false 时，弹出操作会被取消。`didPop` 参数指示返回导航是否真正成功发生。

### canPop

```dart
bool canPop
```

当此值为 false 时，阻止关联的路由被弹出。

如果将 Navigator 中第一个页面的此值设为 false，则会阻止 Flutter 应用退出。

如果某个路由的组件子树中存在任何 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope) 组件，除了此 canPop 之外，它们各自的 `canPop` 也必须为 `true`，该路由才能够被弹出。

### canUpdate()

```dart
bool canUpdate(Page<dynamic> other)
```

此页面是否可以使用 [other] 页面进行更新。

如果两个页面具有相同的 [runtimeType] 和 [key]，则认为它们是可更新的。

### createRoute()

```dart
Route<T> createRoute(BuildContext context)
```

创建与此页面对应的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)。

创建出的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 必须将其 [Route.settings] 属性设置为此 [Page](https://www.yuque.com/thyname/flutter.widgets/page)。

### toString()

```dart
String toString()
```

# NavigatorObserver

```dart
class NavigatorObserver {}
```

用于观察 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 行为的接口。

### navigator

```dart
NavigatorState? get navigator
```

该观察者正在观察的导航器（如果存在的话）。

### didPush()

```dart
void didPush(Route<dynamic> route, Route<dynamic>? previousRoute)
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 压入了 `route`。

紧邻其下方的路由（即先前活动的路由）是 `previousRoute`。

### didPop()

```dart
void didPop(Route<dynamic> route, Route<dynamic>? previousRoute)
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 弹出了 `route`。

紧邻其下方的路由（即新的活动路由）是 `previousRoute`。

### didRemove()

```dart
void didRemove(Route<dynamic> route, Route<dynamic>? previousRoute)
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 移除了 `route`。

如果只移除一个路由，则紧邻其下方的路由（如果存在）即为 `previousRoute`。

如果同时移除多个路由，则位于被移除的最底层路由下方的路由（如果存在）即为 `previousRoute`，并且此方法会针对每个被移除的路由调用一次，顺序从最顶层路由到最底层路由。

### didReplace()

```dart
void didReplace({Route<dynamic>? newRoute, Route<dynamic>? oldRoute})
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 用 `newRoute` 替换了 `oldRoute`。

### didChangeTop()

```dart
void didChangeTop(Route<dynamic> topRoute, Route<dynamic>? previousTopRoute)
```

最顶层的路由已发生变化。

`topRoute` 是新的最顶层路由。它可以是新压入屏幕顶部的路由，也可以是因为先前最顶层的路由已被弹出而成为新最顶层路由的现有路由。

`previousTopRoute` 是变化之前的最顶层路由。它可以是已从屏幕上弹出的路由，也可以是将被 `topRoute` 覆盖的路由。如果这是首次构建，此值也可以为 null。

### didStartUserGesture()

```dart
void didStartUserGesture(Route<dynamic> route, Route<dynamic>? previousRoute)
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的路由正在被用户手势移动。

例如，此方法会在 iOS 返回手势开始时被调用，用于在此类交互期间禁用 Hero 动画。

### didStopUserGesture()

```dart
void didStopUserGesture()
```

用户手势不再控制 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。

与之前对 [didStartUserGesture] 的调用相配对。

# HeroControllerScope

```dart
class HeroControllerScope extends InheritedWidget {}
```

用于承载 Hero 控制器的继承组件。

被承载的 Hero 控制器将被 [child] 子树中的导航器获取。一旦某个导航器获取了此控制器，该导航器将阻止其子树下的任何导航器接收此控制器。

[HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 内部的 Hero 控制器一次只能订阅一个导航器。如果该 Hero 控制器订阅了多个导航器，将会抛出断言错误。当同一 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 下并行存在多个导航器时，可能会发生这种情况。

### HeroControllerScope()

```dart
HeroControllerScope({dynamic key, required HeroController? controller, required Widget child})
```

创建一个用于承载输入的 [controller] 的组件。

### HeroControllerScope.none()

```dart
HeroControllerScope.none({dynamic key, required Widget child})
```

创建一个组件，以阻止子树接收上方的 Hero 控制器。

### controller

```dart
HeroController? controller
```

承载在此组件内部的 Hero 控制器。

### maybeOf()

```dart
HeroController? maybeOf(BuildContext context)
```

从最近的 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 祖先组件中获取 [HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller)，如果不存在则返回 null。

如果 [context] 中存在最近的 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope)，调用此方法将会对其建立依赖关系。

另请参阅：

- [HeroControllerScope.of]，与此方法类似，但在找不到 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 祖先组件时会触发断言。

### of()

```dart
HeroController of(BuildContext context)
```

从最近的 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 祖先组件中获取 [HeroController](https://www.yuque.com/thyname/flutter.widgets/herocontroller)。

如果找不到祖先组件，此方法将在调试模式下触发断言，在发布模式下抛出异常。

调用此方法将会对 [context] 中最近的 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 建立依赖关系。

另请参阅：

- [HeroControllerScope.maybeOf]，与此方法类似，但在找不到 [HeroControllerScope](https://www.yuque.com/thyname/flutter.widgets/herocontrollerscope) 祖先组件时返回 null。

### updateShouldNotify()

```dart
bool updateShouldNotify(HeroControllerScope oldWidget)
```

# RouteTransitionRecord

```dart
abstract class RouteTransitionRecord {}
```

一个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 包装接口，可以被暂存以供 [TransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/transitiondelegate) 决定其底层 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 应如何过渡进入或离开屏幕。

### route

```dart
Route<dynamic> get route
```

获取被包装的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)。

### isWaitingForEnteringDecision

```dart
bool get isWaitingForEnteringDecision
```

此路由是否正在等待关于如何进入屏幕的决策。

如果此属性为真，则此路由需要一个关于如何过渡进入屏幕的明确决策。此决策应在 [TransitionDelegate.resolve] 中做出。

### isWaitingForExitingDecision

```dart
bool get isWaitingForExitingDecision
```

此路由是否正在等待关于如何离开屏幕的决策。

如果此属性为真，则此路由需要一个关于如何过渡离开屏幕的明确决策。此决策应在 [TransitionDelegate.resolve] 中做出。

### markForPush()

```dart
void markForPush()
```

将 [route] 标记为需要带过渡效果地压入。

在 [TransitionDelegate.resolve] 期间，可以对一个进入中的路由（[RouteTransitionRecord.isWaitingForEnteringDecision] 为真）调用此方法，以表明该路由应带有动画过渡地压入 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。

### markForAdd()

```dart
void markForAdd()
```

将 [route] 标记为无需过渡效果地添加。

在 [TransitionDelegate.resolve] 期间，可以对一个进入中的路由（[RouteTransitionRecord.isWaitingForEnteringDecision] 为真）调用此方法，以表明该路由应无动画过渡地添加到 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。

### markForPop()

```dart
void markForPop([dynamic result])
```

将 [route] 标记为需要带过渡效果地弹出。

在 [TransitionDelegate.resolve] 期间，可以对一个退出中的路由调用此方法，以表明该路由应带有动画过渡地从 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 弹出。

### markForComplete()

```dart
void markForComplete([dynamic result])
```

将 [route] 标记为无需过渡效果地完成。

在 [TransitionDelegate.resolve] 期间，可以对一个退出中的路由调用此方法，以表明该路由应以提供的结果完成，并无动画过渡地从 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 移除。

### markForRemove()

```dart
void markForRemove()
```

将 [route] 标记为无需过渡效果地移除。

在 [TransitionDelegate.resolve] 期间，可以对一个退出中的路由调用此方法，以表明该路由应无需完成、也无需动画过渡地从 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 中移除。

# TransitionDelegate

```dart
abstract class TransitionDelegate<T> {}
```

决定从 [Navigator.pages] 中添加和移除的页面应如何过渡进入或离开屏幕的委托。

此抽象类实现了供 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 调用的 API，当它需要就路由如何过渡进入或离开屏幕做出明确决策时会调用该 API。

要做出路由过渡决策，子类必须实现 [resolve]。

{@tool snippet} 以下示例演示了如何实现一个子类，该子类总是无动画过渡地移除或添加路由，并将被移除的路由放置在列表顶部。

```dart
class NoAnimationTransitionDelegate extends TransitionDelegate<void> {
  @override
  Iterable<RouteTransitionRecord> resolve({
    required List<RouteTransitionRecord> newPageRouteHistory,
    required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute,
    required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes,
  }) {
    final List<RouteTransitionRecord> results = <RouteTransitionRecord>[];

    for (final RouteTransitionRecord pageRoute in newPageRouteHistory) {
      if (pageRoute.isWaitingForEnteringDecision) {
        pageRoute.markForAdd();
      }
      results.add(pageRoute);

    }
    for (final RouteTransitionRecord exitingPageRoute in locationToExitingPageRoute.values) {
      if (exitingPageRoute.isWaitingForExitingDecision) {
       exitingPageRoute.markForComplete();
       final List<RouteTransitionRecord>? pagelessRoutes = pageRouteToPagelessRoutes[exitingPageRoute];
       if (pagelessRoutes != null) {
         for (final RouteTransitionRecord pagelessRoute in pagelessRoutes) {
            pagelessRoute.markForComplete();
          }
       }
      }
      results.add(exitingPageRoute);

    }
    return results;
  }
}

```

{@end-tool}

另请参阅：

- [Navigator.transitionDelegate]，它使用此类来做出路由过渡决策。
- [DefaultTransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/defaulttransitiondelegate)，它实现了决定路由如何过渡进入或离开屏幕的默认方式。

### TransitionDelegate()

```dart
TransitionDelegate()
```

创建一个委托，并使子类能够创建常量类。

### resolve()

```dart
Iterable<RouteTransitionRecord> resolve({required List<RouteTransitionRecord> newPageRouteHistory, required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute, required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes})
```

当 [Navigator.pages] 更新时，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会调用此方法来决定路由应如何过渡进入或离开屏幕。

`newPageRouteHistory` 列表包含了所有基于页面的路由，其顺序即为此次更新完成后 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 历史堆栈中的顺序。如果 `newPageRouteHistory` 中的某个路由的 [RouteTransitionRecord.isWaitingForEnteringDecision] 被设为 true，则此路由需要一个关于其应如何过渡进入 Navigator 的明确决策。要做出决策，请调用 [RouteTransitionRecord.markForPush] 或 [RouteTransitionRecord.markForAdd]。

`locationToExitingPageRoute` 包含了在页面更新后从路由历史记录中移除的基于页面的路由。此映射记录了待移除的基于页面的路由，以及该路由在更新前原始路由历史记录中的位置。键是紧邻被移除路由下方的基于页面的路由所表示的位置，值则是待移除的基于页面的路由。如果待移除的路由是最底层的路由，则位置为 null。如果 `locationToExitingPageRoute` 中的某个路由的 [RouteTransitionRecord.isWaitingForExitingDecision] 被设为 true，则此路由需要一个关于其应如何过渡离开 Navigator 的明确决策。要为某个被移除的路由做出决策，请调用 [RouteTransitionRecord.markForPop]、[RouteTransitionRecord.markForComplete]。`locationToExitingPageRoute` 中的路由有可能并不需要决策。如果这些路由已经在先前的页面更新中被弹出，且仍在等待弹出动画完成，就可能发生这种情况。在这种情况下，这些路由仍会被包含在 `locationToExitingPageRoute` 中，其 [RouteTransitionRecord.isWaitingForExitingDecision] 被设为 false，且不需要做出决策。

`pageRouteToPagelessRoutes` 记录了基于页面的路由及其关联的无页面路由。如果某个基于页面的路由正在等待退出决策，其关联的无页面路由也需要就如何过渡离开屏幕做出明确决策。

一旦所有决策都已做出，此方法必须将被移除的路由（无论它们是否需要决策）与 `newPageRouteHistory` 合并，并返回合并后的结果。结果中的顺序即为 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 用于更新路由历史记录的顺序。返回的列表必须保留 `newPageRouteHistory` 中路由的相同顺序。然而，被移除的路由可以自由地插入到返回列表中的任何位置，只要它们全部都被包含在内。

例如，考虑以下情况。

`newPageRouteHistory = [A, B, C]`

`locationToExitingPageRoute = {A -> D, C -> E}`

以下输出是有效的。

`result = [A, B ,C ,D ,E]` 是有效的。`result = [D, A, B ,C ,E]` 也是有效的，因为退出中的路由可以插入到任何位置。

以下输出是无效的。

`result = [B, A, C ,D ,E]` 是无效的，因为 B 必须位于 A 之后。`result = [A, B, C ,E]` 是无效的，因为结果中必须包含 D。

另请参阅：

- [RouteTransitionRecord.markForPush]，使路由带有动画过渡地进入屏幕。
- [RouteTransitionRecord.markForAdd]，使路由无动画过渡地进入屏幕。
- [RouteTransitionRecord.markForPop]，使路由带有动画过渡地离开屏幕。
- [RouteTransitionRecord.markForComplete]，完成路由并使其无动画过渡地离开屏幕。
- [DefaultTransitionDelegate.resolve]，实现了决定路由如何过渡进入或离开屏幕的默认方式。

# DefaultTransitionDelegate

```dart
class DefaultTransitionDelegate<T> extends TransitionDelegate<T> {}
```

如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 未指定其 [Navigator.transitionDelegate]，则会使用此 [TransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/transitiondelegate) 的默认实现。

此过渡委托遵循两条规则。首先，如果进入中的路由与退出中的路由位于同一位置，则所有进入中的路由都会被放置在退出中的路由之上。其次，最顶层的路由总是会带有动画过渡效果。其下方的所有其他路由，要么以 [Route.currentResult] 完成，要么无动画过渡地被添加。

### DefaultTransitionDelegate()

```dart
DefaultTransitionDelegate()
```

创建一个默认的过渡委托。

### resolve()

```dart
Iterable<RouteTransitionRecord> resolve({required List<RouteTransitionRecord> newPageRouteHistory, required Map<RouteTransitionRecord?, RouteTransitionRecord> locationToExitingPageRoute, required Map<RouteTransitionRecord?, List<RouteTransitionRecord>> pageRouteToPagelessRoutes})
```

# kDefaultRouteTraversalEdgeBehavior

```dart
TraversalEdgeBehavior kDefaultRouteTraversalEdgeBehavior
```

[Navigator.routeTraversalEdgeBehavior] 的默认值。

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

# kDefaultRouteDirectionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior kDefaultRouteDirectionalTraversalEdgeBehavior
```

[Navigator.routeDirectionalTraversalEdgeBehavior] 的默认值。

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

# Navigator

```dart
class Navigator extends StatefulWidget {}
```

一个以堆栈方式管理一组子组件的组件。

许多应用程序在其组件层级结构的顶部附近都拥有一个导航器，以便使用 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 来显示其逻辑历史记录，其中最近访问的页面在视觉上位于较旧页面之上。使用这种模式，导航器可以通过在覆盖层中移动组件，实现从一个页面到另一个页面的视觉过渡。类似地，导航器还可以通过将对话框组件定位在当前页面之上来显示对话框。

## Using the Pages API

如果提供了 [Navigator.pages]，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会将其转换为 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 堆栈。[Navigator.pages] 的变化会触发对 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 堆栈的更新。[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会更新其路由，以匹配 [Navigator.pages] 的新配置。要使用此 API，可以创建一个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 子类，并为 [Navigator.pages] 定义一个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 列表。还需要一个 [Navigator.onPopPage] 回调，以便在弹出操作发生时正确清理输入的页面。

默认情况下，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会使用 [DefaultTransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/defaulttransitiondelegate) 来决定路由应如何过渡进入或离开屏幕。要自定义此行为，可以定义一个 [TransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/transitiondelegate) 子类，并将其提供给 [Navigator.transitionDelegate]。

有关使用 Pages API 的更多信息，请参阅 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 组件。

## Using the Navigator API

移动应用通常通过被称为“屏幕”或“页面”的全屏元素来展示其内容。在 Flutter 中，这些元素被称为路由，它们由 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 组件管理。导航器管理着一个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象堆栈，并提供了两种管理该堆栈的方式：声明式 API [Navigator.pages]，或命令式 API [Navigator.push] 和 [Navigator.pop]。

当你的用户界面符合这种堆栈范式（即用户应当能够“导航”返回到堆栈中先前的元素）时，使用路由和 Navigator 是恰当的选择。在某些平台上，例如 Android，系统 UI 会提供一个返回按钮（位于你的应用程序范围之外），允许用户导航返回到应用程序堆栈中先前的路由。在没有这种内置导航机制的平台上，使用 [AppBar](https://www.yuque.com/thyname/flutter.material/appbar)（通常在 [Scaffold.appBar] 属性中使用）可以自动添加一个供用户导航的返回按钮。

### Displaying a full-screen route

尽管你可以直接创建一个导航器，但最常见的做法是使用由 `Router` 创建的导航器，而 `Router` 本身则是由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 或 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 组件创建和配置的。你可以使用 [Navigator.of] 来引用该导航器。

[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 是设置这一切最简单的方式。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 的 home 会成为 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 堆栈底部的路由。这是应用启动时你所看到的内容。

```dart
void main() {
  runApp(const MaterialApp(home: MyAppHome()));
}
```

要在堆栈上压入一个新路由，你可以创建一个 [MaterialPageRoute](https://www.yuque.com/thyname/flutter.material/materialpageroute) 实例，并使用一个构建器函数来创建你希望在屏幕上出现的任何内容。例如：

```dart
Navigator.push(context, MaterialPageRoute<void>(
  builder: (BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('My Page')),
      body: Center(
        child: TextButton(
          child: const Text('POP'),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
    );
  },
));
```

该路由使用构建器函数而非子组件来定义其组件，因为它会根据被压入和弹出的不同时机，在不同的上下文中被构建和重建。

如你所见，可以使用 Navigator 的 pop 方法弹出这个新路由，从而重新显示应用的主页：

```dart
Navigator.pop(context);
```

通常没有必要在使用了 [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 的路由中专门提供一个用于弹出 Navigator 的组件，因为 Scaffold 会自动在其 AppBar 中添加一个“返回”按钮。按下该返回按钮会导致调用 [Navigator.pop]。在 Android 上，按下系统返回按钮也会执行相同的操作。

### Using named navigator routes

移动应用通常需要管理大量路由，通过名称来引用它们往往是最简便的方式。按照惯例，路由名称使用类似路径的结构（例如 '/a/b/c'）。应用的主页路由默认命名为 '/'。

[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 可以使用一个 [Map<String, WidgetBuilder>] 来创建，该映射将路由名称映射到用于创建该路由的构建器函数。[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 会使用此映射为其导航器的 [onGenerateRoute] 回调创建一个值。

```dart
void main() {
  runApp(MaterialApp(
    home: const MyAppHome(), // becomes the route named '/'
    routes: <String, WidgetBuilder> {
      '/a': (BuildContext context) => const MyPage(title: Text('page A')),
      '/b': (BuildContext context) => const MyPage(title: Text('page B')),
      '/c': (BuildContext context) => const MyPage(title: Text('page C')),
    },
  ));
}
```

要按名称显示某个路由：

```dart
Navigator.pushNamed(context, '/b');
```

### Routes can return a value

当压入一个路由是为了向用户询问某个值时，该值可以通过 [pop] 方法的 result 参数返回。

压入路由的方法会返回一个 [Future](https://www.yuque.com/thyname/dart.async/future)。当该路由被弹出时，此 Future 会解析完成，并且该 [Future](https://www.yuque.com/thyname/dart.async/future) 的值即为 [pop] 方法的 `result` 参数。

例如，如果我们想要求用户按下“OK”以确认某项操作，我们可以 `await` [Navigator.push] 的结果：

```dart
bool? value = await Navigator.push(context, MaterialPageRoute<bool>(
  builder: (BuildContext context) {
    return Center(
      child: GestureDetector(
        child: const Text('OK'),
        onTap: () { Navigator.pop(context, true); }
      ),
    );
  }
));
```

如果用户按下“OK”，那么 value 将为 true。如果用户退出该路由，例如通过按下 Scaffold 的返回按钮，那么 value 将为 null。

当某个路由被用来返回一个值时，该路由的类型参数必须与 [pop] 的结果类型相匹配。这就是为什么我们使用 `MaterialPageRoute<bool>` 而非 `MaterialPageRoute<void>` 或仅仅是 `MaterialPageRoute` 的原因。（不过，如果你不想指定类型，那也是可以的。）

### Popup routes

路由不必遮盖整个屏幕。[PopupRoute](https://www.yuque.com/thyname/flutter.widgets/popuproute) 会使用 [ModalRoute.barrierColor] 覆盖屏幕，该颜色可以只是部分不透明，从而让当前屏幕透显出来。弹出式路由是“模态的”，因为它们会阻塞对下方组件的输入。

有一些函数可以创建并显示弹出式路由。例如：[showDialog](https://www.yuque.com/thyname/flutter.material/showdialog)、[showMenu](https://www.yuque.com/thyname/flutter.material/showmenu) 和 [showModalBottomSheet](https://www.yuque.com/thyname/flutter.material/showmodalbottomsheet)。这些函数会像上文描述的那样，返回其所压入路由的 Future。调用者可以等待返回的值，以便在路由被弹出时执行某个操作，或获取该路由的值。

也有一些组件会创建弹出式路由，例如 [PopupMenuButton](https://www.yuque.com/thyname/flutter.material/popupmenubutton) 和 [DropdownButton](https://www.yuque.com/thyname/flutter.material/dropdownbutton)。这些组件会创建 PopupRoute 的内部子类，并使用 Navigator 的 push 和 pop 方法来显示和关闭它们。

### Custom routes

你可以创建自己的组件库路由类子类，例如 [PopupRoute](https://www.yuque.com/thyname/flutter.widgets/popuproute)、[ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 或 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute)，以控制用于显示该路由的动画过渡效果、路由模态屏障的颜色和行为，以及该路由的其他方面。

[PageRouteBuilder](https://www.yuque.com/thyname/flutter.widgets/pageroutebuilder) 类使得可以通过回调的方式定义自定义路由。下面是一个示例，它会在路由出现或消失时对其子组件进行旋转和淡入淡出。此路由并未遮盖整个屏幕，因为它像弹出式路由一样指定了 `opaque: false`。

```dart
Navigator.push(context, PageRouteBuilder<void>(
  opaque: false,
  pageBuilder: (BuildContext context, _, _) {
    return const Center(child: Text('My PageRoute'));
  },
  transitionsBuilder: (_, Animation<double> animation, _, Widget child) {
    return FadeTransition(
      opacity: animation,
      child: RotationTransition(
        turns: Tween<double>(begin: 0.5, end: 1.0).animate(animation),
        child: child,
      ),
    );
  }
));
```

该页面路由由两部分构建而成，即“页面”和“过渡效果”。页面会成为传递给 `transitionsBuilder` 函数的子组件的后代。通常页面只会被构建一次，因为它不依赖于其动画参数（在此示例中用 `_` 省略）。而过渡效果则会在其持续期间的每一帧都被构建。

（在此示例中，路由的返回类型使用了 `void`，因为它不返回任何值。）

### Nesting Navigators

一个应用程序可以使用多个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。将一个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 嵌套在另一个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 之下，可以用来创建一个“内部旅程”，例如标签式导航、用户注册、商店结账，或其他代表你整个应用程序某个子部分的独立旅程。

#### Example

iOS 应用中使用标签式导航是一种标准做法，每个标签都维护自己的导航历史记录。因此，每个标签都拥有自己的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，从而形成一种“并行导航”。

除了标签的并行导航之外，仍然可以启动完全覆盖标签的全屏页面。例如：引导流程或警告对话框。因此，必须存在一个位于标签导航之上的“根” [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。因此，每个标签的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 实际上都是嵌套在单一根 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 之下的嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。

在实践中，用于标签式导航的嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 位于 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 和 [CupertinoTabView](https://www.yuque.com/thyname/flutter.cupertino/cupertinotabview) 组件内部，无需显式创建或管理。

{@tool sample} 以下示例演示了如何使用嵌套的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 来呈现一个独立的用户注册旅程。

尽管此示例使用了两个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 来演示嵌套的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，但仅使用单个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 也可以实现类似的效果。

使用 `flutter run --route=/signup` 运行此示例，即可以注册流程而非主页启动它。

** See code in examples/api/lib/widgets/navigator/navigator.0.dart ** {@end-tool}

[Navigator.of] 会在给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的最近祖先 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 上进行操作。请务必在预期的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 下方提供 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，尤其是在创建了嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的大型 `build` 方法中。可以使用 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件在组件子树中的所需位置获取 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。

### Finding the enclosing route

在模态路由这种常见情况下，可以在构建方法内部使用 [ModalRoute.of] 来获取所在的路由。要判断所在的路由是否为活动路由（例如，以便在路由不活动时使控件变暗），可以在返回的路由上检查 [Route.isCurrent] 属性。

## State Restoration

如果提供了 [restorationScopeId]，并且被一个有效的 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope) 所包围，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 将通过在状态恢复期间重新创建当前 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 历史堆栈，并恢复这些 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的内部状态，来恢复其自身的状态。然而，并非堆栈中所有的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 都能够被恢复：

- 基于 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的路由，如果提供了 [Page.restorationId]，则会恢复其状态。
- 使用经典命令式 API（[push]、[pushNamed] 及其同类方法）添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)，永远无法恢复其状态。
- 使用可恢复的命令式 API（[restorablePush]、[restorablePushNamed] 以及所有其他方法名中带有 "restorable" 的命令式方法）添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)，如果其下方直至并包括下方第一个基于 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的路由在内的所有路由都被恢复，则会恢复其状态。如果其下方不存在基于 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的路由，则只有当其下方所有路由都恢复了各自的状态时，它才会恢复自身状态。

如果某个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 被认为是可恢复的，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会将其 [Route.restorationScopeId] 设置为一个非空值。路由可以使用该 ID 来存储和恢复自身的状态。例如，[ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 会使用此 ID 为其内容组件创建一个 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope)。

### Navigator()

```dart
Navigator({dynamic key, List<Page<dynamic>> pages = const <Page<dynamic>>[], PopPageCallback? onPopPage, String? initialRoute, RouteListFactory onGenerateInitialRoutes = Navigator.defaultGenerateInitialRoutes, RouteFactory? onGenerateRoute, RouteFactory? onUnknownRoute, TransitionDelegate<dynamic> transitionDelegate = const DefaultTransitionDelegate<dynamic>(), bool reportsRouteUpdateToEngine = false, Clip clipBehavior = Clip.hardEdge, List<NavigatorObserver> observers = const <NavigatorObserver>[], bool requestFocus = true, String? restorationScopeId, TraversalEdgeBehavior routeTraversalEdgeBehavior = kDefaultRouteTraversalEdgeBehavior, TraversalEdgeBehavior routeDirectionalTraversalEdgeBehavior = kDefaultRouteDirectionalTraversalEdgeBehavior, DidRemovePageCallback? onDidRemovePage})
```

创建一个以堆栈方式维护子组件历史记录的组件。

如果 [pages] 不为空，则 [onPopPage] 不能为 null。

### pages

```dart
List<Page<dynamic>> pages
```

用于填充历史记录的页面列表。

页面会通过 [Page.createRoute] 转换为路由，这与 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 通过 [Widget.createElement]（以及 [StatefulWidget.createState] 或 [RenderObjectWidget.createRenderObject]）转换为 [Element](https://www.yuque.com/thyname/flutter.widgets/element)（以及 [State](https://www.yuque.com/thyname/flutter.widgets/state) 或 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)）的方式类似。

当此列表更新时，新列表会与先前的列表进行比较，并相应地更新路由集合。

有些 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 并不对应于 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 对象，即那些使用 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) API（[push] 及其同类方法）添加到历史记录中的路由。不对应于 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 对象的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 被称为无页面路由，它会与历史记录中位于其下方、且*确实*对应于某个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 对象的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 相绑定。

被添加或移除的页面可能会按照 [transitionDelegate] 的控制进行动画处理。如果某个被移除的页面上曾使用 [push] 及其同类方法压入了其他无页面路由，那么这些无页面路由也会根据 [transitionDelegate] 的判定，带有或不带动画地一并被移除。

要使用此 API，还必须提供一个 [onPopPage] 回调，以便在某个页面被弹出时正确清理此列表。

如果在组件首次创建时 [initialRoute] 非空，则会使用 [onGenerateInitialRoutes] 在初始历史记录中生成位于 [pages] 对应路由之上的路由。

### onPopPage

```dart
PopPageCallback? onPopPage
```

此项已被弃用，由 [onDidRemovePage] 取代。

当调用 [pop] 但当前 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对应于 [pages] 列表中的某个 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 时被调用。

`result` 参数是该路由将要完成时所使用的值（例如某个对话框返回的值）。

此回调负责调用 [Route.didPop] 并返回此次弹出操作是否成功。

应使用一个不包含该 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对应 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的 [pages] 列表来重建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 组件。下次 [pages] 列表更新时，如果对应于此 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 仍然存在，它将被视为一个需要显示的新路由。

### onDidRemovePage

```dart
DidRemovePageCallback? onDidRemovePage
```

当与给定 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 关联的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 已从 Navigator 中移除时调用。

当路由通过 [Navigator.pop]、[Navigator.pushReplacement] 或其同类方法被移除或完成时，可能会发生这种情况。

此回调负责将给定的页面从 [pages] 列表中移除。

应使用一个不包含给定页面 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 的 [pages] 列表来重建 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 组件。下次 [pages] 列表更新时，如果给定的 [Page](https://www.yuque.com/thyname/flutter.widgets/page) 仍然存在，它将被视为一个需要显示的新页面。

### transitionDelegate

```dart
TransitionDelegate<dynamic> transitionDelegate
```

用于决定在 [pages] 更新期间路由应如何过渡进入或离开屏幕的委托。

默认为 [DefaultTransitionDelegate](https://www.yuque.com/thyname/flutter.widgets/defaulttransitiondelegate)。

### initialRoute

```dart
String? initialRoute
```

要显示的第一个路由的名称。

默认为 [Navigator.defaultRouteName]。

该值会根据 [onGenerateInitialRoutes]（默认为 [defaultGenerateInitialRoutes]）进行解释。

更改 [initialRoute] 不会产生任何效果，因为它只控制*初始*路由。要在应用程序运行期间更改路由，请使用此类上的静态函数，例如 [push] 或 [replace]。

### onGenerateRoute

```dart
RouteFactory? onGenerateRoute
```

调用以为给定的 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings) 生成一个路由。

### onUnknownRoute

```dart
RouteFactory? onUnknownRoute
```

当 [onGenerateRoute] 未能生成路由时调用。

此回调通常用于错误处理。例如，此回调可能总是生成一个描述未找到路由的“未找到”页面。

未知路由既可能源于应用程序中的错误，也可能源于来自外部的压入路由请求，例如来自 Android intent 的请求。

### observers

```dart
List<NavigatorObserver> observers
```

此导航器的观察者列表。

### restorationScopeId

```dart
String? restorationScopeId
```

用于保存和恢复导航器状态（包括其历史记录）的恢复 ID。

{@template flutter.widgets.navigator.restorationScopeId} 如果提供了恢复 ID，导航器将持久化其内部状态（包括路由历史记录以及路由的可恢复状态），并在状态恢复期间恢复它。

如果未提供恢复 ID，则路由历史堆栈将不会被恢复，各个路由的状态恢复功能也会被禁用。

该状态会持久化在使用所提供的恢复 ID 从周围的 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope) 申领的 [RestorationBucket](https://www.yuque.com/thyname/flutter.services/restorationbucket) 中。在该 bucket 内，[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 还会为其子级（各个 [Route](https://www.yuque.com/thyname/flutter.widgets/route)）创建一个新的 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope)。

另请参阅：

- [RestorationManager](https://www.yuque.com/thyname/flutter.services/restorationmanager)，其中解释了状态恢复在 Flutter 中的工作原理。
- [RestorationMixin](https://www.yuque.com/thyname/flutter.widgets/restorationmixin)，其中包含一个展示 Flutter 状态恢复功能的可运行代码示例。
- [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，其中在“状态恢复”标题下解释了导航器如何以及在何种条件下恢复其状态。
- [Navigator.restorablePush]，其中包含一个展示如何向导航器压入可恢复路由的示例。{@endtemplate}

### routeTraversalEdgeBehavior

```dart
TraversalEdgeBehavior routeTraversalEdgeBehavior
```

控制焦点转移超出某个焦点作用域的第一个和最后一个项目的行为，该焦点作用域定义了路由内组件的焦点遍历方式。

{@template flutter.widgets.navigator.routeTraversalEdgeBehavior} 安装在应用顶层的路由内部的焦点，会影响应用相对于其周围平台内容的行为方式。例如，在 web 上，应用至少会被浏览器 UI（例如地址栏、浏览器标签页等）所包围。用户应当能够使用正常的焦点快捷键到达浏览器 UI。类似地，如果应用被嵌入在一个 `<iframe>` 或自定义元素内部，它也应当能够参与到整体的焦点遍历中，包括那些并非由 Flutter 渲染的元素。{@endtemplate}

### routeDirectionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior routeDirectionalTraversalEdgeBehavior
```

控制方向性焦点转移超出某个焦点作用域的第一个和最后一个项目的行为，该焦点作用域定义了路由内组件的焦点遍历方式。

{@macro flutter.widgets.navigator.routeTraversalEdgeBehavior}

### defaultRouteName

```dart
String defaultRouteName
```

应用程序默认路由的名称。

另请参阅：

- [dart:ui.PlatformDispatcher.defaultRouteName]，它反映了应用程序启动时所使用的路由。

### onGenerateInitialRoutes

```dart
RouteListFactory onGenerateInitialRoutes
```

在组件创建时调用，如果 [initialRoute] 不为 null，则用于生成 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象的初始列表。

默认为 [defaultGenerateInitialRoutes]。

[NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate) 和 [initialRoute] 将被传递给该回调。此回调必须返回一个 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象列表，用于对历史记录进行初始化。

在解析 initialRoute 时，如果它有可能包含复杂字符，最好使用 [characters](https://pub.dev/packages/characters) API。这将确保扩展的字素簇和代理对在代码中被当作单个字符处理，与它们在用户看来的呈现方式一致。例如，字符串 "👨‍👩‍👦" 在用户看来是单个字符，`string.characters.length` 直观地返回 1。而另一方面，`string.length` 返回 8，`string.runes.length` 返回 5！

### reportsRouteUpdateToEngine

```dart
bool reportsRouteUpdateToEngine
```

当最顶层路由发生变化时，此导航器是否应向引擎报告路由更新消息。

如果此属性设为 true，则当此导航器检测到最顶层路由发生变化时，会自动向引擎发送路由更新消息。这些消息由 web 引擎用来更新浏览器地址栏。

如果在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 首次创建时此属性被设为 true，则会使用 [SystemNavigator.selectSingleEntryHistory] 请求单条目历史模式。这意味着此属性不应与 [Router](https://www.yuque.com/thyname/flutter.widgets/router) 一起使用 [PlatformRouteInformationProvider](https://www.yuque.com/thyname/flutter.widgets/platformrouteinformationprovider) 的场合同时使用（例如与 [MaterialApp.router] 一起使用时）。

如果组件树中存在多个导航器，最多只能有一个导航器将此属性设为 true（通常是从 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的最顶层导航器）。否则，web 引擎可能会从不同的导航器接收到多条路由更新消息，从而无法正确更新地址栏。

默认为 false。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

在不希望进行裁剪的情况下，请考虑将此属性设为 [Clip.none]。

默认为 [Clip.hardEdge]。

### requestFocus

```dart
bool requestFocus
```

当新路由被压入导航器时，导航器及其新的最顶层路由是否应请求获得焦点。

如果最顶层路由上设置了 [Route.requestFocus]，则该设置将优先于此值。

默认为 true。

### pushNamed()

```dart
Future<T?> pushNamed<T extends Object?>(BuildContext context, String routeName, {Object? arguments})
```

将一个具名路由压入与给定上下文最紧密关联的导航器。

{@template flutter.widgets.navigator.pushNamed} 该路由名称将被传递给 [Navigator.onGenerateRoute] 回调。返回的路由将被压入导航器。

新路由和先前的路由（如果存在的话）都会收到通知（见 [Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPush]）。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是该路由返回值的类型。

要使用 [pushNamed]，必须提供一个 [Navigator.onGenerateRoute] 回调。{@endtemplate}

{@template flutter.widgets.navigator.pushNamed.returnValue} 返回一个 [Future](https://www.yuque.com/thyname/dart.async/future)，当被压入的路由从导航器弹出时，该 Future 会以传给 [pop] 的 `result` 值完成。{@endtemplate}

{@template flutter.widgets.Navigator.pushNamed} 提供的 `arguments` 会通过 [RouteSettings.arguments] 传递给被压入的路由。任何对象都可以作为 `arguments` 传递（例如 [String](https://www.yuque.com/thyname/dart.core/string)、[int](https://www.yuque.com/thyname/dart.core/int)，或自定义 `MyRouteArguments` 类的实例）。通常会使用 [Map](https://www.yuque.com/thyname/dart.core/map) 来传递键值对。

`arguments` 可以在 [Navigator.onGenerateRoute] 或 [Navigator.onUnknownRoute] 中用于构造路由。{@endtemplate}

{@tool snippet}

典型用法如下：

```dart
void _didPushButton() {
  Navigator.pushNamed(context, '/settings');
}
```

{@end-tool}

{@tool snippet}

以下示例展示了如何向路由传递额外的 `arguments`：

```dart
void _showBerlinWeather() {
  Navigator.pushNamed(
    context,
    '/weather',
    arguments: <String, String>{
      'city': 'Berlin',
      'country': 'Germany',
    },
  );
}
```

{@end-tool}

{@tool snippet}

以下示例展示了如何向路由传递一个自定义 Object：

```dart
class WeatherRouteArguments {
  WeatherRouteArguments({ required this.city, required this.country });
  final String city;
  final String country;

  bool get isGermanCapital {
    return country == 'Germany' && city == 'Berlin';
  }
}

void _showWeather() {
  Navigator.pushNamed(
    context,
    '/weather',
    arguments: WeatherRouteArguments(city: 'Berlin', country: 'Germany'),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePushNamed]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePushNamed()

```dart
String restorablePushNamed<T extends Object?>(BuildContext context, String routeName, {Object? arguments})
```

将一个具名路由压入与给定上下文最紧密关联的导航器。

{@template flutter.widgets.navigator.restorablePushNamed} 与通过 [pushNamed] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed}

{@template flutter.widgets.Navigator.restorablePushNamed.arguments} 提供的 `arguments` 会通过 [RouteSettings.arguments] 传递给被压入的路由。任何可以通过 [StandardMessageCodec](https://www.yuque.com/thyname/flutter.services/standardmessagecodec) 序列化的对象都可以作为 `arguments` 传递。通常会使用 Map 来传递键值对。

这些参数可以在 [Navigator.onGenerateRoute] 或 [Navigator.onUnknownRoute] 中用于构造路由。{@endtemplate}

{@template flutter.widgets.Navigator.restorablePushNamed.returnValue} 此方法会为被压入的路由返回一个不透明的 ID，[RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture) 可以使用该 ID 来访问被添加到导航器中的实际 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象及其返回值。如果你不关心该路由对象或路由的返回值，可以忽略此方法的返回值。{@endtemplate}

{@tool snippet}

典型用法如下：

```dart
void _showParisWeather() {
  Navigator.restorablePushNamed(
    context,
    '/weather',
    arguments: <String, String>{
      'city': 'Paris',
      'country': 'France',
    },
  );
}
```

{@end-tool}

### pushReplacementNamed()

```dart
Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

通过压入名为 [routeName] 的路由，来替换与给定上下文最紧密关联的导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@template flutter.widgets.navigator.pushReplacementNamed} 如果 `result` 非空，它将被用作被移除路由的结果；压入该旧路由时所返回的 future 将以 `result` 完成。诸如对话框或弹出菜单之类的路由通常使用这一机制，将用户所选择的值返回给创建其路由的组件。如果提供了 `result`，其类型必须与旧路由所属类的类型参数（`TO`）相匹配。

该路由名称将被传递给 [Navigator.onGenerateRoute] 回调。返回的路由将被压入导航器。

新路由以及位于被移除路由下方的路由都会收到通知（见 [Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didReplace]）。被移除的路由会在新路由完成动画后收到通知（见 [Route.didComplete]）。被移除路由的退出动画不会运行（关于会为被移除路由添加动画的变体，请参阅 [popAndPushNamed]）。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是新路由返回值的类型，`TO` 是旧路由返回值的类型。

要使用 [pushReplacementNamed]，必须提供一个 [Navigator.onGenerateRoute] 回调。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _switchToBrightness() {
  Navigator.pushReplacementNamed(context, '/settings/brightness');
}
```

{@end-tool}

另请参阅：

- [restorablePushReplacementNamed]，它压入一个可以在状态恢复期间被恢复的替换路由。

### restorablePushReplacementNamed()

```dart
String restorablePushReplacementNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

通过压入名为 [routeName] 的路由，来替换与给定上下文最紧密关联的导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@template flutter.widgets.navigator.restorablePushReplacementNamed} 与通过 [pushReplacementNamed] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _switchToAudioVolume() {
  Navigator.restorablePushReplacementNamed(context, '/settings/volume');
}
```

{@end-tool}

### popAndPushNamed()

```dart
Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

将与给定上下文最紧密关联的导航器的当前路由弹出，并在其位置压入一个具名路由。

{@template flutter.widgets.navigator.popAndPushNamed} 先前路由的弹出会按照 [pop] 的方式处理。

新路由的名称将被传递给 [Navigator.onGenerateRoute] 回调。返回的路由将被压入导航器。

新路由、旧路由，以及位于旧路由下方的路由（如果存在的话），都会收到通知（见 [Route.didPop]、[Route.didComplete]、[Route.didPopNext]、[Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPop] 和 [NavigatorObserver.didPush]）。弹出与压入的动画会同时执行，因此即使旧路由和新路由都是不透明的（见 [TransitionRoute.opaque]），下方的路由也可能会短暂可见。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是新路由返回值的类型，`TO` 是旧路由返回值的类型。

要使用 [popAndPushNamed]，必须提供一个 [Navigator.onGenerateRoute] 回调。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _selectAccessibility() {
  Navigator.popAndPushNamed(context, '/settings/accessibility');
}
```

{@end-tool}

另请参阅：

- [restorablePopAndPushNamed]，它压入一个可以在状态恢复期间被恢复的新路由。

### restorablePopAndPushNamed()

```dart
String restorablePopAndPushNamed<T extends Object?, TO extends Object?>(BuildContext context, String routeName, {TO? result, Object? arguments})
```

将与给定上下文最紧密关联的导航器的当前路由弹出，并在其位置压入一个具名路由。

{@template flutter.widgets.navigator.restorablePopAndPushNamed} 与通过 [popAndPushNamed] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _selectNetwork() {
  Navigator.restorablePopAndPushNamed(context, '/settings/network');
}
```

{@end-tool}

### pushNamedAndRemoveUntil()

```dart
Future<T?> pushNamedAndRemoveUntil<T extends Object?>(BuildContext context, String newRouteName, RoutePredicate predicate, {Object? arguments})
```

将具有给定名称的路由压入与给定上下文最紧密关联的导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@template flutter.widgets.navigator.pushNamedAndRemoveUntil} 如果 [Route.willHandlePopInternally] 为真，该谓词可能会被应用于同一个路由多次。

要移除路由直到某个具有特定名称的路由为止，请使用从 [ModalRoute.withName] 返回的 [RoutePredicate](https://www.yuque.com/thyname/flutter.widgets/routepredicate)。

要移除被压入路由下方的所有路由，请使用一个总是返回 false 的 [RoutePredicate](https://www.yuque.com/thyname/flutter.widgets/routepredicate)（例如 `(Route<dynamic> route) => false`）。

被移除的路由会在未完成的情况下被移除，因此此方法不接受返回值参数。

新路由的名称（`routeName`）将被传递给 [Navigator.onGenerateRoute] 回调。返回的路由将被压入导航器。

新路由以及位于最底层被移除路由下方的路由（该路由将成为新路由下方的路由）都会收到通知（见 [Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPush] 和 [NavigatorObserver.didRemove]）。一旦新路由完成动画，被移除的路由就会被释放，且压入这些路由时所返回的 future 将会完成。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是新路由返回值的类型。

要使用 [pushNamedAndRemoveUntil]，必须提供一个 [Navigator.onGenerateRoute] 回调。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _resetToCalendar() {
  Navigator.pushNamedAndRemoveUntil(context, '/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

另请参阅：

- [restorablePushNamedAndRemoveUntil]，它压入一个可以在状态恢复期间被恢复的新路由。

### restorablePushNamedAndRemoveUntil()

```dart
String restorablePushNamedAndRemoveUntil<T extends Object?>(BuildContext context, String newRouteName, RoutePredicate predicate, {Object? arguments})
```

将具有给定名称的路由压入与给定上下文最紧密关联的导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@template flutter.widgets.navigator.restorablePushNamedAndRemoveUntil} 与通过 [pushNamedAndRemoveUntil] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _openCalendar() {
  navigator.restorablePushNamedAndRemoveUntil('/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

### push()

```dart
Future<T?> push<T extends Object?>(BuildContext context, Route<T> route)
```

将给定的路由压入与给定上下文最紧密关联的导航器。

{@template flutter.widgets.navigator.push} 新路由和先前的路由（如果存在的话）都会收到通知（见 [Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPush]）。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是该路由返回值的类型。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _openMyPage() {
  Navigator.push<void>(
    context,
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyPage(),
    ),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePush]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePush()

```dart
String restorablePush<T extends Object?>(BuildContext context, RestorableRouteBuilder<T> routeBuilder, {Object? arguments})
```

将一个新路由压入与给定上下文最紧密关联的导航器。

{@template flutter.widgets.navigator.restorablePush} 与通过 [push] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.push}

{@template flutter.widgets.Navigator.restorablePush} 此方法接受一个 [RestorableRouteBuilder](https://www.yuque.com/thyname/flutter.widgets/restorableroutebuilder) 作为参数，该参数必须是一个使用 `@pragma('vm:entry-point')` 注解的*静态*函数。它必须实例化并返回一个将被添加到导航器的新 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象。提供的 `arguments` 对象会被传递给 `routeBuilder`。导航器会在状态恢复期间再次调用静态的 `routeBuilder` 函数，以重新创建该路由对象。

任何可以通过 [StandardMessageCodec](https://www.yuque.com/thyname/flutter.services/standardmessagecodec) 序列化的对象都可以作为 `arguments` 传递。通常会使用 Map 来传递键值对。{@endtemplate}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push.0.dart ** {@end-tool}

### pushReplacement()

```dart
Future<T?> pushReplacement<T extends Object?, TO extends Object?>(BuildContext context, Route<T> newRoute, {TO? result})
```

通过压入给定的路由，来替换与给定上下文最紧密关联的导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@template flutter.widgets.navigator.pushReplacement} 如果 `result` 非空，它将被用作被移除路由的结果；压入该旧路由时所返回的 future 将以 `result` 完成。诸如对话框或弹出菜单之类的路由通常使用这一机制，将用户所选择的值返回给创建其路由的组件。如果提供了 `result`，其类型必须与旧路由所属类的类型参数（`TO`）相匹配。

新路由以及位于被移除路由下方的路由都会收到通知（见 [Route.didPush] 和 [Route.didChangeNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didReplace]）。被移除的路由会在新路由完成动画后收到通知（见 [Route.didComplete]）。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是新路由返回值的类型，`TO` 是旧路由返回值的类型。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _completeLogin() {
  Navigator.pushReplacement<void, void>(
    context,
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyHomePage(),
    ),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePushReplacement]，它压入一个可以在状态恢复期间被恢复的替换路由。

### restorablePushReplacement()

```dart
String restorablePushReplacement<T extends Object?, TO extends Object?>(BuildContext context, RestorableRouteBuilder<T> routeBuilder, {TO? result, Object? arguments})
```

通过压入一个新路由，来替换与给定上下文最紧密关联的导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@template flutter.widgets.navigator.restorablePushReplacement} 与通过 [pushReplacement] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push_replacement.0.dart ** {@end-tool}

### pushAndRemoveUntil()

```dart
Future<T?> pushAndRemoveUntil<T extends Object?>(BuildContext context, Route<T> newRoute, RoutePredicate predicate)
```

将给定的路由压入与给定上下文最紧密关联的导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@template flutter.widgets.navigator.pushAndRemoveUntil} 如果 [Route.willHandlePopInternally] 为真，该谓词可能会被应用于同一个路由多次。

要移除路由直到某个具有特定名称的路由为止，请使用从 [ModalRoute.withName] 返回的 [RoutePredicate](https://www.yuque.com/thyname/flutter.widgets/routepredicate)。

要移除被压入路由下方的所有路由，请使用一个总是返回 false 的 [RoutePredicate](https://www.yuque.com/thyname/flutter.widgets/routepredicate)（例如 `(Route<dynamic> route) => false`）。

被移除的路由会在未完成的情况下被移除，因此此方法不接受返回值参数。

新压入的路由及其前一个路由会收到 [Route.didPush] 通知。移除完成后，新路由及其新的前一个路由（位于最底层被移除路由下方的路由）会通过 [Route.didChangeNext] 收到通知。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPush] 和 [NavigatorObserver.didRemove]）。一旦新路由完成动画，被移除的路由就会被释放并收到通知。压入这些路由时所返回的 future 将会完成。

当压入新路由时，当前路由内正在进行的手势会被取消。

类型参数 `T` 是新路由返回值的类型。{@endtemplate}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _finishAccountCreation() {
  Navigator.pushAndRemoveUntil<void>(
    context,
    MaterialPageRoute<void>(builder: (BuildContext context) => const MyHomePage()),
    ModalRoute.withName('/'),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePushAndRemoveUntil]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePushAndRemoveUntil()

```dart
String restorablePushAndRemoveUntil<T extends Object?>(BuildContext context, RestorableRouteBuilder<T> newRouteBuilder, RoutePredicate predicate, {Object? arguments})
```

将一个新路由压入与给定上下文最紧密关联的导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@template flutter.widgets.navigator.restorablePushAndRemoveUntil} 与通过 [pushAndRemoveUntil] 压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法压入的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator.restorable_push_and_remove_until.0.dart ** {@end-tool}

### replace()

```dart
void replace<T extends Object?>(BuildContext context, {required Route<dynamic> oldRoute, required Route<T> newRoute})
```

使用一个新路由，替换与给定上下文最紧密关联的导航器上的某个路由。

{@template flutter.widgets.navigator.replace} 旧路由必须当前不可见，因为此方法会跳过动画，因此如果该路由可见，移除操作将会显得突兀。要替换最顶层的路由，请考虑改用 [pushReplacement]，它*确实*会为新路由添加动画，并会延迟移除旧路由，直到新路由完成动画为止。

被移除的路由会被移除，并以 `null` 值完成。

新路由、位于新路由下方的路由（如果存在的话），以及位于新路由上方的路由，都会收到通知（见 [Route.didReplace]、[Route.didChangeNext] 和 [Route.didChangePrevious]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didReplace]）。被移除的路由会被释放，其 future 也会完成。

在构建非线性用户体验时，此方法可以与 [removeRouteBelow] 结合使用，十分有用。

类型参数 `T` 是新路由返回值的类型。{@endtemplate}

另请参阅：

- [replaceRouteBelow]，与此方法相同，但是通过引用待移除路由上方的路由来标识该路由，而非直接标识。
- [restorableReplace]，它添加一个可以在状态恢复期间被恢复的替换路由。

### restorableReplace()

```dart
String restorableReplace<T extends Object?>(BuildContext context, {required Route<dynamic> oldRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

使用一个新路由，替换与给定上下文最紧密关联的导航器上的某个路由。

{@template flutter.widgets.navigator.restorableReplace} 与通过 [replace] 添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.replace}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### replaceRouteBelow()

```dart
void replaceRouteBelow<T extends Object?>(BuildContext context, {required Route<dynamic> anchorRoute, required Route<T> newRoute})
```

使用一个新路由，替换与给定上下文最紧密关联的导航器上的某个路由。待替换的路由是位于给定 `anchorRoute` 下方的那个路由。

{@template flutter.widgets.navigator.replaceRouteBelow} 旧路由必须当前不可见，因为此方法会跳过动画，因此如果该路由可见，移除操作将会显得突兀。要替换最顶层的路由，请考虑改用 [pushReplacement]，它*确实*会为新路由添加动画，并会延迟移除旧路由，直到新路由完成动画为止。

被移除的路由会被移除，并以 `null` 值完成。

新路由、位于新路由下方的路由（如果存在的话），以及位于新路由上方的路由，都会收到通知（见 [Route.didReplace]、[Route.didChangeNext] 和 [Route.didChangePrevious]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didReplace]）。被移除的路由会被释放，其 future 也会完成。

类型参数 `T` 是新路由返回值的类型。{@endtemplate}

另请参阅：

- [replace]，与此方法相同，但直接标识待移除的路由。
- [restorableReplaceRouteBelow]，它添加一个可以在状态恢复期间被恢复的替换路由。

### restorableReplaceRouteBelow()

```dart
String restorableReplaceRouteBelow<T extends Object?>(BuildContext context, {required Route<dynamic> anchorRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

使用一个新路由，替换与给定上下文最紧密关联的导航器上的某个路由。待替换的路由是位于给定 `anchorRoute` 下方的那个路由。

{@template flutter.widgets.navigator.restorableReplaceRouteBelow} 与通过 [restorableReplaceRouteBelow] 添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 不同，使用此方法添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 会在状态恢复期间按照 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的“状态恢复”一节中所述的规则进行恢复。{@endtemplate}

{@macro flutter.widgets.navigator.replaceRouteBelow}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### canPop()

```dart
bool canPop(BuildContext context)
```

与给定上下文最紧密关联的导航器是否可以被弹出。

{@template flutter.widgets.navigator.canPop} 初始路由无法从导航器中弹出，这意味着只有在弹出导航器不会移除初始路由的情况下，此函数才会返回 true。

如果作用域内不存在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则返回 false。

此方法不考虑任何可能从外部阻止弹出的因素，例如 [PopEntry](https://www.yuque.com/thyname/flutter.widgets/popentry)。{@endtemplate}

另请参阅：

- [Route.isFirst]，对于 [canPop] 返回 false 的路由，此属性返回 true。

### maybePop()

```dart
Future<bool> maybePop<T extends Object?>(BuildContext context, [T? result])
```

查询当前路由的 [Route.popDisposition] 获取器或 [Route.willPop] 方法，并据此采取相应行动，可能会因此弹出该路由；返回该弹出请求是否应被视为已处理。

{@template flutter.widgets.navigator.maybePop} 如果 [RoutePopDisposition](https://www.yuque.com/thyname/flutter.widgets/routepopdisposition) 为 [RoutePopDisposition.pop]，则会调用 [pop] 方法，且此方法返回 true，表明它已处理该弹出请求。

如果 [RoutePopDisposition](https://www.yuque.com/thyname/flutter.widgets/routepopdisposition) 为 [RoutePopDisposition.doNotPop]，则此方法返回 true，但不会执行其他任何操作。

如果 [RoutePopDisposition](https://www.yuque.com/thyname/flutter.widgets/routepopdisposition) 为 [RoutePopDisposition.bubble]，则此方法返回 false，调用者需负责将请求发送给包含它的作用域（例如通过关闭应用程序）。

此方法通常是针对用户发起的 [pop] 而调用的。例如在 Android 上，它是由系统返回按钮的绑定所调用的。

类型参数 `T` 是当前路由返回值的类型。（通常此类型未知；请考虑指定 `dynamic` 或 `Null`。）{@endtemplate}

另请参阅：

- [Form](https://www.yuque.com/thyname/flutter.widgets/form)，它提供了一个 `onWillPop` 回调，使表单能够否决由应用返回按钮所发起的 [pop]。
- [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute)，它提供了一个 `scopedWillPopCallback`，可用于定义该路由的 `willPop` 方法。

### pop()

```dart
void pop<T extends Object?>(BuildContext context, [T? result])
```

将与给定上下文最紧密关联的导航器上最顶层的路由弹出。

{@template flutter.widgets.navigator.pop} 首先会调用当前路由的 [Route.didPop] 方法。如果该方法返回 false，则该路由会保留在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的历史记录中（此时预期该路由已经弹出了某些内部状态；参见例如 [LocalHistoryRoute](https://www.yuque.com/thyname/flutter.widgets/localhistoryroute)）。否则，本说明的其余部分将适用。

如果 `result` 非空，它将被用作被弹出路由的结果；压入该被弹出路由时所返回的 future 将以 `result` 完成。诸如对话框或弹出菜单之类的路由通常使用这一机制，将用户所选择的值返回给创建其路由的组件。如果提供了 `result`，其类型必须与被弹出路由所属类的类型参数（`T`）相匹配。

被弹出的路由及其下方的路由都会收到通知（见 [Route.didPop]、[Route.didComplete] 和 [Route.didPopNext]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didPop]）。

类型参数 `T` 是被弹出路由返回值的类型。

如果提供了 `result`，其类型必须与被弹出路由所属类的类型参数（`T`）相匹配。{@endtemplate}

{@tool snippet}

典型用法如下，用于关闭一个路由：

```dart
void _close() {
  Navigator.pop(context);
}
```

{@end-tool}

一个对话框可能会带着一个结果被关闭：

```dart
void _accept() {
  Navigator.pop(context, true); // dialog returns true
}
```

### popUntil()

```dart
void popUntil(BuildContext context, RoutePredicate predicate)
```

在与给定上下文最紧密关联的导航器上反复调用 [pop]，直到谓词返回 true 为止。

{@template flutter.widgets.navigator.popUntil} 如果 [Route.willHandlePopInternally] 为真，该谓词可能会被应用于同一个路由多次。

要弹出直到某个具有特定名称的路由为止，请使用从 [ModalRoute.withName] 返回的 [RoutePredicate](https://www.yuque.com/thyname/flutter.widgets/routepredicate)。

这些路由会以 null 作为其 `return` 值被关闭。

有关弹出路由的语义的更多详情，请参阅 [pop]。{@endtemplate}

{@tool snippet}

典型用法如下：

```dart
void _logout() {
  Navigator.popUntil(context, ModalRoute.withName('/login'));
}
```

{@end-tool}

### popUntilWithResult()

```dart
void popUntilWithResult<T extends Object?>(BuildContext context, RoutePredicate predicate, T? result)
```

在与给定上下文最紧密关联的导航器上反复调用 [pop]，直到谓词返回 true 为止，并将 [result] 返回给最后一个被弹出的路由。

类型参数 `T` 是最后一个被弹出路由返回值的类型。

{@macro flutter.widgets.navigator.popUntil}

### removeRoute()

```dart
void removeRoute<T extends Object?>(BuildContext context, Route<T> route, [T? result])
```

立即从与给定上下文最紧密关联的导航器中移除 `route`，并对其调用 [Route.dispose]。

{@template flutter.widgets.navigator.removeRoute} 此方法调用不会运行任何动画。

被移除路由的下方和上方的路由都会收到通知（见 [Route.didChangeNext] 和 [Route.didChangePrevious]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didRemove]）。被移除的路由会被释放，其 future 也会完成。

给定的 `route` 必须处于历史记录中；如果不是，此方法将抛出异常。

如果 `result` 非空，它将被用作被移除路由的结果；压入该被移除路由时所返回的 future 将以 `result` 完成。如果提供了此值，其类型必须与被弹出路由所属类的类型参数（`T`）相匹配。

类型参数 `T` 是被弹出路由返回值的类型。

如果提供了 `result`，其类型必须与被移除路由所属类的类型参数（`T`）相匹配。

当前路由内正在进行的手势会被取消。{@endtemplate}

此方法可用于，例如，在屏幕方向改变时立即关闭正在显示的下拉菜单。

### removeRouteBelow()

```dart
void removeRouteBelow<T extends Object?>(BuildContext context, Route<T> anchorRoute, [T? result])
```

立即从与给定上下文最紧密关联的导航器中移除一个路由，并对其调用 [Route.dispose]。待移除的路由是位于给定 `anchorRoute` 下方的那个路由。

{@template flutter.widgets.navigator.removeRouteBelow} 此方法调用不会运行任何动画。

被移除路由的下方和上方的路由都会收到通知（见 [Route.didChangeNext] 和 [Route.didChangePrevious]）。如果 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 拥有任何 [Navigator.observers]，它们也会收到通知（见 [NavigatorObserver.didRemove]）。被移除的路由会被释放，其 future 也会完成。

给定的 `anchorRoute` 必须处于历史记录中，且其下方必须存在一个路由；如果不满足这些条件，此方法将抛出异常。

如果 `result` 非空，它将被用作被移除路由的结果；压入该被移除路由时所返回的 future 将以 `result` 完成。如果提供了此值，其类型必须与被弹出路由所属类的类型参数（`T`）相匹配。

类型参数 `T` 是被弹出路由返回值的类型。

如果提供了 `result`，其类型必须与被移除路由所属类的类型参数（`T`）相匹配。

当前路由内正在进行的手势会被取消。{@endtemplate}

### of()

```dart
NavigatorState of(BuildContext context, {bool rootNavigator = false})
```

包含给定上下文的此类最近实例的状态。

典型用法如下：

```dart
Navigator.of(context)
  ..pop()
  ..pop()
  ..pushNamed('/settings');
```

如果将 `rootNavigator` 设为 true，则会改为返回此类最远实例的状态。这对于将内容压入到所有后续 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 实例之上很有用。

如果在给定的 `context` 中不存在 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，此函数将在调试模式下抛出 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)，在发布模式下抛出异常。

此方法的开销可能较大（它需要遍历 Element 树）。

### maybeOf()

```dart
NavigatorState? maybeOf(BuildContext context, {bool rootNavigator = false})
```

包含给定上下文的此类最近实例的状态（如果存在的话）。

典型用法如下：

```dart
NavigatorState? navigatorState = Navigator.maybeOf(context);
if (navigatorState != null) {
  navigatorState
    ..pop()
    ..pop()
    ..pushNamed('/settings');
}
```

如果将 `rootNavigator` 设为 true，则会改为返回此类最远实例的状态。这对于将内容压入到所有后续 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 实例之上很有用。

如果 `context` 中不存在祖先 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，则返回 null。

此方法的开销可能较大（它需要遍历 Element 树）。

### defaultGenerateInitialRoutes()

```dart
List<Route<dynamic>> defaultGenerateInitialRoutes(NavigatorState navigator, String initialRouteName)
```

将一个路由名称转换为一组 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象。

这是 [onGenerateInitialRoutes] 的默认值，当 [initialRoute] 不为 null 时会使用它。

如果此字符串以 `/` 字符开头，且其中包含多个 `/` 字符，那么该字符串会在这些字符处被拆分，并依次使用从字符串开头到每个该字符为止的子字符串作为待压入的路由。

例如，如果将路由 `/stocks/HOOLI` 用作 [initialRoute]，那么 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 会在启动时依次压入以下路由：`/`、`/stocks`、`/stocks/HOOLI`。这既支持深层链接，又使应用程序能够维护一个可预测的路由历史记录。

### createState()

```dart
NavigatorState createState()
```

# NavigatorState

```dart
class NavigatorState extends State<Navigator> with TickerProviderStateMixin, RestorationMixin {}
```

[Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 组件的状态。

可以通过调用 [Navigator.of] 来获取对此类的引用。

### focusNode

```dart
FocusNode focusNode
```

包围各路由的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 所对应的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

### initState()

```dart
void initState()
```

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

### didToggleBucket()

```dart
void didToggleBucket(RestorationBucket? oldBucket)
```

### restorationId

```dart
String? get restorationId
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(Navigator oldWidget)
```

### deactivate()

```dart
void deactivate()
```

### activate()

```dart
void activate()
```

### dispose()

```dart
void dispose()
```

### overlay

```dart
OverlayState? get overlay
```

此导航器用于视觉呈现的覆盖层。

### pushNamed()

```dart
Future<T?> pushNamed<T extends Object?>(String routeName, {Object? arguments})
```

将一个具名路由压入导航器。

{@macro flutter.widgets.navigator.pushNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _aaronBurrSir() {
  navigator.pushNamed('/nyc/1776');
}
```

{@end-tool}

另请参阅：

- [restorablePushNamed]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePushNamed()

```dart
String restorablePushNamed<T extends Object?>(String routeName, {Object? arguments})
```

将一个具名路由压入导航器。

{@macro flutter.widgets.navigator.restorablePushNamed}

{@macro flutter.widgets.navigator.pushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _openDetails() {
  navigator.restorablePushNamed('/nyc/1776');
}
```

{@end-tool}

### pushReplacementNamed()

```dart
Future<T?> pushReplacementNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

通过压入名为 [routeName] 的路由，来替换导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _startBike() {
  navigator.pushReplacementNamed('/jouett/1781');
}
```

{@end-tool}

另请参阅：

- [restorablePushReplacementNamed]，它压入一个可以在状态恢复期间被恢复的替换路由。

### restorablePushReplacementNamed()

```dart
String restorablePushReplacementNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

通过压入名为 [routeName] 的路由，来替换导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@macro flutter.widgets.navigator.restorablePushReplacementNamed}

{@macro flutter.widgets.navigator.pushReplacementNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _startCar() {
  navigator.restorablePushReplacementNamed('/jouett/1781');
}
```

{@end-tool}

### popAndPushNamed()

```dart
Future<T?> popAndPushNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

将导航器的当前路由弹出，并在其位置压入一个具名路由。

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _begin() {
  navigator.popAndPushNamed('/nyc/1776');
}
```

{@end-tool}

另请参阅：

- [restorablePopAndPushNamed]，它压入一个可以在状态恢复期间被恢复的新路由。

### restorablePopAndPushNamed()

```dart
String restorablePopAndPushNamed<T extends Object?, TO extends Object?>(String routeName, {TO? result, Object? arguments})
```

将导航器的当前路由弹出，并在其位置压入一个具名路由。

{@macro flutter.widgets.navigator.restorablePopAndPushNamed}

{@macro flutter.widgets.navigator.popAndPushNamed}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _end() {
  navigator.restorablePopAndPushNamed('/nyc/1776');
}
```

{@end-tool}

### pushNamedAndRemoveUntil()

```dart
Future<T?> pushNamedAndRemoveUntil<T extends Object?>(String newRouteName, RoutePredicate predicate, {Object? arguments})
```

将具有给定名称的路由压入导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@macro flutter.widgets.Navigator.pushNamed}

{@tool snippet}

典型用法如下：

```dart
void _handleOpenCalendar() {
  navigator.pushNamedAndRemoveUntil('/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

另请参阅：

- [restorablePushNamedAndRemoveUntil]，它压入一个可以在状态恢复期间被恢复的新路由。

### restorablePushNamedAndRemoveUntil()

```dart
String restorablePushNamedAndRemoveUntil<T extends Object?>(String newRouteName, RoutePredicate predicate, {Object? arguments})
```

将具有给定名称的路由压入导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@macro flutter.widgets.navigator.restorablePushNamedAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamedAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePushNamed.arguments}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _openCalendar() {
  navigator.restorablePushNamedAndRemoveUntil('/calendar', ModalRoute.withName('/'));
}
```

{@end-tool}

### push()

```dart
Future<T?> push<T extends Object?>(Route<T> route)
```

将给定的路由压入导航器。

{@macro flutter.widgets.navigator.push}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _openPage() {
  navigator.push<void>(
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyPage(),
    ),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePush]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePush()

```dart
String restorablePush<T extends Object?>(RestorableRouteBuilder<T> routeBuilder, {Object? arguments})
```

将一个新路由压入导航器。

{@macro flutter.widgets.navigator.restorablePush}

{@macro flutter.widgets.navigator.push}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push.0.dart ** {@end-tool}

### pushReplacement()

```dart
Future<T?> pushReplacement<T extends Object?, TO extends Object?>(Route<T> newRoute, {TO? result})
```

通过压入给定的路由，来替换导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _doOpenPage() {
  navigator.pushReplacement<void, void>(
    MaterialPageRoute<void>(
      builder: (BuildContext context) => const MyHomePage(),
    ),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePushReplacement]，它压入一个可以在状态恢复期间被恢复的替换路由。

### restorablePushReplacement()

```dart
String restorablePushReplacement<T extends Object?, TO extends Object?>(RestorableRouteBuilder<T> routeBuilder, {TO? result, Object? arguments})
```

通过压入一个新路由，来替换导航器的当前路由，并在新路由完成动画进入后释放先前的路由。

{@macro flutter.widgets.navigator.restorablePushReplacement}

{@macro flutter.widgets.navigator.pushReplacement}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push_replacement.0.dart ** {@end-tool}

### pushAndRemoveUntil()

```dart
Future<T?> pushAndRemoveUntil<T extends Object?>(Route<T> newRoute, RoutePredicate predicate)
```

将给定的路由压入导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.navigator.pushNamed.returnValue}

{@tool snippet}

典型用法如下：

```dart
void _resetAndOpenPage() {
  navigator.pushAndRemoveUntil<void>(
    MaterialPageRoute<void>(builder: (BuildContext context) => const MyHomePage()),
    ModalRoute.withName('/'),
  );
}
```

{@end-tool}

另请参阅：

- [restorablePushAndRemoveUntil]，它压入一个可以在状态恢复期间被恢复的路由。

### restorablePushAndRemoveUntil()

```dart
String restorablePushAndRemoveUntil<T extends Object?>(RestorableRouteBuilder<T> newRouteBuilder, RoutePredicate predicate, {Object? arguments})
```

将一个新路由压入导航器，然后移除所有先前的路由，直到 `predicate` 返回 true 为止。

{@macro flutter.widgets.navigator.restorablePushAndRemoveUntil}

{@macro flutter.widgets.navigator.pushAndRemoveUntil}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

{@tool dartpad} 典型用法如下：

** See code in examples/api/lib/widgets/navigator/navigator_state.restorable_push_and_remove_until.0.dart ** {@end-tool}

### replace()

```dart
void replace<T extends Object?>({required Route<dynamic> oldRoute, required Route<T> newRoute})
```

使用一个新路由，替换导航器上的某个路由。

{@macro flutter.widgets.navigator.replace}

另请参阅：

- [replaceRouteBelow]，与此方法相同，但是通过引用待移除路由上方的路由来标识该路由，而非直接标识。
- [restorableReplace]，它添加一个可以在状态恢复期间被恢复的替换路由。

### restorableReplace()

```dart
String restorableReplace<T extends Object?>({required Route<dynamic> oldRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

使用一个新路由，替换导航器上的某个路由。

{@macro flutter.widgets.navigator.restorableReplace}

{@macro flutter.widgets.navigator.replace}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### replaceRouteBelow()

```dart
void replaceRouteBelow<T extends Object?>({required Route<dynamic> anchorRoute, required Route<T> newRoute})
```

使用一个新路由，替换导航器上的某个路由。待替换的路由是位于给定 `anchorRoute` 下方的那个路由。

{@macro flutter.widgets.navigator.replaceRouteBelow}

另请参阅：

- [replace]，与此方法相同，但直接标识待移除的路由。
- [restorableReplaceRouteBelow]，它添加一个可以在状态恢复期间被恢复的替换路由。

### restorableReplaceRouteBelow()

```dart
String restorableReplaceRouteBelow<T extends Object?>({required Route<dynamic> anchorRoute, required RestorableRouteBuilder<T> newRouteBuilder, Object? arguments})
```

使用一个新路由，替换导航器上的某个路由。待替换的路由是位于给定 `anchorRoute` 下方的那个路由。

{@macro flutter.widgets.navigator.restorableReplaceRouteBelow}

{@macro flutter.widgets.navigator.replaceRouteBelow}

{@macro flutter.widgets.Navigator.restorablePush}

{@macro flutter.widgets.Navigator.restorablePushNamed.returnValue}

### canPop()

```dart
bool canPop()
```

导航器是否可以被弹出。

{@macro flutter.widgets.navigator.canPop}

另请参阅：

- [Route.isFirst]，对于 [canPop] 返回 false 的路由，此属性返回 true。

### maybePop()

```dart
Future<bool> maybePop<T extends Object?>([T? result])
```

查询当前路由的 [Route.popDisposition] 方法，并据此采取相应行动，可能会因此弹出该路由；返回该弹出请求是否应被视为已处理。

{@macro flutter.widgets.navigator.maybePop}

另请参阅：

- [Form](https://www.yuque.com/thyname/flutter.widgets/form)，它提供了一个 [Form.canPop] 布尔值，使表单能够阻止由应用返回按钮发起的任何 [pop]。
- [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute)，它提供了一个 `scopedOnPopCallback`，可用于定义该路由的 `willPop` 方法。

### pop()

```dart
void pop<T extends Object?>([T? result])
```

将导航器上最顶层的路由弹出。

{@macro flutter.widgets.navigator.pop}

{@tool snippet}

典型用法如下，用于关闭一个路由：

```dart
void _handleClose() {
  navigator.pop();
}
```

{@end-tool} {@tool snippet}

一个对话框可能会带着一个结果被关闭：

```dart
void _handleAccept() {
  navigator.pop(true); // dialog returns true
}
```

{@end-tool}

### popUntil()

```dart
void popUntil(RoutePredicate predicate)
```

反复调用 [pop]，直到谓词返回 true 为止。

{@macro flutter.widgets.navigator.popUntil}

{@tool snippet}

典型用法如下：

```dart
void _doLogout() {
  navigator.popUntil(ModalRoute.withName('/login'));
}
```

{@end-tool}

### popUntilWithResult()

```dart
void popUntilWithResult<T extends Object?>(RoutePredicate predicate, T? result)
```

反复调用 [pop]，直到谓词返回 true 为止，并将 [result] 返回给最后一个被弹出的路由。

{@macro flutter.widgets.navigator.popUntil}

### removeRoute()

```dart
void removeRoute<T extends Object?>(Route<T> route, [T? result])
```

立即从导航器中移除 `route`，并对其调用 [Route.dispose]。

{@macro flutter.widgets.navigator.removeRoute}

### removeRouteBelow()

```dart
void removeRouteBelow<T extends Object?>(Route<T> anchorRoute, [T? result])
```

立即从导航器中移除一个路由，并对其调用 [Route.dispose]。待移除的路由是位于给定 `anchorRoute` 下方的那个路由。

{@macro flutter.widgets.navigator.removeRouteBelow}

### finalizeRoute()

```dart
void finalizeRoute(Route<dynamic> route)
```

完成已从导航器弹出的路由的生命周期。

当导航器弹出一个路由时，导航器会保留对该路由的引用，以便在导航器自身从组件树中移除时能够调用 [Route.dispose]。当路由完成任何退出动画后，该路由应调用此函数来完成其生命周期（例如，以接收对 [Route.dispose] 的调用）。

给定的 `route` 必须已经收到过对 [Route.didPop] 的调用。如果 [Route.didPop] 将返回 true，此函数可以直接从 [Route.didPop] 内部调用。

### userGestureInProgress

```dart
bool get userGestureInProgress
```

当前是否有路由正在被用户操作，例如在 iOS 返回手势期间。

另请参阅：

- [userGestureInProgressNotifier]，如果 [userGestureInProgress] 的值发生变化，它会通知其监听器。

### userGestureInProgressNotifier

```dart
ValueNotifier<bool> userGestureInProgressNotifier
```

如果 [userGestureInProgress] 的值发生变化，它会通知其监听器。

### didStartUserGesture()

```dart
void didStartUserGesture()
```

导航器正在被用户手势控制。

例如，当用户开始一个 iOS 返回手势时会调用此方法。

手势结束时，请调用 [didStopUserGesture]。

### didStopUserGesture()

```dart
void didStopUserGesture()
```

一个用户手势已完成。

通知导航器，此前通过 [didStartUserGesture] 通知过的手势已经完成。

### build()

```dart
Widget build(BuildContext context)
```

# NavigatorFinderCallback

```dart
typedef NavigatorFinderCallback = NavigatorState Function(BuildContext context)
```

一个根据给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 查找 [NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate) 的回调。

由 [RestorableRouteFuture.navigatorFinder] 使用，以确定新路由应被添加到哪个导航器。

# RoutePresentationCallback

```dart
typedef RoutePresentationCallback = String Function(NavigatorState navigator, Object? arguments)
```

一个根据给定的 `arguments` 和 `navigator`，向该 `navigator` 添加一个新的可恢复路由，并返回该新路由的不透明 ID 的回调。

通常，此回调会调用 Navigator 上方法名中带有 "restorable" 的某个命令式方法，并返回其返回值。

由 [RestorableRouteFuture.onPresent] 使用。

# RouteCompletionCallback

```dart
typedef RouteCompletionCallback<T> = void Function(T result)
```

用于处理已完成 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的结果的回调。

该路由的返回值（对于例如 void 路由，可以为 null）会被传递给此回调。

由 [RestorableRouteFuture.onComplete] 使用。

# RestorableRouteFuture

```dart
class RestorableRouteFuture<T> extends RestorableProperty<String?> {}
```

提供对通过某个“可恢复” API 方法添加到导航器的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象及其返回值的访问。

当某个 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象希望访问它已压入 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象的返回值时，[RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture) 可确保它在状态恢复之后仍然能够访问该值。

要在由 [navigatorFinder] 定义的导航器上显示一个新路由，请调用 [present]，这将会触发 [onPresent] 回调。[onPresent] 回调必须使用某个“可恢复” API 方法，向提供给它的导航器添加一个新路由。当新添加的路由完成时，[onComplete] 回调会被执行。该路由的返回值（可能为 null）会被传递给它。

当通过 [present] 添加的路由显示在导航器上时，可以通过 [route] 获取器来访问它。

如果该属性被恢复到曾对其调用过 [present]、但该路由尚未完成的状态，[RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture) 会再次从导航器获取被恢复的路由对象，并在其完成时调用 [onComplete]。

[RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture) 只能跟踪一个活动的 [route]。当已调用 [present] 添加了一个路由后，只有在先前添加的路由完成之后，才能再次调用 [present]。

{@tool dartpad} 此示例在 `_MyHomeState` 中使用 [RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture) 来压入一个新的 `MyCounter` 路由，并获取其返回值。

** See code in examples/api/lib/widgets/navigator/restorable_route_future.0.dart ** {@end-tool}

### RestorableRouteFuture()

```dart
RestorableRouteFuture({NavigatorFinderCallback navigatorFinder = _defaultNavigatorFinder, required RoutePresentationCallback onPresent, RouteCompletionCallback<T>? onComplete})
```

创建一个 [RestorableRouteFuture](https://www.yuque.com/thyname/flutter.widgets/restorableroutefuture)。

### navigatorFinder

```dart
NavigatorFinderCallback navigatorFinder
```

一个回调，根据此属性所注册到的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，返回将 [onPresent] 中实例化的路由添加到的导航器的 [NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate)。

### onPresent

```dart
RoutePresentationCallback onPresent
```

一个向提供的导航器添加新 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的回调。

该回调必须使用 [NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate) 上方法名中带有 "restorable" 的某个 API 方法（例如 [NavigatorState.restorablePush]、[NavigatorState.restorablePushNamed] 等），并返回这些方法所返回的不透明 ID。

当调用 [present] 时，此回调会被调用，并传入传给该方法的 `arguments` 对象，以及从 [navigatorFinder] 获取的 [NavigatorState](https://www.yuque.com/thyname/flutter.widgets/navigatorstate)。

### onComplete

```dart
RouteCompletionCallback<T>? onComplete
```

当通过 [onPresent] 添加的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 完成时被调用的回调。

该路由的返回值会被传递给此方法。

### present()

```dart
void present([Object? arguments])
```

显示由 [onPresent] 创建的路由，并在其完成时调用 [onComplete]。

`arguments` 对象会被传递给 [onPresent]，可用于自定义该路由。它必须能够通过 [StandardMessageCodec](https://www.yuque.com/thyname/flutter.services/standardmessagecodec) 序列化。通常会使用 [Map](https://www.yuque.com/thyname/dart.core/map) 来传递键值对。

### isPresent

```dart
bool get isPresent
```

由 [present] 创建的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 是否当前正在显示。

从调用 [present] 之后到该 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 完成之前，此值都返回 true。

### route

```dart
Route<T>? get route
```

[present] 添加到 Navigator 的路由。

当前没有路由正在显示时返回 null

### createDefaultValue()

```dart
String? createDefaultValue()
```

### initWithValue()

```dart
void initWithValue(String? value)
```

### toPrimitives()

```dart
Object? toPrimitives()
```

### fromPrimitives()

```dart
String fromPrimitives(Object? data)
```

### dispose()

```dart
void dispose()
```

### enabled

```dart
bool get enabled
```

# NavigationNotification

```dart
class NavigationNotification extends Notification {}
```

表明导航发生了变化的通知。

具体来说，此通知表明发生了以下至少一种情况：

- 某个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的路由堆栈以任何方式发生了变化。
- 弹出能力发生了变化，例如受 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope) 控制。

### NavigationNotification()

```dart
NavigationNotification({required bool canHandlePop})
```

创建一个表明导航发生了某种变化的通知。

### canHandlePop

```dart
bool canHandlePop
```

表明此 [Notification](https://www.yuque.com/thyname/flutter.widgets/notification) 的发起者能够处理导航弹出操作。
