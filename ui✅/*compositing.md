# Scene

```dart
abstract class Scene {}
```

一个表示已合成场景的不透明对象。

要创建 Scene 对象，请使用 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder)。

Scene 对象可以使用 [FlutterView.render] 方法显示在屏幕上。

### toImageSync()

```dart
Image toImageSync(int width, int height)
```

同步创建此场景的图像句柄。

{@macro dart.ui.painting.Picture.toImageSync}

### toImage()

```dart
Future<Image> toImage(int width, int height)
```

创建当前场景状态的光栅图像表示。

这是一个在后台线程执行的慢操作。

调用者在使用完 [Image](https://www.yuque.com/thyname/dart.ui/image) 后必须将其释放（dispose）。如果结果会与其他方法或类共享，应使用 [Image.clone]，并且必须释放所创建的每个句柄。

### dispose()

```dart
void dispose()
```

释放此场景所使用的资源。

调用此函数后，该场景将无法再被使用。

此方法不能是叶子调用（leaf call），因为该原生函数会调用 Dart API（Dart_SetNativeInstanceField）。

# TransformEngineLayer

```dart
class TransformEngineLayer extends _EngineLayerWrapper {}
```

指向变换引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushTransform] 创建。

{@template dart.ui.sceneBuilder.oldLayerCompatibility} [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 方法中的 `oldLayer` 参数只接受由引擎创建的对象。如果传入此类的自定义实现，[SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 将抛出 [AssertionError](https://www.yuque.com/thyname/dart.core/assertionerror)。{@endtemplate}

# OffsetEngineLayer

```dart
class OffsetEngineLayer extends _EngineLayerWrapper {}
```

指向偏移引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushOffset] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ClipRectEngineLayer

```dart
class ClipRectEngineLayer extends _EngineLayerWrapper {}
```

指向矩形裁剪引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushClipRect] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ClipRRectEngineLayer

```dart
class ClipRRectEngineLayer extends _EngineLayerWrapper {}
```

指向圆角矩形裁剪引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushClipRRect] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ClipRSuperellipseEngineLayer

```dart
class ClipRSuperellipseEngineLayer extends _EngineLayerWrapper {}
```

指向圆角超椭圆裁剪引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushClipRSuperellipse] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ClipPathEngineLayer

```dart
class ClipPathEngineLayer extends _EngineLayerWrapper {}
```

指向路径裁剪引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushClipPath] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# OpacityEngineLayer

```dart
class OpacityEngineLayer extends _EngineLayerWrapper {}
```

指向不透明度引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushOpacity] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ColorFilterEngineLayer

```dart
class ColorFilterEngineLayer extends _EngineLayerWrapper {}
```

指向颜色滤镜引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushColorFilter] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ImageFilterEngineLayer

```dart
class ImageFilterEngineLayer extends _EngineLayerWrapper {}
```

指向图像滤镜引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushImageFilter] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# BackdropFilterEngineLayer

```dart
class BackdropFilterEngineLayer extends _EngineLayerWrapper {}
```

指向背景滤镜引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushBackdropFilter] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# ShaderMaskEngineLayer

```dart
class ShaderMaskEngineLayer extends _EngineLayerWrapper {}
```

指向着色器遮罩引擎层的不透明句柄。

此类的实例由 [SceneBuilder.pushShaderMask] 创建。

{@macro dart.ui.sceneBuilder.oldLayerCompatibility}

# SceneBuilder

```dart
abstract class SceneBuilder {}
```

构建包含给定视觉内容的 [Scene](https://www.yuque.com/thyname/dart.ui/scene)。

随后可以使用 [FlutterView.render] 渲染 [Scene](https://www.yuque.com/thyname/dart.ui/scene)。

要将图形操作绘制到 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 上，首先使用 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 和 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas) 创建一个 [Picture](https://www.yuque.com/thyname/dart.ui/picture)，然后使用 [addPicture] 将其添加到场景中。

## 与 Flutter 框架配合使用

Flutter 框架的 [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding) 提供了一个用于创建 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 对象的钩子（[RendererBinding.createSceneBuilder]），使测试能够接入场景创建逻辑。在 Flutter 框架的上下文中创建 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) 时，建议调用 [RendererBinding.createSceneBuilder]，而不是直接调用 [SceneBuilder.new] 构造函数。

在不使用 Flutter 框架绑定、直接使用 `dart:ui` API 的情况下（如不使用 `flutter_test` 框架等），此建议不适用。

### SceneBuilder()

```dart
SceneBuilder()
```

### pushTransform()

```dart
TransformEngineLayer pushTransform(Float64List matrix4, {TransformEngineLayer? oldLayer})
```

将一个变换操作压入操作栈。

在光栅化之前，对象会先按照给定的矩阵进行变换。

{@template dart.ui.sceneBuilder.oldLayer} 如果 `oldLayer` 不为空，引擎将尝试在渲染新图层时复用为旧图层分配的资源。这纯粹是一种优化，不会影响渲染的正确性。{@endtemplate}

{@template dart.ui.sceneBuilder.oldLayerVsRetained} 将图层传递给 [addRetained]，或作为 push 方法的 `oldLayer` 参数传递，都算作一次*使用*。一个图层在一个场景中最多只能被使用一次。例如，它不能同时传递给两个 push 方法，或同时传递给一个 push 方法和 `addRetained`。

当一个图层被传递给 [addRetained] 时，该保留图层子树下的所有图层也都被视为在此场景中被使用。相同的单次使用限制也适用于其子孙图层。

当一个图层作为 `oldLayer` 参数传递给某个 push 方法时，它将不能在后续帧中再次使用。如果希望继续复用与该图层关联的资源，请存储 push 方法返回的图层对象，并在下一帧中使用该对象而非原始对象。{@endtemplate}

关于操作栈的详细信息，请参见 [pop]。

### pushOffset()

```dart
OffsetEngineLayer pushOffset(double dx, double dy, {OffsetEngineLayer? oldLayer})
```

将一个偏移操作压入操作栈。

这等效于使用一个仅包含平移的矩阵调用 [pushTransform]。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pushClipRect()

```dart
ClipRectEngineLayer pushClipRect(Rect rect, {Clip clipBehavior = Clip.antiAlias, ClipRectEngineLayer? oldLayer})
```

将一个矩形裁剪操作压入操作栈。

给定矩形之外的光栅化内容将被丢弃。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]；关于不同的裁剪模式，请参见 [Clip](https://www.yuque.com/thyname/dart.ui/clip)。默认情况下，裁剪会进行抗锯齿处理（clip = [Clip.antiAlias]）。

### pushClipRRect()

```dart
ClipRRectEngineLayer pushClipRRect(RRect rrect, {Clip clipBehavior = Clip.antiAlias, ClipRRectEngineLayer? oldLayer})
```

将一个圆角矩形裁剪操作压入操作栈。

给定圆角矩形之外的光栅化内容将被丢弃。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]；关于不同的裁剪模式，请参见 [Clip](https://www.yuque.com/thyname/dart.ui/clip)。默认情况下，裁剪会进行抗锯齿处理（clip = [Clip.antiAlias]）。

### pushClipRSuperellipse()

```dart
ClipRSuperellipseEngineLayer pushClipRSuperellipse(RSuperellipse rsuperellipse, {Clip clipBehavior = Clip.antiAlias, ClipRSuperellipseEngineLayer? oldLayer})
```

将一个圆角超椭圆裁剪操作压入操作栈。

给定圆角超椭圆之外的光栅化内容将被丢弃。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]；关于不同的裁剪模式，请参见 [Clip](https://www.yuque.com/thyname/dart.ui/clip)。默认情况下，裁剪会进行抗锯齿处理（clip = [Clip.antiAlias]）。

### pushClipPath()

```dart
ClipPathEngineLayer pushClipPath(Path path, {Clip clipBehavior = Clip.antiAlias, ClipPathEngineLayer? oldLayer})
```

将一个路径裁剪操作压入操作栈。

给定路径之外的光栅化内容将被丢弃。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。关于不同的裁剪模式，请参见 [Clip](https://www.yuque.com/thyname/dart.ui/clip)。默认情况下，裁剪会进行抗锯齿处理（clip = [Clip.antiAlias]）。

### pushOpacity()

```dart
OpacityEngineLayer pushOpacity(int alpha, {Offset? offset = Offset.zero, OpacityEngineLayer? oldLayer})
```

将一个不透明度操作压入操作栈。

给定的 alpha 值会与对象光栅化结果的 alpha 值混合。alpha 值为 0 会使对象完全不可见。alpha 值为 255 则不产生任何效果（即对象保持当前的不透明度）。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pushColorFilter()

```dart
ColorFilterEngineLayer pushColorFilter(ColorFilter filter, {ColorFilterEngineLayer? oldLayer})
```

将一个颜色滤镜操作压入操作栈。

给定颜色会使用给定的混合模式应用到对象的光栅化结果上。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pushImageFilter()

```dart
ImageFilterEngineLayer pushImageFilter(ImageFilter filter, {Offset offset = Offset.zero, ImageFilterEngineLayer? oldLayer})
```

将一个图像滤镜操作压入操作栈。

在将子项的光栅化结果合成到场景之前，会先对其应用给定的滤镜。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pushBackdropFilter()

```dart
BackdropFilterEngineLayer pushBackdropFilter(ImageFilter filter, {BlendMode blendMode = BlendMode.srcOver, BackdropFilterEngineLayer? oldLayer, int? backdropId})
```

将一个背景滤镜操作压入操作栈。

在对子图层进行光栅化之前，会将给定的滤镜应用到场景中当前的内容上（最远追溯到最近的一次 save layer），并使用指定的 [blendMode] 将结果渲染回场景。

如果提供了 [backdropId] 且不为空，则该值将被视为该背景的唯一标识符。在光栅化过程中，当处理第一个具有给定 id 的背景滤镜时，背景的状态会被记录并缓存。所有具有相同标识符的后续背景滤镜都会将其滤镜应用于该缓存的背景。正确使用 backdrop id 能够显著提升具有多个背景滤镜的应用程序的性能。例如，一个在列表视图的每一项中都使用背景模糊滤镜的应用程序，应将所有滤镜设置为相同的 backdrop id。

如果重叠的背景滤镜使用相同的 backdropId，那么每个滤镜都会应用到重叠部分组件渲染之前的背景上。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pushShaderMask()

```dart
ShaderMaskEngineLayer pushShaderMask(Shader shader, Rect maskRect, BlendMode blendMode, {ShaderMaskEngineLayer? oldLayer, FilterQuality filterQuality = FilterQuality.low})
```

将一个着色器遮罩操作压入操作栈。

给定的着色器会使用给定的混合模式，应用到给定矩形范围内对象的光栅化结果上。

{@macro dart.ui.sceneBuilder.oldLayer}

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

关于操作栈的详细信息，请参见 [pop]。

### pop()

```dart
void pop()
```

结束最近一次压入的操作的效果。

场景构建器内部维护着一个操作栈。栈中的每个操作都会应用于添加到场景中的每个对象。调用此函数会从栈中移除最近添加的操作。

### addRetained()

```dart
void addRetained(EngineLayer retainedLayer)
```

添加来自先前帧的保留引擎层子树。

保留图层子树中的所有引擎层都会自动追加到当前的引擎层树中。

因此，在实现 Flutter 框架渲染层中定义的 [Layer](https://www.yuque.com/thyname/flutter.rendering/layer) 概念的子类时，一旦调用了此方法，就无需再为其子图层调用 [Layer.addToScene]。

{@macro dart.ui.sceneBuilder.oldLayerVsRetained}

### addPerformanceOverlay()

```dart
void addPerformanceOverlay(int enabledOptions, Rect bounds)
```

向场景中添加一个显示性能统计信息的对象。

在开发过程中用于评估应用程序的性能。enabledOptions 控制显示哪些统计信息，bounds 控制统计信息显示的位置。

enabledOptions 是一个位域，定义了以下比特位：

- 0x01：displayRasterizerStatistics —— 显示光栅线程帧耗时
- 0x02：visualizeRasterizerStatistics —— 以图表形式显示光栅线程帧耗时
- 0x04：displayEngineStatistics —— 显示 UI 线程帧耗时
- 0x08：visualizeEngineStatistics —— 以图表形式显示 UI 线程帧耗时 将 enabledOptions 设置为 0x0F 可启用当前定义的所有功能。

“UI 线程”是指执行主 Dart isolate（即可以调用 [FlutterView.render] 的 isolate）全部代码的线程。UI 线程帧耗时是指执行 [PlatformDispatcher.onBeginFrame] 回调所花费的总时间。“光栅线程”是指（在 CPU 上运行的）线程，它随后处理 Dart 代码提供的 [Scene](https://www.yuque.com/thyname/dart.ui/scene)，将其转换为 GPU 命令并发送给 GPU。

另请参见渲染库中的 [PerformanceOverlayOption](https://www.yuque.com/thyname/flutter.rendering/performanceoverlayoption) 枚举，以了解更多详情。

### addPicture()

```dart
void addPicture(Offset offset, Picture picture, {bool isComplexHint = false, bool willChangeHint = false})
```

向场景中添加一个 [Picture](https://www.yuque.com/thyname/dart.ui/picture)。

该图片会在给定的 `offset` 处进行光栅化。

如果某个图片在后续帧中被复用，其渲染结果*可能*会被缓存，以降低绘制该图片的开销。图片是否被缓存取决于后端实现。在考虑是否缓存时，是否缓存的选择是基于该图片被绘制的频率以及绘制该图片的开销所做出的启发式判断。要禁用此缓存，请将 `willChangeHint` 设置为 true。要强制进行缓存（在支持缓存的后端中），请将 `isComplexHint` 设置为 true。当两者都被设置时，以 `willChangeHint` 为准。

通常来说，设置这些提示参数用处不大。只有当图片已经被渲染三次以上时，支持图片缓存的后端才会对其进行缓存；因此，为了避免缓存每帧都在变化的动画图片而将 `willChangeHint` 设置为 true 实际上是多余的，因为该图片本来就不会被缓存。类似地，支持图片缓存的后端在决定是否缓存时相对激进，以至于任何足够复杂、值得缓存的图像，即使不设置 `isComplexHint` 为 true，基本上也已经在被缓存了。

### addTexture()

```dart
void addTexture(int textureId, {Offset offset = Offset.zero, double width = 0.0, double height = 0.0, bool freeze = false, FilterQuality filterQuality = FilterQuality.low})
```

向场景中添加一个后端纹理（backend texture）。

该纹理会被缩放到给定的大小，并在给定的偏移处进行光栅化。

如果 `freeze` 为 true，添加到场景中的纹理将不会随新的帧更新。`freeze` 用于调整已嵌入的 Android view 的大小：在调整 Android view 大小时，有一小段时间框架无法判断最新的纹理帧使用的是旧尺寸还是新尺寸，为了解决这个问题，框架会在调整 Android view 大小之前“冻结”纹理，并在确定新尺寸的帧已经就绪后再“解冻”它。

### addPlatformView()

```dart
void addPlatformView(int viewId, {Offset offset = Offset.zero, double width = 0.0, double height = 0.0})
```

向场景中添加一个平台视图（platform view）（例如 iOS 的 UIView）。

在 iOS 上，该图层会将当前的输出表面（surface）拆分为两个表面，一个用于该平台视图之前的场景节点，另一个用于其之后的场景节点。

## 性能影响

添加额外的表面会使 Flutter 直接用于输出缓冲区的显存占用量翻倍。Quartz 可能会为合成 Flutter 表面和平台视图分配额外的缓冲区。

当场景中存在平台视图时，Quartz 需要合成两个 Flutter 表面以及嵌入的 UIView。除此之外，在 iOS 9 以上的版本中，Flutter 帧会与 UIView 帧同步，这会带来额外的性能开销。

`offset` 参数在 iOS 和 Android 上不会被使用。

### build()

```dart
Scene build()
```

完成场景的构建。

返回一个包含已添加到此场景构建器中的对象的 [Scene](https://www.yuque.com/thyname/dart.ui/scene)。随后可以使用 [FlutterView.render] 将该 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 显示在屏幕上。

调用此函数后，场景构建器对象将失效，无法再被使用。
