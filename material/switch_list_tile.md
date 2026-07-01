@docImport 'package:flutter/cupertino.dart';

@docImport 'checkbox_list_tile.dart'; @docImport 'color_scheme.dart'; @docImport 'constants.dart'; @docImport 'ink_well.dart'; @docImport 'material.dart'; @docImport 'radio_list_tile.dart'; @docImport 'scaffold.dart';

# SwitchListTile

```dart
class SwitchListTile extends StatelessWidget {}
```

A [ListTile] with a [Switch]. In other words, a switch with a label.

{@youtube 560 315 https://www.youtube.com/watch?v=0igIjvtEWNU}

The entire list tile is interactive: tapping anywhere in the tile toggles the switch. Tapping and dragging the [Switch] also triggers the [onChanged] callback.

To ensure that [onChanged] correctly triggers, the state passed into [value] must be properly managed. This is typically done by invoking [State.setState] in [onChanged] to toggle the state value.

The [value], [onChanged], [activeThumbColor], [activeThumbImage], and [inactiveThumbImage] properties of this widget are identical to the similarly-named properties on the [Switch] widget.

The [title], [subtitle], [isThreeLine], and [dense] properties are like those of the same name on [ListTile].

The [selected] property on this widget is similar to the [ListTile.selected] property. This tile's [activeThumbColor] is used for the selected item's text color, or the theme's [SwitchThemeData.overlayColor] if [activeThumbColor] is null.

This widget does not coordinate the [selected] state and the [value]; to have the list tile appear selected when the switch button is on, use the same value for both.

The switch is shown on the right by default in left-to-right languages (i.e. in the [ListTile.trailing] slot) which can be changed using [controlAffinity]. The [secondary] widget is placed in the [ListTile.leading] slot.

This widget requires a [Material] widget ancestor in the tree to paint itself on, which is typically provided by the app's [Scaffold]. The [tileColor], and [selectedTileColor] are not painted by the [SwitchListTile] itself but by the [Material] widget ancestor. In this case, one can wrap a [Material] widget around the [SwitchListTile], e.g.:

{@tool snippet}

```dart
ColoredBox(
  color: Colors.green,
  child: Material(
    child: SwitchListTile(
      tileColor: Colors.red,
      title: const Text('SwitchListTile with red background'),
      value: true,
      onChanged:(bool? value) { },
    ),
  ),
)
```

{@end-tool}

## Performance considerations when wrapping [SwitchListTile] with [Material]

Wrapping a large number of [SwitchListTile]s individually with [Material]s is expensive. Consider only wrapping the [SwitchListTile]s that require it or include a common [Material] ancestor where possible.

To show the [SwitchListTile] as disabled, pass null as the [onChanged] callback.

{@tool dartpad} ![SwitchListTile sample](https://flutter.github.io/assets-for-api-docs/assets/material/switch_list_tile.png)

This widget shows a switch that, when toggled, changes the state of a [bool] member field called `_lights`.

** See code in examples/api/lib/material/switch_list_tile/switch_list_tile.0.dart ** {@end-tool}

{@tool dartpad} This sample demonstrates how [SwitchListTile] positions the switch widget relative to the text in different configurations.

** See code in examples/api/lib/material/switch_list_tile/switch_list_tile.1.dart ** {@end-tool}

## Semantics in SwitchListTile

Since the entirety of the SwitchListTile is interactive, it should represent itself as a single interactive entity.

To do so, a SwitchListTile widget wraps its children with a [MergeSemantics] widget. [MergeSemantics] will attempt to merge its descendant [Semantics] nodes into one node in the semantics tree. Therefore, SwitchListTile will throw an error if any of its children requires its own [Semantics] node.

For example, you cannot nest a [RichText] widget as a descendant of SwitchListTile. [RichText] has an embedded gesture recognizer that requires its own [Semantics] node, which directly conflicts with SwitchListTile's desire to merge all its descendants' semantic nodes into one. Therefore, it may be necessary to create a custom radio tile widget to accommodate similar use cases.

{@tool dartpad} ![Switch list tile semantics sample](https://flutter.github.io/assets-for-api-docs/assets/material/switch_list_tile_semantics.png)

Here is an example of a custom labeled radio widget, called LinkedLabelRadio, that includes an interactive [RichText] widget that handles tap gestures.

** See code in examples/api/lib/material/switch_list_tile/custom_labeled_switch.0.dart ** {@end-tool}

## SwitchListTile isn't exactly what I want

If the way SwitchListTile pads and positions its elements isn't quite what you're looking for, you can create custom labeled switch widgets by combining [Switch] with other widgets, such as [Text], [Padding] and [InkWell].

{@tool dartpad} ![Custom switch list tile sample](https://flutter.github.io/assets-for-api-docs/assets/material/switch_list_tile_custom.png)

Here is an example of a custom LabeledSwitch widget, but you can easily make your own configurable widget.

** See code in examples/api/lib/material/switch_list_tile/custom_labeled_switch.1.dart ** {@end-tool}

See also:

- [ListTileTheme], which can be used to affect the style of list tiles, including switch list tiles.
- [CheckboxListTile], a similar widget for checkboxes.
- [RadioListTile], a similar widget for radio buttons.
- [ListTile] and [Switch], the widgets from which this widget is made.

### SwitchListTile()

```dart
SwitchListTile({dynamic key, required bool value, required ValueChanged<bool>? onChanged, Color? activeColor, Color? activeThumbColor, Color? activeTrackColor, Color? inactiveThumbColor, Color? inactiveTrackColor, ImageProvider? activeThumbImage, ImageErrorListener? onActiveThumbImageError, ImageProvider? inactiveThumbImage, ImageErrorListener? onInactiveThumbImageError, WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackOutlineColor, WidgetStateProperty<Icon?>? thumbIcon, MaterialTapTargetSize? materialTapTargetSize, DragStartBehavior dragStartBehavior = DragStartBehavior.start, MouseCursor? mouseCursor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, FocusNode? focusNode, WidgetStatesController? statesController, ValueChanged<bool>? onFocusChange, bool autofocus = false, Color? tileColor, Widget? title, Widget? subtitle, bool? isThreeLine, bool? dense, EdgeInsetsGeometry? contentPadding, Widget? secondary, bool selected = false, ListTileControlAffinity? controlAffinity, ShapeBorder? shape, Color? selectedTileColor, VisualDensity? visualDensity, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, Color? hoverColor, bool internalAddSemanticForOnTap = false})
```

Creates a combination of a list tile and a switch.

The switch tile itself does not maintain any state. Instead, when the state of the switch changes, the widget calls the [onChanged] callback. Most widgets that use a switch will listen for the [onChanged] callback and rebuild the switch tile with a new [value] to update the visual appearance of the switch.

The following arguments are required:

- [value] determines whether this switch is on or off.
- [onChanged] is called when the user toggles the switch on or off.

### SwitchListTile.adaptive()

```dart
SwitchListTile.adaptive({dynamic key, required bool value, required ValueChanged<bool>? onChanged, Color? activeColor, Color? activeThumbColor, Color? activeTrackColor, Color? inactiveThumbColor, Color? inactiveTrackColor, ImageProvider? activeThumbImage, ImageErrorListener? onActiveThumbImageError, ImageProvider? inactiveThumbImage, ImageErrorListener? onInactiveThumbImageError, WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackOutlineColor, WidgetStateProperty<Icon?>? thumbIcon, MaterialTapTargetSize? materialTapTargetSize, DragStartBehavior dragStartBehavior = DragStartBehavior.start, MouseCursor? mouseCursor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, FocusNode? focusNode, WidgetStatesController? statesController, ValueChanged<bool>? onFocusChange, bool autofocus = false, bool? applyCupertinoTheme, Color? tileColor, Widget? title, Widget? subtitle, bool? isThreeLine, bool? dense, EdgeInsetsGeometry? contentPadding, Widget? secondary, bool selected = false, ListTileControlAffinity? controlAffinity, ShapeBorder? shape, Color? selectedTileColor, VisualDensity? visualDensity, bool? enableFeedback, double? horizontalTitleGap, double? minVerticalPadding, double? minLeadingWidth, double? minTileHeight, Color? hoverColor, bool internalAddSemanticForOnTap = false})
```

Creates a Material [ListTile] with an adaptive [Switch], following Material design's [Cross-platform guidelines](https://material.io/design/platform-guidance/cross-platform-adaptation.html).

This widget uses [Switch.adaptive] to change the graphics of the switch component based on the ambient [ThemeData.platform]. On iOS and macOS, a [CupertinoSwitch] will be used. On other platforms a Material design [Switch] will be used.

If a [CupertinoSwitch] is created, the following parameters are ignored: [activeTrackColor], [inactiveThumbColor], [inactiveTrackColor], [activeThumbImage], [inactiveThumbImage].

### value

```dart
bool value
```

Whether this switch is checked.

### onChanged

```dart
ValueChanged<bool>? onChanged
```

Called when the user toggles the switch on or off.

The switch passes the new value to the callback but does not actually change state until the parent widget rebuilds the switch tile with the new value.

If null, the switch will be displayed as disabled.

The callback provided to [onChanged] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt; for example:

{@tool snippet}

```dart
SwitchListTile(
  value: _isSelected,
  onChanged: (bool newValue) {
    setState(() {
      _isSelected = newValue;
    });
  },
  title: const Text('Selection'),
)
```

{@end-tool}

### activeColor

```dart
Color? activeColor
```

{@macro flutter.material.switch.activeColor}

Defaults to [ColorScheme.secondary] of the current [Theme].

### activeThumbColor

```dart
Color? activeThumbColor
```

{@macro flutter.material.switch.activeThumbColor}

Defaults to [ColorScheme.secondary] of the current [Theme].

### activeTrackColor

```dart
Color? activeTrackColor
```

{@macro flutter.material.switch.activeTrackColor}

Defaults to [ColorScheme.secondary] with the opacity set at 50%.

Ignored if created with [SwitchListTile.adaptive].

### inactiveThumbColor

```dart
Color? inactiveThumbColor
```

{@macro flutter.material.switch.inactiveThumbColor}

Defaults to the colors described in the Material design specification.

Ignored if created with [SwitchListTile.adaptive].

### inactiveTrackColor

```dart
Color? inactiveTrackColor
```

{@macro flutter.material.switch.inactiveTrackColor}

Defaults to the colors described in the Material design specification.

Ignored if created with [SwitchListTile.adaptive].

### activeThumbImage

```dart
ImageProvider? activeThumbImage
```

{@macro flutter.material.switch.activeThumbImage}

### onActiveThumbImageError

```dart
ImageErrorListener? onActiveThumbImageError
```

{@macro flutter.material.switch.onActiveThumbImageError}

### inactiveThumbImage

```dart
ImageProvider? inactiveThumbImage
```

{@macro flutter.material.switch.inactiveThumbImage}

Ignored if created with [SwitchListTile.adaptive].

### onInactiveThumbImageError

```dart
ImageErrorListener? onInactiveThumbImageError
```

{@macro flutter.material.switch.onInactiveThumbImageError}

### thumbColor

```dart
WidgetStateProperty<Color?>? thumbColor
```

The color of this switch's thumb.

Resolved in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [activeThumbColor] is used in the selected state and [inactiveThumbColor] in the default state. If that is also null, then the value of [SwitchThemeData.thumbColor] is used. If that is also null, The default value is used.

### trackColor

```dart
WidgetStateProperty<Color?>? trackColor
```

The color of this switch's track.

Resolved in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [activeTrackColor] is used in the selected state and [inactiveTrackColor] in the default state. If that is also null, then the value of [SwitchThemeData.trackColor] is used. If that is also null, then the default value is used.

### trackOutlineColor

```dart
WidgetStateProperty<Color?>? trackOutlineColor
```

{@macro flutter.material.switch.trackOutlineColor}

The [ListTile] will be focused when this [SwitchListTile] requests focus, so the focused outline color of the switch will be ignored.

In Material 3, the outline color defaults to transparent in the selected state and [ColorScheme.outline] in the unselected state. In Material 2, the [Switch] track has no outline.

### thumbIcon

```dart
WidgetStateProperty<Icon?>? thumbIcon
```

The icon to use on the thumb of this switch

Resolved in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [SwitchThemeData.thumbIcon] is used. If this is also null, then the [Switch] does not have any icons on the thumb.

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@macro flutter.material.switch.materialTapTargetSize}

defaults to [MaterialTapTargetSize.shrinkWrap].

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.cupertino.CupertinoSwitch.dragStartBehavior}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.disabled].

If null, then the value of [SwitchThemeData.mouseCursor] is used. If that is also null, then [WidgetStateMouseCursor.clickable] is used.

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

The color for the switch's [Material].

Resolves in the following states:

- [WidgetState.pressed].
- [WidgetState.selected].
- [WidgetState.hovered].

If null, then the value of [activeThumbColor] with alpha [kRadialReactionAlpha] and [hoverColor] is used in the pressed and hovered state. If that is also null, the value of [SwitchThemeData.overlayColor] is used. If that is also null, then the default value is used in the pressed and hovered state.

### splashRadius

```dart
double? splashRadius
```

{@macro flutter.material.switch.splashRadius}

If null, then the value of [SwitchThemeData.splashRadius] is used. If that is also null, then [kRadialReactionRadius] is used.

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

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### tileColor

```dart
Color? tileColor
```

{@macro flutter.material.ListTile.tileColor}

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

A widget to display on the opposite side of the tile from the switch.

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

### contentPadding

```dart
EdgeInsetsGeometry? contentPadding
```

The tile's internal padding.

Insets a [SwitchListTile]'s contents: its [title], [subtitle], [secondary], and [Switch] widgets.

If null, [ListTile]'s default of `EdgeInsets.symmetric(horizontal: 16.0)` is used.

### selected

```dart
bool selected
```

Whether to render icons and text in the [activeThumbColor].

No effort is made to automatically coordinate the [selected] state and the [value] state. To have the list tile appear selected when the switch is on, pass the same value to both.

Normally, this property is left to its default value, false.

### controlAffinity

```dart
ListTileControlAffinity? controlAffinity
```

Defines the position of control and [secondary], relative to text.

By default, the value of [controlAffinity] is [ListTileControlAffinity.platform].

### shape

```dart
ShapeBorder? shape
```

{@macro flutter.material.ListTile.shape}

### selectedTileColor

```dart
Color? selectedTileColor
```

If non-null, defines the background color when [SwitchListTile.selected] is true.

### visualDensity

```dart
VisualDensity? visualDensity
```

Defines how compact the list tile's layout will be.

{@macro flutter.material.themedata.visualDensity}

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

### hoverColor

```dart
Color? hoverColor
```

The color for the tile's [Material] when a pointer is hovering over it.

### applyCupertinoTheme

```dart
bool? applyCupertinoTheme
```

{@macro flutter.cupertino.CupertinoSwitch.applyTheme}

### internalAddSemanticForOnTap

```dart
bool internalAddSemanticForOnTap
```

Whether to add button:true to the semantics if onTap is provided. This is a temporary flag to help changing the behavior of ListTile onTap semantics.

### build()

```dart
Widget build(BuildContext context)
```
