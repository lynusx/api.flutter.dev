@docImport 'action_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'filter_chip.dart'; @docImport 'input_chip.dart'; @docImport 'material.dart';

# ChoiceChip

```dart
class ChoiceChip extends StatelessWidget implements ChipAttributes, SelectableChipAttributes, CheckmarkableChipAttributes, DisabledChipAttributes {}
```

A Material Design choice chip.

[ChoiceChip]s represent a single choice from a set. Choice chips contain related descriptive text or categories.

Requires one of its ancestors to be a [Material] widget.

{@tool dartpad} This example shows how to create [ChoiceChip]s with [onSelected]. When the user taps, the chip will be selected.

** See code in examples/api/lib/material/choice_chip/choice_chip.0.dart ** {@end-tool}

## Material Design 3

[ChoiceChip] can be used for single select Filter chips from Material Design 3. If [ThemeData.useMaterial3] is true, then [ChoiceChip] will be styled to match the Material Design 3 specification for Filter chips. Use [FilterChip] for multiple select Filter chips.

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- [CircleAvatar], which shows images or initials of people.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### ChoiceChip()

```dart
ChoiceChip({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, ValueChanged<bool>? onSelected, double? pressElevation, required bool selected, Color? selectedColor, Color? disabledColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create a chip that acts like a radio button.

The [label], [selected], [autofocus], and [clipBehavior] arguments must not be null. When [onSelected] is null, the [ChoiceChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

### ChoiceChip.elevated()

```dart
ChoiceChip.elevated({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, ValueChanged<bool>? onSelected, double? pressElevation, required bool selected, Color? selectedColor, Color? disabledColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create an elevated chip that acts like a radio button.

The [label], [selected], [autofocus], and [clipBehavior] arguments must not be null. When [onSelected] is null, the [ChoiceChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

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

### onSelected

```dart
ValueChanged<bool>? onSelected
```

### pressElevation

```dart
double? pressElevation
```

### selected

```dart
bool selected
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
