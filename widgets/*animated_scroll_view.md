@docImport 'page_storage.dart'; @docImport 'primary_scroll_controller.dart';

# AnimatedList

```dart
class AnimatedList extends _AnimatedScrollView {}
```

一个可滚动容器，在插入或移除条目时会对其进行动画处理。

此组件的 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate) 可用于动态插入或移除条目。若要引用 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate)，可以提供一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，或在条目的输入回调中使用静态方法 [of]。

{@youtube 560 315 https://www.youtube.com/watch?v=ZtfItHwFlZ8}

{@tool dartpad} 此示例应用程序使用 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，在条目从列表中移除或添加到列表时创建动画效果。

** 代码参见 examples/api/lib/widgets/animated_list/animated_list.0.dart ** {@end-tool}

默认情况下，[AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 会根据 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 指示的内边距自动为列表可滚动区域的边界添加内边距，以避免部分遮挡。若要避免此行为，可将 [padding] 属性重写为零。

{@tool snippet} 以下示例演示了如何使用 [MediaQuery.removePadding] 重写默认的顶部和底部内边距。

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

另请参阅：

- [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，在条目从列表中插入或移除时对其进行动画处理的 sliver。
- [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，在条目从网格中插入或移除时对其进行动画处理的 sliver。
- [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，一个非 sliver 的可滚动容器，在条目插入或移除网格时对其进行动画处理。

### AnimatedList()

```dart
AnimatedList({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, bool shrinkWrap = false, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

创建一个可滚动容器，在条目插入或移除时对其进行动画处理。

### AnimatedList.separated()

```dart
AnimatedList.separated({dynamic key, required AnimatedItemBuilder itemBuilder, required AnimatedItemBuilder separatorBuilder, required Widget Function(BuildContext, int, InvalidType) removedSeparatorBuilder, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, bool shrinkWrap = false, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

一个可滚动容器，在条目插入或移除时对条目及其分隔符进行动画处理。

此组件的 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate) 可用于动态插入或移除条目。若要引用 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate)，可以提供一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，或在条目的输入回调中使用静态方法 [of]。

此组件与由 [ListView.separated] 创建的组件类似。

{@tool dartpad} 此示例应用程序使用 [AnimatedList.separated]，在条目从列表中移除或添加到列表时创建动画效果。

** 代码参见 examples/api/lib/widgets/animated_list/animated_list_separated.0.dart ** {@end-tool}

默认情况下，[AnimatedList.separated] 会根据 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 指示的内边距自动为列表可滚动区域的边界添加内边距，以避免部分遮挡。若要避免此行为，可将 [padding] 属性重写为零。

{@tool snippet} 以下示例演示了如何使用 [MediaQuery.removePadding] 重写默认的顶部和底部内边距。

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

另请参阅：

- [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，在条目从列表中插入或移除时对其进行动画处理的 sliver。
- [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，在条目从网格中插入或移除时对其进行动画处理的 sliver。
- [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，一个非 sliver 的可滚动容器，在条目插入或移除网格时对其进行动画处理。
- [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，对添加到列表（而非网格）或从列表中移除的条目进行动画处理。

### of()

```dart
AnimatedListState of(BuildContext context)
```

包含给定 context 的最近一个此类实例的 state。

此方法通常由 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，则此函数在调试模式下会触发断言，在发布模式下会抛出异常。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [maybeOf]，一个类似的函数，如果找不到 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 祖先，则返回 null。

### maybeOf()

```dart
AnimatedListState? maybeOf(BuildContext context)
```

包含给定 context 的最近一个 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 实例的 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate)。

此方法通常由 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，则此函数将返回 null。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [of]，一个类似的函数，如果找不到 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 祖先，则会抛出异常。

### createState()

```dart
AnimatedListState createState()
```

# AnimatedListState

```dart
class AnimatedListState extends _AnimatedScrollViewState<AnimatedList> {}
```

[AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 的 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate)，[AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 是一个可滚动列表容器，在条目插入或移除时对其进行动画处理。

当使用 [insertItem] 插入一个条目时，会开始运行一个动画。每当需要该条目的组件时，该动画都会被传递给 [AnimatedList.itemBuilder]。

当使用 [insertAllItems] 插入多个条目时，会开始运行一个动画。每当需要条目的组件时，该动画都会被传递给 [AnimatedList.itemBuilder]。

如果使用 [AnimatedList.separated]，每当需要分隔符的组件时，该动画也会被传递给 `AnimatedList.separatorBuilder`。

当使用 [removeItem] 移除一个条目时，其动画会反向播放。被移除条目的动画会被传递给 [removeItem] 的 builder 参数。如果使用 [AnimatedList.separated]，对应分隔符的动画也会被传递给 [AnimatedList.removedSeparatorBuilder] 参数。

需要响应某个事件来插入或移除条目的应用，可以通过全局键（global key）引用 [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 的 state：

```dart
// （例如在有状态组件中）
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
  // 将 "123" 添加到 AnimatedList 中
  listKey.currentState!.insertItem(123);
}
```

[AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist) 条目的输入处理程序也可以使用静态方法 [AnimatedList.of] 来引用其 [AnimatedListState](https://www.yuque.com/thyname/flutter.widgets/animatedliststate)。

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedGrid

```dart
class AnimatedGrid extends _AnimatedScrollView {}
```

一个可滚动容器，在条目插入网格或从网格中移除时对其进行动画处理。

此组件的 [AnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/animatedgridstate) 可用于动态插入或移除条目。若要引用 [AnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/animatedgridstate)，可以提供一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，或在条目的输入回调中使用静态方法 [of]。

此组件与由 [GridView.builder] 创建的组件类似。

{@tool dartpad} 此示例应用程序使用 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，在条目从网格中移除或添加到网格时创建动画效果。

** 代码参见 examples/api/lib/widgets/animated_grid/animated_grid.0.dart ** {@end-tool}

默认情况下，[AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 会根据 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 指示的内边距自动为网格可滚动区域的边界添加内边距，以避免部分遮挡。若要避免此行为，可将 [padding] 属性重写为零。

{@tool snippet} 以下示例演示了如何使用 [MediaQuery.removePadding] 重写默认的顶部和底部内边距。

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

另请参阅：

- [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，在条目插入网格或从网格中移除时对其进行动画处理的 sliver。
- [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，对添加到列表（而非网格）或从列表中移除的条目进行动画处理的 sliver。
- [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，对添加到列表（而非网格）或从列表中移除的条目进行动画处理。

### AnimatedGrid()

```dart
AnimatedGrid({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, required SliverGridDelegate gridDelegate, int initialItemCount = 0, dynamic scrollDirection = Axis.vertical, bool reverse = false, ScrollController? controller, bool? primary, ScrollPhysics? physics, dynamic padding, dynamic clipBehavior = Clip.hardEdge, dynamic scrollCacheExtent})
```

创建一个可滚动容器，在条目插入或移除时对其进行动画处理。

### gridDelegate

```dart
SliverGridDelegate gridDelegate
```

{@template flutter.widgets.AnimatedGrid.gridDelegate} 一个用于控制 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 内子组件布局的委托（delegate）。

另请参阅：

- [SliverGridDelegateWithFixedCrossAxisCount](https://www.yuque.com/thyname/flutter.rendering/slivergriddelegatewithfixedcrossaxiscount)，创建在交叉轴上具有固定数量图块的布局。
- [SliverGridDelegateWithMaxCrossAxisExtent](https://www.yuque.com/thyname/flutter.rendering/slivergriddelegatewithmaxcrossaxisextent)，创建具有最大交叉轴范围的图块布局。{@endtemplate}

### of()

```dart
AnimatedGridState of(BuildContext context)
```

包含给定 context 的最近一个此类实例的 state。

此方法通常由 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，则此函数在调试模式下会触发断言，在发布模式下会抛出异常。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [maybeOf]，一个类似的函数，如果找不到 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 祖先，则返回 null。

### maybeOf()

```dart
AnimatedGridState? maybeOf(BuildContext context)
```

包含给定 context 的最近一个此类实例的 state。

此方法通常由 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，则此函数将返回 null。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [of]，一个类似的函数，如果找不到 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 祖先，则会抛出异常。

### createState()

```dart
AnimatedGridState createState()
```

# AnimatedGridState

```dart
class AnimatedGridState extends _AnimatedScrollViewState<AnimatedGrid> {}
```

[AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 的 [State](https://www.yuque.com/thyname/flutter.widgets/state)，在条目插入或移除时对其进行动画处理。

当使用 [insertItem] 插入一个条目时，会开始运行一个动画。每当需要该条目的组件时，该动画都会被传递给 [AnimatedGrid.itemBuilder]。

当使用 [removeItem] 移除一个条目时，其动画会反向播放。被移除条目的动画会被传递给 [removeItem] 的 builder 参数。

需要响应某个事件来插入或移除条目的应用，可以通过全局键（global key）引用 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 的 state：

```dart
// （例如在有状态组件中）
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
  // 将 "123" 添加到 AnimatedGrid 中
  gridKey.currentState!.insertItem(123);
}
```

[AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 条目的输入处理程序也可以使用静态方法 [AnimatedGrid.of] 来引用其 [AnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/animatedgridstate)。

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedItemBuilder

```dart
typedef AnimatedItemBuilder = Widget Function(BuildContext context, int index, Animation<double> animation)
```

[AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)、[AnimatedList.separated] 和 [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid) 用于构建其动画子组件的 builder 回调的签名。

此签名也被 [AnimatedList.separated] 用于构建其分隔符，并在对应条目被移除后为分隔符的退出过渡设置动画。

[context] 参数是将要创建组件的 build context，[index] 是待构建条目的索引，[animation](https://www.yuque.com/thyname/flutter.animation) 是一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，应使用它为所构建组件的进入过渡设置动画。

对于 [AnimatedList.separated]，[index] 是被构建或移除的分隔符所对应条目的索引。对于 [AnimatedList.separated] 的 `removedSeparatorBuilder`，应使用 [animation](https://www.yuque.com/thyname/flutter.animation) 为所构建组件的退出过渡设置动画。

另请参阅：

- [AnimatedRemovedItemBuilder](https://www.yuque.com/thyname/flutter.widgets/animatedremoveditembuilder)，一个用于以动画方式移除（而非添加）条目的 builder。

# AnimatedRemovedItemBuilder

```dart
typedef AnimatedRemovedItemBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

[AnimatedListState.removeItem] 和 [AnimatedGridState.removeItem] 中用于为已移除子组件设置动画的 builder 回调的签名。

[context] 参数是将要创建组件的 build context，[animation](https://www.yuque.com/thyname/flutter.animation) 是一个 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)，应使用它为所构建组件的退出过渡设置动画。

另请参阅：

- [AnimatedItemBuilder](https://www.yuque.com/thyname/flutter.widgets/animateditembuilder)，一个用于以动画方式添加（而非移除）条目的 builder。

# SliverAnimatedList

```dart
class SliverAnimatedList extends _SliverAnimatedMultiBoxAdaptor {}
```

一个 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)，在条目插入或移除时对其进行动画处理。

此组件的 [SliverAnimatedListState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedliststate) 可用于动态插入或移除条目。若要引用 [SliverAnimatedListState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedliststate)，可以提供一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，或在列表条目的输入回调中使用静态方法 [SliverAnimatedList.of]。

{@tool dartpad} 此示例应用程序使用 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，在条目从列表中移除或添加到列表时创建动画效果。

** 代码参见 examples/api/lib/widgets/animated_list/sliver_animated_list.0.dart ** {@end-tool}

另请参阅：

- [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)，在条目插入或移除时不对其进行动画处理。
- [AnimatedList](https://www.yuque.com/thyname/flutter.widgets/animatedlist)，一个非 sliver 的可滚动容器，在条目插入或移除时对其进行动画处理。
- [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，在条目插入网格或从网格中移除时对其进行动画处理的 sliver。
- [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，一个非 sliver 的可滚动容器，在条目插入网格或从网格中移除时对其进行动画处理。

### SliverAnimatedList()

```dart
SliverAnimatedList({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, int? Function(InvalidType)? findChildIndexCallback, int initialItemCount = 0})
```

创建一个 [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)，在条目插入或移除时对其进行动画处理。

### createState()

```dart
SliverAnimatedListState createState()
```

### of()

```dart
SliverAnimatedListState of(BuildContext context)
```

包含给定 context 的最近一个此类实例的 [SliverAnimatedListState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedliststate)。

此方法通常由 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，则此函数在调试模式下会触发断言，在发布模式下会抛出异常。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [maybeOf]，一个类似的函数，如果找不到 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 祖先，则返回 null。

### maybeOf()

```dart
SliverAnimatedListState? maybeOf(BuildContext context)
```

包含给定 context 的最近一个此类实例的 [SliverAnimatedListState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedliststate)。

此方法通常由 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，则此函数将返回 null。

此方法可能开销较大（它会遍历 element 树）。

此方法不会创建依赖关系，因此当 state 发生变化时不会触发重建。

另请参阅：

- [of]，一个类似的函数，如果找不到 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 祖先，则会抛出异常。

# SliverAnimatedListState

```dart
class SliverAnimatedListState extends _SliverAnimatedMultiBoxAdaptorState<SliverAnimatedList> {}
```

[SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 的 state，在条目插入或移除时对其进行动画处理。

当使用 [insertItem] 插入一个条目时，会开始运行一个动画。每当需要该条目的组件时，该动画都会被传递给 [SliverAnimatedList.itemBuilder]。

当使用 [removeItem] 移除一个条目时，其动画会反向播放。被移除条目的动画会被传递给 [removeItem] 的 builder 参数。

需要响应某个事件来插入或移除条目的应用，可以通过全局键（global key）引用 [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 的 state：

```dart
// （例如在有状态组件中）
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
  // 将 "123" 添加到 AnimatedList 中
  listKey.currentState!.insertItem(123);
}
```

[SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist) 条目的输入处理程序也可以使用静态方法 [SliverAnimatedList.of] 来引用其 [SliverAnimatedListState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedliststate)。

### build()

```dart
Widget build(BuildContext context)
```

# SliverAnimatedGrid

```dart
class SliverAnimatedGrid extends _SliverAnimatedMultiBoxAdaptor {}
```

一个 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)，在条目插入或移除时对其进行动画处理。

此组件的 [SliverAnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgridstate) 可用于动态插入或移除条目。若要引用 [SliverAnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgridstate)，可以提供一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，或在条目的输入回调中使用静态方法 [SliverAnimatedGrid.of]。

{@tool dartpad} 此示例应用程序使用 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，在条目从网格中移除或添加到网格时创建动画效果。

** 代码参见 examples/api/lib/widgets/animated_grid/sliver_animated_grid.0.dart ** {@end-tool}

另请参阅：

- [AnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/animatedgrid)，一个非 sliver 的可滚动容器，在条目插入网格或从网格中移除时对其进行动画处理。
- [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)，在条目插入网格或从网格中移除时不对其进行动画处理。
- [SliverList](https://www.yuque.com/thyname/flutter.widgets/sliverlist)，显示一个未经动画处理的条目列表。
- [SliverAnimatedList](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedlist)，对添加到列表（而非网格）或从列表中移除的条目进行动画处理。

### SliverAnimatedGrid()

```dart
SliverAnimatedGrid({dynamic key, required Widget Function(BuildContext, int, InvalidType) itemBuilder, required SliverGridDelegate gridDelegate, int? Function(InvalidType)? findChildIndexCallback, int initialItemCount = 0})
```

创建一个 [SliverGrid](https://www.yuque.com/thyname/flutter.widgets/slivergrid)，在条目插入或移除时对其进行动画处理。

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

包含给定 context 的最近一个此类实例的 state。

此方法通常由 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，则此函数在调试模式下会触发断言，在发布模式下会抛出异常。

此方法可能开销较大（它会遍历 element 树）。

另请参阅：

- [maybeOf]，一个类似的函数，如果找不到 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 祖先，则返回 null。

### maybeOf()

```dart
SliverAnimatedGridState? maybeOf(BuildContext context)
```

包含给定 context 的最近一个此类实例的 state。

此方法通常由 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 的条目组件使用，用于响应用户输入而插入或移除条目。

如果给定的 context 周围没有 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid)，则此函数将返回 null。

此方法可能开销较大（它会遍历 element 树）。

另请参阅：

- [of]，一个类似的函数，如果找不到 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 祖先，则会抛出异常。

# SliverAnimatedGridState

```dart
class SliverAnimatedGridState extends _SliverAnimatedMultiBoxAdaptorState<SliverAnimatedGrid> {}
```

[SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 的 state，在条目插入或移除时对其进行动画处理。

当使用 [insertItem] 插入一个条目时，会开始运行一个动画。每当需要该条目的组件时，该动画都会被传递给 [SliverAnimatedGrid.itemBuilder]。

当使用 [removeItem] 移除一个条目时，其动画会反向播放。被移除条目的动画会被传递给 [removeItem] 的 builder 参数。

需要响应某个事件来插入或移除条目的应用，可以通过全局键（global key）引用 [SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 的 state：

```dart
// （例如在有状态组件中）
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
  // 将 "123" 添加到 AnimatedGrid 中
  gridKey.currentState!.insertItem(123);
}
```

[SliverAnimatedGrid](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgrid) 条目的输入处理程序也可以使用静态方法 [SliverAnimatedGrid.of] 来引用其 [SliverAnimatedGridState](https://www.yuque.com/thyname/flutter.widgets/sliveranimatedgridstate)。

### build()

```dart
Widget build(BuildContext context)
```
