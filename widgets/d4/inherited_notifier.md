@docImport 'package:flutter/animation.dart'; @docImport 'package:flutter/rendering.dart';

@docImport 'inherited_model.dart'; @docImport 'scroll_position.dart';

# InheritedNotifier

```dart
abstract class InheritedNotifier<T extends Listenable> extends InheritedWidget {}
```

一个用于 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) [notifier] 的继承组件，当 [notifier] 被触发时会更新其依赖者。

这是 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 的一种变体，专门用于 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 的子类，例如 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier) 或 [ValueNotifier](https://www.yuque.com/thyname/flutter.foundation/valuenotifier)。

每当 [notifier] 发出通知、或 [notifier] 本身的标识发生变化时，依赖者都会收到通知。

多次通知会被合并处理，因此即使 [notifier] 在两帧之间多次触发，依赖者也只会重建一次。

通常此类会被子类化，并提供一个 `of` 静态方法，该方法通过该子类调用 [BuildContext.dependOnInheritedWidgetOfExactType]。

[updateShouldNotify] 方法也可以被重写，以改变 [notifier] 本身发生变化时的判断逻辑。当 [notifier] 发生变化时，会以旧的 [notifier] 作为参数调用 [updateShouldNotify] 方法。当该方法返回 true 时，依赖者会被标记为需要在当前帧重建。

{@tool dartpad} 此示例展示了三个旋转的方块，它们使用祖先 [InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier)（`SpinModel`）上 notifier 的值来确定各自的旋转角度。[InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier) 不需要了解其子组件，`notifier` 参数也不需要是动画控制器，它可以是任何实现了 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 的对象（例如 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier)）。

`SpinModel` 类同样可以轻松地监听另一个对象（例如，一个保存输入或数据模型值的独立对象），只要该对象是 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 即可，并从中获取值。后代组件同样不需要持有 [InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier) 的实例即可使用它，它们只需要知道其祖先中存在一个即可。这有助于将 Widget 与其模型解耦。

** 请参阅 examples/api/lib/widgets/inherited_notifier/inherited_notifier.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [Animation](https://www.yuque.com/thyname/flutter.animation/animation)：[Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 的一种实现，每帧都会触发以更新一个值。
- [ViewportOffset](https://www.yuque.com/thyname/flutter.rendering/viewportoffset) 及其子类 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition)：[Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 的实现，在视图滚动时触发。
- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)：一种仅在其值发生变化时才通知依赖者的继承组件。
- [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)：一种允许客户端订阅其值的某些子部分变化的继承组件。

### InheritedNotifier()

```dart
InheritedNotifier({dynamic key, T? notifier, required Widget child})
```

创建一个继承组件，当 [notifier] 发出通知时更新其依赖者。

### notifier

```dart
T? notifier
```

要监听的 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 对象。

每当该对象发出变更通知时，都会触发此 Widget 的依赖者。

默认情况下，每当 [notifier] 发生变化（包括变为 null 或从 null 变化而来）时，如果旧的 notifier 与新的 notifier 不相等（由 `==` 运算符判定），就会发出通知。此行为可以通过重写 [updateShouldNotify] 来改变。

当 [notifier] 为 null 时，不会发出任何通知，因为 null 对象本身无法发出通知。
