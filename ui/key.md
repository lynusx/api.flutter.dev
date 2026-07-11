# KeyEventType

```dart
enum KeyEventType {}
```

The type of a key event.

The key is pressed.

The key is released.

The key is held, causing a repeated key input.

### label

```dart
String get label
```

# KeyEventDeviceType

```dart
enum KeyEventDeviceType {}
```

The source device for the key event.

Not all platforms supply an accurate type.

The device is a keyboard.

The device is a directional pad on something like a television remote control or similar.

The device is a gamepad button

The device is a joystick button

The device is a device connected to an HDMI bus.

### label

```dart
String get label
```

# KeyData

```dart
class KeyData {}
```

Information about a key event.

### KeyData()

```dart
KeyData({required Duration timeStamp, required KeyEventType type, required int physical, required int logical, required String? character, required bool synthesized, KeyEventDeviceType deviceType = KeyEventDeviceType.keyboard})
```

Creates an object that represents a key event.

### timeStamp

```dart
Duration timeStamp
```

Time of event dispatch, relative to an arbitrary timeline.

For synthesized events, the [timeStamp] might not be the actual time that the key press or release happens.

### type

```dart
KeyEventType type
```

The type of the event.

### deviceType

```dart
KeyEventDeviceType deviceType
```

Describes what type of device (keyboard, directional pad, etc.) this event originated from.

### physical

```dart
int physical
```

The key code for the physical key that has changed.

### logical

```dart
int logical
```

The key code for the logical key that has changed.

### character

```dart
String? character
```

Character input from the event.

Ignored for up events.

### synthesized

```dart
bool synthesized
```

If [synthesized] is true, this event does not correspond to a native event.

Although most of Flutter's keyboard events are transformed from native events, some events are not based on native events, and are synthesized only to conform Flutter's key event model (as documented in the `HardwareKeyboard` class in the framework).

For example, some key downs or ups might be lost when the window loses focus. Some platforms provide ways to query whether a key is being held. If the embedder detects an inconsistency between its internal record and the state returned by the system, the embedder will synthesize a corresponding event to synchronize the state without breaking the event model.

As another example, macOS treats CapsLock in a special way by sending down and up events at the down of alternate presses to indicate the direction in which the lock is toggled instead of that the physical key is going. A macOS embedder should normalize the behavior by converting a native down event into a down event followed immediately by a synthesized up event, and the native up event also into a down event followed immediately by a synthesized up event.

Synthesized events do not have a trustworthy [timeStamp], and should not be processed as if the key actually went down or up at the time of the callback.

[KeyRepeatEvent] is never synthesized.

### toString()

```dart
String toString()
```

### toStringFull()

```dart
String toStringFull()
```

Returns a complete textual description of the information in this object.
