@docImport 'page_storage.dart'; @docImport 'primary_scroll_controller.dart';

# AnimatedList

```dart
class AnimatedList extends _AnimatedScrollView {}
```

A scrolling container that animates items when they are inserted or removed.

This widget's [AnimatedListState] can be used to dynamically insert or remove items. To refer to the [AnimatedListState] either provide a [GlobalKey] or use the static [of] method from an item's input callback.

This widget is similar to one created by [ListView.builder].

{@youtube 560 315 https://www.youtube.com/watch?v=ZtfItHwFlZ8}

{@tool dartpad} This sample application uses an [AnimatedList] to create an effect when items are removed or added to the list.

** See code in examples/api/lib/widgets/animated_list/animated_list.0.dart ** {@end-tool}

By default, [AnimatedList] will automatically pad the limits of the list's scrollable to avoid partial obstructions indicated by [MediaQuery]'s padding. To avoid this behavior, override with a zero [padding] property.

{@tool snippet} The following example demonstrates how to override the default top and bottom padding using [MediaQuery.removePadding].

```dart
Widget myWidget(BuildContext context) {
  return MediaQuery.removePadding(
    context: context,
    removeTop: true,
    removeBottom: true,
    child: AnimatedList(
      initialItemCount: 50,
      itemBuilder: (BuildContext context, int index, Animation<double> animation) {
        return Card(
          color: Colors.amber,
          child: Center(child: Text('$index')),
        );
      }
    ),
  );
}
```

{@end-tool}

See also:

- [SliverAnimatedList], a sliver that animates items when they are inserted or removed from a list.
- [SliverAnimatedGrid], a sliver which animates items when they are inserted or removed from a grid.
- [AnimatedGrid], a non-sliver scrolling container that animates items when they are inserted or removed in a grid.

### AnimatedList()

```dart
AnimatedList({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, bool shrinkWrap = false, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

Creates a scrolling container that animates items when they are inserted or removed.

### AnimatedList.separated()

```dart
AnimatedList.separated({dynamic key, required AnimatedItemBuilder itemBuilder, required AnimatedItemBuilder separatorBuilder, required Widget Function(BuildContext, int, InvalidType) removedSeparatorBuilder, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, bool shrinkWrap = false, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

A scrolling container that animates items with separators when they are inserted or removed.

This widget's [AnimatedListState] can be used to dynamically insert or remove items. To refer to the [AnimatedListState] either provide a [GlobalKey] or use the static [of] method from an item's input callback.

This widget is similar to one created by [ListView.separated].

{@tool dartpad} This sample application uses an [AnimatedList.separated] to create an effect when items are removed or added to the list.

** See code in examples/api/lib/widgets/animated_list/animated_list_separated.0.dart ** {@end-tool}

By default, [AnimatedList.separated] will automatically pad the limits of the list's scrollable to avoid partial obstructions indicated by [MediaQuery]'s padding. To avoid this behavior, override with a zero [padding] property.

{@tool snippet} The following example demonstrates how to override the default top and bottom padding using [MediaQuery.removePadding].

```dart
Widget myWidget(BuildContext context) {
  return MediaQuery.removePadding(
    context: context,
    removeTop: true,
    removeBottom: true,
    child: AnimatedList.separated(
      initialItemCount: 50,
      itemBuilder: (BuildContext context, int index, Animation<double> animation) {
        return Card(
          color: Colors.amber,
          child: Center(child: Text('$index')),
        );
      },
      separatorBuilder: (BuildContext context, int index, Animation<double> animation) {
        return const SizedBox(
          height: 1.0,
          width: double.infinity,
          child: ColoredBox(color: Color(0xFF000000)),
        );
      },
      removedSeparatorBuilder: (BuildContext context, int index, Animation<double> animation) {
        return const SizedBox(
          height: 1.0,
          width: double.infinity,
          child: ColoredBox(color: Color(0xFF000000)),
        );
      }
    ),
  );
}
```

{@end-tool}

See also:

- [SliverAnimatedList], a sliver that animates items when they are inserted or removed from a list.
- [SliverAnimatedGrid], a sliver which animates items when they are inserted or removed from a grid.
- [AnimatedGrid], a non-sliver scrolling container that animates items when they are inserted or removed in a grid.
- [AnimatedList], which animates items added and removed from a list instead of a grid.

### of()

```dart
AnimatedListState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [AnimatedList] item widgets that insert or remove items in response to user input.

If no [AnimatedList] surrounds the context given, then this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [maybeOf], a similar function that will return null if no [AnimatedList] ancestor is found.

### maybeOf()

```dart
AnimatedListState? maybeOf(BuildContext context)
```

The [AnimatedListState] from the closest instance of [AnimatedList] that encloses the given context.

This method is typically used by [AnimatedList] item widgets that insert or remove items in response to user input.

If no [AnimatedList] surrounds the context given, then this function will return null.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [of], a similar function that will throw if no [AnimatedList] ancestor is found.

### createState()

```dart
AnimatedListState createState()
```

# AnimatedListState

```dart
class AnimatedListState extends _AnimatedScrollViewState<AnimatedList> {}
```

The [AnimatedListState] for [AnimatedList], a scrolling list container that animates items when they are inserted or removed.

When an item is inserted with [insertItem] an animation begins running. The animation is passed to [AnimatedList.itemBuilder] whenever the item's widget is needed.

When multiple items are inserted with [insertAllItems] an animation begins running. The animation is passed to [AnimatedList.itemBuilder] whenever the item's widget is needed.

If using [AnimatedList.separated], the animation is also passed to `AnimatedList.separatorBuilder` whenever the separator's widget is needed.

When an item is removed with [removeItem] its animation is reversed. The removed item's animation is passed to the [removeItem] builder parameter. If using [AnimatedList.separated], the corresponding separator's animation is also passed to the [AnimatedList.removedSeparatorBuilder] parameter.

An app that needs to insert or remove items in response to an event can refer to the [AnimatedList]'s state with a global key:

```dart
// (e.g. in a stateful widget)
GlobalKey<AnimatedListState> listKey = GlobalKey<AnimatedListState>();

// ...

@override
Widget build(BuildContext context) {
  return AnimatedList(
    key: listKey,
    itemBuilder: (BuildContext context, int index, Animation<double> animation) {
      return const Placeholder();
    },
  );
}

// ...

void _updateList() {
  // adds "123" to the AnimatedList
  listKey.currentState!.insertItem(123);
}
```

[AnimatedList] item input handlers can also refer to their [AnimatedListState] with the static [AnimatedList.of] method.

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedGrid

```dart
class AnimatedGrid extends _AnimatedScrollView {}
```

A scrolling container that animates items when they are inserted into or removed from a grid. in a grid.

This widget's [AnimatedGridState] can be used to dynamically insert or remove items. To refer to the [AnimatedGridState] either provide a [GlobalKey] or use the static [of] method from an item's input callback.

This widget is similar to one created by [GridView.builder].

{@tool dartpad} This sample application uses an [AnimatedGrid] to create an effect when items are removed or added to the grid.

** See code in examples/api/lib/widgets/animated_grid/animated_grid.0.dart ** {@end-tool}

By default, [AnimatedGrid] will automatically pad the limits of the grid's scrollable to avoid partial obstructions indicated by [MediaQuery]'s padding. To avoid this behavior, override with a zero [padding] property.

{@tool snippet} The following example demonstrates how to override the default top and bottom padding using [MediaQuery.removePadding].

```dart
Widget myWidget(BuildContext context) {
  return MediaQuery.removePadding(
    context: context,
    removeTop: true,
    removeBottom: true,
    child: AnimatedGrid(
      gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
        crossAxisCount: 3,
      ),
      initialItemCount: 50,
      itemBuilder: (BuildContext context, int index, Animation<double> animation) {
        return Card(
          color: Colors.amber,
          child: Center(child: Text('$index')),
        );
      }
    ),
  );
}
```

{@end-tool}

See also:

- [SliverAnimatedGrid], a sliver which animates items when they are inserted into or removed from a grid.
- [SliverAnimatedList], a sliver which animates items added and removed from a list instead of a grid.
- [AnimatedList], which animates items added and removed from a list instead of a grid.

### AnimatedGrid()

```dart
AnimatedGrid({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, required SliverGridDelegate gridDelegate, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

Creates a scrolling container that animates items when they are inserted or removed.

### gridDelegate

```dart
SliverGridDelegate gridDelegate
```

{@template flutter.widgets.AnimatedGrid.gridDelegate} A delegate that controls the layout of the children within the [AnimatedGrid].

See also:

- [SliverGridDelegateWithFixedCrossAxisCount], which creates a layout with a fixed number of tiles in the cross axis.
- [SliverGridDelegateWithMaxCrossAxisExtent], which creates a layout with tiles that have a maximum cross-axis extent. {@endtemplate}

### of()

```dart
AnimatedGridState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [AnimatedGrid] item widgets that insert or remove items in response to user input.

If no [AnimatedGrid] surrounds the context given, then this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [maybeOf], a similar function that will return null if no [AnimatedGrid] ancestor is found.

### maybeOf()

```dart
AnimatedGridState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [AnimatedGrid] item widgets that insert or remove items in response to user input.

If no [AnimatedGrid] surrounds the context given, then this function will return null.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [of], a similar function that will throw if no [AnimatedGrid] ancestor is found.

### createState()

```dart
AnimatedGridState createState()
```

# AnimatedGridState

```dart
class AnimatedGridState extends _AnimatedScrollViewState<AnimatedGrid> {}
```

The [State] for an [AnimatedGrid] that animates items when they are inserted or removed.

When an item is inserted with [insertItem] an animation begins running. The animation is passed to [AnimatedGrid.itemBuilder] whenever the item's widget is needed.

When an item is removed with [removeItem] its animation is reversed. The removed item's animation is passed to the [removeItem] builder parameter.

An app that needs to insert or remove items in response to an event can refer to the [AnimatedGrid]'s state with a global key:

```dart
// (e.g. in a stateful widget)
GlobalKey<AnimatedGridState> gridKey = GlobalKey<AnimatedGridState>();

// ...

@override
Widget build(BuildContext context) {
  return AnimatedGrid(
    key: gridKey,
    itemBuilder: (BuildContext context, int index, Animation<double> animation) {
      return const Placeholder();
    },
    gridDelegate: const SliverGridDelegateWithMaxCrossAxisExtent(maxCrossAxisExtent: 100.0),
  );
}

// ...

void _updateGrid() {
  // adds "123" to the AnimatedGrid
  gridKey.currentState!.insertItem(123);
}
```

[AnimatedGrid] item input handlers can also refer to their [AnimatedGridState] with the static [AnimatedGrid.of] method.

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedItemBuilder

```dart
typedef AnimatedItemBuilder = Widget Function(BuildContext context, int index, Animation<double> animation)
```

Signature for the builder callback used by [AnimatedList], [AnimatedList.separated] & [AnimatedGrid] to build their animated children.

This signature is also used by [AnimatedList.separated] to build its separators and to animate their exit transition after their corresponding item has been removed.

The [context] argument is the build context where the widget will be created, the [index] is the index of the item to be built, and the [animation] is an [Animation] that should be used to animate an entry transition for the widget that is built.

For [AnimatedList.separated], the [index] is the index of the corresponding item of the separator that is built or removed. For [AnimatedList.separated] `removedSeparatorBuilder`, the [animation] should be used to animate an exit transition for the widget that is built.

See also:

- [AnimatedRemovedItemBuilder], a builder that is for removing items with animations instead of adding them.

# AnimatedRemovedItemBuilder

```dart
typedef AnimatedRemovedItemBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

Signature for the builder callback used in [AnimatedListState.removeItem] and [AnimatedGridState.removeItem] to animate their children after they have been removed.

The [context] argument is the build context where the widget will be created, and the [animation] is an [Animation] that should be used to animate an exit transition for the widget that is built.

See also:

- [AnimatedItemBuilder], a builder that is for adding items with animations instead of removing them.

# SliverAnimatedList

```dart
class SliverAnimatedList extends _SliverAnimatedMultiBoxAdaptor {}
```

A [SliverList] that animates items when they are inserted or removed.

This widget's [SliverAnimatedListState] can be used to dynamically insert or remove items. To refer to the [SliverAnimatedListState] either provide a [GlobalKey] or use the static [SliverAnimatedList.of] method from a list item's input callback.

{@tool dartpad} This sample application uses a [SliverAnimatedList] to create an animated effect when items are removed or added to the list.

** See code in examples/api/lib/widgets/animated_list/sliver_animated_list.0.dart ** {@end-tool}

See also:

- [SliverList], which does not animate items when they are inserted or removed.
- [AnimatedList], a non-sliver scrolling container that animates items when they are inserted or removed.
- [SliverAnimatedGrid], a sliver which animates items when they are inserted into or removed from a grid.
- [AnimatedGrid], a non-sliver scrolling container that animates items when they are inserted into or removed from a grid.

### SliverAnimatedList()

```dart
SliverAnimatedList({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, int? Function(InvalidType)? findChildIndexCallback, int initialItemCount = 0})
```

Creates a [SliverList] that animates items when they are inserted or removed.

### createState()

```dart
SliverAnimatedListState createState()
```

### of()

```dart
SliverAnimatedListState of(BuildContext context)
```

The [SliverAnimatedListState] from the closest instance of this class that encloses the given context.

This method is typically used by [SliverAnimatedList] item widgets that insert or remove items in response to user input.

If no [SliverAnimatedList] surrounds the context given, then this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [maybeOf], a similar function that will return null if no [SliverAnimatedList] ancestor is found.

### maybeOf()

```dart
SliverAnimatedListState? maybeOf(BuildContext context)
```

The [SliverAnimatedListState] from the closest instance of this class that encloses the given context.

This method is typically used by [SliverAnimatedList] item widgets that insert or remove items in response to user input.

If no [SliverAnimatedList] surrounds the context given, then this function will return null.

This method can be expensive (it walks the element tree).

This method does not create a dependency, and so will not cause rebuilding when the state changes.

See also:

- [of], a similar function that will throw if no [SliverAnimatedList] ancestor is found.

# SliverAnimatedListState

```dart
class SliverAnimatedListState extends _SliverAnimatedMultiBoxAdaptorState<SliverAnimatedList> {}
```

The state for a [SliverAnimatedList] that animates items when they are inserted or removed.

When an item is inserted with [insertItem] an animation begins running. The animation is passed to [SliverAnimatedList.itemBuilder] whenever the item's widget is needed.

When an item is removed with [removeItem] its animation is reversed. The removed item's animation is passed to the [removeItem] builder parameter.

An app that needs to insert or remove items in response to an event can refer to the [SliverAnimatedList]'s state with a global key:

```dart
// (e.g. in a stateful widget)
GlobalKey<AnimatedListState> listKey = GlobalKey<AnimatedListState>();

// ...

@override
Widget build(BuildContext context) {
  return AnimatedList(
    key: listKey,
    itemBuilder: (BuildContext context, int index, Animation<double> animation) {
      return const Placeholder();
    },
  );
}

// ...

void _updateList() {
  // adds "123" to the AnimatedList
  listKey.currentState!.insertItem(123);
}
```

[SliverAnimatedList] item input handlers can also refer to their [SliverAnimatedListState] with the static [SliverAnimatedList.of] method.

### build()

```dart
Widget build(BuildContext context)
```

# SliverAnimatedGrid

```dart
class SliverAnimatedGrid extends _SliverAnimatedMultiBoxAdaptor {}
```

A [SliverGrid] that animates items when they are inserted or removed.

This widget's [SliverAnimatedGridState] can be used to dynamically insert or remove items. To refer to the [SliverAnimatedGridState] either provide a [GlobalKey] or use the static [SliverAnimatedGrid.of] method from an item's input callback.

{@tool dartpad} This sample application uses a [SliverAnimatedGrid] to create an animated effect when items are removed or added to the grid.

** See code in examples/api/lib/widgets/animated_grid/sliver_animated_grid.0.dart ** {@end-tool}

See also:

- [AnimatedGrid], a non-sliver scrolling container that animates items when they are inserted into or removed from a grid.
- [SliverGrid], which does not animate items when they are inserted or removed from a grid.
- [SliverList], which displays a non-animated list of items.
- [SliverAnimatedList], which animates items added and removed from a list instead of a grid.

### SliverAnimatedGrid()

```dart
SliverAnimatedGrid({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, required SliverGridDelegate gridDelegate, int? Function(InvalidType)? findChildIndexCallback, int initialItemCount = 0})
```

Creates a [SliverGrid] that animates items when they are inserted or removed.

### createState()

```dart
SliverAnimatedGridState createState()
```

### gridDelegate

```dart
SliverGridDelegate gridDelegate
```

{@macro flutter.widgets.AnimatedGrid.gridDelegate}

### of()

```dart
SliverAnimatedGridState of(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [SliverAnimatedGrid] item widgets that insert or remove items in response to user input.

If no [SliverAnimatedGrid] surrounds the context given, then this function will assert in debug mode and throw an exception in release mode.

This method can be expensive (it walks the element tree).

See also:

- [maybeOf], a similar function that will return null if no [SliverAnimatedGrid] ancestor is found.

### maybeOf()

```dart
SliverAnimatedGridState? maybeOf(BuildContext context)
```

The state from the closest instance of this class that encloses the given context.

This method is typically used by [SliverAnimatedGrid] item widgets that insert or remove items in response to user input.

If no [SliverAnimatedGrid] surrounds the context given, then this function will return null.

This method can be expensive (it walks the element tree).

See also:

- [of], a similar function that will throw if no [SliverAnimatedGrid] ancestor is found.

# SliverAnimatedGridState

```dart
class SliverAnimatedGridState extends _SliverAnimatedMultiBoxAdaptorState<SliverAnimatedGrid> {}
```

The state for a [SliverAnimatedGrid] that animates items when they are inserted or removed.

When an item is inserted with [insertItem] an animation begins running. The animation is passed to [SliverAnimatedGrid.itemBuilder] whenever the item's widget is needed.

When an item is removed with [removeItem] its animation is reversed. The removed item's animation is passed to the [removeItem] builder parameter.

An app that needs to insert or remove items in response to an event can refer to the [SliverAnimatedGrid]'s state with a global key:

```dart
// (e.g. in a stateful widget)
GlobalKey<AnimatedGridState> gridKey = GlobalKey<AnimatedGridState>();

// ...

@override
Widget build(BuildContext context) {
  return AnimatedGrid(
    key: gridKey,
    itemBuilder: (BuildContext context, int index, Animation<double> animation) {
      return const Placeholder();
    },
    gridDelegate: const SliverGridDelegateWithMaxCrossAxisExtent(maxCrossAxisExtent: 100.0),
  );
}

// ...

void _updateGrid() {
  // adds "123" to the AnimatedGrid
  gridKey.currentState!.insertItem(123);
}
```

[SliverAnimatedGrid] item input handlers can also refer to their [SliverAnimatedGridState] with the static [SliverAnimatedGrid.of] method.

### build()

```dart
Widget build(BuildContext context)
```
