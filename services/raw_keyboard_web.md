@docImport 'hardware_keyboard.dart';

# RawKeyEventDataWeb

```dart
class RawKeyEventDataWeb extends RawKeyEventData {}
```

Platform-specific key event data for Web.

This class is DEPRECATED. Platform specific key event data will no longer available. See [KeyEvent] for what is available.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyEventDataWeb()

```dart
RawKeyEventDataWeb({required String code, required String key, int location = 0, int metaState = modifierNone, int keyCode = 0})
```

Creates a key event data structure specific for Web.

### code

```dart
String code
```

The `KeyboardEvent.code` corresponding to this event.

The [code] represents a physical key on the keyboard, a value that isn't altered by keyboard layout or the state of the modifier keys.

See <https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/code> for more information.

### key

```dart
String key
```

The `KeyboardEvent.key` corresponding to this event.

The [key] represents the key pressed by the user, taking into consideration the state of modifier keys such as Shift as well as the keyboard locale and layout.

See <https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key> for more information.

### location

```dart
int location
```

The `KeyboardEvent.location` corresponding to this event.

The [location] represents the location of the key on the keyboard or other input device, such as left or right modifier keys, or Numpad keys.

See <https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/location> for more information.

### metaState

```dart
int metaState
```

The modifiers that were present when the key event occurred.

See `lib/src/engine/keyboard.dart` in the web engine for the numerical values of the [metaState]. These constants are also replicated as static constants in this class.

See also:

- [modifiersPressed], which returns a Map of currently pressed modifiers and their keyboard side.
- [isModifierPressed], to see if a specific modifier is pressed.
- [isControlPressed], to see if a CTRL key is pressed.
- [isShiftPressed], to see if a SHIFT key is pressed.
- [isAltPressed], to see if an ALT key is pressed.
- [isMetaPressed], to see if a META key is pressed.

### keyCode

```dart
int keyCode
```

The `KeyboardEvent.keyCode` corresponding to this event.

See <https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode> for more information.

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
KeyboardSide getModifierSide(ModifierKey key)
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

### modifierShift

```dart
int modifierShift
```

This mask is used to check the [metaState] field to test whether one of the SHIFT modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierAlt

```dart
int modifierAlt
```

This mask is used to check the [metaState] field to test whether one of the ALT modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierControl

```dart
int modifierControl
```

This mask is used to check the [metaState] field to test whether one of the CTRL modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierMeta

```dart
int modifierMeta
```

This mask is used to check the [metaState] field to test whether one of the META modifier keys is pressed.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierNumLock

```dart
int modifierNumLock
```

This mask is used to check the [metaState] field to test whether the NUM LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierCapsLock

```dart
int modifierCapsLock
```

This mask is used to check the [metaState] field to test whether the CAPS LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.

### modifierScrollLock

```dart
int modifierScrollLock
```

This mask is used to check the [metaState] field to test whether the SCROLL LOCK modifier key is on.

Use this value if you need to decode the [metaState] field yourself, but it's much easier to use [isModifierPressed] if you just want to know if a modifier is pressed.
