@docImport 'package:flutter/material.dart';

@docImport 'editable_text.dart'; @docImport 'focus_scope.dart';

# UndoHistory

```dart
class UndoHistory<T> extends StatefulWidget {}
```

Provides undo/redo capabilities for a [ValueNotifier].

Listens to [value] and saves relevant values for undoing/redoing. The cadence at which values are saved is a best approximation of the native behaviors of a number of hardware keyboard on Flutter's desktop platforms, as there are subtle differences between each of the platforms.

Listens to keyboard undo/redo shortcuts and calls [onTriggered] when a shortcut is triggered that would affect the state of the [value].

The [child] must manage focus on the [focusNode]. For example, using a [TextField] or [Focus] widget.

### UndoHistory()

```dart
UndoHistory({dynamic key, bool Function(T? oldValue, T newValue)? shouldChangeUndoStack, required ValueNotifier<T> value, required void Function(T value) onTriggered, required FocusNode focusNode, T Function(T value)? undoStackModifier, UndoHistoryController? controller, required Widget child})
```

Creates an instance of [UndoHistory].

### value

```dart
ValueNotifier<T> value
```

The value to track over time.

### shouldChangeUndoStack

```dart
bool Function(T? oldValue, T newValue)? shouldChangeUndoStack
```

Called when checking whether a value change should be pushed onto the undo stack.

### undoStackModifier

```dart
T Function(T value)? undoStackModifier
```

Called right before a new entry is pushed to the undo stack.

The value returned from this method will be pushed to the stack instead of the original value.

If null then the original value will always be pushed to the stack.

### onTriggered

```dart
void Function(T value) onTriggered
```

Called when an undo or redo causes a state change.

If the state would still be the same before and after the undo/redo, this will not be called. For example, receiving a redo when there is nothing to redo will not call this method.

Changes to the [value] while this method is running will not be recorded on the undo stack. For example, a [TextInputFormatter] may change the value from what was on the undo stack, but this new value will not be recorded, as that would wipe out the redo history.

### focusNode

```dart
FocusNode focusNode
```

The [FocusNode] that will be used to listen for focus to set the initial undo state for the element.

### controller

```dart
UndoHistoryController? controller
```

{@template flutter.widgets.undoHistory.controller} Controls the undo state.

If null, this widget will create its own [UndoHistoryController]. {@endtemplate}

### child

```dart
Widget child
```

The child widget of [UndoHistory].

### createState()

```dart
State<UndoHistory<T>> createState()
```

# UndoHistoryState

```dart
class UndoHistoryState<T> extends State<UndoHistory<T>> with UndoManagerClient {}
```

State for a [UndoHistory].

Provides [undo], [redo], [canUndo], and [canRedo] for programmatic access to the undo state for custom undo and redo UI implementations.

### undo()

```dart
void undo()
```

### redo()

```dart
void redo()
```

### canUndo

```dart
bool get canUndo
```

### canRedo

```dart
bool get canRedo
```

### handlePlatformUndo()

```dart
void handlePlatformUndo(UndoDirection direction)
```

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(UndoHistory<T> oldWidget)
```

### dispose()

```dart
void dispose()
```

### build()

```dart
Widget build(BuildContext context)
```

# UndoHistoryValue

```dart
class UndoHistoryValue {}
```

Represents whether the current undo stack can undo or redo.

### UndoHistoryValue()

```dart
UndoHistoryValue({bool canUndo = false, bool canRedo = false})
```

Creates a value for whether the current undo stack can undo or redo.

The [canUndo] and [canRedo] arguments must have a value, but default to false.

### empty

```dart
UndoHistoryValue empty
```

A value corresponding to an undo stack that can neither undo nor redo.

### canUndo

```dart
bool canUndo
```

Whether the current undo stack can perform an undo operation.

### canRedo

```dart
bool canRedo
```

Whether the current undo stack can perform a redo operation.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# UndoHistoryController

```dart
class UndoHistoryController extends ValueNotifier<UndoHistoryValue> {}
```

A controller for the undo history, for example for an editable text field.

Whenever a change happens to the underlying value that the [UndoHistory] widget tracks, that widget updates the [value] and the controller notifies it's listeners. Listeners can then read the canUndo and canRedo properties of the value to discover whether [undo] or [redo] are possible.

The controller also has [undo] and [redo] methods to modify the undo history.

{@tool dartpad} This example creates a [TextField] with an [UndoHistoryController] which provides undo and redo buttons.

** See code in examples/api/lib/widgets/undo_history/undo_history_controller.0.dart ** {@end-tool}

See also:

- [EditableText], which uses the [UndoHistory] widget and allows control of the underlying history using an [UndoHistoryController].

### UndoHistoryController()

```dart
UndoHistoryController({UndoHistoryValue? value})
```

Creates a controller for an [UndoHistory] widget.

### onUndo

```dart
ChangeNotifier onUndo
```

Notifies listeners that [undo] has been called.

### onRedo

```dart
ChangeNotifier onRedo
```

Notifies listeners that [redo] has been called.

### undo()

```dart
void undo()
```

Reverts the value on the stack to the previous value.

### redo()

```dart
void redo()
```

Updates the value on the stack to the next value.

### dispose()

```dart
void dispose()
```
