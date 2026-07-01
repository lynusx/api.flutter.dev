@docImport 'package:flutter/material.dart';

# SlottedMultiChildRenderObjectWidget

```dart
abstract class SlottedMultiChildRenderObjectWidget<SlotType, ChildType extends RenderObject> extends RenderObjectWidget with SlottedMultiChildRenderObjectWidgetMixin<SlotType, ChildType> {}
```

A superclass for [RenderObjectWidget]s that configure [RenderObject] subclasses that organize their children in different slots.

Implementers of this mixin have to provide the list of available slots by overriding [slots]. The list of slots must never change for a given class implementing this mixin. In the common case, [Enum] values are used as slots and [slots] is typically implemented to return the value of the enum's `values` getter.

Furthermore, [childForSlot] must be implemented to return the current widget configuration for a given slot.

The [RenderObject] returned by [createRenderObject] and updated by [updateRenderObject] must implement [SlottedContainerRenderObjectMixin].

The type parameter `SlotType` is the type for the slots to be used by this [RenderObjectWidget] and the [RenderObject] it configures. In the typical case, `SlotType` is an [Enum] type.

The type parameter `ChildType` is the type used for the [RenderObject] children (e.g. [RenderBox] or [RenderSliver]). In the typical case, `ChildType` is [RenderBox]. This class does not support having different kinds of children for different slots.

{@tool dartpad} This example uses the [SlottedMultiChildRenderObjectWidget] in combination with the [SlottedContainerRenderObjectMixin] to implement a widget that provides two slots: topLeft and bottomRight. The widget arranges the children in those slots diagonally.

** See code in examples/api/lib/widgets/slotted_render_object_widget/slotted_multi_child_render_object_widget_mixin.0.dart ** {@end-tool}

See also:

- [MultiChildRenderObjectWidget], which configures a [RenderObject] with a single list of children.
- [ListTile], which uses [SlottedMultiChildRenderObjectWidget] in its internal (private) implementation.

### SlottedMultiChildRenderObjectWidget()

```dart
SlottedMultiChildRenderObjectWidget({dynamic key})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

# SlottedMultiChildRenderObjectWidgetMixin

```dart
mixin SlottedMultiChildRenderObjectWidgetMixin<SlotType, ChildType extends RenderObject> on RenderObjectWidget {}
```

A mixin version of [SlottedMultiChildRenderObjectWidget].

This mixin provides the same logic as extending [SlottedMultiChildRenderObjectWidget] directly.

It was deprecated to simplify the process of creating slotted widgets.

### slots

```dart
Iterable<SlotType> get slots
```

Returns a list of all available slots.

The list of slots must be static and must never change for a given class implementing this mixin.

Typically, an [Enum] is used to identify the different slots. In that case this getter can be implemented by returning what the `values` getter of the enum used returns.

### childForSlot()

```dart
Widget? childForSlot(SlotType slot)
```

Returns the widget that is currently occupying the provided `slot`.

The [RenderObject] configured by this class will be configured to have the [RenderObject] produced by the returned [Widget] in the provided `slot`.

### createRenderObject()

```dart
SlottedContainerRenderObjectMixin<SlotType, ChildType> createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, SlottedContainerRenderObjectMixin<SlotType, ChildType> renderObject)
```

### createElement()

```dart
SlottedRenderObjectElement<SlotType, ChildType> createElement()
```

# SlottedContainerRenderObjectMixin

```dart
mixin SlottedContainerRenderObjectMixin<SlotType, ChildType extends RenderObject> on RenderObject {}
```

Mixin for a [RenderObject] configured by a [SlottedMultiChildRenderObjectWidget].

The [RenderObject] child currently occupying a given slot can be obtained by calling [childForSlot].

Implementers may consider overriding [children] to return the children of this render object in a consistent order (e.g. hit test order).

The type parameter `SlotType` is the type for the slots to be used by this [RenderObject] and the [SlottedMultiChildRenderObjectWidget] it was configured by. In the typical case, `SlotType` is an [Enum] type.

The type parameter `ChildType` is the type of [RenderObject] used for the children (e.g. [RenderBox] or [RenderSliver]). In the typical case, `ChildType` is [RenderBox]. This mixin does not support having different kinds of children for different slots.

See [SlottedMultiChildRenderObjectWidget] for example code showcasing how this mixin is used in combination with [SlottedMultiChildRenderObjectWidget].

See also:

- [ContainerRenderObjectMixin], which organizes its children in a single list.

### childForSlot()

```dart
ChildType? childForSlot(SlotType slot)
```

Returns the [RenderObject] child that is currently occupying the provided `slot`.

Returns null if no [RenderObject] is configured for the given slot.

### children

```dart
Iterable<ChildType> get children
```

Returns an [Iterable] of all non-null children.

This getter is used by the default implementation of [attach], [detach], [redepthChildren], [visitChildren], and [debugDescribeChildren] to iterate over the children of this [RenderObject]. The base implementation makes no guarantee about the order in which the children are returned. Subclasses for which the child order is important should override this getter and return the children in the desired order.

### debugNameForSlot()

```dart
String debugNameForSlot(SlotType slot)
```

Returns the debug name for a given `slot`.

This method is called by [debugDescribeChildren] for each slot that is currently occupied by a child to obtain a name for that slot for debug outputs.

The default implementation calls [EnumName.name] on `slot` if it is an [Enum] value and `toString` if it is not.

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# SlottedRenderObjectElement

```dart
class SlottedRenderObjectElement<SlotType, ChildType extends RenderObject> extends RenderObjectElement {}
```

Element used by the [SlottedMultiChildRenderObjectWidget].

### SlottedRenderObjectElement()

```dart
SlottedRenderObjectElement(SlottedMultiChildRenderObjectWidgetMixin<SlotType, ChildType> widget)
```

Creates an element that uses the given widget as its configuration.

### renderObject

```dart
SlottedContainerRenderObjectMixin<SlotType, ChildType> get renderObject
```

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
void update(SlottedMultiChildRenderObjectWidgetMixin<SlotType, ChildType> newWidget)
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(ChildType child, SlotType slot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(ChildType child, SlotType slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(ChildType child, SlotType oldSlot, SlotType newSlot)
```
