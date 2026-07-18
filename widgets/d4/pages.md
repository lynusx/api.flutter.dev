@docImport 'navigator.dart';

# PageRoute

```dart
abstract class PageRoute<T> extends ModalRoute<T> {}
```

一种替换整个屏幕的模态路由。

[PageRouteBuilder](https://www.yuque.com/thyname/flutter.widgets/pageroutebuilder) 子类提供了一种通过回调而非子类化来创建 [PageRoute](https://www.yuque.com/thyname/flutter.widgets/pageroute) 的方式。

如果 `barrierDismissible` 为 true，则按下键盘上的 Esc 键会使当前路由以 null 作为返回值出栈。

另请参阅：

- [Route](https://www.yuque.com/thyname/flutter.widgets/route)，其中说明了泛型类型参数 `T` 的含义。

### PageRoute()

```dart
PageRoute({RouteSettings? settings, bool? requestFocus, TraversalEdgeBehavior? traversalEdgeBehavior, TraversalEdgeBehavior? directionalTraversalEdgeBehavior, bool fullscreenDialog = false, bool allowSnapshotting = true, bool barrierDismissible = false})
```

创建一个替换整个屏幕的模态路由。

### fullscreenDialog

```dart
bool fullscreenDialog
```

{@template flutter.widgets.PageRoute.fullscreenDialog} 此页面路由是否为全屏对话框。

在 Material 和 Cupertino 中，全屏会使应用栏显示关闭按钮而不是返回按钮。在 iOS 上，对话框的过渡动画有所不同，并且无法通过左滑返回手势关闭。 {@endtemplate}

### allowSnapshotting

```dart
bool allowSnapshotting
```

### opaque

```dart
bool get opaque
```

### barrierDismissible

```dart
bool get barrierDismissible
```

### canTransitionTo()

```dart
bool canTransitionTo(TransitionRoute<dynamic> nextRoute)
```

### canTransitionFrom()

```dart
bool canTransitionFrom(TransitionRoute<dynamic> previousRoute)
```

### popGestureEnabled

```dart
bool get popGestureEnabled
```

# PageRouteBuilder

```dart
class PageRouteBuilder<T> extends PageRoute<T> {}
```

一个用于以回调方式定义一次性页面路由的工具类。

调用方必须定义 [pageBuilder] 函数，用于创建路由的主要内容。若要添加过渡动画，可定义 [transitionsBuilder] 函数。

泛型类型参数 `T` 对应所创建的 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 对象的类型参数。

另请参阅：

- [Route](https://www.yuque.com/thyname/flutter.widgets/route)，其中说明了泛型类型参数 `T` 的含义。

### PageRouteBuilder()

```dart
PageRouteBuilder({RouteSettings? settings, bool? requestFocus, required RoutePageBuilder pageBuilder, RouteTransitionsBuilder transitionsBuilder = _defaultTransitionsBuilder, Duration transitionDuration = const Duration(milliseconds: 300), Duration reverseTransitionDuration = const Duration(milliseconds: 300), bool opaque = true, bool barrierDismissible = false, Color? barrierColor, String? barrierLabel, bool maintainState = true, bool fullscreenDialog, bool allowSnapshotting = true})
```

创建一个委托给构建器回调的路由。

### pageBuilder

```dart
RoutePageBuilder pageBuilder
```

{@template flutter.widgets.pageRouteBuilder.pageBuilder} 用于构建路由的主要内容。

有关这些参数的完整定义，请参阅 [ModalRoute.buildPage]。 {@endtemplate}

### transitionsBuilder

```dart
RouteTransitionsBuilder transitionsBuilder
```

{@template flutter.widgets.pageRouteBuilder.transitionsBuilder} 用于构建路由的过渡动画。

[animation](https://www.yuque.com/thyname/flutter.animation) 参数驱动此路由自身的进入和退出过渡动画。当另一个路由被压入此路由之上，或从此路由之上弹出时（若两个路由都允许过渡协调），[secondaryAnimation] 参数会驱动此路由的过渡动画。请参阅 [TransitionRoute.canTransitionTo] 和 [TransitionRoute.canTransitionFrom]。

有关这些参数的完整定义，请参阅 [ModalRoute.buildTransitions]。 {@endtemplate}

默认的过渡效果是直接跳变（即没有动画）。
