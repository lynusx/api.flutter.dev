@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/semantics.dart';

@docImport 'actions.dart'; @docImport 'container.dart'; @docImport 'editable_text.dart'; @docImport 'focus_traversal.dart'; @docImport 'overlay.dart';

# Focus

```dart
class Focus extends StatefulWidget {}
```

一个管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的组件，用于允许键盘焦点赋予该组件及其子组件。

{@youtube 560 315 https://www.youtube.com/watch?v=JCDfh5bs1xc}

当获得或失去焦点时，会调用 [onFocusChange]。

对于键盘事件，如果该组件的 [focusNode] 的 [FocusNode.hasFocus] 为 true，则会调用 [onKey] 和 [onKeyEvent]，除非某个获得焦点的子组件的 [onKey] 或 [onKeyEvent] 回调在被调用时返回了 [KeyEventResult.handled]。

此组件不提供任何焦点变化的可视化指示。任何所需的视觉变化都应在调用 [onFocusChange] 时进行。

要访问最近的祖先 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 并建立一个会在焦点变化时重建组件的关系，请使用 [Focus.of] 和 [FocusScope.of] 静态方法。

要访问最近的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的焦点状态，请在 build 方法中使用 [FocusNode.hasFocus]，这也会在调用组件和会在焦点变化时重建调用组件的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件之间建立关系。

管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 意味着管理其生命周期、监听焦点变化，并在需要时重新设置其父节点，以使焦点层次结构与组件层次结构保持同步。此组件会为你完成所有这些工作。如果你不使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件而需要自行完成这些操作，请参阅 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 以了解节点管理所涉及内容的更多细节。

如果使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 默认构造函数，则此组件会在 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件每次更新时，用 [FocusNode.onKey]、[FocusNode.onKeyEvent]、[FocusNode.skipTraversal]、[FocusNode.canRequestFocus] 和 [FocusNode.descendantsAreFocusable] 的值覆盖给定 [focusNode] 的相应值来管理该节点。

如果改用 [Focus.withExternalFocusNode]，则 [onKey]、[onKeyEvent]、[skipTraversal]、[canRequestFocus] 和 [descendantsAreFocusable] 所返回的值将是外部焦点节点中的值，并且外部焦点节点的值在组件更新时不会被覆盖。

要将一组节点收集到一个限制焦点遍历范围的独占分组中，请使用 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope)。要将一组节点收集到一个具有特定遍历顺序但允许遍历离开该分组的分组中，请使用 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)。

要移动焦点，请通过 [of] 方法获取 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 后使用其上的方法。例如，要将焦点移动到焦点遍历顺序中的下一个节点，调用 `Focus.of(context).nextFocus()`。要取消某个组件的焦点，调用 `Focus.of(context).unfocus()`。

{@tool dartpad} 此示例展示了如何使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 和 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件管理焦点。有关不使用 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 的类似示例，请参阅 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

** See code in examples/api/lib/widgets/focus_scope/focus.0.dart ** {@end-tool}

{@tool dartpad} 此示例展示了如何将另一个组件包装在 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件中以使其可获得焦点。它包装了一个 [Container](https://www.yuque.com/thyname/flutter.widgets/container)，并在其被设置为 [FocusManager.primaryFocus] 时改变该容器的颜色。

如果你还想处理组件上的鼠标悬停和/或键盘操作，可以考虑使用 [FocusableActionDetector](https://www.yuque.com/thyname/flutter.widgets/focusableactiondetector)，它组合了多个不同的组件以提供这些功能。

** See code in examples/api/lib/widgets/focus_scope/focus.1.dart ** {@end-tool}

{@tool dartpad} 此示例展示了如何在新创建的组件创建后立即使其获得焦点。

焦点节点在其请求焦点的那一帧绘制完成之前不会真正获得焦点，因此即使该节点尚未加入焦点树，也可以调用 [FocusNode.requestFocus]。

** See code in examples/api/lib/widgets/focus_scope/focus.2.dart ** {@end-tool}

另请参阅：

- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，它表示焦点层次结构中的一个节点，[FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的 API 文档中包含了对其在整个焦点系统中所起作用的详细说明。
- [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope)，一个使用 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 管理一组可获得焦点的组件的组件。
- [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，一个将焦点节点收集到一个分组中以进行遍历的节点。
- [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，一个管理主焦点并向已获得焦点的节点分发按键事件的单例。
- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，一个用于确定如何将焦点移动到其他节点的对象。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个对其下方组件层次结构中的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点进行分组并施加遍历策略的组件。

### Focus()

```dart
Focus({dynamic key, required Widget child, FocusNode? focusNode, FocusNode? parentNode, bool autofocus = false, ValueChanged<bool>? onFocusChange, FocusOnKeyEventCallback? onKeyEvent, FocusOnKeyCallback? onKey, bool? canRequestFocus, bool? skipTraversal, bool? descendantsAreFocusable, bool? descendantsAreTraversable, bool includeSemantics = true, String? debugLabel})
```

创建一个管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的组件。

### Focus.withExternalFocusNode()

```dart
Focus.withExternalFocusNode({Key? key, required Widget child, required FocusNode focusNode, FocusNode? parentNode, bool autofocus, ValueChanged<bool>? onFocusChange, bool includeSemantics})
```

创建一个使用给定 [focusNode] 作为节点属性真实来源的 Focus 组件，而不是使用此组件自身的属性。

### parentNode

```dart
FocusNode? parentNode
```

为此 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件重新设置 [focusNode] 父节点时使用的可选父节点。

如果 [parentNode] 为 null，则使用 [Focus.maybeOf] 在组件树中查找父节点，这通常是所期望的行为，因为如果焦点树能够反映组件树的形状，将更易于理解焦点系统。

如果焦点树需要具有与组件树不同的形状，请设置此属性。这通常出现在对话框位于 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay)（或组件树的另一部分）中，而出于焦点考虑，希望 overlay 中的组件表现得如同给定 [parentNode] 的子组件的情况下。

默认为 null。

### child

```dart
Widget child
```

此 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 的子组件。

{@macro flutter.widgets.ProxyWidget.child}

### focusNode

```dart
FocusNode? focusNode
```

{@template flutter.widgets.Focus.focusNode} 用作此组件焦点节点的可选焦点节点。

如果未提供，则会自动分配一个由此组件拥有和管理的焦点节点。即使未提供 [focusNode]，该组件也是可获得焦点的。如果提供了，给定的 [focusNode] 将由此组件 _托管_，但不由其 _拥有_。有关托管和/或拥有含义的更多信息，请参阅 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

如果某个祖先组件想要控制此组件何时获得焦点，提供焦点节点有时会很有用。所有者负责在使用完毕后对该焦点节点调用 [FocusNode.dispose]，但此组件会在需要时附加/分离并重新设置该节点的父节点。{@endtemplate}

如果使用 [Focus.withExternalFocusNode] 构造函数，则必须提供一个非空的 [focusNode]。

### autofocus

```dart
bool autofocus
```

{@template flutter.widgets.Focus.autofocus} 如果为 true，则当其作用域内当前没有其他节点获得焦点时，此组件将被选为初始焦点。

理想情况下，每个 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 中只有一个组件设置了 autofocus。如果设置了多个组件的 autofocus，则先添加到树中的组件将获得焦点。

默认为 false。{@endtemplate}

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

焦点变化时调用的处理程序。

当此组件的节点获得焦点时以 true 调用，失去焦点时以 false 调用。

### onKeyEvent

```dart
FocusOnKeyEventCallback? get onKeyEvent
```

当此对象或其某个子对象获得焦点时按下按键的处理程序。

按键事件首先传递给拥有主焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，如果其 [onKeyEvent] 方法返回 [KeyEventResult.ignored]，则会依次传递给焦点层次结构中的每个祖先节点。如果事件到达层次结构的根部，则会被丢弃。

这不是以文本字段方式获取文本输入的方法：它不支持输入法编辑器，也不支持一般意义上的软键盘。对于文本输入，请考虑改用 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)、[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 或 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)，它们支持这些功能。

### onKey

```dart
FocusOnKeyCallback? get onKey
```

当此对象或其某个子对象获得焦点时按下按键的处理程序。

此属性已废弃，将会被移除。请改用 [onKeyEvent]。

按键事件首先传递给拥有主焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，如果其 [onKey] 方法返回 false，则会依次传递给焦点层次结构中的每个祖先节点。如果事件到达层次结构的根部，则会被丢弃。

这不是以文本字段方式获取文本输入的方法：它不支持输入法编辑器，也不支持一般意义上的软键盘。对于文本输入，请考虑改用 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)、[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 或 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)，它们支持这些功能。

### canRequestFocus

```dart
bool get canRequestFocus
```

{@template flutter.widgets.Focus.canRequestFocus} 如果为 true，此组件可以请求主焦点。

默认为 true。如果你希望在对该组件所管理的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 调用 [FocusNode.requestFocus] 时不产生任何效果，请将其设置为 false。这不会影响该节点的子组件，如果此节点是主焦点的祖先，[FocusNode.hasFocus] 仍可能返回 true。

这与 [Focus.skipTraversal] 不同，因为 [Focus.skipTraversal] 仍然允许该组件获得焦点，只是不能通过遍历到达。

将 [FocusNode.canRequestFocus] 设置为 false 意味着该组件在遍历时也会被跳过。

另请参阅：

- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个为其子组件设置遍历策略的组件。
- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，一个可以被扩展以描述遍历策略的类。{@endtemplate}

### skipTraversal

```dart
bool get skipTraversal
```

在焦点节点上设置 [FocusNode.skipTraversal] 标志，使其不会被 [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy) 访问。

这有时用于将可获得焦点但不应通过焦点遍历访问的节点放置在焦点树中，从而使其能够作为焦点链的一部分接收按键事件，但不能通过焦点遍历到达。

这与 [FocusNode.canRequestFocus] 不同，因为它只意味着该组件不能通过遍历到达，而不意味着不能被赋予焦点。它仍然可以被显式地赋予焦点。

### descendantsAreFocusable

```dart
bool get descendantsAreFocusable
```

{@template flutter.widgets.Focus.descendantsAreFocusable} 如果为 false，将使此组件的子组件不可获得焦点。

默认为 true。不影响此节点自身的可获得焦点性（仅影响其子组件），如需影响自身，请使用 [FocusNode.canRequestFocus]。

如果在此值被设置为 false 时有子组件正获得焦点，它们将失去焦点。当 [descendantsAreFocusable] 重新设置为 true 时，它们不会被重新赋予焦点，尽管它们将能够再次接受焦点。

不影响子组件上 [FocusNode.canRequestFocus] 的值。

如果某个子节点在此值改变时失去焦点，焦点将移动到包含此节点的作用域。

另请参阅：

- [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus)，一个使用此属性有条件地排除子树焦点的组件。
- [descendantsAreTraversable]，使此组件的子组件不可遍历。
- [ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal)，一个有条件地排除子树焦点遍历的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它有一个 `descendantsAreFocusable` 参数，可有条件地阻止子树获得焦点。{@endtemplate}

### descendantsAreTraversable

```dart
bool get descendantsAreTraversable
```

{@template flutter.widgets.Focus.descendantsAreTraversable} 如果为 false，将使此组件的子组件不可遍历。

默认为 true。不影响此节点自身的可遍历性（仅影响其子组件），如需影响自身，请使用 [FocusNode.skipTraversal]。

不影响子组件上 [FocusNode.skipTraversal] 的值。不影响子组件的可获得焦点性。

另请参阅：

- [ExcludeFocusTraversal](https://www.yuque.com/thyname/flutter.widgets/excludefocustraversal)，一个使用此属性有条件地排除子树焦点遍历的组件。
- [descendantsAreFocusable]，使此组件的子组件不可获得焦点。
- [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus)，一个有条件地排除子树焦点的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它同样有一个 `descendantsAreFocusable` 参数，可阻止其子组件获得焦点。{@endtemplate}

### includeSemantics

```dart
bool includeSemantics
```

{@template flutter.widgets.Focus.includeSemantics} 在此组件中包含语义信息。

如果为 true，此组件将包含一个指示 [SemanticsProperties.focusable] 和 [SemanticsProperties.focused] 属性的 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 节点。

通常不建议将其设置为 false，因为这会影响无障碍系统可用的语义信息。

默认为 true。{@endtemplate}

### debugLabel

```dart
String? get debugLabel
```

此组件的调试标签。

除了在 [toString] 或 [toStringDeep] 的诊断输出中打印外，不用于其他任何用途。

要获取包含整棵树的字符串，请调用 [debugDescribeFocusTree](https://www.yuque.com/thyname/flutter.widgets/debugdescribefocustree)。要将其打印到控制台，请调用 [debugDumpFocusTree](https://www.yuque.com/thyname/flutter.widgets/debugdumpfocustree)。

默认为 null。

### of()

```dart
FocusNode of(BuildContext context, {bool scopeOk = false, bool createDependency = true})
```

返回最紧密包围给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 的 [focusNode]。

如果在到达最近的 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件之前未找到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点，或者上下文中没有 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件，则此方法将抛出异常。

{@macro flutter.widgets.focus_scope.Focus.maybeOf}

另请参阅：

- [maybeOf]，与此函数类似，但在找不到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点时会返回 null 而不是抛出异常。

### maybeOf()

```dart
FocusNode? maybeOf(BuildContext context, {bool scopeOk = false, bool createDependency = true})
```

返回最紧密包围给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 的 [focusNode]。

如果在到达最近的 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件之前未找到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点，或者作用域内没有 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件，则此方法将返回 null。

{@template flutter.widgets.focus_scope.Focus.maybeOf} 如果 `createDependency` 为 true（默认值），调用此函数会创建一个依赖关系，使给定的上下文在焦点节点获得或失去焦点时重建。{@endtemplate}

另请参阅：

- [of]，与此函数类似，但在找不到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 节点时会抛出异常，而不是返回 null。

### isAt()

```dart
bool isAt(BuildContext context)
```

如果最近的封闭 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件的节点已获得焦点，则返回 true。

一个便捷方法，允许 build 方法写作：`Focus.isAt(context)` 来获取它们在组件层次结构中最近的上方 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 当前是否拥有输入焦点。

如果在到达最近的 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 之前未找到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件，或者到达焦点树的根部仍未找到 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件，则返回 false。

调用此函数会创建一个依赖关系，使给定的上下文在焦点变化时重建。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### createState()

```dart
State<Focus> createState()
```

# FocusScope

```dart
class FocusScope extends Focus {}
```

[FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 与 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 类似，但它还充当其子组件的作用域，将焦点遍历限制在该作用域内的控件中。

例如，当推入一个路由时，会自动创建一个新的 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope)，以防止焦点遍历移动到上一个路由中的控件。

如果你只是想将组件分组，使它们按特定顺序遍历，但焦点仍可以离开该分组，请使用 [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)。

与 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 一样，[FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 提供了 [onFocusChange] 作为在此组件获得或失去焦点时得到通知的方式。

[onKey] 参数允许指定一个按键事件处理程序，该处理程序会在此节点或其某个子节点获得焦点时被调用。按键首先交给主焦点组件，然后沿该节点的祖先向上传播，如果其中某个祖先的 [onKey] 返回 [KeyEventResult.handled]，则停止传播，表示它已处理该事件。

管理 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 意味着管理其生命周期、监听焦点变化，并在需要时重新设置其父节点，以使焦点层次结构与组件层次结构保持同步。此组件会为你完成所有这些工作。如果你不使用 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件而需要自行完成这些操作，请参阅 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 以了解节点管理所涉及内容的更多细节。

[FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 会记住其子组件中最近获得焦点的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，并可以在 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 或 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 上调用 [FocusNode.nextFocus]、[FocusNode.previousFocus] 或 [FocusNode.focusInDirection] 时，将焦点移动到下一个/上一个节点，或特定方向上的节点。

要移动焦点，请通过 [of] 方法获取 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 后使用其上的方法。例如，要将焦点移动到焦点遍历顺序中的下一个节点，调用 `Focus.of(context).nextFocus()`。要取消某个组件的焦点，调用 `Focus.of(context).unfocus()`。

{@tool dartpad} 此示例演示了如何使用 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 将焦点限制在应用程序的特定部分。在此示例中，将焦点限制在 Stack 中可见的部分。

** See code in examples/api/lib/widgets/focus_scope/focus_scope.0.dart ** {@end-tool}

另请参阅：

- [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode)，它表示焦点层次结构中的一个作用域节点。
- [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)，它表示焦点层次结构中的一个节点，并对焦点系统进行了说明。
- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 并提供无需管理节点即可轻松访问焦点管理的组件。
- [FocusManager](https://www.yuque.com/thyname/flutter.widgets/focusmanager)，一个管理焦点并向已获得焦点的节点分发按键事件的单例。
- [FocusTraversalPolicy](https://www.yuque.com/thyname/flutter.widgets/focustraversalpolicy)，一个用于确定如何将焦点移动到其他节点的对象。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于配置组件子树的焦点遍历策略的组件。

### FocusScope()

```dart
FocusScope({dynamic key, FocusScopeNode? node, FocusNode? parentNode, required Widget child, bool autofocus, dynamic onFocusChange, bool? canRequestFocus, bool? skipTraversal, KeyEventResult Function(FocusNode, InvalidType)? onKeyEvent, KeyEventResult Function(FocusNode, InvalidType)? onKey, String? debugLabel, bool includeSemantics, bool? descendantsAreFocusable, bool? descendantsAreTraversable})
```

创建一个管理 [FocusScopeNode](https://www.yuque.com/thyname/flutter.widgets/focusscopenode) 的组件。

### FocusScope.withExternalFocusNode()

```dart
FocusScope.withExternalFocusNode({Key? key, required Widget child, required FocusScopeNode focusScopeNode, FocusNode? parentNode, bool autofocus, bool includeSemantics, ValueChanged<bool>? onFocusChange})
```

创建一个使用给定 [focusScopeNode] 作为节点属性真实来源的 FocusScope 组件，而不是使用此组件自身的属性。

### of()

```dart
FocusScopeNode of(BuildContext context, {bool createDependency = true})
```

返回最紧密包围给定 [context] 的 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 的 [FocusNode.nearestScope]。

如果此节点没有 [Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 或 [FocusScope](https://www.yuque.com/thyname/flutter.widgets/focusscope) 组件祖先，则返回 [FocusManager.rootScope]。

{@macro flutter.widgets.focus_scope.Focus.maybeOf}

### createState()

```dart
State<Focus> createState()
```

# ExcludeFocus

```dart
class ExcludeFocus extends StatelessWidget {}
```

一个控制此组件的子组件是否可获得焦点的组件。

不影响子组件上 [Focus.canRequestFocus] 的值。

另请参阅：

- [Focus](https://www.yuque.com/thyname/flutter.widgets/focus)，一个用于在组件树中添加和管理 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 的组件。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于对组件进行焦点遍历分组的组件，也可以通过设置其 `descendantsAreFocusable` 属性以与此组件相同的方式使用。

### ExcludeFocus()

```dart
ExcludeFocus({dynamic key, bool excluding = true, required Widget child})
```

[ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus) 组件的 const 构造函数。

### excluding

```dart
bool excluding
```

如果为 true，将使此组件的子组件不可获得焦点。

默认为 true。

如果在此值被设置为 true 时有子组件正获得焦点，它们将失去焦点。当 [excluding] 重新设置为 false 时，它们不会被重新赋予焦点，尽管它们将能够再次接受焦点。

不影响子组件上 [FocusNode.canRequestFocus] 的值。

另请参阅：

- [Focus.descendantsAreFocusable]，[Focus](https://www.yuque.com/thyname/flutter.widgets/focus) 组件中控制相同属性的属性。
- [FocusTraversalGroup](https://www.yuque.com/thyname/flutter.widgets/focustraversalgroup)，一个用于组合并配置组件子树的焦点遍历策略的组件，它有一个 `descendantsAreFocusable` 参数，可有条件地阻止子树获得焦点。

### child

```dart
Widget child
```

此 [ExcludeFocus](https://www.yuque.com/thyname/flutter.widgets/excludefocus) 的子组件。

{@macro flutter.widgets.ProxyWidget.child}
