@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/services.dart';

@docImport 'text_selection.dart';

# ContextMenuButtonType

```dart
enum ContextMenuButtonType {}
```

The buttons that can appear in a context menu by default.

See also:

- [ContextMenuButtonItem], which uses this enum to describe a button in a context menu.

A button that cuts the current text selection.

A button that copies the current text selection.

A button that pastes the clipboard contents into the focused text field.

A button that selects all the contents of the focused text field.

A button that deletes the current text selection.

A button that looks up the current text selection.

A button that launches a web search for the current text selection.

A button that displays the share screen for the current text selection.

A button for starting Live Text input.

See also:

- [LiveText], where the availability of Live Text input can be obtained.
- [LiveTextInputStatusNotifier], where the status of Live Text can be listened to.

Anything other than the default button types.

# ContextMenuButtonItem

```dart
class ContextMenuButtonItem {}
```

The type and callback for a context menu button.

See also:

- [AdaptiveTextSelectionToolbar], which can take a list of ContextMenuButtonItems and create a platform-specific context menu with the indicated buttons.
- [IOSSystemContextMenuItem], which serves a similar role but for system-drawn context menu items on iOS.

### ContextMenuButtonItem()

```dart
ContextMenuButtonItem({required VoidCallback? onPressed, ContextMenuButtonType type = ContextMenuButtonType.custom, String? label})
```

Creates a const instance of [ContextMenuButtonItem].

### onPressed

```dart
VoidCallback? onPressed
```

The callback to be called when the button is pressed.

### type

```dart
ContextMenuButtonType type
```

The type of button this represents.

### label

```dart
String? label
```

The label to display on the button.

If a [type] other than [ContextMenuButtonType.custom] is given and a label is not provided, then the default label for that type for the platform will be looked up.

### copyWith()

```dart
ContextMenuButtonItem copyWith({VoidCallback? onPressed, ContextMenuButtonType? type, String? label})
```

Creates a new [ContextMenuButtonItem] with the provided parameters overridden.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```
