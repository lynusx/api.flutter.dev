@docImport 'package:flutter/widgets.dart';

@docImport 'multidrag.dart';

# Drag

```dart
abstract class Drag {}
```

Interface for objects that receive updates about drags.

This interface is used in various ways. For example, [MultiDragGestureRecognizer] uses it to update its clients when it recognizes a gesture. Similarly, the scrolling infrastructure in the widgets library uses it to notify the [DragScrollActivity] when the user drags the scrollable.

### update()

```dart
void update(DragUpdateDetails details)
```

The pointer has moved.

### end()

```dart
void end(DragEndDetails details)
```

The pointer is no longer in contact with the screen.

The velocity at which the pointer was moving when it stopped contacting the screen is available in the `details`.

### cancel()

```dart
void cancel()
```

The input from the pointer is no longer directed towards this receiver.

For example, the user might have been interrupted by a system-modal dialog in the middle of the drag.
