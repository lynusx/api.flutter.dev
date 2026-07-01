# kAndroidToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kAndroidToLogicalKey
```

Maps Android-specific key codes to the matching [LogicalKeyboardKey].

# kAndroidToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kAndroidToPhysicalKey
```

Maps Android-specific scan codes to the matching [PhysicalKeyboardKey].

# kAndroidNumPadMap

```dart
Map<int, LogicalKeyboardKey> kAndroidNumPadMap
```

A map of Android key codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kFuchsiaToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kFuchsiaToLogicalKey
```

Maps Fuchsia-specific IDs to the matching [LogicalKeyboardKey].

# kFuchsiaToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kFuchsiaToPhysicalKey
```

Maps Fuchsia-specific USB HID Usage IDs to the matching [PhysicalKeyboardKey].

# kMacOsToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kMacOsToPhysicalKey
```

Maps macOS-specific key code values representing [PhysicalKeyboardKey].

MacOS doesn't provide a scan code, but a virtual keycode to represent a physical key.

# kMacOsNumPadMap

```dart
Map<int, LogicalKeyboardKey> kMacOsNumPadMap
```

A map of macOS key codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kMacOsFunctionKeyMap

```dart
Map<int, LogicalKeyboardKey> kMacOsFunctionKeyMap
```

A map of macOS key codes which are numbered function keys, so that they can be excluded when asking "is the Fn modifier down?".

# kMacOsToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kMacOsToLogicalKey
```

A map of macOS key codes presenting [LogicalKeyboardKey].

Logical key codes are not available in macOS key events. Most of the logical keys are derived from its `characterIgnoringModifiers`, but those keys that don't have a character representation will be derived from their key codes using this map.

# kIosToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kIosToPhysicalKey
```

Maps iOS-specific key code values representing [PhysicalKeyboardKey].

iOS doesn't provide a scan code, but a virtual keycode to represent a physical key.

# kIosSpecialLogicalMap

```dart
Map<String, LogicalKeyboardKey> kIosSpecialLogicalMap
```

Maps iOS specific string values of nonvisible keys to logical keys

Some unprintable keys on iOS has literal names on their key label, such as "UIKeyInputEscape". See: https://developer.apple.com/documentation/uikit/uikeycommand/input_strings_for_special_keys?language=objc

# kIosNumPadMap

```dart
Map<int, LogicalKeyboardKey> kIosNumPadMap
```

A map of iOS key codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kIosToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kIosToLogicalKey
```

A map of iOS key codes presenting [LogicalKeyboardKey].

Logical key codes are not available in iOS key events. Most of the logical keys are derived from its `characterIgnoringModifiers`, but those keys that don't have a character representation will be derived from their key codes using this map.

# kGlfwToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kGlfwToLogicalKey
```

Maps GLFW-specific key codes to the matching [LogicalKeyboardKey].

# kGlfwNumpadMap

```dart
Map<int, LogicalKeyboardKey> kGlfwNumpadMap
```

A map of GLFW key codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kGtkToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kGtkToLogicalKey
```

Maps GTK-specific key codes to the matching [LogicalKeyboardKey].

# kGtkNumpadMap

```dart
Map<int, LogicalKeyboardKey> kGtkNumpadMap
```

A map of GTK key codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kLinuxToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kLinuxToPhysicalKey
```

Maps XKB specific key code values representing [PhysicalKeyboardKey].

# kWebToLogicalKey

```dart
Map<String, LogicalKeyboardKey> kWebToLogicalKey
```

Maps Web KeyboardEvent codes to the matching [LogicalKeyboardKey].

# kWebToPhysicalKey

```dart
Map<String, PhysicalKeyboardKey> kWebToPhysicalKey
```

Maps Web KeyboardEvent codes to the matching [PhysicalKeyboardKey].

# kWebNumPadMap

```dart
Map<String, LogicalKeyboardKey> kWebNumPadMap
```

A map of Web KeyboardEvent codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kWebLocationMap

```dart
Map<String, List<LogicalKeyboardKey?>> kWebLocationMap
```

A map of Web KeyboardEvent keys which needs to be decided based on location, typically for numpad keys and modifier keys. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.

# kWindowsToLogicalKey

```dart
Map<int, LogicalKeyboardKey> kWindowsToLogicalKey
```

Maps Windows KeyboardEvent codes to the matching [LogicalKeyboardKey].

# kWindowsToPhysicalKey

```dart
Map<int, PhysicalKeyboardKey> kWindowsToPhysicalKey
```

Maps Windows KeyboardEvent codes to the matching [PhysicalKeyboardKey].

# kWindowsNumPadMap

```dart
Map<int, LogicalKeyboardKey> kWindowsNumPadMap
```

A map of Windows KeyboardEvent codes which have printable representations, but appear on the number pad. Used to provide different key objects for keys like KEY_EQUALS and NUMPAD_EQUALS.
