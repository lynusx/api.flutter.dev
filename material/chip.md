@docImport 'action_chip.dart'; @docImport 'app.dart'; @docImport 'choice_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'filter_chip.dart'; @docImport 'input_chip.dart'; @docImport 'scaffold.dart';

# ChipAttributes

```dart
abstract interface class ChipAttributes {}
```

An interface defining the base attributes for a Material Design chip.

Chips are compact elements that represent an attribute, text, entity, or action.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- <https://material.io/design/components/chips.html>

### label

```dart
Widget get label
```

The primary content of the chip.

Typically a [Text] widget.

### avatar

```dart
Widget? get avatar
```

A widget to display prior to the chip's label.

Typically a [CircleAvatar] widget.

### labelStyle

```dart
TextStyle? get labelStyle
```

The style to be applied to the chip's label.

If this is null and [ThemeData.useMaterial3] is true, then [TextTheme.labelLarge] is used. Otherwise, [TextTheme.bodyLarge] is used.

This only has an effect on widgets that respect the [DefaultTextStyle], such as [Text].

If [TextStyle.color] is a [WidgetStateProperty<Color>], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.pressed].

### side

```dart
BorderSide? get side
```

The color and weight of the chip's outline.

Defaults to the border side in the ambient [ChipThemeData]. If the theme border side resolves to null and [ThemeData.useMaterial3] is true, then [BorderSide] with a [ColorScheme.outline] color is used when the chip is enabled, and [BorderSide] with a [ColorScheme.onSurface] color with an opacity of 0.12 is used when the chip is disabled. Otherwise, it defaults to null.

This value is combined with [shape] to create a shape decorated with an outline. To omit the outline entirely, pass [BorderSide.none] to [side].

If it is a [WidgetStateBorderSide], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.pressed].

### shape

```dart
OutlinedBorder? get shape
```

The [OutlinedBorder] to draw around the chip.

Defaults to the shape in the ambient [ChipThemeData]. If the theme shape resolves to null and [ThemeData.useMaterial3] is true, then [RoundedRectangleBorder] with a circular border radius of 8.0 is used. Otherwise, [StadiumBorder] is used.

This shape is combined with [side] to create a shape decorated with an outline. If [side] is not null or side of [shape] is [BorderSide.none], side of [shape] is ignored. To omit the outline entirely, pass [BorderSide.none] to [side].

If it is a [WidgetStateOutlinedBorder], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.pressed].

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### focusNode

```dart
FocusNode? get focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool get autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### color

```dart
WidgetStateProperty<Color?>? get color
```

The color that fills the chip, in all [WidgetState]s.

Defaults to null.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.disabled].

### backgroundColor

```dart
Color? get backgroundColor
```

Color to be used for the unselected, enabled chip's background.

The default is light grey.

### padding

```dart
EdgeInsetsGeometry? get padding
```

The padding between the contents of the chip and the outside [shape].

If this is null and [ThemeData.useMaterial3] is true, then a padding of 8.0 logical pixels on all sides is used. Otherwise, it defaults to a padding of 4.0 logical pixels on all sides.

### visualDensity

```dart
VisualDensity? get visualDensity
```

Defines how compact the chip's layout will be.

Chips are unaffected by horizontal density changes.

{@macro flutter.material.themedata.visualDensity}

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### labelPadding

```dart
EdgeInsetsGeometry? get labelPadding
```

The padding around the [label] widget.

By default, this is 4 logical pixels at the beginning and the end of the label, and zero on top and bottom.

### materialTapTargetSize

```dart
MaterialTapTargetSize? get materialTapTargetSize
```

Configures the minimum size of the tap target.

Defaults to [ThemeData.materialTapTargetSize].

See also:

- [MaterialTapTargetSize], for a description of how this affects tap targets.

### elevation

```dart
double? get elevation
```

Elevation to be applied on the chip relative to its parent.

This controls the size of the shadow below the chip.

Defaults to 0. The value is always non-negative.

### shadowColor

```dart
Color? get shadowColor
```

Color of the chip's shadow when the elevation is greater than 0.

If this is null and [ThemeData.useMaterial3] is true, then [Colors.transparent] color is used. Otherwise, it defaults to null.

### surfaceTintColor

```dart
Color? get surfaceTintColor
```

Color of the chip's surface tint overlay when its elevation is greater than 0.

This is not recommended for use. [Material 3 spec](https://m3.material.io/styles/color/the-color-system/color-roles) introduced a set of tone-based surfaces and surface containers in its [ColorScheme], which provide more flexibility. The intention is to eventually remove surface tint color from the framework.

If this is null, defaults to [Colors.transparent].

### iconTheme

```dart
IconThemeData? get iconTheme
```

Theme used for all icons in the chip.

If this is null and [ThemeData.useMaterial3] is true, then [IconThemeData] with a [ColorScheme.primary] color and a size of 18.0 is used when the chip is enabled, and [IconThemeData] with a [ColorScheme.onSurface] color and a size of 18.0 is used when the chip is disabled. Otherwise, it defaults to null.

### avatarBoxConstraints

```dart
BoxConstraints? get avatarBoxConstraints
```

Optional size constraints for the avatar.

When unspecified, defaults to a minimum size of chip height or label height (whichever is greater) and a padding of 8.0 pixels on all sides.

The default constraints ensure that the avatar is accessible. Specifying this parameter enables creation of avatar smaller than the minimum size, but it is not recommended.

{@tool dartpad} This sample shows how to use [avatarBoxConstraints] to adjust avatar size constraints

** See code in examples/api/lib/material/chip/chip_attributes.avatar_box_constraints.0.dart ** {@end-tool}

### chipAnimationStyle

```dart
ChipAnimationStyle? get chipAnimationStyle
```

Used to override the default chip animations durations.

If [ChipAnimationStyle.enableAnimation] with duration or reverse duration is provided, it will be used to override the chip enable and disable animation durations. If it is null, then default duration will be 75ms.

If [ChipAnimationStyle.selectAnimation] with duration or reverse duration is provided, it will be used to override the chip select and unselect animation durations. If it is null, then default duration will be 195ms.

If [ChipAnimationStyle.avatarDrawerAnimation] with duration or reverse duration is provided, it will be used to override the chip checkmark animation duration. If it is null, then default duration will be 150ms.

If [ChipAnimationStyle.deleteDrawerAnimation] with duration or reverse duration is provided, it will be used to override the chip delete icon animation duration. If it is null, then default duration will be 150ms.

{@tool dartpad} This sample showcases how to override the chip animations durations using [ChipAnimationStyle].

** See code in examples/api/lib/material/chip/chip_attributes.chip_animation_style.0.dart ** {@end-tool}

### mouseCursor

```dart
MouseCursor? get mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

# DeletableChipAttributes

```dart
abstract interface class DeletableChipAttributes {}
```

An interface for Material Design chips that can be deleted.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- <https://material.io/design/components/chips.html>

### deleteIcon

```dart
Widget? get deleteIcon
```

The icon displayed when [onDeleted] is set.

If [deleteIconColor] is provided, it will be used as the color of the delete icon. If [deleteIconColor] is null, then the icon will use the color specified in the chip [IconTheme]. If the [IconTheme] is null, then the icon will use the color specified in the [ThemeData.iconTheme].

If a size is specified in the chip [IconTheme], then the delete icon will use that size. Otherwise, defaults to 18 pixels.

Defaults to an [Icon] widget set to use [Icons.clear]. If [ThemeData.useMaterial3] is false, then defaults to an [Icon] widget set to use [Icons.cancel].

### onDeleted

```dart
VoidCallback? get onDeleted
```

Called when the user taps the [deleteIcon] to delete the chip.

If null, the delete button will not appear on the chip.

The chip will not automatically remove itself: this just tells the app that the user tapped the delete button. In order to delete the chip, you have to do something similar to the following sample:

{@tool dartpad} This sample shows how to use [onDeleted] to remove an entry when the delete button is tapped.

** See code in examples/api/lib/material/chip/deletable_chip_attributes.on_deleted.0.dart ** {@end-tool}

### deleteIconColor

```dart
Color? get deleteIconColor
```

Used to define the delete icon's color with an [IconTheme] that contains the icon.

The default is `Color(0xde000000)` (slightly transparent black) for light themes, and `Color(0xdeffffff)` (slightly transparent white) for dark themes.

The delete icon appears if [DeletableChipAttributes.onDeleted] is non-null.

### deleteButtonTooltipMessage

```dart
String? get deleteButtonTooltipMessage
```

The message to be used for the chip's delete button tooltip.

If provided with an empty string, the tooltip of the delete button will be disabled.

If null, the default [MaterialLocalizations.deleteButtonTooltip] will be used.

If the chip is disabled, the delete button tooltip will not be shown.

### deleteIconBoxConstraints

```dart
BoxConstraints? get deleteIconBoxConstraints
```

Optional size constraints for the delete icon.

When unspecified, defaults to a minimum size of chip height or label height (whichever is greater) and a padding of 8.0 pixels on all sides.

The default constraints ensure that the delete icon is accessible. Specifying this parameter enables creation of delete icon smaller than the minimum size, but it is not recommended.

{@tool dartpad} This sample shows how to use [deleteIconBoxConstraints] to adjust delete icon size constraints.

** See code in examples/api/lib/material/chip/deletable_chip_attributes.delete_icon_box_constraints.0.dart ** {@end-tool}

# CheckmarkableChipAttributes

```dart
abstract interface class CheckmarkableChipAttributes {}
```

An interface for Material Design chips that can have check marks.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- <https://material.io/design/components/chips.html>

### showCheckmark

```dart
bool? get showCheckmark
```

Whether or not to show a check mark when [SelectableChipAttributes.selected] is true.

Defaults to true.

### checkmarkColor

```dart
Color? get checkmarkColor
```

[Color] of the chip's check mark when a check mark is visible.

This will override the color set by the platform's brightness setting.

If null, it will defer to a color selected by the platform's brightness setting.

# SelectableChipAttributes

```dart
abstract interface class SelectableChipAttributes {}
```

An interface for Material Design chips that can be selected.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- <https://material.io/design/components/chips.html>

### selected

```dart
bool get selected
```

Whether or not this chip is selected.

If [onSelected] is not null, this value will be used to determine if the select check mark will be shown or not.

Defaults to false.

### onSelected

```dart
ValueChanged<bool>? get onSelected
```

Called when the chip should change between selected and de-selected states.

When the chip is tapped, then the [onSelected] callback, if set, will be applied to `!selected` (see [selected]).

The chip passes the new value to the callback but does not actually change state until the parent widget rebuilds the chip with the new value.

The callback provided to [onSelected] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt.

The [onSelected] and [TappableChipAttributes.onPressed] callbacks must not both be specified at the same time.

{@tool snippet}

A [StatefulWidget] that illustrates use of onSelected in an [InputChip].

```dart
class Wood extends StatefulWidget {
  const Wood({super.key});

  @override
  State<StatefulWidget> createState() => WoodState();
}

class WoodState extends State<Wood> {
  bool _useChisel = false;

  @override
  Widget build(BuildContext context) {
    return InputChip(
      label: const Text('Use Chisel'),
      selected: _useChisel,
      onSelected: (bool newValue) {
        setState(() {
          _useChisel = newValue;
        });
      },
    );
  }
}
```

{@end-tool}

### pressElevation

```dart
double? get pressElevation
```

Elevation to be applied on the chip relative to its parent during the press motion.

This controls the size of the shadow below the chip.

Defaults to 8. The value is always non-negative.

### selectedColor

```dart
Color? get selectedColor
```

Color to be used for the chip's background, indicating that it is selected.

The chip is selected when [selected] is true.

### selectedShadowColor

```dart
Color? get selectedShadowColor
```

Color of the chip's shadow when the elevation is greater than 0 and the chip is selected.

The default is [Colors.black].

### tooltip

```dart
String? get tooltip
```

Tooltip string to be used for the body area (where the label and avatar are) of the chip.

### avatarBorder

```dart
ShapeBorder get avatarBorder
```

The shape of the translucent highlight painted over the avatar when the [selected] property is true.

Only the outer path of the shape is used.

Defaults to [CircleBorder].

# DisabledChipAttributes

```dart
abstract interface class DisabledChipAttributes {}
```

An interface for Material Design chips that can be enabled and disabled.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- <https://material.io/design/components/chips.html>

### isEnabled

```dart
bool get isEnabled
```

Whether or not this chip is enabled for input.

If this is true, but all of the user action callbacks are null (i.e. [SelectableChipAttributes.onSelected], [TappableChipAttributes.onPressed], and [DeletableChipAttributes.onDeleted]), then the control will still be shown as disabled.

This is typically used if you want the chip to be disabled, but also show a delete button.

For classes which don't have this as a constructor argument, [isEnabled] returns true if their user action callback is set.

Defaults to true.

### disabledColor

```dart
Color? get disabledColor
```

The color used for the chip's background to indicate that it is not enabled.

The chip is disabled when [isEnabled] is false, or all three of [SelectableChipAttributes.onSelected], [TappableChipAttributes.onPressed], and [DeletableChipAttributes.onDeleted] are null.

It defaults to [Colors.black38].

# TappableChipAttributes

```dart
abstract interface class TappableChipAttributes {}
```

An interface for Material Design chips that can be tapped.

The defaults mentioned in the documentation for each attribute are what the implementing classes typically use for defaults (but this class doesn't provide or enforce them).

See also:

- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- <https://material.io/design/components/chips.html>

### onPressed

```dart
VoidCallback? get onPressed
```

Called when the user taps the chip.

If [onPressed] is set, then this callback will be called when the user taps on the label or avatar parts of the chip. If [onPressed] is null, then the chip will be disabled.

{@tool snippet}

```dart
class Blacksmith extends StatelessWidget {
  const Blacksmith({super.key});

  void startHammering() {
    print('bang bang bang');
  }

  @override
  Widget build(BuildContext context) {
    return InputChip(
      label: const Text('Apply Hammer'),
      onPressed: startHammering,
    );
  }
}
```

{@end-tool}

### pressElevation

```dart
double? get pressElevation
```

Elevation to be applied on the chip relative to its parent during the press motion.

This controls the size of the shadow below the chip.

Defaults to 8. The value is always non-negative.

### tooltip

```dart
String? get tooltip
```

Tooltip string to be used for the body area (where the label and avatar are) of the chip.

# ChipAnimationStyle

```dart
class ChipAnimationStyle {}
```

A helper class that overrides the default chip animation parameters.

### ChipAnimationStyle()

```dart
ChipAnimationStyle({AnimationStyle? enableAnimation, AnimationStyle? selectAnimation, AnimationStyle? avatarDrawerAnimation, AnimationStyle? deleteDrawerAnimation})
```

Creates an instance of Chip Animation Style class.

### enableAnimation

```dart
AnimationStyle? enableAnimation
```

If [enableAnimation] with duration or reverse duration is provided, it will be used to override the chip enable and disable animation durations. If it is null, then default duration will be 75ms.

### selectAnimation

```dart
AnimationStyle? selectAnimation
```

If [selectAnimation] with duration or reverse duration is provided, it will be used to override the chip select and unselect animation durations. If it is null, then default duration will be 195ms.

### avatarDrawerAnimation

```dart
AnimationStyle? avatarDrawerAnimation
```

If [avatarDrawerAnimation] with duration or reverse duration is provided, it will be used to override the chip checkmark animation duration. If it is null, then default duration will be 150ms.

### deleteDrawerAnimation

```dart
AnimationStyle? deleteDrawerAnimation
```

If [deleteDrawerAnimation] with duration or reverse duration is provided, it will be used to override the chip delete icon animation duration. If it is null, then default duration will be 150ms.

# Chip

```dart
class Chip extends StatelessWidget implements ChipAttributes, DeletableChipAttributes {}
```

A Material Design chip.

Chips are compact elements that represent an attribute, text, entity, or action.

Supplying a non-null [onDeleted] callback will cause the chip to include a button for deleting the chip.

Its ancestors must include [Material], [MediaQuery], [Directionality], and [MaterialLocalizations]. Typically all of these widgets are provided by [MaterialApp] and [Scaffold]. The [label] and [clipBehavior] arguments must not be null.

{@tool snippet}

```dart
Chip(
  avatar: CircleAvatar(
    backgroundColor: Colors.grey.shade800,
    child: const Text('AB'),
  ),
  label: const Text('Aaron Burr'),
)
```

{@end-tool}

See also:

- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- [CircleAvatar], which shows images or initials of entities.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### Chip()

```dart
Chip({dynamic key, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? labelPadding, Widget? deleteIcon, VoidCallback? onDeleted, Color? deleteIconColor, String? deleteButtonTooltipMessage, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Creates a Material Design chip.

The [elevation] must be null or non-negative.

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

# RawChip

```dart
class RawChip extends StatefulWidget implements ChipAttributes, DeletableChipAttributes, SelectableChipAttributes, CheckmarkableChipAttributes, DisabledChipAttributes, TappableChipAttributes {}
```

A raw Material Design chip.

This serves as the basis for all of the chip widget types to aggregate. It is typically not created directly, one of the other chip types that are appropriate for the use case are used instead:

- [Chip] a simple chip that can only display information and be deleted.
- [InputChip] represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip] allows a single selection from a set of options.
- [FilterChip] a chip that uses tags or descriptive words as a way to filter content.
- [ActionChip]s display a set of actions related to primary content.

Raw chips are typically only used if you want to create your own custom chip type.

Raw chips can be selected by setting [onSelected], deleted by setting [onDeleted], and pushed like a button with [onPressed]. They have a [label], and they can have a leading icon (see [avatar]) and a trailing icon ([deleteIcon]). Colors and padding can be customized.

Requires one of its ancestors to be a [Material] widget.

See also:

- [CircleAvatar], which shows images or initials of people.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- <https://material.io/design/components/chips.html>

### RawChip()

```dart
RawChip({dynamic key, ChipThemeData? defaultProperties, Widget? avatar, required Widget label, TextStyle? labelStyle, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, EdgeInsetsGeometry? labelPadding, Widget? deleteIcon, VoidCallback? onDeleted, Color? deleteIconColor, String? deleteButtonTooltipMessage, VoidCallback? onPressed, ValueChanged<bool>? onSelected, double? pressElevation, bool tapEnabled = true, bool selected = false, bool isEnabled = true, Color? disabledColor, Color? selectedColor, String? tooltip, BorderSide? side, OutlinedBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, WidgetStateProperty<Color?>? color, Color? backgroundColor, MaterialTapTargetSize? materialTapTargetSize, double? elevation, Color? shadowColor, Color? surfaceTintColor, IconThemeData? iconTheme, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, ShapeBorder avatarBorder = const CircleBorder(), BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints, ChipAnimationStyle? chipAnimationStyle, MouseCursor? mouseCursor})
```

Creates a RawChip.

The [onPressed] and [onSelected] callbacks must not both be specified at the same time.

The [pressElevation] and [elevation] must be null or non-negative. Typically, [pressElevation] is greater than [elevation].

### defaultProperties

```dart
ChipThemeData? defaultProperties
```

Defines the defaults for the chip properties if they are not specified elsewhere.

If null then [ChipThemeData.fromDefaults] will be used for the default properties.

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

### deleteIcon

```dart
Widget deleteIcon
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

### onSelected

```dart
ValueChanged<bool>? onSelected
```

### onPressed

```dart
VoidCallback? onPressed
```

### pressElevation

```dart
double? pressElevation
```

### selected

```dart
bool selected
```

### isEnabled

```dart
bool isEnabled
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

### iconTheme

```dart
IconThemeData? iconTheme
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

### tapEnabled

```dart
bool tapEnabled
```

If set, this indicates that the chip should be disabled if all of the tap callbacks ([onSelected], [onPressed]) are null.

For example, the [Chip] class sets this to false because it can't be disabled, even if no callbacks are set on it, since it is used for displaying information only.

Defaults to true.

### createState()

```dart
State<RawChip> createState()
```
