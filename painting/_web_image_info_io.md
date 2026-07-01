# WebImageInfo

```dart
class WebImageInfo implements ImageInfo {}
```

An [ImageInfo] object indicating that the image can only be displayed in an HTML element, and no [dart:ui.Image] can be created for it.

This occurs on the web when the image resource is from a different origin and is not configured for CORS. Since the image bytes cannot be directly fetched, [ui.Image]s cannot be created from it. However, the image can still be displayed if an HTML element is used.

### clone()

```dart
ImageInfo clone()
```

### debugLabel

```dart
String? get debugLabel
```

### dispose()

```dart
void dispose()
```

### image

```dart
ui.Image get image
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
