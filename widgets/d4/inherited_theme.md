@docImport 'package:flutter/material.dart';

# InheritedTheme

```dart
abstract class InheritedTheme extends InheritedWidget {}
```

一个 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)，用于定义颜色和文本样式等视觉属性，[child] 的子树依赖于这些属性。

[wrap] 方法被 [captureAll] 和 [CapturedThemes.wrap] 使用，用于构建一个将 child 包裹在指定部分 Widget 树中所有存在的继承主题（inherited theme）中的 Widget。

在与构建时不同的上下文中显示的 Widget（例如新路由或 overlay 中的内容）将能够看到其构建时所在上下文的祖先继承主题。

{@tool dartpad} 此示例演示了如何使用 `InheritedTheme.capture()` 将新路由的内容包裹在路由构建时存在的继承主题中——即使在路由实际显示时这些主题已不存在。

如果在不使用 `InheritedTheme.capture()` 的情况下运行相同代码，新路由的 Text 组件将继承"something must be wrong"这一后备文本样式，而不是 MyApp 中定义的默认文本样式。

** 请参阅 examples/api/lib/widgets/inherited_theme/inherited_theme.0.dart 中的代码 ** {@end-tool}

### InheritedTheme()

```dart
InheritedTheme({dynamic key, required Widget child})
```

抽象 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

返回此继承主题的一个副本，并指定 [child]。

以下是 [TooltipTheme](https://www.yuque.com/thyname/flutter.material/tooltiptheme) 的典型实现：

```dart
Widget wrap(BuildContext context, Widget child) {
  return TooltipTheme(data: data, child: child);
}
```

### captureAll()

```dart
Widget captureAll(BuildContext context, Widget child, {BuildContext? to})
```

返回一个 Widget，它会将 `child` 包裹在 `context` 与指定的 `to` [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 之间存在的所有继承主题中（[wrap]）。

`to` 上下文必须是 `context` 的祖先。如果未指定 `to`，则会捕获直到 Widget 树根节点为止的所有继承主题。

调用此方法后，`context` 与 `to` 之间存在的主题会针对所提供的 `child` 被冻结。如果原始子树中的主题（或其主题数据）发生变化，这些变化将不会反映到已包裹的 `child` 中——除非再次调用此方法以重新包裹 child。

### capture()

```dart
CapturedThemes capture({required BuildContext from, required BuildContext? to})
```

返回一个 [CapturedThemes](https://www.yuque.com/thyname/flutter.widgets/capturedthemes) 对象，其中包含给定的 `from` 与 `to` [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 之间的所有 [InheritedTheme](https://www.yuque.com/thyname/flutter.widgets/inheritedtheme)。

`to` 上下文必须是 `from` 上下文的祖先。如果 `to` 为 null，则会捕获 `from` 直到 Widget 树根节点为止的所有祖先继承主题。

调用此方法后，`from` 与 `to` 之间存在的主题会在返回的 [CapturedThemes](https://www.yuque.com/thyname/flutter.widgets/capturedthemes) 对象中被冻结。如果原始子树中的主题（或其主题数据）发生变化，这些变化不会应用到 [CapturedThemes](https://www.yuque.com/thyname/flutter.widgets/capturedthemes) 对象中已捕获的主题——除非再次调用此方法以重新捕获更新后的主题。

要将某个 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 包裹在已捕获的主题中，请调用 [CapturedThemes.wrap]。

如果 `from` 与 `to` 之间存在大量 Widget，此方法可能开销较大（它会遍历这两个节点之间的 element 树）。

# CapturedThemes

```dart
class CapturedThemes {}
```

存储一个已捕获的 [InheritedTheme](https://www.yuque.com/thyname/flutter.widgets/inheritedtheme) 列表，可以将其包裹在某个子 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 外部。

作为 [InheritedTheme.capture] 的返回类型使用。

### wrap()

```dart
Widget wrap(Widget child)
```

将一个 `child` [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 包裹在此对象中已捕获的 [InheritedTheme](https://www.yuque.com/thyname/flutter.widgets/inheritedtheme) 中。
