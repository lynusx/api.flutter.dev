@docImport 'editable_text.dart'; @docImport 'keyboard_listener.dart';

# RawKeyboardListener

```dart
class RawKeyboardListener extends StatefulWidget {}
```

A widget that calls a callback whenever the user presses or releases a key on a keyboard.

The [RawKeyboardListener] is deprecated and will be removed. Use [KeyboardListener] instead.

A [RawKeyboardListener] is useful for listening to raw key events and hardware buttons that are represented as keys. Typically used by games and other apps that use keyboards for purposes other than text entry.

For text entry, consider using a [EditableText], which integrates with on-screen keyboards and input method editors (IMEs).

See also:

- [EditableText], which should be used instead of this widget for text entry.
- [KeyboardListener], a similar widget based on the newer [HardwareKeyboard] API.

### RawKeyboardListener()

```dart
RawKeyboardListener({dynamic key, required FocusNode focusNode, bool autofocus = false, bool includeSemantics = true, ValueChanged<RawKeyEvent>? onKey, required Widget child})
```

Creates a widget that receives raw keyboard events.

For text entry, consider using a [EditableText], which integrates with on-screen keyboards and input method editors (IMEs).

### focusNode

```dart
FocusNode focusNode
```

Controls whether this widget has keyboard focus.

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### includeSemantics

```dart
bool includeSemantics
```

{@macro flutter.widgets.Focus.includeSemantics}

### onKey

```dart
ValueChanged<RawKeyEvent>? onKey
```

Called whenever this widget receives a raw keyboard event.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
State<RawKeyboardListener> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
