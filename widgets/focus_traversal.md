@docImport 'dart:ui'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart';

# TraversalRequestFocusCallback

```dart
typedef TraversalRequestFocusCallback = void Function(FocusNode node, {ScrollPositionAlignmentPolicy? alignmentPolicy, double? alignment, Duration? duration, Curve? curve})
```

Signature for the callback that's called when a traversal policy requests focus.

# TraversalDirection

```dart
enum TraversalDirection {}
```

A direction along either the horizontal or vertical axes.

This is used by the [DirectionalFocusTraversalPolicyMixin], and [FocusNode.focusInDirection] to indicate which direction to look in for the next focus.

Indicates a direction above the currently focused widget.

Indicates a direction to the right of the currently focused widget.

This direction is unaffected by the [Directionality] of the current context.

Indicates a direction below the currently focused widget.

Indicates a direction to the left of the currently focused widget.

This direction is unaffected by the [Directionality] of the current context.

# TraversalEdgeBehavior

```dart
enum TraversalEdgeBehavior {}
```

Controls the focus transfer at the edges of a [FocusScopeNode]. For movement transfers (previous or next), the edge represents the first or last items. For directional transfers, the edge represents the outermost items of the [FocusScopeNode], For example: for moving downwards, the edge node is the one with the largest bottom coordinate; for moving leftwards, the edge node is the one with the smallest x coordinate.

This enumeration only controls the traversal behavior performed by [FocusTraversalPolicy]. Other methods of focus transfer, such as direct calls to [FocusNode.requestFocus] and [FocusNode.unfocus], are not affected by this enumeration.

See also:

- [FocusTraversalPolicy], which implements the logic behind this enum.
- [FocusScopeNode], which is configured by this enum.

Keeps the focus among the items of the focus scope.

Transfer focus to the edge node in the opposite direction of [FocusScopeNode] as the edge node continues to move, thus forming a closed loop of focusable items.

For moving transfers, requesting the next focus after the last focusable item will transfer focus to the first item, and requesting focus before the first item will transfer focus to the last item.

For directional transfers, continuing to request right focus at the rightmost node will transfer focus to the leftmost node. Continuing to request left focus at the leftmost node will transfer focus to the rightmost node.

Allows the focus to leave the [FlutterView].

Requesting next focus after the last focusable item or previous to the first item will unfocus any focused nodes. If the focus traversal action was initiated by the embedder (e.g. the Flutter Engine) the embedder receives a result indicating that the focus is no longer within the current [FlutterView]. For example, [NextFocusAction] invoked via keyboard (typically the TAB key) would receive [KeyEventResult.skipRemainingHandlers] allowing the embedder handle the shortcut. On the web, typically the control is transferred to the browser, allowing the user to reach the address bar, escape an `iframe`, or focus on HTML elements other than those managed by Flutter.

Allows focus to traverse up to parent scope.

When reaching the edge of the current scope, requesting the next focus will look up to the parent scope of the current scope and focus the focus node next to the current scope.

If there is no parent scope above the current scope, fallback to [closedLoop] behavior.

Stops the focus traversal at the edge of the focus scope.

Keeps the focus in its current position when it reaches the edge of a focus scope.

# FocusTraversalPolicy

```dart
abstract class FocusTraversalPolicy with Diagnosticable {}
```

Determines how focusable widgets are traversed within a [FocusTraversalGroup].

The focus traversal policy is what determines which widget is "next", "previous", or in a direction from the widget associated with the currently focused [FocusNode] (usually a [Focus] widget).

One of the pre-defined subclasses may be used, or define a custom policy to create a unique focus order.

When defining your own, your subclass should implement [sortDescendants] to provide the order in which you would like the descendants to be traversed.

See also:

- [FocusNode], for a description of the focus system.
- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [FocusNode], which is affected by the traversal policy.
- [WidgetOrderTraversalPolicy], a policy that relies on the widget creation order to describe the order of traversal.
- [ReadingOrderTraversalPolicy], a policy that describes the order as the natural "reading order" for the current [Directionality].
- [OrderedTraversalPolicy], a policy that describes the order explicitly using [FocusTraversalOrder] widgets.
- [DirectionalFocusTraversalPolicyMixin] a mixin class that implements focus traversal in a direction.

### FocusTraversalPolicy()

```dart
FocusTraversalPolicy({TraversalRequestFocusCallback? requestFocusCallback})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

{@template flutter.widgets.FocusTraversalPolicy.requestFocusCallback} The `requestFocusCallback` can be used to override the default behavior of the focus requests. If `requestFocusCallback` is null, it defaults to [FocusTraversalPolicy.defaultTraversalRequestFocusCallback]. {@endtemplate}

### requestFocusCallback

```dart
TraversalRequestFocusCallback requestFocusCallback
```

The callback used to move the focus from one focus node to another when traversing them using a keyboard. By default it requests focus on the next node and ensures the node is visible if it's in a scrollable.

### defaultTraversalRequestFocusCallback()

```dart
void defaultTraversalRequestFocusCallback(FocusNode node, {ScrollPositionAlignmentPolicy? alignmentPolicy, double? alignment, Duration? duration, Curve? curve})
```

The default value for [requestFocusCallback]. Requests focus from `node` and ensures the node is visible by calling [Scrollable.ensureVisible].

### findFirstFocus()

```dart
FocusNode? findFirstFocus(FocusNode currentNode, {bool ignoreCurrentFocus = false})
```

Returns the node that should receive focus if focus is traversing forwards, and there is no current focus.

The node returned is the node that should receive focus if focus is traversing forwards (i.e. with [next]), and there is no current focus in the nearest [FocusScopeNode] that `currentNode` belongs to.

If `ignoreCurrentFocus` is false or not given, this function returns the [FocusScopeNode.focusedChild], if set, on the nearest scope of the `currentNode`, otherwise, returns the first node from [sortDescendants], or the given `currentNode` if there are no descendants.

If `ignoreCurrentFocus` is true, then the algorithm returns the first node from [sortDescendants], or the given `currentNode` if there are no descendants.

See also:

- [next], the function that is called to move the focus to the next node.
- [DirectionalFocusTraversalPolicyMixin.findFirstFocusInDirection], a function that finds the first focusable widget in a particular direction.

### findLastFocus()

```dart
FocusNode findLastFocus(FocusNode currentNode, {bool ignoreCurrentFocus = false})
```

Returns the node that should receive focus if focus is traversing backwards, and there is no current focus.

The node returned is the one that should receive focus if focus is traversing backwards (i.e. with [previous]), and there is no current focus in the nearest [FocusScopeNode] that `currentNode` belongs to.

If `ignoreCurrentFocus` is false or not given, this function returns the [FocusScopeNode.focusedChild], if set, on the nearest scope of the `currentNode`, otherwise, returns the last node from [sortDescendants], or the given `currentNode` if there are no descendants.

If `ignoreCurrentFocus` is true, then the algorithm returns the last node from [sortDescendants], or the given `currentNode` if there are no descendants.

See also:

- [previous], the function that is called to move the focus to the previous node.
- [DirectionalFocusTraversalPolicyMixin.findFirstFocusInDirection], a function that finds the first focusable widget in a particular direction.

### findFirstFocusInDirection()

```dart
FocusNode? findFirstFocusInDirection(FocusNode currentNode, TraversalDirection direction)
```

Returns the first node in the given `direction` that should receive focus if there is no current focus in the scope to which the `currentNode` belongs.

This is typically used by [inDirection] to determine which node to focus if it is called when no node is currently focused.

### invalidateScopeData()

```dart
void invalidateScopeData(FocusScopeNode node)
```

Clears the data associated with the given [FocusScopeNode] for this object.

This is used to indicate that the focus policy has changed its mode, and so any cached policy data should be invalidated. For example, changing the direction in which focus is moving, or changing from directional to next/previous navigation modes.

The default implementation does nothing.

### changedScope()

```dart
void changedScope({FocusNode? node, FocusScopeNode? oldScope})
```

This is called whenever the given [node] is re-parented into a new scope, so that the policy has a chance to update or invalidate any cached data that it maintains per scope about the node.

The [oldScope] is the previous scope that this node belonged to, if any.

The default implementation does nothing.

### next()

```dart
bool next(FocusNode currentNode)
```

Focuses the next widget in the focus scope that contains the given [currentNode].

This should determine what the next node to receive focus should be by inspecting the node tree, and then calling [FocusNode.requestFocus] on the node that has been selected.

Returns true if it successfully found a node and requested focus.

### previous()

```dart
bool previous(FocusNode currentNode)
```

Focuses the previous widget in the focus scope that contains the given [currentNode].

This should determine what the previous node to receive focus should be by inspecting the node tree, and then calling [FocusNode.requestFocus] on the node that has been selected.

Returns true if it successfully found a node and requested focus.

### inDirection()

```dart
bool inDirection(FocusNode currentNode, TraversalDirection direction)
```

Focuses the next widget in the given [direction] in the focus scope that contains the given [currentNode].

This should determine what the next node to receive focus in the given [direction] should be by inspecting the node tree, and then calling [FocusNode.requestFocus] on the node that has been selected.

Returns true if it successfully found a node and requested focus.

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

Sorts the given `descendants` into focus order.

Subclasses should override this to implement a different sort for [next] and [previous] to use in their ordering. If the returned iterable omits a node that is a descendant of the given scope, then the user will be unable to use next/previous keyboard traversal to reach that node.

The node used to initiate the traversal (the one passed to [next] or [previous]) is passed as `currentNode`.

Having the current node in the list is what allows the algorithm to determine which nodes are adjacent to the current node. If the `currentNode` is removed from the list, then the focus will be unchanged when [next] or [previous] are called, and they will return false.

This is not used for directional focus ([inDirection]), only for determining the focus order for [next] and [previous].

When implementing an override for this function, be sure to use [mergeSort] instead of Dart's default list sorting algorithm when sorting items, since the default algorithm is not stable (items deemed to be equal can appear in arbitrary order, and change positions between sorts), whereas [mergeSort] is stable.

# DirectionalFocusTraversalPolicyMixin

```dart
mixin DirectionalFocusTraversalPolicyMixin on FocusTraversalPolicy {}
```

A mixin class that provides an implementation for finding a node in a particular direction.

This can be mixed in to other [FocusTraversalPolicy] implementations that only want to implement new next/previous policies.

Since hysteresis in the navigation order is undesirable, this implementation maintains a stack of previous locations that have been visited on the policy data for the affected [FocusScopeNode]. If the previous direction was the opposite of the current direction, then the this policy will request focus on the previously focused node. Change to another direction other than the current one or its opposite will clear the stack.

For instance, if the focus moves down, down, down, and then up, up, up, it will follow the same path through the widgets in both directions. However, if it moves down, down, down, left, right, and then up, up, up, it may not follow the same path on the way up as it did on the way down, since changing the axis of motion resets the history.

This class implements an algorithm that considers an band extending along the direction of movement within the [FocusScope], the width or height (depending on direction) of the currently focused widget, and finds the closest widget inthat band along the direction of movement. If nothing is found in that band,then it picks the widget with an edge closest to the band in the perpendicular direction. If two out-of-band widgets are the same distance from the band, then it picks the one closest along the direction of movement. When reaching the edge in the direction specified by [FocusScope], different behaviors are taken according to [FocusScopeNode.directionalTraversalEdgeBehavior]. For [TraversalEdgeBehavior.closedLoop], the algorithm will reselect the farthest node in the opposite direction within the band. For [TraversalEdgeBehavior.parentScope], the band will extend to the parent [FocusScopeNode],and if it is still an edge node in the parent, it will continue to search according to the parent's [FocusScopeNode.directionalTraversalEdgeBehavior], If there is no parent scope above the current scope, fallback to [TraversalEdgeBehavior.closedLoop] behavior. For [TraversalEdgeBehavior.leaveFlutterView], the focus will be lost. For [TraversalEdgeBehavior.stop], the current focused element will remain.

The goal of this algorithm is to pick a widget that (to the user) doesn't appear to traverse along the wrong axis, as it might if it only sorted widgets by distance along one axis, but also jumps to the next logical widget in a direction without skipping over widgets.

See also:

- [FocusNode], for a description of the focus system.
- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [WidgetOrderTraversalPolicy], a policy that relies on the widget creation order to describe the order of traversal.
- [ReadingOrderTraversalPolicy], a policy that describes the order as the natural "reading order" for the current [Directionality].
- [OrderedTraversalPolicy], a policy that describes the order explicitly using [FocusTraversalOrder] widgets.

### invalidateScopeData()

```dart
void invalidateScopeData(FocusScopeNode node)
```

### changedScope()

```dart
void changedScope({FocusNode? node, FocusScopeNode? oldScope})
```

### findFirstFocusInDirection()

```dart
FocusNode? findFirstFocusInDirection(FocusNode currentNode, TraversalDirection direction)
```

### inDirection()

```dart
bool inDirection(FocusNode currentNode, TraversalDirection direction)
```

Focuses the next widget in the given [direction] in the [FocusScope] that contains the [currentNode].

This determines what the next node to receive focus in the given [direction] will be by inspecting the node tree, and then calling [FocusNode.requestFocus] on it.

Returns true if it successfully found a node and requested focus.

Maintains a stack of previous locations that have been visited on the policy data for the affected [FocusScopeNode]. If the previous direction was the opposite of the current direction, then the this policy will request focus on the previously focused node. Change to another direction other than the current one or its opposite will clear the stack.

If this function returns true when called by a subclass, then the subclass should return true and not request focus from any node.

# WidgetOrderTraversalPolicy

```dart
class WidgetOrderTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

A [FocusTraversalPolicy] that traverses the focus order in widget hierarchy order.

This policy is used when the order desired is the order in which widgets are created in the widget hierarchy.

See also:

- [FocusNode], for a description of the focus system.
- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [ReadingOrderTraversalPolicy], a policy that describes the order as the natural "reading order" for the current [Directionality].
- [DirectionalFocusTraversalPolicyMixin] a mixin class that implements focus traversal in a direction.
- [OrderedTraversalPolicy], a policy that describes the order explicitly using [FocusTraversalOrder] widgets.

### WidgetOrderTraversalPolicy()

```dart
WidgetOrderTraversalPolicy({void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

Constructs a traversal policy that orders widgets for keyboard traversal based on the widget hierarchy order.

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# ReadingOrderTraversalPolicy

```dart
class ReadingOrderTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

Traverses the focus order in "reading order".

By default, reading order traversal goes in the reading direction, and then down, using this algorithm:

1.  Find the node rectangle that has the highest `top` on the screen.
2.  Find any other nodes that intersect the infinite horizontal band defined by the highest rectangle's top and bottom edges.
3.  Pick the closest to the beginning of the reading order from among the nodes discovered above.

It uses the ambient [Directionality] in the context for the enclosing [FocusTraversalGroup] to determine which direction is "reading order".

See also:

- [FocusNode], for a description of the focus system.
- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [WidgetOrderTraversalPolicy], a policy that relies on the widget creation order to describe the order of traversal.
- [DirectionalFocusTraversalPolicyMixin] a mixin class that implements focus traversal in a direction.
- [OrderedTraversalPolicy], a policy that describes the order explicitly using [FocusTraversalOrder] widgets.

### ReadingOrderTraversalPolicy()

```dart
ReadingOrderTraversalPolicy({void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

Constructs a traversal policy that orders the widgets in "reading order".

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### sort()

```dart
Iterable<FocusNode> sort(Iterable<FocusNode> nodes)
```

Sorts the input focus nodes into reading order.

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# FocusOrder

```dart
abstract class FocusOrder with Diagnosticable implements Comparable<FocusOrder> {}
```

Base class for all sort orders for [OrderedTraversalPolicy] traversal.

{@template flutter.widgets.FocusOrder.comparable} Only orders of the same type are comparable. If a set of widgets in the same [FocusTraversalGroup] contains orders that are not comparable with each other, it will assert, since the ordering between such keys is undefined. To avoid collisions, use a [FocusTraversalGroup] to group similarly ordered widgets together.

When overriding, [FocusOrder.doCompare] must be overridden instead of [FocusOrder.compareTo], which calls [FocusOrder.doCompare] to do the actual comparison. {@endtemplate}

See also:

- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [FocusTraversalOrder], a widget that assigns an order to a widget subtree for the [OrderedTraversalPolicy] to use.
- [NumericFocusOrder], for a focus order that describes its order with a `double`.
- [LexicalFocusOrder], a focus order that assigns a string-based lexical traversal order to a [FocusTraversalOrder] widget.

### FocusOrder()

```dart
FocusOrder()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### compareTo()

```dart
int compareTo(FocusOrder other)
```

Compares this object to another [Comparable].

When overriding [FocusOrder], implement [doCompare] instead of this function to do the actual comparison.

Returns a value like a [Comparator] when comparing `this` to [other]. That is, it returns a negative integer if `this` is ordered before [other], a positive integer if `this` is ordered after [other], and zero if `this` and [other] are ordered together.

The [other] argument must be a value that is comparable to this object.

### doCompare()

```dart
int doCompare(FocusOrder other)
```

The subclass implementation called by [compareTo] to compare orders.

The argument is guaranteed to be of the same [runtimeType] as this object.

The method should return a negative number if this object comes earlier in the sort order than the `other` argument; and a positive number if it comes later in the sort order than `other`. Returning zero causes the system to fall back to the secondary sort order defined by [OrderedTraversalPolicy.secondary]

# NumericFocusOrder

```dart
class NumericFocusOrder extends FocusOrder {}
```

Can be given to a [FocusTraversalOrder] widget to assign a numerical order to a widget subtree that is using a [OrderedTraversalPolicy] to define the order in which widgets should be traversed with the keyboard.

{@macro flutter.widgets.FocusOrder.comparable}

See also:

- [FocusTraversalOrder], a widget that assigns an order to a widget subtree for the [OrderedTraversalPolicy] to use.

### NumericFocusOrder()

```dart
NumericFocusOrder(double order)
```

Creates an object that describes a focus traversal order numerically.

### order

```dart
double order
```

The numerical order to assign to the widget subtree using [FocusTraversalOrder].

Determines the placement of this widget in a sequence of widgets that defines the order in which this node is traversed by the focus policy.

Lower values will be traversed first.

### doCompare()

```dart
int doCompare(NumericFocusOrder other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LexicalFocusOrder

```dart
class LexicalFocusOrder extends FocusOrder {}
```

Can be given to a [FocusTraversalOrder] widget to use a String to assign a lexical order to a widget subtree that is using a [OrderedTraversalPolicy] to define the order in which widgets should be traversed with the keyboard.

This sorts strings using Dart's default string comparison, which is not locale-specific.

{@macro flutter.widgets.FocusOrder.comparable}

See also:

- [FocusTraversalOrder], a widget that assigns an order to a widget subtree for the [OrderedTraversalPolicy] to use.

### LexicalFocusOrder()

```dart
LexicalFocusOrder(String order)
```

Creates an object that describes a focus traversal order lexically.

### order

```dart
String order
```

The String that defines the lexical order to assign to the widget subtree using [FocusTraversalOrder].

Determines the placement of this widget in a sequence of widgets that defines the order in which this node is traversed by the focus policy.

Lower lexical values will be traversed first (e.g. 'a' comes before 'z').

### doCompare()

```dart
int doCompare(LexicalFocusOrder other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OrderedTraversalPolicy

```dart
class OrderedTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

A [FocusTraversalPolicy] that orders nodes by an explicit order that resides in the nearest [FocusTraversalOrder] widget ancestor.

{@macro flutter.widgets.FocusOrder.comparable}

{@tool dartpad} This sample shows how to assign a traversal order to a widget. In the example, the focus order goes from bottom right (the "One" button) to top left (the "Six" button).

** See code in examples/api/lib/widgets/focus_traversal/ordered_traversal_policy.0.dart ** {@end-tool}

See also:

- [FocusTraversalGroup], a widget that groups together and imposes a traversal policy on the [Focus] nodes below it in the widget hierarchy.
- [WidgetOrderTraversalPolicy], a policy that relies on the widget creation order to describe the order of traversal.
- [ReadingOrderTraversalPolicy], a policy that describes the order as the natural "reading order" for the current [Directionality].
- [NumericFocusOrder], a focus order that assigns a numeric traversal order to a [FocusTraversalOrder] widget.
- [LexicalFocusOrder], a focus order that assigns a string-based lexical traversal order to a [FocusTraversalOrder] widget.
- [FocusOrder], an abstract base class for all types of focus traversal orderings.

### OrderedTraversalPolicy()

```dart
OrderedTraversalPolicy({FocusTraversalPolicy? secondary, void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

Constructs a traversal policy that orders widgets for keyboard traversal based on an explicit order.

If [secondary] is null, it will default to [ReadingOrderTraversalPolicy].

### secondary

```dart
FocusTraversalPolicy? secondary
```

This is the policy that is used when a node doesn't have an order assigned, or when multiple nodes have orders which are identical.

If not set, this defaults to [ReadingOrderTraversalPolicy].

This policy determines the secondary sorting order of nodes which evaluate as having an identical order (including those with no order specified).

Nodes with no order specified will be sorted after nodes with an explicit order.

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# FocusTraversalOrder

```dart
class FocusTraversalOrder extends InheritedWidget {}
```

An inherited widget that describes the order in which its child subtree should be traversed.

{@macro flutter.widgets.FocusOrder.comparable}

The order for a widget is determined by the [FocusOrder] returned by [FocusTraversalOrder.of] for a particular context.

### FocusTraversalOrder()

```dart
FocusTraversalOrder({dynamic key, required FocusOrder order, required Widget child})
```

Creates an inherited widget used to describe the focus order of the [child] subtree.

### order

```dart
FocusOrder order
```

The order for the widget descendants of this [FocusTraversalOrder].

### of()

```dart
FocusOrder of(BuildContext context)
```

Finds the [FocusOrder] in the nearest ancestor [FocusTraversalOrder] widget.

It does not create a rebuild dependency because changing the traversal order doesn't change the widget tree, so nothing needs to be rebuilt as a result of an order change.

If no [FocusTraversalOrder] ancestor exists, or the order is null, this will assert in debug mode, and throw an exception in release mode.

### maybeOf()

```dart
FocusOrder? maybeOf(BuildContext context)
```

Finds the [FocusOrder] in the nearest ancestor [FocusTraversalOrder] widget.

It does not create a rebuild dependency because changing the traversal order doesn't change the widget tree, so nothing needs to be rebuilt as a result of an order change.

If no [FocusTraversalOrder] ancestor exists, or the order is null, returns null.

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedWidget oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FocusTraversalGroup

```dart
class FocusTraversalGroup extends StatefulWidget {}
```

A widget that describes the inherited focus policy for focus traversal for its descendants, grouping them into a separate traversal group.

A traversal group is treated as one entity when sorted by the traversal algorithm, so it can be used to segregate different parts of the widget tree that need to be sorted using different algorithms and/or sort orders when using an [OrderedTraversalPolicy].

Within the group, it will use the given [policy] to order the elements. The group itself will be ordered using the parent group's policy.

By default, traverses in reading order using [ReadingOrderTraversalPolicy].

To prevent the members of the group from being focused, set the [descendantsAreFocusable] attribute to false.

{@tool dartpad} This sample shows three rows of buttons, each grouped by a [FocusTraversalGroup], each with different traversal order policies. Use tab traversal to see the order they are traversed in. The first row follows a numerical order, the second follows a lexical order (ordered to traverse right to left), and the third ignores the numerical order assigned to it and traverses in widget order.

** See code in examples/api/lib/widgets/focus_traversal/focus_traversal_group.0.dart ** {@end-tool}

See also:

- [FocusNode], for a description of the focus system.
- [WidgetOrderTraversalPolicy], a policy that relies on the widget creation order to describe the order of traversal.
- [ReadingOrderTraversalPolicy], a policy that describes the order as the natural "reading order" for the current [Directionality].
- [DirectionalFocusTraversalPolicyMixin] a mixin class that implements focus traversal in a direction.

### FocusTraversalGroup()

```dart
FocusTraversalGroup({dynamic key, FocusTraversalPolicy? policy, bool descendantsAreFocusable = true, bool descendantsAreTraversable = true, void Function(FocusNode)? onFocusNodeCreated, required Widget child})
```

Creates a [FocusTraversalGroup] object.

### policy

```dart
FocusTraversalPolicy policy
```

The policy used to move the focus from one focus node to another when traversing them using a keyboard.

If not specified, traverses in reading order using [ReadingOrderTraversalPolicy].

See also:

- [FocusTraversalPolicy] for the API used to impose traversal order policy.
- [WidgetOrderTraversalPolicy] for a traversal policy that traverses nodes in the order they are added to the widget tree.
- [ReadingOrderTraversalPolicy] for a traversal policy that traverses nodes in the reading order defined in the widget tree, and then top to bottom.

### descendantsAreFocusable

```dart
bool descendantsAreFocusable
```

{@macro flutter.widgets.Focus.descendantsAreFocusable}

### descendantsAreTraversable

```dart
bool descendantsAreTraversable
```

{@macro flutter.widgets.Focus.descendantsAreTraversable}

### child

```dart
Widget child
```

The child widget of this [FocusTraversalGroup].

{@macro flutter.widgets.ProxyWidget.child}

### onFocusNodeCreated

```dart
void Function(FocusNode)? onFocusNodeCreated
```

Called when the [FocusNode] of this widget is created.

### maybeOfNode()

```dart
FocusTraversalPolicy? maybeOfNode(FocusNode node)
```

Returns the [FocusTraversalPolicy] that applies to the nearest ancestor of the given [FocusNode].

Will return null if no [FocusTraversalPolicy] ancestor applies to the given [FocusNode].

The [FocusTraversalPolicy] is set by introducing a [FocusTraversalGroup] into the widget tree, which will associate a policy with the focus tree under the nearest ancestor [Focus] widget.

This function differs from [maybeOf] in that it takes a [FocusNode] and only traverses the focus tree to determine the policy in effect. Unlike this function, the [maybeOf] function takes a [BuildContext] and first walks up the widget tree to find the nearest ancestor [Focus] or [FocusScope] widget, and then calls this function with the focus node associated with that widget to determine the policy in effect.

### of()

```dart
FocusTraversalPolicy of(BuildContext context)
```

Returns the [FocusTraversalPolicy] that applies to the [FocusNode] of the nearest ancestor [Focus] widget, given a [BuildContext].

Will throw a [FlutterError] in debug mode, and throw a null check exception in release mode, if no [Focus] ancestor is found, or if no [FocusTraversalPolicy] applies to the associated [FocusNode].

{@template flutter.widgets.focus_traversal.FocusTraversalGroup.of} This function looks up the nearest ancestor [Focus] (or [FocusScope]) widget, and uses its [FocusNode] (or [FocusScopeNode]) to walk up the focus tree to find the applicable [FocusTraversalPolicy] for that node.

Calling this function does not create a rebuild dependency because changing the traversal order doesn't change the widget tree, so nothing needs to be rebuilt as a result of an order change.

The [FocusTraversalPolicy] is set by introducing a [FocusTraversalGroup] into the widget tree, which will associate a policy with the focus tree under the nearest ancestor [Focus] widget. {@endtemplate}

See also:

- [maybeOf] for a similar function that will return null if no [FocusTraversalGroup] ancestor is found.
- [maybeOfNode] for a function that will look for a policy using a given [FocusNode], and return null if no policy applies.

### maybeOf()

```dart
FocusTraversalPolicy? maybeOf(BuildContext context)
```

Returns the [FocusTraversalPolicy] that applies to the [FocusNode] of the nearest ancestor [Focus] widget, or null, given a [BuildContext].

Will return null if it doesn't find an ancestor [Focus] or [FocusScope] widget, or doesn't find a [FocusTraversalPolicy] that applies to the node.

{@macro flutter.widgets.focus_traversal.FocusTraversalGroup.of}

See also:

- [maybeOfNode] for a similar function that will look for a policy using a given [FocusNode].
- [of] for a similar function that will throw if no [FocusTraversalPolicy] applies.

### createState()

```dart
State<FocusTraversalGroup> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RequestFocusIntent

```dart
class RequestFocusIntent extends Intent {}
```

An intent for use with the [RequestFocusAction], which supplies the [FocusNode] that should be focused.

### RequestFocusIntent()

```dart
RequestFocusIntent(FocusNode focusNode, {TraversalRequestFocusCallback? requestFocusCallback})
```

Creates an intent used with [RequestFocusAction].

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### requestFocusCallback

```dart
TraversalRequestFocusCallback requestFocusCallback
```

The callback used to move the focus to the node [focusNode]. By default it requests focus on the node and ensures the node is visible if it's in a scrollable.

### focusNode

```dart
FocusNode focusNode
```

The [FocusNode] that is to be focused.

# RequestFocusAction

```dart
class RequestFocusAction extends Action<RequestFocusIntent> {}
```

An [Action] that requests the focus on the node it is given in its [RequestFocusIntent].

This action can be used to request focus for a particular node, by calling [Action.invoke] like so:

```dart
Actions.invoke(context, RequestFocusIntent(focusNode));
```

Where the `focusNode` is the node for which the focus will be requested.

The difference between requesting focus in this way versus calling [FocusNode.requestFocus] directly is that it will use the [Action] registered in the nearest [Actions] widget associated with [RequestFocusIntent] to make the request, rather than just requesting focus directly. This allows the action to have additional side effects, like logging, or undo and redo functionality.

This [RequestFocusAction] class is the default action associated with the [RequestFocusIntent] in the [WidgetsApp]. It requests focus. You can redefine the associated action with your own [Actions] widget.

See [FocusTraversalPolicy] for more information about focus traversal.

### invoke()

```dart
void invoke(RequestFocusIntent intent)
```

# NextFocusIntent

```dart
class NextFocusIntent extends Intent {}
```

An [Intent] bound to [NextFocusAction], which moves the focus to the next focusable node in the focus traversal order.

See [FocusTraversalPolicy] for more information about focus traversal.

### NextFocusIntent()

```dart
NextFocusIntent()
```

Creates an intent that is used with [NextFocusAction].

# NextFocusAction

```dart
class NextFocusAction extends Action<NextFocusIntent> {}
```

An [Action] that moves the focus to the next focusable node in the focus order.

This action is the default action registered for the [NextFocusIntent], and by default is bound to the [LogicalKeyboardKey.tab] key in the [WidgetsApp].

See [FocusTraversalPolicy] for more information about focus traversal.

### invoke()

```dart
bool invoke(NextFocusIntent intent)
```

Attempts to pass the focus to the next widget.

Returns true if a widget was focused as a result of invoking this action.

Returns false when the traversal reached the end and the engine must pass focus to platform UI.

### toKeyEventResult()

```dart
KeyEventResult toKeyEventResult(NextFocusIntent intent, bool invokeResult)
```

# PreviousFocusIntent

```dart
class PreviousFocusIntent extends Intent {}
```

An [Intent] bound to [PreviousFocusAction], which moves the focus to the previous focusable node in the focus traversal order.

See [FocusTraversalPolicy] for more information about focus traversal.

### PreviousFocusIntent()

```dart
PreviousFocusIntent()
```

Creates an intent that is used with [PreviousFocusAction].

# PreviousFocusAction

```dart
class PreviousFocusAction extends Action<PreviousFocusIntent> {}
```

An [Action] that moves the focus to the previous focusable node in the focus order.

This action is the default action registered for the [PreviousFocusIntent], and by default is bound to a combination of the [LogicalKeyboardKey.tab] key and the [LogicalKeyboardKey.shift] key in the [WidgetsApp].

See [FocusTraversalPolicy] for more information about focus traversal.

### invoke()

```dart
bool invoke(PreviousFocusIntent intent)
```

Attempts to pass the focus to the previous widget.

Returns true if a widget was focused as a result of invoking this action.

Returns false when the traversal reached the beginning and the engine must pass focus to platform UI.

### toKeyEventResult()

```dart
KeyEventResult toKeyEventResult(PreviousFocusIntent intent, bool invokeResult)
```

# DirectionalFocusIntent

```dart
class DirectionalFocusIntent extends Intent {}
```

An [Intent] that represents moving to the next focusable node in the given [direction].

This is the [Intent] bound by default to the [LogicalKeyboardKey.arrowUp], [LogicalKeyboardKey.arrowDown], [LogicalKeyboardKey.arrowLeft], and [LogicalKeyboardKey.arrowRight] keys in the [WidgetsApp], with the appropriate associated directions.

See [FocusTraversalPolicy] for more information about focus traversal.

### DirectionalFocusIntent()

```dart
DirectionalFocusIntent(TraversalDirection direction, {bool ignoreTextFields = true})
```

Creates an intent used to move the focus in the given [direction].

### direction

```dart
TraversalDirection direction
```

The direction in which to look for the next focusable node when the associated [DirectionalFocusAction] is invoked.

### ignoreTextFields

```dart
bool ignoreTextFields
```

If true, then directional focus actions that occur within a text field will not happen when the focus node which received the key is a text field.

Defaults to true.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DirectionalFocusAction

```dart
class DirectionalFocusAction extends Action<DirectionalFocusIntent> {}
```

An [Action] that moves the focus to the focusable node in the direction configured by the associated [DirectionalFocusIntent.direction].

This is the [Action] associated with [DirectionalFocusIntent] and bound by default to the [LogicalKeyboardKey.arrowUp], [LogicalKeyboardKey.arrowDown], [LogicalKeyboardKey.arrowLeft], and [LogicalKeyboardKey.arrowRight] keys in the [WidgetsApp], with the appropriate associated directions.

### DirectionalFocusAction()

```dart
DirectionalFocusAction()
```

Creates a [DirectionalFocusAction].

### DirectionalFocusAction.forTextField()

```dart
DirectionalFocusAction.forTextField()
```

Creates a [DirectionalFocusAction] that ignores [DirectionalFocusIntent]s whose `ignoreTextFields` field is true.

### invoke()

```dart
void invoke(DirectionalFocusIntent intent)
```

# ExcludeFocusTraversal

```dart
class ExcludeFocusTraversal extends StatelessWidget {}
```

A widget that controls whether or not the descendants of this widget are traversable.

Does not affect the value of [FocusNode.skipTraversal] of the descendants.

See also:

- [Focus], a widget for adding and managing a [FocusNode] in the widget tree.
- [ExcludeFocus], a widget that excludes its descendants from focusability.
- [FocusTraversalGroup], a widget that groups widgets for focus traversal, and can also be used in the same way as this widget by setting its `descendantsAreFocusable` attribute.

### ExcludeFocusTraversal()

```dart
ExcludeFocusTraversal({dynamic key, bool excluding = true, required Widget child})
```

Const constructor for [ExcludeFocusTraversal] widget.

### excluding

```dart
bool excluding
```

If true, will make this widget's descendants untraversable.

Defaults to true.

Does not affect the value of [FocusNode.skipTraversal] on the descendants.

See also:

- [Focus.descendantsAreTraversable], the attribute of a [Focus] widget that controls this same property for focus widgets.
- [FocusTraversalGroup], a widget used to group together and configure the focus traversal policy for a widget subtree that has a `descendantsAreFocusable` parameter to conditionally block focus for a subtree.

### child

```dart
Widget child
```

The child widget of this [ExcludeFocusTraversal].

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```
