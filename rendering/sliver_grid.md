@docImport 'package:flutter/widgets.dart';

@docImport 'sliver_fixed_extent_list.dart'; @docImport 'sliver_list.dart';

# SliverGridGeometry

```dart
class SliverGridGeometry {}
```

Describes the placement of a child in a [RenderSliverGrid].

This class is similar to [Rect], in that it gives a two-dimensional position and a two-dimensional dimension, but is direction-agnostic.

{@tool dartpad} This example shows how a custom [SliverGridLayout] uses [SliverGridGeometry] to lay out the children.

** See code in examples/api/lib/widgets/scroll_view/grid_view.0.dart ** {@end-tool}

See also:

- [SliverGridLayout], which represents the geometry of all the tiles in a grid.
- [SliverGridLayout.getGeometryForChildIndex], which returns this object to describe the child's placement.
- [RenderSliverGrid], which uses this class during its [RenderSliverGrid.performLayout] method.

### SliverGridGeometry()

```dart
SliverGridGeometry({required double scrollOffset, required double crossAxisOffset, required double mainAxisExtent, required double crossAxisExtent})
```

Creates an object that describes the placement of a child in a [RenderSliverGrid].

### scrollOffset

```dart
double scrollOffset
```

The scroll offset of the leading edge of the child relative to the leading edge of the parent.

### crossAxisOffset

```dart
double crossAxisOffset
```

The offset of the child in the non-scrolling axis.

If the scroll axis is vertical, this offset is from the left-most edge of the parent to the left-most edge of the child. If the scroll axis is horizontal, this offset is from the top-most edge of the parent to the top-most edge of the child.

### mainAxisExtent

```dart
double mainAxisExtent
```

The extent of the child in the scrolling axis.

If the scroll axis is vertical, this extent is the child's height. If the scroll axis is horizontal, this extent is the child's width.

### crossAxisExtent

```dart
double crossAxisExtent
```

The extent of the child in the non-scrolling axis.

If the scroll axis is vertical, this extent is the child's width. If the scroll axis is horizontal, this extent is the child's height.

### trailingScrollOffset

```dart
double get trailingScrollOffset
```

The scroll offset of the trailing edge of the child relative to the leading edge of the parent.

### getBoxConstraints()

```dart
BoxConstraints getBoxConstraints(SliverConstraints constraints)
```

Returns a tight [BoxConstraints] that forces the child to have the required size, given a [SliverConstraints].

### toString()

```dart
String toString()
```

# SliverGridLayout

```dart
abstract class SliverGridLayout {}
```

The size and position of all the tiles in a [RenderSliverGrid].

Rather that providing a grid with a [SliverGridLayout] directly, the grid is provided a [SliverGridDelegate], which computes a [SliverGridLayout] given a set of [SliverConstraints]. This allows the algorithm to dynamically respond to changes in the environment (e.g. the user rotating the device).

The tiles can be placed arbitrarily, but it is more efficient to place tiles roughly in order by scroll offset because grids reify a contiguous sequence of children.

{@tool dartpad} This example shows how to construct a custom [SliverGridLayout] to lay tiles in a grid form with some cells stretched to fit the entire width of the grid (sometimes called "hero tiles").

** See code in examples/api/lib/widgets/scroll_view/grid_view.0.dart ** {@end-tool}

See also:

- [SliverGridRegularTileLayout], which represents a layout that uses equally sized and spaced tiles.
- [SliverGridGeometry], which represents the size and position of a single tile in a grid.
- [SliverGridDelegate.getLayout], which returns this object to describe the delegate's layout.
- [RenderSliverGrid], which uses this class during its [RenderSliverGrid.performLayout] method.

### SliverGridLayout()

```dart
SliverGridLayout()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getMinChildIndexForScrollOffset()

```dart
int getMinChildIndexForScrollOffset(double scrollOffset)
```

The minimum child index that intersects with (or is after) this scroll offset.

### getMaxChildIndexForScrollOffset()

```dart
int getMaxChildIndexForScrollOffset(double scrollOffset)
```

The maximum child index that intersects with (or is before) this scroll offset.

### getGeometryForChildIndex()

```dart
SliverGridGeometry getGeometryForChildIndex(int index)
```

The size and position of the child with the given index.

### computeMaxScrollOffset()

```dart
double computeMaxScrollOffset(int childCount)
```

The scroll extent needed to fully display all the tiles if there are `childCount` children in total.

The child count will never be null.

# SliverGridRegularTileLayout

```dart
class SliverGridRegularTileLayout extends SliverGridLayout {}
```

A [SliverGridLayout] that uses equally sized and spaced tiles.

Rather that providing a grid with a [SliverGridLayout] directly, you instead provide the grid a [SliverGridDelegate], which can compute a [SliverGridLayout] given the current [SliverConstraints].

This layout is used by [SliverGridDelegateWithFixedCrossAxisCount] and [SliverGridDelegateWithMaxCrossAxisExtent].

See also:

- [SliverGridDelegateWithFixedCrossAxisCount], which uses this layout.
- [SliverGridDelegateWithMaxCrossAxisExtent], which uses this layout.
- [SliverGridLayout], which represents an arbitrary tile layout.
- [SliverGridGeometry], which represents the size and position of a single tile in a grid.
- [SliverGridDelegate.getLayout], which returns this object to describe the delegate's layout.
- [RenderSliverGrid], which uses this class during its [RenderSliverGrid.performLayout] method.

### SliverGridRegularTileLayout()

```dart
SliverGridRegularTileLayout({required int crossAxisCount, required double mainAxisStride, required double crossAxisStride, required double childMainAxisExtent, required double childCrossAxisExtent, required bool reverseCrossAxis})
```

Creates a layout that uses equally sized and spaced tiles.

All of the arguments must not be negative. The `crossAxisCount` argument must be greater than zero.

### crossAxisCount

```dart
int crossAxisCount
```

The number of children in the cross axis.

### mainAxisStride

```dart
double mainAxisStride
```

The number of pixels from the leading edge of one tile to the leading edge of the next tile in the main axis.

### crossAxisStride

```dart
double crossAxisStride
```

The number of pixels from the leading edge of one tile to the leading edge of the next tile in the cross axis.

### childMainAxisExtent

```dart
double childMainAxisExtent
```

The number of pixels from the leading edge of one tile to the trailing edge of the same tile in the main axis.

### childCrossAxisExtent

```dart
double childCrossAxisExtent
```

The number of pixels from the leading edge of one tile to the trailing edge of the same tile in the cross axis.

### reverseCrossAxis

```dart
bool reverseCrossAxis
```

Whether the children should be placed in the opposite order of increasing coordinates in the cross axis.

For example, if the cross axis is horizontal, the children are placed from left to right when [reverseCrossAxis] is false and from right to left when [reverseCrossAxis] is true.

Typically set to the return value of [axisDirectionIsReversed] applied to the [SliverConstraints.crossAxisDirection].

### getMinChildIndexForScrollOffset()

```dart
int getMinChildIndexForScrollOffset(double scrollOffset)
```

### getMaxChildIndexForScrollOffset()

```dart
int getMaxChildIndexForScrollOffset(double scrollOffset)
```

### getGeometryForChildIndex()

```dart
SliverGridGeometry getGeometryForChildIndex(int index)
```

### computeMaxScrollOffset()

```dart
double computeMaxScrollOffset(int childCount)
```

# SliverGridDelegate

```dart
abstract class SliverGridDelegate {}
```

Controls the layout of tiles in a grid.

Given the current constraints on the grid, a [SliverGridDelegate] computes the layout for the tiles in the grid. The tiles can be placed arbitrarily, but it is more efficient to place tiles roughly in order by scroll offset because grids reify a contiguous sequence of children.

{@tool dartpad} This example shows how a [SliverGridDelegate] returns a [SliverGridLayout] configured based on the provided [SliverConstraints] in [getLayout].

** See code in examples/api/lib/widgets/scroll_view/grid_view.0.dart ** {@end-tool}

See also:

- [SliverGridDelegateWithFixedCrossAxisCount], which creates a layout with a fixed number of tiles in the cross axis.
- [SliverGridDelegateWithMaxCrossAxisExtent], which creates a layout with tiles that have a maximum cross-axis extent.
- [GridView], which uses this delegate to control the layout of its tiles.
- [SliverGrid], which uses this delegate to control the layout of its tiles.
- [RenderSliverGrid], which uses this delegate to control the layout of its tiles.

### SliverGridDelegate()

```dart
SliverGridDelegate()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### getLayout()

```dart
SliverGridLayout getLayout(SliverConstraints constraints)
```

Returns information about the size and position of the tiles in the grid.

### shouldRelayout()

```dart
bool shouldRelayout(SliverGridDelegate oldDelegate)
```

Override this method to return true when the children need to be laid out.

This should compare the fields of the current delegate and the given `oldDelegate` and return true if the fields are such that the layout would be different.

# SliverGridDelegateWithFixedCrossAxisCount

```dart
class SliverGridDelegateWithFixedCrossAxisCount extends SliverGridDelegate {}
```

Creates grid layouts with a fixed number of tiles in the cross axis.

For example, if the grid is vertical, this delegate will create a layout with a fixed number of columns. If the grid is horizontal, this delegate will create a layout with a fixed number of rows.

This delegate creates grids with equally sized and spaced tiles.

{@tool dartpad} Here is an example using the [childAspectRatio] property. On a device with a screen width of 800.0, it creates a GridView with each tile with a width of 200.0 and a height of 100.0.

** See code in examples/api/lib/rendering/sliver_grid/sliver_grid_delegate_with_fixed_cross_axis_count.0.dart ** {@end-tool}

{@tool dartpad} Here is an example using the [mainAxisExtent] property. On a device with a screen width of 800.0, it creates a GridView with each tile with a width of 200.0 and a height of 150.0.

** See code in examples/api/lib/rendering/sliver_grid/sliver_grid_delegate_with_fixed_cross_axis_count.1.dart ** {@end-tool}

See also:

- [SliverGridDelegateWithMaxCrossAxisExtent], which creates a layout with tiles that have a maximum cross-axis extent.
- [SliverGridDelegate], which creates arbitrary layouts.
- [GridView], which can use this delegate to control the layout of its tiles.
- [SliverGrid], which can use this delegate to control the layout of its tiles.
- [RenderSliverGrid], which can use this delegate to control the layout of its tiles.

### SliverGridDelegateWithFixedCrossAxisCount()

```dart
SliverGridDelegateWithFixedCrossAxisCount({required int crossAxisCount, double mainAxisSpacing = 0.0, double crossAxisSpacing = 0.0, double childAspectRatio = 1.0, double? mainAxisExtent})
```

Creates a delegate that makes grid layouts with a fixed number of tiles in the cross axis.

The `mainAxisSpacing`, `mainAxisExtent` and `crossAxisSpacing` arguments must not be negative. The `crossAxisCount` and `childAspectRatio` arguments must be greater than zero.

### crossAxisCount

```dart
int crossAxisCount
```

The number of children in the cross axis.

### mainAxisSpacing

```dart
double mainAxisSpacing
```

The number of logical pixels between each child along the main axis.

### crossAxisSpacing

```dart
double crossAxisSpacing
```

The number of logical pixels between each child along the cross axis.

### childAspectRatio

```dart
double childAspectRatio
```

The ratio of the cross-axis to the main-axis extent of each child.

### mainAxisExtent

```dart
double? mainAxisExtent
```

The extent of each tile in the main axis. If provided it would define the logical pixels taken by each tile in the main-axis.

If null, [childAspectRatio] is used instead.

### getLayout()

```dart
SliverGridLayout getLayout(SliverConstraints constraints)
```

### shouldRelayout()

```dart
bool shouldRelayout(SliverGridDelegateWithFixedCrossAxisCount oldDelegate)
```

# SliverGridDelegateWithMaxCrossAxisExtent

```dart
class SliverGridDelegateWithMaxCrossAxisExtent extends SliverGridDelegate {}
```

Creates grid layouts with tiles that each have a maximum cross-axis extent.

This delegate will select a cross-axis extent for the tiles that is as large as possible subject to the following conditions:

- The extent evenly divides the cross-axis extent of the grid.
- The extent is at most [maxCrossAxisExtent].

For example, if the grid is vertical, the grid is 500.0 pixels wide, and [maxCrossAxisExtent] is 150.0, this delegate will create a grid with 4 columns that are 125.0 pixels wide.

This delegate creates grids with equally sized and spaced tiles.

See also:

- [SliverGridDelegateWithFixedCrossAxisCount], which creates a layout with a fixed number of tiles in the cross axis.
- [SliverGridDelegate], which creates arbitrary layouts.
- [GridView], which can use this delegate to control the layout of its tiles.
- [SliverGrid], which can use this delegate to control the layout of its tiles.
- [RenderSliverGrid], which can use this delegate to control the layout of its tiles.

### SliverGridDelegateWithMaxCrossAxisExtent()

```dart
SliverGridDelegateWithMaxCrossAxisExtent({required double maxCrossAxisExtent, double mainAxisSpacing = 0.0, double crossAxisSpacing = 0.0, double childAspectRatio = 1.0, double? mainAxisExtent})
```

Creates a delegate that makes grid layouts with tiles that have a maximum cross-axis extent.

The [maxCrossAxisExtent], [mainAxisExtent], [mainAxisSpacing], and [crossAxisSpacing] arguments must not be negative. The [childAspectRatio] argument must be greater than zero.

### maxCrossAxisExtent

```dart
double maxCrossAxisExtent
```

The maximum extent of tiles in the cross axis.

This delegate will select a cross-axis extent for the tiles that is as large as possible subject to the following conditions:

- The extent evenly divides the cross-axis extent of the grid.
- The extent is at most [maxCrossAxisExtent].

For example, if the grid is vertical, the grid is 500.0 pixels wide, and [maxCrossAxisExtent] is 150.0, this delegate will create a grid with 4 columns that are 125.0 pixels wide.

### mainAxisSpacing

```dart
double mainAxisSpacing
```

The number of logical pixels between each child along the main axis.

### crossAxisSpacing

```dart
double crossAxisSpacing
```

The number of logical pixels between each child along the cross axis.

### childAspectRatio

```dart
double childAspectRatio
```

The ratio of the cross-axis to the main-axis extent of each child.

### mainAxisExtent

```dart
double? mainAxisExtent
```

The extent of each tile in the main axis. If provided it would define the logical pixels taken by each tile in the main-axis.

If null, [childAspectRatio] is used instead.

### getLayout()

```dart
SliverGridLayout getLayout(SliverConstraints constraints)
```

### shouldRelayout()

```dart
bool shouldRelayout(SliverGridDelegateWithMaxCrossAxisExtent oldDelegate)
```

# SliverGridParentData

```dart
class SliverGridParentData extends SliverMultiBoxAdaptorParentData {}
```

Parent data structure used by [RenderSliverGrid].

### crossAxisOffset

```dart
double? crossAxisOffset
```

The offset of the child in the non-scrolling axis.

If the scroll axis is vertical, this offset is from the left-most edge of the parent to the left-most edge of the child. If the scroll axis is horizontal, this offset is from the top-most edge of the parent to the top-most edge of the child.

### toString()

```dart
String toString()
```

# RenderSliverGrid

```dart
class RenderSliverGrid extends RenderSliverMultiBoxAdaptor {}
```

A sliver that places multiple box children in a two dimensional arrangement.

[RenderSliverGrid] places its children in arbitrary positions determined by [gridDelegate]. Each child is forced to have the size specified by the [gridDelegate].

See also:

- [RenderSliverList], which places its children in a linear array.
- [RenderSliverFixedExtentList], which places its children in a linear array with a fixed extent in the main axis.

### RenderSliverGrid()

```dart
RenderSliverGrid({required RenderSliverBoxChildManager childManager, required SliverGridDelegate gridDelegate})
```

Creates a sliver that contains multiple box children that whose size and position are determined by a delegate.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### gridDelegate

```dart
SliverGridDelegate get gridDelegate
```

The delegate that controls the size and position of the children.

### gridDelegate

```dart
set gridDelegate(SliverGridDelegate value)
```

### childCrossAxisPosition()

```dart
double childCrossAxisPosition(RenderBox child)
```

### performLayout()

```dart
void performLayout()
```
