@docImport 'binding.dart';

# RenderObjectToWidgetAdapter

```dart
class RenderObjectToWidgetAdapter<T extends RenderObject> extends RenderObjectWidget {}
```

A bridge from a [RenderObject] to an [Element] tree.

The given container is the [RenderObject] that the [Element] tree should be inserted into. It must be a [RenderObject] that implements the [RenderObjectWithChildMixin] protocol. The type argument `T` is the kind of [RenderObject] that the container expects as its child.

The [RenderObjectToWidgetAdapter] is an alternative to [RootWidget] for bootstrapping an element tree. Unlike [RootWidget] it requires the existence of a render tree (the [container]) to attach the element tree to.

### RenderObjectToWidgetAdapter()

```dart
RenderObjectToWidgetAdapter({Widget? child, required RenderObjectWithChildMixin<T> container, String? debugShortDescription})
```

Creates a bridge from a [RenderObject] to an [Element] tree.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### container

```dart
RenderObjectWithChildMixin<T> container
```

The [RenderObject] that is the parent of the [Element] created by this widget.

### debugShortDescription

```dart
String? debugShortDescription
```

A short description of this widget used by debugging aids.

### createElement()

```dart
RenderObjectToWidgetElement<T> createElement()
```

### createRenderObject()

```dart
RenderObjectWithChildMixin<T> createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderObject renderObject)
```

### attachToRenderTree()

```dart
RenderObjectToWidgetElement<T> attachToRenderTree(BuildOwner owner, [RenderObjectToWidgetElement<T>? element])
```

Inflate this widget and actually set the resulting [RenderObject] as the child of [container].

If `element` is null, this function will create a new element. Otherwise, the given element will have an update scheduled to switch to this widget.

### toStringShort()

```dart
String toStringShort()
```

# RenderObjectToWidgetElement

```dart
class RenderObjectToWidgetElement<T extends RenderObject> extends RenderTreeRootElement with RootElementMixin {}
```

The root of an element tree that is hosted by a [RenderObject].

This element class is the instantiation of a [RenderObjectToWidgetAdapter] widget. It can be used only as the root of an [Element] tree (it cannot be mounted into another [Element]; it's parent must be null).

In typical usage, it will be instantiated for a [RenderObjectToWidgetAdapter] whose container is the [RenderView].

### RenderObjectToWidgetElement()

```dart
RenderObjectToWidgetElement(RenderObjectToWidgetAdapter<T> widget)
```

Creates an element that is hosted by a [RenderObject].

The [RenderObject] created by this element is not automatically set as a child of the hosting [RenderObject]. To actually attach this element to the render tree, call [RenderObjectToWidgetAdapter.attachToRenderTree].

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(RenderObjectToWidgetAdapter<T> newWidget)
```

### performRebuild()

```dart
void performRebuild()
```

### renderObject

```dart
RenderObjectWithChildMixin<T> get renderObject
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, Object? slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, Object? oldSlot, Object? newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, Object? slot)
```
