@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart';

# debugFocusChanges

```dart
bool debugFocusChanges
```

设置为 true 将导致在发生焦点变化时进行大量的日志记录。

可用于调试焦点问题：每次焦点变化时，都会打印焦点树，并记录焦点请求和其他焦点操作的日志。

# KeyEventResult

```dart
enum KeyEventResult {}
```

一个枚举，描述 [FocusOnKeyCallback](https://www.yuque.com/thyname/flutter.widgets/focusonkeycallback) 或 [FocusOnKeyEventCallback](https://www.yuque.com/thyname/flutter.widgets/focusonkeyeventcallback) 应如何处理按键事件。

按键事件已被处理，不应再传播给其他按键事件处理程序。

按键事件未被处理，应继续传播给其他按键事件处理程序，即使是非 Flutter 的处理程序也是如此。

按键事件未被处理，但该按键事件不应传播给其他按键事件处理程序。

它将被返回给平台嵌入层，以传播给文本字段和平台上的非 Flutter 按键事件处理程序。

# combineKeyEventResults()

```dart
KeyEventResult combineKeyEventResults(Iterable<KeyEventResult> results)
```

合并多个 [FocusOnKeyCallback](https://www.yuque.com/thyname/flutter.widgets/focusonkeycallback) 或 [FocusOnKeyEventCallback](https://www.yuque.com/thyname/flutter.widgets/focusonkeyeventcallback) 所返回的结果。

如果任意一个回调返回 [KeyEventResult.handled]，则该节点认为消息已被处理；否则，如果任意一个回调返回 [KeyEventResult.skipRemainingHandlers]，则该节点会跳过剩余的处理程序但不阻止平台进行处理；否则该节点被忽略。

# FocusOnKeyCallback

```dart
typedef FocusOnKeyCallback = KeyEventResult Function(FocusNode node, RawKeyEvent event)
```

[Focus.onKey] 和 [FocusScope.onKey] 用于接收按键事件的回调签名。

此类回调已废弃，将在未来的日期移除。请改用 [FocusOnKeyEventCallback](https://www.yuque.com/thyname/flutter.widgets/focusonkeyeventcallback) 及相关 API。

[node] 是接收该事件的节点。

返回一个 [KeyEventResult](https://www.yuque.com/thyname/flutter.widgets/keyeventresult)，描述按键事件是如何以及是否被处理的。

# FocusOnKeyEventCallback

```dart
typedef FocusOnKeyEventCallback = KeyEventResult Function(FocusNode node, KeyEvent event)
```

[Focus.onKeyEvent] 和 [FocusScope.onKeyEvent] 用于接收按键事件的回调签名。

[node] 是接收该事件的节点。

返回一个 [KeyEventResult](https://www.yuque.com/thyname/flutter.widgets/keyeventresult)，描述按键事件是如何以及是否被处理的。

# OnKeyEventCallback

```dart
typedef OnKeyEventCallback = KeyEventResult Function(KeyEvent event)
```

[FocusManager.addEarlyKeyEventHandler] 和 [FocusManager.addLateKeyEventHandler] 用于的回调签名。

`event` 参数是一个正被发送给该回调以进行处理的 [KeyEvent](https://www.yuque.com/thyname/flutter.services/keyevent)。

[KeyEventResult](https://www.yuque.com/thyname/flutter.widgets/keyeventresult) 返回值指示事件是否将继续传播。如果返回的值是 [KeyEventResult.handled] 或 [KeyEventResult.skipRemainingHandlers]，则事件将不再继续传播。

# FocusAttachment

```dart
class FocusAttachment {}
```

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的一个附加点。

除非要从头构建类似于 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件的东西，否则很少需要使用 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment)。

创建后，[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 必须通过其 _宿主_ [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 借助 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 对象附加到组件树。[FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 由托管 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 或 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 拥有。每个 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 可以有多个 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment)，但该节点在任意时刻只会附加到其中一个上。

此附加是通过调用 [FocusNode.attach] 创建的，通常在宿主组件的 [State.initState] 方法中调用。如果组件被更新为具有不同的焦点节点，则需要在 [State.didUpdateWidget] 中附加新节点，此前需先在之前的 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 上调用 [detach]。一旦分离，该附加点即失效，将不再通过 [reparent] 对 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 进行更改。

如果没有这些附加点，则有可能在构建阶段使一个焦点节点同时附加到组件树的多个部分。

### isAttached

```dart
bool get isAttached
```

如果关联的节点已附加到此附加点，则返回 true。

节点有可能已附加到组件树，但尚未被放入焦点树中（即，在焦点树中还没有父节点）。

### detach()

```dart
void detach()
```

将此附加点关联的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 从焦点树中分离，并断开其与此附加点的连接。

调用 [FocusNode.dispose] 也会自动分离该节点。

### reparent()

```dart
void reparent({FocusNode? parent})
```

确保附加在此附加点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 具有正确的父节点，如有必要则进行更改。

如果给定，确保给定的 [parent] 节点是附加在此附加点的节点的父节点，如有必要则进行更改。但是，通常不需要提供显式的父节点，因为 [reparent] 会使用 [Focus.of] 来确定附加到该点的 [FocusNode.attach] 中给定上下文的正确父节点。

如果 [isAttached] 为 false，则调用此方法不执行任何操作。

每当关联的组件被重建时都应调用此方法，以维护焦点层次结构。

托管 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 应在其 [State.build] 或 [State.didChangeDependencies] 方法中对其托管的节点调用此方法，以防该组件从树中的一个位置移动到具有不同 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 或上下文的另一个位置。

当不使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件来构建焦点树时，或者需要显式提供父节点时（这两种情况都不常见），必须提供可选的 [parent] 参数。

# UnfocusDisposition

```dart
enum UnfocusDisposition {}
```

描述调用 [FocusNode.unfocus] 后应该发生什么。

另请参阅：

- [FocusNode.unfocus]，它将此枚举作为其 `disposition` 参数。

将焦点赋予此节点最近的可获得焦点的封闭作用域，但不像 [previouslyFocusedChild] 那样向下查找叶子 [FocusScopeNode.focusedChild]。

以这种方式让作用域获得焦点，会在该封闭作用域获得焦点时清除其 [FocusScopeNode.focusedChild] 历史记录。因此，在取消焦点之后调用诸如 [FocusNode.nextFocus] 之类的遍历方法，将导致 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 选择它认为应在该作用域中排在首位的节点。

这是 [FocusNode.unfocus] 的默认处置方式。

将焦点赋予此节点最近的可获得焦点的封闭作用域中先前获得焦点的子节点。

如果没有先前获得焦点的子节点，则等同于使用 [scope] 处置方式。

以此处置方式取消焦点将导致 [FocusNode.unfocus] 向上遍历树到最近的可获得焦点的封闭作用域，然后开始向下遍历树，在其 [FocusScopeNode.focusedChild] 处查找获得焦点的子节点。

如果 [FocusScopeNode.focusedChild] 是一个作用域，则查找其 [FocusScopeNode.focusedChild]，依此类推，直到找到不是作用域的叶子 [FocusScopeNode.focusedChild]，或者如果找不到，则找到一个没有获得焦点子节点的叶子作用域。

# FocusNode

```dart
class FocusNode with DiagnosticableTreeMixin, ChangeNotifier {}
```

一个可供有状态组件使用以获取键盘焦点和处理键盘事件的对象。

_请参阅 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件，它们分别是管理各自 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 和 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的实用组件。如果它们不合适，可以直接管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，但这种做法很少见。_

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 是持久对象，构成一个 _焦点树_，它是层次结构中对焦点感兴趣的组件的表示。如果需要将一个焦点节点从 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的祖先传入以控制该祖先所属子组件的焦点，或者组件子系统未被使用，或者 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件提供的控制不充分，则可能需要创建一个焦点节点。

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 被组织成 _作用域_（见 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)），它们构成了限制遍历到一组节点的节点子树。在一个作用域内，最近获得焦点的节点会被记住，如果一个节点获得焦点后又失去焦点，则先前的节点会重新获得焦点。

可以使用 [parent]、[children]、[ancestors] 和 [descendants] 访问器遍历焦点节点层次结构。

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 是 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier)，因此可以注册一个监听器，以便在焦点变化时接收通知。当 [skipTraversal]、[canRequestFocus]、[descendantsAreFocusable] 和 [descendantsAreTraversable] 属性被更新时，监听器也会收到通知。如果正在使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件来管理节点，可以考虑通过调用 [Focus.of] 或 [FocusScope.of] 来建立 [InheritedWidget](https://www.yuque.com/thyname/flutter.widgets/inheritedwidget) 依赖关系。如果仅需要在构建时确定该组件是否已获得焦点，也可以使用 [FocusNode.hasFocus] 来建立类似的依赖关系。

要在调试控制台中查看焦点树，请调用 [debugDumpFocusTree](https://www.yuque.com/thyname/flutter.widgets/debugdumpfocustree)。要以字符串形式获取焦点树，请调用 [debugDescribeFocusTree](https://www.yuque.com/thyname/flutter.widgets/debugdescribefocustree)。

{@template flutter.widgets.FocusNode.lifecycle}

## 生命周期

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)/[FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的生命周期涉及多个参与者。它们由其 _所有者_ 创建和销毁，由其 _宿主_（必须由 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的 [State](https://www.yuque.com/thyname/flutter.widgets/state) 拥有）通过 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 附加、分离和重新设置父节点，并由 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 管理。[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) API 的不同部分适用于这些不同的参与者。

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)（以及因此 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)）是构成 _焦点树_ 一部分的持久对象，它是层次结构中对接收键盘事件感兴趣的组件的稀疏表示。它们必须像其他持久状态一样进行管理，这通常由拥有该节点的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 完成。拥有焦点作用域节点的有状态组件必须从其 [State.dispose] 方法中调用 [dispose]。

创建后，[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 必须通过 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 对象附加到组件树。此附加是通过调用 [attach] 创建的，通常在 [State.initState] 方法中调用。如果托管组件被更新为具有不同的焦点节点，则需要在 [State.didUpdateWidget] 中附加新节点，此前需先在之前的 [FocusAttachment](https://www.yuque.com/thyname/flutter.widgets/focusattachment) 上调用 [FocusAttachment.detach]。

由于 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 构成组件树的稀疏表示，因此每当组件树被重建时都必须对其进行更新。这通常通过调用 [FocusAttachment.reparent] 完成，通常在表示获得焦点区域的组件的 [State.build] 或 [State.didChangeDependencies] 方法中调用，以便可以跟踪分配给 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)（该上下文用于获取 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject)，从而可以确定获得焦点区域的几何形状）。

每次调用 [State.build] 时都创建一个 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 将导致每次构建组件时都失去焦点，这通常不是期望的行为（如果希望失去焦点，请调用 [unfocus]）。

如果（如通常情况）托管的 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 也是该焦点节点的所有者，那么它也会从其 [State.dispose] 中调用 [dispose]（在这种情况下，可以跳过 [FocusAttachment.detach]，因为 dispose 会自动分离）。如果由另一个对象拥有该焦点节点，则该对象必须在使用完该节点后调用 [dispose]。{@endtemplate}

{@template flutter.widgets.FocusNode.keyEvents}

## 按键事件传播

[FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 从 [HardwareKeyboard](https://www.yuque.com/thyname/flutter.services/hardwarekeyboard) 接收按键事件，并将其传递给获得焦点的节点。它从拥有主焦点的节点开始，并调用该节点的 [onKeyEvent] 回调。如果该回调返回 [KeyEventResult.ignored]，表示它未处理该事件，则 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 会移动到该节点的父节点并调用其 [onKeyEvent]。如果该 [onKeyEvent] 返回 [KeyEventResult.handled]，则会停止传播该事件。如果到达根 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)（[FocusManager.rootScope]），该事件将被丢弃。{@endtemplate}

## 焦点遍历

术语 _遍历_（有时称为 _tab 遍历_）指的是按特定顺序（有时也称为 _tab 顺序_，因为 TAB 键通常绑定到移动到下一个组件的操作）将焦点从一个组件移动到下一个组件。

要将焦点赋予 UI 中逻辑上的 _下一个_ 或 _上一个_ 组件，调用 [nextFocus] 或 [previousFocus] 方法。要将焦点赋予特定方向上的组件，调用 [focusInDirection] 方法。

关于什么是 _下一个_ 或 _上一个_ 组件，或者特定方向上的组件的策略，由当前生效的 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 决定。

环境策略是通过在组件层次结构中向上查找 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 组件，并从中获取焦点遍历策略来确定的。不同的焦点节点可以继承不同的策略，因此应用程序的一部分可以按预定义顺序（使用 [OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy)），另一部分可以按阅读顺序（使用 [ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)），具体取决于使用场景。

预定义的策略包括 [WidgetOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/widgetordertraversalpolicy)、[ReadingOrderTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/readingordertraversalpolicy)、[OrderedTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/orderedtraversalpolicy) 和 [DirectionalFocusTraversalPolicyMixin](https://www.yuque.com/thyname/flutter.widgets/directionalfocustraversalpolicymixin)，但也可以基于这些策略构建自定义策略。有关更多信息，请参阅 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)。

{@tool dartpad} 此示例展示了如果不使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件，应如何管理 FocusNode。有关使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件的类似示例，请参阅 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件。

** See code in examples/api/lib/widgets/focus_manager/focus_node.0.dart ** {@end-tool}

另请参阅：

- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 并向其子组件提供焦点信息和操作访问权限的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件。
- [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，一个管理主焦点并向已获得焦点的节点分发按键事件的单例。
- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，一个用于确定如何将焦点移动到其他节点的类。

### FocusNode()

```dart
FocusNode({String? debugLabel, FocusOnKeyCallback? onKey, FocusOnKeyEventCallback? onKeyEvent, bool skipTraversal = false, bool canRequestFocus = true, bool descendantsAreFocusable = true, bool descendantsAreTraversable = true})
```

创建一个焦点节点。

[debugLabel] 在发布版本中会被忽略。

要接收使该节点获得焦点的按键事件，请向 `onKeyEvent` 传入一个监听器。

### skipTraversal

```dart
bool get skipTraversal
```

如果为 true，告知焦点遍历策略在遍历算法中跳过此节点。

这可用于将可获得焦点但不应被遍历到的节点放置在焦点树中，从而使其能够作为焦点链的一部分接收按键事件，但不能通过遍历到达。

这与 [canRequestFocus] 不同，因为它只意味着该节点无法通过遍历到达，而不意味着不能被赋予焦点。它仍然可以被显式地赋予焦点。

### skipTraversal

```dart
set skipTraversal(bool value)
```

### canRequestFocus

```dart
bool get canRequestFocus
```

如果为 true，此焦点节点可以请求主焦点。

默认为 true。如果你希望在此节点上调用 [requestFocus] 时不产生任何效果，请将其设置为 false。

如果在 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 上将其设置为 false，将导致该作用域节点的所有子节点都不可获得焦点。

如果在 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 上将其设置为 false，不会影响该节点的子节点的可获得焦点性。

如果此节点是拥有主焦点的节点的祖先，[hasFocus] 成员仍可能返回 true。

这与 [skipTraversal] 不同，因为 [skipTraversal] 仍然允许该节点获得焦点，只是不能通过 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 遍历到达。

将 [canRequestFocus] 设置为 false 意味着该节点在遍历时也会被跳过。

另请参阅：

- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件。
- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，一个可以被扩展以描述遍历策略的类。

### canRequestFocus

```dart
set canRequestFocus(bool value)
```

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

如果为 false，将禁用此节点所有子节点的焦点。

默认为 true。不影响此节点自身的可获得焦点性，如需影响自身，请使用 [canRequestFocus]。

如果在此值被设置为 false 时有子节点正获得焦点，它们将失去焦点。当 [descendantsAreFocusable] 重新设置为 true 时，它们不会被重新赋予焦点，尽管它们将能够再次接受焦点。

不影响子节点上 [canRequestFocus] 的值。

如果某个子节点在此值改变时失去焦点，焦点将移动到包含此节点的作用域。

另请参阅：

- [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus)，一个使用此属性有条件地排除子树焦点的组件。
- [descendantsAreTraversable]，使此组件的子组件不可遍历。
- [ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal)，一个有条件地排除子树焦点遍历的组件。
- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个将此设置公开为参数的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它也有一个阻止其子组件获得焦点的 `descendantsAreFocusable` 参数。

### descendantsAreFocusable

```dart
set descendantsAreFocusable(bool value)
```

### descendantsAreTraversable

```dart
bool get descendantsAreTraversable
```

如果为 false，告知焦点遍历策略在遍历算法中跳过此节点的所有子节点。

默认为 true。不影响此节点自身的焦点遍历，如需影响自身，请使用 [skipTraversal]。

不影响子节点上 [FocusNode.skipTraversal] 的值。不影响子节点的可获得焦点性。

另请参阅：

- [ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal)，一个使用此属性有条件地排除子树焦点遍历的组件。
- [descendantsAreFocusable]，使此组件的子组件不可获得焦点。
- [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus)，一个有条件地排除子树焦点的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它同样有一个阻止其子组件获得焦点的 `descendantsAreFocusable` 参数。

### descendantsAreTraversable

```dart
set descendantsAreTraversable(bool value)
```

### context

```dart
BuildContext? get context
```

传递给 [attach] 的上下文。

这通常是正被赋予焦点的组件的上下文，因为它用于确定组件的边界。

### onKey

```dart
FocusOnKeyCallback? onKey
```

当此焦点节点在获得焦点时（即 [hasFocus] 返回 true 时）接收到按键事件，则调用此回调。

此属性已废弃，将在未来的日期移除。请改用 [onKeyEvent]。

这是一个基于 [RawKeyEvent](https://www.yuque.com/thyname/flutter.services/rawkeyevent) 的旧版 API，未来将被废弃。建议改用 [onKeyEvent]。

{@macro flutter.widgets.FocusNode.keyEvents}

### onKeyEvent

```dart
FocusOnKeyEventCallback? onKeyEvent
```

当此焦点节点在获得焦点时（即 [hasFocus] 返回 true 时）接收到按键事件，则调用此回调。

{@macro flutter.widgets.FocusNode.keyEvents}

### parent

```dart
FocusNode? get parent
```

返回此对象的父节点。

除了根 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)（[FocusManager.rootScope]）之外的所有节点，在被添加到焦点树中时都会被赋予一个父节点，这是通过 [FocusAttachment.reparent] 完成的。

### children

```dart
Iterable<FocusNode> get children
```

此节点子节点的迭代器。

### traversalChildren

```dart
Iterable<FocusNode> get traversalChildren
```

允许被 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 遍历的子节点的迭代器。

返回此节点可获得焦点、可遍历的子节点列表，而不管这些设置在此焦点节点上的值如何。如果 [descendantsAreFocusable] 为 false，将返回一个空的可迭代对象。

另请参阅

- [traversalDescendants]，遍历该节点的所有子孙节点，而不仅仅是直接子节点。

### debugLabel

```dart
String? get debugLabel
```

用于诊断输出的调试标签。

在发布版本中始终返回 null。

### debugLabel

```dart
set debugLabel(String? value)
```

### descendants

```dart
Iterable<FocusNode> get descendants
```

此节点下方子节点层次结构的 [Iterable](https://www.yuque.com/thyname/dart.core/iterable)，按深度优先顺序排列。

### traversalDescendants

```dart
Iterable<FocusNode> get traversalDescendants
```

返回没有设置 [skipTraversal] 且设置了 [canRequestFocus] 标志的所有子孙节点。

### ancestors

```dart
Iterable<FocusNode> get ancestors
```

此节点祖先的 [Iterable](https://www.yuque.com/thyname/dart.core/iterable)。

从父节点开始，依次遍历此节点的祖先，逐步深入到更远的祖先，直至根 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)（[FocusManager.rootScope]）为止。

### hasFocus

```dart
bool get hasFocus
```

此节点是否拥有输入焦点。

当 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 是返回 true 的 [hasPrimaryFocus] 节点的祖先，或者它自身拥有主焦点时，该 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 拥有焦点。

[hasFocus] 访问器与 [hasPrimaryFocus] 的不同之处在于，只要该节点位于焦点链中的任意位置，[hasFocus] 就为 true，但对于 [hasPrimaryFocus]，该节点必须位于链的末端才会返回 true。

如果其获得焦点的子孙节点均未从其 [onKey] 处理程序返回 true，则对于返回 true 的 [hasFocus] 节点，将接收按键事件。

此对象是一个 [ChangeNotifier](https://www.yuque.com/thyname/flutter.foundation/changenotifier)，每当此值发生变化时，都会通知其 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 监听器（通过 [addListener] 注册）。

另请参阅：

- [Focus.isAt]，一个静态方法，返回最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的焦点节点的焦点状态。

### hasPrimaryFocus

```dart
bool get hasPrimaryFocus
```

如果此节点当前拥有应用程序范围的输入焦点，则返回 true。

当该节点在其最近的祖先 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 中获得焦点，且其所有祖先节点的 [hasFocus] 均为 true，但其任何子孙节点均不是这种情况时，[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 拥有主焦点。

这与 [hasFocus] 的不同之处在于，[hasFocus] 在该节点位于焦点链中的任意位置时即为 true，而这里该节点必须位于链的末端才会返回 true。

对于返回 true 的 [hasPrimaryFocus] 节点，将首先通过其 [onKey] 处理程序接收按键事件。

此对象在此值发生变化时都会通知其监听器。

### highlightMode

```dart
FocusHighlightMode get highlightMode
```

返回当前对此节点生效的 [FocusHighlightMode](https://www.yuque.com/thyname/flutter.widgets/focushighlightmode)。

### nearestScope

```dart
FocusScopeNode? get nearestScope
```

返回此节点上方（包括此节点，如果它是一个作用域）最近的封闭作用域节点。

如果找不到作用域，则返回 null。

使用 [enclosingScope] 在此节点上方查找作用域。

### enclosingScope

```dart
FocusScopeNode? get enclosingScope
```

返回此节点上方最近的封闭作用域节点，如果该节点尚未被添加到焦点树中，则返回 null。

如果此节点本身是一个作用域，这将只返回此作用域的祖先。

使用 [nearestScope] 从此节点本身开始查找。

### size

```dart
Size get size
```

以逻辑单位返回附加组件的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的大小。

大小是全局坐标中经过变换的组件的大小。

### offset

```dart
Offset get offset
```

以逻辑单位返回附加组件的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 左上角的全局偏移量。

偏移量是全局坐标中经过变换的组件的偏移量。

### rect

```dart
Rect get rect
```

以逻辑单位返回附加组件的 [RenderObject](https://www.yuque.com/thyname/flutter.rendering/renderobject) 的全局矩形。

矩形是全局坐标中经过变换的组件的矩形。

### unfocus()

```dart
void unfocus({UnfocusDisposition disposition = UnfocusDisposition.scope})
```

通过将主焦点移动到另一个节点来移除此节点上的焦点。

此方法从拥有主焦点的节点移除焦点，取消任何未完成的赋予其焦点的请求，同时根据 `disposition` 将主焦点设置到另一个节点。

无论此节点是否曾经请求过焦点，都可以安全地调用此方法。如果此节点不拥有焦点或主焦点，则不会发生任何事情。

`disposition` 参数决定了此节点失去焦点后哪个节点将获得主焦点。

如果 `disposition` 设置为 [UnfocusDisposition.scope]（默认值），则最近的封闭作用域祖先中先前获得焦点的节点历史记录将被清除，主焦点将移动到最近的启用了焦点的封闭作用域祖先，忽略该作用域的 [FocusScopeNode.focusedChild]。

如果 `disposition` 设置为 [UnfocusDisposition.previouslyFocusedChild]，则此节点将从 [enclosingScope] 的先前获得焦点列表中移除，焦点将移动到 [enclosingScope] 先前获得焦点的节点，如果该节点本身是一个作用域，则会查找其获得焦点的子节点，依此类推，直到找到叶子焦点节点。如果没有先前获得焦点的子节点，则该作用域本身将获得焦点，如同指定了 [UnfocusDisposition.scope] 一样。

如果你希望此节点失去焦点，并将焦点移动到封闭 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup) 中的下一个或上一个节点，请调用 [nextFocus] 或 [previousFocus]，而不是调用 [unfocus]。

{@tool dartpad} 此示例展示了 [unfocus] 的不同 [UnfocusDisposition](https://www.yuque.com/thyname/flutter.widgets/unfocusdisposition) 值之间的区别。

尝试通过选择四个文本字段来设置焦点，然后选择 "UNFOCUS" 查看取消当前 [FocusManager.primaryFocus] 焦点时发生的情况。

尝试在取消焦点后按 TAB 键，查看选择的下一个组件是什么。

** See code in examples/api/lib/widgets/focus_manager/focus_node.unfocus.0.dart ** {@end-tool}

### consumeKeyboardToken()

```dart
bool consumeKeyboardToken()
```

如果此焦点节点拥有键盘令牌，则将其移除。

此机制有助于区分输入控件是默认获得焦点还是由于用户显式操作而获得焦点。

当一个焦点节点请求焦点时（通过 [FocusScopeNode.requestFocus] 或 [FocusScopeNode.autofocus]），如果该焦点节点尚未拥有键盘令牌，它将获得一个键盘令牌。之后，当该焦点节点获得焦点时，管理 [TextInputConnection](https://www.yuque.com/thyname/flutter.services/textinputconnection) 的组件只有在成功从该焦点节点消费该键盘令牌后，才应显示键盘（即调用 [TextInputConnection.show]）。

如果此方法成功消费了键盘令牌，则返回 true。

### attach()

```dart
FocusAttachment attach(BuildContext? context, {FocusOnKeyEventCallback? onKeyEvent, FocusOnKeyCallback? onKey})
```

由 _宿主_ [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 调用，以将 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 附加到组件树。

要将 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 附加到组件树，请调用 [attach]，通常在 [StatefulWidget](https://www.yuque.com/thyname/flutter.widgets/statefulwidget) 的 [State.initState] 方法中调用。

如果宿主组件中的焦点节点被替换，则需要附加新节点。应先对旧节点调用 [FocusAttachment.detach]，然后对新节点调用 [attach]。这通常发生在 [State.didUpdateWidget] 方法中。

要接收使该节点获得焦点的按键事件，请向 `onKeyEvent` 传入一个监听器。

### dispose()

```dart
void dispose()
```

### requestFocus()

```dart
void requestFocus([FocusNode? node])
```

为此节点，或为提供的 [node]（同时也会将焦点赋予其 [ancestors]）请求主焦点。

如果调用时未传入节点，则为此节点请求焦点。如果该节点尚未被添加到焦点树中，则延迟该焦点请求直到其被添加，从而允许新创建的组件在被添加后立即请求焦点。

如果给定的 [node] 尚不是焦点树的一部分，则此方法会在请求焦点之前将该 [node] 添加为此节点的子节点。

如果给定的 [node] 是一个 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，且该焦点作用域节点具有非空的 [FocusScopeNode.focusedChild]，则为获得焦点的子节点请求焦点。此过程是递归的，会持续进行，直到遇到 [FocusScopeNode.focusedChild] 为 null 的焦点作用域节点，或找到一个普通（非作用域）的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 为止。

该节点会在微任务中被告知它已获得主焦点，因此通知可能比请求晚最多一帧。

### nextFocus()

```dart
bool nextFocus()
```

通过调用 [FocusTraversalPolicy.next] 方法，请求将焦点移动到下一个焦点节点。

如果成功找到节点并请求了焦点，则返回 true。

### previousFocus()

```dart
bool previousFocus()
```

通过调用 [FocusTraversalPolicy.previous] 方法，请求将焦点移动到上一个焦点节点。

如果成功找到节点并请求了焦点，则返回 true。

### focusInDirection()

```dart
bool focusInDirection(TraversalDirection direction)
```

通过调用 [FocusTraversalPolicy.inDirection] 方法，请求将焦点移动到给定方向上最近的焦点节点。

如果成功找到节点并请求了焦点，则返回 true。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### toStringShort()

```dart
String toStringShort()
```

# FocusScopeNode

```dart
class FocusScopeNode extends FocusNode {}
```

[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的一个子类，充当其子孙节点的作用域，维护有关当前或最近获得焦点的子孙节点的信息。

_请参阅 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 和 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件，它们分别是管理各自 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 和 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的实用组件。如果它们不合适，可以直接管理 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)。_

[FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 将 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 组织成 _作用域_。作用域构成了可以作为一个分组进行遍历的节点子树。在一个作用域内，最近获得焦点的节点会被记住，如果一个节点获得焦点后又被移除，原始节点会重新获得焦点。

从 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 调用 [setFirstFocus]，会将给定的焦点作用域设置为此节点的 [focusedChild]，如果它还不是焦点树的一部分，则会采纳它。

{@macro flutter.widgets.FocusNode.lifecycle} {@macro flutter.widgets.FocusNode.keyEvents}

另请参阅：

- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 并向其子组件提供焦点信息和操作访问权限的组件。
- [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，一个管理主焦点并向已获得焦点的节点分发按键事件的单例。

### FocusScopeNode()

```dart
FocusScopeNode({String? debugLabel, KeyEventResult Function(FocusNode, InvalidType)? onKeyEvent, KeyEventResult Function(FocusNode, InvalidType)? onKey, bool skipTraversal, bool canRequestFocus, TraversalEdgeBehavior traversalEdgeBehavior = TraversalEdgeBehavior.closedLoop, TraversalEdgeBehavior directionalTraversalEdgeBehavior = TraversalEdgeBehavior.stop})
```

创建一个 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)。

所有参数都是可选的。

### nearestScope

```dart
FocusScopeNode get nearestScope
```

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

### traversalEdgeBehavior

```dart
TraversalEdgeBehavior traversalEdgeBehavior
```

控制 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 中第一项和最后一项之外的焦点转移。

更改此字段的值不会立即对 UI 产生影响。相反，下次进行焦点遍历时，[FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 会读取此值并应用新的行为。

### directionalTraversalEdgeBehavior

```dart
TraversalEdgeBehavior directionalTraversalEdgeBehavior
```

当焦点位于第一项或最后一项时，控制焦点的方向性转移。

更改此字段的值不会立即对 UI 产生影响。相反，下次进行焦点遍历时，[FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 会读取此值并应用新的行为。

### isFirstFocus

```dart
bool get isFirstFocus
```

如果此作用域是其父作用域的获得焦点的子节点，则返回 true。

### focusedChild

```dart
FocusNode? get focusedChild
```

返回如果此作用域节点获得焦点，应获得焦点的此节点的子节点。

如果 [hasFocus] 为 true，则此指向此节点当前获得焦点的子节点。

如果没有当前获得焦点的子节点，则返回 null。

### traversalChildren

```dart
Iterable<FocusNode> get traversalChildren
```

允许被 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 遍历的子节点的迭代器。

如果此作用域节点不可获得焦点，或者 [descendantsAreFocusable] 为 false，将返回一个空的可迭代对象。

另请参阅：

- [traversalDescendants]，遍历该节点的所有子孙节点，而不仅仅是直接子节点。

### traversalDescendants

```dart
Iterable<FocusNode> get traversalDescendants
```

返回没有设置 [skipTraversal] 且设置了 [canRequestFocus] 标志的所有子孙节点。

如果此作用域节点不可获得焦点，或者 [descendantsAreFocusable] 为 false，将返回一个空的可迭代对象。

### setFirstFocus()

```dart
void setFirstFocus(FocusScopeNode scope)
```

使给定的 [scope] 成为此作用域的活动子作用域。

如果给定的 [scope] 尚不是焦点树的一部分，则将其作为此作用域的子节点添加到树中。如果它已经是焦点树的一部分，则给定的作用域必须是此作用域的子孙节点。

### autofocus()

```dart
void autofocus(FocusNode node)
```

如果此作用域缺少焦点，请求给定的节点成为焦点。

如果给定的节点尚不是焦点树的一部分，则将其作为此节点的子节点添加。

适用于希望在没有其他组件已获得焦点时抢先获得焦点的组件。

该节点会在微任务中被告知它已获得主焦点，因此通知可能比请求晚最多一帧。

### requestScopeFocus()

```dart
void requestScopeFocus()
```

请求作用域本身获得焦点，而不尝试查找应获得焦点的子孙节点。

仅当你想将焦点停放在作用域本身时才使用此方法。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FocusHighlightMode

```dart
enum FocusHighlightMode {}
```

一个枚举，描述显示焦点信息时使用哪种焦点高亮行为。

触摸界面除了会调出软键盘的控件外，不会显示焦点高亮。

如果使用传统鼠标和键盘的设备连接了触摸屏，如果用户正在使用触摸屏，它也可以进入 `touch` 模式。

传统界面（键盘和鼠标）会通过某种焦点高亮显示当前获得焦点的控件。

如果触摸设备（如手机）连接了键盘和/或鼠标，如果用户正在使用这些输入设备，它也可以进入 `traditional` 模式。

# FocusHighlightStrategy

```dart
enum FocusHighlightStrategy {}
```

一个枚举，描述如何确定 [FocusManager.highlightMode] 的当前值。该策略在 [FocusManager.highlightStrategy] 上设置。

自动根据最近接收到的输入类型在各种高亮模式之间切换。这是默认值。

[FocusManager.highlightMode] 始终返回 [FocusHighlightMode.touch]。

[FocusManager.highlightMode] 始终返回 [FocusHighlightMode.traditional]。

# FocusManager

```dart
class FocusManager with DiagnosticableTreeMixin, ChangeNotifier {}
```

管理焦点树。

焦点树是一棵独立的、比组件树更稀疏的树，维护组件树中可获得焦点的组件之间的层次关系。

焦点管理器负责跟踪哪个 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 拥有主输入焦点（[primaryFocus](https://www.yuque.com/thyname/flutter.widgets/primaryfocus)），持有作为焦点树根节点的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)（[rootScope]），以及当前的 [highlightMode] 是什么。它还负责将 [KeyEvent](https://www.yuque.com/thyname/flutter.services/keyevent) 分发给焦点树中的节点。

单例 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 实例由 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 作为 [WidgetsBinding.focusManager] 持有，可以方便地通过 [FocusManager.instance] 静态访问器访问。

要查找给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，请使用 [Focus.of]。要查找给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，请使用 [FocusScope.of]。

如果你希望在 [primaryFocus](https://www.yuque.com/thyname/flutter.widgets/primaryfocus) 每次变化时都得到通知，请通过 [addListener] 注册一个监听器。当你不再想接收这些事件时，例如对象即将被销毁时，必须通过 [removeListener] 取消注册，以避免内存泄漏。移除监听器通常在有状态组件的 [State.dispose] 中完成。

[highlightMode] 描述了应如何在 UI 中的组件上显示焦点高亮。[highlightMode] 的变化通过 [addHighlightModeListener] 单独通知，并通过 [removeHighlightModeListener] 移除。当用户从鼠标切换到触摸界面，或反之时，[highlightMode] 会发生变化。

用于在组件树中管理焦点的组件包括：

- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个在焦点树中管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的组件，使焦点树能够反映组件层次结构中的变化。
- [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope)，一个在焦点树中管理 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的组件，创建一个用于将焦点限制在一组焦点节点中的新作用域。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个将使用给定 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 描述的顺序遍历的节点分组在一起的组件。

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，焦点树中可以获得焦点的节点。
- [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，焦点树中用于将子树收集到分组并将焦点限制在其中的节点。
- 全局访问器 [primaryFocus](https://www.yuque.com/thyname/flutter.widgets/primaryfocus)，可便捷地从任何地方访问当前焦点管理器状态。

### FocusManager()

```dart
FocusManager()
```

创建一个管理焦点树的对象。

很少直接调用此构造函数。要访问 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，请考虑改用 [FocusManager.instance] 访问器（它从 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 单例中获取该实例）。

这个新构造的焦点管理器尚未注册管理焦点所需的事件处理程序。要注册这些事件处理程序，调用方必须调用 [registerGlobalHandlers]。有关需要注意的事项，请参阅该方法的文档。

### registerGlobalHandlers()

```dart
void registerGlobalHandlers()
```

注册管理焦点所需的全局输入事件处理程序。

这会在 [HardwareKeyboard](https://www.yuque.com/thyname/flutter.services/hardwarekeyboard) 的共享实例上调用 [HardwareKeyboard.addHandler]，并在全局手势路由表中添加一个路由。因此，只应有一个 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 实例注册其全局处理程序。

当不再需要此焦点管理器时，对其调用 [dispose] 将取消注册这些处理程序。

### dispose()

```dart
void dispose()
```

### instance

```dart
FocusManager get instance
```

提供从 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 实例方便地访问当前 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 单例的方式。

### highlightStrategy

```dart
FocusHighlightStrategy get highlightStrategy
```

设置确定 [highlightMode] 的策略。

如果设置为 [FocusHighlightStrategy.automatic]，则高亮模式将根据最近使用的交互模式而变化。例如，如果最近的交互是触摸交互，则 [highlightMode] 将返回 [FocusHighlightMode.touch]，焦点高亮将只出现在会调出软键盘的组件上。如果最近的交互是非触摸交互（硬件键盘按键、鼠标点击等），则 [highlightMode] 将返回 [FocusHighlightMode.traditional]，焦点高亮将出现在所有组件上。

如果设置为 [FocusHighlightStrategy.alwaysTouch] 或 [FocusHighlightStrategy.alwaysTraditional]，则 [highlightMode] 将始终分别返回 [FocusHighlightMode.touch] 或 [FocusHighlightMode.traditional]，而不管最近的 UI 交互类型如何。

[highlightMode] 的初始值取决于 [defaultTargetPlatform](https://www.yuque.com/thyname/flutter.foundation/defaulttargetplatform) 和 [RendererBinding.mouseTracker] 的 [MouseTracker.mouseIsConnected] 的值，对最初的交互模式最合适的方式进行推测。

默认为 [FocusHighlightStrategy.automatic]。

### highlightStrategy

```dart
set highlightStrategy(FocusHighlightStrategy value)
```

### highlightMode

```dart
FocusHighlightMode get highlightMode
```

指示焦点高亮的当前交互模式。

返回的值取决于所使用的 [highlightStrategy]，并可能（取决于 [highlightStrategy] 的值）取决于用户最近使用的交互模式。

如果 [highlightMode] 返回 [FocusHighlightMode.touch]，则组件除非执行文本输入，否则不应绘制其焦点高亮。

如果 [highlightMode] 返回 [FocusHighlightMode.traditional]，则组件应在其获得焦点时始终绘制其焦点高亮。

### addHighlightModeListener()

```dart
void addHighlightModeListener(ValueChanged<FocusHighlightMode> listener)
```

注册一个闭包，当 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 通知其监听器 [highlightMode] 的值已更改时调用该闭包。

### removeHighlightModeListener()

```dart
void removeHighlightModeListener(ValueChanged<FocusHighlightMode> listener)
```

从 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 通知的闭包列表中移除先前注册的闭包。

### addEarlyKeyEventHandler()

```dart
void addEarlyKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.addEarlyKeyEventHandler} 向一组处理程序中添加一个按键事件处理程序，该组处理程序会在焦点树中的任何按键事件处理程序之前被调用。

对于 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 接收到的每一个按键事件，该组中的所有处理程序都将被调用。如果其中任意一个处理程序返回 [KeyEventResult.handled] 或 [KeyEventResult.skipRemainingHandlers]，则焦点树中的任何处理程序都不会被调用。

如果在现有回调正在被调用期间添加了处理程序，它们将不会被调用，直到下一次按键事件发生。

另请参阅：

- [removeEarlyKeyEventHandler]，移除由此函数添加的处理程序。
- [addLateKeyEventHandler]，一个类似的机制，用于添加在焦点树有机会处理事件之后被调用的处理程序。{@endtemplate}

### removeEarlyKeyEventHandler()

```dart
void removeEarlyKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.removeEarlyKeyEventHandler} 移除通过调用 [addEarlyKeyEventHandler] 添加的按键处理程序。

如果在现有回调正在被调用期间移除了处理程序，它们将继续被调用，直到收到下一次按键事件。

另请参阅：

- [addEarlyKeyEventHandler]，添加由此函数移除的处理程序。{@endtemplate}

### addLateKeyEventHandler()

```dart
void addLateKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.addLateKeyEventHandler} 向一组处理程序中添加一个按键事件处理程序，如果焦点树中没有任何按键事件处理程序处理该事件，则会调用这些处理程序。

如果事件到达焦点树的根部仍未被处理，则该组中的所有处理程序都将被调用。如果其中任意一个返回 [KeyEventResult.handled] 或 [KeyEventResult.skipRemainingHandlers]，则将停止向平台传播事件。

如果在现有回调正在被调用期间添加了处理程序，它们将不会被调用，直到下一次未被焦点树处理的按键事件发生。

另请参阅：

- [removeLateKeyEventHandler]，移除由此函数添加的处理程序。
- [addEarlyKeyEventHandler]，一个类似的机制，用于添加在焦点树有机会处理事件之前被调用的处理程序。{@endtemplate}

### removeLateKeyEventHandler()

```dart
void removeLateKeyEventHandler(OnKeyEventCallback handler)
```

{@template flutter.widgets.focus_manager.FocusManager.removeLateKeyEventHandler} 移除通过调用 [addLateKeyEventHandler] 添加的按键处理程序。

如果在现有回调正在被调用期间移除了处理程序，它们将继续被调用，直到收到下一次按键事件。

另请参阅：

- [addLateKeyEventHandler]，添加由此函数移除的处理程序。{@endtemplate}

### rootScope

```dart
FocusScopeNode rootScope
```

焦点树中的根 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)。

此字段很少直接使用。要为给定的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 查找最近的 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，请调用 [FocusNode.nearestScope]。

### primaryFocus

```dart
FocusNode? get primaryFocus
```

当前拥有主焦点的节点。

### applyFocusChangesIfNeeded()

```dart
void applyFocusChangesIfNeeded()
```

应用任何待处理的焦点变化，并通知监听器焦点已发生变化。

不得在构建阶段调用。此方法旨在需要在其他事情发生之前解决待处理的焦点变化时，在帧后回调或微任务中调用。

不能在构建阶段调用它，是因为并非所有监听器在构建期间接收更新都是安全的。

通常，[FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 会自动调用此方法，但有时有必要确保在执行某个操作之前没有待处理的焦点变化。例如，[MenuAnchor](https://www.yuque.com/thyname/flutter.material/menuanchor) 类使用此方法确保在执行菜单项被选中时的回调之前，先前的焦点已被恢复。

如果没有待处理的焦点变化，调用此方法是安全的。

### listenToApplicationLifecycleChangesIfSupported()

```dart
void listenToApplicationLifecycleChangesIfSupported()
```

如果此 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 尚未激活应用程序生命周期监听器，且应用未在原生移动平台上运行，则使其能够监听应用程序生命周期的变化。

通常，此 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 的应用程序生命周期监听器是在构造时设置的，但有时在构造时 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 没有 [defaultTargetPlatform](https://www.yuque.com/thyname/flutter.foundation/defaulttargetplatform) 中的相关平台上下文，因此需要手动初始化它。这可能发生在测试环境中，其初始化自身 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 的 [BuildOwner](https://www.yuque.com/thyname/flutter.widgets/buildowner) 在初始化期间可能没有准确的平台上下文的情况下。在这种情况下，测试框架需要在为给定测试设置好测试变体之后调用此方法，以便 [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager) 能够在支持的情况下准确监听应用程序生命周期变化。

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# primaryFocus

```dart
FocusNode? get primaryFocus
```

提供从 [WidgetsBinding](https://www.yuque.com/thyname/flutter.widgets/widgetsbinding) 实例方便地访问当前 [FocusManager.primaryFocus] 的方式。

# debugDescribeFocusTree()

```dart
String debugDescribeFocusTree()
```

返回当前焦点树及每个节点当前属性的文本表示。

在发布版本中将返回空字符串。

# debugDumpFocusTree()

```dart
void debugDumpFocusTree()
```

打印当前焦点树及每个节点当前属性的文本表示。

在发布版本中不执行任何操作。
