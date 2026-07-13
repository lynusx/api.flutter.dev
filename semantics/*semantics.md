@docImport 'dart:ui';

@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# SemanticsNodeVisitor

```dart
typedef SemanticsNodeVisitor = bool Function(SemanticsNode node)
```

为每个 [SemanticsNode] 调用的函数签名。

返回 false 以停止访问节点。

由 [SemanticsNode.visitChildren] 使用。

# MoveCursorHandler

```dart
typedef MoveCursorHandler = void Function(bool extendSelection)
```

用于移动光标的 [SemanticsAction] 的函数签名。

如果 `extendSelection` 设置为 true，则光标移动应扩展当前选区（或者，如果当前没有选中任何内容，则开始一个新的选区）。

# SetSelectionHandler

```dart
typedef SetSelectionHandler = void Function(TextSelection selection)
```

[SemanticsAction.setSelection] 处理器的函数签名，用于将文本选区（或光标位置）更改为 `selection`。

# SetTextHandler

```dart
typedef SetTextHandler = void Function(String text)
```

[SemanticsAction.setText] 处理器的函数签名，用于将当前文本替换为输入的 `text`。

# ScrollToOffsetHandler

```dart
typedef ScrollToOffsetHandler = void Function(Offset targetOffset)
```

[SemanticsAction.scrollToOffset] 处理器的函数签名，用于将可滚动容器滚动到指定的 `targetOffset`。

# SemanticsActionHandler

```dart
typedef SemanticsActionHandler = void Function(Object? args)
```

[SemanticsAction] 处理器的函数签名。

由 [SemanticsConfiguration.getActionHandler] 返回。

# SemanticsUpdateCallback

```dart
typedef SemanticsUpdateCallback = void Function(SemanticsUpdate update)
```

接收语义更新并不返回任何结果的函数签名。

由 [SemanticsOwner.onSemanticsUpdate] 使用。

# ChildSemanticsConfigurationsDelegate

```dart
typedef ChildSemanticsConfigurationsDelegate = ChildSemanticsConfigurationsResult Function(List<SemanticsConfiguration>)
```

[SemanticsConfiguration.childConfigurationsDelegate] 的函数签名。

输入列表包含所有希望向上合并的渲染子级所对应的 [SemanticsConfiguration]。可以用 [SemanticsTag] 标记某个渲染子级，并通过 [SemanticsConfiguration.tagsChildrenWith] 查找其 [SemanticsConfiguration]。

返回值是这些配置的排列方式，包括哪些配置继续向上合并，哪些配置组成兄弟合并组。

使用 [ChildSemanticsConfigurationsResultBuilder] 生成返回值。

# AccessibilityFocusBlockType

```dart
enum AccessibilityFocusBlockType {}
```

控制无障碍焦点的阻止方式。

通常用于防止屏幕阅读器聚焦到 UI 的某些部分。

设置此属性还会阻止该语义节点报告键盘可聚焦性，但不会影响由 [FocusNode] 处理的实际键盘焦点。

无障碍焦点**未被阻止**。

阻止整个子树的无障碍焦点。

仅阻止**当前节点**的无障碍焦点。其后代节点可能仍然可以获得焦点。

两个节点合并时所使用的 AccessibilityFocusBlockType。

# SemanticsTag

```dart
class SemanticsTag {}
```

[SemanticsNode] 的标签。

标签可以被 [SemanticsNode] 的父节点解读，父节点可以根据标签的存在与否来决定如何将带标签的节点添加为子节点。标签不会被发送到引擎。

例如，[RenderSemanticsGestureHandler] 使用标签来确定某个子节点是否应从可滚动区域中排除（就语义而言）。

提供的 [name] 仅用于调试。使用 `new` 操作符创建的两个具有相同 [name] 的标签并不被视为相同。但是，使用 `const` 操作符创建的两个具有相同 [name] 的标签始终相同。

### SemanticsTag()

```dart
SemanticsTag(String name)
```

创建一个 [SemanticsTag]。

提供的 [name] 仅用于调试。使用 `new` 操作符创建的两个具有相同 [name] 的标签并不被视为相同。但是，使用 `const` 操作符创建的两个具有相同 [name] 的标签始终相同。

### name

```dart
String name
```

此标签的可读名称，用于调试。

该字符串不用于判断两个标签是否相同。

### toString()

```dart
String toString()
```

# ChildSemanticsConfigurationsResult

```dart
class ChildSemanticsConfigurationsResult {}
```

包含子级 [SemanticsConfiguration] 排列方式的结果。

当 [PipelineOwner] 构建语义树时，它使用 [SemanticsConfiguration.childConfigurationsDelegate] 返回的 [ChildSemanticsConfigurationsResult] 来决定语义节点应如何形成。

使用 [ChildSemanticsConfigurationsResultBuilder] 构建该结果。

### mergeUp

```dart
List<SemanticsConfiguration> mergeUp
```

返回应合并到父语义节点中的 [SemanticsConfiguration]。

属于语义边界或与其他 [SemanticsConfiguration] 存在冲突的 [SemanticsConfiguration] 将形成独立的语义节点。其余的都将合并到父节点中。

### siblingMergeGroups

```dart
List<List<SemanticsConfiguration>> siblingMergeGroups
```

希望合并在一起并形成一个兄弟 [SemanticsNode] 的子级语义配置组。

在给定组中，属于语义边界或与同组中其他 [SemanticsConfiguration] 存在冲突的所有 [SemanticsConfiguration] 都将从该兄弟合并组中排除，并照常形成独立的语义节点。

合并所产生的结果 [SemanticsNode] 将作为直接父语义节点的兄弟节点被附加上去。例如，`RenderObjectA` 有一个渲染子级 `RenderObjectB`。如果它们都各自形成自己的语义节点 `SemanticsNodeA` 和 `SemanticsNodeB`，那么由 `RenderObjectB` 的兄弟合并组产生的任何语义节点都将作为 `SemanticsNodeB` 的兄弟节点附加到 `SemanticsNodeA` 上。

# ChildSemanticsConfigurationsResultBuilder

```dart
class ChildSemanticsConfigurationsResultBuilder {}
```

用于根据注解构建 [ChildSemanticsConfigurationsResult] 的构建器。

要使用此构建器，可以使用 [markAsMergeUp] 和 [markAsSiblingMergeGroup] 来标注 [SemanticsConfiguration] 的排列方式。一旦所有配置都完成标注，就可以使用 [build] 生成 [ChildSemanticsConfigurationsResult]。

### ChildSemanticsConfigurationsResultBuilder()

```dart
ChildSemanticsConfigurationsResultBuilder()
```

创建一个 [ChildSemanticsConfigurationsResultBuilder]。

### markAsMergeUp()

```dart
void markAsMergeUp(SemanticsConfiguration config)
```

将该 [SemanticsConfiguration] 标记为需要合并到父语义节点中。

该 [SemanticsConfiguration] 将被添加到此构建器所构建的 [ChildSemanticsConfigurationsResult.mergeUp] 中。

### markAsSiblingMergeGroup()

```dart
void markAsSiblingMergeGroup(List<SemanticsConfiguration> configs)
```

将一组 [SemanticsConfiguration] 标记为需要合并在一起，并形成一个兄弟 [SemanticsNode]。

这组 [SemanticsConfiguration] 将被添加到此构建器所构建的 [ChildSemanticsConfigurationsResult.siblingMergeGroups] 中。

### build()

```dart
ChildSemanticsConfigurationsResult build()
```

构建一个包含该排列方式的 [ChildSemanticsConfigurationsResult]。

# CustomSemanticsAction

```dart
class CustomSemanticsAction {}
```

自定义语义操作的标识符。

可以提供自定义语义操作，使复杂的用户交互更易于访问。例如，如果某个应用程序具有需要用户按住某项内容才能移动它的拖放列表，那么使用硬件开关与应用程序交互的用户可能会遇到困难。可以通过创建自定义操作，并将其与用于在列表中上移或下移某个项目的处理器配对，来使其变得可访问。

在 Android 上，这些操作会显示在本地上下文菜单中。在 iOS 上，这些操作会显示在径向上下文菜单中。

本地化和文本方向不会自动应用于所提供的 label 或 hint。

此类的实例应使用 const 实例化，或将新实例缓存在静态字段中。

另请参阅：

- [SemanticsProperties]，其中提供了自定义操作的处理器。

### CustomSemanticsAction()

```dart
CustomSemanticsAction({required String? label})
```

创建一个新的 [CustomSemanticsAction]。

[label] 不能为空。

### CustomSemanticsAction.overridingAction()

```dart
CustomSemanticsAction.overridingAction({required String? hint, required SemanticsAction? action})
```

创建一个覆盖标准语义操作的新 [CustomSemanticsAction]。

[hint] 不能为空。

### label

```dart
String? label
```

此自定义语义操作的用户可读名称。

### hint

```dart
String? hint
```

此自定义语义操作的提示说明。

### action

```dart
SemanticsAction? action
```

此操作所替换的标准语义操作。

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```

### getIdentifier()

```dart
int getIdentifier(CustomSemanticsAction action)
```

获取给定 `action` 的标识符。

### getAction()

```dart
CustomSemanticsAction? getAction(int id)
```

获取给定标识符对应的 `action`。

### resetForTests()

```dart
void resetForTests()
```

在测试之间重置内部状态。如果断言被禁用，则不执行任何操作。

# AttributedString

```dart
class AttributedString {}
```

携带 [StringAttribute] 列表的字符串。

### AttributedString()

```dart
AttributedString(String string, {List<StringAttribute> attributes = const <StringAttribute>[]})
```

创建一个带属性的字符串。

[attributes] 中的 [TextRange] 必须在 [string] 的长度范围内。

创建带属性字符串后，不得更改 [attributes]。

### string

```dart
String string
```

带属性字符串中存储的纯字符串。

### attributes

```dart
List<StringAttribute> attributes
```

该字符串携带的属性。

创建该字符串后不得修改此列表。

### operator +()

```dart
AttributedString operator +(AttributedString other)
```

通过连接操作数返回一个新的 [AttributedString]

返回的 [AttributedString] 的字符串属性列表将包含来自两个操作数、并已更新文本范围的字符串属性。

### operator ==()

```dart
bool operator ==(Object other)
```

如果两个 [AttributedString] 的字符串和属性均相等，则它们相等。

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# AttributedStringProperty

```dart
class AttributedStringProperty extends DiagnosticsProperty<AttributedString> {}
```

用于 [AttributedString] 的 [DiagnosticsProperty]，在没有属性时显示字符串，否则显示更多细节。

### AttributedStringProperty()

```dart
AttributedStringProperty(String name, dynamic value, {dynamic showName, bool showWhenEmpty = false, dynamic defaultValue, dynamic level, dynamic description})
```

为 [AttributedString] 对象创建诊断属性。

此类属性用于 [SemanticsData] 对象。

### showWhenEmpty

```dart
bool showWhenEmpty
```

当 [value] 是一个其 [AttributedString.string] 为空字符串的 [AttributedString] 时，是否显示该属性。

此设置会覆盖 [defaultValue]。

### isInteresting

```dart
bool get isInteresting
```

### valueToString()

```dart
String valueToString({TextTreeConfiguration? parentConfiguration})
```

# SemanticsLabelBuilder

```dart
final class SemanticsLabelBuilder {}
```

用于创建具有正确文本方向处理和间距的、语义正确的拼接标签的构建器。

此构建器有助于处理拼接多个文本部分时的复杂性，包括处理特定语言的细微差异，例如从右到左（RTL）与从左到右（LTR）的文本方向，以及正确的间距。

用法示例：

```dart
SemanticsLabelBuilder builder = SemanticsLabelBuilder()
  ..addPart('Hello')
  ..addPart('world');
String label = builder.build(); // "Hello world"
```

对于需要正确 RTL 支持的多语言文本：

```dart
SemanticsLabelBuilder builder = SemanticsLabelBuilder(textDirection: TextDirection.ltr)
  ..addPart('Welcome', textDirection: TextDirection.ltr)
  ..addPart('مرحبا', textDirection: TextDirection.rtl); // Arabic
String label = builder.build(); // "Welcome \u202Bمرحبا\u202C" (with Unicode embedding)
```

### SemanticsLabelBuilder()

```dart
SemanticsLabelBuilder({String separator = ' ', TextDirection? textDirection})
```

创建一个新的 [SemanticsLabelBuilder]。

[separator] 用于文本部分之间（默认为空格）。[textDirection] 指定拼接后标签的整体文本方向。

### separator

```dart
String separator
```

文本部分之间使用的分隔符。

### textDirection

```dart
TextDirection? textDirection
```

拼接后标签的整体文本方向。

### addPart()

```dart
void addPart(String label, {TextDirection? textDirection})
```

添加一个文本部分。

如果指定了 [textDirection]，则该部分将使用此文本方向。空的部分将被忽略。

### isEmpty

```dart
bool get isEmpty
```

如果尚未向此构建器添加任何部分，则返回 true。

### length

```dart
int get length
```

返回已添加到此构建器的部分数量。

### build()

```dart
String build()
```

根据已添加的部分构建并返回拼接后的标签。

此方法会以正确的文本方向处理和间距拼接所有部分。

### clear()

```dart
void clear()
```

清除此构建器中的所有部分，使其可以重新使用。

# SemanticsData

```dart
class SemanticsData with Diagnosticable {}
```

关于 [SemanticsNode] 对象的摘要信息。

某个语义节点可能会 [SemanticsNode.mergeAllDescendantsIntoThisNode]，这意味着该语义节点上的各个字段无法完整描述该节点处的语义。此数据结构包含该节点的完整语义信息。

通常通过 [SemanticsNode.getSemanticsData] 获取。

### SemanticsData()

```dart
SemanticsData({required SemanticsFlags flagsCollection, required int actions, required String identifier, required Object? traversalParentIdentifier, required Object? traversalChildIdentifier, required AttributedString attributedLabel, required AttributedString attributedValue, required AttributedString attributedIncreasedValue, required AttributedString attributedDecreasedValue, required AttributedString attributedHint, required String tooltip, required TextDirection? textDirection, required Rect rect, required TextSelection? textSelection, required int? scrollIndex, required int? scrollChildCount, required double? scrollPosition, required double? scrollExtentMax, required double? scrollExtentMin, required int? platformViewId, required int? maxValueLength, required int? currentValueLength, required int headingLevel, required Uri? linkUrl, required SemanticsRole role, required Set<String>? controlsNodes, required SemanticsValidationResult validationResult, required ui.SemanticsHitTestBehavior hitTestBehavior, required SemanticsInputType inputType, required Locale? locale, required String? minValue, required String? maxValue, Set<SemanticsTag>? tags, Matrix4? transform, List<int>? customSemanticsActionIds})
```

创建一个语义数据对象。

如果 [label] 不为空，则 [textDirection] 也不能为 null。

### flags

```dart
int get flags
```

适用于此节点的 [SemanticsFlag] 位字段。

### flagsCollection

```dart
SemanticsFlags flagsCollection
```

语义标志。

### actions

```dart
int actions
```

适用于此节点的 [SemanticsAction] 位字段。

### identifier

```dart
String identifier
```

{@macro flutter.semantics.SemanticsProperties.identifier}

### traversalParentIdentifier

```dart
Object? traversalParentIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalParentIdentifier}

### traversalChildIdentifier

```dart
Object? traversalChildIdentifier
```

{@macro flutter.semantics.SemanticsProperties.traversalChildIdentifier}

### label

```dart
String get label
```

此节点当前标签的文本描述。

阅读方向由 [textDirection] 给出。

此属性暴露了 [attributedLabel] 的原始文本。

### attributedLabel

```dart
AttributedString attributedLabel
```

以 [AttributedString] 格式表示的此节点当前标签的文本描述。

阅读方向由 [textDirection] 给出。

另请参阅 [label]，它仅暴露原始文本。

### value

```dart
String get value
```

此节点当前值的文本描述。

阅读方向由 [textDirection] 给出。

此属性暴露了 [attributedValue] 的原始文本。

### attributedValue

```dart
AttributedString attributedValue
```

以 [AttributedString] 格式表示的此节点当前值的文本描述。

阅读方向由 [textDirection] 给出。

另请参阅 [value]，它仅暴露原始文本。

### increasedValue

```dart
String get increasedValue
```

执行 [SemanticsAction.increase] 操作后，[value] 将变为的值。

阅读方向由 [textDirection] 给出。

此属性暴露了 [attributedIncreasedValue] 的原始文本。

### attributedIncreasedValue

```dart
AttributedString attributedIncreasedValue
```

以 [AttributedString] 格式表示的、执行 [SemanticsAction.increase] 操作后 [value] 将变为的值。

阅读方向由 [textDirection] 给出。

另请参阅 [increasedValue]，它仅暴露原始文本。

### decreasedValue

```dart
String get decreasedValue
```

执行 [SemanticsAction.decrease] 操作后，[value] 将变为的值。

阅读方向由 [textDirection] 给出。

此属性暴露了 [attributedDecreasedValue] 的原始文本。

### attributedDecreasedValue

```dart
AttributedString attributedDecreasedValue
```

以 [AttributedString] 格式表示的、执行 [SemanticsAction.decrease] 操作后 [value] 将变为的值。

阅读方向由 [textDirection] 给出。

另请参阅 [decreasedValue]，它仅暴露原始文本。

### hint

```dart
String get hint
```

对该节点执行操作后所产生结果的简要文本描述。

阅读方向由 [textDirection] 给出。

此属性暴露了 [attributedHint] 的原始文本。

### attributedHint

```dart
AttributedString attributedHint
```

以 [AttributedString] 格式表示的、对该节点执行操作后所产生结果的简要文本描述。

阅读方向由 [textDirection] 给出。

另请参阅 [hint]，它仅暴露原始文本。

### tooltip

```dart
String tooltip
```

该 Widget 工具提示的文本描述。

阅读方向由 [textDirection] 给出。

### headingLevel

```dart
int headingLevel
```

表示此子树代表一个标题。

值为 0 表示它不是标题。该值应为 1 到 6 之间的数字，表示作为标题的层级。

### textDirection

```dart
TextDirection? textDirection
```

[label]、[value]、[increasedValue]、[decreasedValue] 和 [hint] 中文本的阅读方向。

### textSelection

```dart
TextSelection? textSelection
```

如果此节点表示一个文本字段，则为 [value] 中当前选中的文本（或光标位置）。

### scrollChildCount

```dart
int? scrollChildCount
```

参与语义构建的可滚动子级总数。

如果子级数量未知或无限制，则该值为 null。

### scrollIndex

```dart
int? scrollIndex
```

滚动节点中第一个可见的语义子级的索引。

### scrollPosition

```dart
double? scrollPosition
```

如果该节点可滚动，表示以逻辑像素为单位的当前滚动位置。

属性 [scrollExtentMin] 和 [scrollExtentMax] 表示该属性有效的取值范围。[scrollPosition] 的值可能（暂时）超出该范围，例如在发生过度滚动（overscroll）期间。

另请参阅：

- [ScrollPosition.pixels]，该值通常取自此处。

### scrollExtentMax

```dart
double? scrollExtentMax
```

如果该节点可滚动，表示 [scrollPosition] 的最大有效取值。

如果滚动是无限制的，此值可能为无穷大。

另请参阅：

- [ScrollPosition.maxScrollExtent]，该值通常取自此处。

### scrollExtentMin

```dart
double? scrollExtentMin
```

如果该节点可滚动，表示 [scrollPosition] 的最小有效取值。

如果滚动是无限制的，此值可能为无穷大。

另请参阅：

- [ScrollPosition.minScrollExtent]，该值通常取自此处。

### platformViewId

```dart
int? platformViewId
```

平台视图的 id，其语义节点将作为子节点添加到此节点。

如果该值不为 null，则此 SemanticsNode 不得拥有任何子节点，因为这些子节点将被所引用平台视图的语义节点替换。

另请参阅：

- [AndroidView]，Android 的平台视图。
- [UiKitView]，iOS 的平台视图。

### maxValueLength

```dart
int? maxValueLength
```

可输入到可编辑文本字段中的最大字符数。

就此函数而言，一个字符被定义为一个 Unicode 标量值。

仅当设置了 [SemanticsFlag.isTextField] 时才应设置此项。默认为 null，表示不对文本字段施加任何限制。

### currentValueLength

```dart
int? currentValueLength
```

已输入到可编辑文本字段中的当前字符数。

就此函数而言，一个字符被定义为一个 Unicode 标量值。

仅当设置了 [SemanticsFlag.isTextField] 时才应设置此项。当设置了 [maxValueLength] 时，必须同时设置此项。

### linkUrl

```dart
Uri? linkUrl
```

此节点链接到的 URL。

另请参阅：

- [SemanticsFlag.isLink]，表示此节点是一个链接。

### rect

```dart
Rect rect
```

该节点在其坐标系中的边界框。

### tags

```dart
Set<SemanticsTag>? tags
```

与该节点关联的 [SemanticsTag] 集合。

### transform

```dart
Matrix4? transform
```

从该节点的坐标系到其父节点坐标系的变换。

默认情况下，该变换为 null，表示恒等变换（即此节点与其父节点使用相同的坐标系）。

### customSemanticsActionIds

```dart
List<int>? customSemanticsActionIds
```

该节点的自定义语义操作及标准操作覆盖的标识符。

该列表必须按升序排列。

另请参阅：

- [CustomSemanticsAction]，其中说明了自定义操作。

### role

```dart
SemanticsRole role
```

{@macro flutter.semantics.SemanticsNode.role}

### controlsNodes

```dart
Set<String>? controlsNodes
```

{@macro flutter.semantics.SemanticsNode.controlsNodes}

{@macro flutter.semantics.SemanticsProperties.controlsNodes}

### validationResult

```dart
SemanticsValidationResult validationResult
```

{@macro flutter.semantics.SemanticsProperties.validationResult}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior hitTestBehavior
```

{@macro flutter.semantics.SemanticsProperties.hitTestBehavior}

### inputType

```dart
SemanticsInputType inputType
```

{@macro flutter.semantics.SemanticsNode.inputType}

### locale

```dart
Locale? locale
```

该语义节点的语言区域。

辅助技术使用此属性来正确解读该语义节点的内容。

### maxValue

```dart
String? maxValue
```

{@macro flutter.semantics.SemanticsProperties.maxValue}

### minValue

```dart
String? minValue
```

{@macro flutter.semantics.SemanticsProperties.minValue}

### hasFlag()

```dart
bool hasFlag(SemanticsFlag flag)
```

[flags] 是否包含给定的标志。

### hasAction()

```dart
bool hasAction(SemanticsAction action)
```

[actions] 是否包含给定的操作。

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# SemanticsHintOverrides

```dart
class SemanticsHintOverrides extends DiagnosticableTree {}
```

提供在受支持平台上覆盖默认提示的值。

在 iOS 上，这些值始终会被忽略。

### SemanticsHintOverrides()

```dart
SemanticsHintOverrides({String? onTapHint, String? onLongPressHint})
```

创建一个语义提示覆盖。

### onTapHint

```dart
String? onTapHint
```

点击操作的提示文本。

如果为 null，则使用标准提示。

该提示应描述点击发生后会发生什么，而不是描述点击是通过何种方式完成的。

不好的示例：'Double tap to show movies'（双击以显示电影）。好的示例：'show movies'（显示电影）。

### onLongPressHint

```dart
String? onLongPressHint
```

长按操作的提示文本。

如果为 null，则使用标准提示。

该提示应描述长按发生后会发生什么，而不是描述长按是通过何种方式完成的。

不好的示例：'Double tap and hold to show tooltip'（双击并按住以显示工具提示）。好的示例：'show tooltip'（显示工具提示）。

### isNotEmpty

```dart
bool get isNotEmpty
```

是否存在任何非空的提示值。

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SemanticsProperties

```dart
class SemanticsProperties extends DiagnosticableTree {}
```

包含辅助技术用于使应用程序更易于访问的属性。

此类的属性用于在语义树中生成 [SemanticsNode]。

### SemanticsProperties()

```dart
SemanticsProperties({bool? enabled, bool? checked, bool? mixed, bool? expanded, bool? selected, bool? toggled, bool? button, bool? link, Uri? linkUrl, bool? header, int? headingLevel, bool? textField, bool? slider, bool? keyboardKey, bool? readOnly, bool? focusable, bool? focused, AccessibilityFocusBlockType? accessibilityFocusBlockType, bool? inMutuallyExclusiveGroup, bool? hidden, bool? obscured, bool? multiline, bool? scopesRoute, bool? namesRoute, bool? image, bool? liveRegion, bool? isRequired, int? maxValueLength, int? currentValueLength, String? identifier, Object? traversalParentIdentifier, Object? traversalChildIdentifier, String? label, AttributedString? attributedLabel, String? value, AttributedString? attributedValue, String? increasedValue, AttributedString? attributedIncreasedValue, String? decreasedValue, AttributedString? attributedDecreasedValue, String? hint, String? tooltip, AttributedString? attributedHint, SemanticsHintOverrides? hintOverrides, TextDirection? textDirection, SemanticsSortKey? sortKey, SemanticsTag? tagForChildren, SemanticsRole? role, Set<String>? controlsNodes, SemanticsInputType? inputType, SemanticsValidationResult validationResult = SemanticsValidationResult.none, ui.SemanticsHitTestBehavior? hitTestBehavior, VoidCallback? onTap, VoidCallback? onLongPress, VoidCallback? onScrollLeft, VoidCallback? onScrollRight, VoidCallback? onScrollUp, VoidCallback? onScrollDown, VoidCallback? onIncrease, VoidCallback? onDecrease, VoidCallback? onCopy, VoidCallback? onCut, VoidCallback? onPaste, MoveCursorHandler? onMoveCursorForwardByCharacter, MoveCursorHandler? onMoveCursorBackwardByCharacter, MoveCursorHandler? onMoveCursorForwardByWord, MoveCursorHandler? onMoveCursorBackwardByWord, SetSelectionHandler? onSetSelection, SetTextHandler? onSetText, VoidCallback? onDidGainAccessibilityFocus, VoidCallback? onDidLoseAccessibilityFocus, VoidCallback? onFocus, VoidCallback? onDismiss, VoidCallback? onExpand, VoidCallback? onCollapse, Map<CustomSemanticsAction, VoidCallback>? customSemanticsActions, String? minValue, String? maxValue})
```

创建一个语义注解。

### enabled

```dart
bool? enabled
```

如果不为 null，表示该子树代表可以处于启用或禁用状态的内容。

例如，用户当前可以与之交互的按钮会将此字段设置为 true。当前不响应用户交互的按钮会将此字段设置为 false。

### checked

```dart
bool? checked
```

如果不为 null，表示该子树代表一个具有"选中"状态的复选框或类似 Widget，以及其当前状态。

当三态 Checkbox 的 [Checkbox.value] 为 null（表示混合状态）时，此值应为 false，此时 [mixed] 将为 true。

此属性与 [toggled] 和 [mixed] 互斥。

### mixed

```dart
bool? mixed
```

如果不为 null，表示该子树代表一个具有"半选中"状态或类似状态的复选框或类似 Widget，以及其当前是否处于该半选中状态。

当 [Checkbox.tristate] 为 false，或该 Widget 不是复选框时，此值必须为 null。当三态复选框完全未选中/选中时，此值应为 false。

此属性与 [checked] 和 [toggled] 互斥。

### expanded

```dart
bool? expanded
```

如果不为 null，表示该子树代表可以处于"展开"或"折叠"状态的内容。

例如，如果某个 [SubmenuButton] 被打开，则应将此属性设置为 true；否则应设置为 false。

### toggled

```dart
bool? toggled
```

如果不为 null，表示该子树代表一个具有"开启"状态的切换开关或类似 Widget，以及其当前状态。

此属性与 [checked] 和 [mixed] 互斥。

### selected

```dart
bool? selected
```

如果不为 null，表示该子树代表可以处于选中或未选中状态的内容，以及其当前状态。

例如，标签栏中的活动标签被视为"已选中"，而其他所有标签均为未选中。

### button

```dart
bool? button
```

如果不为 null，表示该子树代表一个按钮。

当按钮获得焦点时，TalkBack/VoiceOver 会为用户提供"button"（按钮）提示。

### link

```dart
bool? link
```

如果不为 null，表示该子树代表一个链接。

当链接获得焦点时，iOS 的 VoiceOver 会为用户提供独特的提示。Android 的 Talkback 播报链接提示的方式与按钮相同。

### header

```dart
bool? header
```

如果不为 null，表示该子树代表一个标题。

标题通常是页面或章节的顶部元素，例如页面标题或应用栏标题。

### textField

```dart
bool? textField
```

如果不为 null，表示该子树代表一个文本字段。

TalkBack/VoiceOver 为在文本字段中输入文本提供了特殊便利。

### slider

```dart
bool? slider
```

如果不为 null，表示该子树代表一个滑块。

当滑块获得焦点时，Talkback/VoiceOver 会为用户提供"slider"（滑块）提示。

### keyboardKey

```dart
bool? keyboardKey
```

如果不为 null，表示该子树代表一个键盘按键。

### readOnly

```dart
bool? readOnly
```

如果不为 null，表示该子树为只读。

仅当 [textField] 为 true 时适用。

TalkBack/VoiceOver 会将其视为不可编辑的文本字段。

### focusable

```dart
bool? focusable
```

如果不为 null，表示该节点是否能够持有输入焦点。

如果 [focusable] 设置为 false，则 [focused] 不得为 true。

输入焦点表示该节点将接收键盘事件。不要将其与无障碍焦点混淆。无障碍焦点是 TalkBack/VoiceOver 在其正在朗读的元素周围绘制的绿色/黑色矩形高亮，与输入焦点是分开的。

### focused

```dart
bool? focused
```

如果不为 null，表示该节点当前是否持有输入焦点。

如果为 null，则该节点不可聚焦。

在任何时刻，树中最多应有一个节点持有输入焦点，并且当 [focusable] 为 false 时不应将其设置为 true。

输入焦点表示该节点将接收键盘事件。不要将其与无障碍焦点混淆。无障碍焦点是 TalkBack/VoiceOver 绘制的绿色/黑色矩形高亮，与输入焦点是分开的。

### accessibilityFocusBlockType

```dart
AccessibilityFocusBlockType? accessibilityFocusBlockType
```

如果不为 null，表示该子树或当前节点在无障碍焦点方面是否被阻止。

这里指的是无障碍焦点，即 TalkBack 和 VoiceOver 等屏幕阅读器所使用的焦点。它不同于输入焦点，输入焦点通常由当前响应键盘输入的元素持有。

### inMutuallyExclusiveGroup

```dart
bool? inMutuallyExclusiveGroup
```

如果不为 null，表示某个语义节点是否处于互斥组中。

例如，单选按钮处于互斥组中，因为该组中只能有一个单选按钮被标记为 [checked]。

### hidden

```dart
bool? hidden
```

如果不为 null，表示该节点是否被视为隐藏。

隐藏元素当前在屏幕上不可见。它们可能被其他元素遮挡，或位于视口的可见区域之外。

隐藏元素无法通过常规触摸获得无障碍焦点。使其获得焦点的唯一方式是通过线性导航将焦点移动到它们上面。

平台可以完全忽略隐藏元素，并鼓励新平台这样做。

通常应将某个元素从语义树中完全排除，而不是将其标记为隐藏。隐藏元素之所以被包含在语义树中，仅仅是为了绕过平台限制，它们主要用于在 iOS 上实现无障碍滚动。

### obscured

```dart
bool? obscured
```

如果不为 null，表示是否应隐藏 [value]。

此选项通常与 [textField] 结合设置，以表示该文本字段包含密码（或其他敏感信息）。这样做会指示屏幕阅读器不要朗读该值。

### multiline

```dart
bool? multiline
```

[value] 是否来自支持多行文本编辑的字段。

此选项仅在 [textField] 为 true 时才有意义，用于表示它是单行还是多行文本字段。

当 [textField] 为 false 时，此选项为 null。

### scopesRoute

```dart
bool? scopesRoute
```

如果不为 null，表示该节点是否对应于应播报路由名称的子树的根节点。

通常，此项会与 [SemanticsConfiguration.explicitChildNodes] 结合设置，因为带有此标志的节点不会被 Android 或 iOS 视为可聚焦。

另请参阅：

- [SemanticsFlag.scopesRoute]，其中描述了如何选择所播报的值。

### namesRoute

```dart
bool? namesRoute
```

如果不为 null，表示该节点是否包含某个路由的语义标签。

另请参阅：

- [SemanticsFlag.namesRoute]，其中描述了该名称的使用方式。

### image

```dart
bool? image
```

如果不为 null，表示该节点是否代表一张图片。

另请参阅：

- [SemanticsFlag.isImage]，此设置所控制的标志。

### liveRegion

```dart
bool? liveRegion
```

如果不为 null，表示该节点是否应被视为实时区域（live region）。

实时区域表示对该语义节点的更新很重要。平台可以利用此信息向用户发出礼貌性播报，以告知其该节点的更新情况。

实时区域的一个例子是 [SnackBar] Widget。在 Android 和 iOS 上，即使该 Widget 没有无障碍焦点，实时区域也会自动触发礼貌性播报。如果操作系统的无障碍服务已经在播报其他内容（例如朗读已获得焦点的 Widget 的标签，或提供系统播报），则该播报可能不会被朗读。

另请参阅：

- [SemanticsFlag.isLiveRegion]，此设置所控制的语义标志。
- [SemanticsConfiguration.liveRegion]，其中对实时区域进行了完整描述。

### isRequired

```dart
bool? isRequired
```

如果不为 null，表示该节点是否应被视为必填项。

如果为 true，则在表单可以提交之前，必须在该语义节点上输入内容。如果为 false，则该节点在表单提交前为可选项。如果为 null，则该节点不具有必填语义。

例如，登录表单要求其电子邮件文本字段不能为空。

在 Web 上，这会在与该语义节点对应的 DOM 元素上设置 `aria-required` 属性。

另请参阅：

- [SemanticsFlag.isRequired]，此设置所控制的标志。

### maxValueLength

```dart
int? maxValueLength
```

可输入到可编辑文本字段中的最大字符数。

就此函数而言，一个字符被定义为一个 Unicode 标量值。

仅当 [textField] 为 true 时才应设置此项。默认为 null，表示不对文本字段施加任何限制。

### currentValueLength

```dart
int? currentValueLength
```

已输入到可编辑文本字段中的当前字符数。

就此函数而言，一个字符被定义为一个 Unicode 标量值。

仅当 [textField] 为 true 时才应设置此项。当设置了 [maxValueLength] 时，必须同时设置此项。

### identifier

```dart
String? identifier
```

{@template flutter.semantics.SemanticsProperties.identifier} 为原生无障碍层级结构中的语义节点提供一个标识符。

该值不会暴露给应用的用户。

它通常用于通过按原生无障碍进行查询的工具（如 UIAutomator、XCUITest 或 Appium）进行 UI 测试。它可以与 [CommonFinders.bySemanticsIdentifier] 匹配。

设置此属性会隐式强制创建一个新的 [SemanticsNode]（等同于在 [Semantics] 中将 `container` 设置为 true）。这确保了该标识符始终附加在其自身的节点上，而不会被合并到祖先节点中。

在 Android 上，此项用于 `AccessibilityNodeInfo.setViewIdResourceName`。它将在无障碍层级结构中以 `resource-id` 的形式出现。

在 iOS 上，这将设置 `UIAccessibilityElement.accessibilityIdentifier`。

在 Web 上，这将在与该语义节点对应的 DOM 元素上设置 `flt-semantics-identifier` 属性。{@endtemplate}

### traversalParentIdentifier

```dart
Object? traversalParentIdentifier
```

{@template flutter.semantics.SemanticsProperties.traversalParentIdentifier} 用于在语义遍历树中建立父子关系的标识符。

此属性用于在可能未在 Widget 树中直接连接的语义节点之间创建逻辑父子关系。它主要与 [OverlayPortal] 一起使用，以确保当浮层内容需要在语义上与其父 Widget 连接时，能有正确的无障碍遍历顺序。

当某个语义节点具有 [traversalParentIdentifier] 时，表示该节点可以作为其他引用了此标识符的节点（通过其 [traversalChildIdentifier]）的父节点。这使得辅助技术能够以正确的逻辑顺序浏览 UI。

`traversalParentIdentifier` 在整个语义结构中必须唯一。任何两个语义节点都不能拥有相同的 `traversalParentIdentifier`。这个唯一标识符是其遍历子节点的唯一引用依据。要将其他节点嫁接为该节点的遍历子节点，需为它们的 `traversalChildIdentifier` 赋予相同的值。{@endtemplate}

### traversalChildIdentifier

```dart
Object? traversalChildIdentifier
```

{@template flutter.semantics.SemanticsProperties.traversalChildIdentifier} 用于在语义遍历树中建立父子关系的标识符。

此属性用于在可能未在 Widget 树中直接连接的语义节点之间创建逻辑父子关系。它主要与 [OverlayPortal] 一起使用，以确保当浮层内容需要在语义上与其父 Widget 连接时，能有正确的无障碍遍历顺序。

当某个语义节点具有 [traversalChildIdentifier] 时，表示该节点应被视为另一个以相同标识符作为其 [traversalParentIdentifier] 的节点的子节点。这使得辅助技术能够以正确的逻辑顺序浏览 UI。

`traversalChildIdentifier` 的值可以在多个语义节点中重复。要将一个或多个节点确立为某个父节点的遍历子节点，需为其赋予与该父节点的 `traversalParentIdentifier` 相同的值。{@endtemplate}

### label

```dart
String? label
```

提供该 Widget 的文本描述。

如果提供了 label，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [label] 和 [attributedLabel]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.label]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [attributedLabel]，此属性的 [AttributedString] 版本。

### attributedLabel

```dart
AttributedString? attributedLabel
```

提供该 Widget 文本描述的 [AttributedString] 版本。

如果提供了 [attributedLabel]，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [label] 和 [attributedLabel]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.attributedLabel]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [label]，此属性的纯字符串版本。

### value

```dart
String? value
```

提供该 Widget 值的文本描述。

如果提供了 value，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [value] 和 [attributedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.value]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [attributedLabel]，此属性的 [AttributedString] 版本。

### attributedValue

```dart
AttributedString? attributedValue
```

提供该 Widget 值的文本描述的 [AttributedString] 版本。

如果提供了 [attributedValue]，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [value] 和 [attributedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.attributedValue]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [value]，此属性的纯字符串版本。

### increasedValue

```dart
String? increasedValue
```

在对该 Widget 执行 [SemanticsAction.increase] 操作后，[value] 或 [attributedValue] 将变为的值。

如果提供了该值，则还必须设置 [onIncrease]，并且必须存在环境 [Directionality]，或必须提供显式的 [textDirection]。

调用者不得同时提供 [increasedValue] 和 [attributedIncreasedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.increasedValue]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [attributedIncreasedValue]，此属性的 [AttributedString] 版本。

### attributedIncreasedValue

```dart
AttributedString? attributedIncreasedValue
```

在对该 Widget 执行 [SemanticsAction.increase] 操作后，[value] 或 [attributedValue] 将变为的 [AttributedString]。

如果提供了 [attributedIncreasedValue]，则还必须设置 [onIncrease]，并且必须存在环境 [Directionality]，或必须提供显式的 [textDirection]。

调用者不得同时提供 [increasedValue] 和 [attributedIncreasedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.attributedIncreasedValue]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [increasedValue]，此属性的纯字符串版本。

### decreasedValue

```dart
String? decreasedValue
```

在对该 Widget 执行 [SemanticsAction.decrease] 操作后，[value] 或 [attributedValue] 将变为的值。

如果提供了该值，则还必须设置 [onDecrease]，并且必须存在环境 [Directionality]，或必须提供显式的 [textDirection]。

调用者不得同时提供 [decreasedValue] 和 [attributedDecreasedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.decreasedValue]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [attributedDecreasedValue]，此属性的 [AttributedString] 版本。

### attributedDecreasedValue

```dart
AttributedString? attributedDecreasedValue
```

在对该 Widget 执行 [SemanticsAction.decrease] 操作后，[value] 或 [attributedValue] 将变为的 [AttributedString]。

如果提供了 [attributedDecreasedValue]，则还必须设置 [onDecrease]，并且必须存在环境 [Directionality]，或必须提供显式的 [textDirection]。

调用者不得同时提供 [decreasedValue] 和 [attributedDecreasedValue]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.attributedDecreasedValue]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [decreasedValue]，此属性的纯字符串版本。

### hint

```dart
String? hint
```

提供对该 Widget 执行操作所产生结果的简要文本描述。

如果提供了 hint，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [hint] 和 [attributedHint]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.hint]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [attributedHint]，此属性的 [AttributedString] 版本。

### attributedHint

```dart
AttributedString? attributedHint
```

提供对该 Widget 执行操作所产生结果的简要文本描述的 [AttributedString] 版本。

如果提供了 [attributedHint]，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

调用者不得同时提供 [hint] 和 [attributedHint]。两者中必须有一个为 null。

另请参阅：

- [SemanticsConfiguration.attributedHint]，描述了它在 TalkBack 和 VoiceOver 中的暴露方式。
- [hint]，此属性的纯字符串版本。

### tooltip

```dart
String? tooltip
```

提供该 Widget 工具提示的文本描述。

在 Android 中，此属性设置 `AccessibilityNodeInfo.setTooltipText`。在 iOS 中，此属性会被追加到 `UIAccessibilityElement.accessibilityLabel` 的末尾。

如果提供了 [tooltip]，则必须存在环境 [Directionality]，或应提供显式的 [textDirection]。

### headingLevel

```dart
int? headingLevel
```

文档结构中的标题层级。

标题将内容划分为多个部分。例如，通讯录应用程序可能定义标题 A、B、C 等，将按字母顺序排列的联系人列表划分为多个部分。

屏幕阅读器使用此值来确定该标题在页面结构中代表哪一部分。1 级标题通常表示页面的主标题，2 级标题表示第一个子章节，3 级标题是该子章节的下一级子章节，以此类推。

在 Web 上，这会设置 `aria-level` 属性（例如 `aria-level="1"`）。在 Android 上，这会设置无障碍的 `isHeading` 属性。

### hintOverrides

```dart
SemanticsHintOverrides? hintOverrides
```

覆盖平台提供的默认无障碍提示。

此 [hintOverrides] 属性不会影响平台处理提示的方式；它仅设置将由辅助技术朗读的自定义文本。

在 Android 上，这些覆盖会替换具有点击或长按操作的语义节点的默认提示。例如，如果提供了 [SemanticsHintOverrides.onTapHint]，屏幕阅读器将不会说"Double tap to activate"（双击以激活），而是会说"Double tap to <onTapHint>"。

在 iOS 上，此属性会被忽略，将采用默认平台行为。

用法示例：

```dart
const Semantics.fromProperties(
 properties: SemanticsProperties(
   hintOverrides: SemanticsHintOverrides(
     onTapHint: 'open settings',
   ),
 ),
 child: Text('button'),
)
```

### textDirection

```dart
TextDirection? textDirection
```

[label]、[value]、[increasedValue]、[decreasedValue] 和 [hint] 的阅读方向。

默认为环境 [Directionality]。

### sortKey

```dart
SemanticsSortKey? sortKey
```

确定该节点在其兄弟节点中的遍历排序位置。

用于描述平台上的无障碍服务（例如 iOS 上的 VoiceOver 和 Android 上的 TalkBack）应以何种顺序遍历该语义节点。

### tagForChildren

```dart
SemanticsTag? tagForChildren
```

应用于该 Widget 的子级 [SemanticsNode] 的标签。

该标签会被添加到所有经过此 Widget 所对应的 RenderObject、并试图附加到父 SemanticsNode 上的子级 [SemanticsNode]。

标签用于向父 SemanticsNode 传达某个子级 SemanticsNode 曾经过某个特定的 RenderObject。父节点可以利用此信息来确定语义树的结构。

另请参阅：

- [SemanticsConfiguration.addTagForChildren]，此处提供的标签将被传递给它。

### linkUrl

```dart
Uri? linkUrl
```

此节点链接到的 URL。

在 Web 上，这用于设置对应 DOM 元素的 `href` 属性。

另请参阅：

- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href

### onTap

```dart
VoidCallback? onTap
```

[SemanticsAction.tap] 的处理器。

这是用户用手指在屏幕上短暂点击而不移动的语义等价物。例如，按钮应当实现此操作。

iOS 上的 VoiceOver 用户和 Android 上的 TalkBack 用户*可能*会在某元素获得焦点时通过双击屏幕来触发此操作。

注意：不同的操作系统或辅助技术可能会对用户输入采取不同的解读方式。有些可能会模拟真实的屏幕点击，而有些可能会调用语义点击。妥善处理点击的一种方式是为手势点击和语义点击都提供相同的处理器。

### onLongPress

```dart
VoidCallback? onLongPress
```

[SemanticsAction.longPress] 的处理器。

这是用户用手指按住屏幕几秒钟而不移动的语义等价物。

iOS 上的 VoiceOver 用户和 Android 上的 TalkBack 用户*可能*会在第二次点击后不抬起手指，通过双击屏幕来触发此操作。

注意：不同的操作系统或辅助技术可能会对用户输入采取不同的解读方式。有些可能会模拟真实的长按，而有些可能会调用语义长按。妥善处理长按的一种方式是为手势长按和语义长按都提供相同的处理器。

### onScrollLeft

```dart
VoidCallback? onScrollLeft
```

[SemanticsAction.scrollLeft] 的处理器。

这是用户手指在屏幕上从右向左移动的语义等价物。它应被水平可滚动的控件识别。

iOS 上的 VoiceOver 用户可以通过三指向左滑动来触发此操作。Android 上的 TalkBack 用户可以通过一个连续动作路径中先向右再向左滑动来触发此操作。在 Android 上，[onScrollUp] 和 [onScrollLeft] 共享相同的手势。因此，只应提供其中之一。

### onScrollRight

```dart
VoidCallback? onScrollRight
```

[SemanticsAction.scrollRight] 的处理器。

这是用户手指在屏幕上从左向右移动的语义等价物。它应被水平可滚动的控件识别。

iOS 上的 VoiceOver 用户可以通过三指向右滑动来触发此操作。Android 上的 TalkBack 用户可以通过一个连续动作路径中先向左再向右滑动来触发此操作。在 Android 上，[onScrollDown] 和 [onScrollRight] 共享相同的手势。因此，只应提供其中之一。

### onScrollUp

```dart
VoidCallback? onScrollUp
```

[SemanticsAction.scrollUp] 的处理器。

这是用户手指在屏幕上从下向上移动的语义等价物。它应被垂直可滚动的控件识别。

iOS 上的 VoiceOver 用户可以通过三指向上滑动来触发此操作。Android 上的 TalkBack 用户可以通过一个连续动作路径中先向右再向左滑动来触发此操作。在 Android 上，[onScrollUp] 和 [onScrollLeft] 共享相同的手势。因此，只应提供其中之一。

### onScrollDown

```dart
VoidCallback? onScrollDown
```

[SemanticsAction.scrollDown] 的处理器。

这是用户手指在屏幕上从上向下移动的语义等价物。它应被垂直可滚动的控件识别。

iOS 上的 VoiceOver 用户可以通过三指向下滑动来触发此操作。Android 上的 TalkBack 用户可以通过一个连续动作路径中先向左再向右滑动来触发此操作。在 Android 上，[onScrollDown] 和 [onScrollRight] 共享相同的手势。因此，只应提供其中之一。

### onIncrease

```dart
VoidCallback? onIncrease
```

[SemanticsAction.increase] 的处理器。

这是一个增大该 Widget 所表示值的请求。例如，滑块控件可能会识别此操作。

如果设置了 [value]，则还必须提供 [increasedValue]，并且 [onIncrease] 必须确保 [value] 将被设置为 [increasedValue]。

iOS 上的 VoiceOver 用户可以通过单指向上滑动来触发此操作。Android 上的 TalkBack 用户可以通过按音量增大键来触发此操作。

### onDecrease

```dart
VoidCallback? onDecrease
```

[SemanticsAction.decrease] 的处理器。

这是一个减小该 Widget 所表示值的请求。例如，滑块控件可能会识别此操作。

如果设置了 [value]，则还必须提供 [decreasedValue]，并且 [onDecrease] 必须确保 [value] 将被设置为 [decreasedValue]。

iOS 上的 VoiceOver 用户可以通过单指向下滑动来触发此操作。Android 上的 TalkBack 用户可以通过按音量减小键来触发此操作。

### onCopy

```dart
VoidCallback? onCopy
```

[SemanticsAction.copy] 的处理器。

这是一个将当前选中内容复制到剪贴板的请求。

例如，Android 上的 TalkBack 用户可以通过文本字段的本地上下文菜单触发此操作。

### onCut

```dart
VoidCallback? onCut
```

[SemanticsAction.cut] 的处理器。

这是一个剪切当前选中内容并将其放入剪贴板的请求。

例如，Android 上的 TalkBack 用户可以通过文本字段的本地上下文菜单触发此操作。

### onPaste

```dart
VoidCallback? onPaste
```

[SemanticsAction.paste] 的处理器。

这是一个粘贴剪贴板当前内容的请求。

例如，Android 上的 TalkBack 用户可以通过文本字段的本地上下文菜单触发此操作。

### onMoveCursorForwardByCharacter

```dart
MoveCursorHandler? onMoveCursorForwardByCharacter
```

[SemanticsAction.moveCursorForwardByCharacter] 的处理器。

当用户希望将文本字段中的光标向前移动一个字符时，会调用此处理器。

当输入焦点位于文本字段中时，TalkBack 用户可以通过按音量增大键来触发此操作。

### onMoveCursorBackwardByCharacter

```dart
MoveCursorHandler? onMoveCursorBackwardByCharacter
```

[SemanticsAction.moveCursorBackwardByCharacter] 的处理器。

当用户希望将文本字段中的光标向后移动一个字符时，会调用此处理器。

当输入焦点位于文本字段中时，TalkBack 用户可以通过按音量减小键来触发此操作。

### onMoveCursorForwardByWord

```dart
MoveCursorHandler? onMoveCursorForwardByWord
```

[SemanticsAction.moveCursorForwardByWord] 的处理器。

当用户希望将文本字段中的光标向后移动一个单词时，会调用此处理器。

TalkBack 用户可以通过按音量减小键来触发此操作。

### onMoveCursorBackwardByWord

```dart
MoveCursorHandler? onMoveCursorBackwardByWord
```

[SemanticsAction.moveCursorBackwardByWord] 的处理器。

当用户希望将文本字段中的光标向后移动一个单词时，会调用此处理器。

TalkBack 用户可以通过按音量减小键来触发此操作。

### onSetSelection

```dart
SetSelectionHandler? onSetSelection
```

[SemanticsAction.setSelection] 的处理器。

当用户希望更改文本字段中当前选中的文本，或更改光标位置时，会调用此处理器。

TalkBack 用户可以通过在本地上下文菜单中选择"移动光标到开头/结尾"或"全选"来触发此处理器。

### onSetText

```dart
SetTextHandler? onSetText
```

[SemanticsAction.setText] 的处理器。

当用户希望用新文本替换文本字段中的当前文本时，会调用此处理器。

语音辅助（Voice access）用户可以通过对 Android 设备说出 `type <text>` 来触发此处理器。

### onDidGainAccessibilityFocus

```dart
VoidCallback? onDidGainAccessibilityFocus
```

[SemanticsAction.didGainAccessibilityFocus] 的处理器。

当带有此处理器注解的节点获得无障碍焦点时，会调用此处理器。无障碍焦点是屏幕上显示的绿色（Android 上的 TalkBack）或黑色（iOS 上的 VoiceOver）矩形，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点不同于输入焦点。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

另请参阅：

- [onDidLoseAccessibilityFocus]，当无障碍焦点从该节点移除时会被调用。
- [onFocus]，当辅助技术请求某个 Widget 获得输入焦点时会被调用。
- [FocusNode]、[FocusScope]、[FocusManager]，用于管理输入焦点。

### onDidLoseAccessibilityFocus

```dart
VoidCallback? onDidLoseAccessibilityFocus
```

[SemanticsAction.didLoseAccessibilityFocus] 的处理器。

当带有此处理器注解的节点失去无障碍焦点时，会调用此处理器。无障碍焦点是屏幕上显示的绿色（Android 上的 TalkBack）或黑色（iOS 上的 VoiceOver）矩形，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点不同于输入焦点。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

另请参阅：

- [onDidGainAccessibilityFocus]，当节点获得无障碍焦点时会被调用。
- [FocusNode]、[FocusScope]、[FocusManager]，用于管理输入焦点。

### onFocus

```dart
VoidCallback? onFocus
```

{@template flutter.semantics.SemanticsProperties.onFocus} [SemanticsAction.focus] 的处理器。

当辅助技术请求与该语义节点对应的可聚焦 Widget 获得输入焦点时，会调用此处理器。管理该 Widget 焦点的 [FocusNode] 必须获得焦点。该 Widget 必须开始响应相关的按键事件。例如：

- 按钮必须响应通过键盘快捷键产生的点击/单击事件。
- 文本字段必须获得焦点并变为可编辑，如有必要，还应显示屏幕键盘。
- 复选框、开关和单选按钮必须能够通过键盘快捷键进行切换。

焦点行为因平台和所使用的辅助技术而异。有关更多详细信息，请参阅 [SemanticsAction.focus] 的文档。

另请参阅：

- [onDidGainAccessibilityFocus]，当节点获得无障碍焦点时会被调用。{@endtemplate}

### onDismiss

```dart
VoidCallback? onDismiss
```

[SemanticsAction.dismiss] 的处理器。

这是一个关闭当前获得焦点节点的请求。

Android 上的 TalkBack 用户可以在本地上下文菜单中触发此操作，iOS 上的 VoiceOver 用户可以通过标准手势或菜单选项触发此操作。

### onExpand

```dart
VoidCallback? onExpand
```

[SemanticsAction.expand] 的处理器。

这是一个展开当前获得焦点节点的请求。例如，下拉菜单可能会识别此操作。

仅当该节点处于折叠状态（即 [expanded] 为 false）时，才应设置此处理器。

### onCollapse

```dart
VoidCallback? onCollapse
```

[SemanticsAction.collapse] 的处理器。

这是一个折叠当前获得焦点节点的请求。例如，下拉菜单可能会识别此操作。

仅当该节点处于展开状态（即 [expanded] 为 true）时，才应设置此处理器。

### customSemanticsActions

```dart
Map<CustomSemanticsAction, VoidCallback>? customSemanticsActions
```

从每个受支持的 [CustomSemanticsAction] 到所提供处理器的映射。

每当收到类型为 [SemanticsAction.customAction] 的语义操作时，就会调用与每个自定义操作关联的处理器。所提供的参数将是一个标识符，用于从该映射中检索自定义操作实例，然后再从该实例中获取正确的处理器。

另请参阅：

- [CustomSemanticsAction]，其中说明了自定义操作。

### role

```dart
SemanticsRole? role
```

{@template flutter.semantics.SemanticsProperties.role} 用于描述该子树所代表角色的枚举。

为 Widget 子树设置角色有助于辅助技术（例如屏幕阅读器）正确理解并与 UI 交互。

如果未设置，则默认为 [SemanticsRole.none]，表示该子树不代表任何复杂的 UI 或控件。

有关可用角色的列表，请参阅 [SemanticsRole]。{@endtemplate}

### controlsNodes

```dart
Set<String>? controlsNodes
```

该子树所控制的 Widget 的 [SemanticsNode.identifier]。

{@template flutter.semantics.SemanticsProperties.controlsNodes} 如果某个 Widget 正在控制另一个 Widget 的可见性或内容——例如 [Tab] 控制 [TabBarView] 子级的可见性，或 [ExpansionTile] 控制其展开内容的可见性——则必须为该内容分配一个 [SemanticsNode.identifier]，并向该属性提供一组标识符，其中包括该内容的标识符。{@endtemplate}

### validationResult

```dart
SemanticsValidationResult validationResult
```

{@template flutter.semantics.SemanticsProperties.validationResult} 描述该 Widget 所代表表单字段的验证结果。

提供验证结果有助于辅助技术（例如屏幕阅读器）向用户传达其在表单中提供的信息是否正确。

如果未设置，则默认为 [SemanticsValidationResult.none]，表示该语义节点没有可用的验证信息。

有关可用验证结果的列表，请参阅 [SemanticsValidationResult]。{@endtemplate}

### hitTestBehavior

```dart
ui.SemanticsHitTestBehavior? hitTestBehavior
```

{@template flutter.semantics.SemanticsProperties.hitTestBehavior} 描述该语义节点在命中测试期间应如何表现。

有关更多详细信息，请参阅 [ui.SemanticsHitTestBehavior]。{@endtemplate}

### inputType

```dart
SemanticsInputType? inputType
```

{@template flutter.semantics.SemanticsProperties.inputType} 可编辑 Widget 的输入类型。

此属性仅在该子树代表文本字段时使用。

辅助技术使用此属性为用户提供更好的信息。例如，屏幕阅读器在文本字段获得焦点时会朗读其输入类型。{@endtemplate}

### maxValue

```dart
String? maxValue
```

{@template flutter.semantics.SemanticsProperties.maxValue} 该节点的最大值。

与 [value] 结合使用以定义节点的当前值和范围。典型用法是进度指示器，其中 [value] 表示当前进度，[maxValue] 定义最大可能值。

{@endtemplate}

### minValue

```dart
String? minValue
```

{@template flutter.semantics.SemanticsProperties.minValue} 该节点的最小值。

与 [value] 结合使用以定义节点的当前值和范围。典型用法是进度指示器，其中 [value] 表示当前进度，[minValue] 定义最小可能值。

{@endtemplate}

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toStringShort()

```dart
String toStringShort()
```

# debugResetSemanticsIdCounter()

```dart
void debugResetSemanticsIdCounter()
```

在测试中使用此函数重置用于生成 [SemanticsNode.id] 的计数器。
