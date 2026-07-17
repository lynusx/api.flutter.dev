@docImport 'dart:ui'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart';

# TraversalRequestFocusCallback

```dart
typedef TraversalRequestFocusCallback = void Function(FocusNode node, {ScrollPositionAlignmentPolicy? alignmentPolicy, double? alignment, Duration? duration, Curve? curve})
```

当遍历策略请求焦点时被调用的回调签名。

# TraversalDirection

```dart
enum TraversalDirection {}
```

沿水平轴或垂直轴的一个方向。

这由 [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin) 和 [FocusNode.focusInDirection] 使用，以指示朝哪个方向查找下一个焦点。

指示当前获得焦点的组件上方的方向。

指示当前获得焦点的组件右侧的方向。

此方向不受当前上下文的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 影响。

指示当前获得焦点的组件下方的方向。

指示当前获得焦点的组件左侧的方向。

此方向不受当前上下文的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 影响。

# TraversalEdgeBehavior

```dart
enum TraversalEdgeBehavior {}
```

控制 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 边缘的焦点转移。对于移动转移（上一个或下一个），边缘表示第一项或最后一项。对于方向性转移，边缘表示 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 中最外侧的项目，例如：对于向下移动，边缘节点是底部坐标最大的节点；对于向左移动，边缘节点是 x 坐标最小的节点。

此枚举仅控制由 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 执行的遍历行为。焦点转移的其他方法，例如直接调用 [FocusNode.requestFocus] 和 [FocusNode.unfocus]，不受此枚举的影响。

另请参阅：

- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，实现此枚举背后逻辑的类。
- [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，由此枚举配置的类。

将焦点保持在焦点作用域的项目之中。

随着边缘节点继续移动，将焦点转移到 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 相反方向上的边缘节点，从而形成一个可获得焦点项目的闭环。

对于移动转移，在最后一个可获得焦点的项目之后请求下一个焦点，将把焦点转移到第一个项目，在第一个项目之前请求上一个焦点，将把焦点转移到最后一个项目。

对于方向性转移，在最右侧的节点继续请求向右焦点，将把焦点转移到最左侧的节点。在最左侧的节点继续请求向左焦点，将把焦点转移到最右侧的节点。

允许焦点离开 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。

在最后一个可获得焦点的项目之后请求下一个焦点，或在第一个项目之前请求上一个焦点，将取消任何已获得焦点节点的焦点。如果焦点遍历操作是由嵌入层（例如 Flutter 引擎）发起的，嵌入层将收到一个指示焦点不再位于当前 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 内的结果。例如，通过键盘调用（通常是 TAB 键）的 [NextFocusAction](https://www.yuque.com/thyname/flutter.widgets/nextfocusaction) 将收到 [KeyEventResult.skipRemainingHandlers]，从而使嵌入层能够处理该快捷键。在 web 上，控制权通常会转移给浏览器，使用户能够到达地址栏、跳出 `iframe`，或将焦点转移到 Flutter 管理之外的 HTML 元素上。

允许焦点向上遍历到父作用域。

到达当前作用域的边缘时，请求下一个焦点将向上查找当前作用域的父作用域，并使当前作用域旁边的焦点节点获得焦点。

如果当前作用域上方没有父作用域，则回退到 [closedLoop] 行为。

在焦点作用域的边缘停止焦点遍历。

当焦点到达焦点作用域的边缘时，将焦点保持在当前位置。

# FocusTraversalPolicy

```dart
abstract class FocusTraversalPolicy with Diagnosticable {}
```

确定 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 中可获得焦点的组件如何被遍历。

焦点遍历策略决定了相对于当前获得焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)（通常是一个 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件）所关联的组件，哪个组件是"下一个"、"上一个"或某个方向上的组件。

可以使用某个预定义的子类，或者定义一个自定义策略来创建独特的焦点顺序。

在定义自己的策略时，子类应实现 [sortDescendants] 以提供你希望子孙节点被遍历的顺序。

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，有关焦点系统的说明。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，受遍历策略影响的对象。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种依赖组件创建顺序来描述遍历顺序的策略。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种根据当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 描述为自然"阅读顺序"的策略。
- [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy)，一种使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件显式描述顺序的策略。
- [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin)，一个实现按方向进行焦点遍历的混入类。

### FocusTraversalPolicy()

```dart
FocusTraversalPolicy({TraversalRequestFocusCallback? requestFocusCallback})
```

抽象 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便它们可以在 const 表达式中使用。

{@template flutter.widgets.FocusTraversalPolicy.requestFocusCallback} `requestFocusCallback` 可用于覆盖焦点请求的默认行为。如果 `requestFocusCallback` 为 null，则默认为 [FocusTraversalPolicy.defaultTraversalRequestFocusCallback]。{@endtemplate}

### requestFocusCallback

```dart
TraversalRequestFocusCallback requestFocusCallback
```

使用键盘遍历时，用于将焦点从一个焦点节点移动到另一个焦点节点的回调。默认情况下，它会请求下一个节点的焦点，并确保该节点在可滚动组件中可见。

### defaultTraversalRequestFocusCallback()

```dart
void defaultTraversalRequestFocusCallback(FocusNode node, {ScrollPositionAlignmentPolicy? alignmentPolicy, double? alignment, Duration? duration, Curve? curve})
```

[requestFocusCallback] 的默认值。请求 `node` 的焦点，并通过调用 [Scrollable.ensureVisible] 确保该节点可见。

### findFirstFocus()

```dart
FocusNode? findFirstFocus(FocusNode currentNode, {bool ignoreCurrentFocus = false})
```

返回如果焦点正向前遍历且当前没有焦点时应获得焦点的节点。

返回的节点是如果焦点正向前遍历（即使用 [next]）且 `currentNode` 所属的最近 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 中当前没有焦点时应获得焦点的节点。

如果未给定 `ignoreCurrentFocus` 或其为 false，此函数将返回 `currentNode` 最近作用域的 [FocusScopeNode.focusedChild]（如果已设置），否则返回 [sortDescendants] 中的第一个节点，如果没有子孙节点，则返回给定的 `currentNode`。

如果 `ignoreCurrentFocus` 为 true，则该算法返回 [sortDescendants] 中的第一个节点，如果没有子孙节点，则返回给定的 `currentNode`。

另请参阅：

- [next]，被调用以将焦点移动到下一个节点的函数。
- [DirectionalFocusTraversalPolicyMixin.findFirstFocusInDirection]，一个用于查找特定方向上第一个可获得焦点组件的函数。

### findLastFocus()

```dart
FocusNode findLastFocus(FocusNode currentNode, {bool ignoreCurrentFocus = false})
```

返回如果焦点正向后遍历且当前没有焦点时应获得焦点的节点。

返回的节点是如果焦点正向后遍历（即使用 [previous]）且 `currentNode` 所属的最近 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 中当前没有焦点时应获得焦点的节点。

如果未给定 `ignoreCurrentFocus` 或其为 false，此函数将返回 `currentNode` 最近作用域的 [FocusScopeNode.focusedChild]（如果已设置），否则返回 [sortDescendants] 中的最后一个节点，如果没有子孙节点，则返回给定的 `currentNode`。

如果 `ignoreCurrentFocus` 为 true，则该算法返回 [sortDescendants] 中的最后一个节点，如果没有子孙节点，则返回给定的 `currentNode`。

另请参阅：

- [previous]，被调用以将焦点移动到上一个节点的函数。
- [DirectionalFocusTraversalPolicyMixin.findFirstFocusInDirection]，一个用于查找特定方向上第一个可获得焦点组件的函数。

### findFirstFocusInDirection()

```dart
FocusNode? findFirstFocusInDirection(FocusNode currentNode, TraversalDirection direction)
```

如果 `currentNode` 所属的作用域中当前没有焦点，返回给定 `direction` 上应获得焦点的第一个节点。

这通常由 [inDirection] 用于确定在没有节点当前获得焦点时调用它应使哪个节点获得焦点。

### invalidateScopeData()

```dart
void invalidateScopeData(FocusScopeNode node)
```

清除此对象关联的给定 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的数据。

用于指示焦点策略已更改其模式，因此应使策略缓存的任何数据失效。例如，更改焦点移动的方向，或从方向性导航模式更改为下一个/上一个导航模式。

默认实现不执行任何操作。

### changedScope()

```dart
void changedScope({FocusNode? node, FocusScopeNode? oldScope})
```

每当给定的 [node] 被重新设置父节点到一个新的作用域时调用此方法，以便该策略有机会更新或使其为该节点维护的每个作用域的任何缓存数据失效。

[oldScope] 是此节点先前所属的作用域（如果有）。

默认实现不执行任何操作。

### next()

```dart
bool next(FocusNode currentNode)
```

在包含给定 [currentNode] 的焦点作用域中，使下一个组件获得焦点。

这应该通过检查节点树来确定应获得焦点的下一个节点是什么，然后对选定的节点调用 [FocusNode.requestFocus]。

如果成功找到节点并请求了焦点，则返回 true。

### previous()

```dart
bool previous(FocusNode currentNode)
```

在包含给定 [currentNode] 的焦点作用域中，使上一个组件获得焦点。

这应该通过检查节点树来确定应获得焦点的上一个节点是什么，然后对选定的节点调用 [FocusNode.requestFocus]。

如果成功找到节点并请求了焦点，则返回 true。

### inDirection()

```dart
bool inDirection(FocusNode currentNode, TraversalDirection direction)
```

在包含给定 [currentNode] 的焦点作用域中，使给定 [direction] 上的下一个组件获得焦点。

这应该通过检查节点树来确定给定 [direction] 上应获得焦点的下一个节点是什么，然后对选定的节点调用 [FocusNode.requestFocus]。

如果成功找到节点并请求了焦点，则返回 true。

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

将给定的 `descendants` 排序为焦点顺序。

子类应重写此方法，以实现 [next] 和 [previous] 使用的不同排序方式。如果返回的可迭代对象省略了给定作用域的某个子孙节点，则用户将无法使用下一个/上一个键盘遍历到达该节点。

用于发起遍历的节点（传递给 [next] 或 [previous] 的节点）作为 `currentNode` 传入。

在列表中保留当前节点是该算法能够确定哪些节点与当前节点相邻的原因。如果从列表中移除了 `currentNode`，则调用 [next] 或 [previous] 时焦点将保持不变，并且它们将返回 false。

这不用于方向性焦点（[inDirection]），仅用于确定 [next] 和 [previous] 的焦点顺序。

在实现此函数的重写时，请确保在排序项目时使用 [mergeSort](https://www.yuque.com/thyname/flutter.foundation/mergesort) 而不是 Dart 的默认列表排序算法，因为默认算法不是稳定的（被认为相等的项目可能以任意顺序出现，并在多次排序之间改变位置），而 [mergeSort](https://www.yuque.com/thyname/flutter.foundation/mergesort) 是稳定的。

# DirectionalFocusTraversalPolicyMixin

```dart
mixin DirectionalFocusTraversalPolicyMixin on FocusTraversalPolicy {}
```

一个混入类，提供了在特定方向上查找节点的实现。

这可以混入到其他仅想实现新的下一个/上一个策略的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 实现中。

由于导航顺序中的滞后现象是不可取的，此实现在受影响的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的策略数据上维护了一个先前访问位置的栈。如果先前的方向与当前方向相反，则该策略将请求先前获得焦点的节点获得焦点。改变到当前方向或其相反方向以外的另一个方向将清空该栈。

例如，如果焦点向下、向下、向下移动，然后向上、向上、向上移动，它将在两个方向上遵循相同的组件路径。但是，如果它向下、向下、向下、向左、向右移动，然后向上、向上、向上移动，由于改变移动轴会重置历史记录，它在向上移动时可能不会遵循与向下移动时相同的路径。

此类实现了一种算法，该算法考虑沿移动方向延伸的一个带状区域，其宽度或高度（取决于方向）为当前获得焦点组件的宽度或高度，并在该带状区域内沿移动方向查找最近的组件。如果在该带状区域内未找到任何内容，则会选取在垂直方向上与该带状区域边缘最接近的组件。如果两个带状区域外的组件与该带状区域的距离相同，则会选取沿移动方向最近的那个。当到达 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 指定方向的边缘时，会根据 [FocusScopeNode.directionalTraversalEdgeBehavior] 采取不同的行为。对于 [TraversalEdgeBehavior.closedLoop]，该算法将在带状区域内重新选择相反方向上最远的节点。对于 [TraversalEdgeBehavior.parentScope]，该带状区域将扩展到父 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，如果它在父作用域中仍然是边缘节点，则会根据父作用域的 [FocusScopeNode.directionalTraversalEdgeBehavior] 继续查找。如果当前作用域上方没有父作用域，则回退到 [TraversalEdgeBehavior.closedLoop] 行为。对于 [TraversalEdgeBehavior.leaveFlutterView]，焦点将丢失。对于 [TraversalEdgeBehavior.stop]，当前获得焦点的元素将保持不变。

此算法的目标是选取一个（对用户而言）不会显得沿错误轴遍历的组件，这可能是仅按一个轴上的距离对组件进行排序时发生的情况，但也要在某个方向上跳转到下一个逻辑组件时不跳过任何组件。

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，有关焦点系统的说明。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种依赖组件创建顺序来描述遍历顺序的策略。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种根据当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 描述为自然"阅读顺序"的策略。
- [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy)，一种使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件显式描述顺序的策略。

### invalidateScopeData()

```dart
void invalidateScopeData(FocusScopeNode node)
```

### changedScope()

```dart
void changedScope({FocusNode? node, FocusScopeNode? oldScope})
```

### findFirstFocusInDirection()

```dart
FocusNode? findFirstFocusInDirection(FocusNode currentNode, TraversalDirection direction)
```

### inDirection()

```dart
bool inDirection(FocusNode currentNode, TraversalDirection direction)
```

在包含 [currentNode] 的 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 中，使给定 [direction] 上的下一个组件获得焦点。

这通过检查节点树来确定给定 [direction] 上应获得焦点的下一个节点是什么，然后对其调用 [FocusNode.requestFocus]。

如果成功找到节点并请求了焦点，则返回 true。

在受影响的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的策略数据上维护了一个先前访问位置的栈。如果先前的方向与当前方向相反，则该策略将请求先前获得焦点的节点获得焦点。改变到当前方向或其相反方向以外的另一个方向将清空该栈。

如果此函数在被子类调用时返回 true，则该子类应返回 true，并且不从任何节点请求焦点。

# WidgetOrderTraversalPolicy

```dart
class WidgetOrderTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

一个按组件层次结构顺序遍历焦点顺序的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

当所需的顺序是组件在组件层次结构中创建的顺序时，使用此策略。

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，有关焦点系统的说明。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种根据当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 描述为自然"阅读顺序"的策略。
- [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin)，一个实现按方向进行焦点遍历的混入类。
- [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy)，一种使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件显式描述顺序的策略。

### WidgetOrderTraversalPolicy()

```dart
WidgetOrderTraversalPolicy({void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

构造一个基于组件层次结构顺序对组件进行键盘遍历排序的遍历策略。

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# ReadingOrderTraversalPolicy

```dart
class ReadingOrderTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

按"阅读顺序"遍历焦点顺序。

默认情况下，阅读顺序遍历沿阅读方向进行，然后向下，使用以下算法：

1.  查找屏幕上 `top` 值最高的节点矩形。
2.  查找与该最高矩形的上下边缘所定义的无限水平带状区域相交的所有其他节点。
3.  在上述发现的节点中，选取阅读顺序上最靠前的节点。

它使用封闭 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 上下文中环境的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 来确定哪个方向是"阅读顺序"。

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，有关焦点系统的说明。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种依赖组件创建顺序来描述遍历顺序的策略。
- [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin)，一个实现按方向进行焦点遍历的混入类。
- [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy)，一种使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件显式描述顺序的策略。

### ReadingOrderTraversalPolicy()

```dart
ReadingOrderTraversalPolicy({void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

构造一个按"阅读顺序"对组件进行排序的遍历策略。

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### sort()

```dart
Iterable<FocusNode> sort(Iterable<FocusNode> nodes)
```

将输入的焦点节点按阅读顺序排序。

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# FocusOrder

```dart
abstract class FocusOrder with Diagnosticable implements Comparable<FocusOrder> {}
```

[OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 遍历所有排序方式的基类。

{@template flutter.widgets.FocusOrder.comparable} 只有相同类型的顺序才具有可比性。如果同一 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 中的一组组件包含彼此不可比较的顺序，将触发断言，因为此类键之间的顺序未定义。为避免冲突，请使用 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 将顺序相似的组件分组在一起。

重写时，必须重写 [FocusOrder.doCompare] 而不是 [FocusOrder.compareTo]，后者会调用 [FocusOrder.doCompare] 来执行实际的比较。{@endtemplate}

另请参阅：

- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder)，一个为组件子树分配顺序供 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 使用的组件。
- [NumericFocusOrder](https://www.yuque.com/thyname/flutter.widgets/numericfocusorder)，一种用 `double` 描述其顺序的焦点顺序。
- [LexicalFocusOrder](https://www.yuque.com/thyname/flutter.widgets/lexicalfocusorder)，一种为 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件分配基于字符串的词法遍历顺序的焦点顺序。

### FocusOrder()

```dart
FocusOrder()
```

抽象 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便它们可以在 const 表达式中使用。

### compareTo()

```dart
int compareTo(FocusOrder other)
```

将此对象与另一个 [Comparable](https://www.yuque.com/thyname/dart.core/comparable) 进行比较。

重写 [FocusOrder](https://www.yuque.com/thyname/flutter.widgets/focusorder) 时，应实现 [doCompare] 而不是此函数来执行实际的比较。

返回一个类似 [Comparator](https://www.yuque.com/thyname/dart.core/comparator) 在比较 `this` 与 [other] 时的值。即，如果 `this` 排在 [other] 之前，则返回负整数；如果 `this` 排在 [other] 之后，则返回正整数；如果 `this` 和 [other] 排序相同，则返回零。

[other] 参数必须是可与此对象比较的值。

### doCompare()

```dart
int doCompare(FocusOrder other)
```

由 [compareTo] 调用的子类实现，用于比较顺序。

参数保证与此对象的 [runtimeType] 相同。

如果此对象在排序中先于 `other` 参数，该方法应返回一个负数；如果排在 `other` 之后，应返回一个正数。返回零会导致系统回退到由 [OrderedTraversalPolicy.secondary] 定义的次级排序顺序。

# NumericFocusOrder

```dart
class NumericFocusOrder extends FocusOrder {}
```

可以赋给 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件，为使用 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 定义键盘遍历顺序的组件子树分配一个数字顺序。

{@macro flutter.widgets.FocusOrder.comparable}

另请参阅：

- [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder)，一个为组件子树分配顺序供 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 使用的组件。

### NumericFocusOrder()

```dart
NumericFocusOrder(double order)
```

创建一个以数字方式描述焦点遍历顺序的对象。

### order

```dart
double order
```

使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 分配给组件子树的数字顺序。

确定此组件在由焦点策略遍历的组件序列中的位置。

数值较低的先被遍历。

### doCompare()

```dart
int doCompare(NumericFocusOrder other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LexicalFocusOrder

```dart
class LexicalFocusOrder extends FocusOrder {}
```

可以赋给 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件，使用字符串为使用 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 定义键盘遍历顺序的组件子树分配一个词法顺序。

这使用 Dart 的默认字符串比较对字符串进行排序，该比较不是特定于语言区域的。

{@macro flutter.widgets.FocusOrder.comparable}

另请参阅：

- [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder)，一个为组件子树分配顺序供 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 使用的组件。

### LexicalFocusOrder()

```dart
LexicalFocusOrder(String order)
```

创建一个以词法方式描述焦点遍历顺序的对象。

### order

```dart
String order
```

使用 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 定义分配给组件子树的词法顺序的字符串。

确定此组件在由焦点策略遍历的组件序列中的位置。

词法值较低的先被遍历（例如，'a' 排在 'z' 之前）。

### doCompare()

```dart
int doCompare(LexicalFocusOrder other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OrderedTraversalPolicy

```dart
class OrderedTraversalPolicy extends FocusTraversalPolicy with DirectionalFocusTraversalPolicyMixin {}
```

一个按最近的祖先 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件中的显式顺序对节点进行排序的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

{@macro flutter.widgets.FocusOrder.comparable}

{@tool dartpad} 此示例展示了如何为组件分配遍历顺序。在此示例中，焦点顺序从右下角（"One" 按钮）到左上角（"Six" 按钮）。

** See code in examples/api/lib/widgets/focus_traversal/ordered_traversal_policy.0.dart ** {@end-tool}

另请参阅：

- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种依赖组件创建顺序来描述遍历顺序的策略。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种根据当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 描述为自然"阅读顺序"的策略。
- [NumericFocusOrder](https://www.yuque.com/thyname/flutter.widgets/numericfocusorder)，一种为 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件分配数字遍历顺序的焦点顺序。
- [LexicalFocusOrder](https://www.yuque.com/thyname/flutter.widgets/lexicalfocusorder)，一种为 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件分配基于字符串的词法遍历顺序的焦点顺序。
- [FocusOrder](https://www.yuque.com/thyname/flutter.widgets/focusorder)，所有类型焦点遍历排序的抽象基类。

### OrderedTraversalPolicy()

```dart
OrderedTraversalPolicy({FocusTraversalPolicy? secondary, void Function(FocusNode, {double? alignment, ScrollPositionAlignmentPolicy? alignmentPolicy, InvalidType curve, Duration? duration})? requestFocusCallback})
```

构造一个基于显式顺序对组件进行键盘遍历排序的遍历策略。

如果 [secondary] 为 null，将默认为 [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)。

### secondary

```dart
FocusTraversalPolicy? secondary
```

当某个节点没有分配顺序，或者多个节点具有相同的顺序时使用的策略。

如果未设置，默认为 [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)。

此策略决定了被评估为具有相同顺序（包括那些未指定顺序的节点）的节点的次级排序顺序。

未指定顺序的节点将排在具有显式顺序的节点之后。

### sortDescendants()

```dart
Iterable<FocusNode> sortDescendants(Iterable<FocusNode> descendants, FocusNode currentNode)
```

# FocusTraversalOrder

```dart
class FocusTraversalOrder extends InheritedWidget {}
```

一个描述其子树应以何种顺序遍历的继承组件。

{@macro flutter.widgets.FocusOrder.comparable}

组件的顺序由特定上下文中 [FocusTraversalOrder.of] 返回的 [FocusOrder](https://www.yuque.com/thyname/flutter.widgets/focusorder) 确定。

### FocusTraversalOrder()

```dart
FocusTraversalOrder({dynamic key, required FocusOrder order, required Widget child})
```

创建一个用于描述 [child] 子树焦点顺序的继承组件。

### order

```dart
FocusOrder order
```

此 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 的组件子孙节点的顺序。

### of()

```dart
FocusOrder of(BuildContext context)
```

在最近的祖先 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件中查找 [FocusOrder](https://www.yuque.com/thyname/flutter.widgets/focusorder)。

它不会创建重建依赖关系，因为更改遍历顺序不会改变组件树，因此不需要因顺序更改而重建任何内容。

如果不存在 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 祖先，或者该顺序为 null，则在调试模式下将触发断言，在发布模式下将抛出异常。

### maybeOf()

```dart
FocusOrder? maybeOf(BuildContext context)
```

在最近的祖先 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 组件中查找 [FocusOrder](https://www.yuque.com/thyname/flutter.widgets/focusorder)。

它不会创建重建依赖关系，因为更改遍历顺序不会改变组件树，因此不需要因顺序更改而重建任何内容。

如果不存在 [FocusTraversalOrder](https://www.yuque.com/thyname/flutter.widgets/focustraversalorder) 祖先，或者该顺序为 null，则返回 null。

### updateShouldNotify()

```dart
bool updateShouldNotify(InheritedWidget oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FocusTraversalGroup

```dart
class FocusTraversalGroup extends StatefulWidget {}
```

一个描述其子孙节点所继承的焦点遍历策略的组件，将它们分组到一个单独的遍历分组中。

一个遍历分组在被遍历算法排序时被视为一个整体实体，因此它可以用于分隔组件树中需要使用不同算法和/或排序顺序进行排序的不同部分（当使用 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 时）。

在此分组内，将使用给定的 [policy] 对元素进行排序。该分组本身将使用父分组的策略进行排序。

默认情况下，使用 [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy) 按阅读顺序遍历。

要阻止该分组的成员获得焦点，请将 [descendantsAreFocusable] 属性设置为 false。

{@tool dartpad} 此示例展示了三行按钮，每行都用 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 分组，每个分组具有不同的遍历顺序策略。使用 tab 遍历查看它们被遍历的顺序。第一行遵循数字顺序，第二行遵循词法顺序（顺序为从右到左遍历），第三行忽略分配给它的数字顺序，按组件顺序遍历。

** See code in examples/api/lib/widgets/focus_traversal/focus_traversal_group.0.dart ** {@end-tool}

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，有关焦点系统的说明。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种依赖组件创建顺序来描述遍历顺序的策略。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种根据当前 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 描述为自然"阅读顺序"的策略。
- [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin)，一个实现按方向进行焦点遍历的混入类。

### FocusTraversalGroup()

```dart
FocusTraversalGroup({dynamic key, FocusTraversalPolicy? policy, bool descendantsAreFocusable = true, bool descendantsAreTraversable = true, void Function(FocusNode)? onFocusNodeCreated, required Widget child})
```

创建一个 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 对象。

### policy

```dart
FocusTraversalPolicy policy
```

使用键盘遍历时，用于将焦点从一个焦点节点移动到另一个焦点节点的策略。

如果未指定，使用 [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy) 按阅读顺序遍历。

另请参阅：

- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，用于施加遍历顺序策略的 API。
- [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)，一种按组件添加到组件树的顺序遍历节点的遍历策略。
- [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)，一种按组件树中定义的阅读顺序遍历节点，然后从上到下的遍历策略。

### descendantsAreFocusable

```dart
bool descendantsAreFocusable
```

{@macro flutter.widgets.Focus.descendantsAreFocusable}

### descendantsAreTraversable

```dart
bool descendantsAreTraversable
```

{@macro flutter.widgets.Focus.descendantsAreTraversable}

### child

```dart
Widget child
```

此 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 的子组件。

{@macro flutter.widgets.ProxyWidget.child}

### onFocusNodeCreated

```dart
void Function(FocusNode)? onFocusNodeCreated
```

当此组件的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 被创建时调用。

### maybeOfNode()

```dart
FocusTraversalPolicy? maybeOfNode(FocusNode node)
```

返回适用于给定 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 最近祖先的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

如果没有适用于给定 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 祖先，将返回 null。

[FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 是通过在组件树中引入 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 来设置的，它会将策略与最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件下方的焦点树关联。

此函数与 [maybeOf] 的不同之处在于，它接受一个 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，并且只遍历焦点树以确定生效的策略。与此函数不同，[maybeOf] 函数接受一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，并首先向上遍历组件树以查找最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件，然后使用与该组件关联的焦点节点调用此函数以确定生效的策略。

### of()

```dart
FocusTraversalPolicy of(BuildContext context)
```

给定一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，返回适用于最近祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

如果找不到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 祖先，或者没有适用于关联 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，将在调试模式下抛出 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)，在发布模式下抛出空检查异常。

{@template flutter.widgets.focus_traversal.FocusTraversalGroup.of} 此函数查找最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)（或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope)）组件，并使用其 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)（或 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)）向上遍历焦点树，以查找适用于该节点的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

调用此函数不会创建重建依赖关系，因为更改遍历顺序不会改变组件树，因此不需要因顺序更改而重建任何内容。

[FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 是通过在组件树中引入 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 来设置的，它会将策略与最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件下方的焦点树关联。{@endtemplate}

另请参阅：

- [maybeOf]，一个类似的函数，如果找不到 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 祖先，将返回 null。
- [maybeOfNode]，一个使用给定 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 查找策略的函数，如果没有适用的策略，将返回 null。

### maybeOf()

```dart
FocusTraversalPolicy? maybeOf(BuildContext context)
```

给定一个 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，返回适用于最近祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，如果没有则返回 null。

如果找不到祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件，或找不到适用于该节点的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，将返回 null。

{@macro flutter.widgets.focus_traversal.FocusTraversalGroup.of}

另请参阅：

- [maybeOfNode]，一个使用给定 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 查找策略的类似函数。
- [of]，一个类似的函数，如果没有适用的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，将抛出异常。

### createState()

```dart
State<FocusTraversalGroup> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RequestFocusIntent

```dart
class RequestFocusIntent extends Intent {}
```

一个与 [RequestFocusAction](https://www.yuque.com/thyname/flutter.widgets/requestfocusaction) 一起使用的意图，提供应被赋予焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

### RequestFocusIntent()

```dart
RequestFocusIntent(FocusNode focusNode, {TraversalRequestFocusCallback? requestFocusCallback})
```

创建一个与 [RequestFocusAction](https://www.yuque.com/thyname/flutter.widgets/requestfocusaction) 一起使用的意图。

{@macro flutter.widgets.FocusTraversalPolicy.requestFocusCallback}

### requestFocusCallback

```dart
TraversalRequestFocusCallback requestFocusCallback
```

用于将焦点移动到节点 [focusNode] 的回调。默认情况下，它会请求该节点的焦点，并确保该节点在可滚动组件中可见（如果适用）。

### focusNode

```dart
FocusNode focusNode
```

将获得焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

# RequestFocusAction

```dart
class RequestFocusAction extends Action<RequestFocusIntent> {}
```

一个在其 [RequestFocusIntent](https://www.yuque.com/thyname/flutter.widgets/requestfocusintent) 中所给定的节点上请求焦点的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。

可以通过如下方式调用 [Action.invoke] 来使用此操作请求特定节点的焦点：

```dart
Actions.invoke(context, RequestFocusIntent(focusNode));
```

其中 `focusNode` 是将请求焦点的节点。

以此方式请求焦点与直接调用 [FocusNode.requestFocus] 的区别在于，它将使用与最近的 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件中注册的、与 [RequestFocusIntent](https://www.yuque.com/thyname/flutter.widgets/requestfocusintent) 关联的 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 来发出请求，而不是仅仅直接请求焦点。这使得该操作可以具有额外的副作用，例如日志记录，或撤销和重做功能。

此 [RequestFocusAction](https://www.yuque.com/thyname/flutter.widgets/requestfocusaction) 类是 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中与 [RequestFocusIntent](https://www.yuque.com/thyname/flutter.widgets/requestfocusintent) 关联的默认操作。它请求焦点。你可以使用自己的 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件重新定义关联的操作。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### invoke()

```dart
void invoke(RequestFocusIntent intent)
```

# NextFocusIntent

```dart
class NextFocusIntent extends Intent {}
```

一个绑定到 [NextFocusAction](https://www.yuque.com/thyname/flutter.widgets/nextfocusaction) 的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)，将焦点移动到焦点遍历顺序中的下一个可获得焦点的节点。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### NextFocusIntent()

```dart
NextFocusIntent()
```

创建一个与 [NextFocusAction](https://www.yuque.com/thyname/flutter.widgets/nextfocusaction) 一起使用的意图。

# NextFocusAction

```dart
class NextFocusAction extends Action<NextFocusIntent> {}
```

一个将焦点移动到焦点顺序中下一个可获得焦点节点的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。

此操作是为 [NextFocusIntent](https://www.yuque.com/thyname/flutter.widgets/nextfocusintent) 注册的默认操作，默认情况下在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中绑定到 [LogicalKeyboardKey.tab] 键。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### invoke()

```dart
bool invoke(NextFocusIntent intent)
```

尝试将焦点传递给下一个组件。

如果由于调用此操作而使某个组件获得焦点，则返回 true。

当遍历到达末尾且引擎必须将焦点传递给平台 UI 时，返回 false。

### toKeyEventResult()

```dart
KeyEventResult toKeyEventResult(NextFocusIntent intent, bool invokeResult)
```

# PreviousFocusIntent

```dart
class PreviousFocusIntent extends Intent {}
```

一个绑定到 [PreviousFocusAction](https://www.yuque.com/thyname/flutter.widgets/previousfocusaction) 的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)，将焦点移动到焦点遍历顺序中的上一个可获得焦点的节点。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### PreviousFocusIntent()

```dart
PreviousFocusIntent()
```

创建一个与 [PreviousFocusAction](https://www.yuque.com/thyname/flutter.widgets/previousfocusaction) 一起使用的意图。

# PreviousFocusAction

```dart
class PreviousFocusAction extends Action<PreviousFocusIntent> {}
```

一个将焦点移动到焦点顺序中上一个可获得焦点节点的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。

此操作是为 [PreviousFocusIntent](https://www.yuque.com/thyname/flutter.widgets/previousfocusintent) 注册的默认操作，默认情况下在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中绑定到 [LogicalKeyboardKey.tab] 键与 [LogicalKeyboardKey.shift] 键的组合。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### invoke()

```dart
bool invoke(PreviousFocusIntent intent)
```

尝试将焦点传递给上一个组件。

如果由于调用此操作而使某个组件获得焦点，则返回 true。

当遍历到达开头且引擎必须将焦点传递给平台 UI 时，返回 false。

### toKeyEventResult()

```dart
KeyEventResult toKeyEventResult(PreviousFocusIntent intent, bool invokeResult)
```

# DirectionalFocusIntent

```dart
class DirectionalFocusIntent extends Intent {}
```

一个表示移动到给定 [direction] 上下一个可获得焦点节点的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

这是在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中默认绑定到 [LogicalKeyboardKey.arrowUp]、[LogicalKeyboardKey.arrowDown]、[LogicalKeyboardKey.arrowLeft] 和 [LogicalKeyboardKey.arrowRight] 键的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)，并具有相应的关联方向。

有关焦点遍历的更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

### DirectionalFocusIntent()

```dart
DirectionalFocusIntent(TraversalDirection direction, {bool ignoreTextFields = true})
```

创建一个用于在给定 [direction] 上移动焦点的意图。

### direction

```dart
TraversalDirection direction
```

当关联的 [DirectionalFocusAction](https://www.yuque.com/thyname/flutter.widgets/directionalfocusaction) 被调用时，查找下一个可获得焦点节点的方向。

### ignoreTextFields

```dart
bool ignoreTextFields
```

如果为 true，则当接收按键的焦点节点是文本字段时，在文本字段内发生的方向性焦点操作将不会执行。

默认为 true。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DirectionalFocusAction

```dart
class DirectionalFocusAction extends Action<DirectionalFocusIntent> {}
```

一个将焦点移动到由关联的 [DirectionalFocusIntent.direction] 配置的方向上的可获得焦点节点的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。

这是与 [DirectionalFocusIntent](https://www.yuque.com/thyname/flutter.widgets/directionalfocusintent) 关联的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)，默认情况下在 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 中绑定到 [LogicalKeyboardKey.arrowUp]、[LogicalKeyboardKey.arrowDown]、[LogicalKeyboardKey.arrowLeft] 和 [LogicalKeyboardKey.arrowRight] 键，并具有相应的关联方向。

### DirectionalFocusAction()

```dart
DirectionalFocusAction()
```

创建一个 [DirectionalFocusAction](https://www.yuque.com/thyname/flutter.widgets/directionalfocusaction)。

### DirectionalFocusAction.forTextField()

```dart
DirectionalFocusAction.forTextField()
```

创建一个忽略 `ignoreTextFields` 字段为 true 的 [DirectionalFocusIntent](https://www.yuque.com/thyname/flutter.widgets/directionalfocusintent) 的 [DirectionalFocusAction](https://www.yuque.com/thyname/flutter.widgets/directionalfocusaction)。

### invoke()

```dart
void invoke(DirectionalFocusIntent intent)
```

# ExcludeFocusTraversal

```dart
class ExcludeFocusTraversal extends StatelessWidget {}
```

一个控制此组件的子孙节点是否可被遍历的组件。

不影响子孙节点的 [FocusNode.skipTraversal] 值。

另请参阅：

- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个用于在组件树中添加和管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的组件。
- [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus)，一个将其子孙节点排除在可获得焦点之外的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于对组件进行焦点遍历分组的组件，也可以通过设置其 `descendantsAreFocusable` 属性以与此组件相同的方式使用。

### ExcludeFocusTraversal()

```dart
ExcludeFocusTraversal({dynamic key, bool excluding = true, required Widget child})
```

[ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal) 组件的 const 构造函数。

### excluding

```dart
bool excluding
```

如果为 true，将使此组件的子孙节点不可遍历。

默认为 true。

不影响子孙节点的 [FocusNode.skipTraversal] 值。

另请参阅：

- [Focus.descendantsAreTraversable]，[Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件中控制相同属性的属性。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它有一个 `descendantsAreFocusable` 参数，可有条件地阻止子树获得焦点。

### child

```dart
Widget child
```

此 [ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal) 的子组件。

{@macro flutter.widgets.ProxyWidget.child}
