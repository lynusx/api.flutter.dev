@docImport 'package:flutter/material.dart';

@docImport 'single_child_scroll_view.dart'; @docImport 'text.dart';

# PageController

```dart
class PageController extends ScrollController {}
```

[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 的控制器。

页面控制器（page controller）可让你控制 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中显示哪一页。除了可以控制 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 内部内容的像素偏移量外，[PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 还允许你以"页"为单位控制偏移量，一页即为视口大小的一个增量。

另请参阅：

- [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview)，此对象所控制的组件。

{@tool snippet}

此组件使用默认构造函数引入了一个包含两页的 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)、[Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 和 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview)。两个页面中均包含一个 [ElevatedButton](https://www.yuque.com/thyname/flutter.material/elevatedbutton)，用于借助 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 让 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 播放动画切换。

```dart
class MyPageView extends StatefulWidget {
  const MyPageView({super.key});

  @override
  State<MyPageView> createState() => _MyPageViewState();
}

class _MyPageViewState extends State<MyPageView> {
  final PageController _pageController = PageController();

  @override
  void dispose() {
    _pageController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: PageView(
          controller: _pageController,
          children: <Widget>[
            ColoredBox(
              color: Colors.red,
              child: Center(
                child: ElevatedButton(
                  onPressed: () {
                    if (_pageController.hasClients) {
                      _pageController.animateToPage(
                        1,
                        duration: const Duration(milliseconds: 400),
                        curve: Curves.easeInOut,
                      );
                    }
                  },
                  child: const Text('Next'),
                ),
              ),
            ),
            ColoredBox(
              color: Colors.blue,
              child: Center(
                child: ElevatedButton(
                  onPressed: () {
                    if (_pageController.hasClients) {
                      _pageController.animateToPage(
                        0,
                        duration: const Duration(milliseconds: 400),
                        curve: Curves.easeInOut,
                      );
                    }
                  },
                  child: const Text('Previous'),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

{@end-tool}

### PageController()

```dart
PageController({int initialPage = 0, bool keepPage = true, double viewportFraction = 1.0, void Function(ScrollPosition)? onAttach, void Function(ScrollPosition)? onDetach})
```

创建一个页面控制器。

### initialPage

```dart
int initialPage
```

首次创建 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 时要显示的页面。

### keepPage

```dart
bool keepPage
```

将当前 [page] 保存到 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 中，并在此控制器所控制的可滚动组件被重新创建时恢复该状态。

如果此属性设为 false，则当前 [page] 永远不会被保存，且始终使用 [initialPage] 来初始化滚动偏移量。如果为 true（默认值），首次创建此控制器所控制的可滚动组件时会使用 initialPage，因为此时还没有可恢复的页面。此后，会恢复已保存的页面，并忽略 [initialPage]。

另请参阅：

- [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，当同一路由中出现多个可滚动组件时应使用它，以区分不同组件所使用的 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 保存位置。

### viewportFraction

```dart
double viewportFraction
```

{@template flutter.widgets.pageview.viewportFraction} 每个页面应占据的视口比例。

默认为 1.0，即每个页面在滚动方向上填满整个视口。 {@endtemplate}

### page

```dart
double? get page
```

所控制的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中当前显示的页面。

在以下情况下，此 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 无法获知当前页面。读取 [page] 会在以下情况下抛出 [AssertionError](https://www.yuque.com/thyname/dart.core/assertionerror)：

1.  当前没有 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 正在使用此 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller)。一旦有 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 开始使用此 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller)，新的 [page] 位置会按以下方式推导：

- 首先，根据所附加的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，以及若 [keepPage] 为 true 时该 context 的 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 中保存的位置来确定。
- 其次，根据 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 的 [initialPage] 来确定。

2.  有多个 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 在使用同一个 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller)。

可以使用 [hasClients] 属性来检查访问 [page] 之前是否已附加了 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview)。

### animateToPage()

```dart
Future<void> animateToPage(int page, {required Duration duration, required Curve curve})
```

将所控制的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 从当前页面动画切换到给定页面。

动画持续时间为给定的 duration，并遵循给定的 curve 曲线。动画完成后，返回的 [Future](https://www.yuque.com/thyname/dart.async/future) 会 resolve。

### jumpToPage()

```dart
void jumpToPage(int page)
```

更改所控制的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中显示的页面。

将页面位置从当前值直接跳转到给定值，不带动画，也不检查新值是否在有效范围内。

### nextPage()

```dart
Future<void> nextPage({required Duration duration, required Curve curve})
```

将所控制的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 动画切换到下一页。

动画持续时间为给定的 duration，并遵循给定的 curve 曲线。动画完成后，返回的 [Future](https://www.yuque.com/thyname/dart.async/future) 会 resolve。

### previousPage()

```dart
Future<void> previousPage({required Duration duration, required Curve curve})
```

将所控制的 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 动画切换到上一页。

动画持续时间为给定的 duration，并遵循给定的 curve 曲线。动画完成后，返回的 [Future](https://www.yuque.com/thyname/dart.async/future) 会 resolve。

### createScrollPosition()

```dart
ScrollPosition createScrollPosition(ScrollPhysics physics, ScrollContext context, ScrollPosition? oldPosition)
```

### attach()

```dart
void attach(ScrollPosition position)
```

# PageMetrics

```dart
class PageMetrics extends FixedScrollMetrics {}
```

[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 的度量信息。

这些度量信息可在由 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 生成的 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 上获取。

### PageMetrics()

```dart
PageMetrics({required double? minScrollExtent, required double? maxScrollExtent, required double? pixels, required double? viewportDimension, required dynamic axisDirection, required double viewportFraction, required double devicePixelRatio})
```

创建与 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 相关联的值的一份不可变快照。

### copyWith()

```dart
PageMetrics copyWith({double? minScrollExtent, double? maxScrollExtent, double? pixels, double? viewportDimension, AxisDirection? axisDirection, double? viewportFraction, double? devicePixelRatio})
```

### page

```dart
double? get page
```

[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中当前显示的页面。

### viewportFraction

```dart
double viewportFraction
```

每个页面所占据的视口比例。

用于根据当前的 [pixels] 计算出 [page]。

# PageScrollPhysics

```dart
class PageScrollPhysics extends ScrollPhysics {}
```

[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 所使用的滚动物理效果。

此物理效果会使页面视图吸附（snap）到页面边界。

另请参阅：

- [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics)，定义滚动物理效果 API 的基类。
- [PageView.physics]，可用于覆盖页面视图所使用的物理效果。

### PageScrollPhysics()

```dart
PageScrollPhysics({ScrollPhysics? parent})
```

为 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 创建物理效果。

### applyTo()

```dart
PageScrollPhysics applyTo(ScrollPhysics? ancestor)
```

### createBallisticSimulation()

```dart
Simulation? createBallisticSimulation(ScrollMetrics position, double velocity)
```

### allowImplicitScrolling

```dart
bool get allowImplicitScrolling
```

# PageView

```dart
class PageView extends StatefulWidget {}
```

一种按页滚动的可滚动列表。

PageView 的每个子组件都会被强制设为与视口相同的大小。

你可以使用 [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 来控制 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中显示哪一页。除了可以控制 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 内部内容的像素偏移量外，[PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 还允许你以"页"为单位控制偏移量，一页即为视口大小的一个增量。

[PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller) 还可用于控制 [PageController.initialPage]（决定首次构建 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 时显示哪一页），以及 [PageController.viewportFraction]（决定各页面大小占视口大小的比例）。

{@youtube 560 315 https://www.youtube.com/watch?v=J1gE9xvph-A}

{@tool dartpad} 这是一个 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 的示例。它会在三个页面中分别创建一个居中的 [Text](https://www.yuque.com/thyname/flutter.widgets/text)，这些页面可以水平滚动切换。

** See code in examples/api/lib/widgets/page_view/page_view.0.dart ** {@end-tool}

## 在会话期间保持滚动位置

滚动视图会尝试使用 [PageStorage](https://www.yuque.com/thyname/flutter.widgets/pagestorage) 来保持其滚动位置。对于 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview)，可以通过将 [PageController.keepPage] 设为 false 来禁用此行为。如果启用了此功能，建议为此组件的 [key] 使用 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey)，以便区分不同的滚动视图。

另请参阅：

- [PageController](https://www.yuque.com/thyname/flutter.widgets/pagecontroller)，控制视图中显示哪一页。
- [SingleChildScrollView](https://www.yuque.com/thyname/flutter.widgets/singlechildscrollview)，当你需要让单个子组件可滚动时使用。
- [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)，用于显示可滚动的盒状列表。
- [GridView](https://www.yuque.com/thyname/flutter.widgets/gridview)，用于显示可滚动的盒状网格。
- [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 和 [NotificationListener](https://www.yuque.com/thyname/flutter.widgets/notificationlistener)，可用于在不使用 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller) 的情况下监视滚动位置。

### PageView()

```dart
PageView({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, List<Widget> children = const <Widget>[], DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

根据一份显式的 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget) [List](https://www.yuque.com/thyname/dart.core/list) 创建一个按页滚动的可滚动列表。

此构造函数适用于子组件数量较少的页面视图，因为构造该 [List](https://www.yuque.com/thyname/dart.core/list) 需要为每一个可能显示的子组件执行相应的工作。

与框架中的其他组件一样，此组件要求传入的 [children] 列表在传入之后不会被修改。更多细节请参阅 [SliverChildListDelegate.children] 的文档。

{@template flutter.widgets.PageView.allowImplicitScrolling} 如果 [allowImplicitScrolling] 为 true，[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 在无障碍滚动方面的表现将更接近 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview)：隐式滚动操作会移动到下一页，而不是进入当前页面的内容内部。 {@endtemplate}

### PageView.builder()

```dart
PageView.builder({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, required NullableIndexedWidgetBuilder itemBuilder, ChildIndexGetter? findChildIndexCallback, int? itemCount, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

使用按需创建的组件，创建一个按页滚动的可滚动列表。

此构造函数适用于子组件数量较多（甚至无限）的页面视图，因为 builder 只会针对实际可见的子组件被调用。

提供非空的 [itemCount] 可以让 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 计算出最大滚动范围。

[itemBuilder] 只会以大于或等于零，且小于 [itemCount] 的索引被调用。

{@macro flutter.widgets.ListView.builder.itemBuilder}

{@template flutter.widgets.PageView.findChildIndexCallback} [findChildIndexCallback] 对应 [SliverChildBuilderDelegate.findChildIndexCallback] 属性。如果为 null，当子组件构建器返回的子组件顺序发生变化时，子组件可能无法映射到其原有的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，这可能导致状态丢失。如果子组件的顺序之后可能会发生变化，则需要实现此回调。 {@endtemplate}

{@macro flutter.widgets.PageView.allowImplicitScrolling}

### PageView.custom()

```dart
PageView.custom({dynamic key, Axis scrollDirection = Axis.horizontal, bool reverse = false, PageController? controller, ScrollPhysics? physics, bool pageSnapping = true, ValueChanged<int>? onPageChanged, required SliverChildDelegate childrenDelegate, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool allowImplicitScrolling = false, ScrollCacheExtent? scrollCacheExtent, String? restorationId, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, ScrollBehavior? scrollBehavior, bool padEnds = true})
```

使用自定义的子组件模型，创建一个按页滚动的可滚动列表。

{@tool dartpad} 此示例展示了一个 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview)，它使用自定义的 [SliverChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/sliverchildbuilderdelegate) 来支持子组件重新排序。

** See code in examples/api/lib/widgets/page_view/page_view.1.dart ** {@end-tool}

{@macro flutter.widgets.PageView.allowImplicitScrolling}

### allowImplicitScrolling

```dart
bool allowImplicitScrolling
```

{@template flutter.widgets.PageView.allowImplicitScrolling} 控制该组件的页面是否响应 [RenderObject.showOnScreen]，从而支持隐式的无障碍滚动。

当此标志设为 false 时，当无障碍焦点到达当前页面末尾，用户尝试将焦点移动到下一个元素时，焦点会转移到页面视图外部的下一个组件。

当此标志设为 true 时，当无障碍焦点到达当前页面末尾，用户尝试将焦点移动到下一个元素时，焦点会转移到页面视图中的下一页。 {@endtemplate}

### scrollCacheExtent

```dart
ScrollCacheExtent scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

在 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 中，默认的 [scrollCacheExtent] 使用 [ScrollCacheExtent.viewport]，该值表示在可见区域之外要缓存的视口长度数量。

当 [PageController.viewportFraction] 为 1.0（默认值）时，此值等同于要缓存的页面数量。例如，`ScrollCacheExtent.viewport(2.0)` 会在可见页面的前后各缓存 2 页。

当 [PageController.viewportFraction] 小于 1.0 时，单个视口内可能会同时显示多个页面，因此 `ScrollCacheExtent.viewport(1.0)` 在每个方向上缓存的页面数可能会超过一页。

也可以使用 [ScrollCacheExtent.pixels] 以逻辑像素而非视口大小来指定缓存范围。

如果指定了 [scrollCacheExtent]，其值必须与 [allowImplicitScrolling] 保持一致：当 [allowImplicitScrolling] 为 true 时，该值必须大于 0.0；当 [allowImplicitScrolling] 为 false 时，该值必须为 0.0。

如果 [allowImplicitScrolling] 为 true，默认为 `ScrollCacheExtent.viewport(1.0)`；如果为 false，默认为 `ScrollCacheExtent.viewport(0.0)`。

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

### scrollDirection

```dart
Axis scrollDirection
```

滚动视图偏移量随每一页递增所沿的 [Axis](https://www.yuque.com/thyname/flutter.painting/axis)（轴）。

有关正在进行的主动滚动方向，请参阅 [ScrollDirection](https://www.yuque.com/thyname/flutter.rendering/scrolldirection)。

默认为 [Axis.horizontal]。

### reverse

```dart
bool reverse
```

页面视图是否沿阅读方向滚动。

例如，如果阅读方向为从左到右，且 [scrollDirection] 为 [Axis.horizontal]，那么当 [reverse] 为 false 时，页面视图从左向右滚动；当 [reverse] 为 true 时，则从右向左滚动。

类似地，如果 [scrollDirection] 为 [Axis.vertical]，那么当 [reverse] 为 false 时，页面视图从上向下滚动；当 [reverse] 为 true 时，则从下向上滚动。

默认为 false。

### controller

```dart
PageController? controller
```

可用于控制此页面视图滚动到的位置的对象。

### physics

```dart
ScrollPhysics? physics
```

页面视图应如何响应用户输入。

例如，决定用户停止拖动页面视图后，页面视图会如何继续播放动画。

在使用之前，物理效果会先通过 [PageScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/pagescrollphysics) 修改，以吸附到页面边界。

如果为 [scrollBehavior] 提供了显式的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)，该 behavior 提供的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 将在 [physics](https://www.yuque.com/thyname/flutter.physics) 之后优先生效。

默认与平台惯例保持一致。

### pageSnapping

```dart
bool pageSnapping
```

设为 false 可禁用页面吸附，适用于自定义滚动行为。

如果 [padEnds] 为 false，且 [PageController.viewportFraction] < 1.0，页面将吸附到视口起始处；否则页面将吸附到视口居中处。

### onPageChanged

```dart
ValueChanged<int>? onPageChanged
```

每当视口中央的页面发生变化时调用。

### childrenDelegate

```dart
SliverChildDelegate childrenDelegate
```

为 [PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 提供子组件的委托对象。

[PageView.custom] 构造函数允许你显式指定此委托。[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) 和 [PageView.builder] 构造函数则分别创建了包装给定 [List](https://www.yuque.com/thyname/dart.core/list) 和 [IndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/indexedwidgetbuilder) 的 childrenDelegate。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

默认为 [HitTestBehavior.opaque]。

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.widgets.scrollable.scrollBehavior}

所继承的 [ScrollConfiguration](https://www.yuque.com/thyname/flutter.widgets/scrollconfiguration) 的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 默认会被修改为不应用 [Scrollbar](https://www.yuque.com/thyname/flutter.material/scrollbar)。

### padEnds

```dart
bool padEnds
```

是否在列表两端添加内边距。

如果此值为 true，且 [PageController.viewportFraction] < 1.0，将添加内边距，使得滚动到起始处或末尾处时，第一个和最后一个子 sliver 会分别位于视口中央。

如果 [PageController.viewportFraction] >= 1.0，此属性没有效果。

此属性默认为 true。
