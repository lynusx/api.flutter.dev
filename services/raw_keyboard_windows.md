@docImport 'hardware_keyboard.dart';

# RawKeyEventDataWindows

```dart
class RawKeyEventDataWindows extends RawKeyEventData {}
```

Platform-specific key event data for Windows.

This class is DEPRECATED. Platform specific key event data will no longer available. See [KeyEvent] for what is available.

This object contains information about key events obtained from Windows's win32 API.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyEventDataWindows()

```dart
RawKeyEventDataWindows({int keyCode = 0, int scanCode = 0, int characterCodePoint = 0, int modifiers = 0})
```

Creates a key event data structure specific for Windows.

### keyCode

```dart
int keyCode
```

The hardware key code corresponding to this key event.

This is the physical key that was pressed, not the Unicode character. See [characterCodePoint] for the Unicode character.

### scanCode

```dart
int scanCode
```

The hardware scan code id corresponding to this key event.

These values are not reliable and vary from device to device, so this information is mainly useful for debugging.

### characterCodePoint

```dart
int characterCodePoint
```

The Unicode code point represented by the key event, if any.

If there is no Unicode code point, this value is zero.

### modifiers

```dart
int modifiers
```

A mask of the current modifiers. The modifier values must be in sync with the Windows embedder. See: https://github.com/flutter/flutter/blob/230240c56880f2c19bf92d2c32203b064054f173/engine/src/flutter/shell/platform/windows/keyboard_key_channel_handler.cc#L44

### keyLabel

```dart
String get keyLabel
```

### physicalKey

```dart
PhysicalKeyboardKey get physicalKey
```

### logicalKey

```dart
LogicalKeyboardKey get logicalKey
```

### isModifierPressed()

```dart
bool isModifierPressed(ModifierKey key, {KeyboardSide side = KeyboardSide.any})
```

### getModifierSide()

```dart
KeyboardSide? getModifierSide(ModifierKey key)
```

### shouldDispatchEvent()

```dart
bool shouldDispatchEvent()
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

### modifierShift

```dart
int modifierShift
```

This mask is used to check the [modifiers] field to test whether one of the SHIFT modifier keys is pressed.

{@template flutter.services.RawKeyEventDataWindows.modifierShift} Use this value if you need to decode the [modifiers] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed. {@endtemplate}

### modifierLeftShift

```dart
int modifierLeftShift
```

This mask is used to check the [modifiers] field to test whether the left SHIFT modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierRightShift

```dart
int modifierRightShift
```

This mask is used to check the [modifiers] field to test whether the right SHIFT modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierControl

```dart
int modifierControl
```

This mask is used to check the [modifiers] field to test whether one of the CTRL modifier keys is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierLeftControl

```dart
int modifierLeftControl
```

This mask is used to check the [modifiers] field to test whether the left CTRL modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierRightControl

```dart
int modifierRightControl
```

This mask is used to check the [modifiers] field to test whether the right CTRL modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierAlt

```dart
int modifierAlt
```

This mask is used to check the [modifiers] field to test whether one of the ALT modifier keys is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierLeftAlt

```dart
int modifierLeftAlt
```

This mask is used to check the [modifiers] field to test whether the left ALT modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierRightAlt

```dart
int modifierRightAlt
```

This mask is used to check the [modifiers] field to test whether the right ALT modifier key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierLeftMeta

```dart
int modifierLeftMeta
```

This mask is used to check the [modifiers] field to test whether the left WIN modifier keys is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierRightMeta

```dart
int modifierRightMeta
```

This mask is used to check the [modifiers] field to test whether the right WIN modifier keys is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierCaps

```dart
int modifierCaps
```

This mask is used to check the [modifiers] field to test whether the CAPS LOCK key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierNumLock

```dart
int modifierNumLock
```

This mask is used to check the [modifiers] field to test whether the NUM LOCK key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}

### modifierScrollLock

```dart
int modifierScrollLock
```

This mask is used to check the [modifiers] field to test whether the SCROLL LOCK key is pressed.

{@macro flutter.services.RawKeyEventDataWindows.modifierShift}
