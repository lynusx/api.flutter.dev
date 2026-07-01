@docImport 'package:flutter/widgets.dart';

# EagerGestureRecognizer

```dart
class EagerGestureRecognizer extends OneSequenceGestureRecognizer {}
```

A gesture recognizer that eagerly claims victory in all gesture arenas.

This is typically passed in [AndroidView.gestureRecognizers] in order to immediately dispatch all touch events inside the view bounds to the embedded Android view. See [AndroidView.gestureRecognizers] for more details.

### EagerGestureRecognizer()

```dart
EagerGestureRecognizer({Set<InvalidType>? supportedDevices, bool Function(int) allowedButtonsFilter})
```

Create an eager gesture recognizer.

{@macro flutter.gestures.GestureRecognizer.supportedDevices}

### addAllowedPointer()

```dart
void addAllowedPointer(PointerDownEvent event)
```

### debugDescription

```dart
String get debugDescription
```

### didStopTrackingLastPointer()

```dart
void didStopTrackingLastPointer(int pointer)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event)
```
