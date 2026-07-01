@docImport 'package:flutter/material.dart';

@docImport 'animated_scroll_view.dart'; @docImport 'container.dart'; @docImport 'implicit_animations.dart'; @docImport 'indexed_stack.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver_fill.dart'; @docImport 'sliver_persistent_header.dart'; @docImport 'sliver_prototype_extent_list.dart'; @docImport 'text.dart'; @docImport 'two_dimensional_viewport.dart'; @docImport 'viewport.dart';

# SliverWithKeepAliveWidget

```dart
abstract class SliverWithKeepAliveWidget extends RenderObjectWidget {}
```

A base class for slivers that have [KeepAlive] children.

See also:

- [KeepAlive], which marks whether its child widget should be kept alive.
- [SliverChildBuilderDelegate] and [SliverChildListDelegate], slivers which make use of the keep alive functionality through the `addAutomaticKeepAlives` property.
- [SliverGrid] and [SliverList], two sliver widgets that are commonly wrapped with [KeepAlive] widgets to preserve their sliver child subtrees.

### SliverWithKeepAliveWidget()

```dart
SliverWithKeepAliveWidget({dynamic key})
```

Initializes fields for subclasses.

### createRenderObject()

```dart
RenderSliverWithKeepAliveMixin createRenderObject(BuildContext context)
```

# SliverMultiBoxAdaptorWidget

```dart
abstract class SliverMultiBoxAdaptorWidget extends SliverWithKeepAliveWidget {}
```

A base class for slivers that have multiple box children.

Helps subclasses build their children lazily using a [SliverChildDelegate].

The widgets returned by the [delegate] are cached and the delegate is only consulted again if it changes and the new delegate's [SliverChildDelegate.shouldRebuild] method returns true.

### SliverMultiBoxAdaptorWidget()

```dart
SliverMultiBoxAdaptorWidget({dynamic key, required SliverChildDelegate delegate})
```

Initializes fields for subclasses.

### delegate

```dart
SliverChildDelegate delegate
```

{@template flutter.widgets.SliverMultiBoxAdaptorWidget.delegate} The delegate that provides the children for this widget.

The children are constructed lazily using this delegate to avoid creating more children than are visible through the [Viewport].

## Using more than one delegate in a [Viewport]

If multiple delegates are used in a single scroll view, the first child of each delegate will always be laid out, even if it extends beyond the currently viewable area. This is because at least one child is required in order to estimate the max scroll offset for the whole scroll view, as it uses the currently built children to estimate the remaining children's extent.

See also:

- [SliverChildBuilderDelegate] and [SliverChildListDelegate], which are commonly used subclasses of [SliverChildDelegate] that use a builder callback and an explicit child list, respectively. {@endtemplate}

### createElement()

```dart
SliverMultiBoxAdaptorElement createElement()
```

### createRenderObject()

```dart
RenderSliverMultiBoxAdaptor createRenderObject(BuildContext context)
```

### estimateMaxScrollOffset()

```dart
double? estimateMaxScrollOffset(SliverConstraints? constraints, int firstIndex, int lastIndex, double leadingScrollOffset, double trailingScrollOffset)
```

Returns an estimate of the max scroll extent for all the children.

Subclasses should override this function if they have additional information about their max scroll extent.

This is used by [SliverMultiBoxAdaptorElement] to implement part of the [RenderSliverBoxChildManager] API.

The default implementation defers to [delegate] via its [SliverChildDelegate.estimateMaxScrollOffset] method.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverList

```dart
class SliverList extends SliverMultiBoxAdaptorWidget {}
```

A sliver that places multiple box children in a linear array along the main axis.

_To learn more about slivers, see [CustomScrollView.slivers]._

Each child is forced to have the [SliverConstraints.crossAxisExtent] in the cross axis but determines its own main axis extent.

[SliverList] determines its scroll offset by "dead reckoning" because children outside the visible part of the sliver are not materialized, which means [SliverList] cannot learn their main axis extent. Instead, newly materialized children are placed adjacent to existing children.

{@youtube 560 315 https://www.youtube.com/watch?v=ORiTTaVY6mM}

If the children have a fixed extent in the main axis, consider using [SliverFixedExtentList] rather than [SliverList] because [SliverFixedExtentList] does not need to perform layout on its children to obtain their extent in the main axis and is therefore more efficient.

{@macro flutter.widgets.SliverChildDelegate.lifecycle}

{@tool dartpad}

This example shows a [SliverList] with a dynamic number of items.

** See code in examples/api/lib/widgets/sliver/sliver_list.0.dart ** {@end-tool}

See also:

- <https://docs.flutter.dev/ui/layout/scrolling/slivers>, a description of what slivers are and how to use them.
- [CustomScrollView], which accepts slivers like [SliverList] to create custom scroll effects.
- [SliverFixedExtentList], which is more efficient for children with the same extent in the main axis.
- [SliverPrototypeExtentList], which is similar to [SliverFixedExtentList] except that it uses a prototype list item instead of a pixel value to define the main axis extent of each item.
- [SliverAnimatedList], which animates items added to or removed from a list.
- [SliverGrid], which places multiple children in a two dimensional grid.
- [SliverAnimatedGrid], a sliver which animates items when they are inserted into or removed from a grid.

### SliverList()

```dart
SliverList({dynamic key, required SliverChildDelegate delegate})
```

Creates a sliver that places box children in a linear array.

### SliverList.builder()

```dart
SliverList.builder({dynamic key, required NullableIndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, int? itemCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, int semanticIndexOffset = 0})
```

A sliver that places multiple box children in a linear array along the main axis.

This constructor is appropriate for sliver lists with a large (or infinite) number of children because the builder is called only for those children that are actually visible.

Providing a non-null `itemCount` improves the ability of the [SliverList] to estimate the maximum scroll extent.

`itemBuilder` will be called only with indices greater than or equal to zero and less than `itemCount`.

{@macro flutter.widgets.ListView.builder.itemBuilder}

{@macro flutter.widgets.PageView.findChildIndexCallback}

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property.

{@tool snippet} This example, which would be provided in [CustomScrollView.slivers], shows an infinite number of items in varying shades of blue:

```dart
SliverList.builder(
  itemBuilder: (BuildContext context, int index) {
    return Container(
      alignment: Alignment.center,
      color: Colors.lightBlue[100 * (index % 9)],
      child: Text('list item $index'),
    );
  },
)
```

{@end-tool}

### SliverList.separated()

```dart
SliverList.separated({dynamic key, required NullableIndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, ChildIndexGetter? findItemIndexCallback, required NullableIndexedWidgetBuilder separatorBuilder, int? itemCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true})
```

A sliver that places multiple box children, separated by box widgets, in a linear array along the main axis.

This constructor is appropriate for sliver lists with a large (or infinite) number of children because the builder is called only for those children that are actually visible.

Providing a non-null `itemCount` improves the ability of the [SliverList] to estimate the maximum scroll extent.

`itemBuilder` will be called only with indices greater than or equal to zero and less than `itemCount`.

{@macro flutter.widgets.ListView.builder.itemBuilder}

{@macro flutter.widgets.PageView.findChildIndexCallback}

{@macro flutter.widgets.ListView.separated.findItemIndexCallback}

The `separatorBuilder` is similar to `itemBuilder`, except it is the widget that gets placed between itemBuilder(context, index) and itemBuilder(context, index + 1).

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property.

{@tool snippet} This example shows how to create a [SliverList] whose [Container] items are separated by [Divider]s. The [SliverList] would be provided in [CustomScrollView.slivers].

```dart
SliverList.separated(
  itemBuilder: (BuildContext context, int index) {
    return Container(
      alignment: Alignment.center,
      color: Colors.lightBlue[100 * (index % 9)],
      child: Text('list item $index'),
    );
  },
  separatorBuilder: (BuildContext context, int index) {
    return const SizedBox(
      height: 1.0,
      width: double.infinity,
      child: ColoredBox(color: Color(0xFF000000)),
    );
  },
)
```

{@end-tool}

### SliverList.list()

```dart
SliverList.list({dynamic key, required List<Widget> children, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true})
```

A sliver that places multiple box children in a linear array along the main axis.

This constructor uses a list of [Widget]s to build the sliver.

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property.

{@tool snippet} This example, which would be provided in [CustomScrollView.slivers], shows a list containing two [Text] widgets:

```dart
SliverList.list(
  children: const <Widget>[
    Text('Hello'),
    Text('World!'),
  ],
);
```

{@end-tool}

### createElement()

```dart
SliverMultiBoxAdaptorElement createElement()
```

### createRenderObject()

```dart
RenderSliverList createRenderObject(BuildContext context)
```

# SliverFixedExtentList

```dart
class SliverFixedExtentList extends SliverMultiBoxAdaptorWidget {}
```

A sliver that places multiple box children with the same main axis extent in a linear array.

_To learn more about slivers, see [CustomScrollView.slivers]._

[SliverFixedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the [itemExtent] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

[SliverFixedExtentList] is more efficient than [SliverList] because [SliverFixedExtentList] does not need to perform layout on its children to obtain their extent in the main axis.

{@tool snippet}

This example, which would be inserted into a [CustomScrollView.slivers] list, shows an infinite number of items in varying shades of blue:

```dart
SliverFixedExtentList(
  itemExtent: 50.0,
  delegate: SliverChildBuilderDelegate(
    (BuildContext context, int index) {
      return Container(
        alignment: Alignment.center,
        color: Colors.lightBlue[100 * (index % 9)],
        child: Text('list item $index'),
      );
    },
  ),
)
```

{@end-tool}

{@macro flutter.widgets.SliverChildDelegate.lifecycle}

See also:

- [SliverPrototypeExtentList], which is similar to [SliverFixedExtentList] except that it uses a prototype list item instead of a pixel value to define the main axis extent of each item.
- [SliverVariedExtentList], which supports children with varying (but known upfront) extents.
- [SliverFillViewport], which determines the [itemExtent] based on [SliverConstraints.viewportMainAxisExtent].
- [SliverList], which does not require its children to have the same extent in the main axis.

### SliverFixedExtentList()

```dart
SliverFixedExtentList({dynamic key, required SliverChildDelegate delegate, required double itemExtent})
```

Creates a sliver that places box children with the same main axis extent in a linear array.

### SliverFixedExtentList.builder()

```dart
SliverFixedExtentList.builder({dynamic key, required NullableIndexedWidgetBuilder itemBuilder, required double itemExtent, ChildIndexGetter? findChildIndexCallback, int? itemCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, int semanticIndexOffset = 0})
```

A sliver that places multiple box children in a linear array along the main axis.

[SliverFixedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the [itemExtent] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

This constructor is appropriate for sliver lists with a large (or infinite) number of children whose extent is already determined.

Providing a non-null `itemCount` improves the ability of the [SliverFixedExtentList] to estimate the maximum scroll extent.

`itemBuilder` will be called only with indices greater than or equal to zero and less than `itemCount`.

{@macro flutter.widgets.ListView.builder.itemBuilder}

The `itemExtent` argument is the extent of each item.

{@macro flutter.widgets.PageView.findChildIndexCallback}

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property. {@tool snippet}

This example, which would be inserted into a [CustomScrollView.slivers] list, shows an infinite number of items in varying shades of blue:

```dart
SliverFixedExtentList.builder(
  itemExtent: 50.0,
  itemBuilder: (BuildContext context, int index) {
    return Container(
      alignment: Alignment.center,
      color: Colors.lightBlue[100 * (index % 9)],
      child: Text('list item $index'),
    );
  },
)
```

{@end-tool}

### SliverFixedExtentList.list()

```dart
SliverFixedExtentList.list({dynamic key, required List<Widget> children, required double itemExtent, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true})
```

A sliver that places multiple box children in a linear array along the main axis.

[SliverFixedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the [itemExtent] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

This constructor uses a list of [Widget]s to build the sliver.

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property.

{@tool snippet} This example, which would be inserted into a [CustomScrollView.slivers] list, shows an infinite number of items in varying shades of blue:

```dart
SliverFixedExtentList.list(
  itemExtent: 50.0,
  children: const <Widget>[
    Text('Hello'),
    Text('World!'),
  ],
);
```

{@end-tool}

### itemExtent

```dart
double itemExtent
```

The extent the children are forced to have in the main axis.

### createRenderObject()

```dart
RenderSliverFixedExtentList createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverFixedExtentList renderObject)
```

# SliverVariedExtentList

```dart
class SliverVariedExtentList extends SliverMultiBoxAdaptorWidget {}
```

A sliver that places its box children in a linear array and constrains them to have the corresponding extent returned by [itemExtentBuilder].

_To learn more about slivers, see [CustomScrollView.slivers]._

[SliverVariedExtentList] arranges its children in a line along the main axis starting at offset zero and without gaps. Each child is constrained to the corresponding extent along the main axis and the [SliverConstraints.crossAxisExtent] along the cross axis.

[SliverVariedExtentList] is more efficient than [SliverList] because [SliverVariedExtentList] does not need to lay out its children to obtain their extent along the main axis. It's a little more flexible than [SliverFixedExtentList] because this allow the children to have different extents.

See also:

- [SliverFixedExtentList], whose children are forced to a given pixel extent.
- [SliverPrototypeExtentList], which is similar to [SliverFixedExtentList] except that it uses a prototype list item instead of a pixel value to define the main axis extent of each item.
- [SliverList], which does not require its children to have the same extent in the main axis.
- [SliverFillViewport], which sizes its children based on the size of the viewport, regardless of what else is in the scroll view.

### SliverVariedExtentList()

```dart
SliverVariedExtentList({dynamic key, required SliverChildDelegate delegate, required ItemExtentBuilder itemExtentBuilder})
```

Creates a sliver that places box children with the same main axis extent in a linear array.

### SliverVariedExtentList.builder()

```dart
SliverVariedExtentList.builder({dynamic key, required NullableIndexedWidgetBuilder itemBuilder, required ItemExtentBuilder itemExtentBuilder, ChildIndexGetter? findChildIndexCallback, int? itemCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true})
```

A sliver that places multiple box children in a linear array along the main axis.

[SliverVariedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the returned extent of [itemExtentBuilder] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

This constructor is appropriate for sliver lists with a large (or infinite) number of children whose extent is already determined.

Providing a non-null `itemCount` improves the ability of the [SliverVariedExtentList] to estimate the maximum scroll extent.

### SliverVariedExtentList.list()

```dart
SliverVariedExtentList.list({dynamic key, required List<Widget> children, required ItemExtentBuilder itemExtentBuilder, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true})
```

A sliver that places multiple box children in a linear array along the main axis.

[SliverVariedExtentList] places its children in a linear array along the main axis starting at offset zero and without gaps. Each child is forced to have the returned extent of [itemExtentBuilder] in the main axis and the [SliverConstraints.crossAxisExtent] in the cross axis.

This constructor uses a list of [Widget]s to build the sliver.

### itemExtentBuilder

```dart
ItemExtentBuilder itemExtentBuilder
```

The children extent builder.

Should return null if asked to build an item extent with a greater index than exists.

### createRenderObject()

```dart
RenderSliverVariedExtentList createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverVariedExtentList renderObject)
```

# SliverGrid

```dart
class SliverGrid extends SliverMultiBoxAdaptorWidget {}
```

A sliver that places multiple box children in a two dimensional arrangement.

_To learn more about slivers, see [CustomScrollView.slivers]._

[SliverGrid] places its children in arbitrary positions determined by [gridDelegate]. Each child is forced to have the size specified by the [gridDelegate].

The main axis direction of a grid is the direction in which it scrolls; the cross axis direction is the orthogonal direction.

{@youtube 560 315 https://www.youtube.com/watch?v=ORiTTaVY6mM}

{@tool snippet}

This example, which would be inserted into a [CustomScrollView.slivers] list, shows twenty boxes in a pretty teal grid:

```dart
SliverGrid.builder(
  gridDelegate: const SliverGridDelegateWithMaxCrossAxisExtent(
    maxCrossAxisExtent: 200.0,
    mainAxisSpacing: 10.0,
    crossAxisSpacing: 10.0,
    childAspectRatio: 4.0,
  ),
  itemCount: 20,
  itemBuilder: (BuildContext context, int index) {
    return Container(
      alignment: Alignment.center,
      color: Colors.teal[100 * (index % 9)],
      child: Text('grid item $index'),
    );
  },
)
```

{@end-tool}

{@macro flutter.widgets.SliverChildDelegate.lifecycle}

See also:

- [SliverList], which places its children in a linear array.
- [SliverFixedExtentList], which places its children in a linear array with a fixed extent in the main axis.
- [SliverPrototypeExtentList], which is similar to [SliverFixedExtentList] except that it uses a prototype list item instead of a pixel value to define the main axis extent of each item.

### SliverGrid()

```dart
SliverGrid({dynamic key, required SliverChildDelegate delegate, required SliverGridDelegate gridDelegate})
```

Creates a sliver that places multiple box children in a two dimensional arrangement.

### SliverGrid.builder()

```dart
SliverGrid.builder({dynamic key, required SliverGridDelegate gridDelegate, required NullableIndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, int? itemCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, int semanticIndexOffset = 0})
```

A sliver that creates a 2D array of widgets that are created on demand.

This constructor is appropriate for sliver grids with a large (or infinite) number of children because the builder is called only for those children that are actually visible.

Providing a non-null `itemCount` improves the ability of the [SliverGrid] to estimate the maximum scroll extent.

`itemBuilder` will be called only with indices greater than or equal to zero and less than `itemCount`.

{@macro flutter.widgets.ListView.builder.itemBuilder}

{@macro flutter.widgets.PageView.findChildIndexCallback}

The [gridDelegate] argument is required.

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildBuilderDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildBuilderDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildBuilderDelegate.addSemanticIndexes] property.

### SliverGrid.count()

```dart
SliverGrid.count({dynamic key, required int crossAxisCount, double mainAxisSpacing = 0.0, double crossAxisSpacing = 0.0, double childAspectRatio = 1.0, List<Widget> children = const <Widget>[]})
```

Creates a sliver that places multiple box children in a two dimensional arrangement with a fixed number of tiles in the cross axis.

Uses a [SliverGridDelegateWithFixedCrossAxisCount] as the [gridDelegate], and a [SliverChildListDelegate] as the [delegate].

See also:

- [GridView.count], the equivalent constructor for [GridView] widgets.

### SliverGrid.extent()

```dart
SliverGrid.extent({dynamic key, required double maxCrossAxisExtent, double mainAxisSpacing = 0.0, double crossAxisSpacing = 0.0, double childAspectRatio = 1.0, List<Widget> children = const <Widget>[]})
```

Creates a sliver that places multiple box children in a two dimensional arrangement with tiles that each have a maximum cross-axis extent.

Uses a [SliverGridDelegateWithMaxCrossAxisExtent] as the [gridDelegate], and a [SliverChildListDelegate] as the [delegate].

See also:

- [GridView.extent], the equivalent constructor for [GridView] widgets.

### SliverGrid.list()

```dart
SliverGrid.list({dynamic key, required SliverGridDelegate gridDelegate, required List<Widget> children, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, int semanticIndexOffset = 0})
```

Creates a sliver that places multiple box children in a two dimensional arrangement.

_To learn more about slivers, see [CustomScrollView.slivers]._

Uses a [SliverChildListDelegate] as the [delegate].

The `addAutomaticKeepAlives` argument corresponds to the [SliverChildListDelegate.addAutomaticKeepAlives] property. The `addRepaintBoundaries` argument corresponds to the [SliverChildListDelegate.addRepaintBoundaries] property. The `addSemanticIndexes` argument corresponds to the [SliverChildListDelegate.addSemanticIndexes] property. The `semanticIndexOffset` argument corresponds to the [SliverChildListDelegate.semanticIndexOffset] property.

{@tool snippet} This example, which would be inserted into a [CustomScrollView.slivers] list, shows a grid of [Container] widgets.

```dart
SliverGrid.list(
  gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 3,
  ),
  children: <Widget>[
    Container(color: Colors.red),
    Container(color: Colors.green),
    Container(color: Colors.blue),
    Container(color: Colors.yellow),
    Container(color: Colors.orange),
    Container(color: Colors.purple),
  ],
);
```

{@end-tool}

### gridDelegate

```dart
SliverGridDelegate gridDelegate
```

The delegate that controls the size and position of the children.

### createRenderObject()

```dart
RenderSliverGrid createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverGrid renderObject)
```

### estimateMaxScrollOffset()

```dart
double estimateMaxScrollOffset(SliverConstraints? constraints, int firstIndex, int lastIndex, double leadingScrollOffset, double trailingScrollOffset)
```

# SliverMultiBoxAdaptorElement

```dart
class SliverMultiBoxAdaptorElement extends RenderObjectElement implements RenderSliverBoxChildManager {}
```

An element that lazily builds children for a [SliverMultiBoxAdaptorWidget].

Implements [RenderSliverBoxChildManager], which lets this element manage the children of subclasses of [RenderSliverMultiBoxAdaptor].

### SliverMultiBoxAdaptorElement()

```dart
SliverMultiBoxAdaptorElement(SliverMultiBoxAdaptorWidget widget, {bool replaceMovedChildren = false})
```

Creates an element that lazily builds children for the given widget.

If `replaceMovedChildren` is set to true, a new child is proactively inflate for the index that was previously occupied by a child that moved to a new index. The layout offset of the moved child is copied over to the new child. RenderObjects, that depend on the layout offset of existing children during [RenderObject.performLayout] should set this to true (example: [RenderSliverList]). For RenderObjects that figure out the layout offset of their children without looking at the layout offset of existing children this should be set to false (example: [RenderSliverFixedExtentList]) to avoid inflating unnecessary children.

### renderObject

```dart
RenderSliverMultiBoxAdaptor get renderObject
```

### update()

```dart
void update(SliverMultiBoxAdaptorWidget newWidget)
```

### performRebuild()

```dart
void performRebuild()
```

### createChild()

```dart
void createChild(int index, {required RenderBox? after})
```

### updateChild()

```dart
Element? updateChild(Element? child, Widget? newWidget, Object? newSlot)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### removeChild()

```dart
void removeChild(RenderBox child)
```

### estimateMaxScrollOffset()

```dart
double estimateMaxScrollOffset(SliverConstraints? constraints, {int? firstIndex, int? lastIndex, double? leadingScrollOffset, double? trailingScrollOffset})
```

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### childCount

```dart
int get childCount
```

### didStartLayout()

```dart
void didStartLayout()
```

### didFinishLayout()

```dart
void didFinishLayout()
```

### debugAssertChildListLocked()

```dart
bool debugAssertChildListLocked()
```

### didAdoptChild()

```dart
void didAdoptChild(RenderBox child)
```

### setDidUnderflow()

```dart
void setDidUnderflow(bool value)
```

### insertRenderObjectChild()

```dart
void insertRenderObjectChild(RenderObject child, int slot)
```

### moveRenderObjectChild()

```dart
void moveRenderObjectChild(RenderObject child, int oldSlot, int newSlot)
```

### removeRenderObjectChild()

```dart
void removeRenderObjectChild(RenderObject child, int slot)
```

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### debugVisitOnstageChildren()

```dart
void debugVisitOnstageChildren(ElementVisitor visitor)
```

# SliverOpacity

```dart
class SliverOpacity extends SingleChildRenderObjectWidget {}
```

A sliver widget that makes its sliver child partially transparent.

This class paints its sliver child into an intermediate buffer and then blends the sliver back into the scene partially transparent.

For values of opacity other than 0.0 and 1.0, this class is relatively expensive because it requires painting the sliver child into an intermediate buffer. For the value 0.0, the sliver child is not painted at all. For the value 1.0, the sliver child is painted immediately without an intermediate buffer.

{@tool dartpad}

This example shows a [SliverList] when the `_visible` member field is true, and hides it when it is false.

This is more efficient than adding and removing the sliver child widget from the tree on demand, but it does not affect how much the list scrolls (the [SliverList] is still present, merely invisible).

** See code in examples/api/lib/widgets/sliver/sliver_opacity.1.dart ** {@end-tool}

See also:

- [Opacity], which can apply a uniform alpha effect to its child using the [RenderBox] layout protocol.
- [AnimatedOpacity], which uses an animation internally to efficiently animate [Opacity].
- [SliverVisibility], which can hide a child more efficiently (albeit less subtly, because it is either visible or hidden, rather than allowing fractional opacity values). Specifically, the [SliverVisibility.maintain] constructor is equivalent to using a sliver opacity widget with values of `0.0` or `1.0`.

### SliverOpacity()

```dart
SliverOpacity({dynamic key, required double opacity, bool alwaysIncludeSemantics = false, Widget? sliver})
```

Creates a sliver that makes its sliver child partially transparent.

The [opacity] argument must be between zero and one, inclusive.

### opacity

```dart
double opacity
```

The fraction to scale the sliver child's alpha value.

An opacity of 1.0 is fully opaque. An opacity of 0.0 is fully transparent (i.e. invisible).

Values 1.0 and 0.0 are painted with a fast path. Other values require painting the sliver child into an intermediate buffer, which is expensive.

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

Whether the semantic information of the sliver child is always included.

Defaults to false.

When true, regardless of the opacity settings, the sliver child semantic information is exposed as if the widget were fully visible. This is useful in cases where labels may be hidden during animations that would otherwise contribute relevant semantics.

### createRenderObject()

```dart
RenderSliverOpacity createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOpacity renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverIgnorePointer

```dart
class SliverIgnorePointer extends SingleChildRenderObjectWidget {}
```

A sliver widget that is invisible during hit testing.

When [ignoring] is true, this widget (and its subtree) is invisible to hit testing. It still consumes space during layout and paints its sliver child as usual. It just cannot be the target of located events, because it returns false from [RenderSliver.hitTest].

## Semantics

Using this class may also affect how the semantics subtree underneath is collected.

{@macro flutter.widgets.IgnorePointer.semantics}

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

See also:

- [IgnorePointer], the equivalent widget for boxes.

### SliverIgnorePointer()

```dart
SliverIgnorePointer({dynamic key, bool ignoring = true, bool? ignoringSemantics, Widget? sliver})
```

Creates a sliver widget that is invisible to hit testing.

### ignoring

```dart
bool ignoring
```

Whether this sliver is ignored during hit testing.

Regardless of whether this sliver is ignored during hit testing, it will still consume space during layout and be visible during painting.

{@macro flutter.widgets.IgnorePointer.semantics}

### ignoringSemantics

```dart
bool? ignoringSemantics
```

Whether the semantics of this sliver is ignored when compiling the semantics tree.

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

### createRenderObject()

```dart
RenderSliverIgnorePointer createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverIgnorePointer renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverOffstage

```dart
class SliverOffstage extends SingleChildRenderObjectWidget {}
```

A sliver that lays its sliver child out as if it was in the tree, but without painting anything, without making the sliver child available for hit testing, and without taking any room in the parent.

Animations continue to run in offstage sliver children, and therefore use battery and CPU time, regardless of whether the animations end up being visible.

To hide a sliver widget from view while it is not needed, prefer removing the widget from the tree entirely rather than keeping it alive in an [Offstage] subtree.

See also:

- [Offstage], the equivalent widget for boxes.

### SliverOffstage()

```dart
SliverOffstage({dynamic key, bool offstage = true, Widget? sliver})
```

Creates a sliver that visually hides its sliver child.

### offstage

```dart
bool offstage
```

Whether the sliver child is hidden from the rest of the tree.

If true, the sliver child is laid out as if it was in the tree, but without painting anything, without making the child available for hit testing, and without taking any room in the parent.

If false, the sliver child is included in the tree as normal.

### createRenderObject()

```dart
RenderSliverOffstage createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOffstage renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createElement()

```dart
SingleChildRenderObjectElement createElement()
```

# KeepAlive

```dart
class KeepAlive extends ParentDataWidget<KeepAliveParentDataMixin> {}
```

Mark a child as needing to stay alive even when it's in a lazy list that would otherwise remove it.

This widget is used in [RenderAbstractViewport]s, such as [Viewport] or [TwoDimensionalViewport], to manage the lifecycle of widgets that need to remain alive even when scrolled out of view.

The [SliverChildBuilderDelegate] and [SliverChildListDelegate] delegates, used with [SliverList] and [SliverGrid], as well as the scroll view counterparts [ListView] and [GridView], have an `addAutomaticKeepAlives` feature, which is enabled by default. This feature inserts [AutomaticKeepAlive] widgets around each child, which in turn configure [KeepAlive] widgets in response to [KeepAliveNotification]s.

The same `addAutomaticKeepAlives` feature is supported by [TwoDimensionalChildBuilderDelegate] and [TwoDimensionalChildListDelegate].

Keep-alive behavior can be managed by using [KeepAlive] directly or by relying on notifications. For convenience, [AutomaticKeepAliveClientMixin] may be mixed into a [State] subclass. Further details are available in the documentation for [AutomaticKeepAliveClientMixin].

{@tool dartpad} This sample demonstrates how to use the [KeepAlive] widget to preserve the state of individual list items in a [ListView] when they are scrolled out of view.

By default, [ListView.builder] only keeps the widgets currently visible in the viewport alive. When an item scrolls out of view, it may be disposed to free up resources. This can cause the state of [StatefulWidget]s to be lost if not explicitly preserved.

In this example, each item in the list is a [StatefulWidget] that maintains a counter. Tapping the "+" button increments the counter. To selectively preserve the state, each item is wrapped in a [KeepAlive] widget, with the keepAlive parameter set based on the item’s index:

- For even-indexed items, `keepAlive: true`, so their state is preserved even when scrolled off-screen.
- For odd-indexed items, `keepAlive: false`, so their state is discarded when they are no longer visible.

** See code in examples/api/lib/widgets/keep_alive/keep_alive.0.dart ** {@end-tool}

See also:

- [AutomaticKeepAlive], which allows subtrees to request to be kept alive in lazy lists.
- [AutomaticKeepAliveClientMixin], which is a mixin with convenience methods for clients of [AutomaticKeepAlive]. Used with [State] subclasses.

### KeepAlive()

```dart
KeepAlive({dynamic key, required bool keepAlive, required Widget child})
```

Marks a child as needing to remain alive.

### keepAlive

```dart
bool keepAlive
```

Whether to keep the child alive.

If this is false, it is as if this widget was omitted.

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

### debugCanApplyOutOfTurn()

```dart
bool debugCanApplyOutOfTurn()
```

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

### debugTypicalAncestorWidgetDescription

```dart
String get debugTypicalAncestorWidgetDescription
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverConstrainedCrossAxis

```dart
class SliverConstrainedCrossAxis extends StatelessWidget {}
```

A sliver that constrains the cross axis extent of its sliver child.

The [SliverConstrainedCrossAxis] takes a [maxExtent] parameter and uses it as the cross axis extent of the [SliverConstraints] passed to the sliver child. The widget ensures that the [maxExtent] is a nonnegative value.

This is useful when you want to apply a custom cross-axis extent constraint to a sliver child, as slivers typically consume the full cross axis extent.

This widget also sets its parent data's [SliverPhysicalParentData.crossAxisFlex] to 0, so that it informs [SliverCrossAxisGroup] that it should not flex in the cross axis direction.

{@tool dartpad} In this sample the [SliverConstrainedCrossAxis] sizes its child so that the cross axis extent takes up less space than the actual viewport.

** See code in examples/api/lib/widgets/sliver/sliver_constrained_cross_axis.0.dart ** {@end-tool}

See also:

- [SliverCrossAxisGroup], the widget which makes use of 0 flex factor set by this widget.

### SliverConstrainedCrossAxis()

```dart
SliverConstrainedCrossAxis({dynamic key, required double maxExtent, required Widget sliver})
```

Creates a sliver that constrains the cross axis extent of its sliver child.

The [maxExtent] parameter is required and must be nonnegative.

### maxExtent

```dart
double maxExtent
```

The cross axis extent to apply to the sliver child.

This value must be nonnegative.

### sliver

```dart
Widget sliver
```

The widget below this widget in the tree.

Must be a sliver.

### build()

```dart
Widget build(BuildContext context)
```

# SliverCrossAxisExpanded

```dart
class SliverCrossAxisExpanded extends ParentDataWidget<SliverPhysicalContainerParentData> {}
```

Set a flex factor for allocating space in the cross axis direction.

This is a [ParentDataWidget] to be used in [SliverCrossAxisGroup]. After all slivers with null or zero flex (e.g. [SliverConstrainedCrossAxis]) are laid out (which should determine their own [SliverGeometry.crossAxisExtent]), the remaining space is laid out among the slivers with nonzero flex proportionally to their flex value.

### SliverCrossAxisExpanded()

```dart
SliverCrossAxisExpanded({dynamic key, required int flex, required Widget sliver})
```

Creates an object that assigns a [flex] value to the child sliver.

The provided [flex] value must be greater than 0.

### flex

```dart
int flex
```

Flex value for allocating cross axis extent left after laying out the children with constrained cross axis. The children with flex values will have the remaining extent allocated proportionally to their flex value. This must an integer between 0 and infinity, exclusive.

### applyParentData()

```dart
void applyParentData(RenderObject renderObject)
```

### debugTypicalAncestorWidgetClass

```dart
Type get debugTypicalAncestorWidgetClass
```

# SliverCrossAxisGroup

```dart
class SliverCrossAxisGroup extends MultiChildRenderObjectWidget {}
```

A sliver that places multiple sliver children in a linear array along the cross axis.

## Layout algorithm

_This section describes how the framework causes [RenderSliverCrossAxisGroup] to position its children._

Layout for a [RenderSliverCrossAxisGroup] has four steps:

1.  Layout each child with a null or zero flex factor with cross axis constraint being whatever cross axis space is remaining after laying out any previous sliver. Slivers with null or zero flex factor should determine their own [SliverGeometry.crossAxisExtent]. For example, the [SliverConstrainedCrossAxis] widget uses either [SliverConstrainedCrossAxis.maxExtent] or [SliverConstraints.crossAxisExtent], deciding between whichever is smaller.
2.  Divide up the remaining cross axis space among the children with non-zero flex factors according to their flex factor. For example, a child with a flex factor of 2.0 will receive twice the amount of cross axis space as a child with a flex factor 1.0.
3.  Layout each of the remaining children with the cross axis constraint allocated in the previous step.
4.  Set the geometry to that of whichever child has the longest [SliverGeometry.scrollExtent] with the [SliverGeometry.crossAxisExtent] adjusted to [SliverConstraints.crossAxisExtent].

{@tool dartpad} In this sample the [SliverCrossAxisGroup] sizes its three [children] so that the first normal [SliverList] has a flex factor of 1, the second [SliverConstrainedCrossAxis] has a flex factor of 0 and a maximum cross axis extent of 200.0, and the third [SliverCrossAxisExpanded] has a flex factor of 2.

** See code in examples/api/lib/widgets/sliver/sliver_cross_axis_group.0.dart ** {@end-tool}

See also:

- [SliverCrossAxisExpanded], which is the [ParentDataWidget] for setting a flex value to a widget.
- [SliverConstrainedCrossAxis], which is a [RenderObjectWidget] for setting an extent to constrain the widget to.
- [SliverMainAxisGroup], which is the [RenderObjectWidget] for laying out multiple slivers along the main axis.

### SliverCrossAxisGroup()

```dart
SliverCrossAxisGroup({dynamic key, required List<Widget> slivers})
```

Creates a sliver that places sliver children in a linear array along the cross axis.

### createRenderObject()

```dart
RenderSliverCrossAxisGroup createRenderObject(BuildContext context)
```

# SliverMainAxisGroup

```dart
class SliverMainAxisGroup extends MultiChildRenderObjectWidget {}
```

A sliver that places multiple sliver children in a linear array along the main axis, one after another.

## Layout algorithm

_This section describes how the framework causes [RenderSliverMainAxisGroup] to position its children._

Layout for a [RenderSliverMainAxisGroup] has four steps:

1.  Keep track of an offset variable which is the total [SliverGeometry.scrollExtent] of the slivers laid out so far.
2.  To determine the constraints for the next sliver child to layout, calculate the amount of paint extent occupied from 0.0 to the offset variable and subtract this from [SliverConstraints.remainingPaintExtent] minus to use as the child's [SliverConstraints.remainingPaintExtent]. For the [SliverConstraints.scrollOffset], take the provided constraint's value and subtract out the offset variable, using 0.0 if negative.
3.  Once we finish laying out all the slivers, this offset variable represents the total [SliverGeometry.scrollExtent] of the sliver group. Since it is possible for specialized slivers to try to paint itself outside of the bounds of the sliver group's scroll extent (see [SliverPersistentHeader]), we must do a second pass to set a [SliverPhysicalParentData.paintOffset] to make sure it is within the bounds of the sliver group.
4.  Finally, set the [RenderSliverMainAxisGroup.geometry] with the total [SliverGeometry.scrollExtent], [SliverGeometry.paintExtent] calculated from the constraints and [SliverGeometry.scrollExtent], and [SliverGeometry.maxPaintExtent].

{@tool dartpad} In this sample the [CustomScrollView] renders a [SliverMainAxisGroup] and a [SliverToBoxAdapter] with some content. The [SliverMainAxisGroup] renders a [SliverAppBar], [SliverList], and [SliverToBoxAdapter]. Notice that when the [SliverMainAxisGroup] goes out of view, so does the pinned [SliverAppBar].

** See code in examples/api/lib/widgets/sliver/sliver_main_axis_group.0.dart ** {@end-tool}

See also:

- [SliverPersistentHeader], which is a [RenderObjectWidget] which may require adjustment to its [SliverPhysicalParentData.paintOffset] to make it fit within the computed [SliverGeometry.scrollExtent] of the [SliverMainAxisGroup].
- [SliverCrossAxisGroup], which is the [RenderObjectWidget] for laying out multiple slivers along the cross axis.

### SliverMainAxisGroup()

```dart
SliverMainAxisGroup({dynamic key, required List<Widget> slivers})
```

Creates a sliver that places sliver children in a linear array along the main axis.

### createElement()

```dart
MultiChildRenderObjectElement createElement()
```

### createRenderObject()

```dart
RenderSliverMainAxisGroup createRenderObject(BuildContext context)
```

# SliverEnsureSemantics

```dart
class SliverEnsureSemantics extends SingleChildRenderObjectWidget {}
```

A sliver that ensures its sliver child is included in the semantics tree.

This sliver ensures that its child sliver is still visited by the [RenderViewport] when constructing the semantics tree, and is not clipped out of the semantics tree by the [RenderViewport] when it is outside the current viewport and outside the cache extent.

The child sliver may still be excluded from the semantics tree if its [RenderSliver] does not provide a valid [RenderSliver.semanticBounds]. This sliver does not guarantee its child sliver is laid out.

Be mindful when positioning [SliverEnsureSemantics] in a [CustomScrollView] after slivers that build their children lazily, like [SliverList]. Lazy slivers might underestimate the total scrollable size (scroll extent) before the [SliverEnsureSemantics] widget. This inaccuracy can cause problems for assistive technologies (e.g., screen readers), which rely on a correct scroll extent to navigate properly; they might fail to scroll accurately to the content wrapped by [SliverEnsureSemantics].

To avoid this potential issue and ensure the scroll extent is calculated accurately up to this sliver, it's recommended to use slivers that can determine their extent precisely beforehand. Instead of [SliverList], consider using [SliverFixedExtentList], [SliverVariedExtentList], or [SliverPrototypeExtentList]. If using [SliverGrid], ensure it employs a delegate such as [SliverGridDelegateWithFixedCrossAxisCount] or [SliverGridDelegateWithMaxCrossAxisExtent]. Using these alternatives guarantees that the scrollable area's size is known accurately, allowing assistive technologies to function correctly with [SliverEnsureSemantics].

{@tool dartpad} This example shows how to use [SliverEnsureSemantics] to keep certain headers and lists available to assistive technologies while they are outside the current viewport and cache extent.

** See code in examples/api/lib/widgets/sliver/sliver_ensure_semantics.0.dart ** {@end-tool}

### SliverEnsureSemantics()

```dart
SliverEnsureSemantics({dynamic key, required Widget sliver})
```

Creates a sliver that ensures its sliver child is included in the semantics tree.

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```
