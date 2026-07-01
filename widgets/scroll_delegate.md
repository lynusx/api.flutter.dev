@docImport 'scroll_view.dart'; @docImport 'sliver.dart'; @docImport 'spacer.dart'; @docImport 'two_dimensional_scroll_view.dart'; @docImport 'viewport.dart';

# SemanticIndexCallback

```dart
typedef SemanticIndexCallback = int? Function(Widget widget, int localIndex)
```

A callback which produces a semantic index given a widget and the local index.

Return a null value to prevent a widget from receiving an index.

A semantic index is used to tag child semantic nodes for accessibility announcements in scroll view.

See also:

- [CustomScrollView], for an explanation of scroll semantics.
- [SliverChildBuilderDelegate], for an explanation of how this is used to generate indexes.

# SliverChildDelegate

```dart
abstract class SliverChildDelegate {}
```

A delegate that supplies children for slivers.

Many slivers lazily construct their box children to avoid creating more children than are visible through the [Viewport]. Rather than receiving their children as an explicit [List], they receive their children using a [SliverChildDelegate].

It's uncommon to subclass [SliverChildDelegate]. Instead, consider using one of the existing subclasses that provide adaptors to builder callbacks or explicit child lists.

{@template flutter.widgets.SliverChildDelegate.lifecycle}

## Child elements' lifecycle

### Creation

While laying out the list, visible children's elements, states and render objects will be created lazily based on existing widgets (such as in the case of [SliverChildListDelegate]) or lazily provided ones (such as in the case of [SliverChildBuilderDelegate]).

### Destruction

When a child is scrolled out of view, the associated element subtree, states and render objects are destroyed. A new child at the same position in the sliver will be lazily recreated along with new elements, states and render objects when it is scrolled back.

### Destruction mitigation

In order to preserve state as child elements are scrolled in and out of view, the following options are possible:

- Moving the ownership of non-trivial UI-state-driving business logic out of the sliver child subtree. For instance, if a list contains posts with their number of upvotes coming from a cached network response, store the list of posts and upvote number in a data model outside the list. Let the sliver child UI subtree be easily recreate-able from the source-of-truth model object. Use [StatefulWidget]s in the child widget subtree to store instantaneous UI state only.

- Letting [KeepAlive] be the root widget of the sliver child widget subtree that needs to be preserved. The [KeepAlive] widget marks the child subtree's top render object child for keepalive. When the associated top render object is scrolled out of view, the sliver keeps the child's render object (and by extension, its associated elements and states) in a cache list instead of destroying them. When scrolled back into view, the render object is repainted as-is (if it wasn't marked dirty in the interim).

This only works if the [SliverChildDelegate] subclasses don't wrap the child widget subtree with other widgets such as [AutomaticKeepAlive] and [RepaintBoundary] via `addAutomaticKeepAlives` and `addRepaintBoundaries`.

- Using [AutomaticKeepAlive] widgets (inserted by default in [SliverChildListDelegate] or [SliverChildListDelegate]). [AutomaticKeepAlive] allows descendant widgets to control whether the subtree is actually kept alive or not. This behavior is in contrast with [KeepAlive], which will unconditionally keep the subtree alive.

As an example, the [EditableText] widget signals its sliver child element subtree to stay alive while its text field has input focus. If it doesn't have focus and no other descendants signaled for keepalive via a [KeepAliveNotification], the sliver child element subtree will be destroyed when scrolled away.

[AutomaticKeepAlive] descendants typically signal it to be kept alive by using the [AutomaticKeepAliveClientMixin], then implementing the [AutomaticKeepAliveClientMixin.wantKeepAlive] getter and calling [AutomaticKeepAliveClientMixin.updateKeepAlive].

## Using more than one delegate in a [Viewport]

If multiple delegates are used in a single scroll view, the first child of each delegate will always be laid out, even if it extends beyond the currently viewable area. This is because at least one child is required in order to [estimateMaxScrollOffset] for the whole scroll view, as it uses the currently built children to estimate the remaining children's extent. {@endtemplate}

See also:

- [SliverChildBuilderDelegate], which is a delegate that uses a builder callback to construct the children.
- [SliverChildListDelegate], which is a delegate that has an explicit list of children.

### SliverChildDelegate()

```dart
SliverChildDelegate()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### build()

```dart
Widget? build(BuildContext context, int index)
```

Returns the child with the given index.

Should return null if asked to build a widget with a greater index than exists. If this returns null, [estimatedChildCount] must subsequently return a precise non-null value (which is then used to implement [RenderSliverBoxChildManager.childCount]).

Subclasses typically override this function and wrap their children in [AutomaticKeepAlive], [IndexedSemantics], and [RepaintBoundary] widgets.

The values returned by this method are cached. To indicate that the widgets have changed, a new delegate must be provided, and the new delegate's [shouldRebuild] method must return true.

### estimatedChildCount

```dart
int? get estimatedChildCount
```

Returns an estimate of the number of children this delegate will build.

Used to estimate the maximum scroll offset if [estimateMaxScrollOffset] returns null.

Return null if there are an unbounded number of children or if it would be too difficult to estimate the number of children.

This must return a precise number once [build] has returned null, as it used to implement [RenderSliverBoxChildManager.childCount].

### estimateMaxScrollOffset()

```dart
double? estimateMaxScrollOffset(int firstIndex, int lastIndex, double leadingScrollOffset, double trailingScrollOffset)
```

Returns an estimate of the max scroll extent for all the children.

Subclasses should override this function if they have additional information about their max scroll extent.

The default implementation returns null, which causes the caller to extrapolate the max scroll offset from the given parameters.

### didFinishLayout()

```dart
void didFinishLayout(int firstIndex, int lastIndex)
```

Called at the end of layout to indicate that layout is now complete.

The `firstIndex` argument is the index of the first child that was included in the current layout. The `lastIndex` argument is the index of the last child that was included in the current layout.

Useful for subclasses that wish to track which children are included in the underlying render tree.

### shouldRebuild()

```dart
bool shouldRebuild(SliverChildDelegate oldDelegate)
```

Called whenever a new instance of the child delegate class is provided to the sliver.

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If the method returns false, then the [build] call might be optimized away.

### findIndexByKey()

```dart
int? findIndexByKey(Key key)
```

Find index of child element with associated key.

This will be called during `performRebuild` in [SliverMultiBoxAdaptorElement] to check if a child has moved to a different position. It should return the index of the child element with associated key, null if not found.

If not provided, a child widget may not map to its existing [RenderObject] when the order of children returned from the children builder changes. This may result in state-loss.

### toString()

```dart
String toString()
```

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

Add additional information to the given description for use by [toString].

# ChildIndexGetter

```dart
typedef ChildIndexGetter = int? Function(Key key)
```

Called to find the new index of a child based on its `key` in case of reordering.

If the child with the `key` is no longer present, null is returned.

Used by [SliverChildBuilderDelegate.findChildIndexCallback].

# SliverChildBuilderDelegate

```dart
class SliverChildBuilderDelegate extends SliverChildDelegate {}
```

A delegate that supplies children for slivers using a builder callback.

Many slivers lazily construct their box children to avoid creating more children than are visible through the [Viewport]. This delegate provides children using a [NullableIndexedWidgetBuilder] callback, so that the children do not even have to be built until they are displayed.

The widgets returned from the builder callback are automatically wrapped in [AutomaticKeepAlive] widgets if [addAutomaticKeepAlives] is true (the default) and in [RepaintBoundary] widgets if [addRepaintBoundaries] is true (also the default).

## Accessibility

The [CustomScrollView] requires that its semantic children are annotated using [IndexedSemantics]. This is done by default in the delegate with the `addSemanticIndexes` parameter set to true.

If multiple delegates are used in a single scroll view, then the indexes will not be correct by default. The `semanticIndexOffset` can be used to offset the semantic indexes of each delegate so that the indexes are monotonically increasing. For example, if a scroll view contains two delegates where the first has 10 children contributing semantics, then the second delegate should offset its children by 10.

{@tool snippet}

This sample code shows how to use `semanticIndexOffset` to handle multiple delegates in a single scroll view.

```dart
CustomScrollView(
  semanticChildCount: 4,
  slivers: <Widget>[
    SliverGrid(
      gridDelegate: _gridDelegate,
      delegate: SliverChildBuilderDelegate(
        (BuildContext context, int index) {
           return const Text('...');
         },
         childCount: 2,
       ),
     ),
    SliverGrid(
      gridDelegate: _gridDelegate,
      delegate: SliverChildBuilderDelegate(
        (BuildContext context, int index) {
           return const Text('...');
         },
         childCount: 2,
         semanticIndexOffset: 2,
       ),
     ),
  ],
)
```

{@end-tool}

In certain cases, only a subset of child widgets should be annotated with a semantic index. For example, in [ListView.separated()] the separators do not have an index associated with them. This is done by providing a `semanticIndexCallback` which returns null for separators indexes and rounds the non-separator indexes down by half.

{@tool snippet}

This sample code shows how to use `semanticIndexCallback` to handle annotating a subset of child nodes with a semantic index. There is a [Spacer] widget at odd indexes which should not have a semantic index.

```dart
CustomScrollView(
  semanticChildCount: 5,
  slivers: <Widget>[
    SliverGrid(
      gridDelegate: _gridDelegate,
      delegate: SliverChildBuilderDelegate(
        (BuildContext context, int index) {
           if (index.isEven) {
             return const Text('...');
           }
           return const Spacer();
         },
         semanticIndexCallback: (Widget widget, int localIndex) {
           if (localIndex.isEven) {
             return localIndex ~/ 2;
           }
           return null;
         },
         childCount: 10,
       ),
     ),
  ],
)
```

{@end-tool}

See also:

- [SliverChildListDelegate], which is a delegate that has an explicit list of children.
- [IndexedSemantics], for an example of manually annotating child nodes with semantic indexes.

### SliverChildBuilderDelegate()

```dart
SliverChildBuilderDelegate(NullableIndexedWidgetBuilder builder, {ChildIndexGetter? findChildIndexCallback, int? childCount, bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, SemanticIndexCallback semanticIndexCallback = _kDefaultSemanticIndexCallback, int semanticIndexOffset = 0})
```

Creates a delegate that supplies children for slivers using the given builder callback.

The [builder], [addAutomaticKeepAlives], [addRepaintBoundaries], [addSemanticIndexes], and [semanticIndexCallback] arguments must not be null.

If the order in which [builder] returns children ever changes, consider providing a [findChildIndexCallback]. This allows the delegate to find the new index for a child that was previously located at a different index to attach the existing state to the [Widget] at its new location.

### builder

```dart
NullableIndexedWidgetBuilder builder
```

Called to build children for the sliver.

Will be called only for indices greater than or equal to zero and less than [childCount] (if [childCount] is non-null).

Should return null if asked to build a widget with a greater index than exists.

May result in an infinite loop or run out of memory if [childCount] is null and the [builder] always provides a zero-size widget (such as `Container()` or `SizedBox.shrink()`). If possible, provide children with non-zero size, return null from [builder], or set a [childCount].

The delegate wraps the children returned by this builder in [RepaintBoundary] widgets.

### childCount

```dart
int? childCount
```

The total number of children this delegate can provide.

If null, the number of children is determined by the least index for which [builder] returns null.

May result in an infinite loop or run out of memory if [childCount] is null and the [builder] always provides a zero-size widget (such as `Container()` or `SizedBox.shrink()`). If possible, provide children with non-zero size, return null from [builder], or set a [childCount].

### addAutomaticKeepAlives

```dart
bool addAutomaticKeepAlives
```

{@template flutter.widgets.SliverChildBuilderDelegate.addAutomaticKeepAlives} Whether to wrap each child in an [AutomaticKeepAlive].

Typically, lazily laid out children are wrapped in [AutomaticKeepAlive] widgets so that the children can use [KeepAliveNotification]s to preserve their state when they would otherwise be garbage collected off-screen.

This feature (and [addRepaintBoundaries]) must be disabled if the children are going to manually maintain their [KeepAlive] state. It may also be more efficient to disable this feature if it is known ahead of time that none of the children will ever try to keep themselves alive.

Defaults to true.

{@tool dartpad} This sample demonstrates how to use the [AutomaticKeepAlive] widget in combination with the [AutomaticKeepAliveClientMixin] to selectively preserve the state of individual items in a scrollable list.

Normally, widgets in a lazily built list like [ListView.builder] are disposed of when they leave the visible area to maintain performance. This means that any state inside a [StatefulWidget] would be lost unless explicitly preserved.

In this example, each list item is a [StatefulWidget] that includes a counter and an increment button. To preserve the state of selected items (based on their index), the [AutomaticKeepAlive] widget and [AutomaticKeepAliveClientMixin] are used:

- The `wantKeepAlive` getter in the item’s state class returns true for even-indexed items, indicating that their state should be preserved.
- For odd-indexed items, `wantKeepAlive` returns false, so their state is not preserved when scrolled out of view.

** See code in examples/api/lib/widgets/keep_alive/automatic_keep_alive.0.dart ** {@end-tool}

{@tool dartpad} This sample demonstrates how to use the [KeepAlive] widget to preserve the state of individual list items in a [ListView] when they are scrolled out of view.

By default, [ListView.builder] only keeps the widgets currently visible in the viewport alive. When an item scrolls out of view, it may be disposed to free up resources. This can cause the state of [StatefulWidget]s to be lost if not explicitly preserved.

In this example, each item in the list is a [StatefulWidget] that maintains a counter. Tapping the "+" button increments the counter. To selectively preserve the state, each item is wrapped in a [KeepAlive] widget, with the keepAlive parameter set based on the item’s index:

- For even-indexed items, `keepAlive: true`, so their state is preserved even when scrolled off-screen.
- For odd-indexed items, `keepAlive: false`, so their state is discarded when they are no longer visible.

** See code in examples/api/lib/widgets/keep_alive/keep_alive.0.dart ** {@end-tool}

- [AutomaticKeepAlive], which allows subtrees to request to be kept alive in lazy lists.
- [AutomaticKeepAliveClientMixin], which is a mixin with convenience methods for clients of [AutomaticKeepAlive]. Used with [State] subclasses.
- [KeepAlive] which marks a child as needing to stay alive even when it's in a lazy list that would otherwise remove it. {@endtemplate}

### addRepaintBoundaries

```dart
bool addRepaintBoundaries
```

{@template flutter.widgets.SliverChildBuilderDelegate.addRepaintBoundaries} Whether to wrap each child in a [RepaintBoundary].

Typically, children in a scrolling container are wrapped in repaint boundaries so that they do not need to be repainted as the list scrolls. If the children are easy to repaint (e.g., solid color blocks or a short snippet of text), it might be more efficient to not add a repaint boundary and instead always repaint the children during scrolling.

Defaults to true. {@endtemplate}

### addSemanticIndexes

```dart
bool addSemanticIndexes
```

{@template flutter.widgets.SliverChildBuilderDelegate.addSemanticIndexes} Whether to wrap each child in an [IndexedSemantics].

Typically, children in a scrolling container must be annotated with a semantic index in order to generate the correct accessibility announcements. This should only be set to false if the indexes have already been provided by an [IndexedSemantics] widget.

Defaults to true.

See also:

- [IndexedSemantics], for an explanation of how to manually provide semantic indexes. {@endtemplate}

### semanticIndexOffset

```dart
int semanticIndexOffset
```

{@template flutter.widgets.SliverChildBuilderDelegate.semanticIndexOffset} An initial offset to add to the semantic indexes generated by this widget.

Defaults to zero. {@endtemplate}

### semanticIndexCallback

```dart
SemanticIndexCallback semanticIndexCallback
```

{@template flutter.widgets.SliverChildBuilderDelegate.semanticIndexCallback} A [SemanticIndexCallback] which is used when [addSemanticIndexes] is true.

Defaults to providing an index for each widget. {@endtemplate}

### findChildIndexCallback

```dart
ChildIndexGetter? findChildIndexCallback
```

{@template flutter.widgets.SliverChildBuilderDelegate.findChildIndexCallback} Called to find the new index of a child based on its key in case of reordering.

If not provided, a child widget may not map to its existing [RenderObject] when the order of children returned from the children builder changes. This may result in state-loss.

This callback should take an input [Key], and it should return the index of the child element with that associated key, or null if not found. {@endtemplate}

### findIndexByKey()

```dart
int? findIndexByKey(Key key)
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### shouldRebuild()

```dart
bool shouldRebuild(SliverChildBuilderDelegate oldDelegate)
```

# SliverChildListDelegate

```dart
class SliverChildListDelegate extends SliverChildDelegate {}
```

A delegate that supplies children for slivers using an explicit list.

Many slivers lazily construct their box children to avoid creating more children than are visible through the [Viewport]. This delegate provides children using an explicit list, which is convenient but reduces the benefit of building children lazily.

In general building all the widgets in advance is not efficient. It is better to create a delegate that builds them on demand using [SliverChildBuilderDelegate] or by subclassing [SliverChildDelegate] directly.

This class is provided for the cases where either the list of children is known well in advance (ideally the children are themselves compile-time constants, for example), and therefore will not be built each time the delegate itself is created, or the list is small, such that it's likely always visible (and thus there is nothing to be gained by building it on demand). For example, the body of a dialog box might fit both of these conditions.

The widgets in the given [children] list are automatically wrapped in [AutomaticKeepAlive] widgets if [addAutomaticKeepAlives] is true (the default) and in [RepaintBoundary] widgets if [addRepaintBoundaries] is true (also the default).

## Accessibility

The [CustomScrollView] requires that its semantic children are annotated using [IndexedSemantics]. This is done by default in the delegate with the `addSemanticIndexes` parameter set to true.

If multiple delegates are used in a single scroll view, then the indexes will not be correct by default. The `semanticIndexOffset` can be used to offset the semantic indexes of each delegate so that the indexes are monotonically increasing. For example, if a scroll view contains two delegates where the first has 10 children contributing semantics, then the second delegate should offset its children by 10.

In certain cases, only a subset of child widgets should be annotated with a semantic index. For example, in [ListView.separated()] the separators do not have an index associated with them. This is done by providing a `semanticIndexCallback` which returns null for separators indexes and rounds the non-separator indexes down by half.

See [SliverChildBuilderDelegate] for sample code using `semanticIndexOffset` and `semanticIndexCallback`.

See also:

- [SliverChildBuilderDelegate], which is a delegate that uses a builder callback to construct the children.

### SliverChildListDelegate()

```dart
SliverChildListDelegate(List<Widget> children, {bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, SemanticIndexCallback semanticIndexCallback = _kDefaultSemanticIndexCallback, int semanticIndexOffset = 0})
```

Creates a delegate that supplies children for slivers using the given list.

The [children], [addAutomaticKeepAlives], [addRepaintBoundaries], [addSemanticIndexes], and [semanticIndexCallback] arguments must not be null.

If the order of children never changes, consider using the constant [SliverChildListDelegate.fixed] constructor.

### SliverChildListDelegate.fixed()

```dart
SliverChildListDelegate.fixed(List<Widget> children, {bool addAutomaticKeepAlives = true, bool addRepaintBoundaries = true, bool addSemanticIndexes = true, SemanticIndexCallback semanticIndexCallback = _kDefaultSemanticIndexCallback, int semanticIndexOffset = 0})
```

Creates a constant version of the delegate that supplies children for slivers using the given list.

If the order of the children will change, consider using the regular [SliverChildListDelegate] constructor.

The [children], [addAutomaticKeepAlives], [addRepaintBoundaries], [addSemanticIndexes], and [semanticIndexCallback] arguments must not be null.

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

### semanticIndexOffset

```dart
int semanticIndexOffset
```

{@macro flutter.widgets.SliverChildBuilderDelegate.semanticIndexOffset}

### semanticIndexCallback

```dart
SemanticIndexCallback semanticIndexCallback
```

{@macro flutter.widgets.SliverChildBuilderDelegate.semanticIndexCallback}

### children

```dart
List<Widget> children
```

The widgets to display.

If this list is going to be mutated, it is usually wise to put a [Key] on each of the child widgets, so that the framework can match old configurations to new configurations and maintain the underlying render objects.

Also, a [Widget] in Flutter is immutable, so directly modifying the [children] such as `someWidget.children.add(...)` or passing a reference of the original list value to the [children] parameter will result in incorrect behaviors. Whenever the children list is modified, a new list object must be provided.

The following code corrects the problem mentioned above.

```dart
class SomeWidgetState extends State<SomeWidget> {
  final List<Widget> _children = <Widget>[];

  void someHandler() {
    setState(() {
      // The key here allows Flutter to reuse the underlying render
      // objects even if the children list is recreated.
      _children.add(ChildWidget(key: UniqueKey()));
    });
  }

  @override
  Widget build(BuildContext context) {
    // Always create a new list of children as a Widget is immutable.
    return PageView(children: List<Widget>.of(_children));
  }
}
```

### findIndexByKey()

```dart
int? findIndexByKey(Key key)
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### shouldRebuild()

```dart
bool shouldRebuild(SliverChildListDelegate oldDelegate)
```

# TwoDimensionalChildDelegate

```dart
abstract class TwoDimensionalChildDelegate extends ChangeNotifier {}
```

A delegate that supplies children for scrolling in two dimensions.

A [TwoDimensionalScrollView] lazily constructs its box children to avoid creating more children than are visible through the [TwoDimensionalViewport]. Rather than receiving children as an explicit [List], it receives its children using a [TwoDimensionalChildDelegate].

As a ChangeNotifier, this delegate allows subclasses to notify its listeners (typically as a subclass of [RenderTwoDimensionalViewport]) to rebuild when aspects of the delegate change. When values returned by getters or builders on this delegate change, [notifyListeners] should be called. This signals to the [RenderTwoDimensionalViewport] that the getters and builders need to be re-queried to update the layout of children in the viewport.

See also:

- [TwoDimensionalChildBuilderDelegate], an concrete subclass of this that lazily builds children on demand.
- [TwoDimensionalChildListDelegate], an concrete subclass of this that uses a two dimensional array to layout children.

### TwoDimensionalChildDelegate()

```dart
TwoDimensionalChildDelegate()
```

Creates a delegate that supplies children for scrolling in two dimensions.

### build()

```dart
Widget? build(BuildContext context, ChildVicinity vicinity)
```

Returns the child with the given [ChildVicinity], which is described in terms of x and y indices.

Subclasses must implement this function and will typically wrap their children in [RepaintBoundary] widgets.

The values returned by this method are cached. To indicate that the widgets have changed, a new delegate must be provided, and the new delegate's [shouldRebuild] method must return true. Alternatively, calling [notifyListeners] will allow the same delegate to be used.

### shouldRebuild()

```dart
bool shouldRebuild(TwoDimensionalChildDelegate oldDelegate)
```

Called whenever a new instance of the child delegate class is provided.

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If the method returns false, then the [build] call might be optimized away.

# TwoDimensionalChildBuilderDelegate

```dart
class TwoDimensionalChildBuilderDelegate extends TwoDimensionalChildDelegate {}
```

A delegate that supplies children for a [TwoDimensionalScrollView] using a builder callback.

The widgets returned from the builder callback are automatically wrapped in [RepaintBoundary] widgets if [addRepaintBoundaries] is true (also the default).

See also:

- [TwoDimensionalChildListDelegate], which is a similar delegate that has an explicit two dimensional array of children.
- [SliverChildBuilderDelegate], which is a delegate that uses a builder callback to construct the children in one dimension instead of two.
- [SliverChildListDelegate], which is a delegate that has an explicit list of children in one dimension instead of two.

### TwoDimensionalChildBuilderDelegate()

```dart
TwoDimensionalChildBuilderDelegate({required TwoDimensionalIndexedWidgetBuilder builder, int? maxXIndex, int? maxYIndex, bool addRepaintBoundaries = true, bool addAutomaticKeepAlives = true})
```

Creates a delegate that supplies children for a [TwoDimensionalScrollView] using the given builder callback.

### builder

```dart
TwoDimensionalIndexedWidgetBuilder builder
```

Called to build children on demand.

Implementors of [RenderTwoDimensionalViewport.layoutChildSequence] call this builder to create the children of the viewport. For [ChildVicinity] indices greater than [maxXIndex] or [maxYIndex], null will be returned by the default [build] implementation. This default behavior can be changed by overriding the build method.

Must return null if asked to build a widget with a [ChildVicinity] that does not exist.

The delegate wraps the children returned by this builder in [RepaintBoundary] widgets if [addRepaintBoundaries] is true.

### maxXIndex

```dart
int? get maxXIndex
```

The maximum [ChildVicinity.xIndex] for children in the x axis.

{@template flutter.widgets.twoDimensionalChildBuilderDelegate.maxIndex} For each [ChildVicinity], the child's relative location is described in terms of x and y indices to facilitate a consistent visitor pattern for all children in the viewport.

This is fairly straightforward in the context of a table implementation, where there is usually the same number of columns in every row and vice versa, each aligned one after the other.

When plotting children more abstractly in two dimensional space, there may be more x indices for a given y index than another y index. An example of this would be a scatter plot where there are more children at the top of the graph than at the bottom.

If null, subclasses of [RenderTwoDimensionalViewport] can continue call on the [builder] until null has been returned for each known index of x and y. In some cases, null may not be a terminating result, such as a table with a merged cell spanning multiple indices. Refer to the [TwoDimensionalViewport] subclass to learn how this value is applied in the specific use case.

If not null, the value must be greater than or equal to -1, where -1 indicates there will be no children at all provided to the [TwoDimensionalViewport].

If the value changes, the delegate will call [notifyListeners]. This informs the [RenderTwoDimensionalViewport] that any cached information from the delegate is invalid. {@endtemplate}

This value represents the greatest x index of all [ChildVicinity]s for the two dimensional scroll view.

See also:

- [RenderTwoDimensionalViewport.buildOrObtainChildFor], the method that leads to calling on the delegate to build a child of the given [ChildVicinity].

### maxXIndex

```dart
set maxXIndex(int? value)
```

### maxYIndex

```dart
int? get maxYIndex
```

The maximum [ChildVicinity.yIndex] for children in the y axis.

{@macro flutter.widgets.twoDimensionalChildBuilderDelegate.maxIndex}

This value represents the greatest y index of all [ChildVicinity]s for the two dimensional scroll view.

See also:

- [RenderTwoDimensionalViewport.buildOrObtainChildFor], the method that leads to calling on the delegate to build a child of the given [ChildVicinity].

### maxYIndex

```dart
set maxYIndex(int? value)
```

### addRepaintBoundaries

```dart
bool addRepaintBoundaries
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addRepaintBoundaries}

### addAutomaticKeepAlives

```dart
bool addAutomaticKeepAlives
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addAutomaticKeepAlives}

### build()

```dart
Widget? build(BuildContext context, ChildVicinity vicinity)
```

### shouldRebuild()

```dart
bool shouldRebuild(TwoDimensionalChildDelegate oldDelegate)
```

# TwoDimensionalChildListDelegate

```dart
class TwoDimensionalChildListDelegate extends TwoDimensionalChildDelegate {}
```

A delegate that supplies children for a [TwoDimensionalViewport] using an explicit two dimensional array.

In general, building all the widgets in advance is not efficient. It is better to create a delegate that builds them on demand using [TwoDimensionalChildBuilderDelegate] or by subclassing [TwoDimensionalChildDelegate] directly.

This class is provided for the cases where either the list of children is known well in advance (ideally the children are themselves compile-time constants, for example), and therefore will not be built each time the delegate itself is created, or the array is small, such that it's likely always visible (and thus there is nothing to be gained by building it on demand).

The widgets in the given [children] list are automatically wrapped in [RepaintBoundary] widgets if [addRepaintBoundaries] is true (also the default).

The [children] are accessed for each [ChildVicinity.yIndex] and [ChildVicinity.xIndex] of the [TwoDimensionalViewport] as `children[vicinity.yIndex][vicinity.xIndex]`.

See also:

- [TwoDimensionalChildBuilderDelegate], which is a delegate that uses a builder callback to construct the children.
- [SliverChildBuilderDelegate], which is a delegate that uses a builder callback to construct the children in one dimension instead of two.
- [SliverChildListDelegate], which is a delegate that has an explicit list of children in one dimension instead of two.

### TwoDimensionalChildListDelegate()

```dart
TwoDimensionalChildListDelegate({bool addRepaintBoundaries = true, bool addAutomaticKeepAlives = true, required List<List<Widget>> children})
```

Creates a delegate that supplies children for a [TwoDimensionalScrollView].

The [children] and [addRepaintBoundaries] must not be null.

### children

```dart
List<List<Widget>> children
```

The widgets to display.

Also, a [Widget] in Flutter is immutable, so directly modifying the [children] such as `someWidget.children.add(...)` or passing a reference of the original list value to the [children] parameter will result in incorrect behaviors. Whenever the children list is modified, a new list object must be provided.

The [children] are accessed for each [ChildVicinity.yIndex] and [ChildVicinity.xIndex] of the [TwoDimensionalViewport] as `children[vicinity.yIndex][vicinity.xIndex]`.

### addRepaintBoundaries

```dart
bool addRepaintBoundaries
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addRepaintBoundaries}

### addAutomaticKeepAlives

```dart
bool addAutomaticKeepAlives
```

{@macro flutter.widgets.SliverChildBuilderDelegate.addAutomaticKeepAlives}

### build()

```dart
Widget? build(BuildContext context, ChildVicinity vicinity)
```

### shouldRebuild()

```dart
bool shouldRebuild(TwoDimensionalChildListDelegate oldDelegate)
```
