@docImport 'choice_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'elevated_button.dart'; @docImport 'input_chip.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart';

# ActionChip

```dart
class ActionChip extends StatelessWidget implements ChipAttributes, TappableChipAttributes, DisabledChipAttributes {}
```

A Material Design action chip.

Action chips are a set of options which trigger an action related to primary content. Action chips should appear dynamically and contextually in a UI.

Action chips can be tapped to trigger an action or show progress and confirmation. For Material 3, a disabled state is supported for Action chips and is specified with [onPressed] being null. For previous versions of Material Design, it is recommended to remove the Action chip from the interface entirely rather than display a disabled chip.

Action chips are displayed after primary content, such as below a card or persistently at the bottom of a screen.

The material button widgets, [ElevatedButton], [TextButton], and [OutlinedButton], are an alternative to action chips, which should appear statically and consistently in a UI.

Requires one of its ancestors to be a [Material] widget.

{@tool dartpad} This example shows how to create an [ActionChip] with a leading icon. The icon is updated when the [ActionChip] is pressed.

** See code in examples/api/lib/material/action_chip/action_chip.0.dart ** {@end-tool}

## Material Design 3

[ActionChip] can be used for both the Assist and Suggestion chips from Material Design 3. If [ThemeData.useMaterial3] is true, then [ActionChip] will be styled to match the Material Design 3 Assist and Suggestion chips.

### Creating an Assist chip

Assist chips are used to provide a quick way to perform an action. To create an Action chip, set the icon property to the icon that represents the action and set the label to the name of the action.

### Creating a Suggestion chip

Suggestion chips usually display generated suggestions for the user, like a suggested response to a message.

To create a Suggestion chip, set the label to the suggestion and don't set the icon property.

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [CircleAvatar], which shows images or initials of people.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### ActionChip()

```dart
ActionChip({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, VoidCallback? onPressed, double? pressElevation, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, Color? disabledColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, BoxConstraints? avatarBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create a chip that acts like a button.

The [label], [autofocus], and [clipBehavior] arguments must not be null. When [onPressed] is null, the [ActionChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

### ActionChip.elevated()

```dart
ActionChip.elevated({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, VoidCallback? onPressed, double? pressElevation, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, Color? disabledColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, BoxConstraints? avatarBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Create an elevated chip that acts like a button.

The [label], [autofocus], and [clipBehavior] arguments must not be null. When [onPressed] is null, the [ActionChip] will be disabled. The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

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

### onPressed

```dart
VoidCallback? onPressed
```

### pressElevation

```dart
double? pressElevation
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

### disabledColor

```dart
Color? disabledColor
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
