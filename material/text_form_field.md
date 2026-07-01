# TextFormField

```dart
class TextFormField extends FormField<String> {}
```

A [FormField] that contains a [TextField].

This is a convenience widget that wraps a [TextField] widget in a [FormField].

A [Form] ancestor is not required. The [Form] allows one to save, reset, or validate multiple fields at once. To use without a [Form], pass a `GlobalKey<FormFieldState>` (see [GlobalKey]) to the constructor and use [GlobalKey.currentState] to save or reset the form field.

When a [controller] is specified, its [TextEditingController.text] defines the [initialValue]. If this [FormField] is part of a scrolling container that lazily constructs its children, like a [ListView] or a [CustomScrollView], then a [controller] should be specified. The controller's lifetime should be managed by a stateful widget ancestor of the scrolling container.

If a [controller] is not specified, [initialValue] can be used to give the automatically generated controller an initial value.

{@macro flutter.material.textfield.wantKeepAlive}

Remember to call [TextEditingController.dispose] of the [TextEditingController] when it is no longer needed. This will ensure any resources used by the object are discarded.

By default, `decoration` will apply the ambient [InputDecorationThemeData] for the current context to the [InputDecoration], see [InputDecoration.applyDefaults].

For a documentation about the various parameters, see [TextField].

{@tool snippet}

Creates a [TextFormField] with an [InputDecoration] and validator function.

![If the user enters valid text, the TextField appears normally without any warnings to the user](https://flutter.github.io/assets-for-api-docs/assets/material/text_form_field.png)

![If the user enters invalid text, the error message returned from the validator function is displayed in dark red underneath the input](https://flutter.github.io/assets-for-api-docs/assets/material/text_form_field_error.png)

```dart
TextFormField(
  decoration: const InputDecoration(
    icon: Icon(Icons.person),
    hintText: 'What do people call you?',
    labelText: 'Name *',
  ),
  onSaved: (String? value) {
    // This optional block of code can be used to run
    // code when the user saves the form.
  },
  validator: (String? value) {
    return (value != null && value.contains('@')) ? 'Do not use the @ char.' : null;
  },
)
```

{@end-tool}

{@tool dartpad} This example shows how to move the focus to the next field when the user presses the SPACE key.

** See code in examples/api/lib/material/text_form_field/text_form_field.1.dart ** {@end-tool}

{@tool dartpad} This example shows how to force an error text to the field after making an asynchronous call.

** See code in examples/api/lib/material/text_form_field/text_form_field.2.dart ** {@end-tool}

See also:

- <https://material.io/design/components/text-fields.html>
- [TextField], which is the underlying text field without the [Form] integration.
- [InputDecorator], which shows the labels and other visual elements that surround the actual text editing widget.
- Learn how to use a [TextEditingController] in one of our [cookbook recipes](https://docs.flutter.dev/cookbook/forms/text-field-changes#2-use-a-texteditingcontroller).

### TextFormField()

```dart
TextFormField({dynamic key, Object groupId = EditableText, TextEditingController? controller, String? initialValue, FocusNode? focusNode, dynamic forceErrorText, InputDecoration? decoration = const InputDecoration(), TextInputType? keyboardType, TextCapitalization textCapitalization = TextCapitalization.none, TextInputAction? textInputAction, TextStyle? style, StrutStyle? strutStyle, TextDirection? textDirection, TextAlign textAlign = TextAlign.start, TextAlignVertical? textAlignVertical, bool autofocus = false, bool readOnly = false, ToolbarOptions? toolbarOptions, bool? showCursor, String obscuringCharacter = '•', bool obscureText = false, bool autocorrect = true, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, MaxLengthEnforcement? maxLengthEnforcement, int? maxLines = 1, int? minLines, bool expands = false, int? maxLength, ValueChanged<String>? onChanged, GestureTapCallback? onTap, bool onTapAlwaysCalled = false, TapRegionCallback? onTapOutside, TapRegionUpCallback? onTapUpOutside, VoidCallback? onEditingComplete, ValueChanged<String>? onFieldSubmitted, dynamic onSaved, dynamic validator, dynamic errorBuilder, List<TextInputFormatter>? inputFormatters, bool? enabled, bool? ignorePointers, double cursorWidth = 2.0, double? cursorHeight, Radius? cursorRadius, Color? cursorColor, Color? cursorErrorColor, Brightness? keyboardAppearance, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), bool? enableInteractiveSelection, bool? selectAllOnFocus, TextSelectionControls? selectionControls, InputCounterWidgetBuilder? buildCounter, ScrollPhysics? scrollPhysics, Iterable<String>? autofillHints, AutovalidateMode? autovalidateMode, ScrollController? scrollController, dynamic restorationId, bool enableIMEPersonalizedLearning = true, MouseCursor? mouseCursor, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, SpellCheckConfiguration? spellCheckConfiguration, TextMagnifierConfiguration? magnifierConfiguration, UndoHistoryController? undoController, AppPrivateCommandCallback? onAppPrivateCommand, bool? cursorOpacityAnimates, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ContentInsertionConfiguration? contentInsertionConfiguration, MaterialStatesController? statesController, Clip clipBehavior = Clip.hardEdge, bool scribbleEnabled = true, bool stylusHandwritingEnabled = EditableText.defaultStylusHandwritingEnabled, bool canRequestFocus = true, List<Locale>? hintLocales})
```

Creates a [FormField] that contains a [TextField].

When a [controller] is specified, [initialValue] must be null (the default). If [controller] is null, then a [TextEditingController] will be constructed automatically and its `text` will be initialized to [initialValue] or the empty string.

For documentation about the various parameters, see the [TextField] class and [TextField.new], the constructor.

### controller

```dart
TextEditingController? controller
```

Controls the text being edited.

If null, this widget will create its own [TextEditingController] and initialize its [TextEditingController.text] with [initialValue].

### groupId

```dart
Object groupId
```

{@macro flutter.widgets.editableText.groupId}

### onChanged

```dart
ValueChanged<String>? onChanged
```

{@template flutter.material.TextFormField.onChanged} Called when the user initiates a change to the TextField's value: when they have inserted or deleted text or reset the form. {@endtemplate}

### createState()

```dart
FormFieldState<String> createState()
```
