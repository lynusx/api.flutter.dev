@docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'fade_in_image.dart'; @docImport 'icon.dart'; @docImport 'transitions.dart';

# createLocalImageConfiguration()

```dart
ImageConfiguration createLocalImageConfiguration(BuildContext context, {Size? size})
```

根据给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)（以及可选的 size）创建一个 [ImageConfiguration](https://www.yuque.com/thyname/flutter.painting/imageconfiguration)。

该对象必须传递给 [BoxPainter.paint] 以及 [ImageProvider.resolve]。

如果该方法不是在 build 方法中调用的，则应在依赖项发生变化时重新调用，例如通过在 [State.didChangeDependencies] 中调用它，以便捕获环境中的任何变化（例如设备像素比发生变化时）。

另请参阅：

- [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider)，其中包含一个展示该方法用法的示例。

# precacheImage()

```dart
Future<void> precacheImage(ImageProvider provider, BuildContext context, {Size? size, ImageErrorListener? onError})
```

将图片预取到图片缓存中。

返回一个 [Future](https://www.yuque.com/thyname/dart.async/future)，当 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 产生的第一张图片可用或加载失败时，该 Future 将会完成。

如果该图片随后被 [Image](https://www.yuque.com/thyname/dart.ui/image)、[BoxDecoration](https://www.yuque.com/thyname/flutter.painting/boxdecoration) 或 [FadeInImage](https://www.yuque.com/thyname/flutter.widgets/fadeinimage) 使用，其加载速度可能会更快。图片的使用方不必使用同一个 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 实例。只要两张图片共享同一个键（key），[ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 就能够找到该图片，并且该图片会被缓存持有。

如果图片被禁用、图片过大，或者自定义 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 实现所规定的其他条件不满足，缓存可能会拒绝持有该图片。

只要 [ImageStreamCompleter](https://www.yuque.com/thyname/flutter.painting/imagestreamcompleter) 至少有一个监听器，[ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 就会持有传递给 [ImageCache.putIfAbsent] 的所有图片的引用。此方法会在其 Future 完成后，一直等到当前帧结束才会释放自身的监听器。这使调用方有机会在必要时监听该流。调用方可以通过调用 [ImageProvider.obtainCacheStatus] 来判断图片最终是否进入了缓存。如果图片仅以 [ImageCacheStatus.live] 状态被持有，而调用方希望将已解析的图片保留在内存中，则应立即调用 `provider.resolve` 并向返回的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 添加监听器。即使图片原本不适合放入缓存，只要调用方尚未从该流中移除其监听器，该图片就会一直被固定在内存中。

调用方应谨慎处理将大图片或大量图片固定在内存中的情况，因为这可能导致内存耗尽，进而被操作系统终止。可用物理内存越少，调用方就越容易遇到内存不足（OOM）的问题。这类问题通常表现为进程立即终止，有时甚至没有任何其他错误信息。

[BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 和 [Size](https://www.yuque.com/thyname/dart.ui/size) 用于选择图片配置（参见 [createLocalImageConfiguration](https://www.yuque.com/thyname/flutter.widgets/createlocalimageconfiguration)）。

即使预缓存失败，返回的 Future 也不会以错误状态完成。可以使用 `onError` 参数手动处理预缓存过程中出现的错误。

另请参阅：

- [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache)，用于持有可被复用的图片。

# ImageFrameBuilder

```dart
typedef ImageFrameBuilder = Widget Function(BuildContext context, Widget child, int? frame, bool wasSynchronouslyLoaded)
```

[Image.frameBuilder] 使用的签名，用于控制 [Image](https://www.yuque.com/thyname/dart.ui/image) 构建时所使用的组件。

`child` 参数包含默认的图片组件。通常，此构建器会以某种方式包裹 `child` 组件并返回被包裹后的组件。如果此构建器直接返回 `child`，其效果将与 [Image.frameBuilder] 为 null 时相同。

`frame` 参数指定当前正在渲染的图片帧的索引。在第一帧图片就绪之前该值为 null，第一帧图片就绪时该值为零。对于单帧图片，该值永远不会大于零。对于多帧图片（例如动图 GIF），每当显示一个新的图片帧（包括动画循环播放时），该值就会加一。

`wasSynchronouslyLoaded` 参数指定该图片是否是同步可用的（即在 [Image](https://www.yuque.com/thyname/dart.ui/image) 组件本身被创建的同一个[渲染管线帧](rendering/RendererBinding/drawFrame.html)中可用），从而能够被立即绘制。如果该值为 false，则说明存在一个或多个渲染管线帧，在这些帧中图片尚不可被绘制。对于多帧图片（例如动图 GIF），所有图片帧的该参数值都是相同的。换言之，如果第一帧图片是立即可用的，那么该参数在所有图片帧中都将为 true。

另请参阅：

- [Image.frameBuilder]，在 [Image](https://www.yuque.com/thyname/dart.ui/image) 组件中使用该签名。

# ImageLoadingBuilder

```dart
typedef ImageLoadingBuilder = Widget Function(BuildContext context, Widget child, ImageChunkEvent? loadingProgress)
```

[Image.loadingBuilder] 使用的签名，用于构建表示图片加载进度的组件。

这对于以增量方式加载的图片（例如通过本地文件系统或网络加载）非常有用，可用于在应用中向用户展示图片何时会显示。

`child` 参数包含默认的图片组件，并保证非空。通常，此构建器会以某种方式包裹 `child` 组件并返回被包裹后的组件。如果此构建器直接返回 `child`，其效果将与 [Image.loadingBuilder] 为 null 时相同。

`loadingProgress` 参数包含当前图片加载的进度。当图片正在加载时，该参数非空；但在以下情况下该参数为 null：

- 组件首次渲染、尚未加载任何字节时。
- 图片已完全加载完毕、可供绘制时。

如果调用方实现了自定义的 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 和 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 实例（这种情况非常罕见），则有可能产生在图片帧加载完成后仍继续触发图片区块（chunk）事件的图片流。在这种情况下，`child` 参数将代表当前已完全加载的图片帧。

另请参阅：

- [Image.loadingBuilder]，在 [Image](https://www.yuque.com/thyname/dart.ui/image) 组件中使用该签名。
- [ImageChunkListener](https://www.yuque.com/thyname/flutter.painting/imagechunklistener)，一个用于监听原始 [ImageChunkEvent](https://www.yuque.com/thyname/flutter.painting/imagechunkevent) 的更底层签名。

# ImageErrorWidgetBuilder

```dart
typedef ImageErrorWidgetBuilder = Widget Function(BuildContext context, Object error, StackTrace? stackTrace)
```

[Image.errorBuilder] 使用的签名，用于创建一个替代组件，以代替图片进行渲染。

# Image

```dart
class Image extends StatefulWidget {}
```

一个用于显示图片的组件。

{@youtube 560 315 https://www.youtube.com/watch?v=7oIAs-0G4mw}

框架提供了多个构造函数，以支持多种指定图片的方式：

- [Image.new]，从 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 获取图片。
- [Image.asset]，通过键从 [AssetBundle](https://www.yuque.com/thyname/flutter.services/assetbundle) 获取图片。
- [Image.network]，从 URL 获取图片。
- [Image.file]，从 [File](https://www.yuque.com/thyname/dart.io/file) 获取图片。
- [Image.memory]，从 [Uint8List](https://www.yuque.com/thyname/dart.typed_data/uint8list) 获取图片。

支持以下图片格式：{@macro dart.ui.imageFormats}

若要自动执行基于像素密度的资源解析，请使用 [AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage) 指定图片，并确保在 [Image](https://www.yuque.com/thyname/dart.ui/image) 组件树的上层存在 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)、[WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 或 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 组件。

图片使用 [paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 进行绘制，该方法详细说明了此类中各个字段的含义。

{@tool snippet} 默认构造函数可与任何 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider)（例如 [NetworkImage](https://www.yuque.com/thyname/flutter.painting/networkimage)）配合使用，以显示来自网络的图片。

![显示图片组件所展示的一只猫头鹰图片](https://flutter.github.io/assets-for-api-docs/assets/widgets/owl.jpg)

```dart
const Image(
  image: NetworkImage('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl.jpg'),
)
```

{@end-tool}

{@tool snippet} [Image](https://www.yuque.com/thyname/dart.ui/image) 组件还提供了多个构造函数，便于显示不同类型的图片。本示例中，使用 [Image.network] 构造函数显示一张来自网络的图片。

![使用快捷构造函数、由图片组件展示的一只猫头鹰图片](https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg)

```dart
Image.network('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg')
```

{@end-tool}

多帧图片（例如动图 GIF）在 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode) 被禁用时会暂停，与其他动画的行为一致。当动画通过 [MediaQueryData.disableAnimations]（例如出于无障碍目的）被禁用时，它们同样会暂停。如果图片首次加载时动画就已被暂停，则会显示第一帧，随后动画将停止。

{@tool snippet} / 使用 [TickerMode](https://www.yuque.com/thyname/flutter.widgets/tickermode) 暂停多帧图片的示例。

```dart
TickerMode(
  enabled: !isPaused,
  child: Image(image: myAnimatedGif),
),
```

{@end-tool}

## 内存占用

图片以未压缩的形式存储在内存中（以便能够被渲染）。较大的图片会占用大量内存：一张 4K 图片（3840×2160）在假设每像素 32 位的情况下，将占用超过 30MB 的内存。

由于这些图片会被缓存到 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 中，这一问题会进一步加剧——大图片占用内存的时间可能会远超其实际显示的时间。

[Image.asset]、[Image.network]、[Image.file] 和 [Image.memory] 构造函数允许通过 `cacheWidth` 和 `cacheHeight` 参数指定自定义的解码尺寸。此后，引擎将按照指定的尺寸而非图片的原始尺寸对图片进行解码和存储。

这可以显著降低内存占用。例如，一张 4K 图片如果实际渲染尺寸仅为 384×216 像素（水平和垂直方向均为原尺寸的十分之一），若通过 `cacheWidth` 和 `cacheHeight` 参数指定该尺寸，则仅占用 330KB 内存，内存占用降低了 100 倍。

## 自定义图片提供者

{@tool sample} 本示例创建了一个 [NetworkImage](https://www.yuque.com/thyname/flutter.painting/networkimage) 的变体，它会将所有 [ImageConfiguration](https://www.yuque.com/thyname/flutter.painting/imageconfiguration) 信息（区域设置、平台、尺寸等）通过图片 URL 中的查询参数一并传递给服务器。

** 请参见 examples/api/lib/painting/image_provider/image_provider.0.dart 中的代码 ** {@end-tool}

另请参阅：

- [Icon](https://www.yuque.com/thyname/flutter.widgets/icon)，从字体显示图片。
- [Ink.image]，在 Material 应用中显示图片的首选方式（尤其是当图片位于 [Material](https://www.yuque.com/thyname/flutter.material/material) 中，且其上方带有 [InkWell](https://www.yuque.com/thyname/flutter.material/inkwell) 时）。
- [Image](https://www.yuque.com/thyname/dart.ui/image)，[dart:ui](https://www.yuque.com/thyname/dart.ui) 库中的类。
- 参考手册：[从网络显示图片](https://docs.flutter.dev/cookbook/images/network-image)
- 参考手册：[使用占位符渐显图片](https://docs.flutter.dev/cookbook/images/fading-in-images)

### Image()

```dart
Image({dynamic key, required ImageProvider image, ImageFrameBuilder? frameBuilder, ImageLoadingBuilder? loadingBuilder, ImageErrorWidgetBuilder? errorBuilder, String? semanticLabel, bool excludeFromSemantics = false, double? width, double? height, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool gaplessPlayback = false, bool isAntiAlias = false, FilterQuality filterQuality = FilterQuality.medium})
```

创建一个用于显示图片的组件。

若要显示来自网络或资源包的图片，请考虑分别使用 [Image.network] 和 [Image.asset]。

应当指定 [width] 和 [height] 参数，或者将该组件放置在具有严格布局约束的上下文中。否则，图片加载过程中其尺寸会发生变化，从而导致不美观的布局跳动。

{@template flutter.widgets.image.filterQualityParameter} 使用 [filterQuality] 指定图片的渲染质量。{@endtemplate}

如果 [excludeFromSemantics] 为 true，则 [semanticLabel] 将被忽略。

### Image.network()

```dart
Image.network(String src, {dynamic key, double scale = 1.0, ImageFrameBuilder? frameBuilder, ImageLoadingBuilder? loadingBuilder, ImageErrorWidgetBuilder? errorBuilder, String? semanticLabel, bool excludeFromSemantics = false, double? width, double? height, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool gaplessPlayback = false, FilterQuality filterQuality = FilterQuality.medium, bool isAntiAlias = false, Map<String, String>? headers, int? cacheWidth, int? cacheHeight, WebHtmlElementStrategy webHtmlElementStrategy = WebHtmlElementStrategy.never})
```

创建一个用于显示从网络获取的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 的组件。

应当指定 [width] 和 [height] 参数，或者将该组件放置在具有严格布局约束的上下文中。否则，图片加载过程中其尺寸会发生变化，从而导致不美观的布局跳动。

`scale` 参数指定以图片原本大小绘制该图片时所使用的线性缩放因子，同时适用于宽度和高度。{@macro flutter.painting.imageInfo.scale}

无论 HTTP 头信息如何，所有网络图片都会被缓存。

可选参数 [headers] 可用于在图片请求中发送自定义 HTTP 头。

{@macro flutter.widgets.image.filterQualityParameter}

如果 [excludeFromSemantics] 为 true，则 [semanticLabel] 将被忽略。

如果提供了 `cacheWidth` 或 `cacheHeight`，则表示引擎应按照指定尺寸对图片进行解码。无论这些参数如何设置，图片都会根据布局约束或 [width]、[height] 进行渲染。这些参数主要用于降低 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

在 Web 平台上，网络图片会忽略 [cacheWidth] 和 [cacheHeight] 参数，因为 Web 引擎将图片解码工作委托给了浏览器，而浏览器不支持自定义解码尺寸。

### Web 平台上的同源策略

由于浏览器对跨域资源共享（CORS）的限制，在 Web 平台上，除非图片托管源明确允许，否则 Flutter 无法从与托管应用的源（域名、协议或端口）不同的其他源获取图片。可以通过配置图片托管服务器来解决 CORS 错误。更多信息请参见 Mozilla 关于[同源策略](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)和 [CORS 错误](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors)的介绍。

如果无法配置托管服务器（例如图片托管在 CDN 上或来自任意 URL），应用可以将 [Image.network] 的 `webHtmlElementStrategy` 参数设置为在 HTML 元素中显示图片，从而绕过同源策略限制。

该 HTML 元素被放置在一个平台视图（platform view）中，因此存在以下缺点：

- 性能欠佳。
- 无法被截图组件捕获。
- `headers` 参数必须为空或 null。
- 部分图片选项会被忽略，包括 [opacity]、[colorBlendMode]、[repeat]、滤镜以及模糊效果。

默认情况下，该功能处于关闭状态（[WebHtmlElementStrategy.never]）。

### Android 权限

从网络获取图片需要网络访问权限。请确保所有 AndroidMainifest.xml 变体（尤其是 release 版本）均已配置该网络权限。更多信息请参见 https://docs.flutter.dev/data-and-backend/networking 。

### Image.file()

```dart
Image.file(File file, {dynamic key, double scale = 1.0, ImageFrameBuilder? frameBuilder, ImageErrorWidgetBuilder? errorBuilder, String? semanticLabel, bool excludeFromSemantics = false, double? width, double? height, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool gaplessPlayback = false, bool isAntiAlias = false, FilterQuality filterQuality = FilterQuality.medium, int? cacheWidth, int? cacheHeight})
```

创建一个用于显示从 [File](https://www.yuque.com/thyname/dart.io/file) 获取的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 的组件。

`scale` 参数指定以图片原本大小绘制该图片时所使用的线性缩放因子，同时适用于宽度和高度。{@macro flutter.painting.imageInfo.scale}

应当指定 [width] 和 [height] 参数，或者将该组件放置在具有严格布局约束的上下文中。否则，图片加载过程中其尺寸会发生变化，从而导致不美观的布局跳动。

在 Android 上，这可能需要 `android.permission.READ_EXTERNAL_STORAGE` 权限。

{@macro flutter.widgets.image.filterQualityParameter}

如果 [excludeFromSemantics] 为 true，则 [semanticLabel] 将被忽略。

如果提供了 `cacheWidth` 或 `cacheHeight`，则表示引擎必须按照指定尺寸对图片进行解码。无论这些参数如何设置，图片都会根据布局约束或 [width]、[height] 进行渲染。这些参数主要用于降低 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

从文件加载图片会在内存中创建该文件的一份副本，并保留在 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 中。系统不会监视底层文件的变化。如果文件发生了变化，应用应从 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 中清除相应条目。

另请参阅：

- [FileImage](https://www.yuque.com/thyname/flutter.painting/fileimage) 提供者，便于清除底层文件。

### Image.asset()

```dart
Image.asset(String name, {dynamic key, AssetBundle? bundle, ImageFrameBuilder? frameBuilder, ImageErrorWidgetBuilder? errorBuilder, String? semanticLabel, bool excludeFromSemantics = false, double? scale, double? width, double? height, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool gaplessPlayback = false, bool isAntiAlias = false, String? package, FilterQuality filterQuality = FilterQuality.medium, int? cacheWidth, int? cacheHeight})
```

创建一个用于显示从资源包中获取的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 的组件。该图片的键由 `name` 参数给出。

在从包中显示图片时，`package` 参数必须为非空；否则该参数应为 null。详情参见"包中的资源"一节。

如果省略 `bundle` 参数或其为 null，则使用 [DefaultAssetBundle](https://www.yuque.com/thyname/flutter.widgets/defaultassetbundle)。

`scale` 参数指定以图片原本大小绘制该图片时所使用的线性缩放因子，同时适用于宽度和高度。{@macro flutter.painting.imageInfo.scale}

默认情况下，系统会尝试进行基于像素密度的资源解析。此外：

- 如果提供了 `scale` 参数且其不为 null，则会使用所指定的确切资源。若要显示具有特定密度的图片变体，必须提供确切的路径（例如 `images/2x/cat.png`）。

如果 [excludeFromSemantics] 为 true，则 [semanticLabel] 将被忽略。

如果提供了 `cacheWidth` 或 `cacheHeight`，则表示引擎必须按照指定尺寸对图片进行解码。无论这些参数如何设置，图片都会根据布局约束或 [width]、[height] 进行渲染。这些参数主要用于降低 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

应当指定 [width] 和 [height] 参数，或者将该组件放置在具有严格布局约束的上下文中。否则，图片加载过程中其尺寸会发生变化，从而导致不美观的布局跳动。

{@macro flutter.widgets.image.filterQualityParameter}

{@tool snippet}

假设项目的 `pubspec.yaml` 文件包含以下内容：

```yaml
flutter:
  assets:
    - images/cat.png
    - images/2x/cat.png
    - images/3.5x/cat.png
```

{@end-tool}

在设备像素比为 2.0 的屏幕上，以下组件将会渲染 `images/2x/cat.png` 文件：

```dart
Image.asset('images/cat.png')
```

这对应于项目 `images/2x/` 目录下名为 `cat.png` 的文件（路径相对于 `pubspec.yaml` 文件）。

在设备像素比为 4.0 的设备上，将使用 `images/3.5x/cat.png` 资源。在设备像素比为 1.0 的设备上，将使用 `images/cat.png` 资源。

可以在磁盘中省略 `images/cat.png` 图片（不过其仍必须存在于清单中）。如果省略了该文件，那么在设备像素比为 1.0 的设备上，将改用 `images/2x/cat.png` 图片。

## 包中的资源

要使用包中的资源创建组件，必须提供 [package] 参数。例如，假设某个名为 `my_icons` 的包中含有 `icons/heart.png`。

{@tool snippet} 那么，要显示该图片，可使用：

```dart
Image.asset('icons/heart.png', package: 'my_icons')
```

{@end-tool}

包自身所使用的资源，也应当像上面这样通过 [package] 参数来显示。

如果所需资源已在包的 `pubspec.yaml` 中指定，它就会随应用自动打包。特别地，包自身所使用的资源必须在其 `pubspec.yaml` 中指定。

包也可以选择在其 `lib/` 文件夹中存放未在其 `pubspec.yaml` 中指定的资源。在这种情况下，若要打包这些图片，应用必须指定需要包含哪些图片。例如，一个名为 `fancy_backgrounds` 的包可能包含：

lib/backgrounds/background1.png lib/backgrounds/background2.png lib/backgrounds/background3.png

要包含（例如）第一张图片，应用的 `pubspec.yaml` 应在 assets 部分中指定它：

```yaml
assets:
  - packages/fancy_backgrounds/backgrounds/background1.png
```

`lib/` 是隐含的，因此不应包含在资源路径中。

另请参阅：

- [AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage)，用于实现省略 scale 时的行为。
- [ExactAssetImage](https://www.yuque.com/thyname/flutter.painting/exactassetimage)，用于实现存在 scale 时的行为。
- <https://docs.flutter.dev/ui/assets/assets-and-images>，Flutter 中关于资源的介绍。

### Image.memory()

```dart
Image.memory(Uint8List bytes, {dynamic key, double scale = 1.0, ImageFrameBuilder? frameBuilder, ImageErrorWidgetBuilder? errorBuilder, String? semanticLabel, bool excludeFromSemantics = false, double? width, double? height, Color? color, Animation<double>? opacity, BlendMode? colorBlendMode, BoxFit? fit, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, Rect? centerSlice, bool matchTextDirection = false, bool gaplessPlayback = false, bool isAntiAlias = false, FilterQuality filterQuality = FilterQuality.medium, int? cacheWidth, int? cacheHeight})
```

创建一个用于显示从 [Uint8List](https://www.yuque.com/thyname/dart.typed_data/uint8list) 获取的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream) 的组件。

`bytes` 参数指定已编码的图片字节数据，可以使用以下任一受支持的图片格式进行编码：{@macro dart.ui.imageFormats}

`scale` 参数指定以图片原本大小绘制该图片时所使用的线性缩放因子，同时适用于宽度和高度。{@macro flutter.painting.imageInfo.scale}

该方法仅接受压缩图片格式（例如 PNG）。未压缩格式（例如 [dart:ui.Image.toByteData] 的默认格式 rawRgba）将导致异常。

应当指定 [width] 和 [height] 参数，或者将该组件放置在具有严格布局约束的上下文中。否则，图片加载过程中其尺寸会发生变化，从而导致不美观的布局跳动。

{@macro flutter.widgets.image.filterQualityParameter}

如果 [excludeFromSemantics] 为 true，则 [semanticLabel] 将被忽略。

如果提供了 `cacheWidth` 或 `cacheHeight`，则表示引擎必须按照指定尺寸对图片进行解码。无论这些参数如何设置，图片都会根据布局约束或 [width]、[height] 进行渲染。这些参数主要用于降低 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

### image

```dart
ImageProvider image
```

要显示的图片。

### frameBuilder

```dart
ImageFrameBuilder? frameBuilder
```

一个构建函数，负责创建代表此图片的组件。

如果为 null，此组件将在第一帧图片可用后立即显示该图片（如果图片是异步可用的，则会出现"弹出"效果）。调用方可以使用此构建器为图片添加效果（例如在图片变为可用时进行渐显），或在图片加载期间显示占位组件。

有关传递给此构建器的参数的更多信息，请参见 [ImageFrameBuilder](https://www.yuque.com/thyname/flutter.widgets/imageframebuilder) 的文档。

若要更精细地控制图片加载进度如何传达给用户，请参见 [loadingBuilder]。

## 与 [loadingBuilder] 链式组合

如果同时为图片指定了 [loadingBuilder]，两个构建器将被链接在一起：此构建器的*结果*将作为 `child` 参数传递给 [loadingBuilder]。例如，考虑以下联合使用的构建器：

{@template flutter.widgets.Image.frameBuilder.chainedBuildersExample}

```dart
Image(
  image: _image,
  frameBuilder: (BuildContext context, Widget child, int? frame, bool? wasSynchronouslyLoaded) {
    return Padding(
      padding: const EdgeInsets.all(8.0),
      child: child,
    );
  },
  loadingBuilder: (BuildContext context, Widget child, ImageChunkEvent? loadingProgress) {
    return Center(child: child);
  },
)
```

在此示例中，组件层级结构将包含以下内容：

```dart
Center(
  child: Padding(
    padding: const EdgeInsets.all(8.0),
    child: image,
  ),
),
```

{@endtemplate}

{@tool dartpad} 以下示例演示了如何使用此构建器实现图片加载完成后渐显的效果。

本示例包含了 [FadeInImage](https://www.yuque.com/thyname/flutter.widgets/fadeinimage) 组件开箱即用功能的一个有限子集。

** 请参见 examples/api/lib/widgets/image/image.frame_builder.0.dart 中的代码 ** {@end-tool}

### loadingBuilder

```dart
ImageLoadingBuilder? loadingBuilder
```

一个构建器，用于指定图片仍在加载时向用户展示的组件。

如果为 null，且图片是增量加载的（例如通过网络加载），用户将无法获知图片字节的加载进度。

有关传递给此构建器的参数的更多信息，请参见 [ImageLoadingBuilder](https://www.yuque.com/thyname/flutter.widgets/imageloadingbuilder) 的文档。

## 性能影响

如果为图片指定了 [loadingBuilder]，[Image](https://www.yuque.com/thyname/dart.ui/image) 组件很可能会在图片加载完成之前的每个[渲染管线帧](rendering/RendererBinding/drawFrame.html)中都被重建。这对于诸如显示加载进度指示器之类的场景很有用，但对于更简单的场景（例如显示一个不依赖于加载进度的静态占位组件，如静态的"loading"文字），使用 [frameBuilder] 可能同样能够满足需求，且开销更小。

## 与 [frameBuilder] 链式组合

如果同时为图片指定了 [frameBuilder]，两个构建器将被链接在一起：传递给此构建器的 `child` 参数将包含 [frameBuilder] 的*结果*。例如，考虑以下联合使用的构建器：

{@macro flutter.widgets.Image.frameBuilder.chainedBuildersExample}

{@tool dartpad} 以下示例使用 [loadingBuilder] 在图片通过网络加载期间显示 [CircularProgressIndicator](https://www.yuque.com/thyname/flutter.material/circularprogressindicator)。

** 请参见 examples/api/lib/widgets/image/image.loading_builder.0.dart 中的代码 ** {@end-tool}

在真实网络环境下，针对慢速网络运行前述示例时，会在图片加载完成、渲染出最终图片之前，渲染出如下所示的加载进度指示器。

{@animation 400 400 https://flutter.github.io/assets-for-api-docs/assets/widgets/loading_progress_image.mp4}

### errorBuilder

```dart
ImageErrorWidgetBuilder? errorBuilder
```

图片加载过程中发生错误时调用的构建函数。

如果未提供此构建器，任何异常都会上报给 [FlutterError.onError]。如果提供了此构建器，调用方应当要么通过提供替代组件来处理该异常，要么重新抛出该异常。

{@tool dartpad} 以下示例使用 [errorBuilder] 在图片加载失败时显示"Image failed to load"文字来代替图片，并将错误信息打印到控制台。

** 请参见 examples/api/lib/widgets/image/image.error_builder.0.dart 中的代码 ** {@end-tool}

### width

```dart
double? width
```

如果非空，则要求图片具有此宽度（以逻辑像素为单位）。

如果为 null，图片会选择一个能够最好地保持其固有宽高比的尺寸。

强烈建议同时指定 [width] 和 [height]，或者将该组件放置在具有严格布局约束的上下文中，以避免图片在加载过程中改变尺寸。如果无法提前获知确切的图片尺寸，可以考虑使用 [fit] 来使图片的渲染方式适应给定的宽度和高度。

### height

```dart
double? height
```

如果非空，则要求图片具有此高度（以逻辑像素为单位）。

如果为 null，图片会选择一个能够最好地保持其固有宽高比的尺寸。

强烈建议同时指定 [width] 和 [height]，或者将该组件放置在具有严格布局约束的上下文中，以避免图片在加载过程中改变尺寸。如果无法提前获知确切的图片尺寸，可以考虑使用 [fit] 来使图片的渲染方式适应给定的宽度和高度。

### color

```dart
Color? color
```

如果非空，此颜色会通过 [colorBlendMode] 与每个图片像素进行混合。

### opacity

```dart
Animation<double>? opacity
```

如果非空，在绘制到画布之前，会将 [Animation](https://www.yuque.com/thyname/flutter.animation/animation) 的值与每个图片像素的不透明度相乘。

这比使用 [FadeTransition](https://www.yuque.com/thyname/flutter.widgets/fadetransition) 更改图片的不透明度更加高效，因为后者需要创建新的合成图层。合成图层可能会使内存占用翻倍，因为图片会被绘制到一个离屏渲染目标上。

另请参阅：

- [AlwaysStoppedAnimation](https://www.yuque.com/thyname/flutter.animation/alwaysstoppedanimation)，可用于根据单一不透明度值创建 [Animation](https://www.yuque.com/thyname/flutter.animation/animation)。

### filterQuality

```dart
FilterQuality filterQuality
```

图片的渲染质量。

{@template flutter.widgets.image.filterQuality} 如果图片本身质量很高，且其像素与物理屏幕像素完美对齐，则可能不需要额外的质量增强。在这种情况下，[FilterQuality.none] 将是效率最高的选择。

如果像素与屏幕像素未完美对齐，或者图片本身质量较低，[FilterQuality.none] 可能会产生不理想的伪影。在这种情况下，可以考虑使用其他 [FilterQuality](https://www.yuque.com/thyname/dart.ui/filterquality) 值来改善渲染出的图片质量。由于变换或缩放的原因，像素可能会与屏幕像素错位。

默认为 [FilterQuality.medium]。

另请参阅：

- [FilterQuality](https://www.yuque.com/thyname/dart.ui/filterquality)，包含所有可能的滤镜质量选项的枚举。{@endtemplate}

### colorBlendMode

```dart
BlendMode? colorBlendMode
```

用于将 [color] 与该图片进行组合。

默认值为 [BlendMode.srcIn]。就混合模式而言，[color] 是源（source），该图片是目标（destination）。

另请参阅：

- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)，其中包含各混合模式效果的示意说明。

### fit

```dart
BoxFit? fit
```

在布局过程中分配的空间内，如何嵌入该图片。

默认值因其他字段而异。详情参见 [paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 中的相关讨论。

### alignment

```dart
AlignmentGeometry alignment
```

如何在其边界内对齐该图片。

对齐方式会将图片中给定的位置与布局边界中给定的位置对齐。例如，[Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值为 (-1.0, -1.0) 会将图片对齐到其布局边界的左上角，而 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 值为 (1.0, 1.0) 会将图片的右下角与其布局边界的右下角对齐。类似地，对齐值 (0.0, 1.0) 会将图片底部中点与其布局边界底部边缘的中点对齐。

若要显示图片的某一子部分，可以考虑使用 [CustomPainter](https://www.yuque.com/thyname/flutter.rendering/custompainter) 和 [Canvas.drawImageRect]。

如果 [alignment] 依赖于 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)（即它是一个 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)），则作用域内必须存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含了便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，类似于 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，但用于指定相对于文本方向的对齐方式。

### repeat

```dart
ImageRepeat repeat
```

如何绘制布局边界内未被图片覆盖的部分。

### centerSlice

```dart
Rect? centerSlice
```

九宫格图片（nine-patch image）的中心切片。

图片中位于中心切片内的区域将同时在水平和垂直方向上被拉伸，以适应目标尺寸。中心切片上方和下方的区域仅会在水平方向上被拉伸，而中心切片左侧和右侧的区域仅会在垂直方向上被拉伸。

### matchTextDirection

```dart
bool matchTextDirection
```

是否按照 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection) 的方向绘制图片。

如果为 true，则在 [TextDirection.ltr] 上下文中，图片将以其原点位于左上角进行绘制（即图片的"正常"绘制方向）；而在 [TextDirection.rtl] 上下文中，图片将在水平方向上以 -1 的缩放因子进行绘制，从而使其原点位于右上角。

这偶尔用于从右到左的环境中显示那些原本为从左到右语言区域设计的图片。使用此选项时应格外小心，避免翻转带有完整阴影、文字或其他效果的图片，因为翻转后这些内容会显得不正确。

如果此项为 true，则作用域内必须存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件。

### gaplessPlayback

```dart
bool gaplessPlayback
```

当图片提供者发生变化时，是继续显示旧图片（true），还是短暂显示空白（false，默认值）。

## 设计讨论

### 为什么 [gaplessPlayback] 的默认值是 false？

将 [gaplessPlayback] 的默认值设为 false 有助于避免出现展示过期或误导性信息的情况。考虑以下场景：

假设我们构建了一个 “Person” 组件，用于显示当前已加载人物的头像 [Image](https://www.yuque.com/thyname/dart.ui/image) 及其姓名。我们可以在任意时刻请求将一个新的人物加载到该组件中。假设当前已加载了某个人物，此时组件加载了一个新的人物。如果此时 [Image](https://www.yuque.com/thyname/dart.ui/image) 加载失败，会发生什么？

- 选项 A（[gaplessPlayback] = false）：新人物的姓名会与一张空白图片一同显示。

- 选项 B（[gaplessPlayback] = true）：组件会显示上一个人物的头像，同时显示新加载人物的姓名。

这正是默认值为 false 的原因。多数情况下，更换图片提供者时，你并不仅仅是在更换图片本身——你实际上是在移除旧组件、添加新组件，并不希望这两者之间存在任何关联。启用 [gaplessPlayback] 后，你可能会在无意间打破这一预期，从而意外复用了旧组件。

### semanticLabel

```dart
String? semanticLabel
```

对图片的语义描述。

用于在 Android 上为 TalkBack、在 iOS 上为 VoiceOver 提供该图片的说明。

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

是否将此图片排除在语义之外。

适用于那些不为应用提供有意义信息的图片。

### isAntiAlias

```dart
bool isAntiAlias
```

是否以抗锯齿方式绘制该图片。

抗锯齿可以缓解图片旋转时产生的锯齿状伪影。
