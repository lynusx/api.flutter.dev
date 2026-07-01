@docImport 'slider.dart'; @docImport 'switch.dart';

# CupertinoThumbPainter

```dart
class CupertinoThumbPainter {}
```

Paints an iOS-style slider thumb or switch thumb.

Used by [CupertinoSlider].

### CupertinoThumbPainter()

```dart
CupertinoThumbPainter({Color color = CupertinoColors.white, List<BoxShadow> shadows = _kSliderBoxShadows})
```

Creates an object that paints an iOS-style slider thumb.

### CupertinoThumbPainter.switchThumb()

```dart
CupertinoThumbPainter.switchThumb({Color color = CupertinoColors.white, List<BoxShadow> shadows = _kSwitchBoxShadows})
```

Creates an object that paints an iOS-style switch thumb.

### color

```dart
Color color
```

The color of the interior of the thumb.

### shadows

```dart
List<BoxShadow> shadows
```

The list of [BoxShadow] to paint below the thumb.

### radius

```dart
double radius
```

Half the default diameter of the thumb.

### extension

```dart
double extension
```

The default amount the thumb should be extended horizontally when pressed.

### paint()

```dart
void paint(Canvas canvas, Rect rect)
```

Paints the thumb onto the given canvas in the given rectangle.

Consider using [radius] and [extension] when deciding how large a rectangle to use for the thumb.
