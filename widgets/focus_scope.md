@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/semantics.dart';

@docImport 'actions.dart'; @docImport 'container.dart'; @docImport 'editable_text.dart'; @docImport 'focus_traversal.dart'; @docImport 'overlay.dart';

# Focus

```dart
class Focus extends StatefulWidget {}
```

A widget that manages a [FocusNode] to allow keyboard focus to be given to this widget and its descendants.

{@youtube 560 315 https://www.youtube.com/watch?v=JCDfh5bs1xc}

When the focus is gained or lost, [onFocusChange] is called.

For keyboard events, [onKey] and [onKeyEvent] are called if [FocusNode.hasFocus] is true for this widget's [focusNode], unless a focused descendant's [onKey] or [onKeyEvent] callback returned [KeyEventResult.handled] when called.

This widget does not provide any visual indication that the focus has changed. Any desired visual changes should be made when [onFocusChange] is called.

To access the [FocusNode] of the nearest ancestor [Focus] widget and establish a relationship that will rebuild the widget when the focus changes, use the [Focus.of] and [FocusScope.of] static methods.

To access the focused state of the nearest [Focus] widget, use [FocusNode.hasFocus] from a build method, which also establishes a relationship between the calling widget and the [Focus] widget that will rebuild the calling widget when the focus changes.

Managing a [FocusNode] means managing its lifecycle, listening for changes in focus, and re-parenting it when needed to keep the focus hierarchy in sync with the widget hierarchy. This widget does all of those things for you. See [FocusNode] for more information about the details of what node management entails if you are not using a [Focus] widget and you need to do it yourself.

If the [Focus] default constructor is used, then this widget will manage any given [focusNode] by overwriting the appropriate values of the [focusNode] with the values of [FocusNode.onKey], [FocusNode.onKeyEvent], [FocusNode.skipTraversal], [FocusNode.canRequestFocus], and [FocusNode.descendantsAreFocusable] whenever the [Focus] widget is updated.

If the [Focus.withExternalFocusNode] is used instead, then the values returned by [onKey], [onKeyEvent], [skipTraversal], [canRequestFocus], and [descendantsAreFocusable] will be the values in the external focus node, and the external focus node's values will not be overwritten when the widget is updated.

To collect a sub-tree of nodes into an exclusive group that restricts focus traversal to the group, use a [FocusScope]. To collect a sub-tree of nodes into a group that has a specific order to its traversal but allows the traversal to escape the group, use a [FocusTraversalGroup].

To move the focus, use methods on [FocusNode] by getting the [FocusNode] through the [of] method. For instance, to move the focus to the next node in the focus traversal order, call `Focus.of(context).nextFocus()`. To unfocus a widget, call `Focus.of(context).unfocus()`.

{@tool dartpad} This example shows how to manage focus using the [Focus] and [FocusScope] widgets. See [FocusNode] for a similar example that doesn't use [Focus] or [FocusScope].

** See code in examples/api/lib/widgets/focus_scope/focus.0.dart ** {@end-tool}

{@tool dartpad} This example shows how to wrap another widget in a [Focus] widget to make it focusable. It wraps a [Container], and changes the container's color when it is set as the [FocusManager.primaryFocus].

If you also want to handle mouse hover and/or keyboard actions on a widget, consider using a [FocusableActionDetector], which combines several different widgets to provide those capabilities.

** See code in examples/api/lib/widgets/focus_scope/focus.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to focus a newly-created widget immediately after it is created.

The focus node will not actually be given the focus until after the frame in which it has requested focus is drawn, so it is OK to call [FocusNode.requestFocus] on a node which is not yet in the focus tree.

** See code in examples/api/lib/widgets/focus_scope/focus.2.dart ** {@end-tool}

See also:

- [FocusNode], which represents a node in the focus hierarchy and [FocusNode]'s API documentation includes a detailed explanation of its role in the overall focus system.
- [FocusScope], a widget that manages a group of focusable widgets using a [FocusScopeNode].
- [FocusScopeNode], a node that collects focus nodes into a group for traversal.
- [FocusManager], a singleton that manages the primary focus and distributes key events to focused nodes.
- [FocusTraversalPolicy], an object used to determine how to move the focus to other nodes.
- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.

### Focus()

```dart
Focus({dynamic key, required Widget child, FocusNode? focusNode, FocusNode? parentNode, bool autofocus = false, ValueChanged<bool>? onFocusChange, FocusOnKeyEventCallback? onKeyEvent, FocusOnKeyCallback? onKey, bool? canRequestFocus, bool? skipTraversal, bool? descendantsAreFocusable, bool? descendantsAreTraversable, bool includeSemantics = true, String? debugLabel})
```

Creates a widget that manages a [FocusNode].

### Focus.withExternalFocusNode()

```dart
Focus.withExternalFocusNode({Key? key, required Widget child, required FocusNode focusNode, FocusNode? parentNode, bool autofocus, ValueChanged<bool>? onFocusChange, bool includeSemantics})
```

Creates a Focus widget that uses the given [focusNode] as the source of truth for attributes on the node, rather than the attributes of this widget.

### parentNode

```dart
FocusNode? parentNode
```

The optional parent node to use when reparenting the [focusNode] for this [Focus] widget.

If [parentNode] is null, then [Focus.maybeOf] is used to find the parent in the widget tree, which is typically what is desired, since it is easier to reason about the focus tree if it mirrors the shape of the widget tree.

Set this property if the focus tree needs to have a different shape than the widget tree. This is typically in cases where a dialog is in an [Overlay] (or another part of the widget tree), and focus should behave as if the widgets in the overlay are descendants of the given [parentNode] for purposes of focus.

Defaults to null.

### child

```dart
Widget child
```

The child widget of this [Focus].

{@macro flutter.widgets.ProxyWidget.child}

### focusNode

```dart
FocusNode? focusNode
```

{@template flutter.widgets.Focus.focusNode} An optional focus node to use as the focus node for this widget.

If one is not supplied, then one will be automatically allocated, owned, and managed by this widget. The widget will be focusable even if a [focusNode] is not supplied. If supplied, the given [focusNode] will be _hosted_ by this widget, but not owned. See [FocusNode] for more information on what being hosted and/or owned implies.

Supplying a focus node is sometimes useful if an ancestor to this widget wants to control when this widget has the focus. The owner will be responsible for calling [FocusNode.dispose] on the focus node when it is done with it, but this widget will attach/detach and reparent the node when needed. {@endtemplate}

A non-null [focusNode] must be supplied if using the [Focus.withExternalFocusNode] constructor.

### autofocus

```dart
bool autofocus
```

{@template flutter.widgets.Focus.autofocus} True if this widget will be selected as the initial focus when no other node in its scope is currently focused.

Ideally, there is only one widget with autofocus set in each [FocusScope]. If there is more than one widget with autofocus set, then the first one added to the tree will get focus.

Defaults to false. {@endtemplate}

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### onKeyEvent

```dart
FocusOnKeyEventCallback? get onKeyEvent
```

A handler for keys that are pressed when this object or one of its children has focus.

Key events are first given to the [FocusNode] that has primary focus, and if its [onKeyEvent] method returns [KeyEventResult.ignored], then they are given to each ancestor node up the focus hierarchy in turn. If an event reaches the root of the hierarchy, it is discarded.

This is not the way to get text input in the manner of a text field: it leaves out support for input method editors, and doesn't support soft keyboards in general. For text input, consider [TextField], [EditableText], or [CupertinoTextField] instead, which do support these things.

### onKey

```dart
FocusOnKeyCallback? get onKey
```

A handler for keys that are pressed when this object or one of its children has focus.

This property is deprecated and will be removed. Use [onKeyEvent] instead.

Key events are first given to the [FocusNode] that has primary focus, and if its [onKey] method return false, then they are given to each ancestor node up the focus hierarchy in turn. If an event reaches the root of the hierarchy, it is discarded.

This is not the way to get text input in the manner of a text field: it leaves out support for input method editors, and doesn't support soft keyboards in general. For text input, consider [TextField], [EditableText], or [CupertinoTextField] instead, which do support these things.

### canRequestFocus

```dart
bool get canRequestFocus
```

{@template flutter.widgets.Focus.canRequestFocus} If true, this widget may request the primary focus.

Defaults to true. Set to false if you want the [FocusNode] this widget manages to do nothing when [FocusNode.requestFocus] is called on it. Does not affect the children of this node, and [FocusNode.hasFocus] can still return true if this node is the ancestor of the primary focus.

This is different than [Focus.skipTraversal] because [Focus.skipTraversal] still allows the widget to be focused, just not traversed to.

Setting [FocusNode.canRequestFocus] to false implies that the widget will also be skipped for traversal purposes.

See also:

- [FocusTraversalGroup], a widget that sets the traversal policy for its descendants.
- [FocusTraversalPolicy], a class that can be extended to describe a traversal policy. {@endtemplate}

### skipTraversal

```dart
bool get skipTraversal
```

Sets the [FocusNode.skipTraversal] flag on the focus node so that it won't be visited by the [FocusTraversalPolicy].

This is sometimes useful if a [Focus] widget should receive key events as part of the focus chain, but shouldn't be accessible via focus traversal.

This is different from [FocusNode.canRequestFocus] because it only implies that the widget can't be reached via traversal, not that it can't be focused. It may still be focused explicitly.

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

{@template flutter.widgets.Focus.descendantsAreFocusable} If false, will make this widget's descendants unfocusable.

Defaults to true. Does not affect focusability of this node (just its descendants): for that, use [FocusNode.canRequestFocus].

If any descendants are focused when this is set to false, they will be unfocused. When [descendantsAreFocusable] is set to true again, they will not be refocused, although they will be able to accept focus again.

Does not affect the value of [FocusNode.canRequestFocus] on the descendants.

If a descendant node loses focus when this value is changed, the focus will move to the scope enclosing this node.

See also:

- [ExcludeFocus], a widget that uses this property to conditionally exclude focus for a subtree.
- [descendantsAreTraversable], which makes this widget's descendants untraversable.
- [ExcludeFocusTraversal], a widget that conditionally excludes focus traversal for a subtree.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that has a `descendantsAreFocusable` parameter to conditionally block focus for a subtree. {@endtemplate}

### descendantsAreTraversable

```dart
bool get descendantsAreTraversable
```

{@template flutter.widgets.Focus.descendantsAreTraversable} If false, will make this widget's descendants untraversable.

Defaults to true. Does not affect traversability of this node (just its descendants): for that, use [FocusNode.skipTraversal].

Does not affect the value of [FocusNode.skipTraversal] on the descendants. Does not affect focusability of the descendants.

See also:

- [ExcludeFocusTraversal], a widget that uses this property to conditionally exclude focus traversal for a subtree.
- [descendantsAreFocusable], which makes this widget's descendants unfocusable.
- [ExcludeFocus], a widget that conditionally excludes focus for a subtree.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that has a `descendantsAreFocusable` parameter to conditionally block focus for a subtree. {@endtemplate}

### includeSemantics

```dart
bool includeSemantics
```

{@template flutter.widgets.Focus.includeSemantics} Include semantics information in this widget.

If true, this widget will include a [Semantics] node that indicates the [SemanticsProperties.focusable] and [SemanticsProperties.focused] properties.

It is not typical to set this to false, as that can affect the semantics information available to accessibility systems.

Defaults to true. {@endtemplate}

### debugLabel

```dart
String? get debugLabel
```

A debug label for this widget.

Not used for anything except to be printed in the diagnostic output from [toString] or [toStringDeep].

To get a string with the entire tree, call [debugDescribeFocusTree]. To print it to the console call [debugDumpFocusTree].

Defaults to null.

### of()

```dart
FocusNode of(BuildContext context, {bool scopeOk = false, bool createDependency = true})
```

Returns the [focusNode] of the [Focus] that most tightly encloses the given [BuildContext].

If no [Focus] node is found before reaching the nearest [FocusScope] widget, or there is no [Focus] widget in the context, then this method will throw an exception.

{@macro flutter.widgets.focus_scope.Focus.maybeOf}

See also:

- [maybeOf], which is similar to this function, but will return null instead of throwing if it doesn't find a [Focus] node.

### maybeOf()

```dart
FocusNode? maybeOf(BuildContext context, {bool scopeOk = false, bool createDependency = true})
```

Returns the [focusNode] of the [Focus] that most tightly encloses the given [BuildContext].

If no [Focus] node is found before reaching the nearest [FocusScope] widget, or there is no [Focus] widget in scope, then this method will return null.

{@template flutter.widgets.focus_scope.Focus.maybeOf} If `createDependency` is true (which is the default), calling this function creates a dependency that will rebuild the given context when the focus node gains or loses focus. {@endtemplate}

See also:

- [of], which is similar to this function, but will throw an exception if it doesn't find a [Focus] node, instead of returning null.

### isAt()

```dart
bool isAt(BuildContext context)
```

Returns true if the nearest enclosing [Focus] widget's node is focused.

A convenience method to allow build methods to write: `Focus.isAt(context)` to get whether or not the nearest [Focus] above them in the widget hierarchy currently has the input focus.

Returns false if no [Focus] widget is found before reaching the nearest [FocusScope], or if the root of the focus tree is reached without finding a [Focus] widget.

Calling this function creates a dependency that will rebuild the given context when the focus changes.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createState()

```dart
State<Focus> createState()
```

# FocusScope

```dart
class FocusScope extends Focus {}
```

A [FocusScope] is similar to a [Focus], but also serves as a scope for its descendants, restricting focus traversal to the scoped controls.

For example a new [FocusScope] is created automatically when a route is pushed, keeping the focus traversal from moving to a control in a previous route.

If you just want to group widgets together in a group so that they are traversed in a particular order, but the focus can still leave the group, use a [FocusTraversalGroup].

Like [Focus], [FocusScope] provides an [onFocusChange] as a way to be notified when the focus is given to or removed from this widget.

The [onKey] argument allows specification of a key event handler that is invoked when this node or one of its children has focus. Keys are handed to the primary focused widget first, and then they propagate through the ancestors of that node, stopping if one of them returns [KeyEventResult.handled] from [onKey], indicating that it has handled the event.

Managing a [FocusScopeNode] means managing its lifecycle, listening for changes in focus, and re-parenting it when needed to keep the focus hierarchy in sync with the widget hierarchy. This widget does all of those things for you. See [FocusScopeNode] for more information about the details of what node management entails if you are not using a [FocusScope] widget and you need to do it yourself.

[FocusScopeNode]s remember the last [FocusNode] that was focused within their descendants, and can move that focus to the next/previous node, or a node in a particular direction when the [FocusNode.nextFocus], [FocusNode.previousFocus], or [FocusNode.focusInDirection] are called on a [FocusNode] or [FocusScopeNode].

To move the focus, use methods on [FocusNode] by getting the [FocusNode] through the [of] method. For instance, to move the focus to the next node in the focus traversal order, call `Focus.of(context).nextFocus()`. To unfocus a widget, call `Focus.of(context).unfocus()`.

{@tool dartpad} This example demonstrates using a [FocusScope] to restrict focus to a particular portion of the app. In this case, restricting focus to the visible part of a Stack.

** See code in examples/api/lib/widgets/focus_scope/focus_scope.0.dart ** {@end-tool}

See also:

- [FocusScopeNode], which represents a scope node in the focus hierarchy.
- [FocusNode], which represents a node in the focus hierarchy and has an explanation of the focus system.
- [Focus], a widget that manages a [FocusNode] and allows easy access to managing focus without having to manage the node.
- [FocusManager], a singleton that manages the focus and distributes key events to focused nodes.
- [FocusTraversalPolicy], an object used to determine how to move the focus to other nodes.
- [FocusTraversalGroup], a widget used to configure the focus traversal policy for a widget subtree.

### FocusScope()

```dart
FocusScope({dynamic key, FocusScopeNode? node, FocusNode? parentNode, required Widget child, bool autofocus, dynamic onFocusChange, bool? canRequestFocus, bool? skipTraversal, KeyEventResult Function(FocusNode, InvalidType)? onKeyEvent, KeyEventResult Function(FocusNode, InvalidType)? onKey, String? debugLabel, bool includeSemantics, bool? descendantsAreFocusable, bool? descendantsAreTraversable})
```

Creates a widget that manages a [FocusScopeNode].

### FocusScope.withExternalFocusNode()

```dart
FocusScope.withExternalFocusNode({Key? key, required Widget child, required FocusScopeNode focusScopeNode, FocusNode? parentNode, bool autofocus, bool includeSemantics, ValueChanged<bool>? onFocusChange})
```

Creates a FocusScope widget that uses the given [focusScopeNode] as the source of truth for attributes on the node, rather than the attributes of this widget.

### of()

```dart
FocusScopeNode of(BuildContext context, {bool createDependency = true})
```

Returns the [FocusNode.nearestScope] of the [Focus] or [FocusScope] that most tightly encloses the given [context].

If this node doesn't have a [Focus] or [FocusScope] widget ancestor, then the [FocusManager.rootScope] is returned.

{@macro flutter.widgets.focus_scope.Focus.maybeOf}

### createState()

```dart
State<Focus> createState()
```

# ExcludeFocus

```dart
class ExcludeFocus extends StatelessWidget {}
```

A widget that controls whether or not the descendants of this widget are focusable.

Does not affect the value of [Focus.canRequestFocus] on the descendants.

See also:

- [Focus], a widget for adding and managing a [FocusNode] in the widget tree.
- [FocusTraversalGroup], a widget that groups widgets for focus traversal, and can also be used in the same way as this widget by setting its `descendantsAreFocusable` attribute.

### ExcludeFocus()

```dart
ExcludeFocus({dynamic key, bool excluding = true, required Widget child})
```

Const constructor for [ExcludeFocus] widget.

### excluding

```dart
bool excluding
```

If true, will make this widget's descendants unfocusable.

Defaults to true.

If any descendants are focused when this is set to true, they will be unfocused. When [excluding] is set to false again, they will not be refocused, although they will be able to accept focus again.

Does not affect the value of [FocusNode.canRequestFocus] on the descendants.

See also:

- [Focus.descendantsAreFocusable], the attribute of a [Focus] widget that controls this same property for focus widgets.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that has a `descendantsAreFocusable` parameter to conditionally block focus for a subtree.

### child

```dart
Widget child
```

The child widget of this [ExcludeFocus].

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```
