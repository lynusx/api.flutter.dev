# SemanticsAction

```dart
class SemanticsAction {}
```

可从操作系统无障碍 API 传递给语义节点的可能操作。

### index

```dart
int index
```

此操作的数值。

每个操作在此位域中设置一位。

### name

```dart
String name
```

此标志的可读名称，用于调试目的。

### tap

```dart
SemanticsAction tap
```

用户在屏幕上短暂点击且不移动手指的等效操作。

### longPress

```dart
SemanticsAction longPress
```

用户按住屏幕几秒钟且不移动手指的等效操作。

### scrollLeft

```dart
SemanticsAction scrollLeft
```

用户手指在屏幕上从右向左滑动的等效操作。

此操作应由可水平滚动的控件识别。

### scrollRight

```dart
SemanticsAction scrollRight
```

用户手指在屏幕上从左向右滑动的等效操作。

此操作应由可水平滚动的控件识别。

### scrollUp

```dart
SemanticsAction scrollUp
```

用户手指在屏幕上从下向上滑动的等效操作。

此操作应由可垂直滚动的控件识别。

### scrollDown

```dart
SemanticsAction scrollDown
```

用户手指在屏幕上从上向下滑动的等效操作。

此操作应由可垂直滚动的控件识别。

### scrollToOffset

```dart
SemanticsAction scrollToOffset
```

请求将可滚动容器滚动到给定的滚动偏移量。

此 [SemanticsAction](https://www.yuque.com/thyname/dart.ui/semanticsaction) 的负载是一个 flutter 标准编码的 [Float64List](https://www.yuque.com/thyname/dart.typed_data/float64list)，长度为 2，包含接收该操作的可滚动容器应滚动到的目标水平和垂直偏移量（以逻辑像素为单位）。

此操作用于 iOS 完全键盘访问功能，以显示当前在视口中不可见的内容。

### increase

```dart
SemanticsAction increase
```

请求增加语义节点所表示的值。

例如，滑块控件可能会识别此操作。

### decrease

```dart
SemanticsAction decrease
```

请求减少语义节点所表示的值。

例如，滑块控件可能会识别此操作。

### showOnScreen

```dart
SemanticsAction showOnScreen
```

请求在屏幕上完全显示该语义节点。

例如，此操作可能会发送给可滚动列表中部分不可见的节点，以将其显示在屏幕上。

### moveCursorForwardByCharacter

```dart
SemanticsAction moveCursorForwardByCharacter
```

将光标向前移动一个字符。

例如用于文本字段中的光标控制。

此操作包含一个布尔参数，指示光标移动是否应扩展（或开始）一个选区。

### moveCursorBackwardByCharacter

```dart
SemanticsAction moveCursorBackwardByCharacter
```

将光标向后移动一个字符。

例如用于文本字段中的光标控制。

此操作包含一个布尔参数，指示光标移动是否应扩展（或开始）一个选区。

### setText

```dart
SemanticsAction setText
```

替换文本字段中的当前文本。

例如用于语音访问中的文本编辑。

此操作包含一个字符串参数，即用于替换的新文本。

### setSelection

```dart
SemanticsAction setSelection
```

将文本选区设置为给定范围。

提供的参数是一个 Map<String, int>，包含键 `base` 和 `extent`，指示语义节点 `value` 中选区的起止位置。这两个键的值范围可以是 0 到 `value` 的长度（含）。

如果将 `base` 和 `extent` 设置为相同的值，会将光标移动到该位置（不选中任何内容）。

### copy

```dart
SemanticsAction copy
```

将当前选区复制到剪贴板。

### cut

```dart
SemanticsAction cut
```

剪切当前选区并放入剪贴板。

### paste

```dart
SemanticsAction paste
```

粘贴剪贴板中的当前内容。

### didGainAccessibilityFocus

```dart
SemanticsAction didGainAccessibilityFocus
```

指示该节点已获得无障碍焦点。

当标注此处理程序的节点获得无障碍焦点时，会调用此处理程序。无障碍焦点是屏幕上显示的绿色（Android 上的 TalkBack）或黑色（iOS 上的 VoiceOver）矩形框，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点不同于输入焦点。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

另请参阅：

- [focus]，用于控制输入焦点。

### didLoseAccessibilityFocus

```dart
SemanticsAction didLoseAccessibilityFocus
```

指示该节点已失去无障碍焦点。

当标注此处理程序的节点失去无障碍焦点时，会调用此处理程序。无障碍焦点是屏幕上显示的绿色（Android 上的 TalkBack）或黑色（iOS 上的 VoiceOver）矩形框，用于指示无障碍用户当前正在与哪个元素交互。

无障碍焦点不同于输入焦点。输入焦点通常由当前响应键盘输入的元素持有。无障碍焦点和输入焦点可以由两个不同的节点持有！

### customAction

```dart
SemanticsAction customAction
```

指示用户已调用自定义无障碍操作。

每当向语义节点添加自定义无障碍操作时，都会自动添加此处理程序。

### dismiss

```dart
SemanticsAction dismiss
```

请求应关闭该节点。

例如，[SnackBar](https://www.yuque.com/thyname/flutter.material/snackbar) 可能具有关闭操作，用于向用户表明该消息在不再相关后可以被移除。在 Android 上（使用 TalkBack），聚焦该节点时会朗读特殊提示文本，且本地上下文菜单中会提供自定义操作。在 iOS 上（使用 VoiceOver），用户可以执行标准手势将其关闭。

### moveCursorForwardByWord

```dart
SemanticsAction moveCursorForwardByWord
```

将光标向前移动一个单词。

例如用于文本字段中的光标控制。

此操作包含一个布尔参数，指示光标移动是否应扩展（或开始）一个选区。

### moveCursorBackwardByWord

```dart
SemanticsAction moveCursorBackwardByWord
```

将光标向后移动一个单词。

例如用于文本字段中的光标控制。

此操作包含一个布尔参数，指示光标移动是否应扩展（或开始）一个选区。

### focus

```dart
SemanticsAction focus
```

将输入焦点移动到相应的 Widget。

最常见的情况是，输入焦点决定哪个 Widget 将接收键盘输入。可以接收此操作的语义节点应设置了 [SemanticsFlag.isFocusable]。此类可聚焦 Widget 的示例包括按钮、复选框、开关和文本字段。

收到此操作后，相应的 Widget 必须将输入焦点移动到自身。否则可能导致糟糕的用户体验，例如用户输入被路由到错误的 Widget。特别是文本字段，必须在需要时立即变为可编辑状态并打开虚拟键盘。按钮必须响应来自键盘的点击/单击事件。

Widget 对此操作的响应必须是幂等的。可能会多次收到此操作，或者在 Widget 已经获得焦点时收到此操作。

焦点行为特定于平台和所使用的辅助技术。通常在桌面操作系统（如 Windows、macOS 和 Linux）上，移动无障碍焦点也会移动输入焦点。而在移动设备上，无障碍焦点与输入焦点分离更为常见。为了使两者同步，用户需要采取显式操作（例如双击以激活）。有时此行为是可配置的。例如，macOS 上的 VoiceOver 可以在全局操作系统用户设置中配置为将输入焦点与 VoiceOver 焦点一起移动，或使两者保持分离。因此，Widget 不应期望以任何特定的组合或顺序收到 [didGainAccessibilityFocus] 和 [focus] 操作的报告。

在 Web 上，DOM 的 "focus" 事件等效于 [SemanticsAction.focus]。无障碍焦点在浏览器内无法被观察到。相反，浏览器会根据平台特性和用户偏好来判断是否应将输入焦点移动到某个元素，如果是，则触发 DOM 的 "focus" 事件。此事件会作为 [SemanticsAction.focus] 转发给框架。因此，在 Web 上，引擎永远不会发送 [didGainAccessibilityFocus]。

在 Android 上，输入焦点可通过 `AccessibilityAction#ACTION_FOCUS` 观察到，与通过 `AccessibilityAction#ACTION_ACCESSIBILITY_FOCUS` 观察到的无障碍焦点是分开的。

另请参阅：

- [didGainAccessibilityFocus]，用于通知框架关于无障碍焦点环（如 Android 上的 TalkBack 和 iOS 上的 VoiceOver）的移动，此移动不会移动输入焦点。

### expand

```dart
SemanticsAction expand
```

请求应展开该节点。

例如，此操作可能会被下拉菜单识别。

### collapse

```dart
SemanticsAction collapse
```

请求应折叠该节点。

例如，此操作可能会被下拉菜单识别。

### values

```dart
List<SemanticsAction> get values
```

### fromIndex()

```dart
SemanticsAction? fromIndex(int index)
```

### toString()

```dart
String toString()
```

# SemanticsRole

```dart
enum SemanticsRole {}
```

用于描述语义节点角色的枚举。

这些角色会被转换为每个平台上对应的原生无障碍角色。

不代表任何角色。

标签按钮。

另请参阅：

- [tabBar]，即标签按钮容器的角色。

包含标签按钮。

另请参阅：

- [tab]，即标签按钮的角色。

标签的主显示区域。

弹出对话框。

警告对话框。

以行列形式排列数据的表格结构。

另请参阅：

- 表格相关角色 [cell]、[row]、[columnHeader]。

[table] 中不包含列或行标题信息的单元格。

另请参阅：

- 表格相关角色 [table]、[row]、[columnHeader]。

[table] 中一行 [cell] 或 [columnHeader]。

另请参阅：

- 表格相关角色 [table]、[cell]、[columnHeader]。

[table] 中包含列标题信息的单元格。

另请参阅：

- 表格相关角色 [table]、[cell]、[row]。

用于在内容间拖动的控件。

例如，[ReorderableList](https://www.yuque.com/thyname/flutter.widgets/reorderablelist) 的拖动手柄。

点击时用于循环切换内容的控件。

例如，[CalendarDatePicker](https://www.yuque.com/thyname/flutter.material/calendardatepicker) 的上一月/下一月按钮。

带有下拉列表框的输入字段。

例如，[DropdownMenu](https://www.yuque.com/thyname/flutter.material/dropdownmenu)。

[menu] 的一种呈现方式，通常始终可见，且通常水平排列显示。

例如，[MenuBar](https://www.yuque.com/thyname/flutter.material/menubar)。

一个始终可见的控件列表，或可打开和关闭的 Widget。

例如，[MenuAnchor](https://www.yuque.com/thyname/flutter.material/menuanchor) 或 [DropdownButton](https://www.yuque.com/thyname/flutter.material/dropdownbutton)。

由 [menu] 或 [menuBar] 创建的下拉菜单中的项。

另请参阅：

- [menuItemCheckbox]，带复选框的菜单项。[menuItemCheckbox] 也可用于 [menu] 和 [menuBar]。
- [menuItemRadio]，带单选按钮的菜单项。此角色也被 [menu] 或 [menuBar] 使用。

由 [menu] 或 [menuBar] 创建的下拉菜单中带复选框的项。

另请参阅：

- 菜单相关角色 [menuItem] 和 [menuItemRadio]。

由 [menu] 或 [menuBar] 创建的下拉菜单中带单选按钮的项。

另请参阅：

- 菜单相关角色 [menuItem] 和 [menuItemCheckbox]。

以垂直或水平布局显示多个 [listItem] 的容器。

例如，[LisView] 或 [Column](https://www.yuque.com/thyname/flutter.widgets/column)。

[list] 中的项。

表示表单的区域。

悬停在组件上时显示的弹出窗口，用于提供上下文说明。

旋转以指示应用程序正忙的图形对象。

例如，[CircularProgressIndicator](https://www.yuque.com/thyname/flutter.material/circularprogressindicator)。

显示带数字进度的图形对象。

例如，[LinearProgressIndicator](https://www.yuque.com/thyname/flutter.material/linearprogressindicator)。

允许用户输入按键组合或序列的键盘快捷键字段。

例如，[Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts)。

一组单选按钮。

用于提供不足以构成 [alert] 的建议性信息的组件。

例如，网页的加载消息。

用于提供重要且通常具有时效性信息的组件。

alert 角色仅应用于需要用户立即关注的信息，例如：

- 表单字段中输入了无效值。
- 用户的登录会话即将过期。
- 与服务器的连接已丢失，本地更改将不会被保存。

与主要内容相关的辅助部分。

complementary 角色是地标角色之一。此角色可用于描述侧边栏或提示框。

更多信息，请参阅：https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/complementary_role

页脚部分，包含版权信息、导航链接和隐私声明等标识信息。

contentInfo 角色是地标角色之一。更多信息，请参阅：https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/contentinfo_role

文档的主要内容。

该部分包含与文档中心主题直接相关或对其进行扩展的内容，或应用程序的主要功能。

此角色是地标角色之一。更多信息，请参阅：https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/main_role

包含导航链接的网页区域。

此角色是地标角色之一。更多信息，请参阅：https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/navigation_role

足够重要但无法用其他地标角色（如 main、contentinfo、complementary 或 navigation）描述的内容部分。

更多信息，请参阅：https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/region_role

# SemanticsInputType

```dart
enum SemanticsInputType {}
```

描述输入字段的数据类型。

通常用于补充文本字段。

非文本字段的默认值。

描述通用文本字段。

描述 URL 文本字段。

描述用于电话输入的文本字段。

描述作为搜索框的文本字段。

描述用于电子邮件输入的文本字段。

# SemanticsFlag

```dart
class SemanticsFlag {}
```

可与语义节点关联的布尔值。

### index

```dart
int index
```

此标志的数值。

每个标志在此位域中设置一位。

### name

```dart
String name
```

此标志的可读名称，用于调试目的。

### hasCheckedState

```dart
SemanticsFlag hasCheckedState
```

{@template dart.ui.semantics.hasCheckedState} 该语义节点具有 "checked"（已选中）或 "unchecked"（未选中）的属性。

此标志与 [hasToggledState] 互斥。

例如，复选框或单选按钮 Widget 具有选中状态。

另请参阅：

- [SemanticsFlag.isChecked]，用于控制节点是 "已选中" 还是 "未选中"。{@endtemplate}

### isChecked

```dart
SemanticsFlag isChecked
```

{@template dart.ui.semantics.isChecked} 具有 [hasCheckedState] 的语义节点是否已选中。

如果为 true，语义节点为 "已选中"。如果为 false，语义节点为 "未选中"。

例如，如果复选框显示可见的对勾，则 [isChecked] 为 true。

另请参阅：

- [SemanticsFlag.hasCheckedState]，用于启用选中状态。{@endtemplate}

### isCheckStateMixed

```dart
SemanticsFlag isCheckStateMixed
```

{@template dart.ui.semantics.isCheckStateMixed} 三态复选框是否处于混合状态。

如果为 true，则此语义节点所代表的复选框处于混合状态。

例如，[Checkbox.tristate] 设置为 true 的 [Checkbox](https://www.yuque.com/thyname/flutter.material/checkbox) 可以具有已选中、未选中或混合状态。

当复选框处于已选中或未选中状态时，此值必须为 false。{@endtemplate}

### hasSelectedState

```dart
SemanticsFlag hasSelectedState
```

{@template dart.ui.semantics.hasSelectedState} 该语义节点具有 "selected"（已选中）或 "unselected"（未选中）的属性。

此节点对应的 Widget 当前是否被选中由 [isSelected] 标志决定。

当未设置此标志时，用户无法选择对应的 Widget，[isSelected] 的存在与否也没有任何意义。{@endtemplate}

### isSelected

```dart
SemanticsFlag isSelected
```

{@template dart.ui.semantics.isSelected} 语义节点是否被选中。

此标志仅在设置了 [hasSelectedState] 标志的节点中有意义。

如果为 true，语义节点为 "已选中"。如果为 false，语义节点为 "未选中"。

例如，标签栏中的活动标签的 [isSelected] 被设置为 true。{@endtemplate}

### isButton

```dart
SemanticsFlag isButton
```

{@template dart.ui.semantics.isButton} 该语义节点是否表示一个按钮。

各平台对按钮有特殊处理，例如 Android 的 TalkBack 和 iOS 的 VoiceOver 在聚焦对象是按钮时会提供额外的提示。{@endtemplate}

### isTextField

```dart
SemanticsFlag isTextField
```

{@template dart.ui.semantics.isTextField} 该语义节点是否表示一个文本字段。

文本字段会以此身份被朗读，并允许通过无障碍功能进行文本输入。{@endtemplate}

### isSlider

```dart
SemanticsFlag isSlider
```

{@template dart.ui.semantics.isSlider} 该语义节点是否表示一个滑块。{@endtemplate}

### isKeyboardKey

```dart
SemanticsFlag isKeyboardKey
```

{@template dart.ui.semantics.isKeyboardKey} 该语义节点是否表示一个键盘按键。{@endtemplate}

### isReadOnly

```dart
SemanticsFlag isReadOnly
```

{@template dart.ui.semantics.isReadOnly} 该语义节点是否为只读。

仅当 [isTextField] 为 true 时适用。{@endtemplate}

### isLink

```dart
SemanticsFlag isLink
```

{@template dart.ui.semantics.isLink} 该语义节点是否为可交互链接。

各平台对链接有特殊处理，例如 iOS 的 VoiceOver 在聚焦对象是链接时会提供额外的提示，以及通过另一个导航菜单解析链接的能力。{@endtemplate}

### isFocusable

```dart
SemanticsFlag isFocusable
```

{@template dart.ui.semantics.isFocusable} 该语义节点是否能够获得用户的焦点。

获得焦点的元素通常是当前键盘输入的接收者。{@endtemplate}

### isFocused

```dart
SemanticsFlag isFocused
```

{@template dart.ui.semantics.isFocused} 该语义节点当前是否持有用户的焦点。

获得焦点的元素通常是当前键盘输入的接收者。{@endtemplate}

### hasEnabledState

```dart
SemanticsFlag hasEnabledState
```

{@template dart.ui.semantics.hasEnabledState} 该语义节点具有 "enabled"（启用）或 "disabled"（禁用）的属性。

例如，按钮可以启用或禁用，因此具有 "启用" 状态。静态文本通常既不启用也不禁用，因此没有 "启用" 状态。{@endtemplate}

### isEnabled

```dart
SemanticsFlag isEnabled
```

{@template dart.ui.semantics.isEnabled} 具有 [hasEnabledState] 的语义节点当前是否启用。

禁用的元素不响应用户交互。例如，当前不响应用户交互的按钮应标记为禁用。{@endtemplate}

### isInMutuallyExclusiveGroup

```dart
SemanticsFlag isInMutuallyExclusiveGroup
```

{@template dart.ui.semantics.isInMutuallyExclusiveGroup} 语义节点是否处于互斥组中。

例如，单选按钮处于互斥组中，因为该组中只能有一个单选按钮被标记为 [isChecked]。{@endtemplate}

### isHeader

```dart
SemanticsFlag isHeader
```

{@template dart.ui.semantics.isHeader} 语义节点是否是将内容划分为若干部分的标题。

例如，标题可用于将按字母顺序排列的单词列表划分为 A、B、C 等部分，这在许多通讯录应用程序中可以见到。{@endtemplate}

### isObscured

```dart
SemanticsFlag isObscured
```

{@template dart.ui.semantics.isObscured} 语义节点的值是否被遮蔽。

这通常用于文本字段，以指示其内容为密码或包含其他敏感信息。{@endtemplate}

### isMultiline

```dart
SemanticsFlag isMultiline
```

{@template dart.ui.semantics.isMultiline} 语义节点的值是否来自多行文本字段。

用于文本字段区分单行文本字段和多行文本字段。{@endtemplate}

### scopesRoute

```dart
SemanticsFlag scopesRoute
```

{@template dart.ui.semantics.scopesRoute} 该语义节点是否为应播报路由名称的子树的根节点。

当带有此标志的节点从语义树中移除时，框架将按深度优先绘制顺序选择最后一个带有此标志的节点。当带有此标志的节点被添加到语义树中时，除非同时添加了多个带有此标志的节点，否则会自动选中该节点。在这种情况下，将选中按深度优先绘制顺序最后添加的节点。

从此被选中的节点开始，框架将按深度优先绘制顺序搜索第一个具有 [namesRoute] 标志且标签非空的节点。[namesRoute] 和 [scopesRoute] 标志可以在同一个节点上。找到的节点的标签将作为边缘过渡进行播报。如果未找到非空标签，则：

- VoiceOver 将发出提示音。
- TalkBack 不会进行任何播报。

带有此标志的语义节点通常不可通过无障碍功能获得焦点。

这用于路由、抽屉和对话框等 Widget，以传达可见屏幕中的重大变化。{@endtemplate}

### namesRoute

```dart
SemanticsFlag namesRoute
```

{@template dart.ui.semantics.namesRoute} 语义节点标签是否为在视觉上独立的路由的名称。

这用于抽屉和对话框等特定 Widget，表示该节点的语义标签可用于播报边缘触发的语义更新。

带有此标志的语义节点仍会获得无障碍焦点。

在同一活动路由子树内更新此标签不会导致额外的播报。{@endtemplate}

### isHidden

```dart
SemanticsFlag isHidden
```

{@template dart.ui.semantics.isHidden} 该语义节点是否被视为隐藏。

隐藏的元素当前在屏幕上不可见。它们可能被其他元素遮挡，或位于视口可见区域之外。

隐藏的元素无法通过常规触摸获得无障碍焦点。使其获得焦点的唯一方法是通过线性导航将焦点移至该元素。

平台可以自由地完全忽略隐藏的元素，并鼓励新平台这样做。

通常应将元素从语义树中完全排除，而不是将其标记为隐藏。隐藏的元素仅在语义树中被保留，以规避平台限制，主要用于在 iOS 上实现无障碍滚动。

另请参阅：

- [RenderObject.describeSemanticsClip]{@endtemplate}

### isImage

```dart
SemanticsFlag isImage
```

{@template dart.ui.semantics.isImage} 该语义节点是否表示一张图片。

TalkBack 和 VoiceOver 都会告知用户该语义节点表示一张图片。{@endtemplate}

### isLiveRegion

```dart
SemanticsFlag isLiveRegion
```

{@template dart.ui.semantics.isLiveRegion} 该语义节点是否为实时区域。

实时区域表示对该语义节点的更新很重要。平台可以利用此信息，通过礼貌性播报向用户告知此节点的更新。

实时区域的一个示例是 [SnackBar](https://www.yuque.com/thyname/flutter.material/snackbar) Widget。在 Android 和 iOS 上，即使该 Widget 未获得无障碍焦点，实时区域也会自动触发礼貌性播报。如果操作系统的无障碍服务已在播报其他内容（例如朗读已聚焦 Widget 的标签或提供系统播报），则可能不会朗读此播报。{@endtemplate}

### hasToggledState

```dart
SemanticsFlag hasToggledState
```

{@template dart.ui.semantics.hasToggledState} 该语义节点具有 "on"（开）或 "off"（关）的属性。

此标志与 [hasCheckedState] 互斥。

例如，开关具有切换状态。

另请参阅：

- [SemanticsFlag.isToggled]，用于控制节点是 "开" 还是 "关"。{@endtemplate}

### isToggled

```dart
SemanticsFlag isToggled
```

{@template dart.ui.semantics.isToggled} 如果为 true，语义节点为 "开"。如果为 false，语义节点为 "关"。

例如，如果开关处于开启位置，[isToggled] 为 true。

另请参阅：

- [SemanticsFlag.hasToggledState]，用于启用切换状态。{@endtemplate}

### hasImplicitScrolling

```dart
SemanticsFlag hasImplicitScrolling
```

{@template dart.ui.semantics.hasImplicitScrolling} 当用户尝试将焦点移动到屏幕外的子项时，平台是否可以滚动该语义节点。

例如，[ListView](https://www.yuque.com/thyname/flutter.widgets/listview) Widget 具有隐式滚动功能，以便用户可以轻松地将无障碍焦点移动到下一组子项。[PageView](https://www.yuque.com/thyname/flutter.widgets/pageview) Widget 没有隐式滚动，因此用户在到达当前页面末尾时不会导航到下一页。{@endtemplate}

### hasExpandedState

```dart
SemanticsFlag hasExpandedState
```

{@template dart.ui.semantics.hasExpandedState} 该语义节点具有 "expanded"（已展开）或 "collapsed"（已折叠）的属性。

例如，[SubmenuButton](https://www.yuque.com/thyname/flutter.material/submenubutton) Widget 具有展开状态。

另请参阅：

- [SemanticsFlag.isExpanded]，用于控制节点是 "已展开" 还是 "已折叠"。{@endtemplate}

### isExpanded

```dart
SemanticsFlag isExpanded
```

{@template dart.ui.semantics.isExpanded} 语义节点是否已展开。

如果为 true，语义节点为 "已展开"。如果为 false，语义节点为 "已折叠"。

例如，如果 [SubmenuButton](https://www.yuque.com/thyname/flutter.material/submenubutton) 显示其子项，则 [isExpanded] 为 true。

另请参阅：

- [SemanticsFlag.hasExpandedState]，用于启用展开/折叠状态。{@endtemplate}

### hasRequiredState

```dart
SemanticsFlag hasRequiredState
```

{@template dart.ui.semantics.hasRequiredState} 该语义节点具有是否为必需的属性。

另请参阅：

- [SemanticsFlag.isRequired]，用于控制节点是否为必需。{@endtemplate}

### isRequired

```dart
SemanticsFlag isRequired
```

{@template dart.ui.semantics.isRequired} 语义节点是否为必需。

如果为 true，在提交表单之前需要在该语义节点上进行用户输入。

例如，登录表单要求其电子邮件文本字段非空。

另请参阅：

- [SemanticsFlag.hasRequiredState]，用于启用必需状态。{@endtemplate}

### values

```dart
List<SemanticsFlag> get values
```

### fromIndex()

```dart
SemanticsFlag? fromIndex(int index)
```

### toString()

```dart
String toString()
```

# CheckedState

```dart
enum CheckedState {}
```

语义节点的选中状态。

该语义节点没有选中状态。

该语义节点已选中。

该语义节点未选中。

该语义节点表示处于混合状态的三态复选框。

### CheckedState()

```dart
CheckedState(int value)
```

该标志的构造函数。

### value

```dart
int value
```

该标志的值。

### hasConflict()

```dart
bool hasConflict(CheckedState other)
```

如果两个语义节点都具有选中状态，则它们存在冲突，无法合并。

### merge()

```dart
CheckedState merge(CheckedState other)
```

仅当语义节点之间不存在冲突时才会合并。

# Tristate

```dart
enum Tristate {}
```

语义节点的三态标志

该属性不适用于此语义节点。

该属性适用，且其状态为 "true" 或 "on"。

该属性适用，且其状态为 "false" 或 "off"。

### Tristate()

```dart
Tristate(int value)
```

该标志的构造函数。

### value

```dart
int value
```

该标志的值。

### hasConflict()

```dart
bool hasConflict(Tristate other)
```

如果两个语义节点都具有此属性，则它们存在冲突，无法合并。

### merge()

```dart
Tristate merge(Tristate other)
```

仅当语义节点之间不存在冲突时才会合并。

### toBoolOrNull()

```dart
bool? toBoolOrNull()
```

将三态标志转换为布尔值或 null。

# SemanticsHitTestBehavior

```dart
enum SemanticsHitTestBehavior {}
```

描述语义节点在命中测试期间应表现出的行为。

此枚举允许框架向平台的无障碍层传达指针事件处理行为。不同平台可能会根据其无障碍基础设施以不同方式实现此行为。

另请参阅：

- [SemanticsUpdateBuilder.updateNode]，接受此枚举。

遵循平台默认的命中测试行为推断。

设置为 defer 时，平台将根据语义节点的属性（如交互行为、路由作用域等）推断适当的行为。

在 Web 上，非交互式语义节点的默认推断行为为 `transparent`，允许指针事件穿透。

这是默认值，用于向后兼容。

该语义元素在命中测试中不透明，会消耗其边界内的任何指针事件，阻止它们到达 Z 轴顺序中位于其后面的元素（兄弟节点和祖先节点）。

此节点的子项仍可正常接收指针事件。只有在视觉上位于此节点之后（堆叠顺序更低）的元素才会被阻止接收事件。

这通常用于对话框、底部面板和抽屉等模态界面，这些界面应阻止与其背后内容的交互，同时仍允许与自身内容的交互。

平台实现：

- 在 Web 上，这会转换为 `pointer-events: all` CSS 属性。

该语义元素在命中测试中透明。

透明节点不接收命中测试事件，并允许事件穿透到其后面的元素。

注意：这与框架的 `HitTestBehavior.translucent` 不同，后者在接收事件的同时也允许事件穿透。Web 的二元 `pointer-events` 属性（all 或 none）无法支持真正的半透明行为。

平台实现：

- 在 Web 上，这会转换为 `pointer-events: none` CSS 属性。

# SemanticsFlags

```dart
class SemanticsFlags extends NativeFieldWrapperClass1 {}
```

表示一组布尔标志的集合，用于传达 Widget 的无障碍状态和属性等语义信息。

例如，这些标志可以指示元素是否可勾选、当前是否已勾选、是否可选择，或是否作为按钮使用。

### SemanticsFlags()

```dart
SemanticsFlags({CheckedState isChecked = CheckedState.none, Tristate isSelected = Tristate.none, Tristate isEnabled = Tristate.none, Tristate isToggled = Tristate.none, Tristate isExpanded = Tristate.none, Tristate isRequired = Tristate.none, Tristate isFocused = Tristate.none, bool isButton = false, bool isTextField = false, bool isInMutuallyExclusiveGroup = false, bool isHeader = false, bool isObscured = false, bool scopesRoute = false, bool namesRoute = false, bool isHidden = false, bool isImage = false, bool isLiveRegion = false, bool hasImplicitScrolling = false, bool isMultiline = false, bool isReadOnly = false, bool isLink = false, bool isSlider = false, bool isKeyboardKey = false, bool isAccessibilityFocusBlocked = false})
```

创建一组描述 Widget 各种状态的语义标志。除非另有指定，否则所有标志默认均为 `false`。

### none

```dart
SemanticsFlags none
```

所有标志均设置为 false 的语义标志集合。

### isChecked

```dart
CheckedState isChecked
```

{@macro dart.ui.semantics.hasCheckedState}

### isSelected

```dart
Tristate isSelected
```

{@macro dart.ui.semantics.isSelected}

### isEnabled

```dart
Tristate isEnabled
```

{@macro dart.ui.semantics.isEnabled}

### isToggled

```dart
Tristate isToggled
```

{@macro dart.ui.semantics.isToggled}

### isExpanded

```dart
Tristate isExpanded
```

{@macro dart.ui.semantics.isExpanded}

### isRequired

```dart
Tristate isRequired
```

{@macro dart.ui.semantics.isRequired}

### isFocused

```dart
Tristate isFocused
```

{@macro dart.ui.semantics.isFocused}

### isAccessibilityFocusBlocked

```dart
bool isAccessibilityFocusBlocked
```

该节点的无障碍焦点是否被阻止。

如果为 `true`，则该节点无法获得无障碍焦点。如果为 `false`，是否可获得无障碍焦点则根据节点的角色和其他属性（例如是否为按钮）来确定。

这里指的是无障碍焦点，即 TalkBack 和 VoiceOver 等屏幕阅读器所使用的焦点。它不同于输入焦点，后者通常由当前响应键盘输入的元素持有。

### isButton

```dart
bool isButton
```

{@macro dart.ui.semantics.isButton}

### isTextField

```dart
bool isTextField
```

{@macro dart.ui.semantics.isTextField}

### isInMutuallyExclusiveGroup

```dart
bool isInMutuallyExclusiveGroup
```

{@macro dart.ui.semantics.isInMutuallyExclusiveGroup}

### isHeader

```dart
bool isHeader
```

{@macro dart.ui.semantics.isHeader}

### isObscured

```dart
bool isObscured
```

{@macro dart.ui.semantics.isObscured}

### scopesRoute

```dart
bool scopesRoute
```

{@macro dart.ui.semantics.scopesRoute}

### namesRoute

```dart
bool namesRoute
```

{@macro dart.ui.semantics.namesRoute}

### isHidden

```dart
bool isHidden
```

{@macro dart.ui.semantics.isHidden}

### isImage

```dart
bool isImage
```

{@macro dart.ui.semantics.isImage}

### isLiveRegion

```dart
bool isLiveRegion
```

{@macro dart.ui.semantics.isLiveRegion}

### hasImplicitScrolling

```dart
bool hasImplicitScrolling
```

{@macro dart.ui.semantics.hasImplicitScrolling}

### isMultiline

```dart
bool isMultiline
```

{@macro dart.ui.semantics.isMultiline}

### isReadOnly

```dart
bool isReadOnly
```

{@macro dart.ui.semantics.isReadOnly}

### isLink

```dart
bool isLink
```

{@macro dart.ui.semantics.isLink}

### isSlider

```dart
bool isSlider
```

{@macro dart.ui.semantics.isSlider}

### isKeyboardKey

```dart
bool isKeyboardKey
```

{@macro dart.ui.semantics.isKeyboardKey}

### merge()

```dart
SemanticsFlags merge(SemanticsFlags other)
```

合并两组标志，只要某个标志在两组中的任意一组中为 true，则合并后的集合中该标志即为 true。

### copyWith()

```dart
SemanticsFlags copyWith({CheckedState? isChecked, Tristate? isSelected, Tristate? isEnabled, Tristate? isToggled, Tristate? isExpanded, Tristate? isRequired, Tristate? isFocused, bool? isButton, bool? isTextField, bool? isInMutuallyExclusiveGroup, bool? isHeader, bool? isObscured, bool? scopesRoute, bool? namesRoute, bool? isHidden, bool? isImage, bool? isLiveRegion, bool? hasImplicitScrolling, bool? isMultiline, bool? isReadOnly, bool? isLink, bool? isSlider, bool? isKeyboardKey, bool? isAccessibilityFocusBlocked})
```

复制语义标志，并可选地替换其中部分标志。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toStrings()

```dart
List<String> toStrings()
```

将标志转换为字符串列表。

### hasRepeatedFlags()

```dart
bool hasRepeatedFlags(SemanticsFlags other)
```

检查此实例和 [other] 实例中是否有任何布尔语义标志同时被设置为 true。

### hasConflictingFlags()

```dart
bool hasConflictingFlags(SemanticsFlags other)
```

检查此实例和 [other] 实例中是否存在任何冲突的标志。

# SemanticsValidationResult

```dart
enum SemanticsValidationResult {}
```

表单字段的验证结果。

值的类型、形状和正确性取决于所使用的表单字段种类。例如，电话号码文本字段可能会检查值是否为正确格式的电话号码，和/或该电话号码是否具有正确的区号。一组单选按钮可能会验证用户是否至少选择了一个单选选项。

该节点没有附加验证信息。

这是默认值。大多数语义节点不包含验证信息。通常只有属于输入表单一部分的节点——文本字段、复选框、单选按钮、下拉菜单——才会被验证，并将验证结果附加到其对应的语义节点上。

输入的值有效，不应向用户显示错误。

输入的值无效，应向用户传达错误信息。

# StringAttribute

```dart
abstract base class StringAttribute extends NativeFieldWrapperClass1 {}
```

字符串属性的抽象接口，影响辅助技术（例如 VoiceOver 或 TalkBack）处理文本的方式。

另请参阅：

- [AttributedString](https://www.yuque.com/thyname/flutter.semantics/attributedstring)，使用字符串属性的地方。
- [SpellOutStringAttribute](https://www.yuque.com/thyname/dart.ui/spelloutstringattribute)，使辅助技术在朗读字符串时逐字符拼读。
- [LocaleStringAttribute](https://www.yuque.com/thyname/dart.ui/localestringattribute)，使辅助技术以特定语言处理字符串。

### range

```dart
TextRange range
```

此属性适用的文本范围。

### copy()

```dart
StringAttribute copy({required TextRange range})
```

创建一个新属性，复制所有属性，但 range 会更新为指定的值。

例如，[LocaleStringAttribute](https://www.yuque.com/thyname/dart.ui/localestringattribute) 为其字符范围指定一个 [Locale](https://www.yuque.com/thyname/dart.ui/locale)。复制它将生成一个具有相同语言区域但 [TextRange](https://www.yuque.com/thyname/dart.ui/textrange) 已更新的新 [LocaleStringAttribute](https://www.yuque.com/thyname/dart.ui/localestringattribute)。

# SpellOutStringAttribute

```dart
base class SpellOutStringAttribute extends StringAttribute {}
```

一种字符串属性，使辅助技术（例如 VoiceOver）逐字符拼读字符串。

另请参阅：

- [AttributedString](https://www.yuque.com/thyname/flutter.semantics/attributedstring)，使用字符串属性的地方。
- [LocaleStringAttribute](https://www.yuque.com/thyname/dart.ui/localestringattribute)，使辅助技术以特定语言处理字符串。

### SpellOutStringAttribute()

```dart
SpellOutStringAttribute({required TextRange range})
```

创建一个字符串属性，表示辅助技术在朗读字符串时必须拼读 [range] 内的文本。

### copy()

```dart
StringAttribute copy({required TextRange range})
```

### toString()

```dart
String toString()
```

# LocaleStringAttribute

```dart
base class LocaleStringAttribute extends StringAttribute {}
```

一种字符串属性，使辅助技术（例如 VoiceOver）将字符串视为特定语言处理。

另请参阅：

- [AttributedString](https://www.yuque.com/thyname/flutter.semantics/attributedstring)，使用字符串属性的地方。
- [SpellOutStringAttribute](https://www.yuque.com/thyname/dart.ui/spelloutstringattribute)，使辅助技术在朗读字符串时逐字符拼读。

### LocaleStringAttribute()

```dart
LocaleStringAttribute({required TextRange range, required Locale locale})
```

创建一个字符串属性，表示辅助技术在朗读字符串时必须将 [range] 内的文本视为由 [locale] 指定的语言。

### locale

```dart
Locale locale
```

此属性的语言。

### copy()

```dart
StringAttribute copy({required TextRange range})
```

### toString()

```dart
String toString()
```

# SemanticsUpdateBuilder

```dart
abstract class SemanticsUpdateBuilder {}
```

用于创建 [SemanticsUpdate](https://www.yuque.com/thyname/dart.ui/semanticsupdate) 对象的对象。

创建后，[SemanticsUpdate](https://www.yuque.com/thyname/dart.ui/semanticsupdate) 对象可以传递给 [PlatformDispatcher.updateSemantics]，以更新传达给用户的语义信息。

### SemanticsUpdateBuilder()

```dart
SemanticsUpdateBuilder()
```

创建一个空的 [SemanticsUpdateBuilder](https://www.yuque.com/thyname/dart.ui/semanticsupdatebuilder) 对象。

### updateNode()

```dart
void updateNode({required int id, required SemanticsFlags flags, required int actions, required int maxValueLength, required int currentValueLength, required int textSelectionBase, required int textSelectionExtent, required int platformViewId, required int scrollChildren, required int scrollIndex, required int traversalParent, required double scrollPosition, required double scrollExtentMax, required double scrollExtentMin, required Rect rect, required String identifier, required String label, required List<StringAttribute> labelAttributes, required String value, required List<StringAttribute> valueAttributes, required String increasedValue, required List<StringAttribute> increasedValueAttributes, required String decreasedValue, required List<StringAttribute> decreasedValueAttributes, required String hint, required List<StringAttribute> hintAttributes, required String tooltip, required TextDirection? textDirection, required Float64List transform, required Float64List hitTestTransform, required Int32List childrenInTraversalOrder, required Int32List childrenInHitTestOrder, required Int32List additionalActions, int headingLevel = 0, String linkUrl = '', SemanticsRole role = SemanticsRole.none, required List<String>? controlsNodes, SemanticsValidationResult validationResult = SemanticsValidationResult.none, SemanticsHitTestBehavior hitTestBehavior = SemanticsHitTestBehavior.defer, required SemanticsInputType inputType, required Locale? locale, required String minValue, required String maxValue})
```

更新具有给定 `id` 的节点关联的信息。

语义节点构成一棵树，树的根节点 id 始终为零。`childrenInTraversalOrder` 和 `childrenInHitTestOrder` 是该节点直接子节点的 id。前者按遍历顺序枚举子节点，后者按命中测试顺序枚举相同的子节点。这两个列表长度必须相同，且包含相同的 id，二者的区别仅在于 id 列出的顺序。有关不同子节点顺序的更多信息，请参阅 [DebugSemanticsDumpOrder](https://www.yuque.com/thyname/flutter.semantics/debugsemanticsdumporder)。

系统会保留当前可从根节点访问到的节点。给定的更新不必包含更新中未发生变化的节点信息。如果更新后某个节点无法从根节点访问，该节点将从树中丢弃。

`flags` 是应用于此节点的 [SemanticsFlag](https://www.yuque.com/thyname/dart.ui/semanticsflag) 位域。

`actions` 是该节点可执行的 [SemanticsAction](https://www.yuque.com/thyname/dart.ui/semanticsaction) 位域。如果用户希望对该节点执行这些操作之一，将调用 [PlatformDispatcher.onSemanticsActionEvent]，并指定要执行的操作。由于语义树是异步维护的，调用 [PlatformDispatcher.onSemanticsActionEvent] 回调时指定的操作可能已不再可行。

`identifier` 是一个字符串，用于向通过查询无障碍层次结构工作的 UI 自动化工具（例如 Android UI Automator、iOS XCUITest 或 Appium）描述该节点。它不会暴露给用户。

`label` 是描述此节点的字符串。`value` 属性以字符串形式描述节点的当前值。执行 [SemanticsAction.increase] 操作后，`increasedValue` 字符串将成为 `value` 字符串。执行 [SemanticsAction.decrease] 操作后，`decreasedValue` 字符串将成为 `value` 字符串。`hint` 字符串描述对此节点执行操作会产生的结果。所有这些字符串的阅读方向由 `textDirection` 给出。

`labelAttributes`、`valueAttributes`、`hintAttributes`、`increasedValueAttributes` 和 `decreasedValueAttributes` 分别是 `label`、`value`、`hint`、`increasedValue` 和 `decreasedValue` 所携带的 [StringAttribute](https://www.yuque.com/thyname/dart.ui/stringattribute) 列表。它们的内容在语义更新期间不得更改。

`tooltip` 是一个字符串，用于描述当用户悬停或长按此语义节点的支持 Widget 时的附加信息。

`textSelectionBase` 和 `textSelectionExtent` 字段描述了 `value` 内当前选中的文本。值为 -1 表示当前没有文本选区起点或终点。

`maxValueLength` 字段用于指示可编辑文本字段对输入字符数量有限制。如果为 -1，则表示输入字符数量没有限制。`currentValueLength` 字段指示已使用了多少该限制。当 `maxValueLength` >= 0 时，`currentValueLength` 也必须

> = 0，否则应指定为 -1。

`platformViewId` 字段引用平台视图，其语义节点将作为此节点的子节点添加。如果指定了平台视图，则 `childrenInHitTestOrder` 和 `childrenInTraversalOrder` 必须为空。值为 -1 表示此节点未与平台视图关联。

对于可滚动节点，`scrollPosition` 以逻辑像素描述当前滚动位置。`scrollExtentMax` 和 `scrollExtentMin` 描述 `scrollPosition` 可以取的最大和最小范围值。两者可以均为无穷大，以表示无限制滚动。`scrollPosition` 的值可以（暂时）超出此范围，例如在过度滚动期间。`scrollChildren` 是贡献语义信息的子节点总数，`scrollIndex` 是贡献语义信息的第一个可见子节点的索引。

`traversalParent` 指定作为此节点无障碍遍历逻辑父节点的语义节点的 ID。此参数仅由 Web 引擎使用，用于在绘制顺序中未直接连接的节点之间建立父子关系。为确保正确的无障碍遍历，`traversalParent` 应设置为逻辑遍历父节点 ID。此参数是 Web 特有的，因为其他平台可以在按遍历顺序生成语义树时完成嫁接。嫁接后，遍历顺序和命中测试顺序将不同，这对其他平台是可以接受的。但是，Web 引擎假定这两个顺序完全相同，因此无法在 Web 上提前进行嫁接。相反，Web 引擎通过此参数设置 `aria-owns` 属性来更新遍历顺序。值为 -1 表示没有特殊的遍历父节点。此参数对其他平台没有影响。

`rect` 是此节点在其自身坐标系中所占据的区域。

`transform` 是将此节点的坐标系映射到其父节点坐标系的矩阵。

`headingLevel` 描述此节点是一个标题，以及此节点作为标题所代表的层级。值为 0 表示此节点不是标题。值为 1 或更大表示此节点是指定层级的标题。有效值范围为 1 到 6（含）。此属性仅用于 Web 平台，对其他平台无影响。

`linkUrl` 描述此节点所链接到的 URI。如果该节点不是链接，则应为空字符串。

`role` 描述此节点的角色。如果未设置，默认为 [SemanticsRole.none]。

`locale` 描述此节点中内容（即 label、value 和 hint）的语言。

如果 `validationResult` 不为 null，则表示验证表单字段的结果。如果为 null，表示该节点未被验证，或结果未知。验证用户输入但不使用此参数的表单字段应使用其他方式向用户传达验证错误，例如将验证错误文本嵌入标签中。

`hitTestBehavior` 描述此节点在命中测试期间应表现出的行为。设置为 [SemanticsHitTestBehavior.defer]（默认值）时，平台将根据节点自身的其他语义属性（不从父节点继承）推断适当的行为。不同平台可能会以不同方式实现此行为。

例如，对话框等模态界面可以将此设置为 [SemanticsHitTestBehavior.opaque]，以阻止指针事件到达其背后的内容，而非交互性的装饰元素可以将其设置为 [SemanticsHitTestBehavior.transparent]，以允许指针事件穿透。

另请参阅：

- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/heading_role
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-level
- [SemanticsValidationResult](https://www.yuque.com/thyname/dart.ui/semanticsvalidationresult)，描述 `validationResult` 参数的可能取值。
- [SemanticsHitTestBehavior](https://www.yuque.com/thyname/dart.ui/semanticshittestbehavior)，描述命中测试的行为方式。

### updateCustomAction()

```dart
void updateCustomAction({required int id, String? label, String? hint, int overrideId = -1})
```

更新与给定 `id` 关联的自定义语义操作。

暴露给用户的操作名称为 `label`。对于被覆盖的标准操作，此值会被忽略。

`hint` 应描述执行某项操作后会发生什么，而不是完成点击的方式。例如，使用 "删除" 而不是 "双击以删除"。

`hint` 和 `label` 的文本方向与全局 window 相同。

对于被覆盖的标准操作，`overrideId` 对应一个 [SemanticsAction.index] 值。对于自定义操作，不应提供此参数。

### build()

```dart
SemanticsUpdate build()
```

创建一个封装此对象所记录更新的 [SemanticsUpdate](https://www.yuque.com/thyname/dart.ui/semanticsupdate) 对象。

返回的对象可以传递给 [PlatformDispatcher.updateSemantics]，以实际更新系统保留的语义信息。

调用 build 后，此对象将不可用。

# SemanticsUpdate

```dart
abstract class SemanticsUpdate {}
```

表示一批语义更新的不透明对象。

要创建 SemanticsUpdate 对象，请使用 [SemanticsUpdateBuilder](https://www.yuque.com/thyname/dart.ui/semanticsupdatebuilder)。

可以使用 [PlatformDispatcher.updateSemantics] 方法将语义更新应用于系统保留的语义树。

### dispose()

```dart
void dispose()
```

释放此语义更新所使用的资源。

调用此函数后，该语义更新将无法再使用。

由于该原生函数会调用 Dart API（Dart_SetNativeInstanceField），因此不能是叶调用。
