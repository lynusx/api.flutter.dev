# SemanticsConfiguration

```dart
class SemanticsConfiguration {}
```

描述与拥有该配置的 [RenderObject] 相关联的语义信息。

配置中提供的信息用于生成语义树。

### isSemanticBoundary

```dart
bool get isSemanticBoundary
```

此配置的拥有者 [RenderObject] 是否希望拥有自己的 [SemanticsNode]。

当设置为 true 时，与此配置的拥有者 [RenderObject] 或其任何后代相关联的语义信息将不会泄漏到父级中。由此配置生成的 [SemanticsNode] 将充当边界。

拥有者 [RenderObject] 的后代是否可以将其语义信息添加到此配置引入的 [SemanticsNode] 中，由 [explicitChildNodes] 控制。

如果 [isMergingSemanticsOfDescendants] 也为 true，则此项必须为 true。

### isSemanticBoundary

```dart
set isSemanticBoundary(bool value)
```

### localeForSubtree

```dart
Locale? get localeForSubtree
```

子树中 Widget 的语言区域。

### localeForSubtree

```dart
set localeForSubtree(Locale? value)
```

### locale

```dart
Locale? locale
```

如果此配置形成一个语义节点，则为该结果语义节点的语言区域。

这在内部用于跟踪从父渲染对象继承的语言区域，不应直接使用。

要为渲染对象设置语言区域，请改用 [localeForSubtree]。

### isBlockingUserActions

```dart
bool isBlockingUserActions
```

是否阻止渲染子树的指针相关用户操作。

将此项设置为 true 将阻止用户通过辅助技术中与指针相关的 [SemanticsAction] 与产生此语义配置的渲染对象及其子树进行交互。

由此语义配置创建的 [SemanticsNode] 仍可被辅助技术聚焦。仅会阻止与指针相关的 [SemanticsAction]，例如 [SemanticsAction.tap] 及其同类操作。

如果此语义配置被合并到父语义节点中，则仅会阻止来自此渲染对象及其子树中渲染对象的 [SemanticsAction]。

### explicitChildNodes

```dart
bool explicitChildNodes
```

此配置是否强制要求拥有者 [RenderObject] 的所有希望贡献语义信息到语义树的子级，都必须以显式 [SemanticsNode] 的形式进行。

当设置为 false 时，拥有者 [RenderObject] 的子级可以将它们想要贡献的语义信息标注到父级的 [SemanticsNode] 上。当设置为 true 时，拥有者 [RenderObject] 的子级向语义树贡献语义信息的唯一方式是向树中引入新的显式 [SemanticsNode]。

此设置通常与 [isSemanticBoundary] 结合使用，以创建对子级可写或不可写的语义边界。

### isBlockingSemanticsOfPreviouslyPaintedNodes

```dart
bool isBlockingSemanticsOfPreviouslyPaintedNodes
```

拥有者 [RenderObject] 是否使同一语义边界内先前绘制的其他 [RenderObject] 在无障碍功能中不可达。

如果设置为 true，则在深度优先前序遍历中位于此节点之前的所有兄弟节点和表亲节点的语义信息，都会从语义树中被丢弃，直至到达一个语义边界（由 [isSemanticBoundary] 定义）为止。

如果同一节点上同时设置了 [isSemanticBoundary] 和 [isBlockingSemanticsOfPreviouslyPaintedNodes]，则会丢弃直至下一个作为语义边界的祖先节点为止的所有先前绘制的兄弟节点和表亲节点。

由 [RenderObject.visitChildrenForSemantics] 确定的绘制顺序用于判断某个节点是否位于此节点之前。

### hasBeenAnnotated

```dart
bool get hasBeenAnnotated
```

此配置是否为空。

空配置不包含任何希望贡献给语义树的语义信息。

### onTap

```dart
VoidCallback? get onTap
```

[SemanticsAction.tap] 的处理程序。

这是用户用手指短暂轻触屏幕而不移动的语义等效操作。例如，按钮应实现此操作。

iOS 上的 VoiceOver 用户和 Android 上的 TalkBack 用户可以通过在元素获得焦点时双击屏幕来触发此操作。

在 Android Oreo 之前的版本上，当具有 [onTap] 处理程序的元素获得焦点时双击屏幕，不会调用已注册的处理程序。相反，Android 会在获得焦点元素的中心模拟一次指针按下和抬起事件。这些指针事件的处理方式将与禁用 TalkBack 时的常规轻触相同：这些事件将由任何在该元素中心监听手势的 [GestureDetector] 处理。因此，为确保 [onTap] 处理程序在 Oreo 之前的 Android 版本上正常工作，具有语义 [onTap] 处理程序的元素应始终被带有 onTap 处理程序的 [GestureDetector] 包裹。默认情况下，[GestureDetector] 会注册自己遵循此原则的语义 [onTap] 处理程序。

### onTap

```dart
set onTap(VoidCallback? value)
```

### onLongPress

```dart
VoidCallback? get onLongPress
```

[SemanticsAction.longPress] 的处理程序。

这是用户用手指按住屏幕几秒钟而不移动的语义等效操作。

iOS 上的 VoiceOver 用户和 Android 上的 TalkBack 用户可以通过双击屏幕并在第二次轻触后不抬起手指来触发此操作。

### onLongPress

```dart
set onLongPress(VoidCallback? value)
```

### onScrollLeft

```dart
VoidCallback? get onScrollLeft
```

[SemanticsAction.scrollLeft] 的处理程序。

这是用户手指在屏幕上从右向左移动的语义等效操作。可水平滚动的控件应识别此操作。

iOS 上的 VoiceOver 用户可以通过用三根手指向左滑动来触发此操作。Android 上的 TalkBack 用户可以通过在一次运动路径中先向右滑再向左滑来触发此操作。在 Android 上，[onScrollUp] 和 [onScrollLeft] 共享相同的手势，因此只应提供其中之一。

### onScrollLeft

```dart
set onScrollLeft(VoidCallback? value)
```

### onDismiss

```dart
VoidCallback? get onDismiss
```

[SemanticsAction.dismiss] 的处理程序。

这是关闭当前获得焦点节点的请求。

Android 上的 TalkBack 用户可以在本地上下文菜单中触发此操作，iOS 上的 VoiceOver 用户可以通过标准手势或菜单选项触发此操作。

### onDismiss

```dart
set onDismiss(VoidCallback? value)
```

### onScrollRight

```dart
VoidCallback? get onScrollRight
```

[SemanticsAction.scrollRight] 的处理程序。

这是用户手指在屏幕上从左向右移动的语义等效操作。可水平滚动的控件应识别此操作。

iOS 上的 VoiceOver 用户可以通过用三根手指向右滑动来触发此操作。Android 上的 TalkBack 用户可以通过在一次运动路径中先向左滑再向右滑来触发此操作。在 Android 上，[onScrollDown] 和 [onScrollRight] 共享相同的手势，因此只应提供其中之一。

### onScrollRight

```dart
set onScrollRight(VoidCallback? value)
```

### onScrollUp

```dart
VoidCallback? get onScrollUp
```

[SemanticsAction.scrollUp] 的处理程序。

这是用户手指在屏幕上从下向上移动的语义等效操作。可垂直滚动的控件应识别此操作。

iOS 上的 VoiceOver 用户可以通过用三根手指向上滑动来触发此操作。Android 上的 TalkBack 用户可以通过先向右滑再向左滑来触发此操作。在 Android 上，[onScrollUp] 和 [onScrollLeft] 共享相同的手势。

### onScrollUp

```dart
set onScrollUp(VoidCallback? value)
```

### onScrollDown

```dart
VoidCallback? get onScrollDown
```

[SemanticsAction.scrollDown] 的处理程序。

这是用户手指在屏幕上从上向下移动的语义等效操作。可垂直滚动的控件应识别此操作。

iOS 上的 VoiceOver 用户可以通过用三根手指向下滑动来触发此操作。Android 上的 TalkBack 用户可以通过先向左滑再向右滑来触发此操作。在 Android 上，[onScrollDown] 和 [onScrollRight] 共享相同的手势。

### onScrollDown

```dart
set onScrollDown(VoidCallback? value)
```

### onScrollToOffset

```dart
ScrollToOffsetHandler? get onScrollToOffset
```

[SemanticsAction.scrollToOffset] 的处理程序。

此处理程序仅在 iOS 上由 UIKit 调用：当 iOS 焦点引擎将焦点切换到过于靠近可滚动容器边缘的项目时，为确保获得焦点的项目始终完全可见而调用。

如果该回调不为 `null`，通常应将关联可滚动容器的滚动偏移量直接设置为给定的 `targetOffset`，且不带动画，因为调用方已经对其进行了动画处理：iOS 焦点引擎会在滚动动画期间的每一帧都以已产生动画效果的滚动偏移值调用 [onScrollToOffset]。

### onScrollToOffset

```dart
set onScrollToOffset(ScrollToOffsetHandler? value)
```

### onIncrease

```dart
VoidCallback? get onIncrease
```

[SemanticsAction.increase] 的处理程序。

这是增加 Widget 所表示数值的请求。例如，滑块控件可能会识别此操作。

如果设置了 [value]，则也必须提供 [increasedValue]，并且 [onIncrease] 必须确保 [value] 会被设置为 [increasedValue]。

iOS 上的 VoiceOver 用户可以通过用一根手指向上滑动来触发此操作。Android 上的 TalkBack 用户可以通过按音量增大键来触发此操作。

### onIncrease

```dart
set onIncrease(VoidCallback? value)
```

### onDecrease

```dart
VoidCallback? get onDecrease
```

[SemanticsAction.decrease] 的处理程序。

这是减少 Widget 所表示数值的请求。例如，滑块控件可能会识别此操作。

如果设置了 [value]，则也必须提供 [decreasedValue]，并且 [onDecrease] 必须确保 [value] 会被设置为 [decreasedValue]。

iOS 上的 VoiceOver 用户可以通过用一根手指向下滑动来触发此操作。Android 上的 TalkBack 用户可以通过按音量减小键来触发此操作。

### onDecrease

```dart
set onDecrease(VoidCallback? value)
```

### onCopy

```dart
VoidCallback? get onCopy
```

[SemanticsAction.copy] 的处理程序。

这是将当前选中内容复制到剪贴板的请求。

例如，Android 上的 TalkBack 用户可以从文本字段的本地上下文菜单中触发此操作。

### onCopy

```dart
set onCopy(VoidCallback? value)
```

### onCut

```dart
VoidCallback? get onCut
```

[SemanticsAction.cut] 的处理程序。

这是剪切当前选中内容并将其放入剪贴板的请求。

例如，Android 上的 TalkBack 用户可以从文本字段的本地上下文菜单中触发此操作。

### onCut

```dart
set onCut(VoidCallback? value)
```

### onPaste

```dart
VoidCallback? get onPaste
```

[SemanticsAction.paste] 的处理程序。

这是粘贴剪贴板当前内容的请求。

例如，Android 上的 TalkBack 用户可以从文本字段的本地上下文菜单中触发此操作。

### onPaste

```dart
set onPaste(VoidCallback? value)
```

### onShowOnScreen

```dart
VoidCallback? get onShowOnScreen
```

[SemanticsAction.showOnScreen] 的处理程序。

在屏幕上完全显示该语义节点的请求。例如，此操作可能会被发送给可滚动列表中部分不在屏幕内的节点，以便将其带入屏幕。

对于可滚动列表中的元素，框架为此操作提供了默认实现，不建议通过此设置器提供自定义实现。

### onShowOnScreen

```dart
set onShowOnScreen(VoidCallback? value)
```

### onMoveCursorForwardByCharacter

```dart
MoveCursorHandler? get onMoveCursorForwardByCharacter
```

[SemanticsAction.moveCursorForwardByCharacter] 的处理程序。

当用户希望将文本字段中的光标向前移动一个字符时，会调用此处理程序。

TalkBack 用户可以在输入焦点位于文本字段中时，通过按音量增大键来触发此操作。

### onMoveCursorForwardByCharacter

```dart
set onMoveCursorForwardByCharacter(MoveCursorHandler? value)
```

### onMoveCursorBackwardByCharacter

```dart
MoveCursorHandler? get onMoveCursorBackwardByCharacter
```

[SemanticsAction.moveCursorBackwardByCharacter] 的处理程序。

当用户希望将文本字段中的光标向后移动一个字符时，会调用此处理程序。

TalkBack 用户可以在输入焦点位于文本字段中时，通过按音量减小键来触发此操作。

### onMoveCursorBackwardByCharacter

```dart
set onMoveCursorBackwardByCharacter(MoveCursorHandler? value)
```

### onMoveCursorForwardByWord

```dart
MoveCursorHandler? get onMoveCursorForwardByWord
```

[SemanticsAction.moveCursorForwardByWord] 的处理程序。

当用户希望将文本字段中的光标向后移动一个单词时，会调用此处理程序。

TalkBack 用户可以在输入焦点位于文本字段中时，通过按音量减小键来触发此操作。

### onMoveCursorForwardByWord

```dart
set onMoveCursorForwardByWord(MoveCursorHandler? value)
```

### onMoveCursorBackwardByWord

```dart
MoveCursorHandler? get onMoveCursorBackwardByWord
```

[SemanticsAction.moveCursorBackwardByWord] 的处理程序。

当用户希望将文本字段中的光标向后移动一个单词时，会调用此处理程序。

TalkBack 用户可以在输入焦点位于文本字段中时，通过按音量减小键来触发此操作。

### onMoveCursorBackwardByWord

```dart
set onMoveCursorBackwardByWord(MoveCursorHandler? value)
```

### onSetSelection

```dart
SetSelectionHandler? get onSetSelection
```

[SemanticsAction.setSelection] 的处理程序。

当用户希望更改文本字段中当前选中的文本或更改光标位置时，会调用此处理程序。

TalkBack 用户可以通过从本地上下文菜单中选择"将光标移到开头/结尾"或"全选"来触发此处理程序。

### onSetSelection

```dart
set onSetSelection(SetSelectionHandler? value)
```

### onSetText

```dart
SetTextHandler? get onSetText
```

[SemanticsAction.setText] 的处理程序。

当用户希望用新文本替换文本字段中的当前文本时，会调用此处理程序。

语音访问用户可以通过对 Android 设备说出"type <text>"来触发此处理程序。

### onSetText

```dart
set onSetText(SetTextHandler? value)
```

### onDidGainAccessibilityFocus

```dart
VoidCallback? get onDidGainAccessibilityFocus
```

[SemanticsAction.didGainAccessibilityFocus] 的处理程序。

当标注了此处理程序的节点获得无障碍焦点时，会调用此处理程序。无障碍焦点是指屏幕上显示的绿色（Android TalkBack）或黑色（iOS VoiceOver）矩形框，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点与输入焦点不同。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

另请参阅：

- [onDidLoseAccessibilityFocus]，当无障碍焦点从该节点移除时调用。
- [FocusNode]、[FocusScope]、[FocusManager]，用于管理输入焦点。

### onDidGainAccessibilityFocus

```dart
set onDidGainAccessibilityFocus(VoidCallback? value)
```

### onDidLoseAccessibilityFocus

```dart
VoidCallback? get onDidLoseAccessibilityFocus
```

[SemanticsAction.didLoseAccessibilityFocus] 的处理程序。

当标注了此处理程序的节点失去无障碍焦点时，会调用此处理程序。无障碍焦点是指屏幕上显示的绿色（Android TalkBack）或黑色（iOS VoiceOver）矩形框，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点与输入焦点不同。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

另请参阅：

- [onDidGainAccessibilityFocus]，当节点获得无障碍焦点时调用。
- [FocusNode]、[FocusScope]、[FocusManager]，用于管理输入焦点。

### onDidLoseAccessibilityFocus

```dart
set onDidLoseAccessibilityFocus(VoidCallback? value)
```

### onFocus

```dart
VoidCallback? get onFocus
```

{@macro flutter.semantics.SemanticsProperties.onFocus}

### onFocus

```dart
set onFocus(VoidCallback? value)
```

### onExpand

```dart
VoidCallback? get onExpand
```

[SemanticsAction.expand] 的处理程序。

这是展开当前获得焦点节点的请求。

### onExpand

```dart
set onExpand(VoidCallback? value)
```

### onCollapse

```dart
VoidCallback? get onCollapse
```

[SemanticsAction.collapse] 的处理程序。

这是折叠当前获得焦点节点的请求。

### onCollapse

```dart
set onCollapse(VoidCallback? value)
```

### childConfigurationsDelegate

```dart
ChildSemanticsConfigurationsDelegate? get childConfigurationsDelegate
```

决定如何处理由 Widget 子树产生的 [SemanticsConfiguration] 的委托。

这些 [SemanticsConfiguration] 由子树中的渲染对象产生，并希望向上合并到其父级。此委托可以决定其中哪些应合并在一起以形成兄弟 SemanticsNode，哪些应向上合并到父 SemanticsNode 中。

如果此语义配置的渲染对象是叶子节点，或者子渲染对象不贡献语义信息，则输入的 [SemanticsConfiguration] 列表可以为空。

### childConfigurationsDelegate

```dart
set childConfigurationsDelegate(ChildSemanticsConfigurationsDelegate? value)
```

### getActionHandler()

```dart
SemanticsActionHandler? getActionHandler(SemanticsAction action)
```

返回为 [action] 注册的操作处理程序；如果未注册任何处理程序，则返回 null。

### sortKey

```dart
SemanticsSortKey? get sortKey
```

确定此节点在其兄弟节点遍历排序顺序中的位置。

这用于描述平台上的无障碍服务（例如 iOS 上的 VoiceOver 和 Android 上的 TalkBack）应遍历该语义节点的顺序。

此排序键是否会影响 [SemanticsNode] 的排序顺序，取决于此配置的使用方式。例如，[absorb] 方法在合并多个 [SemanticsConfiguration] 对象时可能决定不使用此键。

### sortKey

```dart
set sortKey(SemanticsSortKey? value)
```

### indexInParent

```dart
int? get indexInParent
```

此节点在父级语义子节点列表中的索引。

这包括所有语义节点，而不仅仅是当前在子节点列表中的节点。例如，如果一个可滚动对象有五个子节点，但前两个不可见（因此不包含在子节点列表中），则最后一个节点的索引仍将是 4。

### indexInParent

```dart
set indexInParent(int? value)
```

### scrollChildCount

```dart
int? get scrollChildCount
```

贡献语义信息的可滚动子节点总数。

如果子节点的数量未知或无界，则此值为 null。

### scrollChildCount

```dart
set scrollChildCount(int? value)
```

### scrollIndex

```dart
int? get scrollIndex
```

贡献语义信息的第一个可见可滚动子节点的索引。

### scrollIndex

```dart
set scrollIndex(int? value)
```

### platformViewId

```dart
int? get platformViewId
```

平台视图的 ID，其语义节点将作为此节点的子节点添加。

### platformViewId

```dart
set platformViewId(int? value)
```

### maxValueLength

```dart
int? get maxValueLength
```

可输入到可编辑文本字段中的最大字符数。

出于此函数的目的，字符被定义为一个 Unicode 标量值。

此项仅应在 [isTextField] 为 true 时设置。默认为 null，表示对文本字段不施加任何限制。

### maxValueLength

```dart
set maxValueLength(int? value)
```

### currentValueLength

```dart
int? get currentValueLength
```

已输入到可编辑文本字段中的当前字符数。

出于此函数的目的，字符被定义为一个 Unicode 标量值。

此项仅应在 [isTextField] 为 true 时设置。设置 [maxValueLength] 时必须同时设置此项。

### currentValueLength

```dart
set currentValueLength(int? value)
```

### isMergingSemanticsOfDescendants

```dart
bool get isMergingSemanticsOfDescendants
```

拥有者 [RenderObject] 及其所有后代提供的语义信息是否应被视为一个逻辑实体。

如果设置为 true，拥有者 [RenderObject] 的 [SemanticsNode] 的后代将把它们的语义信息合并到代表该拥有者 [RenderObject] 的 [SemanticsNode] 中。

将此项设置为 true 要求 [isSemanticBoundary] 也为 true。

### isMergingSemanticsOfDescendants

```dart
set isMergingSemanticsOfDescendants(bool value)
```

### customSemanticsActions

```dart
Map<CustomSemanticsAction, VoidCallback> get customSemanticsActions
```

每个支持的 [CustomSemanticsAction] 的处理程序。

每当向节点添加自定义无障碍操作时，都会自动添加 [SemanticsAction.customAction] 操作。系统会创建一个处理程序，该处理程序使用传入的参数在此映射中查找自定义操作处理程序，如果存在则调用它。

### customSemanticsActions

```dart
set customSemanticsActions(Map<CustomSemanticsAction, VoidCallback> value)
```

### identifier

```dart
String get identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### identifier

```dart
set identifier(String identifier)
```

### traversalParentIdentifier

```dart
Object? get traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalParentIdentifier

```dart
set traversalParentIdentifier(Object? value)
```

### traversalChildIdentifier

```dart
Object? get traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### traversalChildIdentifier

```dart
set traversalChildIdentifier(Object? value)
```

### role

```dart
SemanticsRole get role
```

{@macro flutter.semantics.SemanticsProperties.role}

### role

```dart
set role(SemanticsRole value)
```

### label

```dart
String get label
```

拥有者 [RenderObject] 的文本描述。

设置此属性将覆盖 [attributedLabel]。

阅读方向由 [textDirection] 给出。

另请参阅：

- [attributedLabel]，此属性的 [AttributedString] 形式。

### label

```dart
set label(String label)
```

### attributedLabel

```dart
AttributedString get attributedLabel
```

拥有者 [RenderObject] 的文本描述，以 [AttributedString] 格式表示。

在 iOS 上，此项用于 `UIAccessibility` 协议中定义的 `accessibilityAttributedLabel` 属性。在 Android 上，它会按以下顺序与 [attributedValue] 和 [attributedHint] 拼接在一起：[attributedValue]、[attributedLabel]、[attributedHint]。拼接后的值随后被用作 `Text` 描述。

阅读方向由 [textDirection] 给出。

另请参阅：

- [label]，此属性的原始文本形式。

### attributedLabel

```dart
set attributedLabel(AttributedString attributedLabel)
```

### value

```dart
String get value
```

拥有者 [RenderObject] 当前值的文本描述。

设置此属性将覆盖 [attributedValue]。

阅读方向由 [textDirection] 给出。

另请参阅：

- [attributedValue]，此属性的 [AttributedString] 形式。
- [increasedValue] 和 [attributedIncreasedValue]，描述执行 [SemanticsAction.increase] 后 [value] 将变为的值。
- [decreasedValue] 和 [attributedDecreasedValue]，描述执行 [SemanticsAction.decrease] 后 [value] 将变为的值。

### value

```dart
set value(String value)
```

### attributedValue

```dart
AttributedString get attributedValue
```

拥有者 [RenderObject] 当前值的文本描述，以 [AttributedString] 格式表示。

在 iOS 上，此项用于 `UIAccessibility` 协议中定义的 `accessibilityAttributedValue` 属性。在 Android 上，它会按以下顺序与 [attributedLabel] 和 [attributedHint] 拼接在一起：[attributedValue]、[attributedLabel]、[attributedHint]。拼接后的值随后被用作 `Text` 描述。

阅读方向由 [textDirection] 给出。

另请参阅：

- [value]，此属性的原始文本形式。
- [attributedIncreasedValue]，描述执行 [SemanticsAction.increase] 后 [value] 将变为的值。
- [attributedDecreasedValue]，描述执行 [SemanticsAction.decrease] 后 [value] 将变为的值。

### attributedValue

```dart
set attributedValue(AttributedString attributedValue)
```

### increasedValue

```dart
String get increasedValue
```

执行 [SemanticsAction.increase] 操作后 [value] 将具有的值。

设置此属性将覆盖 [attributedIncreasedValue]。

如果提供了 [SemanticsAction.increase] 的处理程序，并且设置了 [value] 或 [attributedValue] 之一，则必须设置 [attributedIncreasedValue] 或 [increasedValue] 之一。

阅读方向由 [textDirection] 给出。

另请参阅：

- [attributedIncreasedValue]，此属性的 [AttributedString] 形式。

### increasedValue

```dart
set increasedValue(String increasedValue)
```

### attributedIncreasedValue

```dart
AttributedString get attributedIncreasedValue
```

执行 [SemanticsAction.increase] 操作后 [value] 将具有的值，以 [AttributedString] 格式表示。

如果提供了 [SemanticsAction.increase] 的处理程序，并且设置了 [value] 或 [attributedValue] 之一，则必须设置 [attributedIncreasedValue] 或 [increasedValue] 之一。

阅读方向由 [textDirection] 给出。

另请参阅：

- [increasedValue]，此属性的原始文本形式。

### attributedIncreasedValue

```dart
set attributedIncreasedValue(AttributedString attributedIncreasedValue)
```

### decreasedValue

```dart
String get decreasedValue
```

执行 [SemanticsAction.decrease] 操作后 [value] 将具有的值。

设置此属性将覆盖 [attributedDecreasedValue]。

如果提供了 [SemanticsAction.decrease] 的处理程序，并且设置了 [value] 或 [attributedValue] 之一，则必须设置 [attributedDecreasedValue] 或 [decreasedValue] 之一。

阅读方向由 [textDirection] 给出。

- [attributedDecreasedValue]，此属性的 [AttributedString] 形式。

### decreasedValue

```dart
set decreasedValue(String decreasedValue)
```

### attributedDecreasedValue

```dart
AttributedString get attributedDecreasedValue
```

执行 [SemanticsAction.decrease] 操作后 [value] 将具有的值，以 [AttributedString] 格式表示。

如果提供了 [SemanticsAction.decrease] 的处理程序，并且设置了 [value] 或 [attributedValue] 之一，则必须设置 [attributedDecreasedValue] 或 [decreasedValue] 之一。

阅读方向由 [textDirection] 给出。

另请参阅：

- [decreasedValue]，此属性的原始文本形式。

### attributedDecreasedValue

```dart
set attributedDecreasedValue(AttributedString attributedDecreasedValue)
```

### hint

```dart
String get hint
```

对该节点执行操作后结果的简要描述。

设置此属性将覆盖 [attributedHint]。

阅读方向由 [textDirection] 给出。

另请参阅：

- [attributedHint]，此属性的 [AttributedString] 形式。

### hint

```dart
set hint(String hint)
```

### attributedHint

```dart
AttributedString get attributedHint
```

对该节点执行操作后结果的简要描述，以 [AttributedString] 格式表示。

在 iOS 上，此项用于 `UIAccessibility` 协议中定义的 `accessibilityAttributedHint` 属性。在 Android 上，它会按以下顺序与 [attributedLabel] 和 [attributedValue] 拼接在一起：[attributedValue]、[attributedLabel]、[attributedHint]。拼接后的值随后被用作 `Text` 描述。

阅读方向由 [textDirection] 给出。

另请参阅：

- [hint]，此属性的原始文本形式。

### attributedHint

```dart
set attributedHint(AttributedString attributedHint)
```

### tooltip

```dart
String get tooltip
```

Widget 工具提示的文本描述。

阅读方向由 [textDirection] 给出。

### tooltip

```dart
set tooltip(String tooltip)
```

### hintOverrides

```dart
SemanticsHintOverrides? get hintOverrides
```

在受支持的平台上提供覆盖默认提示的提示值。

### hintOverrides

```dart
set hintOverrides(SemanticsHintOverrides? value)
```

### scopesRoute

```dart
bool get scopesRoute
```

该语义节点是否为应播报其值的子树的根节点。

另请参阅：

- [SemanticsFlag.scopesRoute]，路由作用域的完整说明。

### scopesRoute

```dart
set scopesRoute(bool value)
```

### namesRoute

```dart
bool get namesRoute
```

该语义节点是否包含路由的标签。

另请参阅：

- [SemanticsFlag.namesRoute]，路由命名的完整说明。

### namesRoute

```dart
set namesRoute(bool value)
```

### isImage

```dart
bool get isImage
```

该语义节点是否代表一张图片。

### isImage

```dart
set isImage(bool value)
```

### liveRegion

```dart
bool get liveRegion
```

该语义节点是否为实时区域。

实时区域表示对该语义节点的更新很重要。平台可以利用此信息，向用户礼貌地播报以告知其此节点的更新。

实时区域的一个例子是 [SnackBar] Widget。在 Android 和 iOS 上，即使该 Widget 没有获得无障碍焦点，实时区域也会自动触发一次礼貌播报。如果操作系统的无障碍服务已经在播报其他内容（例如正在朗读获得焦点 Widget 的标签或提供系统播报），则此播报可能不会被朗读。

另请参阅：

- [SemanticsFlag.isLiveRegion]，此设置所控制的语义标志。

### liveRegion

```dart
set liveRegion(bool value)
```

### textDirection

```dart
TextDirection? get textDirection
```

[label]、[value]、[hint]、[increasedValue] 和 [decreasedValue] 中文本的阅读方向。

### textDirection

```dart
set textDirection(TextDirection? textDirection)
```

### isSelected

```dart
bool get isSelected
```

拥有者 [RenderObject] 是否被选中（true）或未被选中（false）。

这与是否具有无障碍焦点不同。获得无障碍焦点的元素可能被选中，也可能未被选中；例如，[ListTile] 可以获得无障碍焦点，但其 [ListTile.selected] 属性设置为 false，此时它不会被标记为已选中。

### isSelected

```dart
set isSelected(bool value)
```

### isExpanded

```dart
bool? get isExpanded
```

如果此节点具有可由用户控制的布尔状态，则该状态是展开还是折叠，分别对应 true 和 false。

如果拥有者 [RenderObject] 不具有可由用户控制的展开/折叠状态，请勿调用此字段的设置器。

如果拥有者 [RenderObject] 不具有展开/折叠状态，获取器将返回 null。

### isExpanded

```dart
set isExpanded(bool? value)
```

### isEnabled

```dart
bool? get isEnabled
```

拥有者 [RenderObject] 当前是否已启用。

已禁用的对象不响应用户交互。只有通常会响应用户交互、但当前不响应（例如被禁用的按钮）的对象，才应被标记为已禁用。

对于从不响应用户交互的对象（例如静态文本），不应调用此设置器。

如果拥有者 [RenderObject] 不支持启用/禁用的概念，获取器将返回 null。

此属性不控制是否启用语义功能。如果希望为特定 Widget 禁用语义功能，应使用 [ExcludeSemantics] Widget。

### isEnabled

```dart
set isEnabled(bool? value)
```

### isChecked

```dart
bool? get isChecked
```

如果此节点具有可由用户控制的布尔状态，则该状态是选中还是未选中，分别对应 true 和 false。

如果拥有者 [RenderObject] 不具有可由用户控制的选中/未选中状态，请勿调用此字段的设置器。

如果拥有者 [RenderObject] 不具有选中/未选中状态，获取器将返回 null。

### isChecked

```dart
set isChecked(bool? value)
```

### isCheckStateMixed

```dart
bool? get isCheckStateMixed
```

如果此节点具有可由用户控制的三态，则该状态是否处于混合状态。

如果拥有者 [RenderObject] 不具有可由用户控制的选中/未选中状态，请勿调用此字段的设置器。

如果拥有者 [RenderObject] 不具有混合选中状态，获取器将返回 null。

### isCheckStateMixed

```dart
set isCheckStateMixed(bool? value)
```

### isToggled

```dart
bool? get isToggled
```

如果此节点具有可由用户控制的布尔状态，则该状态是开启还是关闭，分别对应 true 和 false。

如果拥有者 [RenderObject] 不具有可由用户控制的开/关状态，请勿调用此字段的设置器。

如果拥有者 [RenderObject] 不具有开/关状态，获取器将返回 null。

### isToggled

```dart
set isToggled(bool? value)
```

### isInMutuallyExclusiveGroup

```dart
bool get isInMutuallyExclusiveGroup
```

拥有该配置的 RenderObject 是否对应于允许用户从多个互斥选项中选择一个的 UI。

例如，[Radio] 按钮属于互斥组，因为该组中只能有一个单选按钮被标记为 [isChecked]。

### isInMutuallyExclusiveGroup

```dart
set isInMutuallyExclusiveGroup(bool value)
```

### isFocusable

```dart
bool get isFocusable
```

拥有者 [RenderObject] 是否可以持有输入焦点。

### isFocusable

```dart
set isFocusable(bool value)
```

### isFocused

```dart
bool? get isFocused
```

拥有者 [RenderObject] 当前是否持有输入焦点。

### isFocused

```dart
set isFocused(bool? value)
```

### accessibilityFocusBlockType

```dart
AccessibilityFocusBlockType get accessibilityFocusBlockType
```

拥有者 [RenderObject] 及其子树在无障碍焦点（不同于输入焦点）方面是否被阻止。

### accessibilityFocusBlockType

```dart
set accessibilityFocusBlockType(AccessibilityFocusBlockType value)
```

### isButton

```dart
bool get isButton
```

拥有者 [RenderObject] 是否为按钮（true）或不是（false）。

### isButton

```dart
set isButton(bool value)
```

### isLink

```dart
bool get isLink
```

拥有者 [RenderObject] 是否为链接（true）或不是（false）。

### isLink

```dart
set isLink(bool value)
```

### linkUrl

```dart
Uri? get linkUrl
```

拥有者 [RenderObject] 所链接到的 URL。

### linkUrl

```dart
set linkUrl(Uri? value)
```

### isHeader

```dart
bool get isHeader
```

拥有者 [RenderObject] 是否为标题（true）或不是（false）。

### isHeader

```dart
set isHeader(bool value)
```

### headingLevel

```dart
int get headingLevel
```

表示文档结构中的标题级别。

这仅用于 Web 语义功能，在其他平台上会被忽略。

### headingLevel

```dart
set headingLevel(int value)
```

### isSlider

```dart
bool get isSlider
```

拥有者 [RenderObject] 是否为滑块（true）或不是（false）。

### isSlider

```dart
set isSlider(bool value)
```

### isKeyboardKey

```dart
bool get isKeyboardKey
```

拥有者 [RenderObject] 是否为键盘按键（true）或不是（false）。

### isKeyboardKey

```dart
set isKeyboardKey(bool value)
```

### isHidden

```dart
bool get isHidden
```

拥有者 [RenderObject] 是否被视为隐藏。

隐藏元素当前在屏幕上不可见。它们可能被其他元素遮挡，或者位于视口可见区域之外。

隐藏元素无法通过常规触摸获得无障碍焦点。使其获得焦点的唯一方式是通过线性导航将焦点移动到该元素上。

平台可以完全忽略隐藏元素，并鼓励新平台这样做。

通常应将元素从语义树中完全排除，而不是将其标记为隐藏。隐藏元素仅在为了规避平台限制时才会被包含在语义树中，主要用于在 iOS 上实现无障碍滚动。

### isHidden

```dart
set isHidden(bool value)
```

### isTextField

```dart
bool get isTextField
```

拥有者 [RenderObject] 是否为文本字段。

### isTextField

```dart
set isTextField(bool value)
```

### isReadOnly

```dart
bool get isReadOnly
```

拥有者 [RenderObject] 是否为只读。

仅当 [isTextField] 为 true 时适用。

### isReadOnly

```dart
set isReadOnly(bool value)
```

### isObscured

```dart
bool get isObscured
```

是否应隐藏 [value]。

此选项通常与 [isTextField] 结合使用，以表示文本字段包含密码（或其他敏感信息）。这样做会指示屏幕阅读器不朗读 [value]。

### isObscured

```dart
set isObscured(bool value)
```

### isMultiline

```dart
bool get isMultiline
```

文本字段是否为多行。

此选项通常与 [isTextField] 结合使用，以表示文本字段被配置为多行。

### isMultiline

```dart
set isMultiline(bool value)
```

### isRequired

```dart
bool? get isRequired
```

该语义节点是否具有必填状态。

如果拥有者 [RenderObject] 不具有可由用户控制的必填状态，请勿调用此字段的设置器。

如果拥有者 [RenderObject] 不具有必填状态，获取器将返回 null。

另请参阅：

- [SemanticsFlag.isRequired]，必填节点的完整说明。

### isRequired

```dart
set isRequired(bool? value)
```

### hasImplicitScrolling

```dart
bool get hasImplicitScrolling
```

当用户尝试将焦点移动到屏幕外的子节点时，平台是否可以滚动该语义节点。

例如，[ListView] Widget 具有隐式滚动功能，以便用户可以轻松移动到下一组可见子节点。[TabBar] Widget 不具有隐式滚动功能，以便用户在到达标签栏末尾时可以导航到标签页主体内容。

### hasImplicitScrolling

```dart
set hasImplicitScrolling(bool value)
```

### textSelection

```dart
TextSelection? get textSelection
```

如果此节点代表一个文本字段，则为 [value] 中当前选中的文本（或光标位置）。

### textSelection

```dart
set textSelection(TextSelection? value)
```

### scrollPosition

```dart
double? get scrollPosition
```

如果节点是可滚动的，表示当前滚动位置的逻辑像素值。

属性 [scrollExtentMin] 和 [scrollExtentMax] 表示此属性的有效取值范围。[scrollPosition] 的值可能（暂时）超出该范围，例如在过度滚动期间。

另请参阅：

- [ScrollPosition.pixels]，通常从中取得此值。

### scrollPosition

```dart
set scrollPosition(double? value)
```

### scrollExtentMax

```dart
double? get scrollExtentMax
```

如果节点是可滚动的，表示 [scrollPosition] 的最大有效值。

如果滚动是无界的，此值可能为无穷大。

另请参阅：

- [ScrollPosition.maxScrollExtent]，通常从中取得此值。

### scrollExtentMax

```dart
set scrollExtentMax(double? value)
```

### scrollExtentMin

```dart
double? get scrollExtentMin
```

如果节点是可滚动的，表示 [scrollPosition] 的最小有效值。

如果滚动是无界的，此值可能为无穷大。

另请参阅：

- [ScrollPosition.minScrollExtent]，通常从中取得此值。

### scrollExtentMin

```dart
set scrollExtentMin(double? value)
```

### controlsNodes

```dart
Set<String>? get controlsNodes
```

由此节点控制的 Widget 的 [SemanticsNode.identifier] 集合。

### controlsNodes

```dart
set controlsNodes(Set<String>? value)
```

### validationResult

```dart
SemanticsValidationResult get validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### validationResult

```dart
set validationResult(SemanticsValidationResult value)
```

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior get hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### hitTestBehavior

```dart
set hitTestBehavior(ui.SemanticsHitTestBehavior value)
```

### inputType

```dart
SemanticsInputType get inputType
```

{@macro flutter.semantics.SemanticsProperties.inputType}

### inputType

```dart
set inputType(SemanticsInputType value)
```

### maxValue

```dart
String? get maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### maxValue

```dart
set maxValue(String? value)
```

### minValue

```dart
String? get minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### minValue

```dart
set minValue(String? value)
```

### tagsForChildren

```dart
Iterable<SemanticsTag>? get tagsForChildren
```

此配置希望添加到所有子 [SemanticsNode] 的标签集合。

另请参阅：

- [addTagForChildren]，用于添加标签，以及有关其用法的更多信息。

### tagsChildrenWith()

```dart
bool tagsChildrenWith(SemanticsTag tag)
```

此配置是否会用给定的 [SemanticsTag] 标记子语义节点。

### addTagForChildren()

```dart
void addTagForChildren(SemanticsTag tag)
```

指定此配置希望应用于所有子 [SemanticsNode] 的 [SemanticsTag]。

在寻求附加到父 [SemanticsNode] 的过程中，该标签会被添加到所有经过此配置拥有者 [RenderObject] 的 [SemanticsNode]。

标签用于向父 [SemanticsNode] 传达子 [SemanticsNode] 经过了某个特定 [RenderObject] 的信息。父节点可以利用此信息确定语义树的形状。

另请参阅：

- [RenderViewport.excludeFromScrolling]，标签用法的一个示例。

### isCompatibleWith()

```dart
bool isCompatibleWith(SemanticsConfiguration? other)
```

此配置是否与提供的 `other` 配置兼容。

如果两个配置可以添加到同一个 [SemanticsNode] 而不丢失任何语义信息，则称它们是兼容的。

### absorb()

```dart
void absorb(SemanticsConfiguration child)
```

将来自 `child` 的语义信息吸收到此配置中。

这会将两个配置的语义信息相加，并将结果保存在此配置中。

拥有 `child` 配置的 [RenderObject] 必须是拥有此配置的 [RenderObject] 的后代。

只有将 [explicitChildNodes] 设置为 false 的配置才能吸收其他配置，并且建议仅吸收由 [isCompatibleWith] 确定为兼容的配置。

### copy()

```dart
SemanticsConfiguration copy()
```

返回此配置的精确副本。

# DebugSemanticsDumpOrder

```dart
enum DebugSemanticsDumpOrder {}
```

由 [debugDumpSemanticsTree] 使用，用于指定子节点的打印顺序。

按反向命中测试顺序打印节点。

在反向命中测试顺序中，[SemanticsNode] 的最后一个子节点将首先被询问是否要响应用户交互，其次是倒数第二个，依此类推，直到找到接受者为止。

按语义遍历顺序打印节点。

这是用户使用"下一个"和"上一个"手势导航 UI 时的顺序。

# SemanticsSortKey

```dart
abstract class SemanticsSortKey with Diagnosticable implements Comparable<SemanticsSortKey> {}
```

[SemanticsProperties.sortKey] 无障碍遍历顺序排序的所有排序键的基类。

排序键先按 [name] 排序，然后按子类实现的比较方式排序。如果指定了 [SemanticsProperties.sortKey]，则同一语义组内的排序键必须都是相同类型。

没有 [name] 的键会与其他没有 [name] 的键进行比较，并且会在具有 [name] 的键之前被遍历。

如果没有对语义节点应用排序键，则将使用与平台相关的默认算法对其进行排序。

另请参阅：

- [OrdinalSortKey]，一种使用序数进行排序的排序键。

### SemanticsSortKey()

```dart
SemanticsSortKey({String? name})
```

抽象 const 构造函数。此构造函数使子类能够提供 const 构造函数，以便可以在 const 表达式中使用它们。

### name

```dart
String? name
```

一个可选名称，将此排序键与具有相同 [name] 的其他排序键分为一组。

进行比较时，排序键必须具有相同的 `runtimeType`。

没有 [name] 的键会与其他没有 [name] 的键进行比较，并且会在具有 [name] 的键之前被遍历。

### compareTo()

```dart
int compareTo(SemanticsSortKey other)
```

### doCompare()

```dart
int doCompare(SemanticsSortKey other)
```

[compareTo] 的实现。

参数保证与此对象类型相同且具有相同的 [name]。

如果此对象在排序顺序中排在参数之前，该方法应返回一个负数；如果排在其后，应返回一个正数。返回零会导致系统使用默认排序顺序。

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OrdinalSortKey

```dart
class OrdinalSortKey extends SemanticsSortKey {}
```

一种根据给定的 `double` 值进行排序的 [SemanticsSortKey]。

[OrdinalSortKey] 会与其他 [OrdinalSortKey] 进行比较，以按照给定的顺序进行排序。

[OrdinalSortKey] 先按可选的 [name] 排序，然后按其 [order] 排序。如果 [SemanticsProperties.sortKey] 是 [OrdinalSortKey]，则同一语义组中指定的所有其他排序键也必须是 [OrdinalSortKey]。

没有 [name] 的键会与其他没有 [name] 的键进行比较，并且会在具有 [name] 的键之前被遍历。

序数值 [order] 通常为整数，但也可以是分数，例如为了使其恰好位于另外两个连续整数之间。该值必须是有限数（不能是 [double.nan]、[double.infinity] 或 [double.negativeInfinity]）。

### OrdinalSortKey()

```dart
OrdinalSortKey(double order, {String? name})
```

创建一个使用 [double] 作为其键值的 const 语义排序键。

[order] 必须是有限数。

### order

```dart
double order
```

确定此键在定义此节点被平台无障碍服务遍历顺序的键序列中的位置。

值越小越先被遍历。具有相同 [name] 的键将被分为一组，并首先按名称排序，然后按 [order] 排序。

### doCompare()

```dart
int doCompare(OrdinalSortKey other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
