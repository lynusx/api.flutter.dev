@docImport 'package:flutter/material.dart';

# ReorderCallback

```dart
typedef ReorderCallback = void Function(int oldIndex, int newIndex)
```

A callback used by [ReorderableList] to report that a list item has moved to a new position in the list.

Implementations should remove the corresponding list item at [oldIndex] and reinsert it at [newIndex].

{@youtube 560 315 https://www.youtube.com/watch?v=3fB1mxOsqJE}

{@tool snippet}

```dart
final List<MyDataObject> backingList = <MyDataObject>[/* ... */];

void handleReorderItem(int oldIndex, int newIndex) {
  final MyDataObject element = backingList.removeAt(oldIndex);
  backingList.insert(newIndex, element);
}
```

{@end-tool}

See also:

- [ReorderableList], a widget list that allows the user to reorder its items.
- [SliverReorderableList], a sliver list that allows the user to reorder its items.
- [ReorderableListView], a Material Design list that allows the user to reorder its items.

# ReorderItemProxyDecorator

```dart
typedef ReorderItemProxyDecorator = Widget Function(Widget child, int index, Animation<double> animation)
```

Signature for the builder callback used to decorate the dragging item in [ReorderableList] and [SliverReorderableList].

The [child] will be the item that is being dragged, and [index] is the position of the item in the list.

The [animation] will be driven forward from 0.0 to 1.0 while the item is being picked up during a drag operation, and reversed from 1.0 to 0.0 when the item is dropped. This can be used to animate properties of the proxy like an elevation or border.

The returned value will typically be the [child] wrapped in other widgets.

# ReorderDragBoundaryProvider

```dart
typedef ReorderDragBoundaryProvider = DragBoundaryDelegate<Rect>? Function(BuildContext context)
```

Used to provide drag boundaries during drag-and-drop reordering.

{@tool snippet}

```dart
DragBoundary(
 child: CustomScrollView(
   slivers: <Widget>[
     SliverReorderableList(
       itemBuilder: (BuildContext context, int index) {
         return ReorderableDragStartListener(
           key: ValueKey<int>(index),
           index: index,
           child: Text('$index'),
         );
       },
       dragBoundaryProvider: (BuildContext context) {
         return DragBoundary.forRectOf(context);
       },
       itemCount: 5,
       onReorderItem: (int fromIndex, int toIndex) {},
     ),
   ],
 )
)
```

{@end-tool}

See also:

- [DragBoundary], a widget that provides drag boundaries.

# ReorderableList

```dart
class ReorderableList extends StatefulWidget {}
```

A scrolling container that allows the user to interactively reorder the list items.

This widget is similar to one created by [ListView.builder], and uses an [IndexedWidgetBuilder] to create each item.

It is up to the application to wrap each child (or an internal part of the child such as a drag handle) with a drag listener that will recognize the start of an item drag and then start the reorder by calling [ReorderableListState.startItemDragReorder]. This is most easily achieved by wrapping each child in a [ReorderableDragStartListener] or a [ReorderableDelayedDragStartListener]. These will take care of recognizing the start of a drag gesture and call the list state's [ReorderableListState.startItemDragReorder] method.

This widget's [ReorderableListState] can be used to manually start an item reorder, or cancel a current drag. To refer to the [ReorderableListState] either provide a [GlobalKey] or use the static [ReorderableList.of] method from an item's build method.

See also:

- [SliverReorderableList], a sliver list that allows the user to reorder its items.
- [ReorderableListView], a Material Design list that allows the user to reorder its items.

### ReorderableList()

```dart
ReorderableList({dynamic key, required IndexedWidgetBuilder itemBuilder, required int itemCount, ReorderCallback? onReorder, ReorderCallback? onReorderItem, void Function(int index)? onReorderStart, void Function(int index)? onReorderEnd, double? itemExtent, ItemExtentBuilder? itemExtentBuilder, Widget? prototypeItem, ReorderItemProxyDecorator? proxyDecorator, EdgeInsetsGeometry? padding, Axis scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, bool shrinkWrap = false, double anchor = 0.0, double? cacheExtent, ScrollCacheExtent? scrollCacheExtent, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ScrollViewKeyboardDismissBehavior? keyboardDismissBehavior, String? restorationId, Clip clipBehavior = Clip.hardEdge, double? autoScrollerVelocityScalar, ReorderDragBoundaryProvider? dragBoundaryProvider})
```

Creates a scrolling container that allows the user to interactively reorder the list items.

The [itemCount] must be greater than or equal to zero.

### itemBuilder

```dart
IndexedWidgetBuilder itemBuilder
```

{@template flutter.widgets.reorderable_list.itemBuilder} Called, as needed, to build list item widgets.

List items are only built when they're scrolled into view.

The [IndexedWidgetBuilder] index parameter indicates the item's position in the list. The value of the index parameter will be between zero and one less than [itemCount]. All items in the list must have a unique [Key], and should have some kind of listener to start the drag (usually a [ReorderableDragStartListener] or [ReorderableDelayedDragStartListener]). {@endtemplate}

### itemCount

```dart
int itemCount
```

{@template flutter.widgets.reorderable_list.itemCount} The number of items in the list.

It must be a non-negative integer. When zero, nothing is displayed and the widget occupies no space. {@endtemplate}

### onReorder

```dart
ReorderCallback? onReorder
```

{@template flutter.widgets.reorderable_list.onReorder} A callback used by the list to report that a list item has been dragged to a new location in the list and the application should update the order of the items.

If `oldIndex` is before `newIndex`, removing the item at `oldIndex` from the list will reduce the list's length by one. Implementations will need to account for this when inserting before `newIndex`.

This callback has been deprecated in favor of [onReorderItem], which simplifies the reordering logic by automatically handling index adjustments. To migrate, remove the manual adjustment of `newIndex` when items are moved downward in the list.

For example:

```dart
onReorder: (int oldIndex, int newIndex) {
  if (newIndex > oldIndex) {
    newIndex -= 1;
  }

  // Handle reordering...
}
```

becomes

```dart
onReorderItem: (int oldIndex, int newIndex) {
  // Handle reordering...
}
```

{@endtemplate}

### onReorderItem

```dart
ReorderCallback? onReorderItem
```

{@template flutter.widgets.reorderable_list.onReorderItem} A callback used by the list to report that a list item has been dragged to a new location in the list and the application should update the order of the items. {@endtemplate}

### onReorderStart

```dart
void Function(int index)? onReorderStart
```

{@template flutter.widgets.reorderable_list.onReorderStart} A callback that is called when an item drag has started.

The index parameter of the callback is the index of the selected item.

See also:

- [onReorderEnd], which is a called when the dragged item is dropped.
- [onReorderItem], which reports that a list item has been dragged to a new location. {@endtemplate}

### onReorderEnd

```dart
void Function(int index)? onReorderEnd
```

{@template flutter.widgets.reorderable_list.onReorderEnd} A callback that is called when the dragged item is dropped.

The index parameter of the callback is the index where the item is dropped. Unlike [onReorderItem], this is called even when the list item is dropped in the same location.

See also:

- [onReorderStart], which is a called when an item drag has started.
- [onReorderItem], which reports that a list item has been dragged to a new location. {@endtemplate}

### proxyDecorator

```dart
ReorderItemProxyDecorator? proxyDecorator
```

{@template flutter.widgets.reorderable_list.proxyDecorator} A callback that allows the app to add an animated decoration around an item when it is being dragged. {@endtemplate}

### padding

```dart
EdgeInsetsGeometry? padding
```

{@template flutter.widgets.reorderable_list.padding} The amount of space by which to inset the list contents.

It defaults to `EdgeInsets.all(0)`. {@endtemplate}

### scrollDirection

```dart
Axis scrollDirection
```

{@macro flutter.widgets.scroll_view.scrollDirection}

### reverse

```dart
bool reverse
```

{@macro flutter.widgets.scroll_view.reverse}

### controller

```dart
ScrollController? controller
```

{@macro flutter.widgets.scroll_view.controller}

### primary

```dart
bool? primary
```

{@macro flutter.widgets.scroll_view.primary}

### physics

```dart
ScrollPhysics? physics
```

{@macro flutter.widgets.scroll_view.physics}

### shrinkWrap

```dart
bool shrinkWrap
```

{@macro flutter.widgets.scroll_view.shrinkWrap}

### anchor

```dart
double anchor
```

{@macro flutter.widgets.scroll_view.anchor}

### cacheExtent

```dart
double? cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

### scrollCacheExtent

```dart
ScrollCacheExtent? scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### keyboardDismissBehavior

```dart
ScrollViewKeyboardDismissBehavior? keyboardDismissBehavior
```

{@macro flutter.widgets.scroll_view.keyboardDismissBehavior}

If [keyboardDismissBehavior] is null then it will fallback to the inherited [ScrollBehavior.getKeyboardDismissBehavior].

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### itemExtent

```dart
double? itemExtent
```

{@macro flutter.widgets.list_view.itemExtent}

### itemExtentBuilder

```dart
ItemExtentBuilder? itemExtentBuilder
```

{@macro flutter.widgets.list_view.itemExtentBuilder}

### prototypeItem

```dart
Widget? prototypeItem
```

{@macro flutter.widgets.list_view.prototypeItem}

### autoScrollerVelocityScalar

```dart
double? autoScrollerVelocityScalar
```

{@macro flutter.widgets.EdgeDraggingAutoScroller.velocityScalar}

{@macro flutter.widgets.SliverReorderableList.autoScrollerVelocityScalar.default}

### dragBoundaryProvider

```dart
ReorderDragBoundaryProvider? dragBoundaryProvider
```

{@template flutter.widgets.reorderable_list.dragBoundaryProvider} A callback used to provide drag boundaries during drag-and-drop reordering.

If null, the delegate returned by `DragBoundary.forRectMaybeOf` will be used. Defaults to null. {@endtemplate}

### of()

```dart
ReorderableListState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [ReorderableList] item widgets that insert or remove items in response to user input.

If no [ReorderableList] surrounds the given context, then this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

See also:

- [maybeOf], a similar function that will return null if no [ReorderableList] ancestor is found.

### maybeOf()

```dart
ReorderableListState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [ReorderableList] item widgets that insert or remove items in response to user input.

If no [ReorderableList] surrounds the context given, then this function will return null.

This method can be expensive (it walks the element tree).

See also:

- [of], a similar function that will throw if no [ReorderableList] ancestor is found.

### createState()

```dart
ReorderableListState createState()
```

# ReorderableListState

```dart
class ReorderableListState extends State<ReorderableList> {}
```

The state for a list that allows the user to interactively reorder the list items.

An app that needs to start a new item drag or cancel an existing one can refer to the [ReorderableList]'s state with a global key:

```dart
GlobalKey<ReorderableListState> listKey = GlobalKey<ReorderableListState>();
// ...
Widget build(BuildContext context) {
  return ReorderableList(
    key: listKey,
    itemBuilder: (BuildContext context, int index) => const SizedBox(height: 10.0),
    itemCount: 5,
    onReorderItem: (int oldIndex, int newIndex) {
       // ...
    },
  );
}
// ...
listKey.currentState!.cancelReorder();
```

### startItemDragReorder()

```dart
void startItemDragReorder({required int index, required PointerDownEvent event, required MultiDragGestureRecognizer recognizer})
```

Initiate the dragging of the item at [index] that was started with the pointer down [event].

The given [recognizer] will be used to recognize and start the drag item tracking and lead to either an item reorder, or a canceled drag. The list will take ownership of the returned recognizer and will dispose it when it is no longer needed.

Most applications will not use this directly, but will wrap the item (or part of the item, like a drag handle) in either a [ReorderableDragStartListener] or [ReorderableDelayedDragStartListener] which call this for the application.

### cancelReorder()

```dart
void cancelReorder()
```

Cancel any item drag in progress.

This should be called before any major changes to the item list occur so that any item drags will not get confused by changes to the underlying list.

If no drag is active, this will do nothing.

### build()

```dart
Widget build(BuildContext context)
```

# SliverReorderableList

```dart
class SliverReorderableList extends StatefulWidget {}
```

A sliver list that allows the user to interactively reorder the list items.

It is up to the application to wrap each child (or an internal part of the child) with a drag listener that will recognize the start of an item drag and then start the reorder by calling [SliverReorderableListState.startItemDragReorder]. This is most easily achieved by wrapping each child in a [ReorderableDragStartListener] or a [ReorderableDelayedDragStartListener]. These will take care of recognizing the start of a drag gesture and call the list state's start item drag method.

This widget's [SliverReorderableListState] can be used to manually start an item reorder, or cancel a current drag that's already underway. To refer to the [SliverReorderableListState] either provide a [GlobalKey] or use the static [SliverReorderableList.of] method from an item's build method.

See also:

- [ReorderableList], a regular widget list that allows the user to reorder its items.
- [ReorderableListView], a Material Design list that allows the user to reorder its items.

### SliverReorderableList()

```dart
SliverReorderableList({dynamic key, required IndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, required int itemCount, ReorderCallback? onReorder, ReorderCallback? onReorderItem, void Function(int)? onReorderStart, void Function(int)? onReorderEnd, double? itemExtent, ItemExtentBuilder? itemExtentBuilder, Widget? prototypeItem, ReorderItemProxyDecorator? proxyDecorator, ReorderDragBoundaryProvider? dragBoundaryProvider, double? autoScrollerVelocityScalar})
```

Creates a sliver list that allows the user to interactively reorder its items.

The [itemCount] must be greater than or equal to zero.

### itemBuilder

```dart
IndexedWidgetBuilder itemBuilder
```

{@macro flutter.widgets.reorderable_list.itemBuilder}

### findChildIndexCallback

```dart
ChildIndexGetter? findChildIndexCallback
```

{@macro flutter.widgets.SliverChildBuilderDelegate.findChildIndexCallback}

### itemCount

```dart
int itemCount
```

{@macro flutter.widgets.reorderable_list.itemCount}

### onReorder

```dart
ReorderCallback? onReorder
```

{@macro flutter.widgets.reorderable_list.onReorder}

### onReorderItem

```dart
ReorderCallback? onReorderItem
```

{@macro flutter.widgets.reorderable_list.onReorderItem}

### onReorderStart

```dart
void Function(int)? onReorderStart
```

{@macro flutter.widgets.reorderable_list.onReorderStart}

### onReorderEnd

```dart
void Function(int)? onReorderEnd
```

{@macro flutter.widgets.reorderable_list.onReorderEnd}

### proxyDecorator

```dart
ReorderItemProxyDecorator? proxyDecorator
```

{@macro flutter.widgets.reorderable_list.proxyDecorator}

### itemExtent

```dart
double? itemExtent
```

{@macro flutter.widgets.list_view.itemExtent}

### itemExtentBuilder

```dart
ItemExtentBuilder? itemExtentBuilder
```

{@macro flutter.widgets.list_view.itemExtentBuilder}

### prototypeItem

```dart
Widget? prototypeItem
```

{@macro flutter.widgets.list_view.prototypeItem}

### autoScrollerVelocityScalar

```dart
double autoScrollerVelocityScalar
```

{@macro flutter.widgets.EdgeDraggingAutoScroller.velocityScalar}

{@template flutter.widgets.SliverReorderableList.autoScrollerVelocityScalar.default} Defaults to 50 if not set or set to null. {@endtemplate}

### dragBoundaryProvider

```dart
ReorderDragBoundaryProvider? dragBoundaryProvider
```

{@macro flutter.widgets.reorderable_list.dragBoundaryProvider}

### createState()

```dart
SliverReorderableListState createState()
```

### of()

```dart
SliverReorderableListState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [SliverReorderableList] item widgets to start or cancel an item drag operation.

If no [SliverReorderableList] surrounds the context given, this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

See also:

- [maybeOf], a similar function that will return null if no [SliverReorderableList] ancestor is found.

### maybeOf()

```dart
SliverReorderableListState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [SliverReorderableList] item widgets that insert or remove items in response to user input.

If no [SliverReorderableList] surrounds the context given, this function will return null.

This method can be expensive (it walks the element tree).

See also:

- [of], a similar function that will throw if no [SliverReorderableList] ancestor is found.

# SliverReorderableListState

```dart
class SliverReorderableListState extends State<SliverReorderableList> with TickerProviderStateMixin {}
```

The state for a sliver list that allows the user to interactively reorder the list items.

An app that needs to start a new item drag or cancel an existing one can refer to the [SliverReorderableList]'s state with a global key:

```dart
// (e.g. in a stateful widget)
GlobalKey<SliverReorderableListState> listKey = GlobalKey<SliverReorderableListState>();

// ...

@override
Widget build(BuildContext context) {
  return SliverReorderableList(
    key: listKey,
    itemBuilder: (BuildContext context, int index) => const SizedBox(height: 10.0),
    itemCount: 5,
    onReorderItem: (int oldIndex, int newIndex) {
       // ...
    },
  );
}

// ...

void _stop() {
  listKey.currentState!.cancelReorder();
}
```

[ReorderableDragStartListener] and [ReorderableDelayedDragStartListener] refer to their [SliverReorderableList] with the static [SliverReorderableList.of] method.

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(SliverReorderableList oldWidget)
```

### dispose()

```dart
void dispose()
```

### startItemDragReorder()

```dart
void startItemDragReorder({required int index, required PointerDownEvent event, required MultiDragGestureRecognizer recognizer})
```

Initiate the dragging of the item at [index] that was started with the pointer down [event].

The given [recognizer] will be used to recognize and start the drag item tracking and lead to either an item reorder, or a canceled drag.

Most applications will not use this directly, but will wrap the item (or part of the item, like a drag handle) in either a [ReorderableDragStartListener] or [ReorderableDelayedDragStartListener] which call this method when they detect the gesture that triggers a drag start.

### cancelReorder()

```dart
void cancelReorder()
```

Cancel any item drag in progress.

This should be called before any major changes to the item list occur so that any item drags will not get confused by changes to the underlying list.

If a drag operation is in progress, this will immediately reset the list to back to its pre-drag state.

If no drag is active, this will do nothing.

### build()

```dart
Widget build(BuildContext context)
```

# ReorderableDragStartListener

```dart
class ReorderableDragStartListener extends StatelessWidget {}
```

A wrapper widget that will recognize the start of a drag on the wrapped widget by a [PointerDownEvent], and immediately initiate dragging the wrapped item to a new location in a reorderable list.

See also:

- [ReorderableDelayedDragStartListener], a similar wrapper that will only recognize the start after a long press event.
- [ReorderableList], a widget list that allows the user to reorder its items.
- [SliverReorderableList], a sliver list that allows the user to reorder its items.
- [ReorderableListView], a Material Design list that allows the user to reorder its items.

### ReorderableDragStartListener()

```dart
ReorderableDragStartListener({dynamic key, required Widget child, required int index, bool enabled = true})
```

Creates a listener for a drag immediately following a pointer down event over the given child widget.

This is most commonly used to wrap part of a list item like a drag handle.

### child

```dart
Widget child
```

The widget for which the application would like to respond to a tap and drag gesture by starting a reordering drag on a reorderable list.

### index

```dart
int index
```

The index of the associated item that will be dragged in the list.

### enabled

```dart
bool enabled
```

Whether the [child] item can be dragged and moved in the list.

If true, the item can be moved to another location in the list when the user taps on the child. If false, tapping on the child will be ignored.

### build()

```dart
Widget build(BuildContext context)
```

### createRecognizer()

```dart
MultiDragGestureRecognizer createRecognizer()
```

Provides the gesture recognizer used to indicate the start of a reordering drag operation.

By default this returns an [ImmediateMultiDragGestureRecognizer] but subclasses can use this to customize the drag start gesture.

# ReorderableDelayedDragStartListener

```dart
class ReorderableDelayedDragStartListener extends ReorderableDragStartListener {}
```

A wrapper widget that will recognize the start of a drag operation by looking for a long press event. Once it is recognized, it will start a drag operation on the wrapped item in the reorderable list.

See also:

- [ReorderableDragStartListener], a similar wrapper that will recognize the start of the drag immediately after a pointer down event.
- [ReorderableList], a widget list that allows the user to reorder its items.
- [SliverReorderableList], a sliver list that allows the user to reorder its items.
- [ReorderableListView], a Material Design list that allows the user to reorder its items.

### ReorderableDelayedDragStartListener()

```dart
ReorderableDelayedDragStartListener({dynamic key, required Widget child, required int index, bool enabled})
```

Creates a listener for an drag following a long press event over the given child widget.

This is most commonly used to wrap an entire list item in a reorderable list.

### createRecognizer()

```dart
MultiDragGestureRecognizer createRecognizer()
```
