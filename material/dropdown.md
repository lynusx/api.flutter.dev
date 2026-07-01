@docImport 'data_table.dart'; @docImport 'dropdown_menu.dart'; @docImport 'elevated_button.dart'; @docImport 'scaffold.dart'; @docImport 'text_button.dart'; @docImport 'text_theme.dart';

# DropdownButtonBuilder

```dart
typedef DropdownButtonBuilder = List<Widget> Function(BuildContext context)
```

A builder to customize dropdown buttons.

Used by [DropdownButton.selectedItemBuilder].

The list of widgets returned by this builder must be exactly the same length as the [DropdownButton.items] list.

# DropdownMenuItem

```dart
class DropdownMenuItem<T> extends _DropdownMenuItemContainer {}
```

An item in a menu created by a [DropdownButton].

The type `T` is the type of the value the entry represents. All the entries in a given menu must represent values with consistent types.

### DropdownMenuItem()

```dart
DropdownMenuItem({dynamic key, VoidCallback? onTap, T? value, bool enabled = true, dynamic alignment, required dynamic child})
```

Creates an item for a dropdown menu.

The [child] argument is required.

### onTap

```dart
VoidCallback? onTap
```

Called when the dropdown menu item is tapped.

### value

```dart
T? value
```

The value to return if the user selects this menu item.

Eventually returned in a call to [DropdownButton.onChanged].

### enabled

```dart
bool enabled
```

Whether or not a user can select this menu item.

Defaults to `true`.

# DropdownButtonHideUnderline

```dart
class DropdownButtonHideUnderline extends InheritedWidget {}
```

An inherited widget that causes any descendant [DropdownButton] widgets to not include their regular underline.

This is used by [DataTable] to remove the underline from any [DropdownButton] widgets placed within material data tables, as required by the Material Design specification.

### DropdownButtonHideUnderline()

```dart
DropdownButtonHideUnderline({dynamic key, required dynamic child})
```

Creates a [DropdownButtonHideUnderline]. A non-null [child] must be given.

### at()

```dart
bool at(BuildContext context)
```

Returns whether the underline of [DropdownButton] widgets should be hidden.

### updateShouldNotify()

```dart
bool updateShouldNotify(DropdownButtonHideUnderline oldWidget)
```

# DropdownButton

```dart
class DropdownButton<T> extends StatefulWidget {}
```

A Material Design button for selecting from a list of items.

A dropdown button lets the user select from a number of items. The button shows the currently selected item as well as an arrow that opens a menu for selecting another item.

## Updating to [DropdownMenu]

There is a Material 3 version of this component, [DropdownMenu] that is preferred for applications that are configured for Material 3 (see [ThemeData.useMaterial3]). The [DropdownMenu] widget's visuals are a little bit different, see the Material 3 spec at <https://m3.material.io/components/menus/guidelines> for more details.

The [DropdownMenu] widget's API is also slightly different. To update from [DropdownButton] to [DropdownMenu], you will need to make the following changes:

1.  Instead of using [DropdownButton.items], which takes a list of [DropdownMenuItem]s, use [DropdownMenu.dropdownMenuEntries], which takes a list of [DropdownMenuEntry]'s.

2.  Instead of using [DropdownButton.onChanged], use [DropdownMenu.onSelected], which is also a callback that is called when the user selects an entry.

3.  In [DropdownMenu] it is not required to track the current selection in your app's state. So, instead of tracking the current selection in the [DropdownButton.value] property, you can set the [DropdownMenu.initialSelection] property to the item that should be selected before there is any user action.

4.  You may also need to make changes to the styling of the [DropdownMenu], see the properties in the [DropdownMenu] constructor for more details.

See the sample below for an example of migrating from [DropdownButton] to [DropdownMenu].

## Using [DropdownButton]

{@youtube 560 315 https://www.youtube.com/watch?v=ZzQ_PWrFihg}

One ancestor must be a [Material] widget and typically this is provided by the app's [Scaffold].

The type `T` is the type of the [value] that each dropdown item represents. All the entries in a given menu must represent values with consistent types. Typically, an enum is used. Each [DropdownMenuItem] in [items] must be specialized with that same type argument.

The [onChanged] callback should update a state variable that defines the dropdown's value. It should also call [State.setState] to rebuild the dropdown with the new value.

{@tool dartpad} This sample shows a [DropdownButton] with a large arrow icon, purple text style, and bold purple underline, whose value is one of "One", "Two", "Three", or "Four".

![](https://flutter.github.io/assets-for-api-docs/assets/material/dropdown_button.png)

** See code in examples/api/lib/material/dropdown/dropdown_button.0.dart ** {@end-tool}

If the [onChanged] callback is null or the list of [items] is null then the dropdown button will be disabled, i.e. its arrow will be displayed in grey and it will not respond to input. A disabled button will display the [disabledHint] widget if it is non-null. However, if [disabledHint] is null and [hint] is non-null, the [hint] widget will instead be displayed.

{@tool dartpad} This sample shows how you would rewrite the above [DropdownButton] to use the [DropdownMenu].

** See code in examples/api/lib/material/dropdown_menu/dropdown_menu.1.dart ** {@end-tool}

See also:

- [DropdownButtonFormField], which integrates with the [Form] widget.
- [DropdownMenuItem], the class used to represent the [items].
- [DropdownButtonHideUnderline], which prevents its descendant dropdown buttons from displaying their underlines.
- [ElevatedButton], [TextButton], ordinary buttons that trigger a single action.
- <https://material.io/design/components/menus.html#dropdown-menu>

### DropdownButton()

```dart
DropdownButton({dynamic key, required List<DropdownMenuItem<T>>? items, DropdownButtonBuilder? selectedItemBuilder, T? value, Widget? hint, Widget? disabledHint, required ValueChanged<T?>? onChanged, VoidCallback? onTap, int elevation = 8, TextStyle? style, Widget? underline, Widget? icon, Color? iconDisabledColor, Color? iconEnabledColor, double iconSize = 24.0, bool isDense = false, bool isExpanded = false, double? itemHeight = kMinInteractiveDimension, double? menuWidth, Color? focusColor, FocusNode? focusNode, bool autofocus = false, Color? dropdownColor, double? menuMaxHeight, bool? enableFeedback, AlignmentGeometry alignment = AlignmentDirectional.centerStart, BorderRadius? borderRadius, EdgeInsetsGeometry? padding, bool barrierDismissible = true, MouseCursor? mouseCursor, MouseCursor? dropdownMenuItemMouseCursor})
```

Creates a dropdown button.

The [items] must have distinct values. If [value] isn't null then it must be equal to one of the [DropdownMenuItem] values. If [items] or [onChanged] is null, the button will be disabled, the down arrow will be greyed out.

If [value] is null and the button is enabled, [hint] will be displayed if it is non-null.

If [value] is null and the button is disabled, [disabledHint] will be displayed if it is non-null. If [disabledHint] is null, then [hint] will be displayed if it is non-null.

The [dropdownColor] argument specifies the background color of the dropdown when it is open. If it is null, the current theme's [ThemeData.canvasColor] will be used instead.

### items

```dart
List<DropdownMenuItem<T>>? items
```

The list of items the user can select.

If the [onChanged] callback is null or the list of items is null then the dropdown button will be disabled, i.e. its arrow will be displayed in grey and it will not respond to input.

### value

```dart
T? value
```

The value of the currently selected [DropdownMenuItem].

If [value] is null and the button is enabled, [hint] will be displayed if it is non-null.

If [value] is null and the button is disabled, [disabledHint] will be displayed if it is non-null. If [disabledHint] is null, then [hint] will be displayed if it is non-null.

### hint

```dart
Widget? hint
```

A placeholder widget that is displayed by the dropdown button.

If [value] is null and the dropdown is enabled ([items] and [onChanged] are non-null), this widget is displayed as a placeholder for the dropdown button's value.

If [value] is null and the dropdown is disabled and [disabledHint] is null, this widget is used as the placeholder.

### disabledHint

```dart
Widget? disabledHint
```

A preferred placeholder widget that is displayed when the dropdown is disabled.

If [value] is null, the dropdown is disabled ([items] or [onChanged] is null), this widget is displayed as a placeholder for the dropdown button's value.

### onChanged

```dart
ValueChanged<T?>? onChanged
```

{@template flutter.material.dropdownButton.onChanged} Called when the user selects an item.

If the [onChanged] callback is null or the list of [DropdownButton.items] is null then the dropdown button will be disabled, i.e. its arrow will be displayed in grey and it will not respond to input. A disabled button will display the [DropdownButton.disabledHint] widget if it is non-null. If [DropdownButton.disabledHint] is also null but [DropdownButton.hint] is non-null, [DropdownButton.hint] will instead be displayed. {@endtemplate}

### onTap

```dart
VoidCallback? onTap
```

Called when the dropdown button is tapped.

This is distinct from [onChanged], which is called when the user selects an item from the dropdown.

The callback will not be invoked if the dropdown button is disabled.

### selectedItemBuilder

```dart
DropdownButtonBuilder? selectedItemBuilder
```

A builder to customize the dropdown buttons corresponding to the [DropdownMenuItem]s in [items].

When a [DropdownMenuItem] is selected, the widget that will be displayed from the list corresponds to the [DropdownMenuItem] of the same index in [items].

{@tool dartpad} This sample shows a `DropdownButton` with a button with [Text] that corresponds to but is unique from [DropdownMenuItem].

** See code in examples/api/lib/material/dropdown/dropdown_button.selected_item_builder.0.dart ** {@end-tool}

If this callback is null, the [DropdownMenuItem] from [items] that matches [value] will be displayed.

The list of widgets returned by this builder must be exactly the same length as the [items] list.

### elevation

```dart
int elevation
```

The z-coordinate at which to place the menu when open.

The following elevations have defined shadows: 1, 2, 3, 4, 6, 8, 9, 12, 16, and 24. See [kElevationToShadow].

Defaults to 8, the appropriate elevation for dropdown buttons.

### style

```dart
TextStyle? style
```

The text style to use for text in the dropdown button and the dropdown menu that appears when you tap the button.

To use a separate text style for selected item when it's displayed within the dropdown button, consider using [selectedItemBuilder].

{@tool dartpad} This sample shows a `DropdownButton` with a dropdown button text style that is different than its menu items.

** See code in examples/api/lib/material/dropdown/dropdown_button.style.0.dart ** {@end-tool}

Defaults to the [TextTheme.titleMedium] value of the current [ThemeData.textTheme] of the current [Theme].

### underline

```dart
Widget? underline
```

The widget to use for drawing the drop-down button's underline.

Defaults to a 0.0 width bottom border with color 0xFFBDBDBD.

### icon

```dart
Widget? icon
```

The widget to use for the drop-down button's icon.

Defaults to an [Icon] with the [Icons.arrow_drop_down] glyph.

### iconDisabledColor

```dart
Color? iconDisabledColor
```

The color of any [Icon] descendant of [icon] if this button is disabled, i.e. if [onChanged] is null.

Defaults to [MaterialColor.shade400] of [Colors.grey] when the theme's [ThemeData.brightness] is [Brightness.light] and to [Colors.white10] when it is [Brightness.dark]

### iconEnabledColor

```dart
Color? iconEnabledColor
```

The color of any [Icon] descendant of [icon] if this button is enabled, i.e. if [onChanged] is defined.

Defaults to [MaterialColor.shade700] of [Colors.grey] when the theme's [ThemeData.brightness] is [Brightness.light] and to [Colors.white70] when it is [Brightness.dark]

### iconSize

```dart
double iconSize
```

The size to use for the drop-down button's down arrow icon button.

Defaults to 24.0.

### isDense

```dart
bool isDense
```

Reduce the button's height.

By default this button's height is the same as its menu items' heights. If isDense is true, the button's height is reduced by about half. This can be useful when the button is embedded in a container that adds its own decorations, like [InputDecorator].

### isExpanded

```dart
bool isExpanded
```

Set the dropdown's inner contents to horizontally fill its parent.

By default this button's inner width is the minimum size of its contents. If [isExpanded] is true, the inner width is expanded to fill its surrounding container.

### itemHeight

```dart
double? itemHeight
```

If null, then the menu item heights will vary according to each menu item's intrinsic height.

The default value is [kMinInteractiveDimension], which is also the minimum height for menu items.

If this value is null and there isn't enough vertical room for the menu, then the menu's initial scroll offset may not align the selected item with the dropdown button. That's because, in this case, the initial scroll offset is computed as if all of the menu item heights were [kMinInteractiveDimension].

### menuWidth

```dart
double? menuWidth
```

The width of the menu.

If it is not provided, the width of the menu is the width of the dropdown button.

### focusColor

```dart
Color? focusColor
```

The color for the button's [Material] when it has the input focus.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### dropdownColor

```dart
Color? dropdownColor
```

The background color of the dropdown.

If it is not provided, the theme's [ThemeData.canvasColor] will be used instead.

### padding

```dart
EdgeInsetsGeometry? padding
```

Padding around the visible portion of the dropdown widget.

As the padding increases, the size of the [DropdownButton] will also increase. The padding is included in the clickable area of the dropdown widget, so this can make the widget easier to click.

Padding can be useful when used with a custom border. The clickable area will stay flush with the border, as opposed to an external [Padding] widget which will leave a non-clickable gap.

### menuMaxHeight

```dart
double? menuMaxHeight
```

The maximum height of the menu.

The maximum height of the menu must be at least one row shorter than the height of the app's view. This ensures that a tappable area outside of the simple menu is present so the user can dismiss the menu.

If this property is set above the maximum allowable height threshold mentioned above, then the menu defaults to being padded at the top and bottom of the menu by at one menu item's height.

### enableFeedback

```dart
bool? enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

By default, platform-specific feedback is enabled.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### alignment

```dart
AlignmentGeometry alignment
```

Defines how the hint or the selected item is positioned within the button.

Defaults to [AlignmentDirectional.centerStart].

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### borderRadius

```dart
BorderRadius? borderRadius
```

Defines the corner radii of the menu's rounded rectangle shape.

### barrierDismissible

```dart
bool barrierDismissible
```

Determines whether tapping outside the dropdown will close it.

Defaults to `true`.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over this button.

{@macro flutter.material.InkWell.mouseCursor}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### dropdownMenuItemMouseCursor

```dart
MouseCursor? dropdownMenuItemMouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the this button's [items].

{@macro flutter.material.InkWell.mouseCursor}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### createState()

```dart
State<DropdownButton<T>> createState()
```

# DropdownButtonFormField

```dart
class DropdownButtonFormField<T> extends FormField<T> {}
```

A [FormField] that contains a [DropdownButton].

This is a convenience widget that wraps a [DropdownButton] widget in a [FormField].

A [Form] ancestor is not required. The [Form] allows one to save, reset, or validate multiple fields at once. To use without a [Form], pass a [GlobalKey] to the constructor and use [GlobalKey.currentState] to save or reset the form field.

The `value` parameter maps to [FormField.initialValue].

See also:

- [DropdownButton], which is the underlying text field without the [Form] integration.

### DropdownButtonFormField()

```dart
DropdownButtonFormField({dynamic key, required List<DropdownMenuItem<T>>? items, DropdownButtonBuilder? selectedItemBuilder, T? value, T? initialValue, Widget? hint, Widget? disabledHint, required ValueChanged<T?>? onChanged, VoidCallback? onTap, int elevation = 8, TextStyle? style, Widget? icon, Color? iconDisabledColor, Color? iconEnabledColor, double iconSize = 24.0, bool isDense = true, bool isExpanded = false, double? itemHeight, Color? focusColor, FocusNode? focusNode, bool autofocus = false, Color? dropdownColor, InputDecoration? decoration, dynamic onSaved, dynamic validator, dynamic errorBuilder, dynamic forceErrorText, AutovalidateMode? autovalidateMode, double? menuMaxHeight, bool? enableFeedback, AlignmentGeometry alignment = AlignmentDirectional.centerStart, BorderRadius? borderRadius, EdgeInsetsGeometry? padding, bool barrierDismissible = true, MouseCursor? mouseCursor, MouseCursor? dropdownMenuItemMouseCursor})
```

Creates a [DropdownButton] widget that is a [FormField], wrapped in an [InputDecorator].

For a description of the `onSaved`, `validator`, or `autovalidateMode` parameters, see [FormField]. For the rest (other than [decoration]), see [DropdownButton].

### onChanged

```dart
ValueChanged<T?>? onChanged
```

{@macro flutter.material.dropdownButton.onChanged}

This callback is invoked after the parent [Form]'s [Form.onChanged] callback. The field's updated value is available in the [Form.onChanged] callback via [FormFieldState.value].

### decoration

```dart
InputDecoration decoration
```

The decoration to show around the dropdown button form field.

By default, draws a horizontal line under the dropdown button field but can be configured to show an icon, label, hint text, and error text.

If not specified, an [InputDecorator] with the `focusColor` set to the supplied `focusColor` (if any) will be used.

### barrierDismissible

```dart
bool barrierDismissible
```

Determines whether tapping outside the dropdown will close it.

Defaults to `true`.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the dropdown button and its [DropdownMenuItem]s.

{@macro flutter.material.InkWell.mouseCursor}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### dropdownMenuItemMouseCursor

```dart
MouseCursor? dropdownMenuItemMouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the this button's [DropdownMenuItem]s.

{@macro flutter.material.InkWell.mouseCursor}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### createState()

```dart
FormFieldState<T> createState()
```
