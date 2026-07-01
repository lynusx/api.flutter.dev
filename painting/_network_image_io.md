# NetworkImage

```dart
class NetworkImage extends image_provider.ImageProvider<image_provider.NetworkImage> implements image_provider.NetworkImage {}
```

The dart:io implementation of [image_provider.NetworkImage].

### NetworkImage()

```dart
NetworkImage(String url, {double scale = 1.0, Map<String, String>? headers, image_provider.WebHtmlElementStrategy webHtmlElementStrategy = image_provider.WebHtmlElementStrategy.never})
```

Creates an object that fetches the image at the given URL.

### url

```dart
String url
```

### scale

```dart
double scale
```

### headers

```dart
Map<String, String>? headers
```

### webHtmlElementStrategy

```dart
image_provider.WebHtmlElementStrategy webHtmlElementStrategy
```

### obtainKey()

```dart
Future<NetworkImage> obtainKey(image_provider.ImageConfiguration configuration)
```

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(image_provider.NetworkImage key, image_provider.DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(image_provider.NetworkImage key, image_provider.ImageDecoderCallback decode)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```
