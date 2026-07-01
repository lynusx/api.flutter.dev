@docImport 'sliver_fill.dart'; @docImport 'sliver_list.dart';

# RenderSliverFixedExtentBoxAdaptor

```dart
abstract class RenderSliverFixedExtentBoxAdaptor extends RenderSliverMultiBoxAdaptor {}
```

A sliver that contains multiple box children that have the explicit extent in the main axis.

[RenderSliverFixedExtentBoxAdaptor] places its children in a linear array along the main axis. Each child is forced to have the returned value of [itemExtentBuilder] when the [itemExtentBuilder] is non-null or the [itemExtent] when [itemExtentBuilder] is null in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

Subclasses should override [itemExtent] or [itemExtentBuilder] to control the size of the children in the main axis. For a concrete subclass with a configurable [itemExtent], see [RenderSliverFixedExtentList] or [RenderSliverVariedExtentList].

[RenderSliverFixedExtentBoxAdaptor] is more efficient than [RenderSliverList] because [RenderSliverFixedExtentBoxAdaptor] does not need to perform layout on its children to obtain their extent in the main axis.

See also:

- [RenderSliverFixedExtentList], which has a configurable [itemExtent].
- [RenderSliverFillViewport], which determines the [itemExtent] based on [SliverConstraints.viewportMainAxisExtent].
- [RenderSliverFillRemaining], which determines the [itemExtent] based on [SliverConstraints.remainingPaintExtent].
- [RenderSliverList], which does not require its children to have the same extent in the main axis.

### RenderSliverFixedExtentBoxAdaptor()

```dart
RenderSliverFixedExtentBoxAdaptor({required RenderSliverBoxChildManager childManager})
```

Creates a sliver that contains multiple box children that have the same extent in the main axis.

### itemExtent

```dart
double? get itemExtent
```

The main-axis extent of each item.

If this is non-null, the [itemExtentBuilder] must be null. If this is null, the [itemExtentBuilder] must be non-null.

### itemExtentBuilder

```dart
ItemExtentBuilder? get itemExtentBuilder
```

The main-axis extent builder of each item.

If this is non-null, the [itemExtent] must be null. If this is null, the [itemExtent] must be non-null.

### indexToLayoutOffset()

```dart
double indexToLayoutOffset(double itemExtent, int index)
```

The layout offset for the child with the given index.

This function uses the returned value of [itemExtentBuilder] or the [itemExtent] to avoid recomputing item size repeatedly during layout.

By default, places the children in order, without gaps, starting from layout offset zero.

### getMinChildIndexForScrollOffset()

```dart
int getMinChildIndexForScrollOffset(double scrollOffset, double itemExtent)
```

The minimum child index that is visible at the given scroll offset.

This function uses the returned value of [itemExtentBuilder] or the [itemExtent] to avoid recomputing item size repeatedly during layout.

By default, returns a value consistent with the children being placed in order, without gaps, starting from layout offset zero.

### getMaxChildIndexForScrollOffset()

```dart
int getMaxChildIndexForScrollOffset(double scrollOffset, double itemExtent)
```

The maximum child index that is visible at the given scroll offset.

This function uses the returned value of [itemExtentBuilder] or the [itemExtent] to avoid recomputing item size repeatedly during layout.

By default, returns a value consistent with the children being placed in order, without gaps, starting from layout offset zero.

### estimateMaxScrollOffset()

```dart
double estimateMaxScrollOffset(SliverConstraints constraints, {int? firstIndex, int? lastIndex, double? leadingScrollOffset, double? trailingScrollOffset})
```

Called to estimate the total scrollable extents of this object.

Must return the total distance from the start of the child with the earliest possible index to the end of the child with the last possible index.

By default, defers to [RenderSliverBoxChildManager.estimateMaxScrollOffset].

See also:

- [computeMaxScrollOffset], which is similar but must provide a precise value.

### computeMaxScrollOffset()

```dart
double computeMaxScrollOffset(SliverConstraints constraints, double itemExtent)
```

Called to obtain a precise measure of the total scrollable extents of this object.

Must return the precise total distance from the start of the child with the earliest possible index to the end of the child with the last possible index.

This is used when no child is available for the index corresponding to the current scroll offset, to determine the precise dimensions of the sliver. It must return a precise value. It will not be called if the [childManager] returns an infinite number of children for positive indices.

If [itemExtentBuilder] is null, multiplies the [itemExtent] by the number of children reported by [RenderSliverBoxChildManager.childCount]. If [itemExtentBuilder] is non-null, sum the extents of the first [RenderSliverBoxChildManager.childCount] children.

See also:

- [estimateMaxScrollOffset], which is similar but may provide inaccurate values.

### layoutDimensions

```dart
SliverLayoutDimensions get layoutDimensions
```

The layout dimensions for the sliver.

If the sliver has not been laid out yet, this returns a [SliverLayoutDimensions] based on the current [constraints].

### paintExtentOf()

```dart
double paintExtentOf(RenderBox child)
```

### debugAssertDoesMeetConstraints()

```dart
void debugAssertDoesMeetConstraints()
```

### performLayout()

```dart
void performLayout()
```

# RenderSliverFixedExtentList

```dart
class RenderSliverFixedExtentList extends RenderSliverFixedExtentBoxAdaptor {}
```

A sliver that places multiple box children with the same main axis extent in a linear array.

[RenderSliverFixedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the [itemExtent] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

[RenderSliverFixedExtentList] is more efficient than [RenderSliverList] because [RenderSliverFixedExtentList] does not need to perform layout on its children to obtain their extent in the main axis.

See also:

- [RenderSliverList], which does not require its children to have the same extent in the main axis.
- [RenderSliverFillViewport], which determines the [itemExtent] based on [SliverConstraints.viewportMainAxisExtent].
- [RenderSliverFillRemaining], which determines the [itemExtent] based on [SliverConstraints.remainingPaintExtent].

### RenderSliverFixedExtentList()

```dart
RenderSliverFixedExtentList({required RenderSliverBoxChildManager childManager, required double itemExtent})
```

Creates a sliver that contains multiple box children that have a given extent in the main axis.

### itemExtent

```dart
double get itemExtent
```

### itemExtent

```dart
set itemExtent(double value)
```

# RenderSliverVariedExtentList

```dart
class RenderSliverVariedExtentList extends RenderSliverFixedExtentBoxAdaptor {}
```

A sliver that places multiple box children with the corresponding main axis extent in a linear array.

### RenderSliverVariedExtentList()

```dart
RenderSliverVariedExtentList({required RenderSliverBoxChildManager childManager, required ItemExtentBuilder itemExtentBuilder})
```

Creates a sliver that contains multiple box children that have a explicit extent in the main axis.

### itemExtentBuilder

```dart
ItemExtentBuilder get itemExtentBuilder
```

### itemExtentBuilder

```dart
set itemExtentBuilder(ItemExtentBuilder value)
```

### itemExtent

```dart
double? get itemExtent
```
