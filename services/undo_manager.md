# UndoDirection

```dart
enum UndoDirection {}
```

The direction in which an undo action should be performed, whether undo or redo.

Perform an undo action.

Perform a redo action.

# UndoManager

```dart
class UndoManager {}
```

A low-level interface to the system's undo manager.

To receive events from the system undo manager, create an [UndoManagerClient] and set it as the [client] on [UndoManager].

The [setUndoState] method can be used to update the system's undo manager using the `canUndo` and `canRedo` parameters.

When the system undo or redo button is tapped, the current [UndoManagerClient] will receive [UndoManagerClient.handlePlatformUndo] with an [UndoDirection] representing whether the event is "undo" or "redo".

Currently, only iOS has an UndoManagerPlugin implemented on the engine side. On iOS, this can be used to listen to the keyboard undo/redo buttons and the undo/redo gestures.

See also:

- [NSUndoManager](https://developer.apple.com/documentation/foundation/nsundomanager)

### setChannel()

```dart
void setChannel(MethodChannel newChannel)
```

Set the [MethodChannel] used to communicate with the system's undo manager.

This is only meant for testing within the Flutter SDK. Changing this will break the ability to set the undo status or receive undo and redo events from the system. This has no effect if asserts are disabled.

### client

```dart
set client(UndoManagerClient? client)
```

Receive undo and redo events from the system's [UndoManager].

Setting the [client] will cause [UndoManagerClient.handlePlatformUndo] to be called when a system undo or redo is triggered, such as by tapping the undo/redo keyboard buttons or using the 3-finger swipe gestures.

### client

```dart
UndoManagerClient? get client
```

Return the current [UndoManagerClient].

### setUndoState()

```dart
void setUndoState({bool canUndo = false, bool canRedo = false})
```

Set the current state of the system UndoManager. [canUndo] and [canRedo] control the respective "undo" and "redo" buttons of the system UndoManager.

# UndoManagerClient

```dart
mixin UndoManagerClient {}
```

An interface to receive events from a native UndoManager.

### handlePlatformUndo()

```dart
void handlePlatformUndo(UndoDirection direction)
```

Requests that the client perform an undo or redo operation.

Currently only used on iOS 9+ when the undo or redo methods are invoked by the platform. For example, when using three-finger swipe gestures, the iPad keyboard, or voice control.

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

### canUndo

```dart
bool get canUndo
```

Will be true if there are past values on the stack.

### canRedo

```dart
bool get canRedo
```

Will be true if there are future values on the stack.
