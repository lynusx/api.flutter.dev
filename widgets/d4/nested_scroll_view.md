@docImport 'package:flutter/material.dart';

@docImport 'page_storage.dart'; @docImport 'safe_area.dart'; @docImport 'scrollable.dart';

# NestedScrollViewHeaderSliversBuilder

```dart
typedef NestedScrollViewHeaderSliversBuilder = List<Widget> Function(BuildContext context, bool innerBoxIsScrolled)
```

供 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 用于构建其头部的函数签名。

`innerBoxIsScrolled` 参数通常用于控制 [SliverAppBar.forceElevated] 属性，以确保应用栏（app bar）显示阴影，因为在其他情况下，应用栏未必能感知到其下方实际存在内容。

# NestedScrollView

```dart
class NestedScrollView extends StatefulWidget {}
```

一个可以在内部嵌套其他滚动视图的滚动视图，各滚动视图的滚动位置在本质上是相互关联的。

此组件最常见的使用场景是：头部（由 [headerSliverBuilder] 构建）为包含 [TabBar](https://www.yuque.com/thyname/flutter.material/tabbar) 的可伸缩 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)，[body] 为 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview)，从而使可滚动视图的内容根据当前可见的标签页而变化。

## 动机

在普通的 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 中，只存在一组 sliver（滚动视图的组成部分）。如果其中某个 sliver 承载了一个沿相反方向滚动的 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview)（例如允许用户在标签页对应的各个页面之间水平滑动，而列表本身则垂直滚动），那么该 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview) 内的任何列表都不会与外层的 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 产生交互。例如，快速滑动内部列表使其滚动到顶部，并不会使外层 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 中已折叠的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 展开。

[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 通过为外层 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 和内层各个 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview)（即 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview) 内部的滚动视图）提供自定义的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，并将它们关联在一起，从而解决了这个问题，使其在用户看来是一个连贯统一的滚动视图。

{@tool dartpad} 此示例展示了一个 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)：其头部由 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 中的 [TabBar](https://www.yuque.com/thyname/flutter.material/tabbar) 组合而成，body 为 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview)。示例使用一对 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber)/[SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 使内部各列表正确对齐，并使用 [SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea) 避免任何水平方向上的干扰（例如手机横放时 iOS 的“刘海”）。此外，还使用 [PageStorageKey](https://www.yuque.com/thyname/flutter.widgets/pagestoragekey) 来记住每个标签页对应列表的滚动位置。

** 代码见 examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.0.dart ** {@end-tool}

## 在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中使用 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的外层滚动视图（即 [headerSliverBuilder]）中使用 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 时，可能需要一些特殊配置，才能使其表现得如同外层与内层是同一个滚动视图（例如 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)）一样。

### 固定（pinned）的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

固定的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中的表现与在其他滚动视图（如 [CustomScrollView](https://www.yuque.com/thyname/flutter.widgets/customscrollview)）中完全一致。使用 [SliverAppBar.pinned] 时，应用栏会始终固定显示在滚动视图顶部。应用栏仍然可以随着用户滚动而展开或收缩，但它会始终保持可见，而不会被滚出视图之外。

这在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中可以自然实现，因为固定的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 本身并不需要在视口的可见区域内进出移动。无论内层还是外层的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 发生移动，应用栏都会按预期保持固定。

如果应用栏同时具有浮动（floating）、固定（pinned）特性并使用了展开高度，请遵循下文所述的浮动约定。

### 浮动（floating）的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

当在外层滚动视图或 [headerSliverBuilder] 中放置一个使用 [SliverAppBar.floating] 的浮动应用栏时，它不会自动响应内层滚动视图（即 [body]）的滚动而浮现。

这是因为浮动应用栏依据其自身 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 的滚动偏移量来决定浮动行为。由于内层与外层是两个独立的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable)，位于外层头部的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 无法感知内层 body 滚动偏移量的变化。

要使外层浮动，请使用 [NestedScrollView.floatHeaderSlivers]。将其设置为 true 后，嵌套滚动的协调器会优先浮动头部 sliver，然后再将剩余的拖动量应用到 body。

此外，当应用栏同时具有浮动、固定特性并具有展开高度时，同样应当使用 `floatHeaderSlivers` 标志。在这种配置下，应用栏的可伸缩区域会展开和收缩，而应用栏的主要部分则保持固定。

{@tool dartpad} 此简单示例展示了一个头部包含浮动 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 的 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)。通过使用 [floatHeaderSlivers] 属性，外层与内层 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 之间的浮动行为得以协调，使其表现得如同单一的可滚动视图一样。

** 代码见 examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.1.dart ** {@end-tool}

### 吸附（snapping）的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

浮动的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 还可以选择执行吸附动画。若 [SliverAppBar.snap] 为 true，则当滚动使浮动应用栏显现时，会触发一个将整个应用栏滑入视图的动画；同样，若滚动使应用栏消失，该动画也会将应用栏完全滑出视图。

在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中，也可以只实现吸附动画而不使应用栏浮动。不使用 [NestedScrollView.floatHeaderSlivers] 时，应用栏会以吸附方式滑入滑出，而不会浮动。

[SliverAppBar.snap] 动画在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中实现时，应当与 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 和 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 组件配合使用。这些组件会将 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 产生的任何重叠行为吸收，并重定向到 body 中的 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)。如果缺少这一处理，内层的“inner”滚动视图可能会在实际并未滚动的情况下，最终却出现在 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 的下方。

{@tool dartpad} 此简单示例展示了一个头部包含吸附并浮动的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 的 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)。在*不*设置任何额外标志（例如 [NestedScrollView.floatHeaderSlivers]）的情况下，[SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 会以滑入滑出的方式动画，而不会浮动。[SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 与 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 用于维持两个独立滚动视图之间的正确对齐。

** 代码见 examples/api/lib/widgets/nested_scroll_view/nested_scroll_view.2.dart ** {@end-tool}

### 同时吸附并浮动的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

目前，[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 不支持同时对外层滚动视图进行浮动和吸附，例如同时使用 [SliverAppBar.floating] 和 [SliverAppBar.snap]。

### 拉伸（stretching）的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)

目前，[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 不支持对外层滚动视图进行拉伸，例如使用 [SliverAppBar.stretch]。

另请参阅：

- [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)，其中包含浮动、固定和吸附等不同配置的示例。
- [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber)，一种包裹其他 sliver 的 sliver，强制将其布局范围（layout extent）视为重叠部分。
- [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)，一种其 sliver geometry 基于 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 中存储值的 sliver。

### NestedScrollView()

```dart
NestedScrollView({dynamic key, ScrollController? controller, Axis scrollDirection = Axis.vertical, bool reverse = false, ScrollPhysics? physics, required NestedScrollViewHeaderSliversBuilder headerSliverBuilder, required Widget body, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool floatHeaderSlivers = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior})
```

创建一个嵌套滚动视图。

[reverse]、[headerSliverBuilder] 和 [body] 参数不能为 null。

### controller

```dart
ScrollController? controller
```

用于控制外层滚动视图滚动到的位置的对象。

### scrollDirection

```dart
Axis scrollDirection
```

{@macro flutter.widgets.scroll_view.scrollDirection}

此属性仅适用于外层滚动视图（由 [headerSliverBuilder] 返回的 sliver 组成）的 [Axis](https://www.yuque.com/thyname/flutter.painting/axis)。由于内层滚动视图并非直接由 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 配置，若希望两者的轴向一致，需要为 [body] 中的滚动视图配置相同的方向（如果期望它们以相同方向滚动）。这使 NestedScrollView 的配置更加灵活。

### reverse

```dart
bool reverse
```

滚动视图是否沿阅读方向滚动。

例如，如果阅读方向为从左到右，且 [scrollDirection] 为 [Axis.horizontal]，那么当 [reverse] 为 false 时，滚动视图从左向右滚动；为 true 时则从右向左滚动。

类似地，如果 [scrollDirection] 为 [Axis.vertical]，那么当 [reverse] 为 false 时，滚动视图从上向下滚动；为 true 时则从下向上滚动。

此属性仅适用于外层滚动视图（由 [headerSliverBuilder] 返回的 sliver 组成）。由于内层滚动视图并非直接由 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 配置，若希望两者都以相反方向滚动，需要为 [body] 中的滚动视图做相应配置（如果期望它们保持一致）。这使 NestedScrollView 的配置更加灵活。

默认值为 false。

### physics

```dart
ScrollPhysics? physics
```

滚动视图应如何响应用户输入。

例如，决定滚动视图在用户停止拖动后如何继续动画（提供 [ScrollPhysics.createBallisticSimulation] 的自定义实现可以覆盖这一特定的物理行为）。

如果向 [scrollBehavior] 提供了显式的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)，该行为所提供的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 将在 [physics](https://www.yuque.com/thyname/flutter.physics) 之后优先生效。

默认与平台惯例保持一致。

所提供对象的 [ScrollPhysics.applyBoundaryConditions] 实现不应允许滚动超出由传递给该方法的 [ScrollMetrics.minScrollExtent] 和 [ScrollMetrics.maxScrollExtent] 属性所描述的滚动范围。如果不满足这一不变量，嵌套滚动视图对用户滚动的响应可能会出现异常。

此属性仅适用于外层滚动视图（由 [headerSliverBuilder] 返回的 sliver 组成）。由于内层滚动视图并非直接由 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 配置，若希望两者以相同的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 滚动，需要为 [body] 中的滚动视图做相应配置（如果期望它们保持一致），或者使用 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 作为祖先节点，使内外层滚动视图都继承相同的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics)。这使 NestedScrollView 的配置更加灵活。

[ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 还决定了 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 是否可以接受用户输入以更改滚动偏移量。例如，[NeverScrollableScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/neverscrollablescrollphysics) 通常不允许用户拖动滚动视图，但在此情况下，如果两个滚动视图中有一个可以被拖动，则仍会允许拖动。若将内外两个滚动视图都配置为 [NeverScrollableScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/neverscrollablescrollphysics)，则会在这种情况下禁止拖动。

### headerSliverBuilder

```dart
NestedScrollViewHeaderSliversBuilder headerSliverBuilder
```

用于构建位于内层滚动视图（由 [body] 指定）之前的任意组件的构建器。

通常用于创建包含 [TabBar](https://www.yuque.com/thyname/flutter.material/tabbar) 的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar)。

### body

```dart
Widget body
```

在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 内部显示的组件。

通常为 [TabBarView](https://www.yuque.com/thyname/flutter.material/tabbarview)。

[body] 是在提供了 [PrimaryScrollController](https://www.yuque.com/thyname/flutter.widgets/primaryscrollcontroller) 的上下文中构建的，该控制器与 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的滚动控制器相互配合。因此，[body] 内部任何需要随 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 一起滚动的基于 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 的组件（如 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 等），都不应指定显式的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，而应让其默认使用 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 提供的 [PrimaryScrollController](https://www.yuque.com/thyname/flutter.widgets/primaryscrollcontroller)。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### floatHeaderSlivers

```dart
bool floatHeaderSlivers
```

[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的协调器在滚动时是否应优先处理外层可滚动视图，而非内层。

这在外层可滚动视图中包含需要浮动的 [SliverAppBar](https://www.yuque.com/thyname/flutter.material/sliverappbar) 时非常有用。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认值为 [Clip.hardEdge]。

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

默认值为 [HitTestBehavior.opaque]。

### restorationId

```dart
String? restorationId
```

{@macro flutter.widgets.scrollable.restorationId}

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@macro flutter.widgets.scrollable.scrollBehavior}

继承的 [ScrollConfiguration](https://www.yuque.com/thyname/flutter.widgets/scrollconfiguration) 所提供的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 默认会被修改为不应用 [Scrollbar](https://www.yuque.com/thyname/flutter.material/scrollbar)。这是因为 NestedScrollView 无法预先假定外层和内层 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 组件的配置方式，尤其是应将它们视为同一个滚动视图，还是视为各自独立、需要各自不同行为的滚动视图。

### sliverOverlapAbsorberHandleFor()

```dart
SliverOverlapAbsorberHandle sliverOverlapAbsorberHandleFor(BuildContext context)
```

返回距离最近的祖先 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle)。

配置 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 和 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 组件时需要用到此方法。

有关此方法用法的示例代码，请参阅 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 文档。

### createState()

```dart
NestedScrollViewState createState()
```

# NestedScrollViewState

```dart
class NestedScrollViewState extends State<NestedScrollView> {}
```

[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的 [State](https://www.yuque.com/thyname/flutter.widgets/state)。

可以通过 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的 state 访问其子组件的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)，即 [innerController] 和 [outerController]。这对于获取 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中各自的滚动位置非常有用。

如果想要访问 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 的内层或外层滚动控制器，可以通过向 [NestedScrollView.key] 参数提供一个 `GlobalKey<NestedScrollViewState>` 来获取其 [NestedScrollViewState](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewstate)。

{@tool dartpad} 可以通过 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 获取 [NestedScrollViewState](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewstate)。使用以下方式设置后，即可通过 `globalKey.currentState.innerController` 访问内层滚动控制器。

** 代码见 examples/api/lib/widgets/nested_scroll_view/nested_scroll_view_state.0.dart ** {@end-tool}

### innerController

```dart
ScrollController get innerController
```

提供给 [NestedScrollView.body] 中 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)。

操纵此控制器的 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition) 会将外层头部 sliver 向上推出视图之外。除非使用 [ScrollPosition.setPixels]，否则 [outerController] 的位置会被设置为 [ScrollPosition.maxScrollExtent]。

另请参阅：

- [outerController]，它暴露了 [NestedScrollView.headerSliverBuilder] 所包含的 sliver 所使用的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)。

### outerController

```dart
ScrollController get outerController
```

提供给 [NestedScrollView.headerSliverBuilder] 中 sliver 的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)。

若已提供 [NestedScrollView.controller]，则此控制器与其等价。

操纵此控制器的 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition) 会将内层 body sliver 向下推。除非使用 [ScrollPosition.setPixels]，否则 [innerController] 的位置会被设置为 [ScrollPosition.minScrollExtent]。在视觉上，内层 body 会被滚动至其起始位置。

另请参阅：

- [innerController]，它暴露了 [NestedScrollView.body] 中 [ScrollView](https://www.yuque.com/thyname/flutter.widgets/scrollview) 所使用的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)。

### initState()

```dart
void initState()
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### didUpdateWidget()

```dart
void didUpdateWidget(NestedScrollView oldWidget)
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

# SliverOverlapAbsorberHandle

```dart
class SliverOverlapAbsorberHandle extends ChangeNotifier {}
```

提供给 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber)、[SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 和 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 的句柄，用于在 [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 中转移重叠部分。

一个特定的 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 一次只能分配给一个 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber)。它同时也可以（通常也确实）分配给一个或多个 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)，这些注入器必须是同一个 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 中位于 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 之后的后代节点。[SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 必须是 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 的直接后代，并参与同一个 sliver 布局过程。（[SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 则可以是参与嵌套滚动视图 sliver 布局的某个后代节点。）

每当 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 被标记为需要重新布局时，都会使其分配的 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 触发通知。当此情况发生时，[SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)（及其他客户端）有责任将自身标记为需要更新，以便在布局过程中几何形状随之发生变化时能够作出响应。

另请参阅：

- [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)，它使用 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 和 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 来对齐其子组件，其文档中包含此类的示例用法。

### SliverOverlapAbsorberHandle()

```dart
SliverOverlapAbsorberHandle()
```

创建一个 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle)。

### layoutExtent

```dart
double? get layoutExtent
```

[SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 当前吸收的重叠量。

对应于 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 的子组件的 [SliverGeometry.layoutExtent]。

此值会在 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 的布局过程中更新，其他任何时候都不应发生变化。该值变化时不会发出通知；客户端（例如 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)）需要在此对象发出通知时自行将自身标记为需要更新，因为这意味着 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 可能会在该次布局过程中随后改变此值。

### scrollExtent

```dart
double? get scrollExtent
```

[SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 所吸收间隙的总滚动范围（scroll extent）。

对应于 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 的子组件的 [SliverGeometry.scrollExtent]。

此值会在 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 的布局过程中更新，其他任何时候都不应发生变化。该值变化时不会发出通知；客户端（例如 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)）需要在此对象发出通知时自行将自身标记为需要更新，因为这意味着 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 可能会在该次布局过程中随后改变此值。

### toString()

```dart
String toString()
```

# SliverOverlapAbsorber

```dart
class SliverOverlapAbsorber extends SingleChildRenderObjectWidget {}
```

一种包裹另一个 sliver 的 sliver，强制将其布局范围视为重叠部分。

子 `sliver` 请求的重叠量与该组件报告的重叠量之间的差值，称为*已吸收的重叠量*（absorbed overlap），会被记录到 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 中，该句柄通常会被传递给 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector)。

另请参阅：

- [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)，其文档中包含展示如何使用此组件的示例代码。

### SliverOverlapAbsorber()

```dart
SliverOverlapAbsorber({dynamic key, required SliverOverlapAbsorberHandle handle, Widget? sliver})
```

创建一个吸收重叠部分并将其上报给 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 的 sliver。

### handle

```dart
SliverOverlapAbsorberHandle handle
```

用于记录已吸收重叠量的对象。

一个特定的 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 一次只能分配给一个 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber)。

### createRenderObject()

```dart
RenderSliverOverlapAbsorber createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOverlapAbsorber renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverOverlapAbsorber

```dart
class RenderSliverOverlapAbsorber extends RenderSliver with RenderObjectWithChildMixin<RenderSliver> {}
```

一种包裹另一个 sliver 的 sliver，强制将其布局范围视为重叠部分。

子 sliver 请求的重叠量与该组件报告的重叠量之间的差值，称为*已吸收的重叠量*，会被记录到 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 中，该句柄通常会被传递给 [RenderSliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/rendersliveroverlapinjector)。

### RenderSliverOverlapAbsorber()

```dart
RenderSliverOverlapAbsorber({required SliverOverlapAbsorberHandle handle, RenderSliver? sliver})
```

创建一个吸收重叠部分并将其上报给 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 的 sliver。

[sliver] 必须为 [RenderSliver](https://www.yuque.com/thyname/flutter.rendering/rendersliver)。

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

用于记录已吸收重叠量的对象。

一个特定的 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 一次只能分配给一个 [RenderSliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/rendersliveroverlapabsorber)。

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### performLayout()

```dart
void performLayout()
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverOverlapInjector

```dart
class SliverOverlapInjector extends SingleChildRenderObjectWidget {}
```

一种其 sliver geometry 基于 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 中存储值的 sliver。

[SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 必须是共同祖先 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 中位置更靠前的后代节点，以确保在每一帧中，它总是先于 [SliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapinjector) 完成布局。

另请参阅：

- [NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview)，它使用 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 来对齐其子组件，其文档中包含此类的示例用法。

### SliverOverlapInjector()

```dart
SliverOverlapInjector({dynamic key, required SliverOverlapAbsorberHandle handle, Widget? sliver})
```

创建一个高度与给定 [handle] 的布局范围（layout extent）相等的 sliver。

### handle

```dart
SliverOverlapAbsorberHandle handle
```

为此注入器提供数据的 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 所对应的句柄。

该句柄应当是由某个 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 和 [NestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/nestedscrollviewviewport) 所持有的句柄。

### createRenderObject()

```dart
RenderSliverOverlapInjector createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverOverlapInjector renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverOverlapInjector

```dart
class RenderSliverOverlapInjector extends RenderSliver {}
```

一种其 sliver geometry 基于 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 中存储值的 sliver。

[RenderSliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/rendersliveroverlapabsorber) 必须是共同祖先 [RenderViewport](https://www.yuque.com/thyname/flutter.rendering/renderviewport)（很可能是 [RenderNestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/rendernestedscrollviewviewport)）中位置更靠前的后代节点，以确保在每一帧中，它总是先于 [RenderSliverOverlapInjector](https://www.yuque.com/thyname/flutter.widgets/rendersliveroverlapinjector) 完成布局。

### RenderSliverOverlapInjector()

```dart
RenderSliverOverlapInjector({required SliverOverlapAbsorberHandle handle})
```

创建一个高度与给定 [handle] 的范围（extent）相等的 sliver。

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

用于指定此渲染对象所注入间隙宽度的对象。

该句柄应当是由某个 [RenderSliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/rendersliveroverlapabsorber) 和 [RenderNestedScrollViewViewport](https://www.yuque.com/thyname/flutter.widgets/rendernestedscrollviewviewport) 所持有的句柄。

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### performLayout()

```dart
void performLayout()
```

### debugPaint()

```dart
void debugPaint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# NestedScrollViewViewport

```dart
class NestedScrollViewViewport extends Viewport {}
```

[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 所使用的 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 变体。

此视口持有一个 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle)，并在每次需要重新计算布局时（例如发生滚动时）通知该句柄。

### NestedScrollViewViewport()

```dart
NestedScrollViewViewport({dynamic key, dynamic axisDirection, dynamic crossAxisDirection, double anchor, required dynamic offset, dynamic center, List<Widget> slivers, required SliverOverlapAbsorberHandle handle, dynamic clipBehavior})
```

创建一个带有 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 的 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 变体。

### handle

```dart
SliverOverlapAbsorberHandle handle
```

为此注入器提供数据的 [SliverOverlapAbsorber](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorber) 所对应的句柄。

### createRenderObject()

```dart
RenderNestedScrollViewViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderNestedScrollViewViewport renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderNestedScrollViewViewport

```dart
class RenderNestedScrollViewViewport extends RenderViewport {}
```

[NestedScrollView](https://www.yuque.com/thyname/flutter.widgets/nestedscrollview) 所使用的 [RenderViewport](https://www.yuque.com/thyname/flutter.rendering/renderviewport) 变体。

此视口持有一个 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle)，并在每次需要重新计算布局时（例如发生滚动时）通知该句柄。

### RenderNestedScrollViewViewport()

```dart
RenderNestedScrollViewViewport({dynamic axisDirection, required dynamic crossAxisDirection, required dynamic offset, dynamic anchor, dynamic children, dynamic center, required SliverOverlapAbsorberHandle handle, dynamic clipBehavior})
```

创建一个带有 [SliverOverlapAbsorberHandle](https://www.yuque.com/thyname/flutter.widgets/sliveroverlapabsorberhandle) 的 [RenderViewport](https://www.yuque.com/thyname/flutter.rendering/renderviewport) 变体。

### handle

```dart
SliverOverlapAbsorberHandle get handle
```

调用 [markNeedsLayout] 时需要通知的对象。

### handle

```dart
set handle(SliverOverlapAbsorberHandle value)
```

设置此值将会对新对象触发通知。
