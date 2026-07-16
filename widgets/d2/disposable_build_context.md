# DisposableBuildContext

```dart
class DisposableBuildContext<T extends State> {}
```

提供对 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的非泄漏访问。

只有当 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 指向一个活动的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 时，它才是有效的。一旦该 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 被卸载，就不应再访问该 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)。此类使 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 能够安全地与其他对象共享其构建上下文。

此对象的创建者必须保证以下几点：

1. 在 [State.initState] 之后、[State.dispose] 之前创建此对象。特别地，不要尝试在 State 的构造函数中创建此对象。
2. 在 [State.dispose] 中调用 [dispose]。

此对象在释放后不会继续持有该 [State](https://www.yuque.com/thyname/flutter.widgets/state)。

### DisposableBuildContext()

```dart
DisposableBuildContext(T? _state)
```

创建一个对象，用于在不泄漏 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的情况下提供对 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的访问。

创建者必须在该 [State](https://www.yuque.com/thyname/flutter.widgets/state) 被释放时调用 [dispose]。

[State.mounted] 必须为 true。

### context

```dart
BuildContext? get context
```

提供对构建上下文的安全访问。

如果已调用 [dispose]，则返回 null。

否则，断言 [_state] 仍处于挂载状态，并返回其构建上下文。

### dispose()

```dart
void dispose()
```

将该 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 标记为已释放。

此对象的创建者必须在其 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 被卸载时（即调用 [State.dispose] 时）调用 [dispose]。
