@docImport 'text_theme.dart';

# FilterCallback

```dart
typedef FilterCallback<T> = List<DropdownMenuEntry<T>> Function(List<DropdownMenuEntry<T>> entries, String filter)
```

A callback function that returns the list of the items that matches the current applied filter.

Used by [DropdownMenu.filterCallback].

# SearchCallback

```dart
typedef SearchCallback<T> = int? Function(List<DropdownMenuEntry<T>> entries, String query)
```

A callback function that returns the index of the item that matches the current contents of a text field.

If a match doesn't exist then null must be returned.

Used by [DropdownMenu.searchCallback].

# DropdownMenuDecorationBuilder

```dart
typedef DropdownMenuDecorationBuilder = InputDecoration Function(BuildContext context, MenuController controller)
```

The type of builder function used by [DropdownMenu.decorationBuilder] to build the [InputDecoration] passed to the inner text field.

The `context` is the context that the decoration is being built in.

The `controller` is the [MenuController] that can be used to open and close the menu with and query the current state.

# DropdownMenuEntry

```dart
class DropdownMenuEntry<T> {}
```

Defines a [DropdownMenu] menu button that represents one item view in the menu.

See also:

- [DropdownMenu]

### DropdownMenuEntry()

```dart
DropdownMenuEntry({required T value, required String label, Widget? labelWidget, Widget? leadingIcon, Widget? trailingIcon, bool enabled = true, ButtonStyle? style})
```

Creates an entry that is used with [DropdownMenu.dropdownMenuEntries].

### value

```dart
T value
```

the value used to identify the entry.

This value must be unique across all entries in a [DropdownMenu].

### label

```dart
String label
```

The label displayed in the center of the menu item.

### labelWidget

```dart
Widget? labelWidget
```

Overrides the default label widget which is `Text(label)`.

This widget is only displayed in the open dropdown menu. When an item is selected, the menu closes and the text field displays the plain text of the [label].

The dropdown menu's closed state is a text field or a read-only text field on mobile, which can only display text. While custom widgets like icons or images can be shown in [labelWidget] when the menu is open, the text field will only show the [label] string upon selection.

To control the text that appears in the text field for a selected item, set the [label] property to a descriptive string.

{@tool dartpad} This sample shows how to override the default label [Text] widget with one that forces the menu entry to appear on one line by specifying [Text.maxLines] and [Text.overflow].

** See code in examples/api/lib/material/dropdown_menu/dropdown_menu_entry_label_widget.0.dart ** {@end-tool}

### leadingIcon

```dart
Widget? leadingIcon
```

An optional icon to display before the label.

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon to display after the label.

### enabled

```dart
bool enabled
```

Whether the menu item is enabled or disabled.

The default value is true. If true, the [DropdownMenuEntry.label] will be filled out in the text field of the [DropdownMenu] when this entry is clicked; otherwise, this entry is disabled.

### style

```dart
ButtonStyle? style
```

Customizes this menu item's appearance.

Null by default.

# DropdownMenuCloseBehavior

```dart
enum DropdownMenuCloseBehavior {}
```

Defines the behavior for closing the dropdown menu when an item is selected.

Closes all open menus in the widget tree.

Closes only the current dropdown menu.

Does not close any menus.

# DropdownMenu

```dart
class DropdownMenu<T> extends StatefulWidget {}
```

A dropdown menu that can be opened from a [TextField]. The selected menu item is displayed in that field.

{@youtube 560 315 https://www.youtube.com/watch?v=giV9AbM2gd8}

This widget is used to help people make a choice from a menu and put the selected item into the text input field. People can also filter the list based on the text input or search one item in the menu list.

The menu is composed of a list of [DropdownMenuEntry]s. People can provide information, such as: label, leading icon or trailing icon for each entry. The [TextField] will be updated based on the selection from the menu entries. The text field will stay empty if the selected entry is disabled.

When the dropdown menu has focus, it can be traversed by pressing the up or down key. During the process, the corresponding item will be highlighted and the text field will be updated. Disabled items will be skipped during traversal.

The menu can be scrollable if not all items in the list are displayed at once.

{@tool dartpad} This sample shows how to display outlined [DropdownMenu] and filled [DropdownMenu].

** See code in examples/api/lib/material/dropdown_menu/dropdown_menu.0.dart ** {@end-tool}

See also:

- [MenuAnchor], which is a widget used to mark the "anchor" for a set of submenus. The [DropdownMenu] uses a [TextField] as the "anchor".
- [TextField], which is a text input widget that uses an [InputDecoration].
- [DropdownMenuEntry], which is used to build the [MenuItemButton] in the [DropdownMenu] list.

### DropdownMenu()

```dart
DropdownMenu({dynamic key, bool enabled = true, double? width, double? menuHeight, Widget? leadingIcon, Widget? trailingIcon, bool showTrailingIcon = true, FocusNode? trailingIconFocusNode, Widget? label, String? hintText, String? helperText, String? errorText, Widget? selectedTrailingIcon, bool enableFilter = false, bool enableSearch = true, TextInputType? keyboardType, TextStyle? textStyle, TextAlign textAlign = TextAlign.start, Object? inputDecorationTheme, DropdownMenuDecorationBuilder? decorationBuilder, MenuStyle? menuStyle, TextEditingController? controller, T? initialSelection, ValueChanged<T?>? onSelected, FocusNode? focusNode, bool? requestFocusOnTap, bool selectOnly = false, EdgeInsetsGeometry? expandedInsets, FilterCallback<T>? filterCallback, SearchCallback<T>? searchCallback, Offset? alignmentOffset, required List<DropdownMenuEntry<T>> dropdownMenuEntries, List<TextInputFormatter>? inputFormatters, DropdownMenuCloseBehavior closeBehavior = DropdownMenuCloseBehavior.all, int? maxLines = 1, TextInputAction? textInputAction, double? cursorHeight, String? restorationId, MenuController? menuController, EdgeInsets scrollPadding = const EdgeInsets.all(20.0)})
```

Creates a const [DropdownMenu].

The leading and trailing icons in the text field can be customized by using [leadingIcon], [trailingIcon] and [selectedTrailingIcon] properties. They are passed down to the [InputDecoration] properties, and will override values in the [InputDecoration.prefixIcon] and [InputDecoration.suffixIcon].

Except leading and trailing icons, the text field can be configured by the [inputDecorationTheme] property. The menu can be configured by the [menuStyle].

### enabled

```dart
bool enabled
```

Determine if the [DropdownMenu] is enabled.

Defaults to true.

{@tool dartpad} This sample demonstrates how the [enabled] and [requestFocusOnTap] properties affect the textfield's hover cursor.

** See code in examples/api/lib/material/dropdown_menu/dropdown_menu.2.dart ** {@end-tool}

### width

```dart
double? width
```

Determine the width of the [DropdownMenu].

If this is null, the width of the [DropdownMenu] will be the same as the width of the widest menu item plus the width of the leading/trailing icon.

### menuHeight

```dart
double? menuHeight
```

Determine the height of the menu.

If this is null, the menu will display as many items as possible on the screen.

### leadingIcon

```dart
Widget? leadingIcon
```

An optional Icon at the front of the text input field.

Defaults to null. If this is not null, the menu items will have extra paddings to be aligned with the text in the text field.

### trailingIcon

```dart
Widget? trailingIcon
```

An optional icon at the end of the text field.

Defaults to an [Icon] with [Icons.arrow_drop_down].

If [showTrailingIcon] is false, the trailing icon will not be shown.

### showTrailingIcon

```dart
bool showTrailingIcon
```

Specifies if the [DropdownMenu] should show the [trailingIcon].

If [trailingIcon] is set, [DropdownMenu] will use that trailing icon, otherwise a default trailing icon will be created.

If [showTrailingIcon] is false, [trailingIconFocusNode] must be null.

If a value is provided for [decorationBuilder] and the resulting [InputDecoration.suffixIcon] is not null, [showTrailingIcon] has no effect.

Defaults to true.

### trailingIconFocusNode

```dart
FocusNode? trailingIconFocusNode
```

Defines the FocusNode for the trailing icon.

If [showTrailingIcon] is false, [trailingIconFocusNode] must be null.

The [focusNode] is a long-lived object that's typically managed by a [StatefulWidget] parent. See [FocusNode] for more information.

To give the keyboard focus to this widget, provide a [focusNode] and then use the current [FocusScope] to request the focus:

```dart
FocusScope.of(context).requestFocus(myFocusNode);
```

This happens automatically when the widget is tapped.

To be notified when the widget gains or loses the focus, add a listener to the [focusNode]:

```dart
myFocusNode.addListener(() { print(myFocusNode.hasFocus); });
```

If null, this widget will create its own [FocusNode].

### label

```dart
Widget? label
```

Optional widget that describes the input field.

When the input field is empty and unfocused, the label is displayed on top of the input field (i.e., at the same location on the screen where text may be entered in the input field). When the input field receives focus (or if the field is non-empty), the label moves above, either vertically adjacent to, or to the center of the input field.

Defaults to null.

### hintText

```dart
String? hintText
```

Text that suggests what sort of input the field accepts.

Defaults to null;

### helperText

```dart
String? helperText
```

Text that provides context about the [DropdownMenu]'s value, such as how the value will be used.

If non-null, the text is displayed below the input field, in the same location as [errorText]. If a non-null [errorText] value is specified then the helper text is not shown.

Defaults to null;

See also:

- [InputDecoration.helperText], which is the text that provides context about the [InputDecorator.child]'s value.

### errorText

```dart
String? errorText
```

Text that appears below the input field and the border to show the error message.

If non-null, the border's color animates to red and the [helperText] is not shown.

Defaults to null;

See also:

- [InputDecoration.errorText], which is the text that appears below the [InputDecorator.child] and the border.

### selectedTrailingIcon

```dart
Widget? selectedTrailingIcon
```

An optional icon at the end of the text field to indicate that the text field is pressed.

Defaults to an [Icon] with [Icons.arrow_drop_up].

### enableFilter

```dart
bool enableFilter
```

Determine if the menu list can be filtered by the text input.

Defaults to false.

### enableSearch

```dart
bool enableSearch
```

Determine if the first item that matches the text input can be highlighted.

Defaults to true as the search function could be commonly used.

### keyboardType

```dart
TextInputType? keyboardType
```

The type of keyboard to use for editing the text.

Defaults to [TextInputType.text].

### textStyle

```dart
TextStyle? textStyle
```

The text style for the [TextField] of the [DropdownMenu];

Defaults to the overall theme's [TextTheme.bodyLarge] if the dropdown menu theme's value is null.

### textAlign

```dart
TextAlign textAlign
```

The text align for the [TextField] of the [DropdownMenu].

Defaults to [TextAlign.start].

### inputDecorationTheme

```dart
InputDecorationThemeData? get inputDecorationTheme
```

Defines the default appearance of [InputDecoration] to show around the text field.

By default, shows a outlined text field.

### decorationBuilder

```dart
DropdownMenuDecorationBuilder? decorationBuilder
```

The builder function used to create the [InputDecoration] passed to the text field.

If a value is provided for this property and the resulting [InputDecoration.suffixIcon] is null, a default [IconButton] is assigned as the suffix icon. This button's icon will use [trailingIcon] and [selectedTrailingIcon] if those are explicitly defined; otherwise, it defaults to [Icons.arrow_drop_down] for the collapsed state and [Icons.arrow_drop_up] for the expanded state.

If null, the default builder creates a decoration where:

- [InputDecoration.label] is set to [label].
- [InputDecoration.hintText] is set to [hintText].
- [InputDecoration.helperText] is set to [helperText].
- [InputDecoration.errorText] is set to [errorText].
- [InputDecoration.prefixIcon] is set to [leadingIcon].
- [InputDecoration.suffixIcon] is set to an [IconButton] which uses [trailingIcon] and [selectedTrailingIcon] if defined, or [Icons.arrow_drop_down] and [Icons.arrow_drop_up] otherwise.

### menuStyle

```dart
MenuStyle? menuStyle
```

The [MenuStyle] that defines the visual attributes of the menu.

The default width of the menu is set to the width of the text field.

### controller

```dart
TextEditingController? controller
```

Controls the text being edited or selected in the menu.

If null, this widget will create its own [TextEditingController].

### initialSelection

```dart
T? initialSelection
```

The value used for an initial selection.

This property sets the initial value of the dropdown menu when the widget is first created. If the value matches one of the [dropdownMenuEntries], the corresponding label will be displayed in the text field.

Setting this to null does not clear the text field.

To programmatically clear the text field, use a [TextEditingController] and call [TextEditingController.clear] on it.

Defaults to null.

See also:

- [controller], which is required to programmatically clear or modify the text field content.

### onSelected

```dart
ValueChanged<T?>? onSelected
```

The callback is called when a selection is made.

The callback receives the selected entry's value of type `T` when the user chooses an item. It may also be invoked with `null` to indicate that the selection was cleared / that no item was chosen.

Defaults to null. If this callback itself is null, the widget still updates the text field with the selected label.

### focusNode

```dart
FocusNode? focusNode
```

Defines the keyboard focus for this widget.

The [focusNode] is a long-lived object that's typically managed by a [StatefulWidget] parent. See [FocusNode] for more information.

To give the keyboard focus to this widget, provide a [focusNode] and then use the current [FocusScope] to request the focus:

```dart
FocusScope.of(context).requestFocus(myFocusNode);
```

This happens automatically when the widget is tapped.

To be notified when the widget gains or loses the focus, add a listener to the [focusNode]:

```dart
myFocusNode.addListener(() { print(myFocusNode.hasFocus); });
```

If null, this widget will create its own [FocusNode].

## Keyboard

Requesting the focus will typically cause the keyboard to be shown if it's not showing already.

On Android, the user can hide the keyboard - without changing the focus - with the system back button. They can restore the keyboard's visibility by tapping on a text field. The user might hide the keyboard and switch to a physical keyboard, or they might just need to get it out of the way for a moment, to expose something it's obscuring. In this case requesting the focus again will not cause the focus to change, and will not make the keyboard visible.

If this is non-null, the behaviour of [requestFocusOnTap] is overridden by the [FocusNode.canRequestFocus] property.

### requestFocusOnTap

```dart
bool? requestFocusOnTap
```

Determine if the dropdown menu requests focus and the on-screen virtual keyboard is shown in response to a touch event.

Ignored if a [focusNode] is explicitly provided (in which case, [FocusNode.canRequestFocus] controls the behavior).

Defaults to null, which enables platform-specific behavior:

- On mobile platforms, acts as if set to false; tapping on the text field and opening the menu will not cause a focus request and the virtual keyboard will not appear.

- On desktop platforms, acts as if set to true; the dropdown takes the focus when activated.

Set this to true or false explicitly to override the default behavior.

{@tool dartpad} This sample demonstrates how the [enabled] and [requestFocusOnTap] properties affect the textfield's hover cursor.

** See code in examples/api/lib/material/dropdown_menu/dropdown_menu.2.dart ** {@end-tool}

### selectOnly

```dart
bool selectOnly
```

Determines if the dropdown menu behaves as a 'select' component.

This is useful for mobile platforms where a dropdown menu is commonly used as a 'select' widget (i.e., the user can only select from the list, not edit the text field to search or filter).

When true, the inner text field is read-only.

If the text field is also focusable (see [requestFocusOnTap]), the following behaviors are also activated:

- Pressing Enter when the menu is closed opens it.
- The decoration reflects the focus state.

Defaults to false.

### dropdownMenuEntries

```dart
List<DropdownMenuEntry<T>> dropdownMenuEntries
```

Descriptions of the menu items in the [DropdownMenu].

This is a required parameter. It is recommended that at least one [DropdownMenuEntry] is provided. If this is an empty list, the menu will be empty and only contain space for padding.

### expandedInsets

```dart
EdgeInsetsGeometry? expandedInsets
```

Defines the menu text field's width to be equal to its parent's width plus the horizontal width of the specified insets.

If this property is null, the width of the text field will be determined by the width of menu items or [DropdownMenu.width]. If this property is not null, the text field's width will match the parent's width plus the specified insets. If the value of this property is [EdgeInsets.zero], the width of the text field will be the same as its parent's width.

The [expandedInsets]' top and bottom are ignored, only its left and right properties are used.

Defaults to null.

### filterCallback

```dart
FilterCallback<T>? filterCallback
```

When [DropdownMenu.enableFilter] is true, this callback is used to compute the list of filtered items.

{@tool snippet}

In this example the `filterCallback` returns the items that contains the trimmed query.

```dart
DropdownMenu<Text>(
  enableFilter: true,
  filterCallback: (List<DropdownMenuEntry<Text>> entries, String filter) {
    final String trimmedFilter = filter.trim().toLowerCase();
      if (trimmedFilter.isEmpty) {
        return entries;
      }

      return entries
        .where((DropdownMenuEntry<Text> entry) =>
          entry.label.toLowerCase().contains(trimmedFilter),
        )
        .toList();
  },
  dropdownMenuEntries: const <DropdownMenuEntry<Text>>[],
)
```

{@end-tool}

Defaults to null. If this parameter is null and the [DropdownMenu.enableFilter] property is set to true, the default behavior will return a filtered list. The filtered list will contain items that match the text provided by the input field, with a case-insensitive comparison. When this is not null, `enableFilter` must be set to true.

### searchCallback

```dart
SearchCallback<T>? searchCallback
```

When [DropdownMenu.enableSearch] is true, this callback is used to compute the index of the search result to be highlighted.

{@tool snippet}

In this example the `searchCallback` returns the index of the search result that exactly matches the query.

```dart
DropdownMenu<Text>(
  searchCallback: (List<DropdownMenuEntry<Text>> entries, String query) {
    if (query.isEmpty) {
      return null;
    }
    final int index = entries.indexWhere((DropdownMenuEntry<Text> entry) => entry.label == query);

    return index != -1 ? index : null;
  },
  dropdownMenuEntries: const <DropdownMenuEntry<Text>>[],
)
```

{@end-tool}

Defaults to null. If this is null and [DropdownMenu.enableSearch] is true, the default function will return the index of the first matching result which contains the contents of the text input field.

### inputFormatters

```dart
List<TextInputFormatter>? inputFormatters
```

Optional input validation and formatting overrides.

Formatters are run in the provided order when the user changes the text this widget contains. When this parameter changes, the new formatters will not be applied until the next time the user inserts or deletes text. Formatters don't run when the text is changed programmatically via [controller].

See also:

- [TextEditingController], which implements the [Listenable] interface and notifies its listeners on [TextEditingValue] changes.

### alignmentOffset

```dart
Offset? alignmentOffset
```

{@macro flutter.material.MenuAnchor.alignmentOffset}

### closeBehavior

```dart
DropdownMenuCloseBehavior closeBehavior
```

Defines the behavior for closing the dropdown menu when an item is selected.

The close behavior can be set to:

- [DropdownMenuCloseBehavior.all]: Closes all open menus in the widget tree.
- [DropdownMenuCloseBehavior.self]: Closes only the current dropdown menu.
- [DropdownMenuCloseBehavior.none]: Does not close any menus.

This property allows fine-grained control over the menu's closing behavior, which can be useful for creating nested or complex menu structures.

Defaults to [DropdownMenuCloseBehavior.all].

### maxLines

```dart
int? maxLines
```

Specifies the maximum number of lines the selected value can display in the [DropdownMenu].

If the provided value is 1, then the text will not wrap, but will scroll horizontally instead. Defaults to 1.

If this is null, there is no limit to the number of lines, and the text container will start with enough vertical space for one line and automatically grow to accommodate additional lines as they are entered, up to the height of its constraints.

If this is not null, the provided value must be greater than zero. The text field will restrict the input to the given number of lines and take up enough horizontal space to accommodate that number of lines.

See also:

- [TextField.maxLines], which specifies the maximum number of lines the [TextField] can display.

### textInputAction

```dart
TextInputAction? textInputAction
```

{@macro flutter.widgets.TextField.textInputAction}

### cursorHeight

```dart
double? cursorHeight
```

{@macro flutter.widgets.editableText.cursorHeight}

### restorationId

```dart
String? restorationId
```

{@macro flutter.material.textfield.restorationId}

### menuController

```dart
MenuController? menuController
```

An optional controller that allows opening and closing of the menu from other widgets.

### scrollPadding

```dart
EdgeInsets scrollPadding
```

{@macro flutter.widgets.editableText.scrollPadding}

### createState()

```dart
State<DropdownMenu<T>> createState()
```
