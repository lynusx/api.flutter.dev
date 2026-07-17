@docImport 'editable_text.dart'; @docImport 'form.dart'; @docImport 'scrollable.dart';

# AutofillContextAction

```dart
enum AutofillContextAction {}
```

预定义的自动填充上下文清理操作。

在通知平台保存其中的用户输入后，销毁当前的自动填充上下文。

对应于以 `shouldSave == true` 调用 [TextInput.finishAutofillContext]。

在不保存用户输入的情况下销毁当前的自动填充上下文。

对应于以 `shouldSave == false` 调用 [TextInput.finishAutofillContext]。

# AutofillGroup

```dart
class AutofillGroup extends StatefulWidget {}
```

将多个 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient) 组合在一起的 [AutofillScope](https://www.yuque.com/thyname/flutter.services/autofillscope) 组件。

共享同一个最近的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 祖先的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient) 必须一起构建，它们也会被一起自动填充。

{@macro flutter.services.AutofillScope}

[AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 组件只会识别通过 [AutofillGroupState.register] API 注册到它的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)。通常，[AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 不会识别未挂载的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)，例如位于从未被滚动进视口的 [Scrollable](https://www.yuque.com/thyname/flutter.widgets/scrollable) 内部的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)。要解决此问题，应确保同一个 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 中的客户端一起构建。

最顶层的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 组件（即最接近根组件的那些）可用于在当前自动填充上下文不再相关时对其进行清理。

{@macro flutter.services.TextInput.finishAutofillContext}

默认情况下，[onDisposeAction] 被设置为 [AutofillContextAction.commit]，在这种情况下，当任何一个最顶层的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 被释放时，会通知平台保存当前自动填充上下文中的用户输入，然后销毁当前的自动填充上下文以释放资源。例如，你可以用 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 包装一个包含大量可自动填充输入字段的 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的路由，这样 [Form](https://www.yuque.com/thyname/flutter.widgets/form) 的用户输入就可以被保存，供平台以后自动填充使用。

{@tool dartpad} 一个示例表单，其中的可自动填充字段被分组到不同的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 中。

** 请参阅 examples/api/lib/widgets/autofill/autofill_group.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [AutofillContextAction](https://www.yuque.com/thyname/flutter.widgets/autofillcontextaction)，一个枚举，包含在最顶层 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 被释放时要执行的预定义自动填充上下文清理操作。

### AutofillGroup()

```dart
AutofillGroup({dynamic key, required Widget child, AutofillContextAction onDisposeAction = AutofillContextAction.commit})
```

为可自动填充的输入字段创建一个作用域。

### maybeOf()

```dart
AutofillGroupState? maybeOf(BuildContext context)
```

返回包含给定上下文的最近 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 组件的 [AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate)；若找不到，则返回 null。

若 [context] 中存在最近的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup)，调用此方法将对其创建依赖关系。

{@macro flutter.widgets.AutofillGroupState}

另请参阅：

- [AutofillGroup.of]，与此方法类似，但若找不到 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 则会触发断言。
- [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate)，其中使用此方法来获取最近的 [AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate)。

### of()

```dart
AutofillGroupState of(BuildContext context)
```

返回包含给定上下文的最近 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 组件的 [AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate)。

若找不到实例，此方法会在调试模式下触发断言，并在发布模式下抛出异常。

调用此方法将对 [context] 中最近的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 创建依赖关系。

{@macro flutter.widgets.AutofillGroupState}

另请参阅：

- [AutofillGroup.maybeOf]，与此方法类似，但若找不到 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 则返回 null。
- [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate)，其中使用此方法来获取最近的 [AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate)。

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### onDisposeAction

```dart
AutofillContextAction onDisposeAction
```

当此 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 是最顶层的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 且正被释放时，为清理当前自动填充上下文而要执行的 [AutofillContextAction](https://www.yuque.com/thyname/flutter.widgets/autofillcontextaction)。

{@macro flutter.services.TextInput.finishAutofillContext}

默认为 [AutofillContextAction.commit]，它会提示平台保存用户输入并销毁当前的自动填充上下文。

# AutofillGroupState

```dart
class AutofillGroupState extends State<AutofillGroup> with AutofillScopeMixin {}
```

与 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 组件关联的 State。

{@template flutter.widgets.AutofillGroupState} [AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate) 可用于在 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient) 进入此 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 时注册它（例如，当 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 被挂载或重新挂载到 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 的子树上时），并在其退出时取消注册（例如，当 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext) 被卸载或从 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 的子树中重新挂载出去时）。

[AutofillGroupState](https://www.yuque.com/thyname/flutter.widgets/autofillgroupstate) 类还提供了一个 [AutofillGroupState.attach] 方法，支持自动填充的 [TextInputClient](https://www.yuque.com/thyname/flutter.services/textinputclient) 可以调用它（而非 [TextInput.attach]）来创建一个 [TextInputConnection](https://www.yuque.com/thyname/flutter.services/textinputconnection)，以便与平台的文本输入系统进行交互。{@endtemplate}

通常通过 [AutofillGroup.of] 获取。

### register()

```dart
void register(AutofillClient client)
```

将 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient) 添加到此 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup)。

通常，当输入字段应注册到新的 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 时，此方法会由支持自动填充的 [TextInputClient](https://www.yuque.com/thyname/flutter.services/textinputclient)（例如 [EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate)）在 [State.didChangeDependencies] 中调用。

另请参阅：

- [EditableTextState.didChangeDependencies]，其中在需要时会调用此方法来更新当前的 [AutofillScope](https://www.yuque.com/thyname/flutter.services/autofillscope)。

### unregister()

```dart
void unregister(String autofillId)
```

从此 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 中移除具有给定 `autofillId` 的 [AutofillClient](https://www.yuque.com/thyname/flutter.services/autofillclient)。

通常，此方法应在文本字段被释放时，或在其注册到另一个 [AutofillGroup](https://www.yuque.com/thyname/flutter.widgets/autofillgroup) 之前，由该文本字段调用。

另请参阅：

- [EditableTextState.didChangeDependencies]，其中会调用此方法从之前的 [AutofillScope](https://www.yuque.com/thyname/flutter.services/autofillscope) 取消注册。
- [EditableTextState.dispose]，其中当组件即将从树中移除时，会调用此方法从当前的 [AutofillScope](https://www.yuque.com/thyname/flutter.services/autofillscope) 取消注册。
