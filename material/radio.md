@docImport 'checkbox.dart'; @docImport 'list_tile.dart'; @docImport 'material.dart'; @docImport 'radio_list_tile.dart'; @docImport 'slider.dart'; @docImport 'switch.dart';

# Radio

```dart
class Radio<T> extends StatefulWidget {}
```

A Material Design radio button.

This widget builds a [RawRadio] with a material UI.

Used to select between a number of mutually exclusive values. When one radio button in a group is selected, the other radio buttons in the group cease to be selected. The values are of type `T`, the type parameter of the [Radio] class. Enums are commonly used for this purpose.

This widget typically has a [RadioGroup] ancestor, which takes in a [RadioGroup.groupValue], and the [Radio] under it with matching [value] will be selected.

{@tool dartpad} Here is an example of Radio widgets wrapped in ListTiles, which is similar to what you could get with the RadioListTile widget.

The currently selected character is passed into `RadioGroup.groupValue`, which is maintained by the example's `State`. In this case, the first [Radio] will start off selected because `_character` is initialized to `SingingCharacter.lafayette`.

If the second radio button is pressed, the example's state is updated with `setState`, updating `_character` to `SingingCharacter.jefferson`. This causes the buttons to rebuild with the updated `RadioGroup.groupValue`, and therefore the selection of the second button.

Requires one of its ancestors to be a [Material] widget.

** See code in examples/api/lib/material/radio/radio.0.dart ** {@end-tool}

{@tool dartpad} Here is an example of how the you can override the default theme of a [Radio] with [WidgetStateProperty].

In this example:

- The first [Radio] uses a custom [fillColor] that changes depending on whether the radio button is selected.
- The second [Radio] applies a different [backgroundColor] based on its selection state.
- The third [Radio] customizes the [side] property to display a different border color when selected or unselected.

** See code in examples/api/lib/material/radio/radio.1.dart ** {@end-tool}

See also:

- [RadioListTile], which combines this widget with a [ListTile] so that you can give the radio button a label.
- [Slider], for selecting a value in a range.
- [Checkbox] and [Switch], for toggling a particular value on or off.
- <https://material.io/design/components/selection-controls.html#radio-buttons>

### Radio()

```dart
Radio({dynamic key, required T value, T? groupValue, ValueChanged<T?>? onChanged, MouseCursor? mouseCursor, bool toggleable = false, Color? activeColor, WidgetStateProperty<Color?>? fillColor, Color? focusColor, Color? hoverColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, FocusNode? focusNode, bool autofocus = false, bool? enabled, RadioGroupRegistry<T>? groupRegistry, WidgetStateProperty<Color?>? backgroundColor, BorderSide? side, WidgetStateProperty<double?>? innerRadius})
```

Creates a Material Design radio button.

This widget typically has a [RadioGroup] ancestor, which takes in a [RadioGroup.groupValue], and the [Radio] under it with matching [value] will be selected.

The [value] is required.

### Radio.adaptive()

```dart
Radio.adaptive({dynamic key, required T value, T? groupValue, ValueChanged<T?>? onChanged, MouseCursor? mouseCursor, bool toggleable = false, Color? activeColor, WidgetStateProperty<Color?>? fillColor, Color? focusColor, Color? hoverColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, FocusNode? focusNode, bool autofocus = false, bool useCupertinoCheckmarkStyle = false, bool? enabled, RadioGroupRegistry<T>? groupRegistry, WidgetStateProperty<Color?>? backgroundColor, BorderSide? side, WidgetStateProperty<double?>? innerRadius})
```

Creates an adaptive [Radio] based on whether the target platform is iOS or macOS, following Material design's [Cross-platform guidelines](https://material.io/design/platform-guidance/cross-platform-adaptation.html).

On iOS and macOS, this constructor creates a [CupertinoRadio], which has matching functionality and presentation as Material checkboxes, and are the graphics expected on iOS. On other platforms, this creates a Material design [Radio].

If a [CupertinoRadio] is created, the following parameters are ignored: [mouseCursor], [fillColor], [hoverColor], [overlayColor], [splashRadius], [materialTapTargetSize], [visualDensity].

[useCupertinoCheckmarkStyle] is used only if a [CupertinoRadio] is created.

The target platform is based on the current [Theme]: [ThemeData.platform].

### value

```dart
T value
```

{@macro flutter.widget.RawRadio.value}

### groupValue

```dart
T? groupValue
```

{@template flutter.material.Radio.groupValue} The currently selected value for a group of radio buttons.

This radio button is considered selected if its [value] matches the [groupValue].

This is deprecated, use [RadioGroup] to manage group value instead. {@endtemplate}

### onChanged

```dart
ValueChanged<T?>? onChanged
```

{@template flutter.material.Radio.onChanged} Called when the user selects this radio button.

The radio button passes [value] as a parameter to this callback. The radio button does not actually change state until the parent widget rebuilds the radio button with the new [groupValue].

If null, the radio button will be displayed as disabled.

The provided callback will not be invoked if this radio button is already selected and [toggleable] is not set to true.

If the [toggleable] is set to true, tapping a already selected radio will invoke this callback with `null` as value.

The callback provided to [onChanged] should update the state of the parent [StatefulWidget] using the [State.setState] method, so that the parent gets rebuilt. {@endtemplate}

For example:

```dart
Radio<SingingCharacter>(
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

This is deprecated, use [RadioGroup] to handle value change instead.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

{@macro flutter.widget.RawRadio.mouseCursor}

If null, the value of [RadioThemeData.mouseCursor] is used. If that is also null, [WidgetStateMouseCursor.adaptiveClickable] is used.

### toggleable

```dart
bool toggleable
```

{@macro flutter.widget.RawRadio.toggleable}

{@tool dartpad} This example shows how to enable deselecting a radio button by setting the [toggleable] attribute.

** See code in examples/api/lib/material/radio/radio.toggleable.0.dart ** {@end-tool}

### activeColor

```dart
Color? activeColor
```

The color to use when this radio button is selected.

Defaults to [ColorScheme.secondary].

If [fillColor] returns a non-null color in the [WidgetState.selected] state, it will be used instead of this color.

### fillColor

```dart
WidgetStateProperty<Color?>? fillColor
```

{@template flutter.material.radio.fillColor} The color that fills the radio button, in all [WidgetState]s.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

{@tool snippet} This example resolves the [fillColor] based on the current [WidgetState] of the [Radio], providing a different [Color] when it is [WidgetState.disabled].

```dart
Radio<int>(
  value: 1,
  fillColor: WidgetStateProperty.resolveWith<Color>((Set<WidgetState> states) {
    if (states.contains(WidgetState.disabled)) {
      return Colors.orange.withValues(alpha: .32);
    }
    return Colors.orange;
  })
)
```

{@end-tool} {@endtemplate}

If null, then the value of [activeColor] is used in the selected state. If that is also null, then the value of [RadioThemeData.fillColor] is used. If that is also null and [ThemeData.useMaterial3] is false, then [ThemeData.disabledColor] is used in the disabled state, [ColorScheme.secondary] is used in the selected state, and [ThemeData.unselectedWidgetColor] is used in the default state; if [ThemeData.useMaterial3] is true, then [ColorScheme.onSurface] is used in the disabled state, [ColorScheme.primary] is used in the selected state and [ColorScheme.onSurfaceVariant] is used in the default state.

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@template flutter.material.radio.materialTapTargetSize} Configures the minimum size of the tap target. {@endtemplate}

If null, then the value of [RadioThemeData.materialTapTargetSize] is used. If that is also null, then the value of [ThemeData.materialTapTargetSize] is used.

See also:

- [MaterialTapTargetSize], for a description of how this affects tap targets.

### visualDensity

```dart
VisualDensity? visualDensity
```

{@template flutter.material.radio.visualDensity} Defines how compact the radio's layout will be. {@endtemplate}

{@macro flutter.material.themedata.visualDensity}

If null, then the value of [RadioThemeData.visualDensity] is used. If that is also null, then the value of [ThemeData.visualDensity] is used.

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### focusColor

```dart
Color? focusColor
```

The color for the radio's [Material] when it has the input focus.

If [overlayColor] returns a non-null color in the [WidgetState.focused] state, it will be used instead.

If null, then the value of [RadioThemeData.overlayColor] is used in the focused state. If that is also null, then the value of [ThemeData.focusColor] is used.

### hoverColor

```dart
Color? hoverColor
```

{@template flutter.material.radio.hoverColor} The color for the radio's [Material] when a pointer is hovering over it.

If [overlayColor] returns a non-null color in the [WidgetState.hovered] state, it will be used instead. {@endtemplate}

If null, then the value of [RadioThemeData.overlayColor] is used in the hovered state. If that is also null, then the value of [ThemeData.hoverColor] is used.

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

{@template flutter.material.radio.overlayColor} The color for the radio's [Material].

Resolves in the following states:

- [WidgetState.pressed].
- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused]. {@endtemplate}

If null, then the value of [activeColor] with alpha [kRadialReactionAlpha], [focusColor] and [hoverColor] is used in the pressed, focused and hovered state. If that is also null, the value of [RadioThemeData.overlayColor] is used. If that is also null, then in Material 2, the value of [ColorScheme.secondary] with alpha [kRadialReactionAlpha], [ThemeData.focusColor] and [ThemeData.hoverColor] is used in the pressed, focused and hovered state. In Material3, the default values are:

- selected * pressed - Theme.colorScheme.onSurface(0.1) * hovered - Theme.colorScheme.primary(0.08) * focused - Theme.colorScheme.primary(0.1)
- pressed - Theme.colorScheme.primary(0.1)
- hovered - Theme.colorScheme.onSurface(0.08)
- focused - Theme.colorScheme.onSurface(0.1)

### splashRadius

```dart
double? splashRadius
```

{@template flutter.material.radio.splashRadius} The splash radius of the circular [Material] ink response. {@endtemplate}

If null, then the value of [RadioThemeData.splashRadius] is used. If that is also null, then [kRadialReactionRadius] is used.

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

### useCupertinoCheckmarkStyle

```dart
bool useCupertinoCheckmarkStyle
```

Controls whether the checkmark style is used in an iOS-style radio.

Only usable under the [Radio.adaptive] constructor. If set to true, on Apple platforms the radio button will appear as an iOS styled checkmark. Controls the [CupertinoRadio] through [CupertinoRadio.useCheckmarkStyle].

Defaults to false.

### groupRegistry

```dart
RadioGroupRegistry<T>? groupRegistry
```

{@macro flutter.widget.RawRadio.groupRegistry}

Unless provided, the [BuildContext] will be used to look up the ancestor [RadioGroupRegistry].

### enabled

```dart
bool? enabled
```

{@template flutter.material.Radio.enabled} Whether this widget is interactive.

If not provided, this widget will be interactable if one of the following is true:

- A [onChanged] is provided.
- Having a [RadioGroup] with the same type T above this widget.
- A [groupRegistry] is provided.

If this is set to true, one of the above condition must also be true. Otherwise, an assertion error is thrown. {@endtemplate}

### backgroundColor

```dart
WidgetStateProperty<Color?>? backgroundColor
```

{@template flutter.material.Radio.backgroundColor} The color of the background of the radio button, in all [WidgetState]s.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If null, then the ambient [RadioThemeData.backgroundColor] is used. If that is also null the default value is transparent in all states.

### side

```dart
BorderSide? side
```

{@template flutter.material.Radio.side} The side for the circular border of the radio button, in all [WidgetState]s.

This property can be a [BorderSide] or a [WidgetStateBorderSide] to leverage widget state resolution.

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If null, then the ambient [RadioThemeData.side] is used. If that is also null, the default value is a border using the fill color.

### innerRadius

```dart
WidgetStateProperty<double?>? innerRadius
```

{@template flutter.material.Radio.innerRadius} The radius of the inner circle of the radio button, in all [WidgetState]s.

Resolves in the following states:

- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If null, then the ambient [RadioThemeData.innerRadius] is used. If that is also null, the default value is `4.5` in all states.

### createState()

```dart
State<Radio<T>> createState()
```
