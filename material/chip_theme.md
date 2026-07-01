@docImport 'action_chip.dart'; @docImport 'chip.dart'; @docImport 'choice_chip.dart'; @docImport 'circle_avatar.dart'; @docImport 'filter_chip.dart'; @docImport 'input_chip.dart'; @docImport 'material.dart';

# ChipTheme

```dart
class ChipTheme extends InheritedTheme {}
```

Applies a chip theme to descendant [RawChip]-based widgets, like [Chip], [InputChip], [ChoiceChip], [FilterChip], and [ActionChip].

A chip theme describes the color, shape and text styles for the chips it is applied to.

Descendant widgets obtain the current theme's [ChipThemeData] object using [ChipTheme.of]. When a widget uses [ChipTheme.of], it is automatically rebuilt if the theme later changes.

The [ThemeData] object given by the [Theme.of] call also contains a default [ThemeData.chipTheme] that can be customized by copying it (using [ChipThemeData.copyWith]).

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- [ChipThemeData], which describes the actual configuration of a chip theme.
- [ThemeData], which describes the overall theme information for the application.

### ChipTheme()

```dart
ChipTheme({dynamic key, required ChipThemeData data, required dynamic child})
```

Applies the given theme [data] to [child].

### data

```dart
ChipThemeData data
```

Specifies the color, shape, and text style values for descendant chip widgets.

### of()

```dart
ChipThemeData of(BuildContext context)
```

Returns the data from the closest [ChipTheme] instance that encloses the given context.

Defaults to the ambient [ThemeData.chipTheme] if there is no [ChipTheme] in the given build context.

{@tool snippet}

```dart
class Spaceship extends StatelessWidget {
  const Spaceship({super.key});

  @override
  Widget build(BuildContext context) {
    return ChipTheme(
      data: ChipTheme.of(context).copyWith(backgroundColor: Colors.red),
      child: ActionChip(
        label: const Text('Launch'),
        onPressed: () { print('We have liftoff!'); },
      ),
    );
  }
}
```

{@end-tool}

See also:

- [ChipThemeData], which describes the actual configuration of a chip theme.

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ChipTheme oldWidget)
```

# ChipThemeData

```dart
class ChipThemeData with Diagnosticable {}
```

Holds the color, shape, and text styles for a Material Design chip theme.

Use this class to configure a [ChipTheme] widget, or to set the [ThemeData.chipTheme] for a [Theme] widget.

To obtain the current ambient chip theme, use [ChipTheme.of].

The parts of a chip are:

- The "avatar", which is a widget that appears at the beginning of the chip. This is typically a [CircleAvatar] widget.
- The "label", which is the widget displayed in the center of the chip. Typically this is a [Text] widget.
- The "delete icon", which is a widget that appears at the end of the chip.
- The chip is disabled when it is not accepting user input. Only some chips have a disabled state: [ActionChip], [ChoiceChip], [FilterChip], and [InputChip].

The simplest way to create a ChipThemeData is to use [copyWith] on the one you get from [ChipTheme.of], or create an entirely new one with [ChipThemeData.fromDefaults].

{@tool snippet}

```dart
class CarColor extends StatefulWidget {
  const CarColor({super.key});

  @override
  State createState() => _CarColorState();
}

class _CarColorState extends State<CarColor> {
  Color _color = Colors.red;

  @override
  Widget build(BuildContext context) {
    return ChipTheme(
      data: ChipTheme.of(context).copyWith(backgroundColor: Colors.lightBlue),
      child: ChoiceChip(
        label: const Text('Light Blue'),
        onSelected: (bool value) {
          setState(() {
            _color = value ? Colors.lightBlue : Colors.red;
          });
        },
        selected: _color == Colors.lightBlue,
      ),
    );
  }
}
```

{@end-tool}

See also:

- [Chip], a chip that displays information and can be deleted.
- [InputChip], a chip that represents a complex piece of information, such as an entity (person, place, or thing) or conversational text, in a compact form.
- [ChoiceChip], allows a single selection from a set of options. Choice chips contain related descriptive text or categories.
- [FilterChip], uses tags or descriptive words as a way to filter content.
- [ActionChip], represents an action related to primary content.
- [CircleAvatar], which shows images or initials of entities.
- [Wrap], A widget that displays its children in multiple horizontal or vertical runs.
- [ChipTheme] widget, which can override the chip theme of its children.
- [Theme] widget, which performs a similar function to [ChipTheme], but for overall themes.
- [ThemeData], which has a default [ChipThemeData].

### ChipThemeData()

```dart
ChipThemeData({WidgetStateProperty<Color?>? color, Color? backgroundColor, Color? deleteIconColor, Color? disabledColor, Color? selectedColor, Color? secondarySelectedColor, Color? shadowColor, Color? surfaceTintColor, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, EdgeInsetsGeometry? labelPadding, EdgeInsetsGeometry? padding, BorderSide? side, OutlinedBorder? shape, TextStyle? labelStyle, TextStyle? secondaryLabelStyle, Brightness? brightness, double? elevation, double? pressElevation, IconThemeData? iconTheme, BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints})
```

Create a [ChipThemeData] given a set of exact values. All the values must be specified except for [shadowColor], [selectedShadowColor], [elevation], and [pressElevation], which may be null.

This will rarely be used directly. It is used by [lerp] to create intermediate themes based on two themes.

### ChipThemeData.fromDefaults()

```dart
ChipThemeData.fromDefaults({Brightness? brightness, Color? primaryColor, required Color secondaryColor, required TextStyle labelStyle})
```

Generates a ChipThemeData from a brightness, a primary color, and a text style.

The [brightness] is used to select a primary color from the default values.

The optional [primaryColor] is used as the base color for the other colors. The opacity of the [primaryColor] is ignored. If a [primaryColor] is specified, then the [brightness] is ignored, and the theme brightness is determined from the [primaryColor].

Only one of [primaryColor] or [brightness] may be specified.

The [secondaryColor] is used for the selection colors needed by [ChoiceChip].

This is used to generate the default chip theme for a [ThemeData].

### color

```dart
WidgetStateProperty<Color?>? color
```

Overrides the default for [ChipAttributes.color].

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default for [ChipAttributes.backgroundColor] which is used for unselected, enabled chip backgrounds.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### deleteIconColor

```dart
Color? deleteIconColor
```

Overrides the default for [DeletableChipAttributes.deleteIconColor].

This property applies to [Chip], [InputChip], [RawChip].

### disabledColor

```dart
Color? disabledColor
```

Overrides the default for [DisabledChipAttributes.disabledColor], the background color which indicates that the chip is not enabled.

This property applies to [ActionChip], [ChoiceChip], [FilterChip], [InputChip], and [RawChip].

### selectedColor

```dart
Color? selectedColor
```

Overrides the default for [SelectableChipAttributes.selectedColor], the background color that indicates that the chip is selected.

This property applies to [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### secondarySelectedColor

```dart
Color? secondarySelectedColor
```

Overrides the default for [ChoiceChip.selectedColor], the background color that indicates that the chip is selected.

### shadowColor

```dart
Color? shadowColor
```

Overrides the default for [ChipAttributes.shadowColor], the Color of the chip's shadow when its elevation is greater than 0.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default for [ChipAttributes.surfaceTintColor], the Color of the chip's surface tint overlay when its elevation is greater than 0.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### selectedShadowColor

```dart
Color? selectedShadowColor
```

Overrides the default for [SelectableChipAttributes.selectedShadowColor], the Color of the chip's shadow when its elevation is greater than 0 and the chip is selected.

This property applies to [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### showCheckmark

```dart
bool? showCheckmark
```

Overrides the default for [CheckmarkableChipAttributes.showCheckmark], which indicates if a check mark should be shown.

This property applies to [FilterChip], [InputChip], [RawChip].

### checkmarkColor

```dart
Color? checkmarkColor
```

Overrides the default for [CheckmarkableChipAttributes.checkmarkColor].

This property applies to [FilterChip], [InputChip], [RawChip].

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

Overrides the default for [ChipAttributes.labelPadding], the padding around the chip's label widget.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### padding

```dart
EdgeInsetsGeometry? padding
```

Overrides the default for [ChipAttributes.padding], the padding between the contents of the chip and the outside [shape].

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### side

```dart
BorderSide? side
```

Overrides the default for [ChipAttributes.side], the color and weight of the chip's outline.

This value is combined with [shape] to create a shape decorated with an outline. If it is a [WidgetStateBorderSide], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.pressed].

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### shape

```dart
OutlinedBorder? shape
```

Overrides the default for [ChipAttributes.shape], the shape of border to draw around the chip.

This shape is combined with [side] to create a shape decorated with an outline. If it is a [WidgetStateOutlinedBorder], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.disabled].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.pressed].

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### labelStyle

```dart
TextStyle? labelStyle
```

Overrides the default for [ChipAttributes.labelStyle], the style of the [DefaultTextStyle] that contains the chip's label.

This only has an effect on label widgets that respect the [DefaultTextStyle], such as [Text].

This property applies to [ActionChip], [Chip], [FilterChip], [InputChip], [RawChip].

### secondaryLabelStyle

```dart
TextStyle? secondaryLabelStyle
```

Overrides the default for [ChoiceChip.labelStyle], the style of the [DefaultTextStyle] that contains the chip's label.

This only has an effect on label widgets that respect the [DefaultTextStyle], such as [Text].

### brightness

```dart
Brightness? brightness
```

Overrides the default value for all chips which affects various base material color choices in the chip rendering.

### elevation

```dart
double? elevation
```

Overrides the default for [ChipAttributes.elevation], the elevation of the chip's [Material].

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### pressElevation

```dart
double? pressElevation
```

Overrides the default for [TappableChipAttributes.pressElevation], the elevation of the chip's [Material] during a "press" or tap down.

This property applies to [ActionChip], [InputChip], [RawChip].

### iconTheme

```dart
IconThemeData? iconTheme
```

Overrides the default for [ChipAttributes.iconTheme], the theme used for all icons in the chip.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### avatarBoxConstraints

```dart
BoxConstraints? avatarBoxConstraints
```

Overrides the default for [ChipAttributes.avatarBoxConstraints], the size constraints for the avatar widget.

This property applies to [ActionChip], [Chip], [ChoiceChip], [FilterChip], [InputChip], [RawChip].

### deleteIconBoxConstraints

```dart
BoxConstraints? deleteIconBoxConstraints
```

Overrides the default for [DeletableChipAttributes.deleteIconBoxConstraints]. the size constraints for the delete icon widget.

This property applies to [Chip], [FilterChip], [InputChip], [RawChip].

### copyWith()

```dart
ChipThemeData copyWith({WidgetStateProperty<Color?>? color, Color? backgroundColor, Color? deleteIconColor, Color? disabledColor, Color? selectedColor, Color? secondarySelectedColor, Color? shadowColor, Color? surfaceTintColor, Color? selectedShadowColor, bool? showCheckmark, Color? checkmarkColor, EdgeInsetsGeometry? labelPadding, EdgeInsetsGeometry? padding, BorderSide? side, OutlinedBorder? shape, TextStyle? labelStyle, TextStyle? secondaryLabelStyle, Brightness? brightness, double? elevation, double? pressElevation, IconThemeData? iconTheme, BoxConstraints? avatarBoxConstraints, BoxConstraints? deleteIconBoxConstraints})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
ChipThemeData? lerp(ChipThemeData? a, ChipThemeData? b, double t)
```

Linearly interpolate between two chip themes.

{@macro dart.ui.shadow.lerp}

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
