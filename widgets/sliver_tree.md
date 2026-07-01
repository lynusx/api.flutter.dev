@docImport 'viewport.dart';

# TreeSliverNode

```dart
class TreeSliverNode<T> {}
```

A data structure for configuring children of a [TreeSliver].

A [TreeSliverNode.content] can be of any type [T], but must correspond with the same type of the [TreeSliver].

The values returned by [depth], [parent] and [isExpanded] getters are managed by the [TreeSliver]'s state.

### TreeSliverNode()

```dart
TreeSliverNode(T content, {List<TreeSliverNode<T>>? children, bool expanded = false})
```

Creates a [TreeSliverNode] instance for use in a [TreeSliver].

### content

```dart
T get content
```

The subject matter of the node.

Must correspond with the type of [TreeSliver].

### children

```dart
List<TreeSliverNode<T>> get children
```

Other [TreeSliverNode]s that this node will be [parent] to.

Modifying the children of nodes in a [TreeSliver] will cause the tree to be rebuilt so that newly added active nodes are reflected in the tree.

### isExpanded

```dart
bool get isExpanded
```

Whether or not this node is expanded in the tree.

Cannot be expanded if there are no children.

### depth

```dart
int? get depth
```

The number of parent nodes between this node and the root of the tree.

### parent

```dart
TreeSliverNode<T>? get parent
```

The parent [TreeSliverNode] of this node.

### toString()

```dart
String toString()
```

# TreeSliverNodeBuilder

```dart
typedef TreeSliverNodeBuilder = Widget Function(BuildContext context, TreeSliverNode<Object?> node, AnimationStyle animationStyle)
```

Signature for a function that creates a [Widget] to represent the given [TreeSliverNode] in the [TreeSliver].

Used by [TreeSliver.treeNodeBuilder] to build rows on demand for the tree.

# TreeSliverRowExtentBuilder

```dart
typedef TreeSliverRowExtentBuilder = double Function(TreeSliverNode<Object?> node, SliverLayoutDimensions dimensions)
```

Signature for a function that returns an extent for the given [TreeSliverNode] in the [TreeSliver].

Used by [TreeSliver.treeRowExtentBuilder] to size rows on demand in the tree. The provided [SliverLayoutDimensions] provide information about the current scroll state and [Viewport] dimensions.

See also:

- [SliverVariedExtentList], which uses a similar item extent builder for dynamic child sizing in the list.

# TreeSliverNodeCallback

```dart
typedef TreeSliverNodeCallback = void Function(TreeSliverNode<Object?> node)
```

Signature for a function that is called when a [TreeSliverNode] is toggled, changing its expanded state.

See also:

- [TreeSliver.onNodeToggle], for controlling node expansion programmatically.

# TreeSliverStateMixin

```dart
mixin TreeSliverStateMixin<T> {}
```

A mixin for classes implementing a tree structure as expected by a [TreeSliverController].

Used by [TreeSliver] to implement an interface for the [TreeSliverController].

This allows the [TreeSliverController] to be used in other widgets that implement this interface.

The type [T] correlates to the type of [TreeSliver] and [TreeSliverNode], representing the type of [TreeSliverNode.content].

### isExpanded()

```dart
bool isExpanded(TreeSliverNode<T> node)
```

Returns whether or not the given [TreeSliverNode] is expanded.

### isActive()

```dart
bool isActive(TreeSliverNode<T> node)
```

Returns whether or not the given [TreeSliverNode] is enclosed within its parent [TreeSliverNode].

If the [TreeSliverNode.parent] [isExpanded] (and all its parents are expanded), or this is a root node, the given node is active and this method will return true. This does not reflect whether or not the node is visible in the [Viewport].

### toggleNode()

```dart
void toggleNode(TreeSliverNode<T> node)
```

Switches the given [TreeSliverNode]s expanded state.

May trigger an animation to reveal or hide the node's children based on the [TreeSliver.toggleAnimationStyle].

If the node does not have any children, nothing will happen.

### collapseAll()

```dart
void collapseAll()
```

Closes all parent [TreeSliverNode]s in the tree.

### expandAll()

```dart
void expandAll()
```

Expands all parent [TreeSliverNode]s in the tree.

### getNodeFor()

```dart
TreeSliverNode<T>? getNodeFor(T content)
```

Retrieves the [TreeSliverNode] containing the associated content, if it exists.

If no node exists, this will return null. This does not reflect whether or not a node [isActive], or if it is visible in the viewport.

### getActiveIndexFor()

```dart
int? getActiveIndexFor(TreeSliverNode<T> node)
```

Returns the current row index of the given [TreeSliverNode].

If the node is not currently active in the tree, meaning its parent is collapsed, this will return null.

# TreeSliverController

```dart
class TreeSliverController {}
```

Enables control over the [TreeSliverNode]s of a [TreeSliver].

It can be useful to expand or collapse nodes of the tree programmatically, for example to reconfigure an existing node based on a system event. To do so, create a [TreeSliver] with a [TreeSliverController] that's owned by a stateful widget or look up the tree's automatically created [TreeSliverController] with [TreeSliverController.of]

The controller's methods to expand or collapse nodes cause the the [TreeSliver] to rebuild, so they may not be called from a build method.

### TreeSliverController()

```dart
TreeSliverController()
```

Create a controller to be used with [TreeSliver.controller].

### isExpanded()

```dart
bool isExpanded(TreeSliverNode<Object?> node)
```

Whether the given [TreeSliverNode] built with this controller is in an expanded state.

See also:

- [expandNode], which expands a given [TreeSliverNode].
- [collapseNode], which collapses a given [TreeSliverNode].
- [TreeSliver.controller] to create a TreeSliver with a controller.

### isActive()

```dart
bool isActive(TreeSliverNode<Object?> node)
```

Whether or not the given [TreeSliverNode] is enclosed within its parent [TreeSliverNode].

If the [TreeSliverNode.parent] [isExpanded], or this is a root node, the given node is active and this method will return true. This does not reflect whether or not the node is visible in the [Viewport].

### getNodeFor()

```dart
TreeSliverNode<Object?>? getNodeFor(Object? content)
```

Returns the [TreeSliverNode] containing the associated content, if it exists.

If no node exists, this will return null. This does not reflect whether or not a node [isActive], or if it is currently visible in the viewport.

### toggleNode()

```dart
void toggleNode(TreeSliverNode<Object?> node)
```

Switches the given [TreeSliverNode]s expanded state.

May trigger an animation to reveal or hide the node's children based on the [TreeSliver.toggleAnimationStyle].

If the node does not have any children, nothing will happen.

### expandNode()

```dart
void expandNode(TreeSliverNode<Object?> node)
```

Expands the [TreeSliverNode] that was built with this controller.

If the node is already in the expanded state (see [isExpanded]), calling this method has no effect.

Calling this method may cause the [TreeSliver] to rebuild, so it may not be called from a build method.

Calling this method will trigger the [TreeSliver.onNodeToggle] callback.

See also:

- [collapseNode], which collapses the [TreeSliverNode].
- [isExpanded] to check whether the tile is expanded.
- [TreeSliver.controller] to create a TreeSliver with a controller.

### expandAll()

```dart
void expandAll()
```

Expands all parent [TreeSliverNode]s in the tree.

### collapseAll()

```dart
void collapseAll()
```

Closes all parent [TreeSliverNode]s in the tree.

### collapseNode()

```dart
void collapseNode(TreeSliverNode<Object?> node)
```

Collapses the [TreeSliverNode] that was built with this controller.

If the node is already in the collapsed state (see [isExpanded]), calling this method has no effect.

Calling this method may cause the [TreeSliver] to rebuild, so it may not be called from a build method.

Calling this method will trigger the [TreeSliver.onNodeToggle] callback.

See also:

- [expandNode], which expands the tile.
- [isExpanded] to check whether the tile is expanded.
- [TreeSliver.controller] to create a TreeSliver with a controller.

### getActiveIndexFor()

```dart
int? getActiveIndexFor(TreeSliverNode<Object?> node)
```

Returns the current row index of the given [TreeSliverNode].

If the node is not currently active in the tree, meaning its parent is collapsed, this will return null.

### of()

```dart
TreeSliverController of(BuildContext context)
```

Finds the [TreeSliverController] for the closest [TreeSliver] instance that encloses the given context.

If no [TreeSliver] encloses the given context, calling this method will cause an assert in debug mode, and throw an exception in release mode.

To return null if there is no [TreeSliver] use [maybeOf] instead.

Typical usage of the [TreeSliverController.of] function is to call it from within the `build` method of a descendant of a [TreeSliver].

When the [TreeSliver] is actually created in the same `build` function as the callback that refers to the controller, then the `context` argument to the `build` function can't be used to find the [TreeSliverController] (since it's "above" the widget being returned in the widget tree). In cases like that you can add a [Builder] widget, which provides a new scope with a [BuildContext] that is "under" the [TreeSliver].

### maybeOf()

```dart
TreeSliverController? maybeOf(BuildContext context)
```

Finds the [TreeSliver] from the closest instance of this class that encloses the given context and returns its [TreeSliverController].

If no [TreeSliver] encloses the given context then return null. To throw an exception instead, use [of] instead of this function.

See also:

- [of], a similar function to this one that throws if no [TreeSliver] encloses the given context. Also includes some sample code in its documentation.

# TreeSliver

```dart
class TreeSliver<T> extends StatefulWidget {}
```

A widget that displays [TreeSliverNode]s that expand and collapse in a vertically and horizontally scrolling [Viewport].

The type [T] correlates to the type of [TreeSliver] and [TreeSliverNode], representing the type of [TreeSliverNode.content].

The rows of the tree are laid out on demand by the [Viewport]'s render object, using [TreeSliver.treeNodeBuilder]. This will only be called for the nodes that are visible, or within the [Viewport.cacheExtent].

The [TreeSliver.treeNodeBuilder] returns the [Widget] that represents the given [TreeSliverNode].

The [TreeSliver.treeRowExtentBuilder] returns a double representing the extent of a given node in the main axis.

Providing a [TreeSliverController] will enable querying and controlling the state of nodes in the tree.

A [TreeSliver] only supports a vertical axis direction of [AxisDirection.down] and a horizontal axis direction of [AxisDirection.right].

{@tool dartpad} This example uses a [TreeSliver] to display nodes, highlighting nodes as they are selected.

** See code in examples/api/lib/widgets/sliver/sliver_tree.0.dart ** {@end-tool}

{@tool dartpad} This example shows a highly customized [TreeSliver] configured to [TreeSliverIndentationType.none]. This allows the indentation to be handled by the developer in [TreeSliver.treeNodeBuilder], where a decoration is used to fill the indented space.

** See code in examples/api/lib/widgets/sliver/sliver_tree.1.dart ** {@end-tool}

### TreeSliver()

```dart
TreeSliver({dynamic key, required List<TreeSliverNode<T>> tree, TreeSliverNodeBuilder treeNodeBuilder = TreeSliver.defaultTreeNodeBuilder, TreeSliverRowExtentBuilder treeRowExtentBuilder = TreeSliver.defaultTreeRowExtentBuilder, TreeSliverController? controller, TreeSliverNodeCallback? onNodeToggle, AnimationStyle? toggleAnimationStyle, TreeSliverIndentationType indentation = TreeSliverIndentationType.standard, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, SemanticIndexCallback semanticIndexCallback = _kDefaultSemanticIndexCallback, int semanticIndexOffset = 0, int? Function(Key)? findChildIndexCallback})
```

Creates an instance of a [TreeSliver] for displaying [TreeSliverNode]s that animate expanding and collapsing of nodes.

### tree

```dart
List<TreeSliverNode<T>> tree
```

The list of [TreeSliverNode]s that may be displayed in the [TreeSliver].

Beyond root nodes, whether or not a given [TreeSliverNode] is displayed depends on the [TreeSliverNode.isExpanded] value of its parent. The [TreeSliver] will set the [TreeSliverNode.parent] and [TreeSliverNode.depth] as nodes are built on demand to ensure the integrity of the tree.

### treeNodeBuilder

```dart
TreeSliverNodeBuilder treeNodeBuilder
```

Called to build and entry of the [TreeSliver] for the given node.

By default, if this is unset, the [TreeSliver.defaultTreeNodeBuilder] is used.

### treeRowExtentBuilder

```dart
TreeSliverRowExtentBuilder treeRowExtentBuilder
```

Called to calculate the extent of the widget built for the given [TreeSliverNode].

By default, if this is unset, the [TreeSliver.defaultTreeRowExtentBuilder] is used.

See also:

- [SliverVariedExtentList.itemExtentBuilder], a very similar method that allows users to dynamically compute extents on demand.

### controller

```dart
TreeSliverController? controller
```

If provided, the controller can be used to expand and collapse [TreeSliverNode]s, or lookup information about the current state of the [TreeSliver].

### onNodeToggle

```dart
TreeSliverNodeCallback? onNodeToggle
```

Called when a [TreeSliverNode] expands or collapses.

This will not be called if a [TreeSliverNode] does not have any children.

### toggleAnimationStyle

```dart
AnimationStyle? toggleAnimationStyle
```

The default [AnimationStyle] for expanding and collapsing nodes in the [TreeSliver].

The default [AnimationStyle.duration] uses [TreeSliver.defaultAnimationDuration], which is 150 milliseconds.

The default [AnimationStyle.curve] uses [TreeSliver.defaultAnimationCurve], which is [Curves.linear].

To disable the tree animation, use [AnimationStyle.noAnimation].

### indentation

```dart
TreeSliverIndentationType indentation
```

The number of pixels children will be offset by in the cross axis based on their [TreeSliverNode.depth].

{@macro flutter.rendering.TreeSliverIndentationType}

### addAutomaticKeepAlives

```dart
bool addAutomaticKeepAlives
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addAutomaticKeepAlives}

### addRepaintBoundaries

```dart
bool addRepaintBoundaries
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addRepaintBoundaries}

### addSemanticIndexes

```dart
bool addSemanticIndexes
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addSemanticIndexes}

### semanticIndexCallback

```dart
SemanticIndexCallback semanticIndexCallback
```

{@macro flutter.widgets.SliverChildBuilderDelegate.semanticIndexCallback}

### semanticIndexOffset

```dart
int semanticIndexOffset
```

{@macro flutter.widgets.SliverChildBuilderDelegate.semanticIndexOffset}

### findChildIndexCallback

```dart
int? Function(Key)? findChildIndexCallback
```

{@macro flutter.widgets.SliverChildBuilderDelegate.findChildIndexCallback}

### defaultToggleAnimationStyle

```dart
AnimationStyle defaultToggleAnimationStyle
```

The default [AnimationStyle] used for node expand and collapse animations, when one has not been provided in [toggleAnimationStyle].

### defaultAnimationCurve

```dart
Curve defaultAnimationCurve
```

A default of [Curves.linear], which is used in the tree's expanding and collapsing node animation.

### defaultAnimationDuration

```dart
Duration defaultAnimationDuration
```

A default [Duration] of 150 milliseconds, which is used in the tree's expanding and collapsing node animation.

### wrapChildToToggleNode()

```dart
Widget wrapChildToToggleNode({required TreeSliverNode<Object?> node, required Widget child})
```

A wrapper method for triggering the expansion or collapse of a [TreeSliverNode].

Used as part of [TreeSliver.defaultTreeNodeBuilder] to wrap the leading icon of parent [TreeSliverNode]s such that tapping on it triggers the animation.

If defining your own [TreeSliver.treeNodeBuilder], this method can be used to wrap any part, or all, of the returned widget in order to trigger the change in state for the node.

### defaultTreeRowExtentBuilder()

```dart
double defaultTreeRowExtentBuilder(TreeSliverNode<Object?> node, SliverLayoutDimensions dimensions)
```

Returns the fixed default extent for rows in the tree, which is 40 pixels.

Used by [TreeSliver.treeRowExtentBuilder].

### defaultTreeNodeBuilder()

```dart
Widget defaultTreeNodeBuilder(BuildContext context, TreeSliverNode<Object?> node, AnimationStyle toggleAnimationStyle)
```

Returns the default tree row for a given [TreeSliverNode].

Used by [TreeSliver.treeNodeBuilder].

This will return a [Row] containing the [toString] of [TreeSliverNode.content]. If the [TreeSliverNode] is a parent of additional nodes, a arrow icon will precede the content, and will trigger an expand and collapse animation when tapped.

### createState()

```dart
State<TreeSliver<T>> createState()
```
