@docImport 'package:flutter/widgets.dart';

# DeviceGestureSettings

```dart
class DeviceGestureSettings {}
```

The device specific gesture settings scaled into logical pixels.

This configuration can be retrieved from the window, or more commonly from a [MediaQuery] widget.

See also:

- [ui.GestureSettings], the configuration that this is derived from.

### DeviceGestureSettings()

```dart
DeviceGestureSettings({double? touchSlop})
```

Create a new [DeviceGestureSettings] with configured settings in logical pixels.

### DeviceGestureSettings.fromView()

```dart
DeviceGestureSettings.fromView(ui.FlutterView view)
```

Create a new [DeviceGestureSettings] from the provided [view].

### touchSlop

```dart
double? touchSlop
```

The touch slop value in logical pixels, or `null` if it was not set.

### panSlop

```dart
double? get panSlop
```

The touch slop value for pan gestures, in logical pixels, or `null` if it was not set.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```
