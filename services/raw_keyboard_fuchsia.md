@docImport 'hardware_keyboard.dart';

# RawKeyEventDataFuchsia

```dart
class RawKeyEventDataFuchsia extends RawKeyEventData {}
```

Platform-specific key event data for Fuchsia.

This class is deprecated and will be removed. Platform specific key event data will no longer be available. See [KeyEvent] for what is available.

This object contains information about key events obtained from Fuchsia's `KeyData` interface.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyEventDataFuchsia()

```dart
RawKeyEventDataFuchsia({int hidUsage = 0, int codePoint = 0, int modifiers = 0})
```

Creates a key event data structure specific for Fuchsia.

### hidUsage

```dart
int hidUsage
```

The USB HID usage.

See <http://www.usb.org/developers/hidpage/Hut1_12v2.pdf> for more information.

### codePoint

```dart
int codePoint
```

The Unicode code point represented by the key event, if any.

If there is no Unicode code point, this value is zero.

Dead keys are represented as Unicode combining characters.

### modifiers

```dart
int modifiers
```

The modifiers that were present when the key event occurred.

See <https://android.googlesource.com/platform/prebuilts/fuchsia_sdk/+/main/fidl/fuchsia.ui.input/input_event_constants.fidl> for the numerical values of the modifiers. Many of these are also replicated as static constants in this class.

See also:

- [modifiersPressed], which returns a Map of currently pressed modifiers and their keyboard side.
- [isModifierPressed], to see if a specific modifier is pressed.
- [isControlPressed], to see if a CTRL key is pressed.
- [isShiftPressed], to see if a SHIFT key is pressed.
- [isAltPressed], to see if an ALT key is pressed.
- [isMetaPressed], to see if a META key is pressed.

### keyLabel

```dart
String get keyLabel
```

### logicalKey

```dart
LogicalKeyboardKey get logicalKey
```

### physicalKey

```dart
PhysicalKeyboardKey get physicalKey
```

### isModifierPressed()

```dart
bool isModifierPressed(ModifierKey key, {KeyboardSide side = KeyboardSide.any})
```

### getModifierSide()

```dart
KeyboardSide? getModifierSide(ModifierKey key)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### modifierNone

```dart
int modifierNone
```

The [modifiers] field indicates that no modifier keys are pressed if it equals this value.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierCapsLock

```dart
int modifierCapsLock
```

This mask is used to check the [modifiers] field to test whether the CAPS LOCK modifier key is on.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftShift

```dart
int modifierLeftShift
```

This mask is used to check the [modifiers] field to test whether the left SHIFT modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightShift

```dart
int modifierRightShift
```

This mask is used to check the [modifiers] field to test whether the right SHIFT modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierShift

```dart
int modifierShift
```

This mask is used to check the [modifiers] field to test whether one of the SHIFT modifier keys is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftControl

```dart
int modifierLeftControl
```

This mask is used to check the [modifiers] field to test whether the left CTRL modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightControl

```dart
int modifierRightControl
```

This mask is used to check the [modifiers] field to test whether the right CTRL modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierControl

```dart
int modifierControl
```

This mask is used to check the [modifiers] field to test whether one of the CTRL modifier keys is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftAlt

```dart
int modifierLeftAlt
```

This mask is used to check the [modifiers] field to test whether the left ALT modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightAlt

```dart
int modifierRightAlt
```

This mask is used to check the [modifiers] field to test whether the right ALT modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierAlt

```dart
int modifierAlt
```

This mask is used to check the [modifiers] field to test whether one of the ALT modifier keys is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftMeta

```dart
int modifierLeftMeta
```

This mask is used to check the [modifiers] field to test whether the left META modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightMeta

```dart
int modifierRightMeta
```

This mask is used to check the [modifiers] field to test whether the right META modifier key is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierMeta

```dart
int modifierMeta
```

This mask is used to check the [modifiers] field to test whether one of the META modifier keys is pressed.

Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.
