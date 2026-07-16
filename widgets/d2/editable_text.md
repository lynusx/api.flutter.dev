# SelectionChangedCallback

```dart
typedef SelectionChangedCallback = void Function(TextSelection selection, SelectionChangedCause? cause)
```

当用户更改选区（包括光标位置）时，用于报告该变化的回调签名。

# AppPrivateCommandCallback

```dart
typedef AppPrivateCommandCallback = void Function(String action, Map<String, dynamic> data)
```

用于报告应用私有命令（app private command）结果的回调签名。

# EditableTextContextMenuBuilder

```dart
typedef EditableTextContextMenuBuilder = Widget Function(BuildContext context, EditableTextState editableTextState)
```

为给定的 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 构建上下文菜单的组件 builder 签名。

另请参阅：

- [SelectableRegionContextMenuBuilder](https://www.yuque.com/thyname/flutter.widgets/selectableregioncontextmenubuilder)，为 [SelectableRegion](https://www.yuque.com/thyname/flutter.widgets/selectableregion) 执行相同角色的类型。

# kDefaultContentInsertionMimeTypes

```dart
List<String> kDefaultContentInsertionMimeTypes
```

未提供 allowedMimeTypes 时使用的默认 MIME 类型。

默认值支持插入任何受支持格式的图片。

# TextEditingController

```dart
class TextEditingController extends ValueNotifier<TextEditingValue> {}
```

用于可编辑文本字段的控制器。

每当用户通过关联的 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 修改文本字段时，该文本字段会更新其 [value]，控制器则会通知其监听器。监听器随后可以读取 [text] 和 [selection] 属性，以了解用户输入了什么内容，或选区是如何更新的。

同样，如果你修改了 [text] 或 [selection] 属性，文本字段将收到通知并做出相应更新。

[TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 还可用于为文本字段提供初始值。如果你使用一个已经具有 [text] 的控制器来构建文本字段，该文本字段将以此文本作为其初始值。

该控制器的 [value]（以及 [text] 和 [selection]）可以在添加到此控制器的监听器内部进行更新。需要注意避免无限循环，因为监听器自身内部发起的更改也会触发对该监听器的通知。在监听器内部修改组合区域（composing region）也可能与某些输入法产生不良交互。例如，Gboard 会尝试恢复以编程方式修改过的文本组合区域，从而在框架与输入法之间形成无限的通信循环。建议改用 [TextInputFormatter](https://www.yuque.com/thyname/flutter.services/textinputformatter) 来实现即时输入修改。

如果需要同时更改 [text] 和 [selection] 属性，请改为设置控制器的 [value]。设置 [text] 会清除选区和组合范围。

请记得在不再需要 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 时调用 [dispose]，以确保释放该对象所使用的所有资源。

{@tool dartpad} 此示例创建了一个带有 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，其变更监听器会强制将输入的文本转为小写，并使光标始终保持在输入内容的末尾。

** 参见 examples/api/lib/widgets/editable_text/text_editing_controller.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，一种可通过 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 控制的 Material 风格文本字段。
- [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，一种可通过 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 控制的原始可编辑文本区域。
- 在我们的一篇 [烹饪书教程](https://docs.flutter.dev/cookbook/forms/text-field-changes#2-use-a-texteditingcontroller) 中了解如何使用 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller)。

### TextEditingController()

```dart
TextEditingController({String? text})
```

创建一个用于可编辑文本字段的控制器，初始时没有选区。

此构造函数会将为 null 的 [text] 参数视为空字符串处理。

初始选区为 `TextSelection.collapsed(offset: -1)`。这表示完全没有选区（此时 [TextSelection.isValid] 为 false）。当使用选区无效的控制器构建的文本字段获得焦点时，该文本字段会更新选区（该选区将是一个位于文本末尾的空选区）。

可考虑使用 [TextEditingController.fromValue] 同时初始化文本和选区。

{@tool dartpad} 此示例创建了一个 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，其 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的初始选区为空（折叠），并位于文本的开头（偏移量为 0）。

** 参见 examples/api/lib/widgets/editable_text/text_editing_controller.1.dart 中的代码 ** {@end-tool}

### TextEditingController.fromValue()

```dart
TextEditingController.fromValue(TextEditingValue? value)
```

根据初始的 [TextEditingValue](https://www.yuque.com/thyname/flutter.services/texteditingvalue) 为可编辑文本字段创建一个控制器。

此构造函数会将为 null 的 [value] 参数视为 [TextEditingValue.empty] 处理。

### text

```dart
String get text
```

用户当前正在编辑的字符串。

### text

```dart
set text(String newText)
```

将当前 [text] 更新为给定的 `newText`，并移除该控制器所持有的现有选区和组合范围。

此 setter 通常仅用于测试，因为它会重置光标位置和组合状态。对于生产代码，**建议改用 [value] setter 来更新 [text] 值**，并为新的 [text] 指定一个合理的选区范围。

设置此值会通知此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的所有监听器需要进行更新（会调用 [notifyListeners]）。因此，此属性只应在帧与帧之间设置，例如响应用户操作时设置，而不应在构建、布局或绘制阶段设置。可以在添加到此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的监听器中设置此属性。

### value

```dart
set value(TextEditingValue newValue)
```

### buildTextSpan()

```dart
TextSpan buildTextSpan({required BuildContext context, TextStyle? style, required bool withComposing})
```

根据当前编辑值构建 [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan)。

默认情况下会使组合范围内的文本显示为带下划线。子类可以重写此方法以自定义文本的外观。

### selection

```dart
TextSelection get selection
```

[text] 中当前被选中的范围。

如果选区是折叠的，则此属性给出光标在文本中的偏移量。

### selection

```dart
set selection(TextSelection newSelection)
```

设置此值会通知此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的所有监听器需要进行更新（会调用 [notifyListeners]）。因此，此属性只应在帧与帧之间设置，例如响应用户操作时设置，而不应在构建、布局或绘制阶段设置。

可以在添加到此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的监听器中设置此属性；但是，不应在另一条语句中同时设置 [text]。若要同时更改 [text] 和 [selection]，请改为更改控制器的 [value]。

如果新的选区超出组合范围，组合范围将被清除。

### clear()

```dart
void clear()
```

将 [value] 设置为空。

调用此函数后，[text] 将变为空字符串，选区将折叠在偏移量 0 处。

调用此方法会通知此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的所有监听器需要进行更新（会调用 [notifyListeners]）。因此，此方法只应在帧与帧之间调用，例如响应用户操作时调用，而不应在构建、布局或绘制阶段调用。

### clearComposing()

```dart
void clearComposing()
```

将组合区域设置为一个空范围。

组合区域是指仍在被输入法编辑中的文本范围。调用此函数表示用户已完成该区域的输入编辑。

调用此方法会通知此 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 的所有监听器需要进行更新（会调用 [notifyListeners]）。因此，此方法只应在帧与帧之间调用，例如响应用户操作时调用，而不应在构建、布局或绘制阶段调用。

# ToolbarOptions

```dart
class ToolbarOptions {}
```

[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的工具栏配置。

工具栏是当用户右键单击或长按 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 时弹出的上下文菜单。它包含若干选项：剪切、复制、粘贴和全选。

[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 及其派生组件都有各自默认的 [ToolbarOptions](https://www.yuque.com/thyname/flutter.widgets/toolbaroptions)。如果希望对工具栏选项进行显式控制，可创建自定义的 [ToolbarOptions](https://www.yuque.com/thyname/flutter.widgets/toolbaroptions)。

### ToolbarOptions()

```dart
ToolbarOptions({bool copy = false, bool cut = false, bool paste = false, bool selectAll = false})
```

使用给定的选项创建一个工具栏配置。

如果未显式设置，所有选项默认均为 false。

### empty

```dart
ToolbarOptions empty
```

一个未启用任何选项的 [ToolbarOptions](https://www.yuque.com/thyname/flutter.widgets/toolbaroptions) 实例。

### copy

```dart
bool copy
```

是否在工具栏中显示复制选项。

默认为 false。

### cut

```dart
bool cut
```

是否在工具栏中显示剪切选项。

如果 [EditableText.readOnly] 设置为 true，无论如何都会禁用剪切。

默认为 false。

### paste

```dart
bool paste
```

是否在工具栏中显示粘贴选项。

如果 [EditableText.readOnly] 设置为 true，无论如何都会禁用粘贴。

默认为 false。

### selectAll

```dart
bool selectAll
```

是否在工具栏中显示全选选项。

默认为 false。

# ContentInsertionConfiguration

```dart
class ContentInsertionConfiguration {}
```

配置通过软键盘插入媒体内容的能力。

此配置为通过系统输入法插入的任何富媒体内容提供处理程序，同时也提供了限制插入内容 MIME 类型的能力。

另请参阅：

- [EditableText.contentInsertionConfiguration]

### ContentInsertionConfiguration()

```dart
ContentInsertionConfiguration({required ValueChanged<KeyboardInsertedContent> onContentInserted, List<String> allowedMimeTypes = kDefaultContentInsertionMimeTypes})
```

使用指定的选项创建一个内容插入配置。

必须提供插入内容的处理程序，即 [onContentInserted]。

也可以通过 [allowedMimeTypes] 提供允许插入内容的 MIME 类型，该列表不能为空。

### onContentInserted

```dart
ValueChanged<KeyboardInsertedContent> onContentInserted
```

当用户通过虚拟/屏幕键盘插入内容时调用，目前仅在 Android 上使用。

[KeyboardInsertedContent](https://www.yuque.com/thyname/flutter.services/keyboardinsertedcontent) 持有表示所插入内容的数据。

{@tool dartpad}

此示例展示了如何在你的 `TextField` 中访问所插入内容的数据。

** 参见 examples/api/lib/widgets/editable_text/editable_text.on_content_inserted.0.dart 中的代码 ** {@end-tool}

另请参阅：

- <https://developer.android.com/guide/topics/text/image-keyboard>

### allowedMimeTypes

```dart
List<String> allowedMimeTypes
```

{@template flutter.widgets.contentInsertionConfiguration.allowedMimeTypes} 当用户通过设备键盘插入基于图片的内容时使用，目前仅在 Android 上使用。

传入的字符串列表将决定通过设备键盘允许插入哪些 MIME 类型。

默认的 MIME 类型由 [kDefaultContentInsertionMimeTypes](https://www.yuque.com/thyname/flutter.widgets/kdefaultcontentinsertionmimetypes) 给出。这些是所有能够被处理并从键盘插入的 MIME 类型。

此字段不能为空列表。

{@tool dartpad} 此示例展示了如何将图片插入限制为特定的文件类型。

** 参见 examples/api/lib/widgets/editable_text/editable_text.on_content_inserted.0.dart 中的代码 ** {@end-tool}

另请参阅：

- <https://developer.android.com/guide/topics/text/image-keyboard> {@endtemplate}

# EditableText

```dart
class EditableText extends StatefulWidget {}
```

一个基础的文本输入字段。

此组件与 [TextInput](https://www.yuque.com/thyname/flutter.services/textinput) 服务交互，让用户可以编辑其中包含的文本。它同时提供滚动、选择和光标移动功能。

[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 是一个底层组件，旨在作为自定义组件集的构建基础。若需要完整的用户体验，请考虑使用 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) 或 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)。

## 处理用户输入

目前，用户可以通过键盘或文本选择菜单更改此组件所包含的文本。当用户插入或删除文本时，你会收到变更通知，并有机会修改新的文本值：

- 首先会对用户输入应用 [inputFormatters]。

- [controller] 的 [TextEditingController.value] 会被更新为格式化后的结果，controller 的监听器会收到通知。

- 最后会调用 [onChanged] 回调（如果已指定）。

## 输入操作（Input Actions）

可以提供 [TextInputAction](https://www.yuque.com/thyname/flutter.services/textinputaction)，以自定义 Android 和 iOS 软键盘上操作按钮的外观。默认操作为 [TextInputAction.done]。

许多 [TextInputAction](https://www.yuque.com/thyname/flutter.services/textinputaction) 在 Android 和 iOS 之间是通用的。但是，如果提供的 [textInputAction] 在调试模式下不受当前平台支持，当相应的 EditableText 获得焦点时会抛出错误。例如，在 Android 设备上运行时提供 iOS 专有的 "emergencyCall" 操作将在调试模式下产生错误。在发布模式下，不兼容的 [TextInputAction](https://www.yuque.com/thyname/flutter.services/textinputaction) 会被替换为 Android 上的 "unspecified" 或 iOS 上的 "default"。可以通过检测当前平台并选择相应操作来选取合适的 [textInputAction]。

{@template flutter.widgets.EditableText.lifeCycle}

## 生命周期

编辑完成后，例如按下键盘上的 "done" 按钮，会依次发生两个操作：

第一步：编辑被最终确定。此步骤的默认行为包括调用 [onChanged]。该默认行为可以被重写。详情请参阅 [onEditingComplete]。

第二步：使用用户的输入值调用 [onSubmitted]。

[onSubmitted] 可用于在用户结束当前聚焦的输入组件编辑后，手动将焦点移至另一个输入组件。

当此组件拥有焦点时，它会通过 [AutomaticKeepAliveClientMixin.wantKeepAlive] 阻止自身被释放，以避免丢失选区。移除焦点后将允许其被释放。 {@endtemplate}

建议不要直接使用此组件，而应考虑使用 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，它是一个功能完善的 Material 设计风格文本输入字段，支持占位文本、标签和 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 集成。

## 文本编辑 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 及其默认 [Action](https://www.yuque.com/thyname/flutter.widgets/action)

此组件为处理常见文本编辑 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)（如删除、复制和粘贴文本字段中的内容）提供了默认的 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。可以使用 [Actions.invoke] 或 [Actions.maybeInvoke] 方法直接调用这些 [Action](https://www.yuque.com/thyname/flutter.widgets/action)。默认的文本编辑键盘 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts)（通常在 [DefaultTextEditingShortcuts](https://www.yuque.com/thyname/flutter.widgets/defaulttexteditingshortcuts) 中声明）也使用这些 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 和 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 来执行其绑定的文本编辑操作。

可以通过在组件树中此组件上方放置一个 [Actions](https://www.yuque.com/thyname/flutter.widgets/actions) 组件，来重写某个特定 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent) 的默认处理方式。有关预定义的可重写 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 如何被重写的更多信息，请参阅 [Action](https://www.yuque.com/thyname/flutter.widgets/action) 类和 [Action.overridable] 构造函数。

### 删除文本的 Intent 及其默认行为

| **Intent 类**                                                                                                  | **存在选中文本时的默认行为**                                                  | **存在光标（[caret](https://en.wikipedia.org/wiki/Caret_navigation)）时的默认行为（选区为 [TextSelection.collapsed]）** |
| :------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
| [DeleteCharacterIntent](https://www.yuque.com/thyname/flutter.widgets/deletecharacterintent)                   | 删除选中的文本                                                                | 删除光标位置前后用户感知意义上的字符                                                                                    |
| [DeleteToNextWordBoundaryIntent](https://www.yuque.com/thyname/flutter.widgets/deletetonextwordboundaryintent) | 删除选中的文本，以及选区的 [TextSelection.extent] 位置前/后的单词             | 从光标位置删除到上一个或下一个单词边界                                                                                  |
| [DeleteToLineBreakIntent](https://www.yuque.com/thyname/flutter.widgets/deletetolinebreakintent)               | 删除选中的文本，并从选区的 [TextSelection.extent] 位置删除到当前行的行首/行尾 | 从光标位置删除到当前行的逻辑行首或行尾                                                                                  |

### 移动 [光标](https://en.wikipedia.org/wiki/Caret_navigation) 的 Intent

| **Intent 类**                                                                                                                                                                               | **存在选中文本时的默认行为**                                                                                               | **存在光标时的默认行为（[TextSelection.collapsed]）** |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------- |
| [ExtendSelectionByCharacterIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionbycharacterintent)（`collapseSelection: true`）                                             | 将选区折叠到选区逻辑上的起点/终点                                                                                          | 将光标移过其前/后用户感知意义上的字符                 |
| [ExtendSelectionToNextWordBoundaryIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontonextwordboundaryintent)（`collapseSelection: true`）                               | 将选区折叠到选区 [TextSelection.extent] 位置前/后的单词边界                                                                | 将光标移动到上一个/下一个单词边界                     |
| [ExtendSelectionToNextWordBoundaryOrCaretLocationIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontonextwordboundaryorcaretlocationintent)（`collapseSelection: true`） | 将选区折叠到选区 [TextSelection.extent] 位置前/后的单词边界，或折叠到 [TextSelection.base]（以在给定方向上距离更近者为准） | 将光标移动到上一个/下一个单词边界                     |
| [ExtendSelectionToLineBreakIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontolinebreakintent)（`collapseSelection: true`）                                             | 将选区折叠到选区 [TextSelection.extent] 所在行的行首/行尾                                                                  | 将光标移动到当前行的行首/行尾                         |
| [ExtendSelectionVerticallyToAdjacentLineIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionverticallytoadjacentlineintent)（`collapseSelection: true`）                   | 将选区折叠到与选区 [TextSelection.extent] 最接近的、位于上一行/下一行相邻位置的位置                                        | 将光标移动到上一行/下一行相邻位置中最接近的位置       |
| [ExtendSelectionVerticallyToAdjacentPageIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionverticallytoadjacentpageintent)（`collapseSelection: true`）                   | 将选区折叠到与选区 [TextSelection.extent] 最接近的、位于上一页/下一页相邻位置的位置                                        | 将光标移动到上一页/下一页相邻位置中最接近的位置       |
| [ExtendSelectionToDocumentBoundaryIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontodocumentboundaryintent)（`collapseSelection: true`）                               | 将选区折叠到文档的起点/终点                                                                                                | 将光标移动到文档的起点/终点                           |

#### 扩展选区的 Intent

| **Intent 类**                                                                                                                                                                                | **存在选中文本时的默认行为**                                                                                         | **存在光标时的默认行为（[TextSelection.collapsed]）**       |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| [ExtendSelectionByCharacterIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionbycharacterintent)（`collapseSelection: false`）                                             | 将选区的 [TextSelection.extent] 移过其前/后用户感知意义上的字符                                                      |
| [ExtendSelectionToNextWordBoundaryIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontonextwordboundaryintent)（`collapseSelection: false`）                               | 将选区的 [TextSelection.extent] 移动到上一个/下一个单词边界                                                          |
| [ExtendSelectionToNextWordBoundaryOrCaretLocationIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontonextwordboundaryorcaretlocationintent)（`collapseSelection: false`） | 将选区的 [TextSelection.extent] 移动到上一个/下一个单词边界，或 [TextSelection.base]（以在给定方向上距离更近者为准） | 将选区的 [TextSelection.extent] 移动到上一个/下一个单词边界 |
| [ExtendSelectionToLineBreakIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontolinebreakintent)（`collapseSelection: false`）                                             | 将选区的 [TextSelection.extent] 移动到所在行的行首/行尾                                                              |
| [ExtendSelectionVerticallyToAdjacentLineIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionverticallytoadjacentlineintent)（`collapseSelection: false`）                   | 将选区的 [TextSelection.extent] 移动到上一行/下一行相邻位置中最接近的位置                                            |
| [ExtendSelectionVerticallyToAdjacentPageIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectionverticallytoadjacentpageintent)（`collapseSelection: false`）                   | 将选区的 [TextSelection.extent] 移动到上一页/下一页相邻位置中最接近的位置                                            |
| [ExtendSelectionToDocumentBoundaryIntent](https://www.yuque.com/thyname/flutter.widgets/extendselectiontodocumentboundaryintent)（`collapseSelection: false`）                               | 将选区的 [TextSelection.extent] 移动到文档的起点/终点                                                                |
| [SelectAllTextIntent](https://www.yuque.com/thyname/flutter.widgets/selectalltextintent)                                                                                                     | 选中整个文档                                                                                                         |

### 其他 Intent

| **Intent 类**                                                                                                                | **默认行为**                                                                                                                                                                                                                                                                                                                   |
| :--------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [DoNothingAndStopPropagationTextIntent](https://www.yuque.com/thyname/flutter.widgets/donothingandstoppropagationtextintent) | 在输入字段中不执行任何操作，并阻止该按键事件在组件树中进一步传播。                                                                                                                                                                                                                                                             |
| [ReplaceTextIntent](https://www.yuque.com/thyname/flutter.widgets/replacetextintent)                                         | 替换输入字段的 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 中当前的 [TextEditingValue](https://www.yuque.com/thyname/flutter.services/texteditingvalue)，并触发所有相关的用户回调和 [TextInputFormatter](https://www.yuque.com/thyname/flutter.services/textinputformatter)。 |
| [UpdateSelectionIntent](https://www.yuque.com/thyname/flutter.widgets/updateselectionintent)                                 | 更新输入字段的 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 中的当前选区，并触发 [onSelectionChanged] 回调。                                                                                                                                                                   |
| [CopySelectionTextIntent](https://www.yuque.com/thyname/flutter.widgets/copyselectiontextintent)                             | 将选中的文本复制或剪切到剪贴板                                                                                                                                                                                                                                                                                                 |
| [PasteTextIntent](https://www.yuque.com/thyname/flutter.widgets/pastetextintent)                                             | 在光标位置之后插入剪贴板中的当前文本，若选区未折叠则替换选中的文本。                                                                                                                                                                                                                                                           |

## 文本编辑 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts)

也可以通过在组件树中此组件上方插入一个 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，直接将键盘快捷键重新映射为新的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。在使用 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 时，大量默认的文本编辑键盘快捷键在 [DefaultTextEditingShortcuts](https://www.yuque.com/thyname/flutter.widgets/defaulttexteditingshortcuts) 中声明，位于组件树的较上层，其与此 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 之间的任何 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件都将重写这些默认设置。

{@template flutter.widgets.editableText.shortcutsAndTextInput}

### [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 与文本输入之间的交互

Shortcuts 会阻止文本输入字段将其按键作为文本输入接收。例如，在组件树中某个文本输入字段上方放置一个 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，并为 [LogicalKeyboardKey.keyA] 创建一个快捷键，将阻止该字段将此按键作为文本输入接收。换句话说，在该字段中输入按键 "A" 将触发该快捷键，而不会在字段中插入字母 "a"。

这是由于 Flutter 中按键事件的处理方式所致。当引擎接收到一次按键时，会首先通过 [SystemChannels.keyEvent] 给框架一个将其作为原始按键事件处理的机会。这正是 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 通过其 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode) 间接监听的内容。如果该事件未被处理，框架接下来会尝试通过 [SystemChannels.textInput] 将其作为文本输入处理，这正是 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 通过 [TextInputClient](https://www.yuque.com/thyname/flutter.services/textinputclient) 监听的内容。

这种"快捷键阻止文本输入进入某个字段"的行为，可以通过在组件树更下层使用另一个 [Shortcuts](https://www.yuque.com/thyname/flutter.widgets/shortcuts) 组件，将所需的按键映射到 [DoNothingAndStopPropagationIntent](https://www.yuque.com/thyname/flutter.widgets/donothingandstoppropagationintent) 来重写。此时该按键事件会被框架报告为未处理，随后将按常规方式作为文本输入发送。 {@endtemplate}

## 手势事件处理

当 [rendererIgnoresPointer] 为 false（默认值）时，此组件为诸如点击、长按和滚动等用户操作提供了基础的、与平台无关的手势处理。

若需要更完整的手势处理，包括双击选中单词、拖拽选区，以及诸如长按等特定平台的手势处理，可考虑将 [rendererIgnoresPointer] 设为 true，并使用 [TextSelectionGestureDetectorBuilder](https://www.yuque.com/thyname/flutter.widgets/textselectiongesturedetectorbuilder)。

{@template flutter.widgets.editableText.showCaretOnScreen}

## 聚焦时保持光标可见

当获得焦点时，此组件会在以下情况下尝试保持文本区域及其光标（即使 [showCursor] 为 `false`）可见：

- 当用户聚焦此文本字段且该字段并非 [readOnly] 时。
- 当用户更改此文本字段的选区，或在该文本字段并非 [readOnly] 时更改文本内容时。
- 当虚拟键盘弹出时。 {@endtemplate}

## 滚动相关注意事项

如果此 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 不是 [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold) 的后代，而是在 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 或嵌套的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 中使用，请考虑在包含此 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的根 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 上方放置一个 [ScrollNotificationObserver](https://www.yuque.com/thyname/flutter.widgets/scrollnotificationobserver)，以确保 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 及其组件（如 [TextSelectionOverlay](https://www.yuque.com/thyname/flutter.widgets/textselectionoverlay)）能够正确协调滚动。

{@template flutter.widgets.editableText.accessibility}

## 常见无障碍问题排查

### 自定义用户输入无障碍公告

要自定义由文本变化触发的用户输入无障碍公告，请使用 [SemanticsService.sendAnnouncement] 来生成所需的无障碍公告。

在 iOS 上，当 [TextInputFormatter](https://www.yuque.com/thyname/flutter.services/textinputformatter) 为货币值文本字段插入千位分隔符时，屏幕键盘可能会错误地播报最近的输入内容。以下示例演示了如何通过始终将文本字段的内容作为美元货币值播报，来抑制默认的无障碍公告（`\$` 用于插入美元符号，`$newText` 用于插入 `newText` 变量）：

```dart
onChanged: (String newText) {
  if (newText.isNotEmpty) {
    SemanticsService.sendAnnouncement(
      View.of(context),
      '\$$newText',
       Directionality.of(context),
    );
  }
}
```

{@endtemplate}

另请参阅：

- [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，一个功能完善的 Material 设计风格文本输入字段，支持占位文本、标签和 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 集成。

### EditableText()

```dart
EditableText({dynamic key, required TextEditingController controller, required FocusNode focusNode, bool readOnly = false, String obscuringCharacter = '•', bool obscureText = false, bool? autocorrect, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, required TextStyle style, StrutStyle? strutStyle, required Color cursorColor, required Color backgroundCursorColor, TextAlign textAlign = TextAlign.start, TextDirection? textDirection, Locale? locale, double? textScaleFactor, TextScaler? textScaler, int? maxLines = 1, int? minLines, bool expands = false, bool forceLine = true, TextHeightBehavior? textHeightBehavior, TextWidthBasis textWidthBasis = TextWidthBasis.parent, bool autofocus = false, bool? showCursor, bool showSelectionHandles = false, Color? selectionColor, TextSelectionControls? selectionControls, TextInputType? keyboardType, TextInputAction? textInputAction, TextCapitalization textCapitalization = TextCapitalization.none, ValueChanged<String>? onChanged, VoidCallback? onEditingComplete, ValueChanged<String>? onSubmitted, AppPrivateCommandCallback? onAppPrivateCommand, SelectionChangedCallback? onSelectionChanged, VoidCallback? onSelectionHandleTapped, Object groupId = EditableText, TapRegionCallback? onTapOutside, TapRegionUpCallback? onTapUpOutside, List<TextInputFormatter>? inputFormatters, MouseCursor? mouseCursor, bool rendererIgnoresPointer = false, double cursorWidth = 2.0, double? cursorHeight, Radius? cursorRadius, bool cursorOpacityAnimates = false, Offset? cursorOffset, bool paintCursorAboveText = false, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), Brightness keyboardAppearance = Brightness.light, DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool? enableInteractiveSelection, bool? selectAllOnFocus, ScrollController? scrollController, ScrollPhysics? scrollPhysics, Color? autocorrectionTextRectColor, ToolbarOptions? toolbarOptions, Iterable<String>? autofillHints = const <String>[], AutofillClient? autofillClient, Clip clipBehavior = Clip.hardEdge, String? restorationId, ScrollBehavior? scrollBehavior, bool scribbleEnabled = true, bool stylusHandwritingEnabled = defaultStylusHandwritingEnabled, bool enableIMEPersonalizedLearning = true, ContentInsertionConfiguration? contentInsertionConfiguration, EditableTextContextMenuBuilder? contextMenuBuilder, SpellCheckConfiguration? spellCheckConfiguration, TextMagnifierConfiguration magnifierConfiguration = TextMagnifierConfiguration.disabled, UndoHistoryController? undoController, List<Locale>? hintLocales, bool? enableInlinePrediction})
```

创建一个基础的文本输入控件。

[maxLines] 属性可以设为 null，以取消对行数的限制。默认值为 1，即此为单行文本字段。[maxLines] 必须为 null 或大于零。

如果未设置或为 null，[keyboardType] 的值将根据 [autofillHints] 推断（若 [autofillHints] 非空）。否则，若 [maxLines] 恰好为 1，则默认为 [TextInputType.text]；若 [maxLines] 为 null 或大于 1，则默认为 [TextInputType.multiline]。

若 [showCursor] 为 false，或 [showCursor] 为 null（默认值）且 [readOnly] 为 true，则不显示文本光标。

### controller

```dart
TextEditingController controller
```

控制正在编辑的文本。

### focusNode

```dart
FocusNode focusNode
```

控制此组件是否拥有键盘焦点。

### obscuringCharacter

```dart
String obscuringCharacter
```

{@template flutter.widgets.editableText.obscuringCharacter} 当 [obscureText] 为 true 时用于遮盖文本的字符。

必须仅为单个字符。

默认为字符 U+2022 BULLET（•）。{@endtemplate}

### obscureText

```dart
bool obscureText
```

{@template flutter.widgets.editableText.obscureText} 是否隐藏正在编辑的文本（例如用于密码）。

当此值设为 true 时，文本字段中的所有字符都将被替换为 [obscuringCharacter]，且该字段中的文本无法通过复制或剪切获取。若 [readOnly] 也为 true，则文本将无法被选中。

默认为 false。{@endtemplate}

### textHeightBehavior

```dart
TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### textWidthBasis

```dart
TextWidthBasis textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### readOnly

```dart
bool readOnly
```

{@template flutter.widgets.editableText.readOnly} 文本是否可以被更改。

当此值设为 true 时，文本无法通过任何快捷键或键盘操作进行修改。该文本仍然可以被选中。

默认为 false。{@endtemplate}

### forceLine

```dart
bool forceLine
```

此组件的宽度是否无论文本宽度如何都占满全部宽度。

当此值设为 false 时，宽度将基于文本宽度确定，同时也会受 [textWidthBasis] 影响。

默认为 true。

另请参阅：

- [textWidthBasis]，用于控制文本宽度的计算方式。

### toolbarOptions

```dart
ToolbarOptions toolbarOptions
```

工具栏选项的配置。

默认情况下，所有选项均已启用。若 [readOnly] 为 true，无论如何都会禁用粘贴和剪切。若 [obscureText] 为 true，无论如何都会禁用剪切和复制。若 [readOnly] 和 [obscureText] 均为 true，全选也将被禁用。

### showSelectionHandles

```dart
bool showSelectionHandles
```

是否显示选区手柄。

当存在活动选区时，边界的每一侧会出现一个手柄；若选区已折叠，则出现一个手柄。可以拖动这些手柄来调整选区。

另请参阅：

- [showCursor]，用于控制光标的可见性。

### showCursor

```dart
bool showCursor
```

{@template flutter.widgets.editableText.showCursor} 是否显示光标。

光标是指 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 获得焦点时闪烁的插入点。{@endtemplate}

另请参阅：

- [showSelectionHandles]，用于控制选区手柄的可见性。

### autocorrect

```dart
bool autocorrect
```

{@template flutter.widgets.editableText.autocorrect} 是否启用自动更正。

在 iOS 上，若 [autofillHints] 包含与密码相关的提示，则为 false，否则为 true。{@endtemplate}

### smartDashesType

```dart
SmartDashesType smartDashesType
```

{@macro flutter.services.TextInputConfiguration.smartDashesType}

### smartQuotesType

```dart
SmartQuotesType smartQuotesType
```

{@macro flutter.services.TextInputConfiguration.smartQuotesType}

### enableSuggestions

```dart
bool enableSuggestions
```

{@macro flutter.services.TextInputConfiguration.enableSuggestions}

### style

```dart
TextStyle style
```

用于可编辑文本的文本样式。

用户或平台可能会通过 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先的 [MediaQueryData.boldText]、[MediaQueryData.lineHeightScaleFactorOverride]、[MediaQueryData.letterSpacingOverride] 和 [MediaQueryData.wordSpacingOverride]，重写此 [style] 的 [TextStyle.fontWeight]、[TextStyle.height]、[TextStyle.letterSpacing] 和 [TextStyle.wordSpacing]，无论其 [TextStyle.inherit] 值如何。

### undoController

```dart
UndoHistoryController? undoController
```

控制当前可编辑文本的撤销状态。

若为 null，此组件将创建其自己的 [UndoHistoryController](https://www.yuque.com/thyname/flutter.widgets/undohistorycontroller)。

### strutStyle

```dart
StrutStyle get strutStyle
```

{@template flutter.widgets.editableText.strutStyle} 用于垂直布局的支柱样式（strut style）。

[StrutStyle](https://www.yuque.com/thyname/dart.ui/strutstyle) 用于建立可预测的垂直布局。由于字体可能因用户输入及字体回退机制而有所不同，默认启用 [StrutStyle.forceStrutHeight]，将所有行锁定为由 [style] 提供的基础 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 的高度。这确保了输入的文本能够适配所分配的空间。

若为 null，所使用的支柱将继承自 [style] 的取值，并将 [StrutStyle.forceStrutHeight] 设为 true。若未传入 [style]，将改用主题的 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 来生成 [strutStyle]。

若要禁用基于支柱的垂直对齐，改为根据所输入字形动态确定垂直布局，请使用 [StrutStyle.disabled]。

Flutter 的支柱基于 [排版学中的支柱概念](<https://en.wikipedia.org/wiki/Strut_(typesetting)>) 及 CSS 的 [line-height](https://www.w3.org/TR/CSS2/visudet.html#line-height)。{@endtemplate}

在可编辑文本和文本字段中，[StrutStyle](https://www.yuque.com/thyname/dart.ui/strutstyle) 不会使用其独立的默认值，而是改为从 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 继承被省略/为空的属性。参见 [StrutStyle.inheritFromTextStyle]。

用户或平台可能会通过 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先的 [MediaQueryData.lineHeightScaleFactorOverride] 重写此 [strutStyle] 的 [StrutStyle.height]。

### textAlign

```dart
TextAlign textAlign
```

{@template flutter.widgets.editableText.textAlign} 文本应如何水平对齐。

默认为 [TextAlign.start]。{@endtemplate}

### textDirection

```dart
TextDirection? textDirection
```

{@template flutter.widgets.editableText.textDirection} 文本的方向性。

这决定了诸如 [TextAlign.start] 和 [TextAlign.end] 之类的 [textAlign] 值应如何解释。

这也用于消除双向文本渲染方式的歧义。例如，如果文本是一段英文短语后跟一段希伯来语短语，在 [TextDirection.ltr] 上下文中，英文短语将位于左侧、希伯来语短语位于其右侧；而在 [TextDirection.rtl] 上下文中，英文短语将位于右侧、希伯来语短语位于其左侧。

默认为周围环境的 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)（如果存在）。{@endtemplate}

### textCapitalization

```dart
TextCapitalization textCapitalization
```

{@template flutter.widgets.editableText.textCapitalization} 配置平台键盘将选择大写还是小写键盘。

仅支持文本类键盘，其他类型的键盘将忽略此配置。大小写处理具有语言区域感知能力。

默认为 [TextCapitalization.none]。

另请参阅：

- [TextCapitalization](https://www.yuque.com/thyname/flutter.services/textcapitalization)，各种大小写行为的说明。

{@endtemplate}

### locale

```dart
Locale? locale
```

当同一个 Unicode 字符可能因语言区域而呈现不同渲染效果时，用于选择字体。

通常很少需要设置此属性。默认情况下，此值通过 `Localizations.localeOf(context)` 从周围的应用继承。

更多信息请参阅 [RenderEditable.locale]。

### textScaleFactor

```dart
double? textScaleFactor
```

{@template flutter.widgets.editableText.textScaleFactor} 已弃用。将在 Flutter 未来版本中移除。请改用 [textScaler]。

每个逻辑像素对应的字体像素数。

例如，若文本缩放因子为 1.5，文本将比指定字号大 50%。

默认为从周围环境的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 获取的 [MediaQueryData.textScaleFactor]，若不存在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 上下文，则为 1.0。{@endtemplate}

### textScaler

```dart
TextScaler? textScaler
```

{@macro flutter.painting.textPainter.textScaler}

### cursorColor

```dart
Color cursorColor
```

绘制光标时使用的颜色。

### autocorrectionTextRectColor

```dart
Color? autocorrectionTextRectColor
```

绘制自动更正矩形（autocorrection Rect）时使用的颜色。

对于 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)，该值被设置为环境 [CupertinoThemeData.primaryColor]、透明度为 20% 的颜色。对于 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，在非 iOS 平台上该值为 null，在 iOS 上使用与 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield) 相同的颜色。

目前，自动更正矩形仅出现在 iOS 上。

默认为 null，即禁用自动更正矩形的绘制。

### backgroundCursorColor

```dart
Color backgroundCursorColor
```

渲染浮动光标（floating cursor）时，用于绘制与文本对齐的背景光标的颜色。

通常应将其设置为 [CupertinoColors.inactiveGray]。

另请参阅：

- [FloatingCursorDragState](https://www.yuque.com/thyname/flutter.services/floatingcursordragstate)，其中详细说明了浮动光标功能。

### maxLines

```dart
int? maxLines
```

{@template flutter.widgets.editableText.maxLines} 一次最多显示的行数，必要时会换行。

这会影响字段本身的高度，但不限制可输入到该字段中的行数。

若此值为 1（默认值），文本不会换行，而是改为水平滚动。

若此值为 null，则行数没有限制，文本容器最初会有足够容纳一行的垂直空间，并随着行的输入自动增长，直至达到其约束的高度上限。

若此值不为 null，其值必须大于零，它将把输入锁定为给定的行数，并占用足以容纳该行数的水平空间。同时设置 [minLines] 可让输入在指示的范围内增长和收缩。

[minLines] 和 [maxLines] 可组合实现的完整行为如下所示。以下示例同样适用于 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)、[TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield)、[CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)。

占据单行且按需水平滚动的输入。

```dart
const TextField()
```

高度从一行开始，随着输入文本的需要增长到所需的任意行数。若其父组件对高度施加了限制，达到该限制后将垂直滚动。

```dart
const TextField(maxLines: null)
```

输入的高度足以容纳给定的行数。若输入了更多行，输入将垂直滚动。

```dart
const TextField(maxLines: 2)
```

高度随内容在最小值和最大值之间增长的输入。使用 `maxLines: null` 可实现无限的最大值。

```dart
const TextField(minLines: 2, maxLines: 4)
```

另请参阅：

- [minLines]，用于设置可见的最小行数。{@endtemplate}
- [expands]，用于确定该字段是否应填满其父容器的高度。

### minLines

```dart
int? minLines
```

{@template flutter.widgets.editableText.minLines} 当内容所占行数少于此值时，该字段所占据的最小行数。

这会影响字段本身的高度，但不限制可输入到该字段中的行数。

若此值为 null（默认值），文本容器最初会有足够容纳一行的垂直空间，并随着行的输入而增长。

可与 [maxLines] 结合使用，实现多种行为。

以下是 [minLines] 和 [maxLines] 可组合实现的部分行为示例。这些同样适用于 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)、[TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield)、[CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)。

始终至少占据 2 行、且最大值无限的输入。根据需要垂直扩展。

```dart
TextField(minLines: 2)
```

高度从 2 行开始，增长到 4 行后达到高度限制。若输入了更多行，将垂直滚动。

```dart
const TextField(minLines:2, maxLines: 4)
```

默认为 null。

另请参阅：

- [maxLines]，用于设置可见的最大行数，并提供了 minLines 和 maxLines 如何交互以产生各种行为的多个示例。{@endtemplate}
- [expands]，用于确定该字段是否应填满其父容器的高度。

### expands

```dart
bool expands
```

{@template flutter.widgets.editableText.expands} 此组件的高度是否将调整为填满其父容器。

若设为 true，并被包裹在诸如 [Expanded](https://www.yuque.com/thyname/flutter.widgets/expanded) 或 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 之类的父组件中，输入将扩展以填满父容器。

当此值设为 true 时，[maxLines] 和 [minLines] 必须均为 null，否则将抛出错误。

默认为 false。

有关 [maxLines]、[minLines] 和 [expands] 如何交互以产生各种行为的完整说明，请参见 [maxLines] 中的示例。

与父容器高度相匹配的输入：

```dart
const Expanded(
  child: TextField(maxLines: null, expands: true),
)
```

{@endtemplate}

### autofocus

```dart
bool autofocus
```

{@template flutter.widgets.editableText.autofocus} 当没有其他组件已获得焦点时，此文本字段是否应自行聚焦。

若为 true，键盘将在此文本字段获得焦点后立即弹出。否则，仅在用户点按该文本字段后才会显示键盘。

默认为 false。{@endtemplate}

### selectionColor

```dart
Color? selectionColor
```

绘制选区时使用的颜色。

若此属性为 null，此组件将从 [DefaultSelectionStyle](https://www.yuque.com/thyname/flutter.widgets/defaultselectionstyle) 获取选区颜色。

对于 [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)，该值被设置为环境 [CupertinoThemeData.primaryColor]、透明度为 20% 的颜色。对于 [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，该值被设置为环境 [TextSelectionThemeData.selectionColor]。

### selectionControls

```dart
TextSelectionControls? selectionControls
```

{@template flutter.widgets.editableText.selectionControls} 用于构建文本选区手柄的可选委托。

历史上，此字段也控制工具栏。现在这一职责已改由 [contextMenuBuilder] 负责。但是，出于向后兼容的考虑，当 [selectionControls] 被设置为一个未混入 [TextSelectionHandleControls](https://www.yuque.com/thyname/flutter.widgets/textselectionhandlecontrols) 的对象时，[contextMenuBuilder] 将被忽略，转而使用 [TextSelectionControls.buildToolbar] 方法。{@endtemplate}

另请参阅：

- [CupertinoTextField](https://www.yuque.com/thyname/flutter.cupertino/cupertinotextfield)，一种包裹 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的组件，会在适合 iOS 平台的用户事件发生时显示选区工具栏。
- [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，一种 Material 设计风格的 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 封装组件，会根据用户在 [ThemeData.platform] 中设置的平台，在适当的用户事件发生时显示选区工具栏。

### keyboardType

```dart
TextInputType keyboardType
```

{@template flutter.widgets.editableText.keyboardType} 用于编辑文本的键盘类型。

若 [maxLines] 为 1，默认为 [TextInputType.text]，否则默认为 [TextInputType.multiline]。{@endtemplate}

### textInputAction

```dart
TextInputAction? textInputAction
```

用于软键盘的操作按钮类型。

### onChanged

```dart
ValueChanged<String>? onChanged
```

{@template flutter.widgets.editableText.onChanged} 当用户对 TextField 的值发起更改时调用：即用户插入或删除了文本时。

当 TextField 的文本通过 [controller] 以编程方式更改时，此回调不会运行。通常无需对此类更改进行通知，因为它们是由应用自身发起的。

若要收到关于 TextField 文本、光标和选区的所有更改通知，可以通过 [TextEditingController.addListener] 为其 [controller] 添加一个监听器。

当用户表明已完成编辑时（例如按下键盘上的 "done" 按钮），[onChanged] 会在 [onSubmitted] 之前被调用。该默认行为可以被重写。详情请参阅 [onEditingComplete]。

{@tool dartpad} 此示例展示了如何使用 onChanged，在用户每次插入或删除字符时检查 TextField 的当前值。

** 参见 examples/api/lib/widgets/editable_text/editable_text.on_changed.0.dart 中的代码 ** {@end-tool} {@endtemplate}

## 处理表情符号及其他复杂字符

{@template flutter.widgets.EditableText.onChanged} 在处理可能包含复杂字符的用户输入文本时，务必始终使用 [characters](https://pub.dev/packages/characters)。这将确保扩展字素簇（extended grapheme clusters）和代理对（surrogate pairs）被当作用户所感知的单个字符处理。

例如，在计算某些用户输入文本的长度时，请使用 `string.characters.length`。切勿使用 `string.length`，甚至 `string.runes.length` 也不行。对于复杂字符 "👨‍👩‍👦"，用户会将其视为单个字符，`string.characters.length` 会直观地返回 1。而 `string.length` 返回 8，`string.runes.length` 则返回 5！{@endtemplate}

另请参阅：

- [inputFormatters]，在 [onChanged] 运行之前调用，可用于校验并更改（"格式化"）输入值。
- [onEditingComplete]、[onSubmitted]、[onSelectionChanged]：更为专门化的输入变更通知。
- [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller)，实现了 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 接口，并在 [TextEditingValue](https://www.yuque.com/thyname/flutter.services/texteditingvalue) 变化时通知其监听器。

### onEditingComplete

```dart
VoidCallback? onEditingComplete
```

{@template flutter.widgets.editableText.onEditingComplete} 当用户提交可编辑内容时调用（例如用户按下键盘上的 "done" 按钮）。

[onEditingComplete] 的默认实现会根据具体情况执行两种不同的行为：

- 当按下完成类操作时，例如 "done"、"go"、"send" 或 "search"，用户的内容将被提交给 [controller]，随后放弃焦点。

- 当按下非完成类操作时，例如 "next" 或 "previous"，用户的内容将被提交给 [controller]，但不会放弃焦点，因为开发者可能希望在 [onSubmitted] 中立即将焦点移至另一个输入组件。

提供 [onEditingComplete] 将阻止上述默认行为。{@endtemplate}

### onSubmitted

```dart
ValueChanged<String>? onSubmitted
```

{@template flutter.widgets.editableText.onSubmitted} 当用户表明已完成对字段中文本的编辑时调用。

默认情况下，[onSubmitted] 会在用户完成编辑后于 [onChanged] 之后调用；或者，如果默认行为已被重写，则在 [onEditingComplete] 之后调用。详情请参阅 [onEditingComplete]。

## 测试

以下是在测试中推荐使用的触发 [onSubmitted] 的方法：

```dart
await tester.testTextInput.receiveAction(TextInputAction.done);
```

通过 `tester.sendKeyEvent` 发送 `LogicalKeyboardKey.enter` 不会触发 [onSubmitted]。这是因为在真实设备上，引擎会将回车键转换为完成操作，而 `tester.sendKeyEvent` 仅将按键发送给框架。{@endtemplate}

### onAppPrivateCommand

```dart
AppPrivateCommandCallback? onAppPrivateCommand
```

{@template flutter.widgets.editableText.onAppPrivateCommand} 用于接收来自输入法的私有命令。

当收到 [TextInputClient.performPrivateCommand] 的结果时调用。

这可用于提供仅特定输入法及其客户端之间已知的领域专属功能。

另请参阅：

- [performPrivateCommand](<https://developer.android.com/reference/android/view/inputmethod/InputConnection#performPrivateCommand(java.lang.String,%20android.os.Bundle)>)，Android 关于 performPrivateCommand 的文档，用于从输入法发送命令。
- [sendAppPrivateCommand](https://developer.android.com/reference/android/view/inputmethod/InputMethodManager#sendAppPrivateCommand)，Android 关于 sendAppPrivateCommand 的文档，用于向输入法发送命令。{@endtemplate}

### onSelectionChanged

```dart
SelectionChangedCallback? onSelectionChanged
```

{@template flutter.widgets.editableText.onSelectionChanged} 当用户更改文本的选区（包括光标位置）时调用。{@endtemplate}

### onSelectionHandleTapped

```dart
VoidCallback? onSelectionHandleTapped
```

{@macro flutter.widgets.SelectionOverlay.onSelectionHandleTapped}

### groupId

```dart
Object groupId
```

{@template flutter.widgets.editableText.groupId} 此文本字段所属 [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion) 的组标识符。

具有相同组标识符的文本字段共享同一个点按区域。默认为 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的类型。

另请参阅：

- [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion)，用于为某个应被纳入设置了 [groupId] 的 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 点按区域的组件赋予 [groupId]。{@endtemplate}

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

{@template flutter.widgets.editableText.onTapOutside} 当文本字段处于聚焦状态时，每次在 [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion) 组之外发生按下时调用。

若此值为 null，将触发 [EditableTextTapOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapoutsideintent)。在默认实现中，当此文本字段的 [focusNode] 上收到 [PointerDownEvent](https://www.yuque.com/thyname/flutter.gestures/pointerdownevent) 时，将调用 [FocusNode.unfocus]。但是，为遵循平台惯例，移动应用的触摸事件（不包括鼠标点击）不会导致其失焦。要更改此行为，可在此处设置回调，或重写 [EditableTextTapOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapoutsideintent)。

传递给该函数的 [PointerDownEvent](https://www.yuque.com/thyname/flutter.gestures/pointerdownevent) 是引发此通知的事件。该事件可能发生在此文本字段直接定义的边界框之外，但会位于某个 [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion) 成员的边界框内。{@endtemplate}

{@tool dartpad} 此示例展示了如何使用 `TextFieldTapRegion` 包裹一组用于增减 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) 中数值的 "微调器" 按钮，且不会导致该文本字段失去键盘焦点。

此示例包含一个通用的 `SpinnerField<T>` 类，你可以将其复制到自己的项目中并进行自定义。

** 参见 examples/api/lib/widgets/tap_region/text_field_tap_region.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [TapRegion](https://www.yuque.com/thyname/flutter.widgets/tapregion)，了解区域组是如何确定的。
- [onTapUpOutside]，在每次抬起点按时调用。
- [EditableTextTapOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapoutsideintent)，此值为 null 时会触发的 intent。

### onTapUpOutside

```dart
TapRegionUpCallback? onTapUpOutside
```

{@template flutter.widgets.editableText.onTapUpOutside} 当文本字段处于聚焦状态时，每次在 [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion) 组之外发生抬起时调用。

若此值为 null，将触发 [EditableTextTapUpOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapupoutsideintent)。在默认实现中，这是一个空操作。要更改此行为，可在此处设置回调，或重写 [EditableTextTapUpOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapupoutsideintent)。

传递给该函数的 [PointerUpEvent](https://www.yuque.com/thyname/flutter.gestures/pointerupevent) 是引发此通知的事件。该事件可能发生在此文本字段直接定义的边界框之外，但会位于某个 [TextFieldTapRegion](https://www.yuque.com/thyname/flutter.widgets/textfieldtapregion) 成员的边界框内。{@endtemplate}

另请参阅：

- [TapRegion](https://www.yuque.com/thyname/flutter.widgets/tapregion)，了解区域组是如何确定的。
- [onTapOutside]，在每次按下点按时调用。
- [EditableTextTapOutsideIntent](https://www.yuque.com/thyname/flutter.widgets/editabletexttapoutsideintent)，此值为 null 时会触发的 intent。

### inputFormatters

```dart
List<TextInputFormatter>? inputFormatters
```

{@template flutter.widgets.editableText.inputFormatters} 可选的输入校验与格式化重写项。

当用户更改此组件包含的文本时，格式化器会按照提供的顺序依次运行。当此参数发生变化时，新的格式化器要到用户下一次插入或删除文本时才会生效。与 [onChanged] 回调类似，当文本通过 [controller] 以编程方式更改时，格式化器不会运行。

另请参阅：

- [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller)，实现了 [Listenable](https://www.yuque.com/thyname/flutter.foundation/listenable) 接口，并在 [TextEditingValue](https://www.yuque.com/thyname/flutter.services/texteditingvalue) 变化时通知其监听器。{@endtemplate}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

鼠标指针进入或悬停在该组件上时使用的光标样式。

若此属性为 null，将使用 [SystemMouseCursors.text]。

[mouseCursor] 是 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 中唯一控制鼠标指针外观的属性。所有其他与 "cursor" 相关的属性均指文本光标，即通常在编辑位置闪烁的竖线。

### rendererIgnoresPointer

```dart
bool rendererIgnoresPointer
```

调用方是否将提供手势处理（true），或 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 是否被期望自行处理基础手势（false）。

若此值为 false，[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)（更具体地说是 [RenderEditable](https://www.yuque.com/thyname/flutter.rendering/rendereditable)）将启用一些基础手势（点按以定位光标、长按以全选，以及一些滚动行为）。

这些行为足以用于调试目的，但不足以满足面向用户的应用需求。若要启用特定平台的行为，请使用 [TextSelectionGestureDetectorBuilder](https://www.yuque.com/thyname/flutter.widgets/textselectiongesturedetectorbuilder) 包裹 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，并将 [rendererIgnoresPointer] 设为 true。

若 [rendererIgnoresPointer] 为 true，此组件创建的 [RenderEditable](https://www.yuque.com/thyname/flutter.rendering/rendereditable) 将不处理指针事件。

此属性默认为 false。

另请参阅：

- [RenderEditable.ignorePointer]，实现此功能的属性。
- [TextSelectionGestureDetectorBuilder](https://www.yuque.com/thyname/flutter.widgets/textselectiongesturedetectorbuilder)，实现特定平台手势与行为的类。

### cursorWidth

```dart
double cursorWidth
```

{@template flutter.widgets.editableText.cursorWidth} 光标的粗细。

默认为 2.0。

光标绘制在文本下方。对于从左到右的文本，光标宽度会向字符边界的右侧延伸；对于从右到左的文本，则向左侧延伸。这相当于相对于选中位置向下游（downstream）方向延伸。负值可用于反转此行为。{@endtemplate}

### cursorHeight

```dart
double? cursorHeight
```

{@template flutter.widgets.editableText.cursorHeight} 光标的高度。

若此属性为 null，将使用 [RenderEditable.preferredLineHeight]。{@endtemplate}

### cursorRadius

```dart
Radius? cursorRadius
```

{@template flutter.widgets.editableText.cursorRadius} 光标圆角的弧度。

默认情况下，光标没有圆角。{@endtemplate}

### cursorOpacityAnimates

```dart
bool cursorOpacityAnimates
```

{@template flutter.widgets.editableText.cursorOpacityAnimates} 光标在每次闪烁期间是否从完全透明渐变为完全不透明。

默认情况下，光标的不透明度在 iOS 平台上会有渐变动画，在 Android 平台上则不会。{@endtemplate}

### cursorOffset

```dart
Offset? cursorOffset
```

{@macro flutter.rendering.RenderEditable.cursorOffset}

### paintCursorAboveText

```dart
bool paintCursorAboveText
```

{@macro flutter.rendering.RenderEditable.paintCursorAboveText}

### selectionHeightStyle

```dart
ui.BoxHeightStyle selectionHeightStyle
```

控制计算所得选区高亮框的高度。

有关可用样式的详情，请参阅 [ui.BoxHeightStyle]。

### selectionWidthStyle

```dart
ui.BoxWidthStyle selectionWidthStyle
```

控制计算所得选区高亮框的宽度。

有关可用样式的详情，请参阅 [ui.BoxWidthStyle]。

### keyboardAppearance

```dart
Brightness keyboardAppearance
```

键盘的外观。

此设置仅在 iOS 设备上生效。

默认为 [Brightness.light]。

### scrollPadding

```dart
EdgeInsets scrollPadding
```

{@template flutter.widgets.editableText.scrollPadding} 当文本字段滚动进入视图时，配置周围 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 的内边距。

当此组件获得焦点且未完全可见时（例如部分滚出屏幕，或被键盘遮挡），它将尝试通过滚动周围的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable)（若存在）来使自己可见。此值控制滚动后 TextField 距离 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 边缘的距离。

默认为 EdgeInsets.all(20.0)。{@endtemplate}

### enableInteractiveSelection

```dart
bool enableInteractiveSelection
```

{@template flutter.widgets.editableText.enableInteractiveSelection} 是否启用用于更改文本选区的用户界面功能。

例如，将此值设为 true 将启用诸如长按 TextField 以选中文本并显示剪切/复制/粘贴菜单，以及点按以移动文本插入点等功能。

若此值为 false，用户无法调整文本选区，剪切/复制/粘贴菜单将被隐藏，剪切/复制/粘贴文本的快捷键将不执行任何操作，仅阻止该按键事件传播给焦点链中的其他按键事件处理程序。

默认为 true。{@endtemplate}

### debugDeterministicCursor

```dart
bool debugDeterministicCursor
```

将此属性设为 true 会使光标在获得焦点后出现时停止闪烁或渐隐渐现。此属性适用于测试目的。

它不影响 EditableText 必须先获得焦点、光标才能首次出现的这一前提。

默认为 false，即呈现典型的闪烁光标。

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### scrollController

```dart
ScrollController? scrollController
```

{@template flutter.widgets.editableText.scrollController} 垂直滚动输入内容时使用的 [ScrollController](https://www.yuque.com/thyname/flutter.widgets/scrollcontroller)。

若为 null，将实例化一个新的 ScrollController。

参见 [Scrollable.controller]。{@endtemplate}

### scrollPhysics

```dart
ScrollPhysics? scrollPhysics
```

{@template flutter.widgets.editableText.scrollPhysics} 垂直滚动输入内容时使用的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics)。

若未指定，将根据当前平台确定行为。

参见 [Scrollable.physics]。{@endtemplate}

如果为 [scrollBehavior] 提供了显式的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)，该 behavior 提供的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics) 将在 [scrollPhysics] 之后优先生效。

### scribbleEnabled

```dart
bool scribbleEnabled
```

{@template flutter.widgets.editableText.scribbleEnabled} 是否为此组件启用 iOS 14 Scribble 功能。

仅在 iPad 上可用。

默认为 true。{@endtemplate}

### stylusHandwritingEnabled

```dart
bool stylusHandwritingEnabled
```

{@template flutter.widgets.editableText.stylusHandwritingEnabled} 此输入是否支持手写笔手写功能，即用户可直接在字段上方书写。

目前仅支持以下设备：

- 运行 iOS 14 及以上版本、使用 Apple Pencil 的 iPad。
- 运行 API 34 及以上版本、使用激活手写笔的 Android 设备。{@endtemplate}

在 Android 上，Scribe 手势的检测发生在 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 之外，通常由 [TextSelectionGestureDetectorBuilder](https://www.yuque.com/thyname/flutter.widgets/textselectiongesturedetectorbuilder) 完成。在 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) 中会自动处理此情况。

另请参阅：

- [ScribbleClient](https://www.yuque.com/thyname/flutter.services/scribbleclient)，可混入任意组件以提供 iOS Scribble 功能。
- [Scribe](https://www.yuque.com/thyname/flutter.services/scribe)，可用于直接与 Android Scribe 交互。

### selectionEnabled

```dart
bool get selectionEnabled
```

{@template flutter.widgets.editableText.selectionEnabled} 与 [enableInteractiveSelection] 相同。

此 getter 的存在主要是为了与 [RenderEditable.selectionEnabled] 保持一致。{@endtemplate}

### selectAllOnFocus

```dart
bool selectAllOnFocus
```

{@template flutter.widgets.editableText.selectAllOnFocus} 此字段在获得焦点时是否应全选文本。

若为 false，聚焦此文本字段时将保持其现有文本选区不变。

在 Web 和桌面平台上默认为 true，在移动平台上默认为 false。{@endtemplate}

### autofillHints

```dart
Iterable<String>? autofillHints
```

{@template flutter.widgets.editableText.autofillHints} 一组字符串列表，帮助自动填充服务识别此文本输入的类型。

若设为 null，此文本输入将不会向平台发送其自动填充信息，从而阻止其参与由其他 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient) 触发的自动填充，即使它们处于同一个 [AutofillScope](https://www.yuque.com/thyname/flutter.services/autofillscope) 中。此外，在 Android 和 Web 上，将此值设为 null 将禁用此文本字段的自动填充功能。

支持自动填充的最低平台 SDK 版本为 Android 的 API 级别 26 及 iOS 10.0。

默认为空列表。

### 设置 iOS 自动填充：

为提供最佳用户体验并确保你的应用完全支持 iOS 上的密码自动填充，请遵循以下步骤：

- 设置你的 iOS 应用的[关联域名](https://developer.apple.com/documentation/safariservices/supporting_associated_domains_in_your_app)。
- 部分自动填充提示仅适用于特定的 [keyboardType]。例如，[AutofillHints.name] 需要 [TextInputType.name]，[AutofillHints.email] 仅适用于 [TextInputType.emailAddress]。请确保输入字段具有兼容的 [keyboardType]。经验表明，[TextInputType.name] 可与 iOS 上预定义的许多自动填充提示良好配合使用。

### 自动填充问题排查

自动填充服务提供商在很大程度上依赖 [autofillHints]。请确保 [autofillHints] 中的条目受当前使用的自动填充服务支持（该服务的名称通常可在移动设备的系统设置中找到）。

#### 点按文本字段时自动填充界面未出现

请检查设备的系统设置，确保已开启自动填充功能，且自动填充服务中存有可用的凭据。

- iOS 密码自动填充：前往"设置" -> "密码"，开启"自动填充密码"，并通过点击右上角的 "+" 按钮添加新密码以进行测试。如果你的应用尚未设置关联域名，可使用任意 "网站"。只要至少存有一个密码，当密码相关字段获得焦点时，你应能在软键盘的快捷类型栏中看到一个钥匙形图标。

- iOS 联系人信息自动填充：iOS 似乎会从设备当前关联的 Apple ID 中提取联系人信息。前往"设置" -> "Apple ID"（通常是第一项，若尚未在设备上设置则显示为"登录你的 iPhone"），并填写相关字段。若要测试更多联系人信息类型，可尝试在"通讯录" -> "我的名片"中添加。

- Android 自动填充：前往"设置" -> "系统" -> "语言和输入法" -> "自动填充服务"。启用你选择的自动填充服务，并确保存在与你的应用关联的可用凭据。

指定 [InputDecoration.hintText] 也可能有助于自动填充服务（如三星 Pass）确定输入字段的预期内容类型，尽管在存在 autofillHints 时通常不需要这样做。

#### 我调用了 `TextInput.finishAutofillContext`，但自动填充保存

提示未显示

- iOS：iOS 在保存用户密码时可能不会显示提示或任何其他视觉提示。前往"设置" -> "密码"，检查你的新密码是否已保存。若未在应用中正确设置关联域名，密码保存和自动生成强密码功能均无法工作。要设置关联域名，请遵循 <https://developer.apple.com/documentation/safariservices/supporting_associated_domains_in_your_app> 中的说明。

{@endtemplate} {@macro flutter.services.AutofillConfiguration.autofillHints}

### autofillClient

```dart
AutofillClient? autofillClient
```

控制此输入字段自动填充行为的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)。

若为 null，此组件的 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 将被用作 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)。此属性可能会重写 [autofillHints]。

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

默认为 [Clip.hardEdge]。

### restorationId

```dart
String? restorationId
```

用于保存和恢复 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 滚动偏移量的恢复 ID（Restoration ID）。

若提供了恢复 ID，[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 将持久化其当前的滚动偏移量，并在状态恢复期间将其恢复。

滚动偏移量会通过使用给定恢复 ID 从周围的 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope) 认领的 [RestorationBucket](https://www.yuque.com/thyname/flutter.services/restorationbucket) 中持久化。

持久化和恢复 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 内容的职责由 [controller] 的所有者负责，该所有者可以为此目的使用 [RestorableTextEditingController](https://www.yuque.com/thyname/flutter.widgets/restorabletexteditingcontroller)。

另请参阅：

- [RestorationManager](https://www.yuque.com/thyname/flutter.services/restorationmanager)，说明了 Flutter 中状态恢复的工作原理。

### scrollBehavior

```dart
ScrollBehavior? scrollBehavior
```

{@template flutter.widgets.editableText.scrollBehavior} 单独应用于此组件的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)。

默认为 null，此时将复制并修改所继承的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)，以改变视口的装饰（如 [Scrollbar](https://www.yuque.com/thyname/flutter.material/scrollbar)）。

[ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 也提供 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics)。若提供了显式的 [ScrollPhysics](https://www.yuque.com/thyname/flutter.widgets/scrollphysics)（通过 [scrollPhysics]），它将优先生效，其次是 [scrollBehavior]，最后才是继承的祖先 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior)。{@endtemplate}

默认情况下，继承的 [ScrollConfiguration](https://www.yuque.com/thyname/flutter.widgets/scrollconfiguration) 的 [ScrollBehavior](https://www.yuque.com/thyname/flutter.widgets/scrollbehavior) 将被修改为仅在 [maxLines] 大于 1 时应用 [Scrollbar](https://www.yuque.com/thyname/flutter.material/scrollbar)。

### enableIMEPersonalizedLearning

```dart
bool enableIMEPersonalizedLearning
```

{@macro flutter.services.TextInputConfiguration.enableIMEPersonalizedLearning}

### contentInsertionConfiguration

```dart
ContentInsertionConfiguration? contentInsertionConfiguration
```

{@template flutter.widgets.editableText.contentInsertionConfiguration} 通过系统输入法插入内容的处理程序配置。

默认为 null，此时将禁用媒体内容插入，系统将显示一条消息，告知用户该文本字段不支持插入媒体内容。

设置 [ContentInsertionConfiguration.onContentInserted] 以提供处理程序。此外，可设置 [ContentInsertionConfiguration.allowedMimeTypes] 以限制插入内容允许的 MIME 类型。

{@tool dartpad}

此示例展示了如何在你的 `TextField` 中访问所插入内容的数据。

** 参见 examples/api/lib/widgets/editable_text/editable_text.on_content_inserted.0.dart 中的代码 ** {@end-tool}

若未提供 [contentInsertionConfiguration]，默认情况下将向 Flutter 引擎发送一个空的 MIME 类型列表。必须提供处理程序函数，才能自定义插入内容所允许的 MIME 类型。

若在没有处理程序的情况下插入了富媒体内容，系统将显示一条消息，告知用户当前文本输入不支持插入富媒体内容。{@endtemplate}

### contextMenuBuilder

```dart
EditableTextContextMenuBuilder? contextMenuBuilder
```

{@template flutter.widgets.EditableText.contextMenuBuilder} 在用户请求时构建文本选区工具栏。

当调用 [EditableTextState.showToolbar] 时会构建上下文菜单，通常由 [TextSelectionGestureDetectorBuilder.buildGestureDetector] 所创建组件安装的某个回调触发。[contextMenuBuilder] 返回的组件会被传递给一个 [ContextMenuController](https://www.yuque.com/thyname/flutter.widgets/contextmenucontroller)。

若未提供回调，将不会显示任何上下文菜单。

[contextMenuBuilder] 回调所使用的 [EditableTextContextMenuBuilder](https://www.yuque.com/thyname/flutter.widgets/editabletextcontextmenubuilder) 签名有两个参数：[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate)。

[EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 有两个在构建上下文菜单组件时尤为有用的属性：

- [EditableTextState.contextMenuAnchors] 指定了上下文菜单期望的锚定位置。

- [EditableTextState.contextMenuButtonItems] 表示通常应为此组件构建的按钮（例如剪切、复制、粘贴）。

[TextSelectionToolbarLayoutDelegate](https://www.yuque.com/thyname/flutter.widgets/textselectiontoolbarlayoutdelegate) 类在遵循首选锚定位置方面可能特别有用。

出于向后兼容的考虑，当 [EditableText.selectionControls] 被设置为一个未混入 [TextSelectionHandleControls](https://www.yuque.com/thyname/flutter.widgets/textselectionhandlecontrols) 的对象时，[contextMenuBuilder] 将被忽略，转而使用 [TextSelectionControls.buildToolbar] 方法。

{@tool dartpad} 此示例展示了如何自定义菜单，在此例中是为当前平台保留默认按钮，但修改其外观。

** 参见 examples/api/lib/material/context_menu/editable_text_toolbar_builder.0.dart 中的代码 ** {@end-tool}

{@tool dartpad} 此示例展示了如何仅在当前选中了一个电子邮件地址时显示自定义按钮。

** 参见 examples/api/lib/material/context_menu/editable_text_toolbar_builder.1.dart 中的代码 ** {@end-tool}

另请参阅：

- [AdaptiveTextSelectionToolbar](https://www.yuque.com/thyname/flutter.material/adaptivetextselectiontoolbar)，为当前平台构建默认的文本选区工具栏，同时允许自定义按钮。
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons]，根据给定的 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 为当前平台构建按钮 Widget。
- [BrowserContextMenu](https://www.yuque.com/thyname/flutter.services/browsercontextmenu)，允许在 Web 上禁用浏览器的上下文菜单，转而显示 Flutter 渲染的上下文菜单。{@endtemplate}

### spellCheckConfiguration

```dart
SpellCheckConfiguration? spellCheckConfiguration
```

{@template flutter.widgets.EditableText.spellCheckConfiguration} 详细说明应如何执行拼写检查的配置。

指定用于对文本输入进行拼写检查的 [SpellCheckService](https://www.yuque.com/thyname/flutter.services/spellcheckservice)，以及用于为拼写错误的单词添加样式的 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)。

密码类输入将禁用拼写检查，包括 [obscureText] 为 true、[keyboardType] 为 [TextInputType.visiblePassword]，或 [autofillHints] 包含 [AutofillHints.password] 或 [AutofillHints.newPassword] 的情况。

若 [SpellCheckService](https://www.yuque.com/thyname/flutter.services/spellcheckservice) 保持为 null，默认情况下将禁用拼写检查，除非支持 [DefaultSpellCheckService](https://www.yuque.com/thyname/flutter.services/defaultspellcheckservice)，此时将使用该服务。目前仅在 Android 和 iOS 上受支持。

若此配置保持为 null，则默认禁用拼写检查。{@endtemplate}

### magnifierConfiguration

```dart
TextMagnifierConfiguration magnifierConfiguration
```

用于此文本字段中选区的放大镜配置。

{@macro flutter.widgets.magnifier.intro}

### hintLocales

```dart
List<Locale>? hintLocales
```

{@macro flutter.services.TextInputConfiguration.hintLocales}

### enableInlinePrediction

```dart
bool? enableInlinePrediction
```

{@macro flutter.services.TextInputConfiguration.enableInlinePrediction}

### defaultSelectionHeightStyle

```dart
ui.BoxHeightStyle get defaultSelectionHeightStyle
```

[selectionHeightStyle] 的默认值。

在 Web 平台上，默认为 [ui.BoxHeightStyle.max]。

在原生平台上，所有平台均默认为 [ui.BoxHeightStyle.includeLineSpacingMiddle]。

### defaultSelectionWidthStyle

```dart
ui.BoxWidthStyle get defaultSelectionWidthStyle
```

[selectionWidthStyle] 的默认值。

在 Web 平台上，对于运行基于 WebKit 的 Safari 浏览器的苹果平台，默认为 [ui.BoxWidthStyle.max]；对于其他平台，默认为 [ui.BoxWidthStyle.tight]。

在非 Web 平台上，默认为 [ui.BoxWidthStyle.max]。

### defaultStylusHandwritingEnabled

```dart
bool defaultStylusHandwritingEnabled
```

[stylusHandwritingEnabled] 的默认值。

### getEditableButtonItems()

```dart
List<ContextMenuButtonItem> getEditableButtonItems({required ClipboardStatus? clipboardStatus, required VoidCallback? onCopy, required VoidCallback? onCut, required VoidCallback? onPaste, required VoidCallback? onSelectAll, required VoidCallback? onLookUp, required VoidCallback? onSearchWeb, required VoidCallback? onShare, required VoidCallback? onLiveTextInput})
```

返回 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 列表，表示当前平台默认选区菜单中用于可编辑字段的按钮。

例如，[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 使用此方法为其上下文菜单生成默认按钮。

另请参阅：

- [EditableTextState.contextMenuButtonItems]，为特定 EditableText 提供 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 的方法，作用类似。
- [SelectableRegion.getSelectableButtonItems]，作用类似，但适用于可选中但不可编辑的内容。
- [AdaptiveTextSelectionToolbar](https://www.yuque.com/thyname/flutter.material/adaptivetextselectiontoolbar)，构建工具栏本身，可通过 [AdaptiveTextSelectionToolbar.buttonItems] 接收一组 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem)。
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons]，根据给定的 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 为当前平台构建按钮 Widget。

### createState()

```dart
EditableTextState createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# EditableTextState

```dart
class EditableTextState extends State<EditableText> with AutomaticKeepAliveClientMixin<EditableText>, WidgetsBindingObserver, TickerProviderStateMixin<EditableText>, TextSelectionDelegate, TextInputClient implements AutofillClient {}
```

[EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的 State。

### clipboardStatus

```dart
ClipboardStatusNotifier clipboardStatus
```

检测剪贴板是否可以粘贴。

### currentAutofillScope

```dart
AutofillScope? get currentAutofillScope
```

### spellCheckConfiguration

```dart
SpellCheckConfiguration get spellCheckConfiguration
```

确定拼写检查将如何执行的配置。

如果可能，此配置将包含 [SpellCheckService](https://www.yuque.com/thyname/flutter.services/spellcheckservice) 的默认值（若未另行指定）。

另请参阅：

- [DefaultSpellCheckService](https://www.yuque.com/thyname/flutter.services/defaultspellcheckservice)，默认使用的拼写检查服务。

### spellCheckEnabled

```dart
bool get spellCheckEnabled
```

是否启用了拼写检查。

当为该组件指定了 [SpellCheckConfiguration](https://www.yuque.com/thyname/flutter.widgets/spellcheckconfiguration) 时，拼写检查即被启用。

### spellCheckResults

```dart
SpellCheckResults? spellCheckResults
```

文本输入最新的拼写检查结果。

这些结果会通过 [SpellCheckService](https://www.yuque.com/thyname/flutter.services/spellcheckservice) 调用拼写检查而更新，并被此组件用于为文本输入构建 [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan) 树，以及为拼写错误单词的替换建议构建菜单。

### wantKeepAlive

```dart
bool get wantKeepAlive
```

### cutEnabled

```dart
bool get cutEnabled
```

### copyEnabled

```dart
bool get copyEnabled
```

### pasteEnabled

```dart
bool get pasteEnabled
```

### selectAllEnabled

```dart
bool get selectAllEnabled
```

### lookUpEnabled

```dart
bool get lookUpEnabled
```

### searchWebEnabled

```dart
bool get searchWebEnabled
```

### shareEnabled

```dart
bool get shareEnabled
```

### liveTextInputEnabled

```dart
bool get liveTextInputEnabled
```

### copySelection()

```dart
void copySelection(SelectionChangedCause cause)
```

将当前选区复制到 [Clipboard](https://www.yuque.com/thyname/flutter.services/clipboard)。

### cutSelection()

```dart
void cutSelection(SelectionChangedCause cause)
```

将当前选区剪切到 [Clipboard](https://www.yuque.com/thyname/flutter.services/clipboard)。

### pasteText()

```dart
Future<void> pasteText(SelectionChangedCause cause)
```

从 [Clipboard](https://www.yuque.com/thyname/flutter.services/clipboard) 粘贴文本。

### selectAll()

```dart
void selectAll(SelectionChangedCause cause)
```

选中整个文本值。

### lookUpSelection()

```dart
Future<void> lookUpSelection(SelectionChangedCause cause)
```

查找当前选区，类似于 iOS 编辑菜单中的 "查询" 按钮。

目前仅在 iOS 上实现。

若选区为空或已折叠，将抛出错误。

### searchWebForSelection()

```dart
Future<void> searchWebForSelection(SelectionChangedCause cause)
```

针对当前选区发起网络搜索，类似于 iOS 编辑菜单中的 "网页搜索" 按钮。

目前仅在 iOS 上实现。

当 `obscureText` 为 true 或选区为空时，此函数不会执行任何操作。

### shareSelection()

```dart
Future<void> shareSelection(SelectionChangedCause cause)
```

针对当前选区启动分享界面，类似于 iOS 编辑菜单中的 "分享..." 按钮。

目前仅在 iOS 和 Android 上实现。

当 `obscureText` 为 true 或选区为空时，此函数不会执行任何操作。

### findSuggestionSpanAtCursorIndex()

```dart
SuggestionSpan? findSuggestionSpanAtCursorIndex(int cursorIndex)
```

使用二分查找，找到与给定索引匹配的指定 [SuggestionSpan](https://www.yuque.com/thyname/flutter.services/suggestionspan)。

另请参阅：

- [SpellCheckSuggestionsToolbar](https://www.yuque.com/thyname/flutter.material/spellchecksuggestionstoolbar)，Material 风格的拼写检查建议工具栏，使用此方法在工具栏中为拼写错误的单词渲染正确的建议。

### buttonItemsForToolbarOptions()

```dart
List<ContextMenuButtonItem>? buttonItemsForToolbarOptions([TargetPlatform? targetPlatform])
```

返回给定 [ToolbarOptions](https://www.yuque.com/thyname/flutter.widgets/toolbaroptions) 对应的 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 列表。

### getGlyphHeights()

```dart
({double startGlyphHeight, double endGlyphHeight}) getGlyphHeights()
```

获取给定 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 中选区起点和终点处的行高。

另请参阅：

- [TextSelectionToolbarAnchors.getSelectionRect]，依赖此信息。

### contextMenuAnchors

```dart
TextSelectionToolbarAnchors get contextMenuAnchors
```

{@template flutter.widgets.EditableText.getAnchors} 返回默认上下文菜单的锚点位置。{@endtemplate}

另请参阅：

- [contextMenuButtonItems]，为默认上下文菜单按钮提供 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem)。

### contextMenuButtonItems

```dart
List<ContextMenuButtonItem> get contextMenuButtonItems
```

返回 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 列表，表示当前平台针对 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 的默认选区菜单中的按钮。

另请参阅：

- [EditableText.getEditableButtonItems]，作用类似，但适用于任意可编辑字段，而不仅限于 EditableText。
- [SystemContextMenu.getDefaultItems]，作用类似，但适用于系统渲染的上下文菜单。
- [SelectableRegionState.contextMenuButtonItems]，作用类似，但适用于可选中但不可编辑的内容。
- [contextMenuAnchors]，为默认上下文菜单提供锚点位置。
- [AdaptiveTextSelectionToolbar](https://www.yuque.com/thyname/flutter.material/adaptivetextselectiontoolbar)，构建工具栏本身，可通过 [AdaptiveTextSelectionToolbar.buttonItems] 接收一组 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem)。
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons]，根据给定的 [ContextMenuButtonItem](https://www.yuque.com/thyname/flutter.widgets/contextmenubuttonitem) 为当前平台构建按钮 Widget。

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
void didUpdateWidget(EditableText oldWidget)
```

### dispose()

```dart
void dispose()
```

### currentTextEditingValue

```dart
TextEditingValue get currentTextEditingValue
```

### updateEditingValue()

```dart
void updateEditingValue(TextEditingValue value)
```

### performAction()

```dart
void performAction(TextInputAction action)
```

### performPrivateCommand()

```dart
void performPrivateCommand(String action, Map<String, dynamic> data)
```

### insertContent()

```dart
void insertContent(KeyboardInsertedContent content)
```

### updateFloatingCursor()

```dart
void updateFloatingCursor(RawFloatingCursorPoint point)
```

### beginBatchEdit()

```dart
void beginBatchEdit()
```

开始一次新的批量编辑，在此期间对文本编辑值所做的新更新不会发送给平台文本输入插件。

批量编辑可以嵌套。当最外层的批量编辑结束时，若检测到发生了变化，[endBatchEdit] 将尝试把 [currentTextEditingValue] 发送给文本输入插件。

### endBatchEdit()

```dart
void endBatchEdit()
```

结束上一次调用 [beginBatchEdit] 所开始的当前批量编辑，并在需要时将 [currentTextEditingValue] 发送给文本输入插件。

若此 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 未处于批量编辑中，在调试模式下将抛出错误。

### didChangeInputControl()

```dart
void didChangeInputControl(TextInputControl? oldControl, TextInputControl? newControl)
```

### onFocusReceived()

```dart
bool onFocusReceived()
```

### connectionClosed()

```dart
void connectionClosed()
```

### requestKeyboard()

```dart
void requestKeyboard()
```

表明有意与键盘进行交互。

如果此控件已附加到键盘，此函数将请求使键盘变为可见。否则，此函数将向焦点系统请求使其获得焦点。若成功获得焦点，该控件随后将附加到键盘并请求使键盘可见。

### didChangeMetrics()

```dart
void didChangeMetrics()
```

### cursorCurrentlyVisible

```dart
bool get cursorCurrentlyVisible
```

此刻闪烁光标是否确实可见（它有一半时间是隐藏的，因为它在闪烁）。

### cursorBlinkInterval

```dart
Duration get cursorBlinkInterval
```

光标闪烁间隔（光标处于"开启"状态或"关闭"状态所持续的时间）。一个完整的光标闪烁周期是此值的两倍（一半开启，一半关闭）。

### selectionOverlay

```dart
TextSelectionOverlay? get selectionOverlay
```

文本选区手柄的当前状态。

### renderEditable

```dart
RenderEditable renderEditable
```

此组件的后代所使用的渲染器。

当 [RenderEditable.ignorePointer] 为 true 时，此属性通常用于将输入手势通知给渲染器。

### textEditingValue

```dart
TextEditingValue get textEditingValue
```

### userUpdateTextEditingValue()

```dart
void userUpdateTextEditingValue(TextEditingValue value, SelectionChangedCause? cause)
```

### bringIntoView()

```dart
void bringIntoView(TextPosition position)
```

### showToolbar()

```dart
bool showToolbar()
```

在当前光标位置显示选区工具栏。

若无法显示工具栏（例如工具栏已经显示，或当前不存在文本选区），则返回 `false`。

### hideToolbar()

```dart
void hideToolbar([bool hideHandles = true])
```

### toggleToolbar()

```dart
void toggleToolbar([bool hideHandles = true])
```

切换工具栏的可见性。

### showSpellCheckSuggestionsToolbar()

```dart
bool showSpellCheckSuggestionsToolbar()
```

显示带有拼写错误单词的拼写检查建议工具栏，可供点击替换。

### showMagnifier()

```dart
void showMagnifier(Offset positionToShow)
```

若当前不存在放大镜，则在 `positionToShow` 给定的位置显示放大镜。

若已存在放大镜，则将其更新到 `positionToShow` 给定的位置。

若无法显示放大镜（例如当前不存在选区浮层），则不执行任何操作。

### hideMagnifier()

```dart
void hideMagnifier()
```

隐藏放大镜。

### insertTextPlaceholder()

```dart
void insertTextPlaceholder(Size size)
```

### removeTextPlaceholder()

```dart
void removeTextPlaceholder()
```

### performSelector()

```dart
void performSelector(String selectorName)
```

### autofillId

```dart
String get autofillId
```

### textInputConfiguration

```dart
TextInputConfiguration get textInputConfiguration
```

### autofill()

```dart
void autofill(TextEditingValue value)
```

### showAutocorrectionPromptRect()

```dart
void showAutocorrectionPromptRect(int start, int end)
```

### build()

```dart
Widget build(BuildContext context)
```

### buildTextSpan()

```dart
TextSpan buildTextSpan()
```

根据当前编辑值构建 [TextSpan](https://www.yuque.com/thyname/flutter.painting/textspan)。

默认情况下会使组合范围内的文本显示为带下划线。子类可以重写此方法以自定义文本的外观。
