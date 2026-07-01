@docImport 'package:flutter/cupertino.dart';

@docImport 'checkbox_list_tile.dart'; @docImport 'color_scheme.dart'; @docImport 'constants.dart'; @docImport 'ink_well.dart'; @docImport 'material.dart'; @docImport 'scaffold.dart'; @docImport 'switch_list_tile.dart'; @docImport 'switch_theme.dart';

# RadioListTile

```dart
class RadioListTile<T> extends StatefulWidget {}
```

A [ListTile] with a [Radio]. In other words, a radio button with a label.

The entire list tile is interactive: tapping anywhere in the tile selects the radio button.

This widget typically has a [RadioGroup] ancestor, which takes in a [RadioGroup.groupValue], and the [RadioListTile] under it with matching [value] will be selected.

The [title], [subtitle], [isThreeLine], and [dense] properties are like those of the same name on [ListTile].

The [selected] property on this widget is similar to the [ListTile.selected] property. The [fillColor] in the selected state is used for the selected item's text color. If it is null, the [activeColor] is used.

This widget does not coordinate the [selected] state and the [checked] state; to have the list tile appear selected when the radio button is the selected radio button, set [selected] to true when [value] matches [RadioGroup.groupValue].

The radio button is shown on the left by default in left-to-right languages (i.e. the leading edge). This can be changed using [controlAffinity]. The [secondary] widget is placed on the opposite side. This maps to the [ListTile.leading] and [ListTile.trailing] properties of [ListTile].

This widget requires a [Material] widget ancestor in the tree to paint itself on, which is typically provided by the app's [Scaffold]. The [tileColor], and [selectedTileColor] are not painted by the [RadioListTile] itself but by the [Material] widget ancestor. In this case, one can wrap a [Material] widget around the [RadioListTile], e.g.:

{@tool snippet}

```dart
const ColoredBox(
  color: Colors.green,
  child: Material(
    child: RadioListTile<Meridiem>(
      tileColor: Colors.red,
      title: Text('AM'),
      value: Meridiem.am,
    ),
  ),
)
```

{@end-tool}

## Performance considerations when wrapping [RadioListTile] with [Material]

Wrapping a large number of [RadioListTile]s individually with [Material]s is expensive. Consider only wrapping the [RadioListTile]s that require it or include a common [Material] ancestor where possible.

{@tool dartpad} ![RadioListTile sample](https://flutter.github.io/assets-for-api-docs/assets/material/radio_list_tile.png)

This widget shows a pair of radio buttons that control the `_character` field. The field is of the type `SingingCharacter`, an enum.

** See code in examples/api/lib/material/radio_list_tile/radio_list_tile.0.dart ** {@end-tool}

{@tool dartpad} This sample demonstrates how [RadioListTile] positions the radio widget relative to the text in different configurations.

** See code in examples/api/lib/material/radio_list_tile/radio_list_tile.1.dart ** {@end-tool}

## Semantics in RadioListTile

Since the entirety of the RadioListTile is interactive, it should represent itself as a single interactive entity.

To do so, a RadioListTile widget wraps its children with a [MergeSemantics] widget. [MergeSemantics] will attempt to merge its descendant [Semantics] nodes into one node in the semantics tree. Therefore, RadioListTile will throw an error if any of its children requires its own [Semantics] node.

For example, you cannot nest a [RichText] widget as a descendant of RadioListTile. [RichText] has an embedded gesture recognizer that requires its own [Semantics] node, which directly conflicts with RadioListTile's desire to merge all its descendants' semantic nodes into one. Therefore, it may be necessary to create a custom radio tile widget to accommodate similar use cases.

{@tool dartpad} ![Radio list tile semantics sample](https://flutter.github.io/assets-for-api-docs/assets/material/radio_list_tile_semantics.png)

Here is an example of a custom labeled radio widget, called LinkedLabelRadio, that includes an interactive [RichText] widget that handles tap gestures.

** See code in examples/api/lib/material/radio_list_tile/custom_labeled_radio.0.dart ** {@end-tool}

## RadioListTile isn't exactly what I want

If the way RadioListTile pads and positions its elements isn't quite what you're looking for, you can create custom labeled radio widgets by combining [Radio] with other widgets, such as [Text], [Padding] and [InkWell].

{@tool dartpad} ![Custom radio list tile sample](https://flutter.github.io/assets-for-api-docs/assets/material/radio_list_tile_custom.png)

Here is an example of a custom LabeledRadio widget, but you can easily make your own configurable widget.

** See code in examples/api/lib/material/radio_list_tile/custom_labeled_radio.1.dart ** {@end-tool}

See also:

- [ListTileTheme], which can be used to affect the style of list tiles, including radio list tiles.
- [CheckboxListTile], a similar widget for checkboxes.
- [SwitchListTile], a similar widget for switches.
- [ListTile] and [Radio], the widgets from which this widget is made.

### RadioListTile()

```dart
RadioListTile({dynamic key, required T value, T? groupValue, ValueChanged<T?>? onChanged, MouseCursor? mouseCursor, bool toggleable = false, Color? activeColor, WidgetStateProperty<Color?>? fillColor, Color? hoverColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, Widget? title, Widget? subtitle, bool? isThreeLine, bool? dense, Widget? secondary, bool selected = false, ListTileControlAffinity? controlAffinity, bool autofocus = false, EdgeInsetsGeometry? contentPadding, ShapeBorder? shape, Color? tileColor, Color? selectedTileColor, VisualDensity? visualDensity, FocusNode? focusNode, WidgetStatesController? statesController, ValueChanged<bool>? onFocusChange, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, double radioScaleFactor = 1.0, ListTileTitleAlignment? titleAlignment, bool? enabled, bool internalAddSemanticForOnTap = false, WidgetStateProperty<Color?>? radioBackgroundColor, BorderSide? radioSide, WidgetStateProperty<double?>? radioInnerRadius})
```

Creates a combination of a list tile and a radio button.

This widget typically has a [RadioGroup] ancestor, which takes in a [RadioGroup.groupValue], and the [RadioListTile] under it with matching [value] will be selected.

[value] must be provided

### RadioListTile.adaptive()

```dart
RadioListTile.adaptive({dynamic key, required T value, T? groupValue, ValueChanged<T?>? onChanged, MouseCursor? mouseCursor, bool toggleable = false, Color? activeColor, WidgetStateProperty<Color?>? fillColor, Color? hoverColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, Widget? title, Widget? subtitle, bool? isThreeLine, bool? dense, Widget? secondary, bool selected = false, ListTileControlAffinity? controlAffinity, bool autofocus = false, EdgeInsetsGeometry? contentPadding, ShapeBorder? shape, Color? tileColor, Color? selectedTileColor, VisualDensity? visualDensity, FocusNode? focusNode, WidgetStatesController? statesController, ValueChanged<bool>? onFocusChange, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, double radioScaleFactor = 1.0, bool? enabled, bool useCupertinoCheckmarkStyle = false, ListTileTitleAlignment? titleAlignment, bool internalAddSemanticForOnTap = false, WidgetStateProperty<Color?>? radioBackgroundColor, BorderSide? radioSide, WidgetStateProperty<double?>? radioInnerRadius})
```

Creates a combination of a list tile and a platform adaptive radio.

The checkbox uses [Radio.adaptive] to show a [CupertinoRadio] for iOS platforms, or [Radio] for all others.

All other properties are the same as [RadioListTile].

### value

```dart
T value
```

The value represented by this radio button.

### groupValue

```dart
T? groupValue
```

The currently selected value for this group of radio buttons.

This radio button is considered selected if its [value] matches the [groupValue].

leave this unassigned or null if building this widget under [RadioGroup].

### onChanged

```dart
ValueChanged<T?>? onChanged
```

Called when the user selects this radio button.

The radio button passes [value] as a parameter to this callback. The radio button does not actually change state until the parent widget rebuilds the radio tile with the new [groupValue].

If null, the radio button will be displayed as disabled.

The provided callback will not be invoked if this radio button is already selected.

The callback provided to [onChanged] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt; for example:

```dart
RadioListTile<SingingCharacter>(
  title: const Text('Lafayette'),
  value: SingingCharacter.lafayette,
  // ignore: deprecated_member_use
  groupValue: _character,
  // ignore: deprecated_member_use
  onChanged: (SingingCharacter? newValue) {
    setState(() {
      _character = newValue;
    });
  },
)
```

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [RadioThemeData.mouseCursor] is used. If that is also null, then [WidgetStateMouseCursor.clickable] is used.

### toggleable

```dart
bool toggleable
```

Set to true if this radio list tile is allowed to be returned to an indeterminate state by selecting it again when selected.

To indicate returning to an indeterminate state, [onChanged] will be called with null.

If true, [RadioGroup.onChanged] is called with [value] when selected while [RadioGroup.groupValue] != [value], and with null when selected again while [RadioGroup.groupValue] == [value].

If false, [RadioGroup.onChanged] will be called with [value] when it is selected while [groupValue] != [value], and only by selecting another radio button in the group (i.e. changing the value of [RadioGroup.groupValue]) can this radio list tile be unselected.

The default is false.

{@tool dartpad} This example shows how to enable deselecting a radio button by setting the [toggleable] attribute.

** See code in examples/api/lib/material/radio_list_tile/radio_list_tile.toggleable.0.dart ** {@end-tool}

### activeColor

```dart
Color? activeColor
```

The color to use when this radio button is selected.

Defaults to [ColorScheme.secondary] of the current [Theme].

### fillColor

```dart
WidgetStateProperty<Color?>? fillColor
```

The color that fills the radio button.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [activeColor] is used in the selected state. If that is also null, then the value of [RadioThemeData.fillColor] is used. If that is also null, then the default value is used.

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@macro flutter.material.radio.materialTapTargetSize}

Defaults to [MaterialTapTargetSize.shrinkWrap].

### hoverColor

```dart
Color? hoverColor
```

{@macro flutter.material.radio.hoverColor}

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The color for the radio's [Material].

Resolves in the following states:

- [WidgetState.pressed].
- [WidgetState.selected].
- [WidgetState.hovered].

If null, then the value of [activeColor] with alpha [kRadialReactionAlpha] and [hoverColor] is used in the pressed and hovered state. If that is also null, the value of [SwitchThemeData.overlayColor] is used. If that is also null, then the default value is used in the pressed and hovered state.

### splashRadius

```dart
double? splashRadius
```

{@macro flutter.material.radio.splashRadius}

If null, then the value of [RadioThemeData.splashRadius] is used. If that is also null, then [kRadialReactionRadius] is used.

### title

```dart
Widget? title
```

The primary content of the list tile.

Typically a [Text] widget.

### subtitle

```dart
Widget? subtitle
```

Additional content displayed below the title.

Typically a [Text] widget.

### secondary

```dart
Widget? secondary
```

A widget to display on the opposite side of the tile from the radio button.

Typically an [Icon] widget.

### isThreeLine

```dart
bool? isThreeLine
```

Whether this list tile is intended to display three lines of text.

If null, the value from [ListTileThemeData.isThreeLine] is used. If that is also null, the value from [ThemeData.listTileTheme] is used. If still null, the default value is `false`.

### dense

```dart
bool? dense
```

Whether this list tile is part of a vertically dense list.

If this property is null then its value is based on [ListTileThemeData.dense].

### selected

```dart
bool selected
```

Whether to render icons and text in the [activeColor].

No effort is made to automatically coordinate the [selected] state and the [checked] state. To have the list tile appear selected when the radio button is the selected radio button, set [selected] to true when [value] matches [RadioGroup.groupValue].

Normally, this property is left to its default value, false.

### controlAffinity

```dart
ListTileControlAffinity? controlAffinity
```

Where to place the control relative to the text.

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

Defines the insets surrounding the contents of the tile.

Insets the [Radio], [title], [subtitle], and [secondary] widgets in [RadioListTile].

When null, `EdgeInsets.symmetric(horizontal: 16.0)` is used.

### shape

```dart
ShapeBorder? shape
```

If specified, [shape] defines the shape of the [RadioListTile]'s [InkWell] border.

### tileColor

```dart
Color? tileColor
```

If specified, defines the background color for `RadioListTile` when [RadioListTile.selected] is false.

### selectedTileColor

```dart
Color? selectedTileColor
```

If non-null, defines the background color when [RadioListTile.selected] is true.

### visualDensity

```dart
VisualDensity? visualDensity
```

Defines how compact the list tile's layout will be.

{@macro flutter.material.themedata.visualDensity}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### statesController

```dart
WidgetStatesController? statesController
```

Controls the interactive states of the backing [ListTile].

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

{@macro flutter.material.inkwell.onFocusChange}

### enableFeedback

```dart
bool? enableFeedback
```

{@macro flutter.material.ListTile.enableFeedback}

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### horizontalTitleGap

```dart
double? horizontalTitleGap
```

{@macro flutter.material.ListTile.horizontalTitleGap}

### minVerticalPadding

```dart
double? minVerticalPadding
```

{@macro flutter.material.ListTile.minVerticalPadding}

### minLeadingWidth

```dart
double? minLeadingWidth
```

{@macro flutter.material.ListTile.minLeadingWidth}

### minTileHeight

```dart
double? minTileHeight
```

{@macro flutter.material.ListTile.minTileHeight}

### titleAlignment

```dart
ListTileTitleAlignment? titleAlignment
```

Defines how [ListTile.leading] and [ListTile.trailing] are vertically aligned relative to the [ListTile]'s titles ([ListTile.title] and [ListTile.subtitle]).

If this property is null then [ListTileThemeData.titleAlignment] is used. If that is also null then [ListTileTitleAlignment.threeLine] is used.

See also:

- [ListTileTheme.of], which returns the nearest [ListTileTheme]'s [ListTileThemeData].

### internalAddSemanticForOnTap

```dart
bool internalAddSemanticForOnTap
```

Whether to add button:true to the semantics if onTap is provided. This is a temporary flag to help changing the behavior of ListTile onTap semantics.

### useCupertinoCheckmarkStyle

```dart
bool useCupertinoCheckmarkStyle
```

Whether to use the checkbox style for the [CupertinoRadio] control.

Only usable under the [RadioListTile.adaptive] constructor. If set to true, on Apple platforms the radio button will appear as an iOS styled checkmark. Controls the [CupertinoRadio] through [CupertinoRadio.useCheckmarkStyle].

Defaults to false.

### radioScaleFactor

```dart
double radioScaleFactor
```

Controls the scaling factor applied to the [Radio] within the [RadioListTile].

Defaults to 1.0.

### enabled

```dart
bool? enabled
```

Whether this widget is interactable.

If not provided, this widget will be interactable if one of the following is true:

- A [onChanged] is provided.
- Having a [RadioGroup] with the same type T above this widget.

If this is set to true, one of the above condition must also be true. Otherwise, an assertion error is thrown.

### radioBackgroundColor

```dart
WidgetStateProperty<Color?>? radioBackgroundColor
```

The color of the background of the radio button, in all [WidgetState]s.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then it is transparent in all states.

### radioSide

```dart
BorderSide? radioSide
```

The side for the circular border of the radio button, in all [WidgetState]s.

This property can be a [BorderSide] or a [WidgetStateBorderSide] to leverage widget state resolution.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then it defaults to a border using the fill color.

### radioInnerRadius

```dart
WidgetStateProperty<double?>? radioInnerRadius
```

The radius of the inner circle of the radio button, in all [WidgetState]s.

Resolves in the following states:

- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then it defaults to `4.5` in all states.

### checked

```dart
bool get checked
```

Whether this radio button is checked.

To control this value, set [value] and [groupValue] appropriately.

### createState()

```dart
State<RadioListTile<T>> createState()
```
