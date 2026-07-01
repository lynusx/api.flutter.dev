@docImport 'text_theme.dart';

# DropdownMenuFormField

```dart
class DropdownMenuFormField<T> extends FormField<T> {}
```

A [FormField] that contains a [DropdownMenu].

This is a convenience widget that wraps a [DropdownMenu] widget in a [FormField].

A [Form] ancestor is not required. The [Form] allows one to save, reset, or validate multiple fields at once. To use without a [Form], pass a [GlobalKey] to the constructor and use [GlobalKey.currentState] to save or reset the form field.

The `value` parameter maps to [FormField.initialValue].

See also:

- [DropdownMenu], which is the underlying text field without the [Form] integration.

### DropdownMenuFormField()

```dart
DropdownMenuFormField({dynamic key, bool enabled = true, double? width, double? menuHeight, Widget? leadingIcon, Widget? trailingIcon, bool showTrailingIcon = true, FocusNode? trailingIconFocusNode, Widget? label, String? hintText, String? helperText, Widget? selectedTrailingIcon, bool enableFilter = false, bool enableSearch = true, TextInputType? keyboardType, TextStyle? textStyle, TextAlign textAlign = TextAlign.start, Object? inputDecorationTheme, DropdownMenuDecorationBuilder? decorationBuilder, MenuStyle? menuStyle, TextEditingController? controller, T? initialSelection, ValueChanged<T?>? onSelected, FocusNode? focusNode, bool? requestFocusOnTap, bool selectOnly = false, EdgeInsetsGeometry? expandedInsets, Offset? alignmentOffset, FilterCallback<T>? filterCallback, SearchCallback<T>? searchCallback, required List<DropdownMenuEntry<T>> dropdownMenuEntries, List<TextInputFormatter>? inputFormatters, DropdownMenuCloseBehavior closeBehavior = DropdownMenuCloseBehavior.all, int maxLines = 1, TextInputAction? textInputAction, double? cursorHeight, MenuController? menuController, dynamic restorationId, dynamic onSaved, AutovalidateMode autovalidateMode = AutovalidateMode.disabled, dynamic validator, dynamic forceErrorText, dynamic errorBuilder})
```

Creates a [DropdownMenu] widget that is a [FormField].

For a description of the `onSaved`, `validator`, or `autovalidateMode` parameters, see [FormField]. For the rest, see [DropdownMenu].

### onSelected

```dart
ValueChanged<T?>? onSelected
```

The callback is called when a selection is made.

The callback receives the selected entry's value of type `T` when the user chooses an item. It may also be invoked with `null` to indicate that the selection was cleared / that no item was chosen.

Defaults to null. If this callback itself is null, the widget still updates the text field with the selected label.

### controller

```dart
TextEditingController? controller
```

Controls the text being edited.

If null, this widget will create its own [TextEditingController].

### dropdownMenuEntries

```dart
List<DropdownMenuEntry<T>> dropdownMenuEntries
```

Descriptions of the menu items in the [DropdownMenuFormField].

This is a required parameter. It is recommended that at least one [DropdownMenuEntry] is provided. If this is an empty list, the menu will be empty and only contain space for padding.

### createState()

```dart
FormFieldState<T> createState()
```
