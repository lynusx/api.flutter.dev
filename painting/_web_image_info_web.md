# WebImageInfo

```dart
class WebImageInfo implements ImageInfo {}
```

An [ImageInfo] object indicating that the image can only be displayed in an HTML element, and no [dart:ui.Image] can be created for it.

This occurs on the web when the image resource is from a different origin and is not configured for CORS. Since the image bytes cannot be directly fetched, [Image]s cannot be created from it. However, the image can still be displayed if an HTML element is used.

### WebImageInfo()

```dart
WebImageInfo(web.HTMLImageElement htmlImage, {String? debugLabel})
```

Creates a new [WebImageInfo] from a given HTML element.

### htmlImage

```dart
web.HTMLImageElement htmlImage
```

The HTML element used to display this image. This HTML element has already decoded the image, so size information can be retrieved from it.

### debugLabel

```dart
String? debugLabel
```

### clone()

```dart
WebImageInfo clone()
```

### dispose()

```dart
void dispose()
```

### image

```dart
Image get image
```

### isCloneOf()

```dart
bool isCloneOf(ImageInfo other)
```

### scale

```dart
double get scale
```

### sizeBytes

```dart
int get sizeBytes
```
