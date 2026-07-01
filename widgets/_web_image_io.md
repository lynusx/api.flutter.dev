# RawWebImage

```dart
class RawWebImage extends StatelessWidget {}
```

A [Widget] that displays an image that is backed by an HTML element.

### RawWebImage()

```dart
RawWebImage({dynamic key, required WebImageInfo image, String? debugImageLabel, double? width, double? height, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, bool matchTextDirection = false})
```

Creates a [RawWebImage].

### image

```dart
WebImageInfo image
```

The underlying HTML element to be displayed.

### debugImageLabel

```dart
String? debugImageLabel
```

A debug label explaining the image.

### width

```dart
double? width
```

The requested width for this widget.

### height

```dart
double? height
```

The requested height for this widget.

### fit

```dart
BoxFit? fit
```

How the HTML element should be inscribed in the box constraining it.

### alignment

```dart
AlignmentGeometry alignment
```

How the image should be aligned in the box constraining it.

### matchTextDirection

```dart
bool matchTextDirection
```

Whether or not the alignment of the image should match the text direction.

### build()

```dart
Widget build(BuildContext context)
```
