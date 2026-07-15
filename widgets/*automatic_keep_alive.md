@docImport 'scroll_delegate.dart'; @docImport 'scroll_view.dart';

# AutomaticKeepAlive

```dart
class AutomaticKeepAlive extends StatefulWidget {}
```

允许子树请求在惰性列表中保持存活。

此组件类似于 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive)，但它不是通过显式配置，而是通过监听来自 [child] 及其他后代的 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 消息来工作的。

只要有一个或多个后代发送了 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 且尚未触发其 [KeepAliveNotification.handle]，该子树就会被保持存活。

若要发送这些通知，可考虑使用 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin)。

与 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist) 和 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid) 一起使用的 [SliverChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/sliverchildbuilderdelegate) 和 [SliverChildListDelegate](https://www.yuque.com/thyname/flutter.widgets/sliverchildlistdelegate) 委托，以及对应的滚动视图 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 和 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)，都具有默认启用的 `addAutomaticKeepAlives` 功能。该功能会在每个子组件周围插入 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件，这些组件又会根据 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 来配置 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) 组件。

[TwoDimensionalChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/twodimensionalchildbuilderdelegate) 和 [TwoDimensionalChildListDelegate](https://www.yuque.com/thyname/flutter.widgets/twodimensionalchildlistdelegate) 也支持相同的 `addAutomaticKeepAlives` 功能。

{@tool dartpad} 此示例演示了如何将 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件与 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin) 结合使用，以选择性地保留可滚动列表中各个条目的状态。

通常，为了维持性能，[ListView.builder] 这类惰性构建列表中的组件在离开可见区域时会被释放。这意味着 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 内部的任何状态都会丢失，除非被显式保留。

在此示例中，每个列表项都是一个包含计数器和递增按钮的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)。为了保留（根据索引）选定条目的状态，使用了 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件和 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin)：

- 条目状态类中的 `wantKeepAlive` 获取器对偶数索引的条目返回 true，表示应保留其状态。
- 对于奇数索引的条目，`wantKeepAlive` 返回 false，因此它们滚出视图时状态不会被保留。

** 请参阅 examples/api/lib/widgets/keep_alive/automatic_keep_alive.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin)，一个为 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 的使用方提供便捷方法的混入（mixin）。与 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类一起使用。
- [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive)，它标记一个子组件即使处于原本会将其移除的惰性列表中，也需要保持存活。

### AutomaticKeepAlive()

```dart
AutomaticKeepAlive({dynamic key, required Widget child})
```

创建一个监听 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 并相应维护一个 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) 组件的组件。

### child

```dart
Widget child
```

树中位于此组件下方的组件。

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<AutomaticKeepAlive> createState()
```

# KeepAliveNotification

```dart
class KeepAliveNotification extends Notification {}
```

表示此通知所冒泡经过的子树必须保持存活，即使它通常会作为一种优化而被丢弃。

例如，一个获得焦点的文本字段可能会发出此通知，表示即使用户将该字段滚出屏幕，它也不应被释放。

每个 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 都配置有一个 [handle]，它由一个在子树不再需要保持存活时会被触发的 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 组成。

每当发送该通知的组件从树中移除时（在 [State.deactivate] 中），都应触发 [handle]。若该组件随后被重建且仍需要保持存活，则应在构建期间立即发送一个新的通知（可以使用同一个 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)）。

此通知由 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件监听，该组件会由 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)（及 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)）和 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)（及 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)）组件自动添加到树中。

若未能按上述方式触发 [handle]，很可能会导致 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 无法正确追踪该组件是否应保持存活，从而导致内存泄漏或数据丢失。例如，若请求保持存活的组件从子树中移除，但在移除过程中未触发其 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)，则该子树将持续保持存活，直到列表本身被释放为止。同样，若 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 在组件仍需要保持存活时被触发，但没有立即发送新的 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification)，则该组件在仍希望保持存活的情况下有被垃圾回收的风险。

在同一个 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 内，若在发送第二个通知之前未触发该 [handle]，却在两个 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 中使用同一个 [handle]，则属于错误用法。

若需要更便捷地与 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件交互，可考虑使用内部使用 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 的 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin)。

### KeepAliveNotification()

```dart
KeepAliveNotification(Listenable handle)
```

创建一个表示子树必须保持存活的通知。

### handle

```dart
Listenable handle
```

一个 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)，当发出该通知的组件不再需要保持存活时，会通知其使用方。

每当发送组件从树中移除时（在 [State.deactivate] 中），都应触发该 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)。若该组件随后被重建且仍需要保持存活，则应在构建期间立即发送一个新的通知（可以使用同一个 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)）。

另请参阅：

- [KeepAliveHandle](https://www.yuque.com/thyname/flutter.widgets/keepalivehandle)，一个与此属性配合使用的便捷类。

# KeepAliveHandle

```dart
class KeepAliveHandle extends ChangeNotifier {}
```

一个可手动触发的 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)。

与 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 对象配合使用，作为其 [KeepAliveNotification.handle]。

若需要更便捷地与 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件交互，可考虑使用内部使用 [KeepAliveHandle](https://www.yuque.com/thyname/flutter.widgets/keepalivehandle) 的 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin)。

### dispose()

```dart
void dispose()
```

# AutomaticKeepAliveClientMixin

```dart
mixin AutomaticKeepAliveClientMixin<T extends StatefulWidget> on State<T> {}
```

一个为 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 的使用方提供便捷方法的混入（mixin）。它与 [State](https://www.yuque.com/thyname/flutter.widgets/state) 子类一起使用，以管理惰性构建列表中的保持存活行为。

此混入通过在必要时自动发送 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 来简化与 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 的交互。子类必须实现 [wantKeepAlive] 以指示该组件是否应保持存活，并在其值发生变化时调用 [updateKeepAlive]。

此混入内部管理一个 [KeepAliveHandle](https://www.yuque.com/thyname/flutter.widgets/keepalivehandle)，用于将保持存活需求的变化通知给最近的 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 祖先。[AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 会监听此混入发送的 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification)，并动态地用 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) 组件包装该子树，以便在其不再于视口中可见时保留其状态。

子类必须实现 [wantKeepAlive]，并且其 [build] 方法必须调用 `super.build`（不过其返回值应被忽略）。

之后，每当 [wantKeepAlive] 的值发生变化（或可能发生变化）时，子类都应调用 [updateKeepAlive]。

类型参数 `T` 是被混入此类的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 所对应的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 子类的类型。

与 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist) 和 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid) 一起使用的 [SliverChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/sliverchildbuilderdelegate) 和 [SliverChildListDelegate](https://www.yuque.com/thyname/flutter.widgets/sliverchildlistdelegate) 委托，以及对应的滚动视图 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 和 [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)，都具有默认启用的 `addAutomaticKeepAlives` 功能。该功能会在每个子组件周围插入 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 组件，这些组件又会根据 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 来配置 [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive) 组件。

[TwoDimensionalChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/twodimensionalchildbuilderdelegate) 和 [TwoDimensionalChildListDelegate](https://www.yuque.com/thyname/flutter.widgets/twodimensionalchildlistdelegate) 也支持相同的 `addAutomaticKeepAlives` 功能。

{@tool dartpad} 此示例演示了如何使用 [AutomaticKeepAliveClientMixin](https://www.yuque.com/thyname/flutter.widgets/automatickeepaliveclientmixin) 来使组件的状态即使在滚出视图后仍保持存活。

** 请参阅 examples/api/lib/widgets/keep_alive/automatic_keep_alive_client_mixin.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive)，它监听来自此混入的消息。
- [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification)，此混入发送的通知。
- [KeepAlive](https://www.yuque.com/thyname/flutter.widgets/keepalive)，它标记一个子组件即使处于原本会将其移除的惰性列表中，也需要保持存活。

### wantKeepAlive

```dart
bool get wantKeepAlive
```

当前实例是否应保持存活。

每当此获取器的值发生变化时，都应调用 [updateKeepAlive]。

### updateKeepAlive()

```dart
void updateKeepAlive()
```

通过按需发出 [KeepAliveNotification](https://www.yuque.com/thyname/flutter.widgets/keepalivenotification) 或触发 [KeepAliveHandle](https://www.yuque.com/thyname/flutter.widgets/keepalivehandle)，确保任何 [AutomaticKeepAlive](https://www.yuque.com/thyname/flutter.widgets/automatickeepalive) 祖先都处于良好状态。

### initState()

```dart
void initState()
```

### deactivate()

```dart
void deactivate()
```

### build()

```dart
Widget build(BuildContext context)
```
