@docImport 'action_chip.dart'; @docImport 'choice_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'filter_chip.dart'; @docImport 'material.dart';

# InputChip

```dart
class InputChip extends StatelessWidget implements ChipAttributes, DeletableChipAttributes, SelectableChipAttributes, CheckmarkableChipAttributes, DisabledChipAttributes, TappableChipAttributes {}
```

A Material Design input chip.

Input chips represent a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.

Input chips can be made selectable by setting [onSelected], deletable by setting [onDeleted], and pressable like a button with [onPressed]. They have a [label], and they can have a leading icon (see [avatar]) and a trailing icon ([deleteIcon]). Colors and padding can be customized.

Requires one of its ancestors to be a [Material] widget.

Input chips work together with other UI elements. They can appear:

- In a [Wrap] widget.
- In a horizontally scrollable list, for example configured such as a [ListView] with [ListView.scrollDirection] set to [Axis.horizontal].

{@tool dartpad} This example shows how to create [InputChip]s with [onSelected] and [onDeleted] callbacks. When the user taps the chip, the chip will be selected. When the user taps the delete icon, the chip will be deleted.

** See code in examples/api/lib/material/input_chip/input_chip.0.dart ** {@end-tool}

{@tool dartpad} The following example shows how to generate [InputChip]s from user text input. When the user enters a pizza topping in the text field, the user is presented with a list of suggestions. When selecting one of the suggestions, an [InputChip] is generated in the text field.

** See code in examples/api/lib/material/input_chip/input_chip.1.dart ** {@end-tool}

## Material Design 3

[InputChip] can be used for Input chips from Material Design 3. If [ThemeData.useMaterial3] is true, then [InputChip] will be styled to match the Material Design 3 specification for Input chips.

See also:

- [Chip], a chip that displays information and can be deleted.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- [CircleAvatar], which shows images or initials of people.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### InputChip()

```dart
InputChip({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, bool selected = false, bool isEnabled = true, ValueChanged<bool>? onSelected, Widget? deleteIcon, VoidCallback? onDeleted, Color? deleteIconColor, String? deleteButtonTooltipMessage, VoidCallback? onPressed, double? pressElevation, Color? disabledColor, Color? selectedColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Creates an [InputChip].

The [onPressed] and [onSelected] callbacks must not both be specified at the same time. When both [onPressed] and [onSelected] are null, the chip will be disabled.

The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

### avatar

```dart
Widget? avatar
```

### label

```dart
Widget label
```

### labelStyle

```dart
TextStyle? labelStyle
```

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

### selected

```dart
bool selected
```

### isEnabled

```dart
bool isEnabled
```

### onSelected

```dart
ValueChanged<bool>? onSelected
```

### deleteIcon

```dart
Widget? deleteIcon
```

### onDeleted

```dart
VoidCallback? onDeleted
```

### deleteIconColor

```dart
Color? deleteIconColor
```

### deleteButtonTooltipMessage

```dart
String? deleteButtonTooltipMessage
```

### onPressed

```dart
VoidCallback? onPressed
```

### pressElevation

```dart
double? pressElevation
```

### disabledColor

```dart
Color? disabledColor
```

### selectedColor

```dart
Color? selectedColor
```

### tooltip

```dart
String? tooltip
```

### side

```dart
BorderSide? side
```

### shape

```dart
OutlinedBorder? shape
```

### clipBehavior

```dart
Clip clipBehavior
```

### focusNode

```dart
FocusNode? focusNode
```

### autofocus

```dart
bool autofocus
```

### color

```dart
WidgetStateProperty<Color?>? color
```

### backgroundColor

```dart
Color? backgroundColor
```

### padding

```dart
EdgeInsetsGeometry? padding
```

### visualDensity

```dart
VisualDensity? visualDensity
```

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

### elevation

```dart
double? elevation
```

### shadowColor

```dart
Color? shadowColor
```

### surfaceTintColor

```dart
Color? surfaceTintColor
```

### selectedShadowColor

```dart
Color? selectedShadowColor
```

### showCheckmark

```dart
bool? showCheckmark
```

### checkmarkColor

```dart
Color? checkmarkColor
```

### avatarBorder

```dart
ShapeBorder avatarBorder
```

### iconTheme

```dart
IconThemeData? iconTheme
```

### avatarBoxConstraints

```dart
BoxConstraints? avatarBoxConstraints
```

### deleteIconBoxConstraints

```dart
BoxConstraints? deleteIconBoxConstraints
```

### chipAnimationStyle

```dart
ChipAnimationStyle? chipAnimationStyle
```

### mouseCursor

```dart
MouseCursor? mouseCursor
```

### build()

```dart
Widget build(BuildContext context)
```
