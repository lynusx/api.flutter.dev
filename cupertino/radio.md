@docImport 'package:flutter/material.dart';

@docImport 'checkbox.dart'; @docImport 'slider.dart'; @docImport 'switch.dart';

# CupertinoRadio

```dart
class CupertinoRadio<T> extends StatefulWidget {}
```

A widget that builds a [RawRadio] with a macOS-style UI.

{@youtube 560 315 https://www.youtube.com/watch?v=D0xwcz2IqAY}

Used to select between a number of mutually exclusive values. When one radio button in a group is selected, the other radio buttons in the group are deselected. The values are of type `T`, the type parameter of the [CupertinoRadio] class. Enums are commonly used for this purpose.

This widget typically has a [RadioGroup] ancestor, which takes in a [RadioGroup.groupValue], and the [CupertinoRadio] under it with matching [value] will be selected.

{@tool dartpad} Here is an example of CupertinoRadio widgets wrapped in CupertinoListTiles.

The currently selected character is passed into `RadioGroup.groupValue`, which is maintained by the example's `State`. In this case, the first [CupertinoRadio] will start off selected because `_character` is initialized to `SingingCharacter.lafayette`.

If the second radio button is pressed, the example's state is updated with `setState`, updating `_character` to `SingingCharacter.jefferson`. This causes the buttons to rebuild with the updated `RadioGroup.groupValue`, and therefore the selection of the second button.

** See code in examples/api/lib/cupertino/radio/cupertino_radio.0.dart ** {@end-tool}

See also:

- [CupertinoSlider], for selecting a value in a range.
- [CupertinoCheckbox] and [CupertinoSwitch], for toggling a particular value on or off.
- [Radio], the Material Design equivalent.
- <https://developer.apple.com/design/human-interface-guidelines/components/selection-and-input/toggles/>

### CupertinoRadio()

```dart
CupertinoRadio({dynamic key, required T value, T? groupValue, ValueChanged<T?>? onChanged, MouseCursor? mouseCursor, bool toggleable = false, Color? activeColor, Color? inactiveColor, Color? fillColor, Color? focusColor, FocusNode? focusNode, bool autofocus = false, bool useCheckmarkStyle = false, bool? enabled, RadioGroupRegistry<T>? groupRegistry})
```

Creates a macOS-styled radio button.

The following arguments are required:

- [value] and [groupValue] together determine whether the radio button is selected.
- [onChanged] is called when the user selects this radio button.

### value

```dart
T value
```

{@macro flutter.widget.RawRadio.value}

### groupValue

```dart
T? groupValue
```

{@macro flutter.material.Radio.groupValue}

### onChanged

```dart
ValueChanged<T?>? onChanged
```

{@macro flutter.material.Radio.onChanged}

For example:

```dart
CupertinoRadio<SingingCharacter>(
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

{@macro flutter.widget.RawRadio.mouseCursor}

If null, then [SystemMouseCursors.basic] is used when this radio button is disabled. When this radio button is enabled, [SystemMouseCursors.click] is used on Web, and [SystemMouseCursors.basic] is used on other platforms.

See also:

- [WidgetStateMouseCursor], a [MouseCursor] that implements `WidgetStateProperty` which is used in APIs that need to accept either a [MouseCursor] or a [WidgetStateProperty<MouseCursor>].

### toggleable

```dart
bool toggleable
```

{@macro flutter.widget.RawRadio.toggleable}

{@tool dartpad} This example shows how to enable deselecting a radio button by setting the [toggleable] attribute.

** See code in examples/api/lib/cupertino/radio/cupertino_radio.toggleable.0.dart ** {@end-tool}

### useCheckmarkStyle

```dart
bool useCheckmarkStyle
```

Controls whether the radio displays in a checkbox style or the default iOS radio style.

Defaults to false.

### activeColor

```dart
Color? activeColor
```

The color to use when this radio button is selected.

Defaults to [CupertinoColors.activeBlue].

### inactiveColor

```dart
Color? inactiveColor
```

The color to use when this radio button is not selected.

Defaults to [CupertinoColors.white].

### fillColor

```dart
Color? fillColor
```

The color that fills the inner circle of the radio button when selected.

Defaults to [CupertinoColors.white].

### focusColor

```dart
Color? focusColor
```

The color for the radio's border when it has the input focus.

If null, then a paler form of the [activeColor] will be used.

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

{@macro flutter.material.Radio.enabled}

### createState()

```dart
State<CupertinoRadio<T>> createState()
```
