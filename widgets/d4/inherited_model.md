@docImport 'package:flutter/foundation.dart';

@docImport 'inherited_notifier.dart';

# InheritedModel

```dart
abstract class InheritedModel<T> extends InheritedWidget {}
```

一个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用作模型的基类，这类模型的依赖者可能只依赖整体模型的某一部分或某个"方面"（aspect）。

根据 [InheritedWidget.updateShouldNotify]，当继承组件（inherited widget）发生变化时，其依赖者会被无条件重建。此组件与之类似，但依赖者不会被无条件重建。

依赖 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel) 的 Widget 会通过一个值来限定其依赖关系，该值表明它们依赖模型的哪个"方面"。当模型重建时，依赖者也会随之重建，但仅当模型中发生的变化与它们所提供的方面相对应时才会重建。

类型参数 `T` 是模型方面对象的类型。

{@youtube 560 315 https://www.youtube.com/watch?v=ml5uefGgkaA}

Widget 通过静态方法 [InheritedModel.inheritFrom] 建立对 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel) 的依赖。该方法的 `context` 参数定义了当模型发生变化时将被重建的子树。通常 `inheritFrom` 方法会在特定于模型的静态 `maybeOf` 或 `of` 方法中被调用，这是许多 Flutter 框架类中用于查找的通用约定。例如：

```dart
class MyModel extends InheritedModel<String> {
  const MyModel({super.key, required super.child});

  // ...
  static MyModel? maybeOf(BuildContext context, [String? aspect]) {
    return InheritedModel.inheritFrom<MyModel>(context, aspect: aspect);
  }

  // ...
  static MyModel of(BuildContext context, [String? aspect]) {
    final MyModel? result = maybeOf(context, aspect);
    assert(result != null, 'Unable to find an instance of MyModel...');
    return result!;
  }
}
```

调用 `MyModel.of(context, 'foo')` 或 `MyModel.maybeOf(context, 'foo')` 意味着 `context` 只应在 `MyModel` 的 `foo` 方面发生变化时才重建。如果 `aspect` 为 null，则该模型支持所有方面。

{@tool snippet} 当继承模型（inherited model）重建时，[updateShouldNotify] 和 [updateShouldNotifyDependent] 方法用于决定应该重建哪些内容。如果 [updateShouldNotify] 返回 true，则会针对每个依赖者及其所依赖的方面对象集合测试该继承模型的 [updateShouldNotifyDependent] 方法。[updateShouldNotifyDependent] 方法必须将方面依赖集合与模型自身的变化进行比较。例如：

```dart
class ABModel extends InheritedModel<String> {
  const ABModel({
   super.key,
   this.a,
   this.b,
   required super.child,
  });

  final int? a;
  final int? b;

  @override
  bool updateShouldNotify(ABModel oldWidget) {
    return a != oldWidget.a || b != oldWidget.b;
  }

  @override
  bool updateShouldNotifyDependent(ABModel oldWidget, Set<String> dependencies) {
    return (a != oldWidget.a && dependencies.contains('a'))
      || (b != oldWidget.b && dependencies.contains('b'));
  }

  // ...
}
```

{@end-tool}

在上面的示例中，[updateShouldNotifyDependent] 所检查的依赖项就是传递给 `dependOnInheritedWidgetOfExactType` 的方面字符串。它们以 [Set](https://www.yuque.com/thyname/dart.core/set) 的形式表示，因为一个 Widget 可以依赖模型的多个方面。如果某个 Widget 依赖该模型但未指定方面，那么模型中的变化将导致该 Widget 被无条件重建。

{@tool dartpad} 此示例展示了如何实现 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel)，以基于限定的依赖关系重建 Widget。点击"Resize Logo"按钮时，只有 logo 组件会被重建，而背景组件不受影响。

** 请参阅 examples/api/lib/widgets/inherited_model/inherited_model.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)：一种仅在其值发生变化时才通知依赖者的继承组件。
- [InheritedNotifier](https://www.yuque.com/thyname/flutter.widgets/inheritednotifier)：一种继承组件，其值可以是 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable)，并且每当该值发出通知时都会通知依赖者。

### InheritedModel()

```dart
InheritedModel({dynamic key, required Widget child})
```

创建一个支持通过"方面"（aspect）限定依赖关系的继承组件，即后代 Widget 可以表明它只应在模型的特定方面发生变化时才重建。

### createElement()

```dart
InheritedModelElement<T> createElement()
```

### updateShouldNotifyDependent()

```dart
bool updateShouldNotifyDependent(InheritedModel<T> oldWidget, Set<T> dependencies)
```

如果此模型与 [oldWidget] 之间的变化与任意 [dependencies] 匹配，则返回 true。

### isSupportedAspect()

```dart
bool isSupportedAspect(Object aspect)
```

如果此模型支持给定的 [aspect]，则返回 true。

默认返回 true：此模型支持所有方面。

子类可以重写此方法，以表明它们不支持所有模型方面。这通常用于模型需要"遮蔽"祖先某些方面的场景。

### inheritFrom()

```dart
T? inheritFrom<T extends InheritedModel<Object>>(BuildContext context, {Object? aspect})
```

使 [context] 依赖于类型为 T 的 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel) 的指定 [aspect]。

当模型的给定 [aspect] 发生变化时，[context] 将被重建。[updateShouldNotifyDependent] 方法必须判断模型组件的变化是否对应于某个 [aspect] 值。

此方法所创建的依赖关系针对的是类型为 T 的所有 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel) 祖先，直到并包括第一个使 [isSupportedAspect] 返回 true 的祖先。

如果 [aspect] 为 null，此方法等同于 `context.dependOnInheritedWidgetOfExactType<T>()`。

如果不存在类型为 T 的祖先，则返回 null。

# InheritedModelElement

```dart
class InheritedModelElement<T> extends InheritedElement {}
```

一个以 [InheritedModel](https://www.yuque.com/thyname/flutter.widgets/inheritedmodel) 作为其配置的 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

### InheritedModelElement()

```dart
InheritedModelElement(InheritedModel<T> widget)
```

创建一个以给定 Widget 作为其配置的 Element。
