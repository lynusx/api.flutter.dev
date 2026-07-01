@docImport 'editable_text.dart';

# KeyboardListener

```dart
class KeyboardListener extends StatelessWidget {}
```

A widget that calls a callback whenever the user presses or releases a key on a keyboard.

A [KeyboardListener] is useful for listening to key events and hardware buttons that are represented as keys. Typically used by games and other apps that use keyboards for purposes other than text entry.

For text entry, consider using a [EditableText], which integrates with on-screen keyboards and input method editors (IMEs).

See also:

- [EditableText], which should be used instead of this widget for text entry.

### KeyboardListener()

```dart
KeyboardListener({dynamic key, required FocusNode focusNode, bool autofocus = false, bool includeSemantics = true, ValueChanged<KeyEvent>? onKeyEvent, required Widget child})
```

Creates a widget that receives keyboard events.

For text entry, consider using a [EditableText], which integrates with on-screen keyboards and input method editors (IMEs).

The `key` is an identifier for widgets, and is unrelated to keyboards. See [Widget.key].

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

### onKeyEvent

```dart
ValueChanged<KeyEvent>? onKeyEvent
```

Called whenever this widget receives a keyboard event.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
