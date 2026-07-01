# HttpRequestFactory

```dart
typedef HttpRequestFactory = web.XMLHttpRequest Function()
```

The type for an overridable factory function for creating an HTTP request, used for testing purposes.

# HtmlElementFactory

```dart
typedef HtmlElementFactory = web.HTMLImageElement Function()
```

The type for an overridable factory function for creating HTML elements to display images, used for testing purposes.

# httpRequestFactory

```dart
HttpRequestFactory httpRequestFactory
```

Creates an overridable factory function.

# debugRestoreHttpRequestFactory()

```dart
void debugRestoreHttpRequestFactory()
```

Restores the default HTTP request factory.

# imgElementFactory

```dart
HtmlElementFactory imgElementFactory
```

The factory function that creates HTML elements, can be overridden for tests.

# debugRestoreImgElementFactory()

```dart
void debugRestoreImgElementFactory()
```

Restores the default HTML element factory.

# NetworkImage

```dart
class NetworkImage extends image_provider.ImageProvider<image_provider.NetworkImage> implements image_provider.NetworkImage {}
```

The web implementation of [image_provider.NetworkImage].

NetworkImage on the web does not support decoding to a specified size.

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
