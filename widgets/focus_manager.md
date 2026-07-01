@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart';

# debugFocusChanges

```dart
bool debugFocusChanges
```

Setting to true will cause extensive logging to occur when focus changes occur.

Can be used to debug focus issues: each time the focus changes, the focus tree will be printed and requests for focus and other focus operations will be logged.

# KeyEventResult

```dart
enum KeyEventResult {}
```

An enum that describes how to handle a key event handled by a [FocusOnKeyCallback] or [FocusOnKeyEventCallback].

The key event has been handled, and the event should not be propagated to other key event handlers.

The key event has not been handled, and the event should continue to be propagated to other key event handlers, even non-Flutter ones.

The key event has not been handled, but the key event should not be propagated to other key event handlers.

It will be returned to the platform embedding to be propagated to text fields and non-Flutter key event handlers on the platform.

# combineKeyEventResults()

```dart
KeyEventResult combineKeyEventResults(Iterable<KeyEventResult> results)
```

Combine the results returned by multiple [FocusOnKeyCallback]s or [FocusOnKeyEventCallback]s.

If any callback returns [KeyEventResult.handled], the node considers the message handled; otherwise, if any callback returns [KeyEventResult.skipRemainingHandlers], the node skips the remaining handlers without preventing the platform to handle; otherwise the node is ignored.

# FocusOnKeyCallback

```dart
typedef FocusOnKeyCallback = KeyEventResult Function(FocusNode node, RawKeyEvent event)
```

Signature of a callback used by [Focus.onKey] and [FocusScope.onKey] to receive key events.

This kind of callback is deprecated and will be removed at a future date. Use [FocusOnKeyEventCallback] and associated APIs instead.

The [node] is the node that received the event.

Returns a [KeyEventResult] that describes how, and whether, the key event was handled.

# FocusOnKeyEventCallback

```dart
typedef FocusOnKeyEventCallback = KeyEventResult Function(FocusNode node, KeyEvent event)
```

Signature of a callback used by [Focus.onKeyEvent] and [FocusScope.onKeyEvent] to receive key events.

The [node] is the node that received the event.

Returns a [KeyEventResult] that describes how, and whether, the key event was handled.

# OnKeyEventCallback

```dart
typedef OnKeyEventCallback = KeyEventResult Function(KeyEvent event)
```

Signature of a callback used by [FocusManager.addEarlyKeyEventHandler] and [FocusManager.addLateKeyEventHandler].

The `event` parameter is a [KeyEvent] that is being sent to the callback to be handled.

The [KeyEventResult] return value indicates whether or not the event will continue to be propagated. If the value returned is [KeyEventResult.handled] or [KeyEventResult.skipRemainingHandlers], then the event will not continue to be propagated.

# FocusAttachment

```dart
class FocusAttachment {}
```

An attachment point for a [FocusNode].

Using a [FocusAttachment] is rarely needed, unless building something akin to the [Focus] or [FocusScope] widgets from scratch.

Once created, a [FocusNode] must be attached to the widget tree by its _host_ [StatefulWidget] via a [FocusAttachment] object. [FocusAttachment]s are owned by the [StatefulWidget] that hosts a [FocusNode] or [FocusScopeNode]. There can be multiple [FocusAttachment]s for each [FocusNode], but the node will only ever be attached to one of them at a time.

This attachment is created by calling [FocusNode.attach], usually from the host widget's [State.initState] method. If the widget is updated to have a different focus node, then the new node needs to be attached in [State.didUpdateWidget], after calling [detach] on the previous [FocusAttachment]. Once detached, the attachment is defunct and will no longer make changes to the [FocusNode] through [reparent].

Without these attachment points, it would be possible for a focus node to simultaneously be attached to more than one part of the widget tree during the build stage.

### isAttached

```dart
bool get isAttached
```

Returns true if the associated node is attached to this attachment.

It is possible to be attached to the widget tree, but not be placed in the focus tree (i.e. to not have a parent yet in the focus tree).

### detach()

```dart
void detach()
```

Detaches the [FocusNode] this attachment point is associated with from the focus tree, and disconnects it from this attachment point.

Calling [FocusNode.dispose] will also automatically detach the node.

### reparent()

```dart
void reparent({FocusNode? parent})
```

Ensures that the [FocusNode] attached at this attachment point has the proper parent node, changing it if necessary.

If given, ensures that the given [parent] node is the parent of the node that is attached at this attachment point, changing it if necessary. However, it is usually not necessary to supply an explicit parent, since [reparent] will use [Focus.of] to determine the correct parent node for the context given in [FocusNode.attach].

If [isAttached] is false, then calling this method does nothing.

Should be called whenever the associated widget is rebuilt in order to maintain the focus hierarchy.

A [StatefulWidget] that hosts a [FocusNode] should call this method on the node it hosts during its [State.build] or [State.didChangeDependencies] methods in case the widget is moved from one location in the tree to another location that has a different [FocusScope] or context.

The optional [parent] argument must be supplied when not using [Focus] and [FocusScope] widgets to build the focus tree, or if there is a need to supply the parent explicitly (which are both uncommon).

# UnfocusDisposition

```dart
enum UnfocusDisposition {}
```

Describe what should happen after [FocusNode.unfocus] is called.

See also:

- [FocusNode.unfocus], which takes this as its `disposition` parameter.

Focus the nearest focusable enclosing scope of this node, but do not descend to locate the leaf [FocusScopeNode.focusedChild] the way [previouslyFocusedChild] does.

Focusing the scope in this way clears the [FocusScopeNode.focusedChild] history for the enclosing scope when it receives focus. Because of this, calling a traversal method like [FocusNode.nextFocus] after unfocusing will cause the [FocusTraversalPolicy] to pick the node it thinks should be first in the scope.

This is the default disposition for [FocusNode.unfocus].

Focus the previously focused child of the nearest focusable enclosing scope of this node.

If there is no previously focused child, then this is equivalent to using the [scope] disposition.

Unfocusing with this disposition will cause [FocusNode.unfocus] to walk up the tree to the nearest focusable enclosing scope, then start to walk down the tree, looking for a focused child at its [FocusScopeNode.focusedChild].

If the [FocusScopeNode.focusedChild] is a scope, then look for its [FocusScopeNode.focusedChild], and so on, finding the leaf [FocusScopeNode.focusedChild] that is not a scope, or, failing that, a leaf scope that has no focused child.

# FocusNode

```dart
class FocusNode with DiagnosticableTreeMixin, ChangeNotifier {}
```

An object that can be used by a stateful widget to obtain the keyboard focus and to handle keyboard events.

_Please see the [Focus] and [FocusScope] widgets, which are utility widgets that manage their own [FocusNode]s and [FocusScopeNode]s, respectively. If they aren't appropriate, [FocusNode]s can be managed directly, but doing this is rare._

[FocusNode]s are persistent objects that form a _focus tree_ that is a representation of the widgets in the hierarchy that are interested in focus. A focus node might need to be created if it is passed in from an ancestor of a [Focus] widget to control the focus of the children from the ancestor, or a widget might need to host one if the widget subsystem is not being used, or if the [Focus] and [FocusScope] widgets provide insufficient control.

[FocusNode]s are organized into _scopes_ (see [FocusScopeNode]), which form sub-trees of nodes that restrict traversal to a group of nodes. Within a scope, the most recent nodes to have focus are remembered, and if a node is focused and then unfocused, the previous node receives focus again.

The focus node hierarchy can be traversed using the [parent], [children], [ancestors] and [descendants] accessors.

[FocusNode]s are [ChangeNotifier]s, so a listener can be registered to receive a notification when the focus changes. Listeners will also be notified when [skipTraversal], [canRequestFocus], [descendantsAreFocusable], and [descendantsAreTraversable] properties are updated. If the [Focus] and [FocusScope] widgets are being used to manage the nodes, consider establishing an [InheritedWidget] dependency on them by calling [Focus.of] or [FocusScope.of] instead. [FocusNode.hasFocus] can also be used to establish a similar dependency, especially if all that is needed is to determine whether or not the widget is focused at build time.

To see the focus tree in the debug console, call [debugDumpFocusTree]. To get the focus tree as a string, call [debugDescribeFocusTree].

{@template flutter.widgets.FocusNode.lifecycle}

## Lifecycle

There are several actors involved in the lifecycle of a [FocusNode]/[FocusScopeNode]. They are created and disposed by their _owner_, attached, detached, and re-parented using a [FocusAttachment] by their _host_ (which must be owned by the [State] of a [StatefulWidget]), and they are managed by the [FocusManager]. Different parts of the [FocusNode] API are intended for these different actors.

[FocusNode]s (and hence [FocusScopeNode]s) are persistent objects that form part of a _focus tree_ that is a sparse representation of the widgets in the hierarchy that are interested in receiving keyboard events. They must be managed like other persistent state, which is typically done by a [StatefulWidget] that owns the node. A stateful widget that owns a focus scope node must call [dispose] from its [State.dispose] method.

Once created, a [FocusNode] must be attached to the widget tree via a [FocusAttachment] object. This attachment is created by calling [attach], usually from the [State.initState] method. If the hosting widget is updated to have a different focus node, then the updated node needs to be attached in [State.didUpdateWidget], after calling [FocusAttachment.detach] on the previous [FocusAttachment].

Because [FocusNode]s form a sparse representation of the widget tree, they must be updated whenever the widget tree is rebuilt. This is done by calling [FocusAttachment.reparent], usually from the [State.build] or [State.didChangeDependencies] methods of the widget that represents the focused region, so that the [BuildContext] assigned to the [FocusScopeNode] can be tracked (the context is used to obtain the [RenderObject], from which the geometry of focused regions can be determined).

Creating a [FocusNode] each time [State.build] is invoked will cause the focus to be lost each time the widget is built, which is usually not desired behavior (call [unfocus] if losing focus is desired).

If, as is common, the hosting [StatefulWidget] is also the owner of the focus node, then it will also call [dispose] from its [State.dispose] (in which case the [FocusAttachment.detach] may be skipped, since dispose will automatically detach). If another object owns the focus node, then it must call [dispose] when the node is done being used. {@endtemplate}

{@template flutter.widgets.FocusNode.keyEvents}

## Key Event Propagation

The [FocusManager] receives key events from [HardwareKeyboard] and will pass them to the focused nodes. It starts with the node with the primary focus, and will call the [onKeyEvent] callback for that node. If the callback returns [KeyEventResult.ignored], indicating that it did not handle the event, the [FocusManager] will move to the parent of that node and call its [onKeyEvent]. If that [onKeyEvent] returns [KeyEventResult.handled], then it will stop propagating the event. If it reaches the root [FocusScopeNode], [FocusManager.rootScope], the event is discarded. {@endtemplate}

## Focus Traversal

The term _traversal_, sometimes called _tab traversal_, refers to moving the focus from one widget to the next in a particular order (also sometimes referred to as the _tab order_, since the TAB key is often bound to the action to move to the next widget).

To give focus to the logical _next_ or _previous_ widget in the UI, call the [nextFocus] or [previousFocus] methods. To give the focus to a widget in a particular direction, call the [focusInDirection] method.

The policy for what the _next_ or _previous_ widget is, or the widget in a particular direction, is determined by the [FocusTraversalPolicy] in force.

The ambient policy is determined by looking up the widget hierarchy for a [FocusTraversalGroup] widget, and obtaining the focus traversal policy from it. Different focus nodes can inherit difference policies, so part of the app can go in a predefined order (using [OrderedTraversalPolicy]), and part can go in reading order (using [ReadingOrderTraversalPolicy]), depending upon the use case.

Predefined policies include [WidgetOrderTraversalPolicy], [ReadingOrderTraversalPolicy], [OrderedTraversalPolicy], and [DirectionalFocusTraversalPolicyMixin], but custom policies can be built based upon these policies. See [FocusTraversalPolicy] for more information.

{@tool dartpad} This example shows how a FocusNode should be managed if not using the [Focus] or [FocusScope] widgets. See the [Focus] widget for a similar example using [Focus] and [FocusScope] widgets.

** See code in examples/api/lib/widgets/focus_manager/focus_node.0.dart ** {@end-tool}

See also:

- [Focus], a widget that manages a [FocusNode] and provides access to focus information and actions to its descendant widgets.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree.
- [FocusManager], a singleton that manages the primary focus and distributes key events to focused nodes.
- [FocusTraversalPolicy], a class used to determine how to move the focus to other nodes.

### FocusNode()

```dart
FocusNode({String? debugLabel, FocusOnKeyCallback? onKey, FocusOnKeyEventCallback? onKeyEvent, bool skipTraversal = false, bool canRequestFocus = true, bool descendantsAreFocusable = true, bool descendantsAreTraversable = true})
```

Creates a focus node.

The [debugLabel] is ignored on release builds.

To receive key events that focuses on this node, pass a listener to `onKeyEvent`.

### skipTraversal

```dart
bool get skipTraversal
```

If true, tells the focus traversal policy to skip over this node for purposes of the traversal algorithm.

This may be used to place nodes in the focus tree that may be focused, but not traversed, allowing them to receive key events as part of the focus chain, but not be traversed to via focus traversal.

This is different from [canRequestFocus] because it only implies that the node can't be reached via traversal, not that it can't be focused. It may still be focused explicitly.

### skipTraversal

```dart
set skipTraversal(bool value)
```

### canRequestFocus

```dart
bool get canRequestFocus
```

If true, this focus node may request the primary focus.

Defaults to true. Set to false if you want this node to do nothing when [requestFocus] is called on it.

If set to false on a [FocusScopeNode], will cause all of the children of the scope node to not be focusable.

If set to false on a [FocusNode], it will not affect the focusability of children of the node.

The [hasFocus] member can still return true if this node is the ancestor of a node with primary focus.

This is different than [skipTraversal] because [skipTraversal] still allows the node to be focused, just not traversed to via the [FocusTraversalPolicy].

Setting [canRequestFocus] to false implies that the node will also be skipped for traversal purposes.

See also:

- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree.
- [FocusTraversalPolicy], a class that can be extended to describe a traversal policy.

### canRequestFocus

```dart
set canRequestFocus(bool value)
```

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

If false, will disable focus for all of this node's descendants.

Defaults to true. Does not affect focusability of this node: for that, use [canRequestFocus].

If any descendants are focused when this is set to false, they will be unfocused. When [descendantsAreFocusable] is set to true again, they will not be refocused, although they will be able to accept focus again.

Does not affect the value of [canRequestFocus] on the descendants.

If a descendant node loses focus when this value is changed, the focus will move to the scope enclosing this node.

See also:

- [ExcludeFocus], a widget that uses this property to conditionally exclude focus for a subtree.
- [descendantsAreTraversable], which makes this widget's descendants untraversable.
- [ExcludeFocusTraversal], a widget that conditionally excludes focus traversal for a subtree.
- [Focus], a widget that exposes this setting as a parameter.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that also has a `descendantsAreFocusable` parameter that prevents its children from being focused.

### descendantsAreFocusable

```dart
set descendantsAreFocusable(bool value)
```

### descendantsAreTraversable

```dart
bool get descendantsAreTraversable
```

If false, tells the focus traversal policy to skip over for all of this node's descendants for purposes of the traversal algorithm.

Defaults to true. Does not affect the focus traversal of this node: for that, use [skipTraversal].

Does not affect the value of [FocusNode.skipTraversal] on the descendants. Does not affect focusability of the descendants.

See also:

- [ExcludeFocusTraversal], a widget that uses this property to conditionally exclude focus traversal for a subtree.
- [descendantsAreFocusable], which makes this widget's descendants unfocusable.
- [ExcludeFocus], a widget that conditionally excludes focus for a subtree.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that also has an `descendantsAreFocusable` parameter that prevents its children from being focused.

### descendantsAreTraversable

```dart
set descendantsAreTraversable(bool value)
```

### context

```dart
BuildContext? get context
```

The context that was supplied to [attach].

This is typically the context for the widget that is being focused, as it is used to determine the bounds of the widget.

### onKey

```dart
FocusOnKeyCallback? onKey
```

Called if this focus node receives a key event while focused (i.e. when [hasFocus] returns true).

This property is deprecated and will be removed at a future date. Use [onKeyEvent] instead.

This is a legacy API based on [RawKeyEvent] and will be deprecated in the future. Prefer [onKeyEvent] instead.

{@macro flutter.widgets.FocusNode.keyEvents}

### onKeyEvent

```dart
FocusOnKeyEventCallback? onKeyEvent
```

Called if this focus node receives a key event while focused (i.e. when [hasFocus] returns true).

{@macro flutter.widgets.FocusNode.keyEvents}

### parent

```dart
FocusNode? get parent
```

Returns the parent node for this object.

All nodes except for the root [FocusScopeNode] ([FocusManager.rootScope]) will be given a parent when they are added to the focus tree, which is done using [FocusAttachment.reparent].

### children

```dart
Iterable<FocusNode> get children
```

An iterator over the children of this node.

### traversalChildren

```dart
Iterable<FocusNode> get traversalChildren
```

An iterator over the children that are allowed to be traversed by the [FocusTraversalPolicy].

Returns the list of focusable, traversable children of this node, regardless of those settings on this focus node. Will return an empty iterable if [descendantsAreFocusable] is false.

See also

- [traversalDescendants], which traverses all of the node's descendants, not just the immediate children.

### debugLabel

```dart
String? get debugLabel
```

A debug label that is used for diagnostic output.

Will always return null in release builds.

### debugLabel

```dart
set debugLabel(String? value)
```

### descendants

```dart
Iterable<FocusNode> get descendants
```

An [Iterable] over the hierarchy of children below this one, in depth-first order.

### traversalDescendants

```dart
Iterable<FocusNode> get traversalDescendants
```

Returns all descendants which do not have the [skipTraversal] and do have the [canRequestFocus] flag set.

### ancestors

```dart
Iterable<FocusNode> get ancestors
```

An [Iterable] over the ancestors of this node.

Iterates the ancestors of this node starting at the parent and iterating over successively more remote ancestors of this node, ending at the root [FocusScopeNode] ([FocusManager.rootScope]).

### hasFocus

```dart
bool get hasFocus
```

Whether this node has input focus.

A [FocusNode] has focus when it is an ancestor of a node that returns true from [hasPrimaryFocus], or it has the primary focus itself.

The [hasFocus] accessor is different from [hasPrimaryFocus] in that [hasFocus] is true if the node is anywhere in the focus chain, but for [hasPrimaryFocus] the node must to be at the end of the chain to return true.

A node that returns true for [hasFocus] will receive key events if none of its focused descendants returned true from their [onKey] handler.

This object is a [ChangeNotifier], and notifies its [Listenable] listeners (registered via [addListener]) whenever this value changes.

See also:

- [Focus.isAt], which is a static method that will return the focus state of the nearest ancestor [Focus] widget's focus node.

### hasPrimaryFocus

```dart
bool get hasPrimaryFocus
```

Returns true if this node currently has the application-wide input focus.

A [FocusNode] has the primary focus when the node is focused in its nearest ancestor [FocusScopeNode] and [hasFocus] is true for all its ancestor nodes, but none of its descendants.

This is different from [hasFocus] in that [hasFocus] is true if the node is anywhere in the focus chain, but here the node has to be at the end of the chain to return true.

A node that returns true for [hasPrimaryFocus] will be the first node to receive key events through its [onKey] handler.

This object notifies its listeners whenever this value changes.

### highlightMode

```dart
FocusHighlightMode get highlightMode
```

Returns the [FocusHighlightMode] that is currently in effect for this node.

### nearestScope

```dart
FocusScopeNode? get nearestScope
```

Returns the nearest enclosing scope node above this node, including this node, if it's a scope.

Returns null if no scope is found.

Use [enclosingScope] to look for scopes above this node.

### enclosingScope

```dart
FocusScopeNode? get enclosingScope
```

Returns the nearest enclosing scope node above this node, or null if the node has not yet be added to the focus tree.

If this node is itself a scope, this will only return ancestors of this scope.

Use [nearestScope] to start at this node instead of above it.

### size

```dart
Size get size
```

Returns the size of the attached widget's [RenderObject], in logical units.

Size is the size of the transformed widget in global coordinates.

### offset

```dart
Offset get offset
```

Returns the global offset to the upper left corner of the attached widget's [RenderObject], in logical units.

Offset is the offset of the transformed widget in global coordinates.

### rect

```dart
Rect get rect
```

Returns the global rectangle of the attached widget's [RenderObject], in logical units.

Rect is the rectangle of the transformed widget in global coordinates.

### unfocus()

```dart
void unfocus({UnfocusDisposition disposition = UnfocusDisposition.scope})
```

Removes the focus on this node by moving the primary focus to another node.

This method removes focus from a node that has the primary focus, cancels any outstanding requests to focus it, while setting the primary focus to another node according to the `disposition`.

It is safe to call regardless of whether this node has ever requested focus or not. If this node doesn't have focus or primary focus, nothing happens.

The `disposition` argument determines which node will receive primary focus after this one loses it.

If `disposition` is set to [UnfocusDisposition.scope] (the default), then the previously focused node history of the enclosing scope will be cleared, and the primary focus will be moved to the nearest enclosing scope ancestor that is enabled for focus, ignoring the [FocusScopeNode.focusedChild] for that scope.

If `disposition` is set to [UnfocusDisposition.previouslyFocusedChild], then this node will be removed from the previously focused list in the [enclosingScope], and the focus will be moved to the previously focused node of the [enclosingScope], which (if it is a scope itself), will find its focused child, etc., until a leaf focus node is found. If there is no previously focused child, then the scope itself will receive focus, as if [UnfocusDisposition.scope] were specified.

If you want this node to lose focus and the focus to move to the next or previous node in the enclosing [FocusTraversalGroup], call [nextFocus] or [previousFocus] instead of calling [unfocus].

{@tool dartpad} This example shows the difference between the different [UnfocusDisposition] values for [unfocus].

Try setting focus on the four text fields by selecting them, and then select "UNFOCUS" to see what happens when the current [FocusManager.primaryFocus] is unfocused.

Try pressing the TAB key after unfocusing to see what the next widget chosen is.

** See code in examples/api/lib/widgets/focus_manager/focus_node.unfocus.0.dart ** {@end-tool}

### consumeKeyboardToken()

```dart
bool consumeKeyboardToken()
```

Removes the keyboard token from this focus node if it has one.

This mechanism helps distinguish between an input control gaining focus by default and gaining focus as a result of an explicit user action.

When a focus node requests the focus (either via [FocusScopeNode.requestFocus] or [FocusScopeNode.autofocus]), the focus node receives a keyboard token if it does not already have one. Later, when the focus node becomes focused, the widget that manages the [TextInputConnection] should show the keyboard (i.e. call [TextInputConnection.show]) only if it successfully consumes the keyboard token from the focus node.

Returns true if this method successfully consumes the keyboard token.

### attach()

```dart
FocusAttachment attach(BuildContext? context, {FocusOnKeyEventCallback? onKeyEvent, FocusOnKeyCallback? onKey})
```

Called by the _host_ [StatefulWidget] to attach a [FocusNode] to the widget tree.

In order to attach a [FocusNode] to the widget tree, call [attach], typically from the [StatefulWidget]'s [State.initState] method.

If the focus node in the host widget is swapped out, the new node will need to be attached. [FocusAttachment.detach] should be called on the old node, and then [attach] called on the new node. This typically happens in the [State.didUpdateWidget] method.

To receive key events that focuses on this node, pass a listener to `onKeyEvent`.

### dispose()

```dart
void dispose()
```

### requestFocus()

```dart
void requestFocus([FocusNode? node])
```

Requests the primary focus for this node, or for a supplied [node], which will also give focus to its [ancestors].

If called without a node, request focus for this node. If the node hasn't been added to the focus tree yet, then defer the focus request until it is, allowing newly created widgets to request focus as soon as they are added.

If the given [node] is not yet a part of the focus tree, then this method will add the [node] as a child of this node before requesting focus.

If the given [node] is a [FocusScopeNode] and that focus scope node has a non-null [FocusScopeNode.focusedChild], then request the focus for the focused child. This process is recursive and continues until it encounters either a focus scope node with a null focused child or an ordinary (non-scope) [FocusNode] is found.

The node is notified that it has received the primary focus in a microtask, so notification may lag the request by up to one frame.

### nextFocus()

```dart
bool nextFocus()
```

Request to move the focus to the next focus node, by calling the [FocusTraversalPolicy.next] method.

Returns true if it successfully found a node and requested focus.

### previousFocus()

```dart
bool previousFocus()
```

Request to move the focus to the previous focus node, by calling the [FocusTraversalPolicy.previous] method.

Returns true if it successfully found a node and requested focus.

### focusInDirection()

```dart
bool focusInDirection(TraversalDirection direction)
```

Request to move the focus to the nearest focus node in the given direction, by calling the [FocusTraversalPolicy.inDirection] method.

Returns true if it successfully found a node and requested focus.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### toStringShort()

```dart
String toStringShort()
```

# FocusScopeNode

```dart
class FocusScopeNode extends FocusNode {}
```

A subclass of [FocusNode] that acts as a scope for its descendants, maintaining information about which descendant is currently or was last focused.

_Please see the [FocusScope] and [Focus] widgets, which are utility widgets that manage their own [FocusScopeNode]s and [FocusNode]s, respectively. If they aren't appropriate, [FocusScopeNode]s can be managed directly._

[FocusScopeNode] organizes [FocusNode]s into _scopes_. Scopes form sub-trees of nodes that can be traversed as a group. Within a scope, the most recent nodes to have focus are remembered, and if a node is focused and then removed, the original node receives focus again.

From a [FocusScopeNode], calling [setFirstFocus], sets the given focus scope as the [focusedChild] of this node, adopting if it isn't already part of the focus tree.

{@macro flutter.widgets.FocusNode.lifecycle} {@macro flutter.widgets.FocusNode.keyEvents}

See also:

- [Focus], a widget that manages a [FocusNode] and provides access to focus information and actions to its descendant widgets.
- [FocusManager], a singleton that manages the primary focus and distributes key events to focused nodes.

### FocusScopeNode()

```dart
FocusScopeNode({String? debugLabel, KeyEventResult Function(FocusNode, InvalidType)? onKeyEvent, KeyEventResult Function(FocusNode, InvalidType)? onKey, bool skipTraversal, bool canRequestFocus, TraversalEdgeBehavior traversalEdgeBehavior = TraversalEdgeBehavior.closedLoop, TraversalEdgeBehavior directionalTraversalEdgeBehavior = TraversalEdgeBehavior.stop})
```

Creates a [FocusScopeNode].

All parameters are optional.

### nearestScope

```dart
FocusScopeNode get nearestScope
```

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

### traversalEdgeBehavior

```dart
TraversalEdgeBehavior traversalEdgeBehavior
```

Controls the transfer of focus beyond the first and the last items of a [FocusScopeNode].

Changing this field value has no immediate effect on the UI. Instead, next time focus traversal takes place [FocusTraversalPolicy] will read this value and apply the new behavior.

### directionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior directionalTraversalEdgeBehavior
```

Controls the directional transfer of focus when the focus is on the first or last item.

Changing this field value has no immediate effect on the UI. Instead, next time focus traversal takes place [FocusTraversalPolicy] will read this value and apply the new behavior.

### isFirstFocus

```dart
bool get isFirstFocus
```

Returns true if this scope is the focused child of its parent scope.

### focusedChild

```dart
FocusNode? get focusedChild
```

Returns the child of this node that should receive focus if this scope node receives focus.

If [hasFocus] is true, then this points to the child of this node that is currently focused.

Returns null if there is no currently focused child.

### traversalChildren

```dart
Iterable<FocusNode> get traversalChildren
```

An iterator over the children that are allowed to be traversed by the [FocusTraversalPolicy].

Will return an empty iterable if this scope node is not focusable, or if [descendantsAreFocusable] is false.

See also:

- [traversalDescendants], which traverses all of the node's descendants, not just the immediate children.

### traversalDescendants

```dart
Iterable<FocusNode> get traversalDescendants
```

Returns all descendants which do not have the [skipTraversal] and do have the [canRequestFocus] flag set.

Will return an empty iterable if this scope node is not focusable, or if [descendantsAreFocusable] is false.

### setFirstFocus()

```dart
void setFirstFocus(FocusScopeNode scope)
```

Make the given [scope] the active child scope for this scope.

If the given [scope] is not yet a part of the focus tree, then add it to the tree as a child of this scope. If it is already part of the focus tree, the given scope must be a descendant of this scope.

### autofocus()

```dart
void autofocus(FocusNode node)
```

If this scope lacks a focus, request that the given node become the focus.

If the given node is not yet part of the focus tree, then add it as a child of this node.

Useful for widgets that wish to grab the focus if no other widget already has the focus.

The node is notified that it has received the primary focus in a microtask, so notification may lag the request by up to one frame.

### requestScopeFocus()

```dart
void requestScopeFocus()
```

Requests that the scope itself receive focus, without trying to find a descendant that should receive focus.

This is used only if you want to park the focus on a scope itself.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FocusHighlightMode

```dart
enum FocusHighlightMode {}
```

An enum to describe which kind of focus highlight behavior to use when displaying focus information.

Touch interfaces will not show the focus highlight except for controls which bring up the soft keyboard.

If a device that uses a traditional mouse and keyboard has a touch screen attached, it can also enter `touch` mode if the user is using the touch screen.

Traditional interfaces (keyboard and mouse) will show the currently focused control via a focus highlight of some sort.

If a touch device (like a mobile phone) has a keyboard and/or mouse attached, it also can enter `traditional` mode if the user is using these input devices.

# FocusHighlightStrategy

```dart
enum FocusHighlightStrategy {}
```

An enum to describe how the current value of [FocusManager.highlightMode] is determined. The strategy is set on [FocusManager.highlightStrategy].

Automatic switches between the various highlight modes based on the last kind of input that was received. This is the default.

[FocusManager.highlightMode] always returns [FocusHighlightMode.touch].

[FocusManager.highlightMode] always returns [FocusHighlightMode.traditional].

# FocusManager

```dart
class FocusManager with DiagnosticableTreeMixin, ChangeNotifier {}
```

Manages the focus tree.

The focus tree is a separate, sparser, tree from the widget tree that maintains the hierarchical relationship between focusable widgets in the widget tree.

The focus manager is responsible for tracking which [FocusNode] has the primary input focus (the [primaryFocus]), holding the [FocusScopeNode] that is the root of the focus tree (the [rootScope]), and what the current [highlightMode] is. It also distributes [KeyEvent]s to the nodes in the focus tree.

The singleton [FocusManager] instance is held by the [WidgetsBinding] as [WidgetsBinding.focusManager], and can be conveniently accessed using the [FocusManager.instance] static accessor.

To find the [FocusNode] for a given [BuildContext], use [Focus.of]. To find the [FocusScopeNode] for a given [BuildContext], use [FocusScope.of].

If you would like notification whenever the [primaryFocus] changes, register a listener with [addListener]. When you no longer want to receive these events, as when your object is about to be disposed, you must unregister with [removeListener] to avoid memory leaks. Removing listeners is typically done in [State.dispose] on stateful widgets.

The [highlightMode] describes how focus highlights should be displayed on components in the UI. The [highlightMode] changes are notified separately via [addHighlightModeListener] and removed with [removeHighlightModeListener]. The highlight mode changes when the user switches from a mouse to a touch interface, or vice versa.

The widgets that are used to manage focus in the widget tree are:

- [Focus], a widget that manages a [FocusNode] in the focus tree so that the focus tree reflects changes in the widget hierarchy.
- [FocusScope], a widget that manages a [FocusScopeNode] in the focus tree, creating a new scope for restricting focus to a set of focus nodes.
- [FocusTraversalGroup], a widget that groups together nodes that should be traversed using an order described by a given [FocusTraversalPolicy].

See also:

- [FocusNode], which is a node in the focus tree that can receive focus.
- [FocusScopeNode], which is a node in the focus tree used to collect subtrees into groups and restrict focus to them.
- The [primaryFocus] global accessor, for convenient access from anywhere to the current focus manager state.

### FocusManager()

```dart
FocusManager()
```

Creates an object that manages the focus tree.

This constructor is rarely called directly. To access the [FocusManager], consider using the [FocusManager.instance] accessor instead (which gets it from the [WidgetsBinding] singleton).

This newly constructed focus manager does not have the necessary event handlers registered to allow it to manage focus. To register those event handlers, callers must call [registerGlobalHandlers]. See the documentation in that method for caveats to watch out for.

### registerGlobalHandlers()

```dart
void registerGlobalHandlers()
```

Registers global input event handlers that are needed to manage focus.

This calls the [HardwareKeyboard.addHandler] on the shared instance of [HardwareKeyboard] and adds a route to the global entry in the gesture routing table. As such, only one [FocusManager] instance should register its global handlers.

When this focus manager is no longer needed, calling [dispose] on it will unregister these handlers.

### dispose()

```dart
void dispose()
```

### instance

```dart
FocusManager get instance
```

Provides convenient access to the current [FocusManager] singleton from the [WidgetsBinding] instance.

### highlightStrategy

```dart
FocusHighlightStrategy get highlightStrategy
```

Sets the strategy by which [highlightMode] is determined.

If set to [FocusHighlightStrategy.automatic], then the highlight mode will change depending upon the interaction mode used last. For instance, if the last interaction was a touch interaction, then [highlightMode] will return [FocusHighlightMode.touch], and focus highlights will only appear on widgets that bring up a soft keyboard. If the last interaction was a non-touch interaction (hardware keyboard press, mouse click, etc.), then [highlightMode] will return [FocusHighlightMode.traditional], and focus highlights will appear on all widgets.

If set to [FocusHighlightStrategy.alwaysTouch] or [FocusHighlightStrategy.alwaysTraditional], then [highlightMode] will always return [FocusHighlightMode.touch] or [FocusHighlightMode.traditional], respectively, regardless of the last UI interaction type.

The initial value of [highlightMode] depends upon the value of [defaultTargetPlatform] and [MouseTracker.mouseIsConnected] of [RendererBinding.mouseTracker], making a guess about which interaction is most appropriate for the initial interaction mode.

Defaults to [FocusHighlightStrategy.automatic].

### highlightStrategy

```dart
set highlightStrategy(FocusHighlightStrategy value)
```

### highlightMode

```dart
FocusHighlightMode get highlightMode
```

Indicates the current interaction mode for focus highlights.

The value returned depends upon the [highlightStrategy] used, and possibly (depending on the value of [highlightStrategy]) the most recent interaction mode that they user used.

If [highlightMode] returns [FocusHighlightMode.touch], then widgets should not draw their focus highlight unless they perform text entry.

If [highlightMode] returns [FocusHighlightMode.traditional], then widgets should draw their focus highlight whenever they are focused.

### addHighlightModeListener()

```dart
void addHighlightModeListener(ValueChanged<FocusHighlightMode> listener)
```

Register a closure to be called when the [FocusManager] notifies its listeners that the value of [highlightMode] has changed.

### removeHighlightModeListener()

```dart
void removeHighlightModeListener(ValueChanged<FocusHighlightMode> listener)
```

Remove a previously registered closure from the list of closures that the [FocusManager] notifies.

### addEarlyKeyEventHandler()

```dart
void addEarlyKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.addEarlyKeyEventHandler} Adds a key event handler to a set of handlers that are called before any key event handlers in the focus tree are called.

All of the handlers in the set will be called for every key event the [FocusManager] receives. If any one of the handlers returns [KeyEventResult.handled] or [KeyEventResult.skipRemainingHandlers], then none of the handlers in the focus tree will be called.

If handlers are added while the existing callbacks are being invoked, they will not be called until the next key event occurs.

See also:

- [removeEarlyKeyEventHandler], which removes handlers added by this function.
- [addLateKeyEventHandler], which is a similar mechanism for adding handlers that are invoked after the focus tree has had a chance to handle an event. {@endtemplate}

### removeEarlyKeyEventHandler()

```dart
void removeEarlyKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.removeEarlyKeyEventHandler} Removes a key handler added by calling [addEarlyKeyEventHandler].

If handlers are removed while the existing callbacks are being invoked, they will continue to be called until the next key event is received.

See also:

- [addEarlyKeyEventHandler], which adds the handlers removed by this function. {@endtemplate}

### addLateKeyEventHandler()

```dart
void addLateKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.addLateKeyEventHandler} Adds a key event handler to a set of handlers that are called if none of the key event handlers in the focus tree handle the event.

If the event reaches the root of the focus tree without being handled, then all of the handlers in the set will be called. If any of them returns [KeyEventResult.handled] or [KeyEventResult.skipRemainingHandlers], then event propagation to the platform will be stopped.

If handlers are added while the existing callbacks are being invoked, they will not be called until the next key event is not handled by the focus tree.

See also:

- [removeLateKeyEventHandler], which removes handlers added by this function.
- [addEarlyKeyEventHandler], which is a similar mechanism for adding handlers that are invoked before the focus tree has had a chance to handle an event. {@endtemplate}

### removeLateKeyEventHandler()

```dart
void removeLateKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.removeLateKeyEventHandler} Removes a key handler added by calling [addLateKeyEventHandler].

If handlers are removed while the existing callbacks are being invoked, they will continue to be called until the next key event is received.

See also:

- [addLateKeyEventHandler], which adds the handlers removed by this function. {@endtemplate}

### rootScope

```dart
FocusScopeNode rootScope
```

The root [FocusScopeNode] in the focus tree.

This field is rarely used directly. To find the nearest [FocusScopeNode] for a given [FocusNode], call [FocusNode.nearestScope].

### primaryFocus

```dart
FocusNode? get primaryFocus
```

The node that currently has the primary focus.

### applyFocusChangesIfNeeded()

```dart
void applyFocusChangesIfNeeded()
```

Applies any pending focus changes and notifies listeners that the focus has changed.

Must not be called during the build phase. This method is meant to be called in a post-frame callback or microtask when the pending focus changes need to be resolved before something else occurs.

It can't be called during the build phase because not all listeners are safe to be called with an update during a build.

Typically, this is called automatically by the [FocusManager], but sometimes it is necessary to ensure that no focus changes are pending before executing an action. For example, the [MenuAnchor] class uses this to make sure that the previous focus has been restored before executing a menu callback when a menu item is selected.

It is safe to call this if no focus changes are pending.

### listenToApplicationLifecycleChangesIfSupported()

```dart
void listenToApplicationLifecycleChangesIfSupported()
```

Enables this [FocusManager] to listen to changes of the application lifecycle if it does not already have an application lifecycle listener active, and the app isn't running on a native mobile platform.

Typically, the application lifecycle listener for this [FocusManager] is setup at construction, but sometimes it is necessary to manually initialize it when the [FocusManager] does not have the relevant platform context in [defaultTargetPlatform] at the time of construction. This can happen in a test environment where the [BuildOwner] which initializes its own [FocusManager], may not have the accurate platform context during its initialization. In this case it is necessary for the test framework to call this method after it has set up the test variant for a given test, so the [FocusManager] can accurately listen to application lifecycle changes, if supported.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# primaryFocus

```dart
FocusNode? get primaryFocus
```

Provides convenient access to the current [FocusManager.primaryFocus] from the [WidgetsBinding] instance.

# debugDescribeFocusTree()

```dart
String debugDescribeFocusTree()
```

Returns a text representation of the current focus tree, along with the current attributes on each node.

Will return an empty string in release builds.

# debugDumpFocusTree()

```dart
void debugDumpFocusTree()
```

Prints a text representation of the current focus tree, along with the current attributes on each node.

Will do nothing in release builds.
