@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/services.dart';

# Form

```dart
class Form extends StatefulWidget {}
```

An optional container for grouping together multiple form field widgets (e.g. [TextField] widgets).

Each individual form field should be wrapped in a [FormField] widget, with the [Form] widget as a common ancestor of all of those. Call methods on [FormState] to save, reset, or validate each [FormField] that is a descendant of this [Form]. To obtain the [FormState], you may use [Form.of] with a context whose ancestor is the [Form], or pass a [GlobalKey] to the [Form] constructor and call [GlobalKey.currentState].

{@tool dartpad} This example shows a [Form] with one [TextFormField] to enter an email address and an [ElevatedButton] to submit the form. A [GlobalKey] is used here to identify the [Form] and validate input.

![](https://flutter.github.io/assets-for-api-docs/assets/widgets/form.png)

** See code in examples/api/lib/widgets/form/form.0.dart ** {@end-tool}

See also:

- [GlobalKey], a key that is unique across the entire app.
- [FormField], a single form field widget that maintains the current state.
- [TextFormField], a convenience widget that wraps a [TextField] widget in a [FormField].

### Form()

```dart
Form({dynamic key, required Widget child, bool? canPop, PopInvokedCallback? onPopInvoked, PopInvokedWithResultCallback<Object?>? onPopInvokedWithResult, WillPopCallback? onWillPop, VoidCallback? onChanged, AutovalidateMode? autovalidateMode})
```

Creates a container for form fields.

### maybeOf()

```dart
FormState? maybeOf(BuildContext context)
```

Returns the [FormState] of the closest [Form] widget which encloses the given context, or null if none is found.

Typical usage is as follows:

```dart
FormState? form = Form.maybeOf(context);
form?.save();
```

Calling this method will create a dependency on the closest [Form] in the [context], if there is one.

See also:

- [Form.of], which is similar to this method, but asserts if no [Form] ancestor is found.

### of()

```dart
FormState of(BuildContext context)
```

Returns the [FormState] of the closest [Form] widget which encloses the given context.

Typical usage is as follows:

```dart
FormState form = Form.of(context);
form.save();
```

If no [Form] ancestor is found, this will assert in debug mode, and throw an exception in release mode.

Calling this method will create a dependency on the closest [Form] in the [context].

See also:

- [Form.maybeOf], which is similar to this method, but returns null if no [Form] ancestor is found.

### child

```dart
Widget child
```

The widget below this widget in the tree.

This is the root of the widget hierarchy that contains this form.

{@macro flutter.widgets.ProxyWidget.child}

### onWillPop

```dart
WillPopCallback? onWillPop
```

Enables the form to veto attempts by the user to dismiss the [ModalRoute] that contains the form.

If the callback returns a Future that resolves to false, the form's route will not be popped.

See also:

- [WillPopScope], another widget that provides a way to intercept the back button.

### canPop

```dart
bool? canPop
```

{@macro flutter.widgets.PopScope.canPop}

{@tool dartpad} This sample demonstrates how to use this parameter to show a confirmation dialog when a navigation pop would cause form data to be lost.

** See code in examples/api/lib/widgets/form/form.1.dart ** {@end-tool}

See also:

- [onPopInvokedWithResult], which also comes from [PopScope] and is often used in conjunction with this parameter.
- [PopScope.canPop], which is what [Form] delegates to internally.

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

{@tool dartpad} This sample demonstrates how to use this parameter to show a confirmation dialog when a navigation pop would cause form data to be lost.

** See code in examples/api/lib/widgets/form/form.1.dart ** {@end-tool}

See also:

- [canPop], which also comes from [PopScope] and is often used in conjunction with this parameter.
- [PopScope.onPopInvokedWithResult], which is what [Form] delegates to internally.

### onChanged

```dart
VoidCallback? onChanged
```

Called when one of the form fields changes.

In addition to this callback being invoked, all the form fields themselves will rebuild.

### autovalidateMode

```dart
AutovalidateMode autovalidateMode
```

Used to enable/disable form fields auto validation and update their error text.

{@macro flutter.widgets.FormField.autovalidateMode}

### createState()

```dart
FormState createState()
```

# FormState

```dart
class FormState extends State<Form> {}
```

State associated with a [Form] widget.

A [FormState] object can be used to [save], [reset], and [validate] every [FormField] that is a descendant of the associated [Form].

Typically obtained via [Form.of].

### fields

```dart
Iterable<FormFieldState<dynamic>> get fields
```

The [FormFieldState] objects that are currently registered with this [Form].

### build()

```dart
Widget build(BuildContext context)
```

### save()

```dart
void save()
```

Saves every [FormField] that is a descendant of this [Form].

### reset()

```dart
void reset()
```

Resets every [FormField] that is a descendant of this [Form] back to its [FormField.initialValue].

The [Form.onChanged] callback will be called.

If the form's [Form.autovalidateMode] property is [AutovalidateMode.always], the fields will all be revalidated after being reset.

### clearError()

```dart
void clearError()
```

Clears the validation errors for all [FormField]s in this [Form] without resetting their values.

See also:

- [FormFieldState.clearError], which clears the error for a single form field.

### validate()

```dart
bool validate()
```

Validates every [FormField] that is a descendant of this [Form], and returns true if there are no errors.

The form will rebuild to report the results.

See also:

- [validateGranularly], which also validates descendant [FormField]s, but instead returns a [Set] of fields with errors.

### validateGranularly()

```dart
Set<FormFieldState<Object?>> validateGranularly()
```

Validates every [FormField] that is a descendant of this [Form], and returns a [Set] of [FormFieldState] of the invalid field(s) only, if any.

This method can be useful to highlight field(s) with errors.

The form will rebuild to report the results.

See also:

- [validate], which also validates descendant [FormField]s, and return true if there are no errors.

# FormFieldValidator

```dart
typedef FormFieldValidator<T> = String? Function(T? value)
```

Signature for validating a form field.

Returns an error string to display if the input is invalid, or null otherwise.

Used by [FormField.validator].

# FormFieldErrorBuilder

```dart
typedef FormFieldErrorBuilder = Widget Function(BuildContext context, String errorText)
```

Signature for a callback that builds an error widget.

See also:

- [FormField.errorBuilder], which is of this type, and passes the result error given by [TextFormField.validator].

# FormFieldSetter

```dart
typedef FormFieldSetter<T> = void Function(T? newValue)
```

Signature for being notified when a form field changes value.

Used by [FormField.onSaved].

# FormFieldBuilder

```dart
typedef FormFieldBuilder<T> = Widget Function(FormFieldState<T> field)
```

Signature for building the widget representing the form field.

Used by [FormField.builder].

# FormField

```dart
class FormField<T> extends StatefulWidget {}
```

A single form field.

This widget maintains the current state of the form field, so that updates and validation errors are visually reflected in the UI.

When used inside a [Form], you can use methods on [FormState] to query or manipulate the form data as a whole. For example, calling [FormState.save] will invoke each [FormField]'s [onSaved] callback in turn.

Use a [GlobalKey] with [FormField] if you want to retrieve its current state, for example if you want one form field to depend on another.

A [Form] ancestor is not required. The [Form] allows one to save, reset, or validate multiple fields at once. To use without a [Form], pass a [GlobalKey] to the constructor and use [GlobalKey.currentState] to save or reset the form field.

See also:

- [Form], which is the widget that aggregates the form fields.
- [TextField], which is a commonly used form field for entering text.

### FormField()

```dart
FormField({dynamic key, required FormFieldBuilder<T> builder, FormFieldSetter<T>? onSaved, VoidCallback? onReset, String? forceErrorText, FormFieldValidator<T>? validator, FormFieldErrorBuilder? errorBuilder, T? initialValue, bool enabled = true, AutovalidateMode? autovalidateMode, String? restorationId})
```

Creates a single form field.

### builder

```dart
FormFieldBuilder<T> builder
```

Function that returns the widget representing this form field.

It is passed the form field state as input, containing the current value and validation state of this field.

### onSaved

```dart
FormFieldSetter<T>? onSaved
```

An optional method to call with the final value when the form is saved via [FormState.save].

### onReset

```dart
VoidCallback? onReset
```

An optional method to call when the form field is reset via [FormFieldState.reset].

### forceErrorText

```dart
String? forceErrorText
```

An optional property that forces the [FormFieldState] into an error state by directly setting the [FormFieldState.errorText] property without running the validator function.

When the [forceErrorText] property is provided, the [FormFieldState.errorText] will be set to the provided value, causing the form field to be considered invalid and to display the error message specified.

When [validator] is provided, [forceErrorText] will override any error that it returns. [validator] will not be called unless [forceErrorText] is null.

See also:

- [InputDecoration.errorText], which is used to display error messages in the text field's decoration without effecting the field's state. When [forceErrorText] is not null, it will override [InputDecoration.errorText] value.

### validator

```dart
FormFieldValidator<T>? validator
```

An optional method that validates an input. Returns an error string to display if the input is invalid, or null otherwise.

The returned value is exposed by the [FormFieldState.errorText] property. The [TextFormField] uses this to override the [InputDecoration.errorText] value.

Alternating between error and normal state can cause the height of the [TextFormField] to change if no other subtext decoration is set on the field. To create a field whose height is fixed regardless of whether or not an error is displayed, either wrap the [TextFormField] in a fixed height parent like [SizedBox], or set the [InputDecoration.helperText] parameter to a space.

### errorBuilder

```dart
FormFieldErrorBuilder? errorBuilder
```

Function that returns the widget representing the error to display.

It is passed the form field validator error string as input. The resulting widget is passed to [InputDecoration.error].

If null, the validator error string is passed to [InputDecoration.errorText].

### initialValue

```dart
T? initialValue
```

An optional value to initialize the form field to, or null otherwise.

The `initialValue` affects the form field's state in two cases:

1.  When the form field is first built, `initialValue` determines the field's initial state.
2.  When [FormFieldState.reset] is called (either directly or by calling [FormFieldState.reset]), the form field is reset to this `initialValue`.

### enabled

```dart
bool enabled
```

Whether the form is able to receive user input.

Defaults to true. If [autovalidateMode] is not [AutovalidateMode.disabled], the field will be auto validated. Likewise, if this field is false, the widget will not be validated regardless of [autovalidateMode].

### autovalidateMode

```dart
AutovalidateMode autovalidateMode
```

Used to enable/disable this form field auto validation and update its error text.

{@template flutter.widgets.FormField.autovalidateMode} If [AutovalidateMode.onUserInteraction], this FormField will only auto-validate after its content changes. If [AutovalidateMode.always], it will auto-validate even without user interaction. If [AutovalidateMode.disabled], auto-validation will be disabled.

Defaults to [AutovalidateMode.disabled]. {@endtemplate}

### restorationId

```dart
String? restorationId
```

Restoration ID to save and restore the state of the form field.

Setting the restoration ID to a non-null value results in whether or not the form field validation persists.

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter.

### createState()

```dart
FormFieldState<T> createState()
```

# FormFieldState

```dart
class FormFieldState<T> extends State<FormField<T>> with RestorationMixin {}
```

The current state of a [FormField]. Passed to the [FormFieldBuilder] method for use in constructing the form field's widget.

### value

```dart
T? get value
```

The current value of the form field.

### errorText

```dart
String? get errorText
```

The current validation error returned by the [FormField.validator] callback, or the manually provided error message using the [FormField.forceErrorText] property.

This property is automatically updated when [validate] is called and the [FormField.validator] callback is invoked, or If [FormField.forceErrorText] is set directly to a non-null value.

### hasError

```dart
bool get hasError
```

True if this field has any validation errors.

### hasInteractedByUser

```dart
bool get hasInteractedByUser
```

Returns true if the user has modified the value of this field.

This only updates to true once [didChange] has been called and resets to false when [reset] is called.

### isValid

```dart
bool get isValid
```

True if the current value is valid.

This will not set [errorText] or [hasError] and it will not update error display.

See also:

- [validate], which may update [errorText] and [hasError].

- [FormField.forceErrorText], which also may update [errorText] and [hasError].

### save()

```dart
void save()
```

Calls the [FormField]'s onSaved method with the current value.

### reset()

```dart
void reset()
```

Resets the field to its initial value.

### clearError()

```dart
void clearError()
```

Clears any visible validation error for this field without resetting the field's value.

This sets [errorText] to null and [hasInteractedByUser] to false.

If [AutovalidateMode.always] is used, the error may reappear immediately because the field will trigger a new validation cycle during the next build. See also:

- [FormState.clearError], which clears errors across all fields in the form.

### validate()

```dart
bool validate()
```

Calls [FormField.validator] to set the [errorText] only if [FormField.forceErrorText] is null. When [FormField.forceErrorText] is not null, [FormField.validator] will not be called.

Returns true if there were no errors. See also:

- [isValid], which passively gets the validity without setting [errorText] or [hasError].

### didChange()

```dart
void didChange(T? value)
```

Updates this field's state to the new value. Useful for responding to child widget changes, e.g. [Slider]'s [Slider.onChanged] argument.

Triggers the [Form.onChanged] callback and, if [Form.autovalidateMode] is [AutovalidateMode.always] or [AutovalidateMode.onUserInteraction], revalidates all the fields of the form.

### setValue()

```dart
void setValue(T? value)
```

Sets the value associated with this form field.

This method should only be called by subclasses that need to update the form field value due to state changes identified during the widget build phase, when calling `setState` is prohibited. In all other cases, the value should be set by a call to [didChange], which ensures that `setState` is called.

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

Used to configure the auto validation of [FormField] and [Form] widgets.

No auto validation will occur.

Used to auto-validate [Form] and [FormField] even without user interaction.

Used to auto-validate [Form] and [FormField] only after each user interaction.

Used to auto-validate [Form] and [FormField] only after the field has lost focus.

In order to validate all fields of a [Form] after the first time the user interacts with one, use [always] instead.

Used to auto-validate [Form] and [FormField] after each user interaction, only if the field already has an error.

This is useful for reducing unnecessary validation calls while still ensuring errors are re-checked when the user attempts to fix them.
