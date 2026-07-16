# RawDialogRouteBuilder

```dart
typedef RawDialogRouteBuilder<T> = Route<T> Function(BuildContext context, WidgetBuilder builder)
```

一个路由构建器，接受构建上下文和要放入该路由中的 Widget 作为参数。

# showRawDialog()

```dart
Future<T?> showRawDialog<T>({required BuildContext context, required WidgetBuilder builder, RawDialogRouteBuilder<T>? routeBuilder, bool useRootNavigator = true, RouteSettings? routeSettings, bool fullscreenDialog = false})
```

在应用内容之上显示一个对话框。

{@template flutter.widgets.showRawDialog.windowing} 如果通过 `flutter config --enable-windowing` 启用了窗口化功能，则该对话框会使用窗口系统在其自己的窗口中显示，而不是作为当前窗口内的模态浮层显示。这仅在支持对话框窗口类型的平台上有效。真正的对话框窗口不会带有遮罩层（barrier）。{@endtemplate}

参数 `builder` 用于构建对话框的内容。

{@template flutter.widgets.showRawDialog.context} `context` 参数用于查找对话框所需的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 和 [Theme](https://www.yuque.com/thyname/flutter.material/theme)。它仅在调用该方法时使用。在对话框关闭之前，可以安全地将其对应的 Widget 从 Widget 树中移除。{@endtemplate}

参数 `routeBuilder` 用于构建将被推入 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的 [Route](https://www.yuque.com/thyname/flutter.widgets/route)。默认构建一个 [RawDialogRoute](https://www.yuque.com/thyname/flutter.widgets/rawdialogroute)。当窗口化功能可用时，此参数将被静默忽略。

{@template flutter.widgets.showRawDialog.navigator} `useRootNavigator` 参数用于确定是将对话框推入距离给定 `context` 最远还是最近的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。默认情况下，`useRootNavigator` 为 `true`，此方法创建的对话框路由会被推入根导航器。它不能为 `null`。{@endtemplate}

{@template flutter.widgets.showRawDialog.routeSettings} `routeSettings` 参数会被传递给 [showGeneralDialog](https://www.yuque.com/thyname/flutter.widgets/showgeneraldialog)，详情请参阅 [RouteSettings](https://www.yuque.com/thyname/flutter.widgets/routesettings)。{@endtemplate}

返回一个 [Future](https://www.yuque.com/thyname/dart.async/future)，当对话框关闭时，该 Future 会解析为传递给 [Navigator.pop] 的值（如果有的话）。

另请参阅：

- `WindowManager`，了解有关如何设置窗口化功能的更多信息。
