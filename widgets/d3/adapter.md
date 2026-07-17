@docImport 'binding.dart';

# RenderObjectToWidgetAdapter

```dart
class RenderObjectToWidgetAdapter<T extends RenderObject> extends RenderObjectWidget {}
```

从 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 到 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树的桥梁。

给定的 container 是 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树应插入其中的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。它必须是实现了 [RenderObjectWithChildMixin](https://www.yuque.com/thyname/flutter.rendering/renderobjectwithchildmixin) 协议的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。类型参数 `T` 是 container 期望作为其子节点的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 类型。

[RenderObjectToWidgetAdapter](https://www.yuque.com/thyname/flutter.widgets/renderobjecttowidgetadapter) 是 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 的替代方案，用于引导构建 element 树。与 [RootWidget](https://www.yuque.com/thyname/flutter.widgets/rootwidget) 不同，它需要存在一个渲染树（即 [container]）以便将 element 树附加到其上。

### RenderObjectToWidgetAdapter()

```dart
RenderObjectToWidgetAdapter({Widget? child, required RenderObjectWithChildMixin<T> container, String? debugShortDescription})
```

创建一个从 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 到 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树的桥梁。

### child

```dart
Widget? child
```

此 Widget 下方的子 Widget。

{@macro flutter.widgets.ProxyWidget.child}

### container

```dart
RenderObjectWithChildMixin<T> container
```

作为此 Widget 所创建的 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 的父节点的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)。

### debugShortDescription

```dart
String? debugShortDescription
```

调试工具使用的此 Widget 的简短描述。

### attachToRenderTree()

```dart
RenderObjectToWidgetElement<T> attachToRenderTree(BuildOwner owner, [RenderObjectToWidgetElement<T>? element])
```

膨胀（inflate）此 Widget，并将生成的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 实际设置为 [container] 的子节点。

如果 `element` 为 null，此函数将创建一个新的 element。否则，给定的 element 将安排一次更新，以切换到此 Widget。

# RenderObjectToWidgetElement

```dart
class RenderObjectToWidgetElement<T extends RenderObject> extends RenderTreeRootElement with RootElementMixin {}
```

由 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 承载的 element 树的根节点。

此 element 类是 [RenderObjectToWidgetAdapter](https://www.yuque.com/thyname/flutter.widgets/renderobjecttowidgetadapter) Widget 的实例化。它只能用作 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 树的根节点（不能被挂载到另一个 [Element](https://www.yuque.com/thyname/flutter.widgets/element) 中；其父节点必须为 null）。

在典型用法中，它将为 container 是 [RenderView](https://www.yuque.com/thyname/flutter.rendering/renderview) 的 [RenderObjectToWidgetAdapter](https://www.yuque.com/thyname/flutter.widgets/renderobjecttowidgetadapter) 实例化。

### RenderObjectToWidgetElement()

```dart
RenderObjectToWidgetElement(RenderObjectToWidgetAdapter<T> widget)
```

创建一个由 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 承载的 element。

此 element 创建的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 不会自动设置为承载它的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的子节点。要将此 element 实际附加到渲染树，请调用 [RenderObjectToWidgetAdapter.attachToRenderTree]。
