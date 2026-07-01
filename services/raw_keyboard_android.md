@docImport 'hardware_keyboard.dart';

# RawKeyEventDataAndroid

```dart
class RawKeyEventDataAndroid extends RawKeyEventData {}
```

Platform-specific key event data for Android.

This class is deprecated and will be removed. Platform specific key event data will no longer be available. See [KeyEvent] for what is available.

This object contains information about key events obtained from Android's `KeyEvent` interface.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyEventDataAndroid()

```dart
RawKeyEventDataAndroid({int flags = 0, int codePoint = 0, int plainCodePoint = 0, int keyCode = 0, int scanCode = 0, int metaState = 0, int eventSource = 0, int vendorId = 0, int productId = 0, int deviceId = 0, int repeatCount = 0})
```

Creates a key event data structure specific for Android.

### flags

```dart
int flags
```

The current set of additional flags for this event.

Flags indicate things like repeat state, etc.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getFlags()> for more information.

### codePoint

```dart
int codePoint
```

The Unicode code point represented by the key event, if any.

If there is no Unicode code point, this value is zero.

Dead keys are represented as Unicode combining characters.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getUnicodeChar()> for more information.

### plainCodePoint

```dart
int plainCodePoint
```

The Unicode code point represented by the key event, if any, without regard to any modifier keys which are currently pressed.

If there is no Unicode code point, this value is zero.

Dead keys are represented as Unicode combining characters.

This is the result of calling KeyEvent.getUnicodeChar(0) on Android.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getUnicodeChar(int)> for more information.

### keyCode

```dart
int keyCode
```

The hardware key code corresponding to this key event.

This is the physical key that was pressed, not the Unicode character. See [codePoint] for the Unicode character.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getKeyCode()> for more information.

### scanCode

```dart
int scanCode
```

The hardware scan code id corresponding to this key event.

These values are not reliable and vary from device to device, so this information is mainly useful for debugging.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getScanCode()> for more information.

### metaState

```dart
int metaState
```

The modifiers that were present when the key event occurred.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getMetaState()> for the numerical values of the [metaState]. Many of these constants are also replicated as static constants in this class.

See also:

- [modifiersPressed], which returns a Map of currently pressed modifiers and their keyboard side.
- [isModifierPressed], to see if a specific modifier is pressed.
- [isControlPressed], to see if a CTRL key is pressed.
- [isShiftPressed], to see if a SHIFT key is pressed.
- [isAltPressed], to see if an ALT key is pressed.
- [isMetaPressed], to see if a META key is pressed.

### eventSource

```dart
int eventSource
```

The source of the event.

See <https://developer.android.com/reference/android/view/KeyEvent.html#getSource()> for the numerical values of the `source`. Many of these constants are also replicated as static constants in this class.

### vendorId

```dart
int vendorId
```

The vendor ID of the device that produced the event.

See <https://developer.android.com/reference/android/view/InputDevice.html#getVendorId()> for the numerical values of the [vendorId].

### productId

```dart
int productId
```

The product ID of the device that produced the event.

See <https://developer.android.com/reference/android/view/InputDevice.html#getProductId()> for the numerical values of the [productId].

### deviceId

```dart
int deviceId
```

The ID of the device that produced the event.

See https://developer.android.com/reference/android/view/InputDevice.html#getId()

### repeatCount

```dart
int repeatCount
```

The repeat count of the event.

See <https://developer.android.com/reference/android/view/KeyEvent#getRepeatCount()> for more information.

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

No modifier keys are pressed in the [metaState] field.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierAlt

```dart
int modifierAlt
```

This mask is used to check the [metaState] field to test whether one of the ALT modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftAlt

```dart
int modifierLeftAlt
```

This mask is used to check the [metaState] field to test whether the left ALT modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightAlt

```dart
int modifierRightAlt
```

This mask is used to check the [metaState] field to test whether the right ALT modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierShift

```dart
int modifierShift
```

This mask is used to check the [metaState] field to test whether one of the SHIFT modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftShift

```dart
int modifierLeftShift
```

This mask is used to check the [metaState] field to test whether the left SHIFT modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightShift

```dart
int modifierRightShift
```

This mask is used to check the [metaState] field to test whether the right SHIFT modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierSym

```dart
int modifierSym
```

This mask is used to check the [metaState] field to test whether the SYM modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierFunction

```dart
int modifierFunction
```

This mask is used to check the [metaState] field to test whether the Function modifier key (Fn) is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierControl

```dart
int modifierControl
```

This mask is used to check the [metaState] field to test whether one of the CTRL modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftControl

```dart
int modifierLeftControl
```

This mask is used to check the [metaState] field to test whether the left CTRL modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightControl

```dart
int modifierRightControl
```

This mask is used to check the [metaState] field to test whether the right CTRL modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierMeta

```dart
int modifierMeta
```

This mask is used to check the [metaState] field to test whether one of the META modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierLeftMeta

```dart
int modifierLeftMeta
```

This mask is used to check the [metaState] field to test whether the left META modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierRightMeta

```dart
int modifierRightMeta
```

This mask is used to check the [metaState] field to test whether the right META modifier key is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierCapsLock

```dart
int modifierCapsLock
```

This mask is used to check the [metaState] field to test whether the CAPS LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierNumLock

```dart
int modifierNumLock
```

This mask is used to check the [metaState] field to test whether the NUM LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierScrollLock

```dart
int modifierScrollLock
```

This mask is used to check the [metaState] field to test whether the SCROLL LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.
