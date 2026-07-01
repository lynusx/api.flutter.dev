@docImport 'package:flutter/widgets.dart';

# TreeSliverNodesAnimation

```dart
typedef TreeSliverNodesAnimation = ({int fromIndex, int toIndex, double value})
```

Represents the animation of the children of a parent [TreeSliverNode] that are animating into or out of view.

The `fromIndex` and `toIndex` are identify the animating children following the parent, with the `value` representing the status of the current animation. The value of `toIndex` is inclusive, meaning the child at that index is included in the animating segment.

Provided to [RenderTreeSliver] as part of [RenderTreeSliver.activeAnimations] by [TreeSliver] to properly offset animating children.

# TreeSliverNodeParentData

```dart
class TreeSliverNodeParentData extends SliverMultiBoxAdaptorParentData {}
```

Used to pass information down to [RenderTreeSliver].

### depth

```dart
int depth
```

The depth of the node, used by [RenderTreeSliver] to offset children by by the [TreeSliverIndentationType].

# TreeSliverIndentationType

```dart
class TreeSliverIndentationType {}
```

The style of indentation for [TreeSliverNode]s in a [TreeSliver], as handled by [RenderTreeSliver].

{@template flutter.rendering.TreeSliverIndentationType} By default, the indentation is handled by [RenderTreeSliver]. Child nodes are offset by the indentation specified by [TreeSliverIndentationType.value] in the cross axis of the viewport. This means the space allotted to the indentation will not be part of the space made available to the Widget returned by [TreeSliver.treeNodeBuilder].

Alternatively, the indentation can be implemented in [TreeSliver.treeNodeBuilder], with the depth of the given tree row accessed by [TreeSliverNode.depth]. This allows for more customization in building tree rows, such as filling the indented area with decorations or ink effects.

{@tool dartpad} This example shows a highly customized [TreeSliver] configured to [TreeSliverIndentationType.none]. This allows the indentation to be handled by the developer in [TreeSliver.treeNodeBuilder], where a decoration is used to fill the indented space.

** See code in examples/api/lib/widgets/sliver/sliver_tree.1.dart ** {@end-tool}

{@endtemplate}

### value

```dart
double get value
```

The number of pixels by which [TreeSliverNode]s will be offset according to their [TreeSliverNode.depth].

### standard

```dart
TreeSliverIndentationType standard
```

The default indentation of child [TreeSliverNode]s in a [TreeSliver].

Child nodes will be offset by 10 pixels for each level in the tree.

### none

```dart
TreeSliverIndentationType none
```

Configures no offsetting of child nodes in a [TreeSliver].

Useful if the indentation is implemented in the [TreeSliver.treeNodeBuilder] instead for more customization options.

Child nodes will not be offset in the tree.

### custom()

```dart
TreeSliverIndentationType custom(double value)
```

Configures a custom offset for indenting child nodes in a [TreeSliver].

Child nodes will be offset by the provided number of pixels in the tree. The [value] must be a non negative number.

# RenderTreeSliver

```dart
class RenderTreeSliver extends RenderSliverVariedExtentList {}
```

A sliver that places multiple [TreeSliverNode]s in a linear array along the main access, while staggering nodes that are animating into and out of view.

The extent of each child node is determined by the [itemExtentBuilder].

See also:

- [TreeSliver], the widget that creates and manages this render object.

### RenderTreeSliver()

```dart
RenderTreeSliver({required RenderSliverBoxChildManager childManager, required double? Function(int, SliverLayoutDimensions) itemExtentBuilder, required Map<UniqueKey, TreeSliverNodesAnimation> activeAnimations, required double indentation})
```

Creates the render object that lays out the [TreeSliverNode]s of a [TreeSliver].

### activeAnimations

```dart
Map<UniqueKey, TreeSliverNodesAnimation> get activeAnimations
```

The currently active [TreeSliverNode] animations.

Since the index of animating nodes can change at any time, the unique key is used to track an animation of nodes across frames.

### activeAnimations

```dart
set activeAnimations(Map<UniqueKey, TreeSliverNodesAnimation> value)
```

### indentation

```dart
double get indentation
```

The number of pixels by which child nodes will be offset in the cross axis based on their [TreeSliverNodeParentData.depth].

If zero, can alternatively offset children in [TreeSliver.treeNodeBuilder] for more options to customize the indented space.

### indentation

```dart
set indentation(double value)
```

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### dispose()

```dart
void dispose()
```

### performLayout()

```dart
void performLayout()
```

### getMinChildIndexForScrollOffset()

```dart
int getMinChildIndexForScrollOffset(double scrollOffset, double itemExtent)
```

### getMaxChildIndexForScrollOffset()

```dart
int getMaxChildIndexForScrollOffset(double scrollOffset, double itemExtent)
```

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderObject child)
```

### indexToLayoutOffset()

```dart
double indexToLayoutOffset(double itemExtent, int index)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```
