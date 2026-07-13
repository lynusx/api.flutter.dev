# SemanticsNode

```dart
class SemanticsNode with DiagnosticableTreeMixin {}
```

表示某些语义数据的节点。

语义树在管线的语义阶段(即 [PipelineOwner.flushSemantics] 期间)维护,该阶段发生在合成之后。此后,语义树会被上传到引擎,供辅助技术使用。

### SemanticsNode()

```dart
SemanticsNode({Key? key, VoidCallback? showOnScreen})
```

创建一个语义节点。

每个语义节点在创建时都会被分配一个唯一标识符。

### SemanticsNode.root()

```dart
SemanticsNode.root({Key? key, VoidCallback? showOnScreen, required SemanticsOwner owner})
```

创建一个表示语义树根节点的语义节点。

根节点被分配的标识符为零。

### key

```dart
Key? key
```

在兄弟节点列表中唯一标识此节点。

键用于构建语义树。它们不会被传递到引擎。

### id

```dart
int get id
```

此节点的唯一标识符。

根节点的 id 为零。其他节点在附加到 [SemanticsOwner] 时会被赋予一个唯一 id。如果节点被分离,则其 id 将失效,不应再使用。

在极少数情况下,如果此节点被分离后又重新附加到 [SemanticsOwner],id 可能会发生变化。这种情况只应在应用生成了过多语义节点时发生。

### transform

```dart
Matrix4? get transform
```

此节点的坐标系到其父节点坐标系的变换。

默认情况下,该变换为 null,表示恒等变换(即此节点与其父节点具有相同的坐标系)。

### transform

```dart
set transform(Matrix4? value)
```

### rect

```dart
Rect get rect
```

此节点在其坐标系中的边界框。

### rect

```dart
set rect(Rect value)
```

### parentSemanticsClipRect

```dart
Rect? parentSemanticsClipRect
```

应用于此节点的祖先语义裁剪矩形。

以该节点的坐标系表示。如果没有应用裁剪,则可能为 null。

位于此矩形之外的后代 [SemanticsNode] 将从语义树中排除。与此矩形重叠但位于 [parentPaintClipRect] 之外的后代 [SemanticsNode] 将被包含在树中,但会被标记为隐藏,因为它们被认为在屏幕上不可见。

如果此矩形为 null,则所有位于 [parentPaintClipRect] 之外的后代 [SemanticsNode] 都将从树中排除。

如果此矩形非空,则它必须完全包含 [parentPaintClipRect]。如果 [parentPaintClipRect] 为 null,则此属性也为 null。

### parentPaintClipRect

```dart
Rect? parentPaintClipRect
```

应用于此节点的祖先绘制裁剪矩形。

以该节点的坐标系表示。如果没有应用裁剪,则可能为 null。

位于此矩形之外的后代 [SemanticsNode] 要么从语义树中排除(如果它们与 [parentSemanticsClipRect] 没有重叠),要么被包含并标记为隐藏(如果它们与 [parentSemanticsClipRect] 重叠)。

此矩形完全被 [parentSemanticsClipRect] 包含。

如果此矩形为 null,则 [parentSemanticsClipRect] 也必须为 null。

### indexInParent

```dart
int? indexInParent
```

此节点在父节点语义子节点列表中的索引。

这包括所有语义节点,而不仅仅是当前在子节点列表中的那些。例如,如果一个可滚动组件有五个子节点,但前两个不可见(因此未包含在子节点列表中),则最后一个节点的索引仍为 4。

### isInvisible

```dart
bool get isInvisible
```

节点是否不可见。

如果节点的 [rect] 位于屏幕边界之外因而用户无法访问,并且其语义信息没有按照 [isMergedIntoParent] 所指示的那样合并到(部分)可见的父节点中,则该节点被视为不可见。

可以安全地从语义树中移除不可见的节点,而不会丢失与当前屏幕上显示内容相关的语义信息。

### isMergedIntoParent

```dart
bool get isMergedIntoParent
```

此节点是否将其语义信息合并到某个祖先节点中。

此值表示此节点是否存在任何将 [mergeAllDescendantsIntoThisNode] 设置为 true 的祖先节点。

### isMergedIntoParent

```dart
set isMergedIntoParent(bool value)
```

### areUserActionsBlocked

```dart
bool get areUserActionsBlocked
```

用户是否可以在辅助技术中与此节点交互。

即使此值为 true,此节点仍可以接收辅助功能焦点。将其设置为 true 会阻止用户激活与指针相关的 [SemanticsAction],例如 [SemanticsAction.tap] 或 [SemanticsAction.longPress]。

### areUserActionsBlocked

```dart
set areUserActionsBlocked(bool value)
```

### isPartOfNodeMerging

```dart
bool get isPartOfNodeMerging
```

此节点是否参与语义信息的合并。

如果该节点被合并到祖先节点中,或者有后代节点被合并到此节点中,则返回 true。

另请参阅:

- [isMergedIntoParent]
- [mergeAllDescendantsIntoThisNode]

### mergeAllDescendantsIntoThisNode

```dart
bool get mergeAllDescendantsIntoThisNode
```

此节点及其所有后代是否应被视为一个逻辑实体。

### hasChildren

```dart
bool get hasChildren
```

此节点是否具有非零数量的子节点。

### childrenCount

```dart
int get childrenCount
```

此节点在命中测试(绘制)顺序中的子节点数量。

### childrenCountInTraversalOrder

```dart
int get childrenCountInTraversalOrder
```

此节点在遍历顺序中的子节点数量。

### visitChildren()

```dart
void visitChildren(SemanticsNodeVisitor visitor)
```

访问此节点的直接子节点。

此函数为每个直接子节点调用 visitor,直到 visitor 返回 false。

### owner

```dart
SemanticsOwner? get owner
```

此节点的所有者(如果未附加则为 null)。

此节点所属的整个语义树将具有相同的所有者。

### attached

```dart
bool get attached
```

此节点所属的语义树是否已附加到 [SemanticsOwner]。

在调用 [attach] 期间,此值变为 true。

在调用 [detach] 期间,此值变为 false。

### parent

```dart
SemanticsNode? get parent
```

此节点在语义树中的父节点。

语义树中根节点的 [parent] 为 null。

### traversalParent

```dart
SemanticsNode? get traversalParent
```

此节点在遍历顺序中的实际父节点。

这对于 [OverlayPortal] 或类似场景很有用,在这些场景中,节点的命中测试父节点(即 [parent])与其遍历父节点(即 [traversalParent])不同。如果此节点表示一个 overlay portal 子节点,则 [traversalParent] 是遍历顺序中的 overlay portal 父节点。否则,它与 [parent] 相同。当需要按遍历顺序更新此节点的变换时,将使用 [traversalParent]。

### traversalParent

```dart
set traversalParent(SemanticsNode? value)
```

### depth

```dart
int get depth
```

此节点在语义树中的深度。

树中节点的深度随着向下遍历树而单调递增。兄弟节点之间的深度没有保证关系。

深度用于确保节点按深度顺序处理。

### attach()

```dart
void attach(SemanticsOwner owner)
```

将此节点标记为已附加到给定的所有者。

### detach()

```dart
void detach()
```

将此节点标记为已从其所有者分离。

### debugIsDirty

```dart
bool? get debugIsDirty
```

当启用断言时,返回节点是否被标记为脏(dirty)。

否则,返回 null。

此获取器仅用于框架单元测试。应用程序不得依赖其值。

### tags

```dart
Set<SemanticsTag>? tags
```

此节点被标记的 [SemanticsTag]。

标签用于构建语义树。它们不会被传递到引擎。

### isTagged()

```dart
bool isTagged(SemanticsTag tag)
```

此节点是否被标记为 `tag`。

### flagsCollection

```dart
SemanticsFlags get flagsCollection
```

语义标志。

### hasFlag()

```dart
bool hasFlag(SemanticsFlag flag)
```

此节点当前是否具有给定的 [SemanticsFlag]。

### identifier

```dart
String get identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### traversalParentIdentifier

```dart
Object? get traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalChildIdentifier

```dart
Object? get traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### label

```dart
String get label
```

此节点的文本描述。

阅读方向由 [textDirection] 给出。

这会暴露 [attributedLabel] 的原始文本。

### attributedLabel

```dart
AttributedString get attributedLabel
```

此节点的文本描述,以 [AttributedString] 格式表示。

阅读方向由 [textDirection] 给出。

另请参阅 [label],它仅暴露原始文本。

### value

```dart
String get value
```

节点当前值的文本描述。

阅读方向由 [textDirection] 给出。

这会暴露 [attributedValue] 的原始文本。

### attributedValue

```dart
AttributedString get attributedValue
```

节点当前值的文本描述,以 [AttributedString] 格式表示。

阅读方向由 [textDirection] 给出。

另请参阅 [value],它仅暴露原始文本。

### increasedValue

```dart
String get increasedValue
```

在执行 [SemanticsAction.increase] 操作后 [value] 将具有的值。

此属性仅在此节点上 [SemanticsAction.increase] 操作可用时有效。

阅读方向由 [textDirection] 给出。

这会暴露 [attributedIncreasedValue] 的原始文本。

### attributedIncreasedValue

```dart
AttributedString get attributedIncreasedValue
```

在执行 [SemanticsAction.increase] 操作后, [value] 或 [attributedValue] 将具有的 [AttributedString] 格式的值。

此属性仅在此节点上 [SemanticsAction.increase] 操作可用时有效。

阅读方向由 [textDirection] 给出。

另请参阅 [increasedValue],它仅暴露原始文本。

### decreasedValue

```dart
String get decreasedValue
```

在执行 [SemanticsAction.decrease] 操作后 [value] 将具有的值。

此属性仅在此节点上 [SemanticsAction.decrease] 操作可用时有效。

阅读方向由 [textDirection] 给出。

这会暴露 [attributedDecreasedValue] 的原始文本。

### attributedDecreasedValue

```dart
AttributedString get attributedDecreasedValue
```

在执行 [SemanticsAction.decrease] 操作后, [value] 或 [attributedValue] 将具有的 [AttributedString] 格式的值。

此属性仅在此节点上 [SemanticsAction.decrease] 操作可用时有效。

阅读方向由 [textDirection] 给出。

另请参阅 [decreasedValue],它仅暴露原始文本。

### hint

```dart
String get hint
```

对在此节点上执行操作的结果的简要描述。

阅读方向由 [textDirection] 给出。

这会暴露 [attributedHint] 的原始文本。

### attributedHint

```dart
AttributedString get attributedHint
```

对在此节点上执行操作的结果的简要描述,以 [AttributedString] 格式表示。

阅读方向由 [textDirection] 给出。

另请参阅 [hint],它仅暴露原始文本。

### tooltip

```dart
String get tooltip
```

该 Widget 工具提示的文本描述。

阅读方向由 [textDirection] 给出。

### hintOverrides

```dart
SemanticsHintOverrides? get hintOverrides
```

在受支持的平台上提供覆盖默认提示的提示值。

### textDirection

```dart
TextDirection? get textDirection
```

[label]、[value]、[hint]、[increasedValue] 和 [decreasedValue] 的阅读方向。

### sortKey

```dart
SemanticsSortKey? get sortKey
```

确定此节点在其兄弟节点中的遍历排序位置。

用于描述平台上的辅助功能服务(例如 iOS 上的 VoiceOver 和 Android 上的 TalkBack)应遍历语义节点的顺序。

### textSelection

```dart
TextSelection? get textSelection
```

如果此节点表示一个文本字段,则为 [value] 中当前选中的文本(或光标位置)。

### isMultiline

```dart
bool? get isMultiline
```

如果此节点表示一个文本字段,则指示它是否为多行文本字段。

### scrollChildCount

```dart
int? get scrollChildCount
```

贡献于语义的可滚动子节点总数。

如果子节点数量未知或无界,则此值为 null。

### scrollIndex

```dart
int? get scrollIndex
```

滚动节点第一个可见语义子节点的索引。

### scrollPosition

```dart
double? get scrollPosition
```

如果节点可滚动,则表示当前的滚动位置(以逻辑像素为单位)。

属性 [scrollExtentMin] 和 [scrollExtentMax] 表示此属性的有效取值范围。[scrollPosition] 的值可能(暂时)超出该范围,例如在过度滚动期间。

另请参阅:

- [ScrollPosition.pixels],通常从中获取此值。

### scrollExtentMax

```dart
double? get scrollExtentMax
```

如果节点可滚动,则表示 [scrollPosition] 的最大有效范围值。

如果滚动无界,此值可能为无穷大。

另请参阅:

- [ScrollPosition.maxScrollExtent],通常从中获取此值。

### scrollExtentMin

```dart
double? get scrollExtentMin
```

如果节点可滚动,则表示 [scrollPosition] 的最小有效范围值。

如果滚动无界,此值可能为无穷大。

另请参阅:

- [ScrollPosition.minScrollExtent],通常从中获取此值。

### platformViewId

```dart
int? get platformViewId
```

平台视图的 id,该平台视图的语义节点将作为子节点添加到此节点。

如果此值非空,则 SemanticsNode 不得有任何子节点,因为它们将被引用的平台视图的语义节点所替代。

另请参阅:

- [AndroidView],这是 Android 的平台视图。
- [UiKitView],这是 iOS 的平台视图。

### maxValueLength

```dart
int? get maxValueLength
```

可输入到可编辑文本字段中的最大字符数。

就此函数而言,字符被定义为一个 Unicode 标量值。

此属性只应在设置了 [SemanticsFlag.isTextField] 时设置。默认为 null,表示对文本字段没有施加限制。

### currentValueLength

```dart
int? get currentValueLength
```

当前已输入到可编辑文本字段中的字符数。

就此函数而言,字符被定义为一个 Unicode 标量值。

此属性只应在设置了 [SemanticsFlag.isTextField] 时设置。当设置了 [maxValueLength] 时必须设置此属性。

### headingLevel

```dart
int get headingLevel
```

该 Widget 在屏幕结构层级中作为标题的级别。值为 1 表示最高级别的结构层级,值为 2 表示下一级别,依此类推。

### linkUrl

```dart
Uri? get linkUrl
```

此节点链接到的 URL。

### role

```dart
SemanticsRole get role
```

{@template flutter.semantics.SemanticsNode.role}
此节点表示的角色

节点的角色有助于屏幕阅读器等辅助技术正确理解和与 UI 交互。

有关可能角色的列表,请参阅 [SemanticsRole]。
{@endtemplate}

### controlsNodes

```dart
Set<String>? get controlsNodes
```

{@template flutter.semantics.SemanticsNode.controlsNodes}
此节点所控制的 Widget 的 [SemanticsNode.identifier]。
{@endtemplate}

{@macro flutter.semantics.SemanticsProperties.controlsNodes}

### minValue

```dart
String? get minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### maxValue

```dart
String? get maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### validationResult

```dart
SemanticsValidationResult get validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior get hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### inputType

```dart
SemanticsInputType get inputType
```

{@template flutter.semantics.SemanticsNode.inputType}
可编辑节点的输入类型。

此属性仅在此节点表示一个文本字段时使用。

辅助技术使用此属性为用户提供更好的信息。例如,屏幕阅读器在文本字段获得焦点时会读出其输入类型。
{@endtemplate}

### updateWith()

```dart
void updateWith({required SemanticsConfiguration? config, List<SemanticsNode>? childrenInInversePaintOrder})
```

重新配置此对象的属性,以描述 `config` 参数中提供的配置以及 `childrenInInversePaintOrder` 参数中列出的子节点。

这些参数可以为 null;这表示一个空配置(所有值均为默认值,没有子节点)。

不会保留对 [SemanticsConfiguration] 对象的引用,但子节点列表会按原样使用,因此在此调用之后不应更改它。

### getSemanticsData()

```dart
SemanticsData getSemanticsData()
```

返回此节点语义的摘要。

如果此节点设置了 [mergeAllDescendantsIntoThisNode],则返回的数据包括来自此节点后代的信息。否则,返回的数据与此节点上的数据一致。

### sendEvent()

```dart
void sendEvent(SemanticsEvent event)
```

发送与此 [SemanticsNode] 关联的 [SemanticsEvent]。

应发送语义事件,以将 UI 变更告知相关方(如操作系统的辅助功能系统)。

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines, DiagnosticLevel minLevel = DiagnosticLevel.debug, DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder, int wrapWidth = 65})
```

返回此节点及其后代的字符串表示形式。

[SemanticsNode] 子节点的打印顺序由 [childOrder] 参数控制。

### toDiagnosticsNode()

```dart
DiagnosticsNode toDiagnosticsNode({String? name, DiagnosticsTreeStyle? style = DiagnosticsTreeStyle.sparse, DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder})
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren({DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder})
```

### debugListChildrenInOrder()

```dart
List<SemanticsNode> debugListChildrenInOrder(DebugSemanticsDumpOrder childOrder)
```

按指定顺序返回此节点的直接子节点列表。

# SemanticsOwner

```dart
class SemanticsOwner extends ChangeNotifier {}
```

拥有 [SemanticsNode] 对象,并在渲染树语义发生变化时通知监听者。

要监听语义更新,请调用 [SemanticsBinding.ensureSemantics] 或 [PipelineOwner.ensureSemantics] 以获取 [SemanticsHandle]。这将在必要时创建一个 [SemanticsOwner]。

### SemanticsOwner()

```dart
SemanticsOwner({required SemanticsUpdateCallback onSemanticsUpdate})
```

创建一个管理零个或多个 [SemanticsNode] 对象的 [SemanticsOwner]。

### onSemanticsUpdate

```dart
SemanticsUpdateCallback onSemanticsUpdate
```

[onSemanticsUpdate] 回调预期会将 [SemanticsUpdate] 分派给与此 [PipelineOwner] 和/或 [SemanticsOwner] 关联的 [FlutterView]。

[SemanticsOwner] 会在 [sendSemanticsUpdate] 期间调用 [onSemanticsUpdate],此时机在 [SemanticsUpdate] 构建完成之后,但在 [SemanticsOwner] 的监听者收到通知之前。

### rootSemanticsNode

```dart
SemanticsNode? get rootSemanticsNode
```

语义树的根节点(如果有)。

如果语义树为空,则返回 null。

### getSemanticsNode()

```dart
SemanticsNode? getSemanticsNode(int id)
```

返回具有给定 [id] 的 [SemanticsNode](如果存在)。

### dispose()

```dart
void dispose()
```

### sendSemanticsUpdate()

```dart
void sendSemanticsUpdate()
```

使用 [onSemanticsUpdate] 更新语义。

### performAction()

```dart
void performAction(int id, SemanticsAction action, [Object? args])
```

要求具有给定 id 的 [SemanticsNode] 执行给定的操作。

如果 [SemanticsNode] 未表明它可以执行该操作,则此函数不执行任何操作。

如果给定的 `action` 需要参数,则需要通过 `args` 参数传递。

### performActionAt()

```dart
void performActionAt(Offset position, SemanticsAction action, [Object? args])
```

要求给定位置的 [SemanticsNode] 执行给定的操作。

如果 [SemanticsNode] 未表明它可以执行该操作,则此函数不执行任何操作。

如果给定的 `action` 需要参数,则需要通过 `args` 参数传递。

### toString()

```dart
String toString()
```
