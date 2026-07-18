# NavigatorPopHandler

```dart
class NavigatorPopHandler<T> extends StatefulWidget {}
```

支持处理系统返回手势。

通常包装一个嵌套的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) Widget，使其能够在 [onPopWithResult] 回调中处理系统返回手势。

类型参数 `<T>` 表示 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 返回值的类型，该值会被传递给 [onPopWithResult]。

{@tool dartpad} 此示例演示了如何使用此 Widget，在使用嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 时正确处理系统返回手势。

** 请参阅 examples/api/lib/widgets/navigator_pop_handler/navigator_pop_handler.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 此示例演示了如何使用此 Widget，在使用底部导航栏（其每个标签页均拥有各自的嵌套 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)）时正确处理系统返回手势。

** 请参阅 examples/api/lib/widgets/navigator_pop_handler/navigator_pop_handler.1.dart 中的代码 ** {@end-tool}

另请参阅：

- [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope)，可用于切换 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 处理弹出（pop）操作的能力。
- [NavigationNotification](https://www.yuque.com/thyname/flutter.widgets/navigationnotification)，指示子树中的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 是否可以处理弹出操作。

### NavigatorPopHandler()

```dart
NavigatorPopHandler({dynamic key, VoidCallback? onPop, PopResultCallback<T>? onPopWithResult, bool enabled = true, required Widget child})
```

创建一个 [NavigatorPopHandler](https://www.yuque.com/thyname/flutter.widgets/navigatorpophandler) 实例。

### child

```dart
Widget child
```

放置在此 Widget 下方的 Widget 树中的 Widget。

通常这是一个 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，它将在调用 [onPopWithResult] 时处理弹出操作。

### enabled

```dart
bool enabled
```

此 Widget 处理系统返回手势的能力是启用还是禁用。

当为 false 时，将不会对系统返回手势产生任何影响。如果提供了 [onPop]，仍会调用它。

例如，当嵌套的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 不再处于活动状态但仍保留在 Widget 树中时（例如处于非活动标签页中），可以使用此选项。

默认为 true。

### onPop

```dart
VoidCallback? onPop
```

当发生可处理的弹出事件时调用。

例如，当 [child] 中的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的堆栈上有多个路由时，弹出操作是可处理的。当堆栈上只有单个路由时，弹出操作则不可处理，因此不会调用 [onPop]。

通常用于弹出 [child] 中的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。有关完整示例，请参阅 [NavigatorPopHandler](https://www.yuque.com/thyname/flutter.widgets/navigatorpophandler) 上的示例代码。

### onPopWithResult

```dart
PopResultCallback<T>? onPopWithResult
```

当发生可处理的弹出事件时调用。

例如，当 [child] 中的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator) 的堆栈上有多个路由时，弹出操作是可处理的。当堆栈上只有单个路由时，弹出操作则不可处理，因此不会调用 [onPopWithResult]。

通常用于弹出 [child] 中的 [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)。有关完整示例，请参阅 [NavigatorPopHandler](https://www.yuque.com/thyname/flutter.widgets/navigatorpophandler) 上的示例代码。

传入的 `result` 是被弹出 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的结果。

### createState()

```dart
State<NavigatorPopHandler<T>> createState()
```

# PopResultCallback

```dart
typedef PopResultCallback<T> = void Function(T? result)
```

用于表示一个函数的签名，该函数接收 [Route](https://www.yuque.com/thyname/flutter.widgets/route) 的结果作为参数。
