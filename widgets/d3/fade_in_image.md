# FadeInImage

```dart
class FadeInImage extends StatefulWidget {}
```

在目标图片（[image]）加载期间显示占位图片（[placeholder]），加载完成后再淡入新图片的图片 widget。

使用此类来显示加载时间较长的图片（例如 [NetworkImage.new]），使图片以优雅的动画效果出现在屏幕上，而不是突然弹出。

{@youtube 560 315 https://www.youtube.com/watch?v=pK738Pg9cxc}

如果 [image] 同步发出了一个 [ImageInfo](https://www.yuque.com/thyname/flutter.painting/imageinfo)（例如图片已加载并被缓存的情况），则会立即显示该 [image]，[placeholder] 将永远不会显示。

[fadeOutDuration] 和 [fadeOutCurve] 属性用于控制 [placeholder] 的淡出动画。

[fadeInDuration] 和 [fadeInCurve] 属性用于控制目标图片 [image] 的淡入动画。

建议使用已缓存的 [placeholder]，以便它能够立即显示，从而避免它突然出现在屏幕上。

当 [image] 发生变化时，它会被解析为一个新的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream)。如果新的 [ImageStream.key] 不同，此 widget 会订阅新的流，并用新流发出的图片替换当前显示的图片。

当 [placeholder] 发生变化且 [image] 尚未发出 [ImageInfo](https://www.yuque.com/thyname/flutter.painting/imageinfo) 时，[placeholder] 会被解析为一个新的 [ImageStream](https://www.yuque.com/thyname/flutter.painting/imagestream)。如果新的 [ImageStream.key] 不同，此 widget 会订阅新的流，并用新流发出的图片替换当前显示的图片。

当 [placeholder] 或 [image] 发生变化时，此 widget 会持续显示先前已加载的图片（如果有），直到新的图片提供者提供了不同的图片。这被称为“无缝播放”（gapless playback，另见 [Image.gaplessPlayback]）。

{@tool snippet}

```dart
FadeInImage(
  // here `bytes` is a Uint8List containing the bytes for the in-memory image
  placeholder: MemoryImage(bytes),
  image: const NetworkImage('https://backend.example.com/image.png'),
)
```

{@end-tool}

### FadeInImage()

```dart
FadeInImage({dynamic key, required ImageProvider placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required ImageProvider image, ImageErrorWidgetBuilder? imageErrorBuilder, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, double? width, double? height, BoxFit? fit, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false})
```

创建一个 widget，用于在 [image] 加载期间显示 [placeholder]，加载完成后将占位图片淡出并将目标图片淡入。

[placeholder] 和 [image] 可以组合在 [ResizeImage](https://www.yuque.com/thyname/flutter.painting/resizeimage) 中，以提供自定义的解码/缓存尺寸。

[placeholder] 和 [image] 可以通过 [fit] 和 [placeholderFit] 分别设置各自的 BoxFit。

[placeholder] 和 [image] 可以通过 [filterQuality] 和 [placeholderFilterQuality] 分别设置各自的 FilterQuality。

如果 [excludeFromSemantics] 为 true，则 [imageSemanticLabel] 将被忽略。

### FadeInImage.memoryNetwork()

```dart
FadeInImage.memoryNetwork({dynamic key, required Uint8List placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required String image, ImageErrorWidgetBuilder? imageErrorBuilder, double placeholderScale = 1.0, double imageScale = 1.0, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, double? width, double? height, BoxFit? fit, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false, int? placeholderCacheWidth, int? placeholderCacheHeight, int? imageCacheWidth, int? imageCacheHeight})
```

创建一个 widget，在从网络加载最终图片期间使用存储在内存中的占位图片。

`placeholder` 参数包含内存中图片的字节数据。

`image` 参数是最终图片的 URL。

`placeholderScale` 和 `imageScale` 参数会被传递给各自的 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider)（另见 [ImageInfo.scale]）。

如果提供了 [placeholderCacheWidth]、[placeholderCacheHeight]、[imageCacheWidth] 或 [imageCacheHeight]，则会告知引擎按指定尺寸解码相应的图片。无论这些参数如何设置，图片都会按照布局的约束或 [width] 与 [height] 进行渲染。这些参数主要用于减少 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

另请参阅：

- [Image.memory]，其中有关于从内存加载图片的更多详情。
- [Image.network]，其中有关于从网络加载图片的更多详情。

### FadeInImage.assetNetwork()

```dart
FadeInImage.assetNetwork({dynamic key, required String placeholder, ImageErrorWidgetBuilder? placeholderErrorBuilder, required String image, ImageErrorWidgetBuilder? imageErrorBuilder, AssetBundle? bundle, double? placeholderScale, double imageScale = 1.0, bool excludeFromSemantics = false, String? imageSemanticLabel, Duration fadeOutDuration = const Duration(milliseconds: 300), Curve fadeOutCurve = Curves.easeOut, Duration fadeInDuration = const Duration(milliseconds: 700), Curve fadeInCurve = Curves.easeIn, double? width, double? height, BoxFit? fit, Color? color, BlendMode? colorBlendMode, Color? placeholderColor, BlendMode? placeholderColorBlendMode, BoxFit? placeholderFit, FilterQuality filterQuality = FilterQuality.medium, FilterQuality? placeholderFilterQuality, AlignmentGeometry alignment = Alignment.center, ImageRepeat repeat = ImageRepeat.noRepeat, bool matchTextDirection = false, int? placeholderCacheWidth, int? placeholderCacheHeight, int? imageCacheWidth, int? imageCacheHeight})
```

创建一个 widget，在从网络加载最终图片期间使用存储在资源包（asset bundle）中的占位图片。

`placeholder` 参数是资源包中图片的键。

`image` 参数是最终图片的 URL。

`placeholderScale` 和 `imageScale` 参数会被传递给各自的 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider)（另见 [ImageInfo.scale]）。

如果省略 `placeholderScale` 或其为 null，将尝试对 [placeholder] 图片进行像素密度感知的资源解析。否则，将使用指定的确切资源。

如果提供了 [placeholderCacheWidth]、[placeholderCacheHeight]、[imageCacheWidth] 或 [imageCacheHeight]，则会告知引擎按指定尺寸解码相应的图片。无论这些参数如何设置，图片都会按照布局的约束或 [width] 与 [height] 进行渲染。这些参数主要用于减少 [ImageCache](https://www.yuque.com/thyname/flutter.painting/imagecache) 的内存占用。

另请参阅：

- [Image.asset]，其中有关于从资源包加载图片的更多详情。
- [Image.network]，其中有关于从网络加载图片的更多详情。

### placeholder

```dart
ImageProvider placeholder
```

在目标图片 [image] 加载期间显示的图片。

### placeholderErrorBuilder

```dart
ImageErrorWidgetBuilder? placeholderErrorBuilder
```

在占位图片加载过程中发生错误时调用的构建函数。

如果未提供此构建函数，任何异常都会报告给 [FlutterError.onError]。如果提供了此构建函数，调用方应通过提供替代 widget 来处理该异常，或者重新抛出该异常。

### image

```dart
ImageProvider image
```

加载完成后显示的目标图片。

### imageErrorBuilder

```dart
ImageErrorWidgetBuilder? imageErrorBuilder
```

在图片加载过程中发生错误时调用的构建函数。

如果未提供此构建函数，任何异常都会报告给 [FlutterError.onError]。如果提供了此构建函数，调用方应通过提供替代 widget 来处理该异常，或者重新抛出该异常。

### fadeOutDuration

```dart
Duration fadeOutDuration
```

[placeholder] 淡出动画的持续时间。

### fadeOutCurve

```dart
Curve fadeOutCurve
```

[placeholder] 淡出动画的曲线。

### fadeInDuration

```dart
Duration fadeInDuration
```

[image] 淡入动画的持续时间。

### fadeInCurve

```dart
Curve fadeInCurve
```

[image] 淡入动画的曲线。

### width

```dart
double? width
```

如果非 null，则要求图片具有此宽度。

如果为 null，图片将选择一个能最好地保留其固有宽高比的尺寸。如果占位图片与目标图片的尺寸不一致，可能会导致尺寸突然发生变化。该尺寸还会受到缩放因子的影响。

### color

```dart
Color? color
```

如果非 null，此颜色将使用 [colorBlendMode] 与每个图片像素混合。

该颜色应用于 [image]。

另请参阅：

- [placeholderColor]，应用于 [placeholder] 的颜色。

### colorBlendMode

```dart
BlendMode? colorBlendMode
```

用于将 [color] 与此 [image] 组合。

默认值为 [BlendMode.srcIn]。就该混合模式而言，[color] 是源，此图片是目标。

另请参阅：

- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)，其中包含了每种混合模式效果的示意图。
- [placeholderColorBlendMode]，应用于 [placeholder] 的颜色混合模式。

### placeholderColor

```dart
Color? placeholderColor
```

如果非 null，此颜色将使用 [placeholderColorBlendMode] 与每个占位图片像素混合。

该颜色应用于 [placeholder]。

另请参阅：

- [color]，应用于 [image] 的颜色。

### placeholderColorBlendMode

```dart
BlendMode? placeholderColorBlendMode
```

用于将 [placeholderColor] 与 [placeholder] 图片组合。

默认值为 [BlendMode.srcIn]。就该混合模式而言，[placeholderColor] 是源，此占位图片是目标。

另请参阅：

- [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)，其中包含了每种混合模式效果的示意图。
- [colorBlendMode]，应用于 [image] 的颜色混合模式。

### height

```dart
double? height
```

如果非 null，则要求图片具有此高度。

如果为 null，图片将选择一个能最好地保留其固有宽高比的尺寸。如果占位图片与目标图片的尺寸不一致，可能会导致尺寸突然发生变化。该尺寸还会受到缩放因子的影响。

### fit

```dart
BoxFit? fit
```

如何在布局分配的空间内嵌入图片。

默认值取决于其他字段的设置，详见 [paintImage](https://www.yuque.com/thyname/flutter.painting/paintimage) 处的讨论。

### placeholderFit

```dart
BoxFit? placeholderFit
```

如何在布局分配的空间内嵌入占位图片。

如果未设置值，将回退到 [fit]。

### filterQuality

```dart
FilterQuality filterQuality
```

图片的渲染质量。

{@macro flutter.widgets.image.filterQuality}

### placeholderFilterQuality

```dart
FilterQuality? placeholderFilterQuality
```

占位图片的渲染质量。

{@macro flutter.widgets.image.filterQuality}

### alignment

```dart
AlignmentGeometry alignment
```

如何在图片的边界内对齐图片。

该对齐方式会将图片中给定位置与布局边界中给定位置对齐。例如，[Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 对齐值为 (-1.0, -1.0) 会将图片对齐到其布局边界的左上角，而 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 对齐值为 (1.0, 1.0) 会将图片的右下角与其布局边界的右下角对齐。类似地，对齐值 (0.0, 1.0) 会将图片底部中间与其布局边界底部边缘的中点对齐。

如果 [alignment] 依赖于 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection)（即它是 [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)），则必须存在一个作用域内的环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) widget。

默认为 [Alignment.center]。

另请参阅：

- [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment)，一个包含便捷常量的类，通常用于指定 [AlignmentGeometry](https://www.yuque.com/thyname/flutter.painting/alignmentgeometry)。
- [AlignmentDirectional](https://www.yuque.com/thyname/flutter.painting/alignmentdirectional)，与 [Alignment](https://www.yuque.com/thyname/flutter.painting/alignment) 类似，但用于指定相对于文本方向的对齐方式。

### repeat

```dart
ImageRepeat repeat
```

如何绘制布局边界中未被图片覆盖的部分。

### matchTextDirection

```dart
bool matchTextDirection
```

是否按照 [TextDirection](https://www.yuque.com/thyname/dart.ui/textdirection) 的方向绘制图片。

如果此值为 true，则在 [TextDirection.ltr] 环境下，图片将以其原点位于左上角绘制（图片的“正常”绘制方向）；而在 [TextDirection.rtl] 环境下，图片将在水平方向上以 -1 的缩放因子绘制，使其原点位于右上角。

这种方式偶尔用于从右到左的环境中，对那些为从左到右的语言区域设计的图片进行处理。使用此选项时要小心，不要翻转那些带有完整阴影、文本或其他在翻转后会显得不正确的效果的图片。

如果此值为 true，则必须存在一个作用域内的环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) widget。

### excludeFromSemantics

```dart
bool excludeFromSemantics
```

是否将此图片从语义树中排除。

这对于不向应用提供有意义信息的图片很有用。

### imageSemanticLabel

```dart
String? imageSemanticLabel
```

对 [image] 的语义描述。

用于在 Android 上向 TalkBack、在 iOS 上向 VoiceOver 提供关于 [image] 的描述。

无论是显示 [placeholder] 期间还是图片加载完成后，都会使用此描述。
