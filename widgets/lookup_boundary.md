@docImport 'package:flutter/material.dart';

# LookupBoundary

```dart
class LookupBoundary extends InheritedWidget {}
```

A lookup boundary controls what entities are visible to descendants of the boundary via the static lookup methods provided by the boundary.

The static lookup methods of the boundary mirror the lookup methods by the same name exposed on [BuildContext] and they can be used as direct replacements. Unlike the methods on [BuildContext], these methods do not find any ancestor entities of the closest [LookupBoundary] surrounding the provided [BuildContext]. The root of the tree is an implicit lookup boundary.

{@tool snippet} In the example below, the [LookupBoundary.findAncestorWidgetOfExactType] call returns null because the [LookupBoundary] "hides" `MyWidget` from the [BuildContext] that was queried.

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

A [LookupBoundary] only affects the behavior of the static lookup methods defined on the boundary. It does not affect the behavior of the lookup methods defined on [BuildContext].

A [LookupBoundary] is rarely instantiated directly. They are inserted at locations of the widget tree where the render tree diverges from the element tree, which is rather uncommon. Such anomalies are created by [RenderObjectElement]s that don't attach their [RenderObject] to the closest ancestor [RenderObjectElement], e.g. because they bootstrap a separate stand-alone render tree. This behavior breaks the assumption some widgets have about the structure of the render tree: These widgets may try to reach out to an ancestor widget, assuming that their associated [RenderObject]s are also ancestors, which due to the anomaly may not be the case. At the point where the divergence in the two trees is introduced, a [LookupBoundary] can be used to hide that ancestor from the querying widget. The [ViewAnchor], for example, wraps its [ViewAnchor.view] child in a [LookupBoundary] because the [RenderObject] produced by that widget subtree is not attached to the render tree that the [ViewAnchor] itself belongs to.

As an example, [Material.of] relies on lookup boundaries to hide the [Material] widget from certain descendant button widget. Buttons reach out to their [Material] ancestor to draw ink splashes on its associated render object. This only produces the desired effect if the button render object is a descendant of the [Material] render object. If the element tree and the render tree are not in sync due to anomalies described above, this may not be the case. To avoid incorrect visuals, the [Material] relies on lookup boundaries to hide itself from descendants in subtrees with such anomalies. Those subtrees are expected to introduce their own [Material] widget that buttons there can utilize without crossing a lookup boundary.

### LookupBoundary()

```dart
LookupBoundary({dynamic key, required Widget child})
```

Creates a [LookupBoundary].

A none-null [child] widget must be provided.

### dependOnInheritedWidgetOfExactType()

```dart
T? dependOnInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context, {Object? aspect})
```

Obtains the nearest widget of the given type `T` within the current [LookupBoundary] of `context`, which must be the type of a concrete [InheritedWidget] subclass, and registers the provided build `context` with that widget such that when that widget changes (or a new widget of that type is introduced, or the widget goes away), the build context is rebuilt so that it can obtain new values from that widget.

This method behaves exactly like [BuildContext.dependOnInheritedWidgetOfExactType], except it only considers [InheritedWidget]s of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [InheritedWidget]s past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.dependOnInheritedWidgetOfExactType}

### getInheritedWidgetOfExactType()

```dart
T? getInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context, {Object? aspect})
```

Obtains the nearest widget of the given type `T` within the current [LookupBoundary] of `context`, which must be the type of a concrete [InheritedWidget] subclass.

This method behaves exactly like [BuildContext.getInheritedWidgetOfExactType], except it only considers [InheritedWidget]s of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [InheritedWidget]s past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.getInheritedWidgetOfExactType}

### getElementForInheritedWidgetOfExactType()

```dart
InheritedElement? getElementForInheritedWidgetOfExactType<T extends InheritedWidget>(BuildContext context)
```

Obtains the element corresponding to the nearest widget of the given type `T` within the current [LookupBoundary] of `context`.

`T` must be the type of a concrete [InheritedWidget] subclass. Returns null if no such element is found.

This method behaves exactly like [BuildContext.getElementForInheritedWidgetOfExactType], except it only considers [InheritedWidget]s of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [InheritedWidget]s past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.getElementForInheritedWidgetOfExactType}

### findAncestorWidgetOfExactType()

```dart
T? findAncestorWidgetOfExactType<T extends Widget>(BuildContext context)
```

Returns the nearest ancestor widget of the given type `T` within the current [LookupBoundary] of `context`.

`T` must be the type of a concrete [Widget] subclass.

This method behaves exactly like [BuildContext.findAncestorWidgetOfExactType], except it only considers [Widget]s of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [Widget]s past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.findAncestorWidgetOfExactType}

### findAncestorStateOfType()

```dart
T? findAncestorStateOfType<T extends State>(BuildContext context)
```

Returns the [State] object of the nearest ancestor [StatefulWidget] widget within the current [LookupBoundary] of `context` that is an instance of the given type `T`.

This method behaves exactly like [BuildContext.findAncestorWidgetOfExactType], except it only considers [State] objects of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [State] objects past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.findAncestorStateOfType}

### findRootAncestorStateOfType()

```dart
T? findRootAncestorStateOfType<T extends State>(BuildContext context)
```

Returns the [State] object of the furthest ancestor [StatefulWidget] widget within the current [LookupBoundary] of `context` that is an instance of the given type `T`.

This method behaves exactly like [BuildContext.findRootAncestorStateOfType], except it considers the closest [LookupBoundary] ancestor of `context` to be the root. [State] objects past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.findRootAncestorStateOfType}

### findAncestorRenderObjectOfType()

```dart
T? findAncestorRenderObjectOfType<T extends RenderObject>(BuildContext context)
```

Returns the [RenderObject] object of the nearest ancestor [RenderObjectWidget] widget within the current [LookupBoundary] of `context` that is an instance of the given type `T`.

This method behaves exactly like [BuildContext.findAncestorRenderObjectOfType], except it only considers [RenderObject]s of the specified type `T` between the provided [BuildContext] and its closest [LookupBoundary] ancestor. [RenderObject]s past that [LookupBoundary] are invisible to this method. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.findAncestorRenderObjectOfType}

### visitAncestorElements()

```dart
void visitAncestorElements(BuildContext context, ConditionalElementVisitor visitor)
```

Walks the ancestor chain, starting with the parent of the build context's widget, invoking the argument for each ancestor until a [LookupBoundary] or the root is reached.

This method behaves exactly like [BuildContext.visitAncestorElements], except it only walks the tree up to the closest [LookupBoundary] ancestor of the provided context. The root of the tree is treated as an implicit lookup boundary.

{@macro flutter.widgets.BuildContext.visitAncestorElements}

### visitChildElements()

```dart
void visitChildElements(BuildContext context, ElementVisitor visitor)
```

Walks the non-[LookupBoundary] child [Element]s of the provided `context`.

This method behaves exactly like [BuildContext.visitChildElements], except it only visits children that are not a [LookupBoundary].

{@macro flutter.widgets.BuildContext.visitChildElements}

### debugIsHidingAncestorWidgetOfExactType()

```dart
bool debugIsHidingAncestorWidgetOfExactType<T extends Widget>(BuildContext context)
```

Returns true if a [LookupBoundary] is hiding the nearest [Widget] of the specified type `T` from the provided [BuildContext].

This method throws when asserts are disabled.

### debugIsHidingAncestorStateOfType()

```dart
bool debugIsHidingAncestorStateOfType<T extends State>(BuildContext context)
```

Returns true if a [LookupBoundary] is hiding the nearest [StatefulWidget] with a [State] of the specified type `T` from the provided [BuildContext].

This method throws when asserts are disabled.

### debugIsHidingAncestorRenderObjectOfType()

```dart
bool debugIsHidingAncestorRenderObjectOfType<T extends RenderObject>(BuildContext context)
```

Returns true if a [LookupBoundary] is hiding the nearest [RenderObjectWidget] with a [RenderObject] of the specified type `T` from the provided [BuildContext].

This method throws when asserts are disabled.

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedWidget oldWidget)
```
