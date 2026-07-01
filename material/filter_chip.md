@docImport 'action_chip.dart'; @docImport 'checkbox.dart'; @docImport 'choice_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'input_chip.dart'; @docImport 'material.dart'; @docImport 'switch.dart';

# FilterChip

```dart
class FilterChip extends StatelessWidget implements ChipAttributes, DeletableChipAttributes, SelectableChipAttributes, CheckmarkableChipAttributes, DisabledChipAttributes {}
```

A Material Design filter chip.

Filter chips use tags or descriptive words as a way to filter content.

Filter chips are a good alternative to [Checkbox] or [Switch] widgets. Unlike these alternatives, filter chips allow for clearly delineated and exposed options in a compact area.

Requires one of its ancestors to be a [Material] widget.

{@tool dartpad} This example shows how to use [FilterChip]s to filter through exercises.

** See code in examples/api/lib/material/filter_chip/filter_chip.0.dart ** {@end-tool}

## Material Design 3

[FilterChip] can be used for multiple select Filter chip from Material Design 3. If [ThemeData.useMaterial3] is true, then [FilterChip] will be styled to match the Material Design 3 specification for Filter chips. Use [ChoiceChip] for single select Filter chips.

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [ActionChip], represents an action related to primary content.
- [CircleAvatar], which shows images or initials of people.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### FilterChip()

```dart
FilterChip({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, bool selected = false, required ValueChanged<bool>? onSelected, Widget? deleteIcon, VoidCallback? onDeleted, Color? deleteIconColor, String? deleteButtonTooltipMessage, double? pressElevation, Color? disabledColor, Color? selectedColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create a chip that acts like a checkbox.

The [selected], [label], [autofocus], and [clipBehavior] arguments must not be null. When [onSelected] is null, the [FilterChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

### FilterChip.elevated()

```dart
FilterChip.elevated({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, bool selected = false, required ValueChanged<bool>? onSelected, Widget? deleteIcon, VoidCallback? onDeleted, Color? deleteIconColor, String? deleteButtonTooltipMessage, double? pressElevation, Color? disabledColor, Color? selectedColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create an elevated chip that acts like a checkbox.

The [selected], [label], [autofocus], and [clipBehavior] arguments must not be null. When [onSelected] is null, the [FilterChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

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

### isEnabled

```dart
bool get isEnabled
```

### build()

```dart
Widget build(BuildContext context)
```
