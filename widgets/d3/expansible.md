@docImport 'package:flutter/material.dart';

# ExpansibleComponentBuilder

```dart
typedef ExpansibleComponentBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

用于返回 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 的头部或主体的回调类型。

`animation` 属性暴露了底层的展开或折叠动画，当 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 完全折叠时其值为 0，完全展开时其值为 1。该属性可用于驱动与展开/折叠动画同步的动画效果，例如旋转图标。

参见：

- [Expansible.headerBuilder]，属于此类型。
- [Expansible.bodyBuilder]，同样属于此类型。

# ExpansibleBuilder

```dart
typedef ExpansibleBuilder = Widget Function(BuildContext context, Widget header, Widget body, Animation<double> animation)
```

用于使用 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 的头部和主体构建该 widget 的回调类型。

`header` 属性是由 [Expansible.headerBuilder] 返回的头部。`body` 属性是由 [Expansible.bodyBuilder] 返回并包裹在 [Offstage](https://www.yuque.com/thyname/flutter.widgets/offstage) 中的主体，用于在 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 折叠时隐藏该主体。

`animation` 属性暴露了底层的展开或折叠动画，当 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 完全折叠时其值为 0，完全展开时其值为 1。该属性可用于驱动与展开/折叠动画同步的动画效果，例如旋转图标。

参见：

- [Expansible.expansibleBuilder]，属于此类型。

# ExpansibleController

```dart
class ExpansibleController extends ChangeNotifier {}
```

用于管理 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 展开状态的控制器。

此类是一个 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier)，当 [isExpanded] 的值发生变化时会通知其监听器。

该控制器提供了以编程方式展开或折叠 widget 的方法，并允许外部组件查询当前的展开状态。

调用控制器的 [expand] 和 [collapse] 方法会导致 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 重建，因此不能在 build 方法中调用它们。

请记得在不再需要 [ExpansibleController](https://www.yuque.com/thyname/flutter.widgets/expansiblecontroller) 时调用 [dispose]，以确保释放该对象使用的所有资源。

### ExpansibleController()

```dart
ExpansibleController()
```

创建一个用于 [Expansible.controller] 的控制器。

### isExpanded

```dart
bool get isExpanded
```

使用此控制器构建的可展开 widget 是否处于展开状态。

此属性不考虑动画过程。即使展开动画尚未完成，它也会返回 `true`。

如需在此属性发生变化时收到通知，可使用 [ExpansibleController.addListener] 为控制器添加监听器。

参见：

- [expand]，用于展开该可展开 widget。
- [collapse]，用于折叠该可展开 widget。

### expand()

```dart
void expand()
```

展开使用此控制器构建的 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)。

如果该 widget 已经处于展开状态（参见 [isExpanded]），调用此方法不会产生任何效果。

调用此方法可能会导致 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 重建，因此不能在 build 方法中调用它。

调用此方法会通知该控制器的已注册监听器展开状态已发生变化。

参见：

- [collapse]，用于折叠该可展开 widget。
- [isExpanded]，用于检查该可展开 widget 是否已展开。

### collapse()

```dart
void collapse()
```

折叠使用此控制器构建的 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)。

如果该 widget 已经处于折叠状态（参见 [isExpanded]），调用此方法不会产生任何效果。

调用此方法可能会导致 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 重建，因此不能在 build 方法中调用它。

调用此方法会通知该控制器的已注册监听器展开状态已发生变化。

参见：

- [expand]，用于展开 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)。
- [isExpanded]，用于检查 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 是否已展开。

### toggle()

```dart
void toggle()
```

用于切换当前 [isExpanded] 状态的便捷方法。

调用此方法可能会导致 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 重建，因此不能在 build 方法中调用它。

调用此方法会通知该控制器的已注册监听器展开状态已发生变化。

参见：

- [expand]，用于展开 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)。
- [collapse]，用于折叠 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)。
- [isExpanded]，用于检查 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 是否已展开。

### of()

```dart
ExpansibleController of(BuildContext context)
```

查找与给定 context 最近的 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 实例所对应的 [ExpansibleController](https://www.yuque.com/thyname/flutter.widgets/expansiblecontroller)。

如果给定 context 的祖先中没有 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)，在调试模式下调用此方法会触发断言，在发布模式下则会抛出异常。

如需在没有 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 时返回 null，请改用 [maybeOf]。

[ExpansibleController.of] 函数的典型用法是在 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 后代组件的 `build` 方法中调用它。

### maybeOf()

```dart
ExpansibleController? maybeOf(BuildContext context)
```

查找与给定 context 最近的此类实例所对应的 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)，并返回其 [ExpansibleController](https://www.yuque.com/thyname/flutter.widgets/expansiblecontroller)。

如果给定 context 的祖先中没有 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible)，则返回 null。如需改为抛出异常，请使用 [of] 而非此函数。

参见：

- [of]，与此函数类似，但在没有 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 包含给定 context 时会抛出异常。

# Expansible

```dart
class Expansible extends StatefulWidget {}
```

一个可以展开和折叠的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)。

[Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 由一个始终显示的头部和一个主体组成，主体在折叠状态下隐藏，在展开状态下显示。

[Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 通过由 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 驱动的动画来实现展开或折叠。当该 widget 展开时，其主体的高度会从 0 动画过渡到完全展开时的高度。

此组件通常与 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 结合使用，以创建“展开/折叠”列表项。当与 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 等可滚动组件一起使用时，必须为 [key] 指定唯一的 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，以便 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 在滚动移出和移入视图时能够保存和恢复其展开状态。

提供 [headerBuilder] 和 [bodyBuilder] 回调以构建头部和主体 widget。还可以提供额外的 [expansibleBuilder] 回调，以进一步自定义该 widget 的布局。

[Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 本身不会自动切换展开状态。要切换展开状态，需要在合适的时机（通常是 [headerBuilder] 返回的头部被点击时）调用 [ExpansibleController.expand] 和 [ExpansibleController.collapse]。

{@tool dartpad} 此示例演示了如何使用 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) widget，以及如何使用 [ExpansibleController](https://www.yuque.com/thyname/flutter.widgets/expansiblecontroller) 以编程方式展开或折叠它。

** 参见 examples/api/lib/material/expansible/expansible.0.dart 中的代码 ** {@end-tool}

参见：

- [ExpansionTile](https://www.yuque.com/thyname/flutter.material/expansiontile)，一个具有 Material 风格的可展开折叠 widget。

### Expansible()

```dart
Expansible({dynamic key, required ExpansibleComponentBuilder headerBuilder, required ExpansibleComponentBuilder bodyBuilder, required ExpansibleController controller, ExpansibleBuilder expansibleBuilder = _defaultExpansibleBuilder, AnimationStyle? animationStyle, Duration duration = const Duration(milliseconds: 200), Curve curve = Curves.ease, Curve? reverseCurve, bool maintainState = true})
```

创建一个 [Expansible](https://www.yuque.com/thyname/flutter.widgets/expansible) 实例。

### controller

```dart
ExpansibleController controller
```

用于展开和折叠该 widget。

该控制器负责管理展开状态并切换展开操作。

### headerBuilder

```dart
ExpansibleComponentBuilder headerBuilder
```

构建始终显示的头部。

在许多使用场景中，点击此头部会切换展开状态。要切换展开状态，可调用 [ExpansibleController.expand] 或 [ExpansibleController.collapse]。

### bodyBuilder

```dart
ExpansibleComponentBuilder bodyBuilder
```

构建可折叠的主体。

当此 widget 展开时，其主体的高度会从 0 动画过渡到完全展开的高度。

### animationStyle

```dart
AnimationStyle? animationStyle
```

用于覆盖展开动画的曲线和时长。

如果提供了 [AnimationStyle.duration]，则会使用它而不是 [duration]。如果未提供，则使用 [duration]，其默认值为 200 毫秒。

如果提供了 [AnimationStyle.curve]，则会用它覆盖 [curve]。如果为 null，则使用 [curve]，默认值为 [Curves.ease]。

如果提供了 [AnimationStyle.reverseCurve]，则会用它覆盖 [reverseCurve]。如果为 null，则使用 [reverseCurve]。

如需禁用主题动画，请使用 [AnimationStyle.noAnimation]。

### duration

```dart
Duration duration
```

展开动画的时长。

默认值为 200 毫秒。

此属性已弃用，请改用 [animationStyle]。

### curve

```dart
Curve curve
```

展开动画的曲线。

默认值为 [Curves.ease]。

此属性已弃用，请改用 [animationStyle]。

### reverseCurve

```dart
Curve? reverseCurve
```

展开动画的反向曲线。

如果为 null，则两个方向均使用 [curve]。

此属性已弃用，请改用 [animationStyle]。

### maintainState

```dart
bool maintainState
```

该 widget 在展开或折叠时是否保持主体的状态。

如果为 true，则在该 widget 折叠时主体仍保留在组件树中；否则，主体会在该 widget 折叠时从组件树中移除，并在展开时重新创建。

默认值为 true。

### expansibleBuilder

```dart
ExpansibleBuilder expansibleBuilder
```

使用 [headerBuilder] 和 [bodyBuilder] 的结果构建该 widget。

默认将头部和主体放置在一个 [Column](https://www.yuque.com/thyname/flutter.widgets/column) 中。
