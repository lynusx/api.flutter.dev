@docImport 'package:flutter/material.dart';

@docImport 'scroll_view.dart'; @docImport 'viewport.dart';

# ChangeReportingBehavior

```dart
enum ChangeReportingBehavior {}
```

[ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 中报告已选中项索引的行为。

此项决定何时调用 `onSelectedItemChanged` 回调。

仅当滚动视图停止滚动时才报告已选中项索引。

在每次滚动更新时都报告已选中项索引。

# ListWheelChildDelegate

```dart
abstract class ListWheelChildDelegate {}
```

为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 提供子项的委托。

[ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 在布局期间惰性构建其子项，以避免创建超出 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 可见范围的子项。该委托负责在此阶段为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 提供子项。

另请参阅：

- [ListWheelChildListDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildlistdelegate)：使用显式列表提供子项的委托。
- [ListWheelChildLoopingListDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildloopinglistdelegate)：通过循环显式列表提供无限子项的委托。
- [ListWheelChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildbuilderdelegate)：使用构建器回调提供子项的委托。

### build()

```dart
Widget? build(BuildContext context, int index)
```

返回给定索引处的子项。如果给定索引处的子项不存在，则返回 null。

### estimatedChildCount

```dart
int? get estimatedChildCount
```

返回此委托将构建的子项数量的估计值。

### trueIndexOf()

```dart
int trueIndexOf(int index)
```

返回在给定索引处构建的子项的真实索引。默认为给定的索引；但如果该委托是 [ListWheelChildLoopingListDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildloopinglistdelegate)，则该值为委托所循环到的真实元素的索引。

示例：[ListWheelChildLoopingListDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildloopinglistdelegate) 通过循环一个长度为 8 的列表来构建。此时，trueIndexOf(10) = 2，trueIndexOf(-5) = 3。

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildDelegate oldDelegate)
```

用于检查该委托与旧委托是否存在实际"差异"，以便调用方决定是否需要重建。

# ListWheelChildListDelegate

```dart
class ListWheelChildListDelegate extends ListWheelChildDelegate {}
```

使用显式列表为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 提供子项的委托。

[ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 惰性构建其子项，以避免创建超出 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 可见范围的子项。此委托使用显式列表提供子项，这种方式较为方便，但会削弱惰性构建带来的优势。

一般而言，预先构建所有 widget 并不高效。更好的做法是使用 [ListWheelChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildbuilderdelegate)，或直接继承 [ListWheelChildDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchilddelegate) 来创建按需构建子项的委托。

此类适用于以下情形：子项列表事先已经明确已知（理想情况下这些子项本身就是编译期常量），因此不会在每次创建该委托时重新构建；或者列表较小，几乎总是可见的（因此按需构建并无收益）。例如，对话框的主体内容可能同时满足这两个条件。

### ListWheelChildListDelegate()

```dart
ListWheelChildListDelegate({required List<Widget> children})
```

根据具体的子项列表构造该委托。

### children

```dart
List<Widget> children
```

包含所有可提供子项的列表。

### estimatedChildCount

```dart
int get estimatedChildCount
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildListDelegate oldDelegate)
```

# ListWheelChildLoopingListDelegate

```dart
class ListWheelChildLoopingListDelegate extends ListWheelChildDelegate {}
```

通过循环显式列表为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 提供无限子项的委托。

[ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 惰性构建其子项，以避免创建超出 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 可见范围的子项。此委托使用显式列表提供子项，这种方式较为方便，但会削弱惰性构建带来的优势。

一般而言，预先构建所有 widget 并不高效。更好的做法是使用 [ListWheelChildBuilderDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchildbuilderdelegate)，或直接继承 [ListWheelChildDelegate](https://www.yuque.com/thyname/flutter.widgets/listwheelchilddelegate) 来创建按需构建子项的委托。

此类适用于以下情形：子项列表事先已经明确已知（理想情况下这些子项本身就是编译期常量），因此不会在每次创建该委托时重新构建；或者列表较小，几乎总是可见的（因此按需构建并无收益）。例如，对话框的主体内容可能同时满足这两个条件。

### ListWheelChildLoopingListDelegate()

```dart
ListWheelChildLoopingListDelegate({required List<Widget> children})
```

根据具体的子项列表构造该委托。

### children

```dart
List<Widget> children
```

包含所有可提供子项的列表。

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### trueIndexOf()

```dart
int trueIndexOf(int index)
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildLoopingListDelegate oldDelegate)
```

# ListWheelChildBuilderDelegate

```dart
class ListWheelChildBuilderDelegate extends ListWheelChildDelegate {}
```

使用构建器回调为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 提供子项的委托。

[ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 惰性构建其子项，以避免创建超出 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 可见范围的子项。此委托通过 [IndexedWidgetBuilder](https://www.yuque.com/thyname/flutter.widgets/indexedwidgetbuilder) 回调提供子项，因此子项无需在显示之前就被构建。

### ListWheelChildBuilderDelegate()

```dart
ListWheelChildBuilderDelegate({required NullableIndexedWidgetBuilder builder, int? childCount})
```

根据构建器回调构造该委托。

### builder

```dart
NullableIndexedWidgetBuilder builder
```

惰性调用以构建子项。

### childCount

```dart
int? childCount
```

{@template flutter.widgets.ListWheelChildBuilderDelegate.childCount} 如果非空，则 [childCount] 为可提供的最大子项数量，子项的可用索引范围为 0 到 [childCount] - 1。

如果为 null，则上下限均未知。但 [builder] 必须为一段连续的区间提供子项。如果 builder 在某个索引处返回 null，则该区间在此终止。{@endtemplate}

### estimatedChildCount

```dart
int? get estimatedChildCount
```

### build()

```dart
Widget? build(BuildContext context, int index)
```

### shouldRebuild()

```dart
bool shouldRebuild(ListWheelChildBuilderDelegate oldDelegate)
```

# FixedExtentScrollController

```dart
class FixedExtentScrollController extends ScrollController {}
```

用于子项大小相同的滚动视图的控制器。

与标准 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller) 类似，但增加了便捷机制，可用于读取及跳转到指定的项索引，而不是使用原始的像素滚动偏移量。

另请参阅：

- [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview)：一个具有固定大小子项的可滚动视图 widget，由该控制器控制。
- [FixedExtentMetrics](https://www.yuque.com/thyname/flutter.widgets/fixedextentmetrics)：由 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 的 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 所暴露的 `metrics` 属性，可用于以推送（push）方式而非轮询 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller) 的方式监听当前项索引。

### FixedExtentScrollController()

```dart
FixedExtentScrollController({int initialItem = 0, bool keepScrollOffset, String? debugLabel, void Function(ScrollPosition)? onAttach, void Function(ScrollPosition)? onDetach})
```

为子项大小相同的可滚动组件创建一个滚动控制器。

### initialItem

```dart
int initialItem
```

首次创建滚动视图时要显示的页面。

默认为零。

### selectedItem

```dart
int get selectedItem
```

当前最接近视口中心的已选中项索引。

在以下情况下，[FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller) 无法得知当前项：

1.  当前没有滚动视图正在使用此 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller)。
2.  有多个滚动视图正在使用同一个 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller)。

在此情况下读取 [selectedItem] 将抛出 [AssertionError](https://www.yuque.com/thyname/dart.core/assertionerror)。

可以在访问 [selectedItem] 之前使用 [hasClients] 属性检查是否已附加滚动视图。

### animateToItem()

```dart
Future<void> animateToItem(int itemIndex, {required Duration duration, required Curve curve})
```

使受控滚动视图以动画方式滚动到给定的项索引。

动画将持续给定的时长，并遵循给定的曲线。返回的 [Future](https://www.yuque.com/thyname/dart.async/future) 会在动画完成时结束。

### jumpToItem()

```dart
void jumpToItem(int itemIndex)
```

更改受控滚动视图中位于中心位置的项索引。

将项索引位置从当前值直接跳转到给定值，不带动画，且不检查新值是否在有效范围内。

### createScrollPosition()

```dart
ScrollPosition createScrollPosition(ScrollPhysics physics, ScrollContext context, ScrollPosition? oldPosition)
```

# FixedExtentMetrics

```dart
class FixedExtentMetrics extends FixedScrollMetrics {}
```

用于具有固定子项大小的滚动视图的 [ScrollPosition](https://www.yuque.com/thyname/flutter.widgets/scrollposition) 度量信息。

这些度量信息可在由诸如带有 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller) 的 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 等滚动视图生成的 [ScrollNotification](https://www.yuque.com/thyname/flutter.widgets/scrollnotification) 上获取，并暴露当前的 [itemIndex] 以及该滚动视图的范围（extent）信息。

`FixedExtent` 指的是可滚动子项具有相同的大小，这与父类名 [FixedScrollMetrics](https://www.yuque.com/thyname/flutter.widgets/fixedscrollmetrics) 中的 `Fixed` 不同，后者指的是其不可变性。

### FixedExtentMetrics()

```dart
FixedExtentMetrics({required double? minScrollExtent, required double? maxScrollExtent, required double? pixels, required double? viewportDimension, required dynamic axisDirection, required int itemIndex, required double devicePixelRatio})
```

为 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 创建关联数值的不可变快照。

### copyWith()

```dart
FixedExtentMetrics copyWith({double? minScrollExtent, double? maxScrollExtent, double? pixels, double? viewportDimension, AxisDirection? axisDirection, int? itemIndex, double? devicePixelRatio})
```

### itemIndex

```dart
int itemIndex
```

该滚动视图当前已选中的项索引。

# FixedExtentScrollPhysics

```dart
class FixedExtentScrollPhysics extends ScrollPhysics {}
```

一种始终直接落在子项上、而非落在滚动范围内任意位置的吸附式滚动物理效果（snapping physics）。

其行为类似于老虎机滚轮，不同之处在于弹道模拟（ballistics simulation）永不会过冲，若需要停在某一项上，会在单个项的范围内回滚。

必须与使用 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller) 的可滚动组件配合使用。

超出滚动范围时会将行为交由父级处理。

### FixedExtentScrollPhysics()

```dart
FixedExtentScrollPhysics({ScrollPhysics? parent})
```

创建一个始终落在子项上的滚动物理效果。

### applyTo()

```dart
FixedExtentScrollPhysics applyTo(ScrollPhysics? ancestor)
```

### createBallisticSimulation()

```dart
Simulation? createBallisticSimulation(ScrollMetrics position, double velocity)
```

# ListWheelScrollView

```dart
class ListWheelScrollView extends StatefulWidget {}
```

一个可以在滚轮上滚动子项的容器。

该 widget 与 [ListView](https://www.yuque.com/thyname/flutter.widgets/listview) 类似，但有一个限制：所有子项在滚动轴方向上必须具有相同的大小。

{@youtube 560 315 https://www.youtube.com/watch?v=dUhmWAz4C7Y}

当列表处于零滚动偏移量时，第一个子项与视口中心对齐；当列表处于最终滚动偏移量时，最后一个子项与视口中心对齐。

子项会按照在滚轮上旋转的方式渲染，而不是在平面上滚动。

### ListWheelScrollView()

```dart
ListWheelScrollView({dynamic key, ScrollController? controller, ScrollPhysics? physics, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, ValueChanged<int>? onSelectedItemChanged, bool renderChildrenOutsideViewport = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required List<Widget> children})
```

构造一个子项以滚轮方式滚动的列表。其子项会被传递给一个委托，并在布局期间惰性构建。

### ListWheelScrollView.useDelegate()

```dart
ListWheelScrollView.useDelegate({dynamic key, ScrollController? controller, ScrollPhysics? physics, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, ValueChanged<int>? onSelectedItemChanged, bool renderChildrenOutsideViewport = false, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque, String? restorationId, ScrollBehavior? scrollBehavior, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ChangeReportingBehavior changeReportingBehavior = ChangeReportingBehavior.onScrollUpdate, required ListWheelChildDelegate childDelegate})
```

构造一个子项以滚轮方式滚动的列表。其子项由一个委托管理，并在布局期间惰性构建。

### controller

```dart
ScrollController? controller
```

通常为用于控制当前项的 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller)。

[FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller) 可用于读取当前已选中（居中）的子项，也可用于更改当前项。

如果未提供，则会隐式创建一个新的 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller)。

如果使用 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller) 而非 [FixedExtentScrollController](https://www.yuque.com/thyname/flutter.widgets/fixedextentscrollcontroller)，则 [ScrollNotification.metrics] 将不再提供 [FixedExtentMetrics](https://www.yuque.com/thyname/flutter.widgets/fixedextentmetrics) 来指示当前项索引，且 [onSelectedItemChanged] 也将无法正常工作。

若只需在值发生变化时读取当前已选中项，请使用 [onSelectedItemChanged]。

### physics

```dart
ScrollPhysics? physics
```

滚动视图应如何响应用户输入。

例如，决定用户停止拖动滚动视图后该视图如何继续动画。

如果为 [scrollBehavior] 提供了显式的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)，则该 behavior 所提供的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 将优先于 [physics](https://www.yuque.com/thyname/flutter.physics) 生效。

默认遵循平台约定。

### diameterRatio

```dart
double diameterRatio
```

{@macro flutter.rendering.RenderListWheelViewport.diameterRatio}

### perspective

```dart
double perspective
```

{@macro flutter.rendering.RenderListWheelViewport.perspective}

### offAxisFraction

```dart
double offAxisFraction
```

{@macro flutter.rendering.RenderListWheelViewport.offAxisFraction}

### useMagnifier

```dart
bool useMagnifier
```

{@macro flutter.rendering.RenderListWheelViewport.useMagnifier}

### magnification

```dart
double magnification
```

{@macro flutter.rendering.RenderListWheelViewport.magnification}

### overAndUnderCenterOpacity

```dart
double overAndUnderCenterOpacity
```

{@macro flutter.rendering.RenderListWheelViewport.overAndUnderCenterOpacity}

### itemExtent

```dart
double itemExtent
```

每个子项在主轴方向上的大小。

必须为正数。

### squeeze

```dart
double squeeze
```

{@macro flutter.rendering.RenderListWheelViewport.squeeze}

默认为 1。

### onSelectedItemChanged

```dart
ValueChanged<int>? onSelectedItemChanged
```

一个可选的监听器，在居中的子项发生变化时调用。

### renderChildrenOutsideViewport

```dart
bool renderChildrenOutsideViewport
```

{@macro flutter.rendering.RenderListWheelViewport.renderChildrenOutsideViewport}

### childDelegate

```dart
ListWheelChildDelegate childDelegate
```

用于惰性实例化子项的委托。

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

继承自 [ScrollConfiguration](https://www.yuque.com/thyname/flutter.widgets/scrollconfiguration) 的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 默认会被修改为不应用 [Scrollbar](https://www.yuque.com/thyname/flutter.material/scrollbar)。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### changeReportingBehavior

```dart
ChangeReportingBehavior changeReportingBehavior
```

报告已选中项索引的行为。

此项决定何时调用 [onSelectedItemChanged] 回调。默认为 [ChangeReportingBehavior.onScrollUpdate]。

### createState()

```dart
State<ListWheelScrollView> createState()
```

# ListWheelElement

```dart
class ListWheelElement extends RenderObjectElement implements ListWheelChildManager {}
```

支持为 [ListWheelViewport](https://www.yuque.com/thyname/flutter.widgets/listwheelviewport) 惰性构建子项的 Element。

### ListWheelElement()

```dart
ListWheelElement(ListWheelViewport widget)
```

为给定的 widget 创建一个惰性构建子项的 Element。

### renderObject

```dart
RenderListWheelViewport get renderObject
```

### update()

```dart
void update(ListWheelViewport newWidget)
```

### childCount

```dart
int? get childCount
```

### performRebuild()

```dart
void performRebuild()
```

### retrieveWidget()

```dart
Widget? retrieveWidget(int index)
```

向底层委托请求给定索引处的 widget。

通常 builder 对每个索引只会调用一次，其结果会被缓存。但当该 Element 被重建时，缓存会被清空。

### childExistsAt()

```dart
bool childExistsAt(int index)
```

### createChild()

```dart
void createChild(int index, {required RenderBox? after})
```

### removeChild()

```dart
void removeChild(RenderBox child)
```

### updateChild()

```dart
Element? updateChild(Element? child, Widget? newWidget, Object? newSlot)
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

### forgetChild()

```dart
void forgetChild(Element child)
```

# ListWheelViewport

```dart
class ListWheelViewport extends RenderObjectWidget {}
```

在滚轮上显示子项子集的视口。

该视口通常与 [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview) 搭配使用，它与 [Viewport](https://www.yuque.com/thyname/flutter.widgets/viewport) 类似，都是根据滚动偏移量和子项的尺寸，在可滚动组件中显示子项的一个子集；不同之处在于，它使用 [RenderListWheelViewport](https://www.yuque.com/thyname/flutter.rendering/renderlistwheelviewport) 将子项以滚轮的形式呈现。

另请参阅：

- [ListWheelScrollView](https://www.yuque.com/thyname/flutter.widgets/listwheelscrollview)：将此视口与可滚动组件相结合的 widget。
- [RenderListWheelViewport](https://www.yuque.com/thyname/flutter.rendering/renderlistwheelviewport)：以滚轮形式渲染子项的渲染对象。

### ListWheelViewport()

```dart
ListWheelViewport({dynamic key, double diameterRatio = RenderListWheelViewport.defaultDiameterRatio, double perspective = RenderListWheelViewport.defaultPerspective, double offAxisFraction = 0.0, bool useMagnifier = false, double magnification = 1.0, double overAndUnderCenterOpacity = 1.0, required double itemExtent, double squeeze = 1.0, bool renderChildrenOutsideViewport = false, required ViewportOffset offset, required ListWheelChildDelegate childDelegate, Clip clipBehavior = Clip.hardEdge})
```

创建一个将子项渲染到滚轮上的视口。

[diameterRatio] 参数默认为 2。

[perspective] 参数默认为 0.003。

必须提供 [itemExtent] 参数（以像素为单位），且必须为正数。

[clipBehavior] 参数默认为 [Clip.hardEdge]。

[renderChildrenOutsideViewport] 参数默认为 false，且不能为 null。

必须提供 [offset] 参数。

### diameterRatio

```dart
double diameterRatio
```

{@macro flutter.rendering.RenderListWheelViewport.diameterRatio}

### perspective

```dart
double perspective
```

{@macro flutter.rendering.RenderListWheelViewport.perspective}

### offAxisFraction

```dart
double offAxisFraction
```

{@macro flutter.rendering.RenderListWheelViewport.offAxisFraction}

### useMagnifier

```dart
bool useMagnifier
```

{@macro flutter.rendering.RenderListWheelViewport.useMagnifier}

### magnification

```dart
double magnification
```

{@macro flutter.rendering.RenderListWheelViewport.magnification}

### overAndUnderCenterOpacity

```dart
double overAndUnderCenterOpacity
```

{@macro flutter.rendering.RenderListWheelViewport.overAndUnderCenterOpacity}

### itemExtent

```dart
double itemExtent
```

{@macro flutter.rendering.RenderListWheelViewport.itemExtent}

### squeeze

```dart
double squeeze
```

{@macro flutter.rendering.RenderListWheelViewport.squeeze}

默认为 1。

### renderChildrenOutsideViewport

```dart
bool renderChildrenOutsideViewport
```

{@macro flutter.rendering.RenderListWheelViewport.renderChildrenOutsideViewport}

### offset

```dart
ViewportOffset offset
```

用于描述视口中应显示内容的 [ViewportOffset](https://www.yuque.com/thyname/flutter.rendering/viewportoffset) 对象。

### childDelegate

```dart
ListWheelChildDelegate childDelegate
```

用于惰性实例化子项的委托。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。
