@docImport 'package:flutter/widgets.dart'; @docImport '_web_image_info_io.dart';

# ImageConfiguration

```dart
class ImageConfiguration {}
```

Configuration information passed to the [ImageProvider.resolve] method to select a specific image.

See also:

- [createLocalImageConfiguration], which creates an [ImageConfiguration] based on ambient configuration in a [Widget] environment.
- [ImageProvider], which uses [ImageConfiguration] objects to determine which image to obtain.

### ImageConfiguration()

```dart
ImageConfiguration({AssetBundle? bundle, double? devicePixelRatio, ui.Locale? locale, TextDirection? textDirection, Size? size, TargetPlatform? platform})
```

Creates an object holding the configuration information for an [ImageProvider].

All the arguments are optional. Configuration information is merely advisory and best-effort.

### copyWith()

```dart
ImageConfiguration copyWith({AssetBundle? bundle, double? devicePixelRatio, ui.Locale? locale, TextDirection? textDirection, Size? size, TargetPlatform? platform})
```

Creates an object holding the configuration information for an [ImageProvider].

All the arguments are optional. Configuration information is merely advisory and best-effort.

### bundle

```dart
AssetBundle? bundle
```

The preferred [AssetBundle] to use if the [ImageProvider] needs one and does not have one already selected.

### devicePixelRatio

```dart
double? devicePixelRatio
```

The device pixel ratio where the image will be shown.

### locale

```dart
ui.Locale? locale
```

The language and region for which to select the image.

### textDirection

```dart
TextDirection? textDirection
```

The reading direction of the language for which to select the image.

### size

```dart
Size? size
```

The size at which the image will be rendered.

### platform

```dart
TargetPlatform? platform
```

The [TargetPlatform] for which assets should be used. This allows images to be specified in a platform-neutral fashion yet use different assets on different platforms, to match local conventions e.g. for color matching or shadows.

### empty

```dart
ImageConfiguration empty
```

An image configuration that provides no additional information.

Useful when resolving an [ImageProvider] without any context.

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

# DecoderBufferCallback

```dart
typedef DecoderBufferCallback = Future<ui.Codec> Function(ui.ImmutableBuffer buffer, {int? cacheWidth, int? cacheHeight, bool allowUpscaling})
```

Performs the decode process for use in [ImageProvider.loadBuffer].

This callback allows decoupling of the `cacheWidth`, `cacheHeight`, and `allowUpscaling` parameters from implementations of [ImageProvider] that do not expose them.

See also:

- [ResizeImage], which uses this to override the `cacheWidth`, `cacheHeight`, and `allowUpscaling` parameters.

# ImageDecoderCallback

```dart
typedef ImageDecoderCallback = Future<ui.Codec> Function(ui.ImmutableBuffer buffer, {ui.TargetImageSizeCallback? getTargetSize})
```

Performs the decode process for use in [ImageProvider.loadImage].

This callback allows decoupling of the `getTargetSize` parameter from implementations of [ImageProvider] that do not expose it.

See also:

- [ResizeImage], which uses this to load images at specific sizes.

# ImageProvider

```dart
abstract class ImageProvider<T extends Object> {}
```

Identifies an image without committing to the precise final asset. This allows a set of images to be identified and for the precise image to later be resolved based on the environment, e.g. the device pixel ratio.

To obtain an [ImageStream] from an [ImageProvider], call [resolve], passing it an [ImageConfiguration] object.

[ImageProvider] uses the global [imageCache] to cache images.

The type argument `T` is the type of the object used to represent a resolved configuration. This is also the type used for the key in the image cache. It should be immutable and implement the [==] operator and the [hashCode] getter. Subclasses should subclass a variant of [ImageProvider] with an explicit `T` type argument.

The type argument does not have to be specified when using the type as an argument (where any image provider is acceptable).

The following image formats are supported: {@macro dart.ui.imageFormats}

## Lifecycle of resolving an image

The [ImageProvider] goes through the following lifecycle to resolve an image, once the [resolve] method is called:

1.  Create an [ImageStream] using [createStream] to return to the caller. This stream will be used to communicate back to the caller when the image is decoded and ready to display, or when an error occurs.
2.  Obtain the key for the image using [obtainKey]. Calling this method can throw exceptions into the zone asynchronously or into the call stack synchronously. To handle that, an error handler is created that catches both synchronous and asynchronous errors, to make sure errors can be routed to the correct consumers. The error handler is passed on to [resolveStreamForKey] and the [ImageCache].
3.  If the key is successfully obtained, schedule resolution of the image using that key. This is handled by [resolveStreamForKey]. That method may fizzle if it determines the image is no longer necessary, use the provided [ImageErrorListener] to report an error, set the completer from the cache if possible, or call [loadImage] to fetch the encoded image bytes and schedule decoding.
4.  The [loadImage] method is responsible for both fetching the encoded bytes and decoding them using the provided [ImageDecoderCallback]. It is called in a context that uses the [ImageErrorListener] to report errors back.

Subclasses normally only have to implement the [loadImage] and [obtainKey] methods. A subclass that needs finer grained control over the [ImageStream] type must override [createStream]. A subclass that needs finer grained control over the resolution, such as delaying calling [loadImage], must override [resolveStreamForKey].

The [resolve] method is marked as [nonVirtual] so that [ImageProvider]s can be properly composed, and so that the base class can properly set up error handling for subsequent methods.

## Using an [ImageProvider]

{@tool snippet}

The following shows the code required to write a widget that fully conforms to the [ImageProvider] and [Widget] protocols. (It is essentially a bare-bones version of the [Image] widget.)

```dart
class MyImage extends StatefulWidget {
  const MyImage({
    super.key,
    required this.imageProvider,
  });

  final ImageProvider imageProvider;

  @override
  State<MyImage> createState() => _MyImageState();
}

class _MyImageState extends State<MyImage> {
  ImageStream? _imageStream;
  ImageInfo? _imageInfo;

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    // We call _getImage here because createLocalImageConfiguration() needs to
    // be called again if the dependencies changed, in case the changes relate
    // to the DefaultAssetBundle, MediaQuery, etc, which that method uses.
    _getImage();
  }

  @override
  void didUpdateWidget(MyImage oldWidget) {
    super.didUpdateWidget(oldWidget);
    if (widget.imageProvider != oldWidget.imageProvider) {
      _getImage();
    }
  }

  void _getImage() {
    final ImageStream? oldImageStream = _imageStream;
    _imageStream = widget.imageProvider.resolve(createLocalImageConfiguration(context));
    if (_imageStream!.key != oldImageStream?.key) {
      // If the keys are the same, then we got the same image back, and so we don't
      // need to update the listeners. If the key changed, though, we must make sure
      // to switch our listeners to the new image stream.
      final ImageStreamListener listener = ImageStreamListener(_updateImage);
      oldImageStream?.removeListener(listener);
      _imageStream!.addListener(listener);
    }
  }

  void _updateImage(ImageInfo imageInfo, bool synchronousCall) {
    setState(() {
      // Trigger a build whenever the image changes.
      _imageInfo?.dispose();
      _imageInfo = imageInfo;
    });
  }

  @override
  void dispose() {
    _imageStream?.removeListener(ImageStreamListener(_updateImage));
    _imageInfo?.dispose();
    _imageInfo = null;
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return RawImage(
      image: _imageInfo?.image, // this is a dart:ui Image object
      scale: _imageInfo?.scale ?? 1.0,
    );
  }
}
```

{@end-tool}

## Creating an [ImageProvider]

{@tool sample} In this example, a variant of [NetworkImage] is created that passes all the [ImageConfiguration] information (locale, platform, size, etc) to the server using query arguments in the image URL.

** See code in examples/api/lib/painting/image_provider/image_provider.0.dart ** {@end-tool}

### ImageProvider()

```dart
ImageProvider()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### resolve()

```dart
ImageStream resolve(ImageConfiguration configuration)
```

Resolves this image provider using the given `configuration`, returning an [ImageStream].

This is the public entry-point of the [ImageProvider] class hierarchy.

Subclasses should implement [obtainKey] and [loadImage], which are used by this method. If they need to change the implementation of [ImageStream] used, they should override [createStream]. If they need to manage the actual resolution of the image, they should override [resolveStreamForKey].

See the Lifecycle documentation on [ImageProvider] for more information.

### createStream()

```dart
ImageStream createStream(ImageConfiguration configuration)
```

Called by [resolve] to create the [ImageStream] it returns.

Subclasses should override this instead of [resolve] if they need to return some subclass of [ImageStream]. The stream created here will be passed to [resolveStreamForKey].

### obtainCacheStatus()

```dart
Future<ImageCacheStatus?> obtainCacheStatus({required ImageConfiguration configuration, ImageErrorListener? handleError})
```

Returns the cache location for the key that this [ImageProvider] creates.

The location may be [ImageCacheStatus.untracked], indicating that this image provider's key is not available in the [ImageCache].

If the `handleError` parameter is null, errors will be reported to [FlutterError.onError], and the method will return null.

A completed return value of null indicates that an error has occurred.

### resolveStreamForKey()

```dart
void resolveStreamForKey(ImageConfiguration configuration, ImageStream stream, T key, ImageErrorListener handleError)
```

Called by [resolve] with the key returned by [obtainKey].

Subclasses should override this method rather than calling [obtainKey] if they need to use a key directly. The [resolve] method installs appropriate error handling guards so that errors will bubble up to the right places in the framework, and passes those guards along to this method via the [handleError] parameter.

It is safe for the implementation of this method to call [handleError] multiple times if multiple errors occur, or if an error is thrown both synchronously into the current part of the stack and thrown into the enclosing [Zone].

The default implementation uses the key to interact with the [ImageCache], calling [ImageCache.putIfAbsent] and notifying listeners of the [stream]. Implementers that do not call super are expected to correctly use the [ImageCache].

### evict()

```dart
Future<bool> evict({ImageCache? cache, ImageConfiguration configuration = ImageConfiguration.empty})
```

Evicts an entry from the image cache.

Returns a [Future] which indicates whether the value was successfully removed.

The [ImageProvider] used does not need to be the same instance that was passed to an [Image] widget, but it does need to create a key which is equal to one.

The [cache] is optional and defaults to the global image cache.

The [configuration] is optional and defaults to [ImageConfiguration.empty].

{@tool snippet}

The following sample code shows how an image loaded using the [Image] widget can be evicted using a [NetworkImage] with a matching URL.

```dart
class MyWidget extends StatelessWidget {
  const MyWidget({
    super.key,
    this.url = ' ... ',
  });

  final String url;

  @override
  Widget build(BuildContext context) {
    return Image.network(url);
  }

  void evictImage() {
    final NetworkImage provider = NetworkImage(url);
    provider.evict().then<void>((bool success) {
      if (success) {
        debugPrint('removed image!');
      }
    });
  }
}
```

{@end-tool}

### obtainKey()

```dart
Future<T> obtainKey(ImageConfiguration configuration)
```

Converts an [ImageProvider]'s settings plus an [ImageConfiguration] to a key that describes the precise image to load.

The type of the key is determined by the subclass. It is a value that unambiguously identifies the image (_including its scale_) that the [loadImage] method will fetch. Different [ImageProvider]s given the same constructor arguments and [ImageConfiguration] objects should return keys that are '==' to each other (possibly by using a class for the key that itself implements [==]).

If the result can be determined synchronously, this function should return a [SynchronousFuture]. This allows image resolution to progress synchronously during a frame rather than delaying image loading.

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(T key, DecoderBufferCallback decode)
```

Converts a key into an [ImageStreamCompleter], and begins fetching the image.

This method is deprecated. Implement [loadImage] instead.

The [decode] callback provides the logic to obtain the codec for the image.

See also:

- [ResizeImage], for modifying the key to account for cache dimensions.

### loadImage()

```dart
ImageStreamCompleter loadImage(T key, ImageDecoderCallback decode)
```

Converts a key into an [ImageStreamCompleter], and begins fetching the image.

For backwards-compatibility the default implementation of this method returns an object that will cause [resolveStreamForKey] to consult [loadBuffer]. However, implementors of this interface should only override this method and not [loadBuffer], which is deprecated.

The [decode] callback provides the logic to obtain the codec for the image.

See also:

- [ResizeImage], for modifying the key to account for cache dimensions.

### toString()

```dart
String toString()
```

# AssetBundleImageKey

```dart
class AssetBundleImageKey {}
```

Key for the image obtained by an [AssetImage] or [ExactAssetImage].

This is used to identify the precise resource in the [imageCache].

### AssetBundleImageKey()

```dart
AssetBundleImageKey({required AssetBundle bundle, required String name, required double scale})
```

Creates the key for an [AssetImage] or [AssetBundleImageProvider].

### bundle

```dart
AssetBundle bundle
```

The bundle from which the image will be obtained.

The image is obtained by calling [AssetBundle.load] on the given [bundle] using the key given by [name].

### name

```dart
String name
```

The key to use to obtain the resource from the [bundle]. This is the argument passed to [AssetBundle.load].

### scale

```dart
double scale
```

The scale to place in the [ImageInfo] object of the image.

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

# AssetBundleImageProvider

```dart
abstract class AssetBundleImageProvider extends ImageProvider<AssetBundleImageKey> {}
```

A subclass of [ImageProvider] that knows about [AssetBundle]s.

This factors out the common logic of [AssetBundle]-based [ImageProvider] classes, simplifying what subclasses must implement to just [obtainKey].

### AssetBundleImageProvider()

```dart
AssetBundleImageProvider()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### loadImage()

```dart
ImageStreamCompleter loadImage(AssetBundleImageKey key, ImageDecoderCallback decode)
```

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(AssetBundleImageKey key, DecoderBufferCallback decode)
```

Converts a key into an [ImageStreamCompleter], and begins fetching the image.

# ResizeImageKey

```dart
class ResizeImageKey {}
```

Key used internally by [ResizeImage].

This is used to identify the precise resource in the [imageCache].

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# ResizeImagePolicy

```dart
enum ResizeImagePolicy {}
```

Configures the behavior for [ResizeImage].

This is used in [ResizeImage.policy] to affect how the [ResizeImage.width] and [ResizeImage.height] properties are interpreted.

Sizes the image to the exact width and height specified by [ResizeImage.width] and [ResizeImage.height].

If [ResizeImage.width] and [ResizeImage.height] are both non-null, the output image will have the specified width and height (with the corresponding aspect ratio) regardless of whether it matches the source image's intrinsic aspect ratio. This case is similar to [BoxFit.fill].

If only one of `width` and `height` is non-null, then the output image will be scaled to the associated width or height, and the other dimension will take whatever value is needed to maintain the image's original aspect ratio. These cases are similar to [BoxFit.fitWidth] and [BoxFit.fitHeight], respectively.

If [ResizeImage.allowUpscaling] is false (the default), the width and the height of the output image will each be clamped to the intrinsic width and height of the image. This may result in a different aspect ratio than the aspect ratio specified by the target width and height (e.g. if the height gets clamped downwards but the width does not).

## Examples

The examples below show how [ResizeImagePolicy.exact] works in various scenarios. In each example, the source image has a size of 300x200 (landscape orientation), the red box is a 150x150 square, and the green box is a 400x400 square.

 <table>
 <tr>
 <td>Scenario</td>
 <td>Output</td>
 </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 150,
  height: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_150x150_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_150xnull_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  height: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_nullx150_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 400,
  height: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_400x400_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_400xnull_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  height: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_nullx400_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 400,
  height: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_400x400_true.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  width: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_400xnull_true.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  height: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_exact_nullx400_true.png)

 </td> </tr> </table>

Scales the image as necessary to ensure that it fits within the bounding box specified by [ResizeImage.width] and [ResizeImage.height] while maintaining its aspect ratio.

If [ResizeImage.allowUpscaling] is true, the image will be scaled up or down to best fit the bounding box; otherwise it will only ever be scaled down.

This is conceptually similar to [BoxFit.contain].

## Examples

The examples below show how [ResizeImagePolicy.fit] works in various scenarios. In each example, the source image has a size of 300x200 (landscape orientation), the red box is a 150x150 square, and the green box is a 400x400 square.

 <table>
 <tr>
 <td>Scenario</td>
 <td>Output</td>
 </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 150,
  height: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_150x150_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_150xnull_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  height: 150,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_nullx150_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 400,
  height: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_400x400_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_400xnull_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  height: 400,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_nullx400_false.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 400,
  height: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_400x400_true.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  width: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_400xnull_true.png)

 </td> </tr>
 <tr>
 <td>

```dart
const ResizeImage(
  AssetImage('dragon_cake.jpg'),
  policy: ResizeImagePolicy.fit,
  height: 400,
  allowUpscaling: true,
)
```

 </td>
 <td>

![](https://flutter.github.io/assets-for-api-docs/assets/painting/resize_image_policy_fit_nullx400_true.png)

 </td> </tr> </table>

# ResizeImage

```dart
class ResizeImage extends ImageProvider<ResizeImageKey> {}
```

Instructs Flutter to decode the image at the specified dimensions instead of at its native size.

This allows finer control of the size of the image in [ImageCache] and is generally used to reduce the memory footprint of [ImageCache].

The decoded image may still be displayed at sizes other than the cached size provided here.

The [width] and [height] parameters determine the image resolution. These values also set the image's width & height in logical pixels if it is unconstrained.

{@tool snippet} This example shows how to size the image to half of the screen's width.

```dart
   Image(
     image: ResizeImage(
       FileImage(File('path/to/image')),
       width: MediaQuery.widthOf(context) ~/ 2, // Half of the screen's width.
     ),
   );
```

{@end-tool}

See also:

- [ui.FlutterView.devicePixelRatio], used to convert between physical and logical pixels.

### ResizeImage()

```dart
ResizeImage(ImageProvider imageProvider, {int? width, int? height, ResizeImagePolicy policy = ResizeImagePolicy.exact, bool allowUpscaling = false})
```

Creates an ImageProvider that decodes the image to the specified size.

The cached image will be directly decoded and stored at the resolution defined by `width` and `height`. The image will lose detail and use less memory if resized to a size smaller than the native size.

At least one of `width` and `height` must be non-null.

### imageProvider

```dart
ImageProvider imageProvider
```

The [ImageProvider] that this class wraps.

### width

```dart
int? width
```

The width the image should decode to and cache.

At least one of this and [height] must be non-null.

### height

```dart
int? height
```

The height the image should decode to and cache.

At least one of this and [width] must be non-null.

### policy

```dart
ResizeImagePolicy policy
```

The policy that determines how [width] and [height] are interpreted.

Defaults to [ResizeImagePolicy.exact].

### allowUpscaling

```dart
bool allowUpscaling
```

Whether the [width] and [height] parameters should be clamped to the intrinsic width and height of the image.

In general, it is better for memory usage to avoid scaling the image beyond its intrinsic dimensions when decoding it. If there is a need to scale an image larger, it is better to apply a scale to the canvas, or to use an appropriate [Image.fit].

### resizeIfNeeded()

```dart
ImageProvider<Object> resizeIfNeeded(int? cacheWidth, int? cacheHeight, ImageProvider<Object> provider)
```

Composes the `provider` in a [ResizeImage] only when `cacheWidth` and `cacheHeight` are not both null.

When `cacheWidth` and `cacheHeight` are both null, this will return the `provider` directly.

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(ResizeImageKey key, DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(ResizeImageKey key, ImageDecoderCallback decode)
```

### obtainKey()

```dart
Future<ResizeImageKey> obtainKey(ImageConfiguration configuration)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# WebHtmlElementStrategy

```dart
enum WebHtmlElementStrategy {}
```

The strategy for [Image.network] and [NetworkImage] to decide whether to display images in HTML elements contained in a platform view instead of fetching bytes.

See [Image.network] for more explanation on the impact.

This option is only effective on the Web platform. Other platforms always display network images by fetching bytes.

Only show images by fetching bytes, and report errors if the fetch encounters errors.

Prefer fetching bytes to display images, and fall back to HTML elements when fetching bytes is not available.

This strategy uses HTML elements only if `headers` is empty and the fetch encounters errors. Errors may still be reported if neither approach works.

Prefer HTML elements to display images, and fall back to fetching bytes when HTML elements do not work.

This strategy fetches bytes only if `headers` is not empty, since HTML elements do not support headers. Errors may still be reported if neither approach works.

# NetworkImage

```dart
abstract class NetworkImage extends ImageProvider<NetworkImage> {}
```

Fetches the given URL from the network, associating it with the given scale.

The image will be cached regardless of cache headers from the server.

Typically this class resolves to an image stream that ultimately produces [dart:ui.Image]s. On the Web platform, the [webHtmlElementStrategy] parameter can be used to make the image stream ultimately produce an [WebImageInfo] instead, which makes [Image.network] display the image as an HTML element in a platform view. The feature is by default turned off ([WebHtmlElementStrategy.never]). See [Image.network] for more explanation.

See also:

- [Image.network] for a shorthand of an [Image] widget backed by [NetworkImage].
- The example at [ImageProvider], which shows a custom variant of this class that applies different logic for fetching the image.

### NetworkImage()

```dart
NetworkImage(String url, {double scale, Map<String, String>? headers, WebHtmlElementStrategy webHtmlElementStrategy})
```

Creates an object that fetches the image at the given URL.

The [scale] argument is the linear scale factor for drawing this image at its intended size. See [ImageInfo.scale] for more information.

The [webHtmlElementStrategy] option is by default [WebHtmlElementStrategy.never].

### url

```dart
String get url
```

The URL from which the image will be fetched.

### scale

```dart
double get scale
```

The scale to place in the [ImageInfo] object of the image.

### headers

```dart
Map<String, String>? get headers
```

The HTTP headers that will be used with [HttpClient.get] to fetch image from network.

When running Flutter on the web, headers are not used.

### webHtmlElementStrategy

```dart
WebHtmlElementStrategy get webHtmlElementStrategy
```

On the Web platform, specifies when the image is loaded as a [WebImageInfo], which causes [Image.network] to display the image in an HTML element in a platform view.

See [Image.network] for more explanation.

Defaults to [WebHtmlElementStrategy.never].

Has no effect on other platforms, which always fetch bytes.

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(NetworkImage key, DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(NetworkImage key, ImageDecoderCallback decode)
```

# FileImage

```dart
class FileImage extends ImageProvider<FileImage> {}
```

Decodes the given [File] object as an image, associating it with the given scale.

The provider does not monitor the file for changes. If you expect the underlying data to change, you should call the [evict] method.

See also:

- [Image.file] for a shorthand of an [Image] widget backed by [FileImage].

### FileImage()

```dart
FileImage(File file, {double scale = 1.0})
```

Creates an object that decodes a [File] as an image.

### file

```dart
File file
```

The file to decode into an image.

### scale

```dart
double scale
```

The scale to place in the [ImageInfo] object of the image.

### obtainKey()

```dart
Future<FileImage> obtainKey(ImageConfiguration configuration)
```

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(FileImage key, DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(FileImage key, ImageDecoderCallback decode)
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

# MemoryImage

```dart
class MemoryImage extends ImageProvider<MemoryImage> {}
```

Decodes the given [Uint8List] buffer as an image, associating it with the given scale.

The provided [bytes] buffer should not be changed after it is provided to a [MemoryImage]. To provide an [ImageStream] that represents an image that changes over time, consider creating a new subclass of [ImageProvider] whose [loadImage] method returns a subclass of [ImageStreamCompleter] that can handle providing multiple images.

See also:

- [Image.memory] for a shorthand of an [Image] widget backed by [MemoryImage].

### MemoryImage()

```dart
MemoryImage(Uint8List bytes, {double scale = 1.0})
```

Creates an object that decodes a [Uint8List] buffer as an image.

### bytes

```dart
Uint8List bytes
```

The bytes to decode into an image.

The bytes represent encoded image bytes and can be encoded in any of the following supported image formats: {@macro dart.ui.imageFormats}

See also:

- [PaintingBinding.instantiateImageCodecWithSize]

### scale

```dart
double scale
```

The scale to place in the [ImageInfo] object of the image.

See also:

- [ImageInfo.scale], which gives more information on how this scale is applied.

### obtainKey()

```dart
Future<MemoryImage> obtainKey(ImageConfiguration configuration)
```

### loadBuffer()

```dart
ImageStreamCompleter loadBuffer(MemoryImage key, DecoderBufferCallback decode)
```

### loadImage()

```dart
ImageStreamCompleter loadImage(MemoryImage key, ImageDecoderCallback decode)
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

# ExactAssetImage

```dart
class ExactAssetImage extends AssetBundleImageProvider {}
```

Fetches an image from an [AssetBundle], associating it with the given scale.

This implementation requires an explicit final [assetName] and [scale] on construction, and ignores the device pixel ratio and size in the configuration passed into [resolve]. For a resolution-aware variant that uses the configuration to pick an appropriate image based on the device pixel ratio and size, see [AssetImage].

## Fetching assets

When fetching an image provided by the app itself, use the [assetName] argument to name the asset to choose. For instance, consider a directory `icons` with an image `heart.png`. First, the `pubspec.yaml` of the project should specify its assets in the `flutter` section:

```yaml
flutter:
  assets:
    - icons/heart.png
```

Then, to fetch the image and associate it with scale `1.5`, use:

{@tool snippet}

```dart
const ExactAssetImage('icons/heart.png', scale: 1.5)
```

{@end-tool}

## Assets in packages

To fetch an asset from a package, the [package] argument must be provided. For instance, suppose the structure above is inside a package called `my_icons`. Then to fetch the image, use:

{@tool snippet}

```dart
const ExactAssetImage('icons/heart.png', scale: 1.5, package: 'my_icons')
```

{@end-tool}

Assets used by the package itself should also be fetched using the [package] argument as above.

If the desired asset is specified in the `pubspec.yaml` of the package, it is bundled automatically with the app. In particular, assets used by the package itself must be specified in its `pubspec.yaml`.

A package can also choose to have assets in its 'lib/' folder that are not specified in its `pubspec.yaml`. In this case for those images to be bundled, the app has to specify which ones to include. For instance a package named `fancy_backgrounds` could have:

lib/backgrounds/background1.png lib/backgrounds/background2.png lib/backgrounds/background3.png

To include, say the first image, the `pubspec.yaml` of the app should specify it in the `assets` section:

```yaml
assets:
  - packages/fancy_backgrounds/backgrounds/background1.png
```

The `lib/` is implied, so it should not be included in the asset path.

See also:

- [Image.asset] for a shorthand of an [Image] widget backed by [ExactAssetImage] when using a scale.

### ExactAssetImage()

```dart
ExactAssetImage(String assetName, {double scale = 1.0, AssetBundle? bundle, String? package})
```

Creates an object that fetches the given image from an asset bundle.

The [scale] argument defaults to 1. The [bundle] argument may be null, in which case the bundle provided in the [ImageConfiguration] passed to the [resolve] call will be used instead.

The [package] argument must be non-null when fetching an asset that is included in a package. See the documentation for the [ExactAssetImage] class itself for details.

### assetName

```dart
String assetName
```

The name of the asset.

### keyName

```dart
String get keyName
```

The key to use to obtain the resource from the [bundle]. This is the argument passed to [AssetBundle.load].

### scale

```dart
double scale
```

The scale to place in the [ImageInfo] object of the image.

### bundle

```dart
AssetBundle? bundle
```

The bundle from which the image will be obtained.

If the provided [bundle] is null, the bundle provided in the [ImageConfiguration] passed to the [resolve] call will be used instead. If that is also null, the [rootBundle] is used.

The image is obtained by calling [AssetBundle.load] on the given [bundle] using the key given by [keyName].

### package

```dart
String? package
```

The name of the package from which the image is included. See the documentation for the [ExactAssetImage] class itself for details.

### obtainKey()

```dart
Future<AssetBundleImageKey> obtainKey(ImageConfiguration configuration)
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

# NetworkImageLoadException

```dart
class NetworkImageLoadException implements Exception {}
```

The exception thrown when the HTTP request to load a network image fails.

### NetworkImageLoadException()

```dart
NetworkImageLoadException({required int statusCode, required Uri uri})
```

Creates a [NetworkImageLoadException] with the specified http [statusCode] and [uri].

### statusCode

```dart
int statusCode
```

The HTTP status code from the server.

### uri

```dart
Uri uri
```

Resolved URL of the requested image.

### toString()

```dart
String toString()
```
