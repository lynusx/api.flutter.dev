@docImport 'editable_text.dart'; @docImport 'form.dart'; @docImport 'scrollable.dart';

# AutofillContextAction

```dart
enum AutofillContextAction {}
```

Predefined autofill context clean up actions.

Destroys the current autofill context after informing the platform to save the user input from it.

Corresponds to calling [TextInput.finishAutofillContext] with `shouldSave == true`.

Destroys the current autofill context without saving the user input.

Corresponds to calling [TextInput.finishAutofillContext] with `shouldSave == false`.

# AutofillGroup

```dart
class AutofillGroup extends StatefulWidget {}
```

An [AutofillScope] widget that groups [AutofillClient]s together.

[AutofillClient]s that share the same closest [AutofillGroup] ancestor must be built together, and they will be autofilled together.

{@macro flutter.services.AutofillScope}

The [AutofillGroup] widget only knows about [AutofillClient]s registered to it using the [AutofillGroupState.register] API. Typically, [AutofillGroup] will not pick up [AutofillClient]s that are not mounted, for example, an [AutofillClient] within a [Scrollable] that has never been scrolled into the viewport. To workaround this problem, ensure clients in the same [AutofillGroup] are built together.

The topmost [AutofillGroup] widgets (the ones that are closest to the root widget) can be used to clean up the current autofill context when the current autofill context is no longer relevant.

{@macro flutter.services.TextInput.finishAutofillContext}

By default, [onDisposeAction] is set to [AutofillContextAction.commit], in which case when any of the topmost [AutofillGroup]s is being disposed, the platform will be informed to save the user input from the current autofill context, then the current autofill context will be destroyed, to free resources. You can, for example, wrap a route that contains a [Form] full of autofillable input fields in an [AutofillGroup], so the user input of the [Form] can be saved for future autofill by the platform.

{@tool dartpad} An example form with autofillable fields grouped into different [AutofillGroup]s.

** See code in examples/api/lib/widgets/autofill/autofill_group.0.dart ** {@end-tool}

See also:

- [AutofillContextAction], an enum that contains predefined autofill context clean up actions to be run when a topmost [AutofillGroup] is disposed.

### AutofillGroup()

```dart
AutofillGroup({dynamic key, required Widget child, AutofillContextAction onDisposeAction = AutofillContextAction.commit})
```

Creates a scope for autofillable input fields.

### maybeOf()

```dart
AutofillGroupState? maybeOf(BuildContext context)
```

Returns the [AutofillGroupState] of the closest [AutofillGroup] widget which encloses the given context, or null if one cannot be found.

Calling this method will create a dependency on the closest [AutofillGroup] in the [context], if there is one.

{@macro flutter.widgets.AutofillGroupState}

See also:

- [AutofillGroup.of], which is similar to this method, but asserts if an [AutofillGroup] cannot be found.
- [EditableTextState], where this method is used to retrieve the closest [AutofillGroupState].

### of()

```dart
AutofillGroupState of(BuildContext context)
```

Returns the [AutofillGroupState] of the closest [AutofillGroup] widget which encloses the given context.

If no instance is found, this method will assert in debug mode and throw an exception in release mode.

Calling this method will create a dependency on the closest [AutofillGroup] in the [context].

{@macro flutter.widgets.AutofillGroupState}

See also:

- [AutofillGroup.maybeOf], which is similar to this method, but returns null if an [AutofillGroup] cannot be found.
- [EditableTextState], where this method is used to retrieve the closest [AutofillGroupState].

### child

```dart
Widget child
```

{@macro flutter.widgets.ProxyWidget.child}

### onDisposeAction

```dart
AutofillContextAction onDisposeAction
```

The [AutofillContextAction] to be run when this [AutofillGroup] is the topmost [AutofillGroup] and it's being disposed, in order to clean up the current autofill context.

{@macro flutter.services.TextInput.finishAutofillContext}

Defaults to [AutofillContextAction.commit], which prompts the platform to save the user input and destroy the current autofill context.

### createState()

```dart
AutofillGroupState createState()
```

# AutofillGroupState

```dart
class AutofillGroupState extends State<AutofillGroup> with AutofillScopeMixin {}
```

State associated with an [AutofillGroup] widget.

{@template flutter.widgets.AutofillGroupState} An [AutofillGroupState] can be used to register an [AutofillClient] when it enters this [AutofillGroup] (for example, when an [EditableText] is mounted or reparented onto the [AutofillGroup]'s subtree), and unregister an [AutofillClient] when it exits (for example, when an [EditableText] gets unmounted or reparented out of the [AutofillGroup]'s subtree).

The [AutofillGroupState] class also provides an [AutofillGroupState.attach] method that can be called by [TextInputClient]s that support autofill, instead of [TextInput.attach], to create a [TextInputConnection] to interact with the platform's text input system. {@endtemplate}

Typically obtained using [AutofillGroup.of].

### getAutofillClient()

```dart
AutofillClient? getAutofillClient(String autofillId)
```

### autofillClients

```dart
Iterable<AutofillClient> get autofillClients
```

### register()

```dart
void register(AutofillClient client)
```

Adds the [AutofillClient] to this [AutofillGroup].

Typically, this is called by [TextInputClient]s that support autofill (for example, [EditableTextState]) in [State.didChangeDependencies], when the input field should be registered to a new [AutofillGroup].

See also:

- [EditableTextState.didChangeDependencies], where this method is called to update the current [AutofillScope] when needed.

### unregister()

```dart
void unregister(String autofillId)
```

Removes an [AutofillClient] with the given `autofillId` from this [AutofillGroup].

Typically, this should be called by a text field when it's being disposed, or before it's registered with a different [AutofillGroup].

See also:

- [EditableTextState.didChangeDependencies], where this method is called to unregister from the previous [AutofillScope].
- [EditableTextState.dispose], where this method is called to unregister from the current [AutofillScope] when the widget is about to be removed from the tree.

### didChangeDependencies()

```dart
void didChangeDependencies()
```

### build()

```dart
Widget build(BuildContext context)
```

### dispose()

```dart
void dispose()
```
