@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/services.dart';

# Form

```dart
class Form extends StatefulWidget {}
```

用于将多个表单字段 widget（例如 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) widget）组合在一起的可选容器。

每个表单字段都应包装在 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) widget 中，并以 [Form](https://www.yuque.com/thyname/flutter.widgets/form) widget 作为所有这些字段的共同祖先。调用 [FormState](https://www.yuque.com/thyname/flutter.widgets/formstate) 上的方法可以保存、重置或验证该 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的所有 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 后代。要获取 [FormState](https://www.yuque.com/thyname/flutter.widgets/formstate)，可以使用祖先为该 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的 context 调用 [Form.of]，或者向 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 构造函数传入一个 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，然后调用 [GlobalKey.currentState]。

{@tool dartpad} 此示例展示了一个包含一个用于输入电子邮件地址的 [TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield) 和一个用于提交表单的 [ElevatedButton](https://www.yuque.com/thyname/flutter.material/elevatedbutton) 的 [Form](https://www.yuque.com/thyname/flutter.widgets/form)。此处使用 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey) 来标识该 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 并验证输入。

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/form.png)

** See code in examples/api/lib/widgets/form/form.0.dart ** {@end-tool}

另请参阅：

- [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，一种在整个应用中唯一的键。
- [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，维护当前状态的单个表单字段 widget。
- [TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield)，一个便捷的 widget，用于在 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 中包装 [TextField](https://www.yuque.com/thyname/flutter.material/textfield) widget。

### Form()

```dart
Form({dynamic key, required Widget child, bool? canPop, PopInvokedCallback? onPopInvoked, PopInvokedWithResultCallback<Object?>? onPopInvokedWithResult, WillPopCallback? onWillPop, VoidCallback? onChanged, AutovalidateMode? autovalidateMode})
```

创建一个表单字段的容器。

### maybeOf()

```dart
FormState? maybeOf(BuildContext context)
```

返回包含给定 context 的最近 [Form](https://www.yuque.com/thyname/flutter.widgets/form) widget 的 [FormState](https://www.yuque.com/thyname/flutter.widgets/formstate)；如果未找到，则返回 null。

典型用法如下：

```dart
FormState? form = Form.maybeOf(context);
form?.save();
```

调用此方法会在 [context] 中最近的 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 上创建一个依赖关系（如果存在）。

另请参阅：

- [Form.of]，与此方法类似，但在未找到 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 祖先时会触发断言。

### of()

```dart
FormState of(BuildContext context)
```

返回包含给定 context 的最近 [Form](https://www.yuque.com/thyname/flutter.widgets/form) widget 的 [FormState](https://www.yuque.com/thyname/flutter.widgets/formstate)。

典型用法如下：

```dart
FormState form = Form.of(context);
form.save();
```

如果未找到 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 祖先，此方法会在调试模式下触发断言，并在发布模式下抛出异常。

调用此方法会在 [context] 中最近的 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 上创建一个依赖关系。

另请参阅：

- [Form.maybeOf]，与此方法类似，但在未找到 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 祖先时返回 null。

### child

```dart
Widget child
```

此 widget 下方的 widget 树。

这是包含此表单的 widget 层级结构的根节点。

{@macro flutter.widgets.ProxyWidget.child}

### onWillPop

```dart
WillPopCallback? onWillPop
```

使表单能够否决用户关闭包含该表单的 [ModalRoute](https://www.yuque.com/thyname/flutter.widgets/modalroute) 的尝试。

如果该回调返回一个解析为 false 的 Future，则表单所在的路由将不会被弹出。

另请参阅：

- [WillPopScope](https://www.yuque.com/thyname/flutter.widgets/willpopscope)，另一个提供拦截返回按钮方式的 widget。

### canPop

```dart
bool? canPop
```

{@macro flutter.widgets.PopScope.canPop}

{@tool dartpad} 此示例演示如何使用此参数，在导航弹出会导致表单数据丢失时显示确认对话框。

** See code in examples/api/lib/widgets/form/form.1.dart ** {@end-tool}

另请参阅：

- [onPopInvokedWithResult]，同样来自 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope)，通常与此参数结合使用。
- [PopScope.canPop]，[Form](https://www.yuque.com/thyname/flutter.widgets/form) 内部委托的对象。

### onPopInvoked

```dart
PopInvokedCallback? onPopInvoked
```

{@macro flutter.widgets.navigator.onPopInvokedWithResult}

### onPopInvokedWithResult

```dart
PopInvokedWithResultCallback<Object?>? onPopInvokedWithResult
```

{@macro flutter.widgets.navigator.onPopInvokedWithResult}

{@tool dartpad} 此示例演示如何使用此参数，在导航弹出会导致表单数据丢失时显示确认对话框。

** See code in examples/api/lib/widgets/form/form.1.dart ** {@end-tool}

另请参阅：

- [canPop]，同样来自 [PopScope](https://www.yuque.com/thyname/flutter.widgets/popscope)，通常与此参数结合使用。
- [PopScope.onPopInvokedWithResult]，[Form](https://www.yuque.com/thyname/flutter.widgets/form) 内部委托的对象。

### onChanged

```dart
VoidCallback? onChanged
```

当某个表单字段发生变化时调用。

除了会调用此回调外，所有表单字段自身也会重建。

### autovalidateMode

```dart
AutovalidateMode autovalidateMode
```

用于启用/禁用表单字段的自动验证并更新其错误文本。

{@macro flutter.widgets.FormField.autovalidateMode}

### createState()

```dart
FormState createState()
```

# FormState

```dart
class FormState extends State<Form> {}
```

与 [Form](https://www.yuque.com/thyname/flutter.widgets/form) widget 关联的状态。

[FormState](https://www.yuque.com/thyname/flutter.widgets/formstate) 对象可用于保存（[save]）、重置（[reset]）和验证（[validate]）与该 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 关联的所有 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)。

通常通过 [Form.of] 获取。

### fields

```dart
Iterable<FormFieldState<dynamic>> get fields
```

当前已注册到此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的 [FormFieldState](https://www.yuque.com/thyname/flutter.widgets/formfieldstate) 对象。

### build()

```dart
Widget build(BuildContext context)
```

### save()

```dart
void save()
```

保存与此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 关联的每个 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)。

### reset()

```dart
void reset()
```

将与此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 关联的每个 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 重置为其 [FormField.initialValue]。

会调用 [Form.onChanged] 回调。

如果表单的 [Form.autovalidateMode] 属性为 [AutovalidateMode.always]，则重置后将重新验证所有字段。

### clearError()

```dart
void clearError()
```

清除此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 中所有 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 的验证错误，但不会重置其值。

另请参阅：

- [FormFieldState.clearError]，用于清除单个表单字段的错误。

### validate()

```dart
bool validate()
```

验证与此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 关联的每个 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，如果没有错误则返回 true。

表单会重建以报告结果。

另请参阅：

- [validateGranularly]，同样会验证后代 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，但返回的是包含错误字段的 [Set](https://www.yuque.com/thyname/dart.core/set)。

### validateGranularly()

```dart
Set<FormFieldState<Object?>> validateGranularly()
```

验证与此 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 关联的每个 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，仅返回存在错误的字段（如果有）所对应的 [FormFieldState](https://www.yuque.com/thyname/flutter.widgets/formfieldstate) 组成的 [Set](https://www.yuque.com/thyname/dart.core/set)。

此方法可用于高亮显示有错误的字段。

表单会重建以报告结果。

另请参阅：

- [validate]，同样会验证后代 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，并在没有错误时返回 true。

# FormFieldValidator

```dart
typedef FormFieldValidator<T> = String? Function(T? value)
```

用于验证表单字段的签名。

如果输入无效则返回要显示的错误字符串，否则返回 null。

由 [FormField.validator] 使用。

# FormFieldErrorBuilder

```dart
typedef FormFieldErrorBuilder = Widget Function(BuildContext context, String errorText)
```

用于构建错误 widget 的回调签名。

另请参阅：

- [FormField.errorBuilder]，其类型即为此类型，用于传递 [TextFormField.validator] 给出的错误结果。

# FormFieldSetter

```dart
typedef FormFieldSetter<T> = void Function(T? newValue)
```

用于在表单字段值发生变化时收到通知的签名。

由 [FormField.onSaved] 使用。

# FormFieldBuilder

```dart
typedef FormFieldBuilder<T> = Widget Function(FormFieldState<T> field)
```

用于构建表示表单字段的 widget 的签名。

由 [FormField.builder] 使用。

# FormField

```dart
class FormField<T> extends StatefulWidget {}
```

单个表单字段。

此 widget 维护表单字段的当前状态，以便更新和验证错误能够在 UI 中直观呈现。

在 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 内使用时，可以通过 [FormState](https://www.yuque.com/thyname/flutter.widgets/formstate) 上的方法来查询或操作整个表单的数据。例如，调用 [FormState.save] 将依次调用每个 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 的 [onSaved] 回调。

如果想获取 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 的当前状态（例如希望一个表单字段依赖于另一个字段），请为其配备 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)。

不要求存在 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 祖先。[Form](https://www.yuque.com/thyname/flutter.widgets/form) 允许一次性保存、重置或验证多个字段。若不使用 [Form](https://www.yuque.com/thyname/flutter.widgets/form)，可向构造函数传入 [GlobalKey](https://www.yuque.com/thyname/flutter.widgets/globalkey)，并使用 [GlobalKey.currentState] 来保存或重置该表单字段。

另请参阅：

- [Form](https://www.yuque.com/thyname/flutter.widgets/form)，聚合表单字段的 widget。
- [TextField](https://www.yuque.com/thyname/flutter.material/textfield)，一种常用于输入文本的表单字段。

### FormField()

```dart
FormField({dynamic key, required FormFieldBuilder<T> builder, FormFieldSetter<T>? onSaved, VoidCallback? onReset, String? forceErrorText, FormFieldValidator<T>? validator, FormFieldErrorBuilder? errorBuilder, T? initialValue, bool enabled = true, AutovalidateMode? autovalidateMode, String? restorationId})
```

创建单个表单字段。

### builder

```dart
FormFieldBuilder<T> builder
```

返回表示此表单字段的 widget 的函数。

调用时会传入表单字段状态作为输入，其中包含该字段的当前值和验证状态。

### onSaved

```dart
FormFieldSetter<T>? onSaved
```

一个可选方法，在通过 [FormState.save] 保存表单时以最终值调用。

### onReset

```dart
VoidCallback? onReset
```

一个可选方法，在通过 [FormFieldState.reset] 重置表单字段时调用。

### forceErrorText

```dart
String? forceErrorText
```

一个可选属性，通过直接设置 [FormFieldState.errorText] 属性（而不运行验证函数），强制将 [FormFieldState](https://www.yuque.com/thyname/flutter.widgets/formfieldstate) 置于错误状态。

当提供 [forceErrorText] 属性时，[FormFieldState.errorText] 将被设置为所提供的值，从而使表单字段被视为无效，并显示指定的错误消息。

如果同时提供了 [validator]，[forceErrorText] 将覆盖其返回的任何错误。只有当 [forceErrorText] 为 null 时才会调用 [validator]。

另请参阅：

- [InputDecoration.errorText]，用于在文本字段的装饰中显示错误消息，而不影响该字段的状态。当 [forceErrorText] 不为 null 时，它将覆盖 [InputDecoration.errorText] 的值。

### validator

```dart
FormFieldValidator<T>? validator
```

一个可选方法，用于验证输入。如果输入无效则返回要显示的错误字符串，否则返回 null。

返回值通过 [FormFieldState.errorText] 属性公开。[TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield) 使用此值来覆盖 [InputDecoration.errorText] 的值。

在错误状态和正常状态之间切换可能导致 [TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield) 的高度发生变化（如果该字段未设置其他子文本装饰）。若要创建一个高度固定、不受错误显示与否影响的字段，可以将 [TextFormField](https://www.yuque.com/thyname/flutter.material/textformfield) 包装在诸如 [SizedBox](https://www.yuque.com/thyname/flutter.widgets/sizedbox) 之类的固定高度父级中，或者将 [InputDecoration.helperText] 参数设置为一个空格。

### errorBuilder

```dart
FormFieldErrorBuilder? errorBuilder
```

返回表示要显示的错误的 widget 的函数。

调用时会传入表单字段验证器的错误字符串作为输入。所生成的 widget 会传递给 [InputDecoration.error]。

如果为 null，则验证器的错误字符串会传递给 [InputDecoration.errorText]。

### initialValue

```dart
T? initialValue
```

用于初始化表单字段的可选值，否则为 null。

`initialValue` 会在以下两种情况下影响表单字段的状态：

1.  首次构建表单字段时，`initialValue` 决定该字段的初始状态。
2.  调用 [FormFieldState.reset]（无论是直接调用还是通过调用 [FormFieldState.reset]）时，表单字段会被重置为此 `initialValue`。

### enabled

```dart
bool enabled
```

表单是否能够接收用户输入。

默认为 true。如果 [autovalidateMode] 不为 [AutovalidateMode.disabled]，则该字段将被自动验证。同样，如果此字段为 false，则无论 [autovalidateMode] 为何值，该 widget 都不会被验证。

### autovalidateMode

```dart
AutovalidateMode autovalidateMode
```

用于启用/禁用此表单字段的自动验证并更新其错误文本。

{@template flutter.widgets.FormField.autovalidateMode} 如果为 [AutovalidateMode.onUserInteraction]，此 FormField 只会在其内容发生变化后自动验证。如果为 [AutovalidateMode.always]，即使没有用户交互也会自动验证。如果为 [AutovalidateMode.disabled]，则禁用自动验证。

默认为 [AutovalidateMode.disabled]。{@endtemplate}

### restorationId

```dart
String? restorationId
```

用于保存和恢复表单字段状态的恢复 ID。

将恢复 ID 设置为非 null 值将决定该表单字段的验证是否会被保留。

此 widget 的状态会使用提供的恢复 ID，保存在通过周围 [RestorationScope](https://www.yuque.com/thyname/flutter.widgets/restorationscope) 获取的 [RestorationBucket](https://www.yuque.com/thyname/flutter.services/restorationbucket) 中。

另请参阅：

- [RestorationManager](https://www.yuque.com/thyname/flutter.services/restorationmanager)，其中说明了 Flutter 中状态恢复的工作原理。

### createState()

```dart
FormFieldState<T> createState()
```

# FormFieldState

```dart
class FormFieldState<T> extends State<FormField<T>> with RestorationMixin {}
```

[FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 的当前状态。传递给 [FormFieldBuilder](https://www.yuque.com/thyname/flutter.widgets/formfieldbuilder) 方法，用于构建表单字段的 widget。

### value

```dart
T? get value
```

表单字段的当前值。

### errorText

```dart
String? get errorText
```

由 [FormField.validator] 回调返回的当前验证错误，或通过 [FormField.forceErrorText] 属性手动提供的错误消息。

当调用 [validate] 并触发 [FormField.validator] 回调时，或者当 [FormField.forceErrorText] 被直接设置为非 null 值时，此属性会自动更新。

### hasError

```dart
bool get hasError
```

如果此字段存在任何验证错误，则为 true。

### hasInteractedByUser

```dart
bool get hasInteractedByUser
```

如果用户已修改此字段的值，则返回 true。

只有在调用 [didChange] 后才会更新为 true，并在调用 [reset] 时重置为 false。

### isValid

```dart
bool get isValid
```

如果当前值有效，则为 true。

这不会设置 [errorText] 或 [hasError]，也不会更新错误显示。

另请参阅：

- [validate]，可能会更新 [errorText] 和 [hasError]。

- [FormField.forceErrorText]，同样可能更新 [errorText] 和 [hasError]。

### save()

```dart
void save()
```

以当前值调用该 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 的 onSaved 方法。

### reset()

```dart
void reset()
```

将字段重置为其初始值。

### clearError()

```dart
void clearError()
```

清除此字段的任何可见验证错误，但不会重置字段的值。

这会将 [errorText] 设置为 null，并将 [hasInteractedByUser] 设置为 false。

如果使用了 [AutovalidateMode.always]，由于该字段会在下一次构建期间触发新的验证周期，错误可能会立即重新出现。另请参阅：

- [FormState.clearError]，用于清除表单中所有字段的错误。

### validate()

```dart
bool validate()
```

仅当 [FormField.forceErrorText] 为 null 时，调用 [FormField.validator] 来设置 [errorText]。当 [FormField.forceErrorText] 不为 null 时，不会调用 [FormField.validator]。

如果没有错误则返回 true。另请参阅：

- [isValid]，被动获取有效性，而不设置 [errorText] 或 [hasError]。

### didChange()

```dart
void didChange(T? value)
```

将此字段的状态更新为新值。可用于响应子 widget 的变化，例如 [Slider](https://www.yuque.com/thyname/flutter.material/slider) 的 [Slider.onChanged] 参数。

触发 [Form.onChanged] 回调；如果 [Form.autovalidateMode] 为 [AutovalidateMode.always] 或 [AutovalidateMode.onUserInteraction]，还会重新验证表单的所有字段。

### setValue()

```dart
void setValue(T? value)
```

设置与此表单字段关联的值。

此方法只应由子类调用，用于在 widget 构建阶段（此时禁止调用 `setState`）响应状态变化而更新表单字段的值。在所有其他情况下，应通过调用 [didChange] 来设置值，以确保调用 `setState`。

### restorationId

```dart
String? get restorationId
```

### restoreState()

```dart
void restoreState(RestorationBucket? oldBucket, bool initialRestore)
```

### deactivate()

```dart
void deactivate()
```

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(FormField<T> oldWidget)
```

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

# AutovalidateMode

```dart
enum AutovalidateMode {}
```

用于配置 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield) 和 [Form](https://www.yuque.com/thyname/flutter.widgets/form) widget 的自动验证。

不会进行自动验证。

用于在没有用户交互的情况下自动验证 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 和 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)。

用于仅在每次用户交互后自动验证 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 和 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)。

用于仅在字段失去焦点后自动验证 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 和 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)。

如果希望在用户与某个字段发生首次交互后验证 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的所有字段，请改用 [always]。

用于在每次用户交互后自动验证 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 和 [FormField](https://www.yuque.com/thyname/flutter.widgets/formfield)，但仅在该字段已存在错误时进行。

这有助于减少不必要的验证调用，同时仍能确保在用户尝试修复错误时重新检查错误。
