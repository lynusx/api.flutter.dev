@docImport 'package:flutter/material.dart';

# LookupBoundary

```dart
class LookupBoundary extends InheritedWidget {}
```

查找边界（lookup boundary）通过其提供的静态查找方法，控制该边界的后代可以查找到哪些实体。

该边界上的静态查找方法与 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 上同名的查找方法一一对应，可以作为其直接替代品使用。与 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 上的方法不同，这些方法不会查找到最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的任何祖先实体。树的根节点是一个隐式的查找边界。

{@tool snippet} 在下面的示例中，[LookupBoundary.findAncestorWidgetOfExactType] 调用返回 null，因为 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 对被查询的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) "隐藏" 了 `MyWidget`。

```dart
MyWidget(
  child: LookupBoundary(
    child: Builder(
      builder: (BuildContext context) {
        MyWidget? widget = LookupBoundary.findAncestorWidgetOfExactType<MyWidget>(context);
        return Text('$widget'); // "null"
      },
    ),
  ),
)
```

{@end-tool}

[LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 仅影响该边界上定义的静态查找方法的行为，不会影响 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 上定义的查找方法的行为。

[LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 很少被直接实例化。它们通常被插入到渲染树（render tree）与元素树（element tree）发生分歧的位置，这种情况相当少见。此类异常是由不将其 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 附加到最近的祖先 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 的 [RenderObjectElement](https://www.yuque.com/thyname/flutter.widgets/renderobjectelement) 造成的，例如因为它们自行引导（bootstrap）了一个独立的渲染树。这种行为会打破某些组件（widget）对渲染树结构的假设：这些组件可能试图查找某个祖先组件，并假定其关联的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 也是祖先节点，但由于上述异常，实际情况可能并非如此。在两棵树产生分歧的位置，可以使用 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 向发起查询的组件隐藏该祖先节点。例如，[ViewAnchor](https://www.yuque.com/thyname/flutter.widgets/viewanchor) 会将其 [ViewAnchor.view] 子组件包裹在一个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 中，因为该组件子树所产生的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 并未附加到 [ViewAnchor](https://www.yuque.com/thyname/flutter.widgets/viewanchor) 自身所属的渲染树上。

举例来说，[Material.of] 依赖查找边界，将 [Material](https://www.yuque.com/thyname/flutter.material/material) 组件对某些后代按钮组件隐藏。按钮会查找其祖先 [Material](https://www.yuque.com/thyname/flutter.material/material)，以便在其关联的渲染对象上绘制水波纹（ink splash）效果。只有当按钮的渲染对象是 [Material](https://www.yuque.com/thyname/flutter.material/material) 渲染对象的后代时，这一效果才能正确呈现。如果由于上述异常导致元素树与渲染树不同步，情况可能并非如此。为避免出现错误的视觉效果，[Material](https://www.yuque.com/thyname/flutter.material/material) 依赖查找边界，在存在此类异常的子树中向后代隐藏自身。这些子树需要自行引入一个 [Material](https://www.yuque.com/thyname/flutter.material/material) 组件，供其内部的按钮使用，而无需跨越查找边界。

### LookupBoundary()

```dart
LookupBoundary({dynamic key, required Widget child})
```

创建一个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary)。

必须提供一个非空的 [child] 组件。

### dependOnInheritedWidgetOfExactType()

```dart
T? dependOnInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context, {Object? aspect})
```

在 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 的范围内，获取给定类型 `T` 的最近组件，`T` 必须是某个具体 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类的类型，并将提供的构建上下文 `context` 注册到该组件上，以便当该组件发生变化（或引入了新的同类型组件，或该组件被移除）时，该构建上下文会被重建，从而可以从该组件获取新的值。

此方法的行为与 [BuildContext.dependOnInheritedWidgetOfExactType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.dependOnInheritedWidgetOfExactType}

### getInheritedWidgetOfExactType()

```dart
T? getInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context, {Object? aspect})
```

在 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 的范围内，获取给定类型 `T` 的最近组件，`T` 必须是某个具体 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类的类型。

此方法的行为与 [BuildContext.getInheritedWidgetOfExactType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.getInheritedWidgetOfExactType}

### getElementForInheritedWidgetOfExactType()

```dart
InheritedElement? getElementForInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context)
```

获取与 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内、给定类型 `T` 的最近组件相对应的元素。

`T` 必须是某个具体 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 子类的类型。若未找到此类元素，则返回 null。

此方法的行为与 [BuildContext.getElementForInheritedWidgetOfExactType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget)。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.getElementForInheritedWidgetOfExactType}

### findAncestorWidgetOfExactType()

```dart
T? findAncestorWidgetOfExactType<T extends Widget>(BuildContext context)
```

返回 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内、给定类型 `T` 的最近祖先组件。

`T` 必须是某个具体 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 子类的类型。

此方法的行为与 [BuildContext.findAncestorWidgetOfExactType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) 对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.findAncestorWidgetOfExactType}

### findAncestorStateOfType()

```dart
T? findAncestorStateOfType<T extends State>(BuildContext context)
```

返回 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内、最近的祖先 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 中类型为 `T` 的实例的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

此方法的行为与 [BuildContext.findAncestorWidgetOfExactType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.findAncestorStateOfType}

### findRootAncestorStateOfType()

```dart
T? findRootAncestorStateOfType<T extends State>(BuildContext context)
```

返回 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内、最远的祖先 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 中类型为 `T` 的实例的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象。

此方法的行为与 [BuildContext.findRootAncestorStateOfType] 完全相同，区别在于它将 `context` 最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先视为根节点。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 对象对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.findRootAncestorStateOfType}

### findAncestorRenderObjectOfType()

```dart
T? findAncestorRenderObjectOfType<T extends RenderObject>(BuildContext context)
```

返回 `context` 当前 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 范围内、最近的祖先 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget) 中类型为 `T` 的实例的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 对象。

此方法的行为与 [BuildContext.findAncestorRenderObjectOfType] 完全相同，区别在于它只会在提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 与其最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先之间查找指定类型 `T` 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。位于该 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 之外的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 对此方法不可见。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.findAncestorRenderObjectOfType}

### visitAncestorElements()

```dart
void visitAncestorElements(BuildContext context, ConditionalElementVisitor visitor)
```

遍历祖先链，从构建上下文所属组件的父节点开始，对每个祖先节点调用传入的参数，直到到达某个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 或根节点为止。

此方法的行为与 [BuildContext.visitAncestorElements] 完全相同，区别在于它只会遍历到提供的 context 最近的 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 祖先为止。树的根节点被视为一个隐式的查找边界。

{@macro flutter.widgets.BuildContext.visitAncestorElements}

### visitChildElements()

```dart
void visitChildElements(BuildContext context, ElementVisitor visitor)
```

遍历提供的 `context` 中非 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 的子 [Element](https://www.yuque.com/thyname/flutter.widgets/element)。

此方法的行为与 [BuildContext.visitChildElements] 完全相同，区别在于它只会遍历非 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 的子节点。

{@macro flutter.widgets.BuildContext.visitChildElements}

### debugIsHidingAncestorWidgetOfExactType()

```dart
bool debugIsHidingAncestorWidgetOfExactType<T extends Widget>(BuildContext context)
```

如果某个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 对提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 隐藏了指定类型 `T` 的最近 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，则返回 true。

此方法在断言（assert）被禁用时会抛出异常。

### debugIsHidingAncestorStateOfType()

```dart
bool debugIsHidingAncestorStateOfType<T extends State>(BuildContext context)
```

如果某个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 对提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 隐藏了具有指定类型 `T` 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 的最近 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget)，则返回 true。

此方法在断言（assert）被禁用时会抛出异常。

### debugIsHidingAncestorRenderObjectOfType()

```dart
bool debugIsHidingAncestorRenderObjectOfType<T extends RenderObject>(BuildContext context)
```

如果某个 [LookupBoundary](https://www.yuque.com/thyname/flutter.widgets/lookupboundary) 对提供的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 隐藏了具有指定类型 `T` 的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的最近 [RenderObjectWidget](https://www.yuque.com/thyname/flutter.widgets/renderobjectwidget)，则返回 true。

此方法在断言（assert）被禁用时会抛出异常。
