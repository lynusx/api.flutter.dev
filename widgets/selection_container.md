@docImport 'package:flutter/material.dart';

@docImport 'selectable_region.dart';

# SelectionContainer

```dart
class SelectionContainer extends StatefulWidget {}
```

A container that handles [SelectionEvent]s for the [Selectable]s in the subtree.

This widget is useful when one wants to customize selection behaviors for a group of [Selectable]s

The state of this container is a single selectable and will register itself to the [registrar] if provided. Otherwise, it will register to the [SelectionRegistrar] from the context. Consider using a [SelectionArea] widget to provide a root registrar.

The containers handle the [SelectionEvent]s from the registered [SelectionRegistrar] and delegate the events to the [delegate].

This widget uses [SelectionRegistrarScope] to host the [delegate] as the [SelectionRegistrar] for the subtree to collect the [Selectable]s, and [SelectionEvent]s received by this container are sent to the [delegate] using the [SelectionHandler] API of the delegate.

{@tool dartpad} This sample demonstrates how to create a [SelectionContainer] that only allows selecting everything or nothing with no partial selection.

** See code in examples/api/lib/material/selection_container/selection_container.0.dart ** {@end-tool}

See also:

- [SelectableRegion], which provides an overview of the selection system.
- [SelectionContainer.disabled], which disable selection for a subtree.

### SelectionContainer()

```dart
SelectionContainer({dynamic key, SelectionRegistrar? registrar, required SelectionContainerDelegate? delegate, required Widget child})
```

Creates a selection container to collect the [Selectable]s in the subtree.

If [registrar] is not provided, this selection container gets the [SelectionRegistrar] from the context instead.

### SelectionContainer.disabled()

```dart
SelectionContainer.disabled({dynamic key, required Widget child})
```

Creates a selection container that disables selection for the subtree.

{@tool dartpad} This sample demonstrates how to disable selection for a Text under a SelectionArea.

** See code in examples/api/lib/material/selection_container/selection_container_disabled.0.dart ** {@end-tool}

### registrar

```dart
SelectionRegistrar? registrar
```

The [SelectionRegistrar] this container is registered to.

If null, this widget gets the [SelectionRegistrar] from the current context.

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### delegate

```dart
SelectionContainerDelegate? delegate
```

The delegate for [SelectionEvent]s sent to this selection container.

The [Selectable]s in the subtree are added or removed from this delegate using [SelectionRegistrar] API.

This delegate is responsible for updating the selections for the selectables under this widget.

### maybeOf()

```dart
SelectionRegistrar? maybeOf(BuildContext context)
```

Gets the immediate ancestor [SelectionRegistrar] of the [BuildContext].

If this returns null, either there is no [SelectionContainer] above the [BuildContext] or the immediate [SelectionContainer] is not enabled.

### createState()

```dart
State<SelectionContainer> createState()
```

# SelectionRegistrarScope

```dart
class SelectionRegistrarScope extends InheritedWidget {}
```

An inherited widget to host a [SelectionRegistrar] for the subtree.

Use [SelectionContainer.maybeOf] to get the SelectionRegistrar from a context.

This widget is automatically created as part of [SelectionContainer] and is generally not used directly, except for disabling selection for a part of subtree. In that case, one can wrap the subtree with [SelectionContainer.disabled].

### SelectionRegistrarScope()

```dart
SelectionRegistrarScope({dynamic key, required SelectionRegistrar? registrar, required Widget child})
```

Creates a selection registrar scope that host the [registrar].

### registrar

```dart
SelectionRegistrar? registrar
```

The [SelectionRegistrar] hosted by this widget.

### updateShouldNotify()

```dart
bool updateShouldNotify(SelectionRegistrarScope oldWidget)
```

# SelectionContainerDelegate

```dart
abstract class SelectionContainerDelegate implements SelectionHandler, SelectionRegistrar {}
```

A delegate to handle [SelectionEvent]s for a [SelectionContainer].

This delegate needs to implement [SelectionRegistrar] to register [Selectable]s in the [SelectionContainer] subtree.

### getTransformFrom()

```dart
Matrix4 getTransformFrom(Selectable child)
```

Gets the paint transform from the [Selectable] child to [SelectionContainer] of this delegate.

Returns a matrix that maps the [Selectable] paint coordinate system to the coordinate system of [SelectionContainer].

Can only be called after [SelectionContainer] is laid out.

### getTransformTo()

```dart
Matrix4 getTransformTo(RenderObject? ancestor)
```

Gets the paint transform from the [SelectionContainer] of this delegate to the `ancestor`.

Returns a matrix that maps the [SelectionContainer] paint coordinate system to the coordinate system of `ancestor`.

If `ancestor` is null, this method returns a matrix that maps from the local paint coordinate system to the coordinate system of the [PipelineOwner.rootNode].

Can only be called after [SelectionContainer] is laid out.

### hasSize

```dart
bool get hasSize
```

Whether the [SelectionContainer] has undergone layout and has a size.

See also:

- [RenderBox.hasSize], which is used internally by this method.

### containerSize

```dart
Size get containerSize
```

Gets the size of the [SelectionContainer] of this delegate.

Can only be called after [SelectionContainer] is laid out.
