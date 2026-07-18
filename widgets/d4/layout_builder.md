@docImport 'basic.dart'; @docImport 'single_child_scroll_view.dart'; @docImport 'sliver_layout_builder.dart';

# LayoutWidgetBuilder

```dart
typedef LayoutWidgetBuilder = Widget Function(BuildContext context, BoxConstraints constraints)
```

[LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 的 builder 函数的签名。

# AbstractLayoutBuilder

```dart
abstract class AbstractLayoutBuilder<LayoutInfoType> extends RenderObjectWidget {}
```

一个抽象的父类，用于将其构建过程推迟到布局阶段的 Widget。

与 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件类似，不同之处在于其实现会在布局阶段调用 [builder] 函数，并提供配置子组件子树所需的 [LayoutInfoType]。

当子组件树依赖于仅在布局阶段才可用的信息、且不依赖于子组件的固有尺寸时，此类非常有用。

[LayoutInfoType] 通常应是不可变的。该实现使用 [LayoutInfoType] 的相等性来避免不必要的重建：如果布局阶段计算出的新 [LayoutInfoType] 与之前的 [LayoutInfoType] 相同（由 `LayoutInfoType.==` 定义），则该实现会尝试避免再次调用 [builder]，除非 [updateShouldRebuild] 返回 true。由此产生的对应 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 会保留最新的 [LayoutInfoType]，用于此目的，这可能会使某个 [LayoutInfoType] 对象在 Widget 从树中移除之前一直保留在内存中。

子类必须返回一个混入了 [RenderAbstractLayoutBuilderMixin](https://www.yuque.com/thyname/flutter.widgets/renderabstractlayoutbuildermixin) 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

### AbstractLayoutBuilder()

```dart
AbstractLayoutBuilder({dynamic key})
```

创建一个将其构建过程推迟到布局阶段的 Widget。

### builder

```dart
Widget Function(BuildContext context, LayoutInfoType layoutInfo) get builder
```

在布局阶段被调用以构建 Widget 树。

builder 不能返回 null。

### createElement()

```dart
RenderObjectElement createElement()
```

### updateShouldRebuild()

```dart
bool updateShouldRebuild(AbstractLayoutBuilder<LayoutInfoType> oldWidget)
```

即使布局约束相同，是否仍需要再次调用 [builder]。

当此 Widget 的配置被更新时，通常需要调用 [builder] 回调来构建此 Widget 的 child。但是，子类可以提供无需重建 child 即可更新 Widget 的方式。此类子类可以使用此方法来告知框架何时应重建 child Widget。

当框架调用此方法时，新配置的 Widget 会被询问是否需要重建，并将旧 Widget 作为参数传入。

另请参阅：

- [State.setState] 和 [State.didUpdateWidget]：介绍了 Widget 配置变化及其触发方式。
- [Element.update]：实际更新 Widget 配置的方法。

### createRenderObject()

```dart
RenderAbstractLayoutBuilderMixin<LayoutInfoType, RenderObject> createRenderObject(BuildContext context)
```

# ConstrainedLayoutBuilder

```dart
abstract class ConstrainedLayoutBuilder<ConstraintType extends Constraints> extends AbstractLayoutBuilder<ConstraintType> {}
```

一种特殊化的 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder)，其 Widget 子树依赖于将要施加于该 Widget 的传入 [ConstraintType]。

{@template flutter.widgets.ConstrainedLayoutBuilder} 在以下情况下会调用 [builder] 函数：

- Widget 首次进行布局时。
- 父组件传入不同的布局约束时。
- 父组件更新此 Widget 且 [updateShouldRebuild] 返回 `true` 时。
- [builder] 函数所订阅的依赖项发生变化时。

如果父组件重复传入相同的约束，则在布局期间不会调用 [builder] 函数。

如果某个祖先跳过了此子树的布局，导致约束过时，则 `builder` 会使用最后已知的约束进行重建。{@endtemplate}

### ConstrainedLayoutBuilder()

```dart
ConstrainedLayoutBuilder({dynamic key, required Widget Function(BuildContext context, ConstraintType constraints) builder})
```

创建一个将其构建过程推迟到布局阶段的 Widget。

### builder

```dart
Widget Function(BuildContext context, ConstraintType constraints) builder
```

# RenderAbstractLayoutBuilderMixin

```dart
mixin RenderAbstractLayoutBuilderMixin<LayoutInfoType, ChildType extends RenderObject> on RenderObjectWithChildMixin<ChildType>, RenderObjectWithLayoutCallbackMixin {}
```

用于由具有相同 `LayoutInfoType` 的 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder) 所创建的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的通用 mixin。

提供了一个 [layoutCallback] 实现，该实现会在需要时调用 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder) 的 builder 回调。

实现者可以重写 [layoutInfo] 实现，提供一个可以在 [layoutCallback]（在 [performLayout] 中调用）中安全访问的值。默认的 [layoutInfo] 返回传入的 [Constraints](https://www.yuque.com/thyname/flutter.rendering/constraints)。

此 mixin 取代了 [RenderConstrainedLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/renderconstrainedlayoutbuilder)。

改变布局回调。

### layoutCallback()

```dart
void layoutCallback()
```

调用通过 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder) 提供的 builder 回调，并在需要时重建 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder) 的 Widget 树。

如果自上次调用此方法以来 [layoutInfo] 未发生变化，且在 Widget 重建时 [AbstractLayoutBuilder.updateShouldRebuild] 返回了 `false`，则不会执行进一步的操作。

此方法通常应尽早在类的 [performLayout] 实现中被调用，且需在进行任何布局工作之前调用。

### layoutInfo

```dart
LayoutInfoType get layoutInfo
```

用于调用 [AbstractLayoutBuilder.builder] 回调的信息。

这通常是仅在 [performLayout] 中才可用的信息，例如传入的 [Constraints](https://www.yuque.com/thyname/flutter.rendering/constraints)（默认值），而常规 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件无法访问这些信息。

# RenderConstrainedLayoutBuilder

```dart
typedef RenderConstrainedLayoutBuilder<LayoutInfoType, ChildType extends RenderObject> = RenderAbstractLayoutBuilderMixin<LayoutInfoType, ChildType>
```

用于由具有相同 `LayoutInfoType` 的 [AbstractLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/abstractlayoutbuilder) 所创建的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的通用 mixin。

请改用 [RenderAbstractLayoutBuilderMixin](https://www.yuque.com/thyname/flutter.widgets/renderabstractlayoutbuildermixin)，它取代了此 mixin。

# LayoutBuilder

```dart
class LayoutBuilder extends ConstrainedLayoutBuilder<BoxConstraints> {}
```

构建一个可以依赖于父组件尺寸的 Widget 树。

与 [Builder](https://www.yuque.com/thyname/flutter.widgets/builder) 组件类似，不同之处在于框架会在布局阶段调用 [builder] 函数，并提供父组件的约束。当父组件限制了 child 的尺寸、且不依赖于 child 的固有尺寸时，此类非常有用。[LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 的最终尺寸将与其 child 的尺寸一致。

{@macro flutter.widgets.ConstrainedLayoutBuilder}

{@youtube 560 315 https://www.youtube.com/watch?v=IYDVcriKjsw}

如果 child 应该比父组件小，可以考虑将 child 包裹在 [Align](https://www.yuque.com/thyname/flutter.widgets/align) 组件中。如果 child 可能需要更大，可以考虑将其包裹在 [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview) 或 [OverflowBox](https://www.yuque.com/thyname/flutter.widgets/overflowbox) 中。

{@tool dartpad} 此示例使用 [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 根据可用宽度构建不同的 Widget。调整 DartPad 窗口大小即可查看 [LayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/layoutbuilder) 的实际效果！

** 请参阅 examples/api/lib/widgets/layout_builder/layout_builder.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [SliverLayoutBuilder](https://www.yuque.com/thyname/flutter.widgets/sliverlayoutbuilder)：此组件对应的 sliver 版本。
- [Builder](https://www.yuque.com/thyname/flutter.widgets/builder)：在构建阶段调用 `builder` 函数。
- [StatefulBuilder](https://www.yuque.com/thyname/flutter.widgets/statefulbuilder)：将 `setState` 回调传递给其 `builder` 函数。
- [CustomSingleChildLayout](https://www.yuque.com/thyname/flutter.widgets/customsinglechildlayout)：在布局阶段定位其 child。
- [布局组件目录](https://flutter.dev/widgets/layout/)。

### LayoutBuilder()

```dart
LayoutBuilder({dynamic key, required Widget Function(BuildContext, InvalidType) builder})
```

创建一个将其构建过程推迟到布局阶段的 Widget。
