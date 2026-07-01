@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

# KeyboardSide

```dart
enum KeyboardSide {}
```

An enum describing the side of the keyboard that a key is on, to allow discrimination between which key is pressed (e.g. the left or right SHIFT key).

This enum is deprecated and will be removed. There is no direct substitute planned, since this enum will no longer be necessary once [RawKeyEvent] and associated APIs are removed.

See also:

- [RawKeyEventData.isModifierPressed], which accepts this enum as an argument.

Matches if either the left, right or both versions of the key are pressed.

Matches the left version of the key.

Matches the right version of the key.

Matches the left and right version of the key pressed simultaneously.

# ModifierKey

```dart
enum ModifierKey {}
```

An enum describing the type of modifier key that is being pressed.

This enum is deprecated and will be removed. There is no direct substitute planned, since this enum will no longer be necessary once [RawKeyEvent] and associated APIs are removed.

See also:

- [RawKeyEventData.isModifierPressed], which accepts this enum as an argument.

The CTRL modifier key.

Typically, there are two of these.

The SHIFT modifier key.

Typically, there are two of these.

The ALT modifier key.

Typically, there are two of these.

The META modifier key.

Typically, there are two of these. This is, for example, the Windows key on Windows (⊞), the Command (⌘) key on macOS and iOS, and the Search (🔍) key on Android.

The CAPS LOCK modifier key.

Typically, there is one of these. Only shown as "pressed" when the caps lock is on, so on a key up when the mode is turned on, on each key press when it's enabled, and on a key down when it is turned off.

The NUM LOCK modifier key.

Typically, there is one of these. Only shown as "pressed" when the num lock is on, so on a key up when the mode is turned on, on each key press when it's enabled, and on a key down when it is turned off.

The SCROLL LOCK modifier key.

Typically, there is one of these. Only shown as "pressed" when the scroll lock is on, so on a key up when the mode is turned on, on each key press when it's enabled, and on a key down when it is turned off.

The FUNCTION (Fn) modifier key.

Typically, there is one of these.

The SYMBOL modifier key.

Typically, there is one of these.

# RawKeyEventData

```dart
abstract class RawKeyEventData with Diagnosticable {}
```

Base class for platform-specific key event data.

This class is deprecated, and will be removed. Platform specific key event data will no be longer available. See [KeyEvent] for what is available.

This base class exists to have a common type to use for each of the target platform's key event data structures.

See also:

- [RawKeyEventDataAndroid], a specialization for Android.
- [RawKeyEventDataFuchsia], a specialization for Fuchsia.
- [RawKeyDownEvent] and [RawKeyUpEvent], the classes that hold the reference to [RawKeyEventData] subclasses.
- [RawKeyboard], which uses these interfaces to expose key data.

### RawKeyEventData()

```dart
RawKeyEventData()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### isModifierPressed()

```dart
bool isModifierPressed(ModifierKey key, {KeyboardSide side = KeyboardSide.any})
```

Returns true if the given [ModifierKey] was pressed at the time of this event.

This method is deprecated and will be removed. For equivalent information, inspect [HardwareKeyboard.logicalKeysPressed] instead.

If [side] is specified, then this restricts its check to the specified side of the keyboard. Defaults to checking for the key being down on either side of the keyboard. If there is only one instance of the key on the keyboard, then [side] is ignored.

### getModifierSide()

```dart
KeyboardSide? getModifierSide(ModifierKey key)
```

Returns a [KeyboardSide] enum value that describes which side or sides of the given keyboard modifier key were pressed at the time of this event.

This method is deprecated and will be removed.

If the modifier key wasn't pressed at the time of this event, returns null. If the given key only appears in one place on the keyboard, returns [KeyboardSide.all] if pressed. If the given platform does not specify the side, return [KeyboardSide.any].

### isControlPressed

```dart
bool get isControlPressed
```

Returns true if a CTRL modifier key was pressed at the time of this event, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isControlPressed] instead.

Use [isModifierPressed] if you need to know which control key was pressed.

### isShiftPressed

```dart
bool get isShiftPressed
```

Returns true if a SHIFT modifier key was pressed at the time of this event, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isShiftPressed] instead.

Use [isModifierPressed] if you need to know which shift key was pressed.

### isAltPressed

```dart
bool get isAltPressed
```

Returns true if a ALT modifier key was pressed at the time of this event, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isAltPressed] instead.

Use [isModifierPressed] if you need to know which alt key was pressed.

### isMetaPressed

```dart
bool get isMetaPressed
```

Returns true if a META modifier key was pressed at the time of this event, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isMetaPressed] instead.

Use [isModifierPressed] if you need to know which meta key was pressed.

### modifiersPressed

```dart
Map<ModifierKey, KeyboardSide> get modifiersPressed
```

Returns a map of modifier keys that were pressed at the time of this event, and the keyboard side or sides that the key was on.

This method is deprecated and will be removed. For equivalent information, inspect [HardwareKeyboard.logicalKeysPressed] instead.

### physicalKey

```dart
PhysicalKeyboardKey get physicalKey
```

Returns an object representing the physical location of this key on a QWERTY keyboard.

{@macro flutter.services.RawKeyEvent.physicalKey}

See also:

- [logicalKey] for the non-location-specific key generated by this event.
- [RawKeyEvent.physicalKey], where this value is available on the event.

### logicalKey

```dart
LogicalKeyboardKey get logicalKey
```

Returns an object representing the logical key that was pressed.

{@macro flutter.services.RawKeyEvent.logicalKey}

See also:

- [physicalKey] for the location-specific key generated by this event.
- [RawKeyEvent.logicalKey], where this value is available on the event.

### keyLabel

```dart
String get keyLabel
```

Returns the Unicode string representing the label on this key.

This value is an empty string if there's no key label data for a key.

{@template flutter.services.RawKeyEventData.keyLabel} Do not use the [keyLabel] to compose a text string: it will be missing special processing for Unicode strings for combining characters and other special characters, and the effects of modifiers.

If you are looking for the character produced by a key event, use [RawKeyEvent.character] instead.

If you are composing text strings, use the [TextField] or [CupertinoTextField] widgets, since those automatically handle many of the complexities of managing keyboard input, like showing a soft keyboard or interacting with an input method editor (IME). {@endtemplate}

### shouldDispatchEvent()

```dart
bool shouldDispatchEvent()
```

Whether a key down event, and likewise its accompanying key up event, should be dispatched.

Certain events on some platforms should not be dispatched to listeners according to Flutter's event model. For example, on macOS, Fn keys are skipped to be consistent with other platform. On Win32, events dispatched for IME (`VK_PROCESSKEY`) are also skipped.

This method will be called upon every down events. By default, this method always return true. Subclasses should override this method to define the filtering rule for the platform. If this method returns false for an event message, the event will not be dispatched to listeners, but respond with "handled: true" immediately. Moreover, the following up event with the same physical key will also be skipped.

# RawKeyEvent

```dart
abstract class RawKeyEvent with Diagnosticable {}
```

Defines the interface for raw key events.

This type of event has been deprecated, and will be removed at a future date. Instead of using this, use the [KeyEvent] class instead, which means you will use [Focus.onKeyEvent], [HardwareKeyboard] and [KeyboardListener] to get these events instead of the raw key event equivalents.

Raw key events pass through as much information as possible from the underlying platform's key events, which allows them to provide a high level of fidelity but a low level of portability.

The event also provides an abstraction for the [physicalKey] and the [logicalKey], describing the physical location of the key, and the logical meaning of the key, respectively. These are more portable representations of the key events, and should produce the same results regardless of platform.

See also:

- [LogicalKeyboardKey], an object that describes the logical meaning of a key.
- [PhysicalKeyboardKey], an object that describes the physical location of a key.
- [RawKeyDownEvent], a specialization for events representing the user pressing a key.
- [RawKeyUpEvent], a specialization for events representing the user releasing a key.
- [RawKeyboard], which uses this interface to expose key data.
- [RawKeyboardListener], a widget that listens for raw key events.

### RawKeyEvent()

```dart
RawKeyEvent({required RawKeyEventData data, String? character, bool repeat = false})
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### RawKeyEvent.fromMessage()

```dart
RawKeyEvent.fromMessage(Map<String, Object?> message)
```

Creates a concrete [RawKeyEvent] class from a message in the form received on the [SystemChannels.keyEvent] channel.

[RawKeyEvent.repeat] will be derived from the current keyboard state, instead of using the message information.

This exception would only be hit on platforms that haven't yet implemented raw key events, but will only be triggered if the engine for those platforms sends raw key event messages in the first place.

### isKeyPressed()

```dart
bool isKeyPressed(LogicalKeyboardKey key)
```

Returns true if the given [LogicalKeyboardKey] is pressed.

This method is deprecated and will be removed. Use [HardwareKeyboard.isLogicalKeyPressed] instead.

### isControlPressed

```dart
bool get isControlPressed
```

Returns true if a CTRL modifier key is pressed, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isControlPressed] instead.

Use [isKeyPressed] if you need to know which control key was pressed.

### isShiftPressed

```dart
bool get isShiftPressed
```

Returns true if a SHIFT modifier key is pressed, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isShiftPressed] instead.

Use [isKeyPressed] if you need to know which shift key was pressed.

### isAltPressed

```dart
bool get isAltPressed
```

Returns true if a ALT modifier key is pressed, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isAltPressed] instead.

The `AltGr` key that appears on some keyboards is considered to be the same as [LogicalKeyboardKey.altRight] on some platforms (notably Android). On platforms that can distinguish between `altRight` and `altGr`, a press of `AltGr` will not return true here, and will need to be tested for separately.

Use [isKeyPressed] if you need to know which alt key was pressed.

### isMetaPressed

```dart
bool get isMetaPressed
```

Returns true if a META modifier key is pressed, regardless of which side of the keyboard it is on.

This method is deprecated and will be removed. Use [HardwareKeyboard.isMetaPressed] instead.

Use [isKeyPressed] if you need to know which meta key was pressed.

### physicalKey

```dart
PhysicalKeyboardKey get physicalKey
```

Returns an object representing the physical location of this key.

{@template flutter.services.RawKeyEvent.physicalKey} The [PhysicalKeyboardKey] ignores the key map, modifier keys (like SHIFT), and the label on the key. It describes the location of the key as if it were on a QWERTY keyboard regardless of the keyboard mapping in effect.

[PhysicalKeyboardKey]s are used to describe and test for keys in a particular location.

For instance, if you wanted to make a game where the key to the right of the CAPS LOCK key made the player move left, you would be comparing the result of this [physicalKey] with [PhysicalKeyboardKey.keyA], since that is the key next to the CAPS LOCK key on a QWERTY keyboard. This would return the same thing even on a French keyboard where the key next to the CAPS LOCK produces a "Q" when pressed.

If you want to make your app respond to a key with a particular character on it regardless of location of the key, use [RawKeyEvent.logicalKey] instead. {@endtemplate}

See also:

- [logicalKey] for the non-location specific key generated by this event.
- [character] for the character generated by this keypress (if any).

### logicalKey

```dart
LogicalKeyboardKey get logicalKey
```

Returns an object representing the logical key that was pressed.

{@template flutter.services.RawKeyEvent.logicalKey} This method takes into account the key map and modifier keys (like SHIFT) to determine which logical key to return.

If you are looking for the character produced by a key event, use [RawKeyEvent.character] instead.

If you are collecting text strings, use the [TextField] or [CupertinoTextField] widgets, since those automatically handle many of the complexities of managing keyboard input, like showing a soft keyboard or interacting with an input method editor (IME). {@endtemplate}

### character

```dart
String? character
```

Returns the Unicode character (grapheme cluster) completed by this keystroke, if any.

This will only return a character if this keystroke, combined with any preceding keystroke(s), generated a character, and only on a "key down" event. It will return null if no character has been generated by the keystroke (e.g. a "dead" or "combining" key), or if the corresponding key is a key without a visual representation, such as a modifier key or a control key.

This can return multiple Unicode code points, since some characters (more accurately referred to as grapheme clusters) are made up of more than one code point.

The [character] doesn't take into account edits by an input method editor (IME), or manage the visibility of the soft keyboard on touch devices. For composing text, use the [TextField] or [CupertinoTextField] widgets, since those automatically handle many of the complexities of managing keyboard input.

### repeat

```dart
bool repeat
```

Whether this is a repeated down event.

When a key is held down, the systems usually fire a down event and then a series of repeated down events. The [repeat] is false for the first event and true for the following events.

The [repeat] attribute is always false for [RawKeyUpEvent]s.

### data

```dart
RawKeyEventData data
```

Platform-specific information about the key event.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RawKeyDownEvent

```dart
class RawKeyDownEvent extends RawKeyEvent {}
```

The user has pressed a key on the keyboard.

This class has been deprecated and will be removed. Use [KeyDownEvent] instead.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyDownEvent()

```dart
RawKeyDownEvent({required RawKeyEventData data, String? character, bool repeat})
```

Creates a key event that represents the user pressing a key.

# RawKeyUpEvent

```dart
class RawKeyUpEvent extends RawKeyEvent {}
```

The user has released a key on the keyboard.

This class has been deprecated and will be removed. Use [KeyUpEvent] instead.

See also:

- [RawKeyboard], which uses this interface to expose key data.

### RawKeyUpEvent()

```dart
RawKeyUpEvent({required RawKeyEventData data, String? character})
```

Creates a key event that represents the user releasing a key.

# RawKeyEventHandler

```dart
typedef RawKeyEventHandler = bool Function(RawKeyEvent event)
```

A callback type used by [RawKeyboard.keyEventHandler] to send key events to a handler that can determine if the key has been handled or not.

This typedef has been deprecated and will be removed. Use [KeyEventCallback] instead.

The handler should return true if the key has been handled, and false if the key was not handled. It must not return null.

# RawKeyboard

```dart
class RawKeyboard {}
```

An interface for listening to raw key events.

This class is deprecated and will be removed at a future date. The [HardwareKeyboard] class is its replacement.

Raw key events pass through as much information as possible from the underlying platform's key events, which makes them provide a high level of fidelity but a low level of portability.

A [RawKeyboard] is useful for listening to raw key events and hardware buttons that are represented as keys. Typically used by games and other apps that use keyboards for purposes other than text entry.

These key events are typically only key events generated by a hardware keyboard, and not those from software keyboards or input method editors.

## Compared to [HardwareKeyboard]

Behavior-wise, [RawKeyboard] provides a less unified, less regular event model than [HardwareKeyboard]. For example:

- Down events might not be matched with an up event, and vice versa (the set of pressed keys is silently updated).
- The logical key of the down event might not be the same as that of the up event.
- Down events and repeat events are not easily distinguishable (must be tracked manually).
- Lock modes (such as CapsLock) only have their "enabled" state recorded. There's no way to acquire their pressing state.

See also:

- [RawKeyDownEvent] and [RawKeyUpEvent], the classes used to describe specific raw key events.
- [RawKeyboardListener], a widget that listens for raw key events.
- [SystemChannels.keyEvent], the low-level channel used for receiving events from the system.
- [HardwareKeyboard], the recommended replacement.

### instance

```dart
RawKeyboard instance
```

The shared instance of [RawKeyboard].

### addListener()

```dart
void addListener(ValueChanged<RawKeyEvent> listener)
```

Register a listener that is called every time the user presses or releases a hardware keyboard key.

Since the listeners have no way to indicate what they did with the event, listeners are assumed to not handle the key event. These events will also be distributed to other listeners, and to the [keyEventHandler].

Most applications prefer to use the focus system (see [Focus] and [FocusManager]) to receive key events to the focused control instead of this kind of passive listener.

Listeners can be removed with [removeListener].

### removeListener()

```dart
void removeListener(ValueChanged<RawKeyEvent> listener)
```

Stop calling the given listener every time the user presses or releases a hardware keyboard key.

Listeners can be added with [addListener].

### keyEventHandler

```dart
RawKeyEventHandler? get keyEventHandler
```

A handler for raw hardware keyboard events that will stop propagation if the handler returns true.

This property is only a wrapper over [KeyEventManager.keyMessageHandler], and is kept only for backward compatibility. New code should use [KeyEventManager.keyMessageHandler] to set custom global key event handler. Setting [keyEventHandler] will cause [KeyEventManager.keyMessageHandler] to be set with a converted handler. If [KeyEventManager.keyMessageHandler] is set by [FocusManager] (the most common situation), then the exact value of [keyEventHandler] is a dummy callback and must not be invoked.

### keyEventHandler

```dart
set keyEventHandler(RawKeyEventHandler? handler)
```

### handleRawKeyEvent()

```dart
bool handleRawKeyEvent(RawKeyEvent event)
```

Process a new [RawKeyEvent] by recording the state changes and dispatching to listeners.

### keysPressed

```dart
Set<LogicalKeyboardKey> get keysPressed
```

Returns the set of keys currently pressed.

### physicalKeysPressed

```dart
Set<PhysicalKeyboardKey> get physicalKeysPressed
```

Returns the set of physical keys currently pressed.

### lookUpLayout()

```dart
LogicalKeyboardKey? lookUpLayout(PhysicalKeyboardKey physicalKey)
```

Returns the logical key that corresponds to the given pressed physical key.

Returns null if the physical key is not currently pressed.

### clearKeysPressed()

```dart
void clearKeysPressed()
```

Clears the list of keys returned from [keysPressed].

This is used by the testing framework to make sure tests are hermetic.
