@docImport 'package:flutter/material.dart';

# AutocompleteOptionsBuilder

```dart
typedef AutocompleteOptionsBuilder<T extends Object> = FutureOr<Iterable<T>> Function(TextEditingValue textEditingValue)
```

[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 回调的类型，用于根据用户目前已输入的文本，计算该组件字段的可选补全列表。

另请参阅：

- [RawAutocomplete.optionsBuilder]，它属于此类型。

# AutocompleteOnSelected

```dart
typedef AutocompleteOnSelected<T extends Object> = void Function(T option)
```

[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 组件用于表示用户已选择某个选项的回调类型。

另请参阅：

- [RawAutocomplete.onSelected]，它属于此类型。

# AutocompleteOptionsViewBuilder

```dart
typedef AutocompleteOptionsViewBuilder<T extends Object> = Widget Function(BuildContext context, AutocompleteOnSelected<T> onSelected, Iterable<T> options)
```

[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 回调的类型，该回调返回一个 [Widget](https://www.yuque.com/thyname/flutter.widgets/widget)，用于显示指定的 [options]；若用户选择了某个选项，则调用 [onSelected]。

此回调返回的组件将被包装在 [AutocompleteHighlightedOption](https://www.yuque.com/thyname/flutter.widgets/autocompletehighlightedoption) 继承组件中。这样此回调就能够确定当前为键盘导航而高亮显示的是哪个选项。

另请参阅：

- [RawAutocomplete.optionsViewBuilder]，它属于此类型。

# AutocompleteFieldViewBuilder

```dart
typedef AutocompleteFieldViewBuilder = Widget Function(BuildContext context, TextEditingController textEditingController, FocusNode focusNode, VoidCallback onFieldSubmitted)
```

Autocomplete 回调的类型，该回调返回包含输入 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) 或 [TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield) 的组件。

另请参阅：

- [RawAutocomplete.fieldViewBuilder]，它属于此类型。

# AutocompleteOptionToString

```dart
typedef AutocompleteOptionToString<T extends Object> = String Function(T option)
```

[RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 回调的类型，用于将选项值转换为可在组件的选项菜单中显示的字符串。

另请参阅：

- [RawAutocomplete.displayStringForOption]，它属于此类型。

# OptionsViewOpenDirection

```dart
enum OptionsViewOpenDirection {}
```

打开选项视图浮层的方向。

另请参阅：

- [RawAutocomplete.optionsViewOpenDirection]，它属于此类型。
- [RawAutocomplete.optionsViewBuilder]，用于指定如何构建可选选项组件。
- [RawAutocomplete.fieldViewBuilder]，可选地用于指定如何构建对应的字段组件。

向上打开。

选项视图的底边将与由 [RawAutocomplete.fieldViewBuilder] 构建的文本字段的顶边对齐。

向下打开。

选项视图的顶边将与由 [RawAutocomplete.fieldViewBuilder] 构建的文本字段的底边对齐。

在浮层内可用空间最多的方向打开。

可用空间的计算方式为：从字段顶边到浮层顶边的距离（用于向上打开），或从字段底边到浮层底边的距离（用于向下打开）。

若两个方向的可用空间相同，则选项视图向下打开。

# RawAutocomplete

```dart
class RawAutocomplete<T extends Object> extends StatefulWidget {}
```

{@template flutter.widgets.RawAutocomplete.RawAutocomplete} 一个帮助用户通过输入一些文本并从选项列表中进行选择的组件。

用户的文本输入在由 [fieldViewBuilder] 参数构建的字段中接收。要显示的选项通过 [optionsBuilder] 确定，并使用 [optionsViewBuilder] 渲染。

只要 [optionsBuilder] 返回至少一个选项，当字段获得焦点或字段文本发生变化时，选项视图就会打开。当用户选择某个选项、没有匹配的选项，或字段失去焦点时，选项视图就会关闭。{@endtemplate}

这是一个具有非常基础 UI 的核心框架组件。

{@tool dartpad} 此示例展示了如何使用 [fieldViewBuilder] 和 [optionsViewBuilder] 参数创建一个非常基础的自动补全组件。

** 请参阅 examples/api/lib/widgets/autocomplete/raw_autocomplete.0.dart 中的代码 ** {@end-tool}

类型参数 T 表示选项的类型。最常见的情况下它是 String，就像上面的示例那样。不过，也可以使用带有 `toString` 方法的其他类型，或自定义 [displayStringForOption]。选项将使用 `==` 进行比较，因此对于自定义类型，重写 [Object.==] 和 [Object.hashCode] 可能会有帮助。

{@tool dartpad} 此示例与前一个示例类似，但它使用自定义的 T 数据类型，而非直接使用 String。

** 请参阅 examples/api/lib/widgets/autocomplete/raw_autocomplete.1.dart 中的代码 ** {@end-tool}

{@tool dartpad} 此示例展示了在表单中使用 RawAutocomplete 的方法。

** 请参阅 examples/api/lib/widgets/autocomplete/raw_autocomplete.2.dart 中的代码 ** {@end-tool}

另请参阅：

- [Autocomplete](https://www.yuque.com/thyname/flutter.material/autocomplete)，一个基于 RawAutocomplete 的 Material 风格实现。

### RawAutocomplete()

```dart
RawAutocomplete({dynamic key, required AutocompleteOptionsViewBuilder<T> optionsViewBuilder, required AutocompleteOptionsBuilder<T> optionsBuilder, OptionsViewOpenDirection optionsViewOpenDirection = OptionsViewOpenDirection.down, AutocompleteOptionToString<T> displayStringForOption = defaultStringForOption, AutocompleteFieldViewBuilder? fieldViewBuilder, FocusNode? focusNode, AutocompleteOnSelected<T>? onSelected, TextEditingController? textEditingController, TextEditingValue? initialValue})
```

创建一个 RawAutocomplete 实例。

[displayStringForOption]、[optionsBuilder] 和 [optionsViewBuilder] 不得为 null。

### fieldViewBuilder

```dart
AutocompleteFieldViewBuilder? fieldViewBuilder
```

{@template flutter.widgets.RawAutocomplete.fieldViewBuilder} 构建用于获取选项的输入字段。

将提供的 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller) 传递给此处构建的字段，以便 RawAutocomplete 能够监听变化。{@endtemplate}

若此参数为 null，则会改为构建一个 [SizedBox.shrink]。关于该模式的用处，参见 [textEditingController]。

### focusNode

```dart
FocusNode? focusNode
```

用于文本字段的 [FocusNode](https://www.yuque.com/thyname/flutter.widgets/focusnode)。

{@template flutter.widgets.RawAutocomplete.split} 此参数的主要目的是允许使用位于组件树其他部分的单独文本字段，而不是使用 [fieldViewBuilder] 构建的文本字段。例如，可能希望将文本字段放置在 AppBar 中，而将选项放置在主体下方。

按照此模式，可以省略 [fieldViewBuilder]，这样就不会在通常的位置绘制文本字段。可以在其他位置创建一个单独的文本字段，并将 FocusNode 和 TextEditingController 同时传递给该文本字段和 RawAutocomplete。

{@tool dartpad} 此示例展示了如何创建一个文本字段位于 AppBar、结果位于应用主体的自动补全组件。

** 请参阅 examples/api/lib/widgets/autocomplete/raw_autocomplete.focus_node.0.dart 中的代码 ** {@end-tool} {@endtemplate}

若此参数不为 null，则 [textEditingController] 也必须非 null。

### optionsViewBuilder

```dart
AutocompleteOptionsViewBuilder<T> optionsViewBuilder
```

{@template flutter.widgets.RawAutocomplete.optionsViewBuilder} 根据选项对象列表构建可选选项组件。

这些选项会以浮动方式显示在字段的下方或上方的 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 内，而非组件树中与 [RawAutocomplete](https://www.yuque.com/thyname/flutter.widgets/rawautocomplete) 相同的位置。要控制其向上还是向下打开，可使用 [optionsViewOpenDirection]。

为了追踪键盘导航高亮显示的是哪一项，产生的选项将被包装在继承组件 [AutocompleteHighlightedOption](https://www.yuque.com/thyname/flutter.widgets/autocompletehighlightedoption) 中。在此回调内部，可以通过 [AutocompleteHighlightedOption.of] 获取高亮选项的索引，以便通过视觉高亮显示该选项，表明它将是通过键盘选中的选项。

{@endtemplate}

### optionsViewOpenDirection

```dart
OptionsViewOpenDirection optionsViewOpenDirection
```

{@template flutter.widgets.RawAutocomplete.optionsViewOpenDirection} 确定选项视图的打开方向。

默认为 [OptionsViewOpenDirection.down]。{@endtemplate}

### displayStringForOption

```dart
AutocompleteOptionToString<T> displayStringForOption
```

{@template flutter.widgets.RawAutocomplete.displayStringForOption} 返回选项被选中时要在字段中显示的字符串。

当使用自定义 T 类型，且要显示的字符串与用于搜索的字符串不同时，这会很有用。

若未提供，将使用 `option.toString()`。{@endtemplate}

### onSelected

```dart
AutocompleteOnSelected<T>? onSelected
```

{@template flutter.widgets.RawAutocomplete.onSelected} 当用户选择某个选项时调用。{@endtemplate}

### optionsBuilder

```dart
AutocompleteOptionsBuilder<T> optionsBuilder
```

{@template flutter.widgets.RawAutocomplete.optionsBuilder} 一个根据当前 TextEditingValue 返回当前可选选项对象的函数。{@endtemplate}

### textEditingController

```dart
TextEditingController? textEditingController
```

用于文本字段的 [TextEditingController](https://www.yuque.com/thyname/flutter.widgets/texteditingcontroller)。

{@macro flutter.widgets.RawAutocomplete.split}

若此参数不为 null，则 [focusNode] 也必须非 null。

### initialValue

```dart
TextEditingValue? initialValue
```

{@template flutter.widgets.RawAutocomplete.initialValue} 文本字段使用的初始值。{@endtemplate}

设置初始值不会通知 [textEditingController] 的监听器，因此也不会导致选项界面出现。

若定义了 [textEditingController]，则忽略此参数。

### onFieldSubmitted()

```dart
void onFieldSubmitted<T extends Object>(GlobalKey key)
```

为由给定 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 指示的 RawAutocomplete 组件调用 [AutocompleteFieldViewBuilder](https://www.yuque.com/thyname/flutter.widgets/autocompletefieldviewbuilder) 的 onFieldSubmitted 回调。

通常不会使用此方法，除非实现了自定义字段而非使用 [fieldViewBuilder]。在通常情况下，onFieldSubmitted 回调是通过 [AutocompleteFieldViewBuilder](https://www.yuque.com/thyname/flutter.widgets/autocompletefieldviewbuilder) 的签名传递的。若不使用 fieldViewBuilder，则可以通过此静态方法调用同一个回调。

另请参阅：

- [focusNode] 和 [textEditingController]，其中包含展示如何在 fieldViewBuilder 之外创建单独字段的代码示例。

### defaultStringForOption()

```dart
String defaultStringForOption(Object? option)
```

在 [displayStringForOption] 中将选项转换为字符串的默认方式。

使用给定 `option` 的 `toString` 方法。

### createState()

```dart
State<RawAutocomplete<T>> createState()
```

# AutocompletePreviousOptionIntent

```dart
class AutocompletePreviousOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中上一个选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompletePreviousOptionIntent()

```dart
AutocompletePreviousOptionIntent()
```

创建一个 AutocompletePreviousOptionIntent 实例。

# AutocompleteNextOptionIntent

```dart
class AutocompleteNextOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中下一个选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompleteNextOptionIntent()

```dart
AutocompleteNextOptionIntent()
```

创建一个 AutocompleteNextOptionIntent 实例。

# AutocompleteFirstOptionIntent

```dart
class AutocompleteFirstOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中第一个选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompleteFirstOptionIntent()

```dart
AutocompleteFirstOptionIntent()
```

创建一个 AutocompleteFirstOptionIntent 实例。

# AutocompleteLastOptionIntent

```dart
class AutocompleteLastOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中最后一个选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompleteLastOptionIntent()

```dart
AutocompleteLastOptionIntent()
```

创建一个 AutocompleteLastOptionIntent 实例。

# AutocompleteNextPageOptionIntent

```dart
class AutocompleteNextPageOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中当前高亮选项之后一页的选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompleteNextPageOptionIntent()

```dart
AutocompleteNextPageOptionIntent()
```

创建一个 AutocompleteNextPageOptionIntent 实例。

# AutocompletePreviousPageOptionIntent

```dart
class AutocompletePreviousPageOptionIntent extends Intent {}
```

一个用于高亮显示自动补全列表中当前高亮选项之前一页的选项的 [Intent](https://www.yuque.com/thyname/flutter.widgets/intent)。

### AutocompletePreviousPageOptionIntent()

```dart
AutocompletePreviousPageOptionIntent()
```

创建一个 AutocompletePreviousPageOptionIntent 实例。

# AutocompleteHighlightedOption

```dart
class AutocompleteHighlightedOption extends InheritedNotifier<ValueNotifier<int>> {}
```

一个用于指示应为键盘导航高亮显示哪个自动补全选项的继承组件。

`RawAutocomplete` 组件会用此组件包装由 `optionsViewBuilder` 生成的选项视图，以便向构建器提供高亮选项的索引。

在构建器回调中，可以使用静态方法 [of] 获取高亮选项的索引：

```dart
int highlightedIndex = AutocompleteHighlightedOption.of(context);
```

该索引随后可用于判断哪个选项应被赋予视觉提示，表明它将是通过键盘选中的选项。

### AutocompleteHighlightedOption()

```dart
AutocompleteHighlightedOption({dynamic key, required ValueNotifier<int> highlightIndexNotifier, required Widget child})
```

创建一个 AutocompleteHighlightedOption 继承组件的实例。

### of()

```dart
int of(BuildContext context)
```

返回来自最近的 [AutocompleteHighlightedOption](https://www.yuque.com/thyname/flutter.widgets/autocompletehighlightedoption) 祖先的高亮选项索引。

若不存在祖先，则返回 0。

典型用法如下：

```dart
int highlightedIndex = AutocompleteHighlightedOption.of(context);
```
