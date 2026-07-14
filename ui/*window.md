# Display

```dart
class Display {}
```

一种可配置的显示器，[FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 会渲染在其上。

使用 [FlutterView.display] 获取该视图当前所在的显示器。

### id

```dart
int id
```

该显示器的唯一标识符。

此标识符在 Flutter 框架已知的显示器列表中是唯一的，且并非从任何平台特定的显示器标识符派生而来。

### devicePixelRatio

```dart
double devicePixelRatio
```

该显示器的设备像素比。

此值与附加到该显示器的所有视图对象的 [FlutterView.devicePixelRatio] 值相同。

### size

```dart
Size size
```

该显示器的物理尺寸。

### refreshRate

```dart
double refreshRate
```

该显示器的刷新率，单位为 FPS。

### toString()

```dart
String toString()
```

# FlutterView

```dart
class FlutterView {}
```

用于绘制 Flutter [Scene](https://www.yuque.com/thyname/dart.ui/scene) 的视图。

每个 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 都拥有自己的图层树，每当对其调用 [render] 方法并传入一个 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 时，该图层树就会被重新渲染。

[FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 对象的引用可通过 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 获取。

## 嵌入区域与内边距（Insets and Padding）

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/widgets/window_padding.mp4}

在此示意图中，黑色区域表示应用无法在其上绘制内容的系统 UI。红色区域表示视图内边距（view padding），视图可能无法在该区域内检测手势，也可能不希望在其中绘制内容。灰色区域表示系统键盘，当键盘可见时会覆盖底部的视图内边距。

[viewInsets] 是操作系统为系统 UI（例如键盘）保留的物理像素区域，这些系统 UI 会完全遮挡在该区域内绘制的任何内容。

[viewPadding] 是显示器每一侧可能被系统 UI 部分遮挡、或被显示器上的物理侵入部分（例如电视上的过扫描区域或手机上的"刘海"）部分遮挡的物理像素区域。与嵌入区域不同的是，这些区域中的部分区域可能会在不被遮挡的情况下显示视图绘制的像素，例如手机顶部的刘海只覆盖该区域的一部分。而嵌入区域则会部分或完全遮挡窗口，例如不透明的键盘或半透明的状态栏，它们会覆盖某一区域且没有空隙。

[padding] 属性由 [viewInsets] 和 [viewPadding] 共同计算得出。它允许视图嵌入区域在适当情况下"消耗"视图内边距，例如当手机键盘遮挡底部视图内边距时，会将其"吸收"。

希望相对于视图内边距（而不考虑视图嵌入区域）来定位元素的客户端应使用 [viewPadding] 属性，例如，如果你希望在 iPhone 的"安全区域"中央绘制一个组件，无论键盘是否显示都应如此。

[padding] 适用于希望知道应考虑多少内边距、而不关心当前嵌入状态的客户端，例如判断某个手势是否应被视为滚动手势。此值会根据嵌入区域的当前状态而变化。例如，可见的键盘无论如何都会消耗 [viewPadding] 底部区域内的手势，因此在 [padding] 中无需考虑这一点，该值始终可安全地用于此类计算。

### viewId

```dart
int viewId
```

此视图的不透明 ID。

### platformDispatcher

```dart
PlatformDispatcher platformDispatcher
```

此视图注册并从中获取信息的平台调度器。

### display

```dart
Display get display
```

此视图所绘制的 [Display](https://www.yuque.com/thyname/dart.ui/display)。

### devicePixelRatio

```dart
double get devicePixelRatio
```

此视图所显示屏幕上每个逻辑像素对应的设备像素数。

此数值可能不是 2 的幂，甚至可能不是整数。例如，Nexus 6 的设备像素比为 3.5。

设备像素也称为物理像素。逻辑像素也称为与设备无关的像素或与分辨率无关的像素。

根据定义，物理显示器上大约每厘米有 38 个逻辑像素，或每英寸约 96 个逻辑像素。[devicePixelRatio] 返回的值最终来自硬件本身、设备驱动程序，或操作系统/固件中硬编码的值，可能存在不准确的情况，有时误差幅度较大。

Flutter 框架以逻辑像素为单位运作，因此很少需要直接处理此属性。

当此值发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。在使用 Flutter 框架时，通过 [MediaQuery.of] 获取设备像素比（通过 [MediaQueryData.devicePixelRatio]），而不是直接从 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 获取 [devicePixelRatio]，会在该值变化时自动使依赖它的 Widget 重新构建，而无需监听 [PlatformDispatcher.onMetricsChanged]。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [Display.devicePixelRatio]，报告显示器 DPR 的属性。此处的值与 [display] 上暴露的值相等。

### physicalConstraints

```dart
ViewConstraints get physicalConstraints
```

此视图以物理像素表示的尺寸约束。

视图可以采用满足这些约束的任意 [Size](https://www.yuque.com/thyname/dart.ui/size)。UI 框架通常将这些约束用作其布局算法的输入，以确定视图的合适尺寸。要设置视图的尺寸，所选尺寸必须提供给 [render] 方法，并且必须满足约束条件。

当此值发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。

在启动时，视图的约束在 Dart 代码运行之前可能是未知的。如果在应用程序生命周期的早期观察此值，它可能报告所有维度均为零的约束。

此值不考虑任何屏幕键盘或其他系统 UI。如果约束是紧密的，[padding] 和 [viewInsets] 属性提供了视图各侧可能被系统 UI 遮挡多少的信息。如果约束是松散的，则无法预先获知此信息。

另请参阅：

- [physicalSize]，返回视图当前尺寸。

### physicalSize

```dart
Size get physicalSize
```

平台最后一次报告的矩形的当前尺寸，此视图中渲染的场景将被绘制到该矩形中。

如果视图配置了松散的 [physicalConstraints]，此值可能会有几帧的滞后，因为它仅在提供给 [render] 方法的某一帧所选尺寸被平台处理后才会更新。因此，UI 框架的布局算法应使用 [physicalConstraints] 作为根输入，而不是此值。

当此值发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。在使用 Flutter 框架时，通过 [MediaQuery.of] 获取尺寸（通过 [MediaQueryData.size]），而不是直接从 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 获取 [physicalSize]，会在尺寸变化时自动使依赖该尺寸的 Widget 重新构建，而无需监听 [PlatformDispatcher.onMetricsChanged]。

在启动时，视图的尺寸在 Dart 代码运行之前可能是未知的。如果在应用程序生命周期的早期观察此值，它可能报告 [Size.zero]。

此值不考虑任何屏幕键盘或其他系统 UI。[padding] 和 [viewInsets] 属性提供了视图各侧可能被系统 UI 遮挡多少的信息。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。

### viewInsets

```dart
ViewPadding get viewInsets
```

显示矩形各侧的物理像素数，视图可以在该矩形中进行渲染，但操作系统很可能会在其中放置会完全遮挡任何内容的系统 UI（例如键盘）。

当此属性发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。在使用 Flutter 框架时，通过 [MediaQuery.of] 获取嵌入区域（通过 [MediaQueryData.viewInsets]），而不是直接从 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 获取 [viewInsets]，会在其变化时自动使依赖嵌入区域的 Widget 重新构建，而无需监听 [PlatformDispatcher.onMetricsChanged]。

[viewInsets]、[viewPadding] 与 [padding] 之间的关系在 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的文档中有更详细的说明。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [MediaQuery.of]，实现相同功能的更简单机制。
- [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold)，在 Material Design 应用程序中自动应用视图嵌入区域的组件。

### viewPadding

```dart
ViewPadding get viewPadding
```

显示矩形各侧的物理像素数，视图可以在该矩形中进行渲染，但可能会被系统 UI（例如系统通知区域）部分遮挡，或被显示器上的物理侵入部分（例如电视屏幕上的过扫描区域或手机传感器外壳）部分遮挡。

与 [padding] 不同，此值不会随 [viewInsets] 的变化而变化。例如，在 iPhone X 上，此值不会因软键盘的显示或隐藏而改变，而 [padding] 则会改变。

当此属性发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。在使用 Flutter 框架时，通过 [MediaQuery.of] 获取内边距（通过 [MediaQueryData.viewPadding]），而不是直接从 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 获取 [viewPadding]，会在其变化时自动使依赖该内边距的 Widget 重新构建，而无需监听 [PlatformDispatcher.onMetricsChanged]。

[viewInsets]、[viewPadding] 与 [padding] 之间的关系在 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的文档中有更详细的说明。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [MediaQuery.of]，实现相同功能的更简单机制。
- [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold)，在 Material Design 应用程序中自动应用内边距的组件。

### systemGestureInsets

```dart
ViewPadding get systemGestureInsets
```

显示矩形各侧的物理像素数，视图可以在该矩形中进行渲染，但操作系统会为了系统导航而消费其中的输入手势。

例如，操作系统可能会使用屏幕的垂直边缘，从边缘向内滑动可让用户返回到之前访问过的屏幕历史记录。

当此属性发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [MediaQuery.of]，实现相同功能的更简单机制。

### padding

```dart
ViewPadding get padding
```

显示矩形各侧的物理像素数，视图可以在该矩形中进行渲染，但可能会被系统 UI（例如系统通知区域）部分遮挡，或被显示器上的物理侵入部分（例如电视屏幕上的过扫描区域或手机传感器外壳）部分遮挡。

此值通过 `max(0.0, FlutterView.viewPadding - FlutterView.viewInsets)` 计算得出。这会将增加底部嵌入区域的系统输入法视为消耗了相应数量的底部内边距。例如，在 iPhone X 上，当软键盘未显示时，[FlutterView.padding] 的 [EdgeInsets.bottom] 与 [FlutterView.viewPadding] 的 [EdgeInsets.bottom] 相同（以计入底部软按钮区域），但当软键盘显示时，该值将为 `0.0`。

当此值发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。在使用 Flutter 框架时，通过 [MediaQuery.of] 获取内边距（通过 [MediaQueryData.padding]），而不是直接从 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 获取 [padding]，会在其变化时自动使依赖该内边距的 Widget 重新构建，而无需监听 [PlatformDispatcher.onMetricsChanged]。

[viewInsets]、[viewPadding] 与 [padding] 之间的关系在 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的文档中有更详细的说明。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [MediaQuery.of]，实现相同功能的更简单机制。
- [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold)，在 Material Design 应用程序中自动应用内边距的组件。

### gestureSettings

```dart
GestureSettings get gestureSettings
```

针对此视图上执行的触摸手势的附加配置。

例如，手势设置中可能提供以物理像素定义的触摸容差（touch slop），应优先使用该值而非框架的触摸容差常量。

### displayFeatures

```dart
List<DisplayFeature> get displayFeatures
```

{@template dart.ui.ViewConfiguration.displayFeatures} 显示器上被硬件特性遮挡的区域。

此列表仅在 Android 上有数据。如果设备没有显示特性，此列表为空。

定义 [DisplayFeature.bounds] 的坐标空间跨越当前使用的所有屏幕。这意味着屏幕之间的空间实际上是 Flutter 视图空间的一部分，而显示特性的 [DisplayFeature.bounds] 则是一个被遮挡的区域。可以使用 [DisplayFeature.type] 来判断此显示特性是否遮挡屏幕。例如，[DisplayFeatureType.hinge] 和 [DisplayFeatureType.cutout] 都会遮挡显示区域，而 [DisplayFeatureType.fold] 则是显示器上的折痕。

可折叠的 [DisplayFeature](https://www.yuque.com/thyname/dart.ui/displayfeature)（如 [DisplayFeatureType.hinge] 和 [DisplayFeatureType.fold]）还具有 [DisplayFeature.state]，可用于确定设备所处的姿态。{@endtemplate}

当此值发生变化时，会调用 [PlatformDispatcher.onMetricsChanged]。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。
- [MediaQuery.of]，访问此数据的更简单机制。

### displayCornerRadii

```dart
DisplayCornerRadii? get displayCornerRadii
```

以物理像素表示的显示器圆角半径。

目前仅在 Android API 31+ 上有数据。在较早的 Android 版本、iOS 及其他平台上，此值为 `null`。

### render()

```dart
void render(Scene scene, {Size? size})
```

使用新提供的 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 在 GPU 上更新该视图的渲染内容。

此函数必须在 [PlatformDispatcher.onBeginFrame] 或 [PlatformDispatcher.onDrawFrame] 回调被调用的范围内调用。

如果在单次 [PlatformDispatcher.onBeginFrame]/[PlatformDispatcher.onDrawFrame] 回调序列中第二次调用此函数，或在这些回调的范围之外调用此函数，则该调用将被忽略。

要记录图形操作，首先创建一个 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder)，然后构造一个 [Canvas](https://www.yuque.com/thyname/dart.ui/canvas)，将该 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 传递给其构造函数。发出所有图形操作后，在 [PictureRecorder](https://www.yuque.com/thyname/dart.ui/picturerecorder) 上调用 [PictureRecorder.endRecording] 函数，以获得表示已发出图形操作的最终 [Picture](https://www.yuque.com/thyname/dart.ui/picture)。

接下来，创建一个 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder)，并使用 [SceneBuilder.addPicture] 将该 [Picture](https://www.yuque.com/thyname/dart.ui/picture) 添加到其中。然后可以通过 [SceneBuilder.build] 方法获得一个 [Scene](https://www.yuque.com/thyname/dart.ui/scene) 对象，你可以通过此 [render] 函数将其展示给用户。

如果视图配置了松散的 [physicalConstraints]（即 [ViewConstraints.isTight] 返回 false），则必须提供满足这些约束的 `size`。此方法不会检查所提供的 `size` 是否真正满足约束（这应在更高层进行处理），但不合法的 `size` 可能会导致未定义的渲染行为。如果未提供 `size`，则使用 [physicalSize]。

另请参阅：

- [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)，管理帧调度的 Flutter 框架类。
- [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding)，管理布局和绘制的 Flutter 框架类。

### updateSemantics()

```dart
void updateSemantics(SemanticsUpdate update)
```

更改此 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 保留的语义数据。

在通过此方法发送更新之前，必须先调用 [PlatformDispatcher.setSemanticsTreeEnabled] 并传入 true。

此函数会释放给定的更新，这意味着该语义更新之后将无法再使用。

### toString()

```dart
String toString()
```

# SingletonFlutterWindow

```dart
class SingletonFlutterWindow extends FlutterView {}
```

已弃用。将在 Flutter 未来版本中移除。

弃用此类是为了准备 Flutter 即将推出的对多视图乃至多窗口的支持。

此类已拆分为两个类：[FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 和 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher)。[FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 使应用程序能够访问特定于视图的功能，而 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 则包含适用于所有视图的、特定于平台的功能。

此类支持全局 [window](https://www.yuque.com/thyname/dart.ui/window) 单例（该单例同样已弃用）。有关迁移方案，请参阅 [window](https://www.yuque.com/thyname/dart.ui/window) 的文档。

另请参阅：

- [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，使应用程序能够访问特定于视图的功能。
- [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher)，使应用程序能够访问特定于平台的功能。

### onMetricsChanged

```dart
VoidCallback? get onMetricsChanged
```

每当 [devicePixelRatio]、[physicalSize]、[padding]、[viewInsets]、[PlatformDispatcher.views] 或 [systemGestureInsets] 的值发生变化时都会调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

在使用 Flutter 框架时，[MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 组件暴露了这些指标中的大部分。使用 [MediaQuery.of] 获取它们，可让框架在无需管理 [onMetricsChanged] 回调的情况下自动重建依赖它们的组件。

有关更多信息，请参阅 [PlatformDispatcher.onMetricsChanged]。

### onMetricsChanged

```dart
set onMetricsChanged(VoidCallback? callback)
```

### locale

```dart
Locale get locale
```

设备的系统报告默认语言区域。

{@template dart.ui.window.accessorForwardWarning} 访问此值将返回 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 单例中包含的值，因此建议不要从此处获取该值，而应改为从 `WidgetsBinding.instance.platformDispatcher` 获取（或者，在 `WidgetsBinding` 不可用时，从 [PlatformDispatcher.instance] 获取）。此值转发到 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 的原因是为仅使用单个主窗口的应用程序提供便利。{@endtemplate}

这确立了窗口在可能的情况下应使用的、用于渲染其用户界面的语言和格式约定。

这是用户选择的第一个语言区域，也是用户的主要语言区域（设备 UI 显示所使用的语言区域）。

这等同于 `locales.first`，如果 [locales] 列表尚未设置或为空，则会提供一个非空的空语言区域。

### locales

```dart
List<Locale> get locales
```

设备的完整系统报告支持的语言区域列表。

{@macro dart.ui.window.accessorForwardWarning}

这确立了窗口在可能的情况下应使用的、用于渲染其用户界面的语言和格式约定。

此列表按优先级排序，索引较小的语言区域优先于索引较大的语言区域。第一个元素是主要的 [locale]。

每当此值发生变化时，都会调用 [onLocaleChanged] 回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。

### computePlatformResolvedLocale()

```dart
Locale? computePlatformResolvedLocale(List<Locale> supportedLocales)
```

执行平台原生的语言区域解析。

不同平台可能返回不同的结果。

如果平台解析语言区域失败，则此方法将返回 null。

此方法同步返回，是对平台特定 API 的直接调用，不涉及方法通道（method channel）。

### onLocaleChanged

```dart
VoidCallback? get onLocaleChanged
```

每当 [locale] 值发生变化时都会调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此回调何时被调用的机制。

### onLocaleChanged

```dart
set onLocaleChanged(VoidCallback? callback)
```

### initialLifecycleState

```dart
String get initialLifecycleState
```

Dart isolate 初始化后立即所处的生命周期状态。

{@macro dart.ui.window.accessorForwardWarning}

此属性不会随生命周期的变化而更新。

它用于在启动时，使用任何已缓冲的生命周期状态事件来初始化 [SchedulerBinding.lifecycleState]。

### textScaleFactor

```dart
double get textScaleFactor
```

系统报告的文本缩放比例。

{@macro dart.ui.window.accessorForwardWarning}

这确立了根据用户的平台偏好设置渲染文本时应使用的文本缩放系数。

每当此值发生变化时，都会调用 [onTextScaleFactorChanged] 回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此值变化的机制。

### nativeSpellCheckServiceDefined

```dart
bool get nativeSpellCheckServiceDefined
```

当前平台是否支持拼写检查服务。

{@macro dart.ui.window.accessorForwardWarning}

当启用拼写检查但未指定拼写检查服务时，[EditableTextState](https://www.yuque.com/thyname/flutter.widgets/editabletextstate) 使用此选项来定义其 [SpellCheckConfiguration](https://www.yuque.com/thyname/flutter.widgets/spellcheckconfiguration)。

### supportsShowingSystemContextMenu

```dart
bool get supportsShowingSystemContextMenu
```

当前平台是否支持显示系统上下文菜单。

[AdaptiveTextSelectionToolbar](https://www.yuque.com/thyname/flutter.material/adaptivetextselectiontoolbar) 使用此选项来决定是显示系统上下文菜单，还是回退到 Flutter 默认的上下文菜单。

### brieflyShowPassword

```dart
bool get brieflyShowPassword
```

系统设置中是否启用了在遮蔽文本字段中输入时短暂显示字符的功能。

另请参阅：

- [EditableText.obscureText]，设置为 true 时会隐藏文本字段中的文本。

### alwaysUse24HourFormat

```dart
bool get alwaysUse24HourFormat
```

指示是否应始终以 24 小时制显示时间的设置。

{@macro dart.ui.window.accessorForwardWarning}

[showTimePicker](https://www.yuque.com/thyname/flutter.material/showtimepicker) 使用此选项。

### onTextScaleFactorChanged

```dart
VoidCallback? get onTextScaleFactorChanged
```

每当 [textScaleFactor] 值发生变化时都会调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此回调何时被调用的机制。

### onTextScaleFactorChanged

```dart
set onTextScaleFactorChanged(VoidCallback? callback)
```

### platformBrightness

```dart
Brightness get platformBrightness
```

指示宿主平台当前亮度模式的设置。

{@macro dart.ui.window.accessorForwardWarning}

如果平台没有偏好设置，[platformBrightness] 默认为 [Brightness.light]。

### onPlatformBrightnessChanged

```dart
VoidCallback? get onPlatformBrightnessChanged
```

每当 [platformBrightness] 值发生变化时都会调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此回调何时被调用的机制。

### onPlatformBrightnessChanged

```dart
set onPlatformBrightnessChanged(VoidCallback? callback)
```

### systemFontFamily

```dart
String? get systemFontFamily
```

指示宿主平台系统字体的设置。

{@macro dart.ui.window.accessorForwardWarning}

### onSystemFontFamilyChanged

```dart
VoidCallback? get onSystemFontFamilyChanged
```

每当 [systemFontFamily] 值发生变化时都会调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [WidgetsBindingObserver](https://www.yuque.com/thyname/flutter.widgets/widgetsbindingobserver)，一种在 Widgets 层观察此回调何时被调用的机制。

### onSystemFontFamilyChanged

```dart
set onSystemFontFamilyChanged(VoidCallback? callback)
```

### onBeginFrame

```dart
FrameCallback? get onBeginFrame
```

用于通知窗口现在是使用 [SceneBuilder](https://www.yuque.com/thyname/dart.ui/scenebuilder) API 和 [render] 方法提供场景的合适时机的回调。

{@macro dart.ui.window.accessorForwardWarning}

在可能的情况下，此回调由硬件 VSync 信号驱动。仅当自上次调用此回调以来已调用过 [scheduleFrame] 时，才会调用此回调。

[onDrawFrame] 回调会在 [onBeginFrame] 之后、在耗尽 [onBeginFrame] 处理程序排队的所有微任务（例如任何 [Future](https://www.yuque.com/thyname/dart.async/future) 的完成）之后立即被调用。

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)，管理帧调度的 Flutter 框架类。
- [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding)，管理布局和绘制的 Flutter 框架类。

### onBeginFrame

```dart
set onBeginFrame(FrameCallback? callback)
```

### onDrawFrame

```dart
VoidCallback? get onDrawFrame
```

在 [onBeginFrame] 完成并且微任务队列被耗尽之后，为每一帧调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

可以使用此回调来实现帧渲染的第二阶段，该阶段发生在 [onBeginFrame] 阶段排队的任何延迟工作完成之后。

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)，管理帧调度的 Flutter 框架类。
- [RendererBinding](https://www.yuque.com/thyname/flutter.rendering/rendererbinding)，管理布局和绘制的 Flutter 框架类。

### onDrawFrame

```dart
set onDrawFrame(VoidCallback? callback)
```

### onReportTimings

```dart
TimingsCallback? get onReportTimings
```

用于报告近期光栅化帧的 [FrameTiming](https://www.yuque.com/thyname/dart.ui/frametiming) 的回调。

{@macro dart.ui.window.accessorForwardWarning}

相较于直接使用 [PlatformDispatcher.onReportTimings]，更推荐使用 [SchedulerBinding.addTimingsCallback]，因为 [SchedulerBinding.addTimingsCallback] 允许添加多个回调。

可以使用此回调来查看窗口是否丢帧（通过 [FrameTiming.buildDuration] 和 [FrameTiming.rasterDuration]），或是否存在高延迟（通过 [FrameTiming.totalSpan]）。

与 [Timeline](https://www.yuque.com/thyname/dart.developer/timeline) 不同，此处的计时信息在发布（release）模式下也可用（此外还包括 profile 和 debug 模式）。因此可以使用它来监控应用程序在实际环境中的性能表现。

{@macro dart.ui.TimingsCallback.list}

如果此值为 null，则不会执行额外的工作。如果此值不为 null，Flutter 每 1 秒报告计时信息所花费的时间不到 0.1 毫秒（在 iPhone 6S 上测得）。这 0.1 毫秒约占 16 毫秒（60fps 下的帧预算）的 0.6%，或每秒约 0.01% 的 CPU 使用率。

### onReportTimings

```dart
set onReportTimings(TimingsCallback? callback)
```

### onPointerDataPacket

```dart
PointerDataPacketCallback? get onPointerDataPacket
```

当有指针数据可用时调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

另请参阅：

- [GestureBinding](https://www.yuque.com/thyname/flutter.gestures/gesturebinding)，管理指针事件的 Flutter 框架类。

### onPointerDataPacket

```dart
set onPointerDataPacket(PointerDataPacketCallback? callback)
```

### onKeyData

```dart
KeyDataCallback? get onKeyData
```

当有按键数据可用时调用的回调。

框架会在设置该回调时所处的同一个 zone 中调用此回调。

### onKeyData

```dart
set onKeyData(KeyDataCallback? callback)
```

### defaultRouteName

```dart
String get defaultRouteName
```

应用程序启动时嵌入器（embedder）所请求的路由或路径。

{@macro dart.ui.window.accessorForwardWarning}

如果没有请求特定路由，此值将为字符串 "`/`"。

## Android

在 Android 上，可以通过 [FlutterActivity](/javadoc/io/flutter/embedding/android/FlutterActivity.html) 的 intent builder 上的 [initialRoute](/javadoc/io/flutter/embedding/android/FlutterActivity.NewEngineIntentBuilder.html#initialRoute-java.lang.String-) 方法设置初始路由。

对于独立引擎，请参阅 https://docs.flutter.dev/development/add-to-app/android/add-flutter-screen#initial-route-with-a-cached-engine 。

## iOS

在 iOS 上，可以使用 [`FlutterViewController.setInitialRoute`](/ios-embedder/interface_flutter_view_controller.html#a7f269c2da73312f856d42611cc12a33f) 初始化方法设置初始路由。

对于独立引擎，请参阅 https://docs.flutter.dev/development/add-to-app/ios/add-flutter-screen#route 。

另请参阅：

- [Navigator](https://www.yuque.com/thyname/flutter.widgets/navigator)，处理路由的组件。
- [SystemChannels.navigation]，处理来自嵌入器的后续导航请求。

### scheduleFrame()

```dart
void scheduleFrame()
```

请求在下一个合适的时机调用 [onBeginFrame] 和 [onDrawFrame] 回调。

{@template dart.ui.window.functionForwardWarning} 调用此函数会将调用转发到 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 单例上的同一函数，因此建议不要在此处调用它，而应改为在 `WidgetsBinding.instance.platformDispatcher` 上调用（或者，在 `WidgetsBinding` 不可用时，在 [PlatformDispatcher.instance] 上调用）。此函数转发到 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 的原因是为仅使用单个主窗口的应用程序提供便利。{@endtemplate}

另请参阅：

- [SchedulerBinding](https://www.yuque.com/thyname/flutter.scheduler/schedulerbinding)，管理帧调度的 Flutter 框架类。

### semanticsEnabled

```dart
bool get semanticsEnabled
```

用户是否已请求在窗口的语义内容发生变化时调用 [updateSemantics]。

{@macro dart.ui.window.accessorForwardWarning}

每当此值发生变化时，都会调用 [onSemanticsEnabledChanged] 回调。

### onSemanticsEnabledChanged

```dart
VoidCallback? get onSemanticsEnabledChanged
```

当 [semanticsEnabled] 的值发生变化时调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

### onSemanticsEnabledChanged

```dart
set onSemanticsEnabledChanged(VoidCallback? callback)
```

### frameData

```dart
FrameData get frameData
```

当前帧的 [FrameData](https://www.yuque.com/thyname/dart.ui/framedata) 对象。

### onFrameDataChanged

```dart
VoidCallback? get onFrameDataChanged
```

当窗口更新 [FrameData](https://www.yuque.com/thyname/dart.ui/framedata) 时调用的回调。

### onFrameDataChanged

```dart
set onFrameDataChanged(VoidCallback? callback)
```

### accessibilityFeatures

```dart
AccessibilityFeatures get accessibilityFeatures
```

平台可能启用的附加无障碍功能。

### onAccessibilityFeaturesChanged

```dart
VoidCallback? get onAccessibilityFeaturesChanged
```

当 [accessibilityFeatures] 的值发生变化时调用的回调。

{@macro dart.ui.window.accessorForwardWarning}

框架会在设置该回调时所处的同一个 zone 中调用此回调。

### onAccessibilityFeaturesChanged

```dart
set onAccessibilityFeaturesChanged(VoidCallback? callback)
```

### sendPlatformMessage()

```dart
void sendPlatformMessage(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

向特定平台的插件发送消息。

{@macro dart.ui.window.functionForwardWarning}

`name` 参数决定哪个插件接收该消息。`data` 参数包含消息负载，通常是 UTF-8 编码的 JSON，但也可以是任意数据。如果插件对该消息进行了回复，将会调用 `callback` 并传入响应内容。

框架会在调用此方法时所处的同一个 zone 中调用 [callback]。

### onPlatformMessage

```dart
PlatformMessageCallback? get onPlatformMessage
```

已弃用。请迁移至 [ChannelBuffers.setListener]。

每当此窗口收到来自特定平台插件的消息时调用。

{@macro dart.ui.window.accessorForwardWarning}

`name` 参数决定哪个插件发送了该消息。`data` 参数是消息负载，通常是 UTF-8 编码的 JSON，但也可以是任意数据。

消息处理程序必须调用 `callback` 参数中给出的函数。如果处理程序不需要响应，则应向回调传入 null。

框架会在设置该回调时所处的同一个 zone 中调用此回调。

### onPlatformMessage

```dart
set onPlatformMessage(PlatformMessageCallback? callback)
```

### setIsolateDebugName()

```dart
void setIsolateDebugName(String name)
```

设置与此平台调度器的根 isolate 关联的调试名称。

{@macro dart.ui.window.accessorForwardWarning}

通常，调试名称是根据 Dart 端口、入口点和源文件自动生成的。例如：`main.dart$main-1234`。

可以将此方法与 flutter 工具的 `--isolate-filter` 参数结合使用，以调试特定的根 isolate。例如：`flutter attach --isolate-filter=[name]`。请注意，这不会重命名该 isolate 的任何子 isolate。

# AccessibilityFeatures

```dart
class AccessibilityFeatures {}
```

平台可能启用的附加无障碍功能。

无法从 Flutter 启用这些设置，相反，平台会使用它们来指示已启用了额外的无障碍功能。

### accessibleNavigation

```dart
bool get accessibleNavigation
```

是否有正在运行的无障碍服务正在改变设备的交互模式。

例如，Android 上的 TalkBack 和 iOS 上的 VoiceOver 会启用此标志。

### invertColors

```dart
bool get invertColors
```

平台是否正在反转应用程序的颜色。

### disableAnimations

```dart
bool get disableAnimations
```

平台是否请求禁用或简化动画。

### boldText

```dart
bool get boldText
```

平台是否请求以粗体字重渲染文本。

仅在 iOS 和 Android API 31+ 上支持。

### reduceMotion

```dart
bool get reduceMotion
```

平台是否请求简化某些动画并移除视差效果。

仅在 iOS 上支持。

### highContrast

```dart
bool get highContrast
```

平台是否请求以更深的颜色渲染 UI。

仅在 iOS 和 Android API 34+ 上支持。

### onOffSwitchLabels

```dart
bool get onOffSwitchLabels
```

平台是否请求在开关内部显示开/关标签。

仅在 iOS 上支持。

### supportsAnnounce

```dart
bool get supportsAnnounce
```

平台是否支持无障碍播报 API，即 [SemanticsService.sendAnnouncement]。

某些平台不支持或不鼓励使用播报功能。在这些平台上使用 [SemanticsService.sendAnnouncement] 可能会被忽略。可考虑使用其他方式向用户传达信息。例如，Android 不鼓励直接使用消息播报，而是鼓励使用其他语义属性（例如 [SemanticsProperties.liveRegion]）向用户传达信息。

在播报功能已弃用或底层平台不支持的平台上返回 `false`。

在通常支持此类播报且不加以限制的平台（iOS、web 等）上返回 `true`。

### autoPlayAnimatedImages

```dart
bool get autoPlayAnimatedImages
```

平台是否允许自动播放动图。

仅在 iOS 上支持。

在其他平台上始终返回 `true`。

### autoPlayVideos

```dart
bool get autoPlayVideos
```

平台是否允许自动播放视频。

仅在 iOS 上支持。

在其他平台上始终返回 `true`。

### deterministicCursor

```dart
bool get deterministicCursor
```

平台是否请求在可编辑文本字段中显示确定性（不闪烁）的光标。

仅在 iOS 上支持。

# Brightness

```dart
enum Brightness {}
```

描述主题或调色板的对比度。

该颜色较深，需要浅色文本才能达到可读的对比度。

例如，该颜色可能是深灰色，需要白色文本。

该颜色较浅，需要深色文本才能达到可读的对比度。

例如，该颜色可能是亮白色，需要黑色文本。

# window

```dart
SingletonFlutterWindow window
```

已弃用。将在 Flutter 未来版本中移除。

弃用此全局属性是为了准备 Flutter 即将推出的对多视图和多窗口的支持。

它代表只有一个视图的应用程序（例如为单显示器移动设备设计的应用程序）的主视图。如果嵌入器支持多个视图，它将指向创建的第一个视图，该视图被假定为主视图。如果尚未创建任何视图，或者第一个视图已被再次移除，则会抛出异常。

以下选项可用于迁移依赖访问此已弃用属性的代码：

如果有可用的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext)，可考虑通过 [View.of] 查找与该上下文关联的当前 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。它提供了与此已弃用属性相同的功能。不过，特定于平台的功能已移至 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher)，可通过 [View.of] 返回的视图的 [FlutterView.platformDispatcher] 访问。使用带有 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [View.of] 是从此已弃用的 [window](https://www.yuque.com/thyname/dart.ui/window) 属性迁移的首选方案。

如果没有可用于查找 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的上下文，可以直接使用 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 来获取特定于平台的功能。它还在 [PlatformDispatcher.views] 中维护了所有可用 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 的列表，以便在没有上下文的情况下访问特定于视图的功能。如果可能，请考虑通过 binding（例如 `WidgetsBinding.instance.platformDispatcher`）访问 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher)，而不是使用静态单例 [PlatformDispatcher.instance]。有关为何推荐此方式的更多信息，请参阅 [PlatformDispatcher.instance]。

另请参阅：

- [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，使应用程序能够访问特定于视图的功能。
- [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher)，使应用程序能够访问特定于平台的功能。
- [PlatformDispatcher.views]，所有可用视图的列表。

# FrameData

```dart
class FrameData {}
```

每个 Flutter 帧上可用的附加数据。

另请参阅：

- [Window.frameData] 和 [PlatformDispatcher.frameData]，暴露当前帧帧数据的属性。
- [PlatformDispatcher.onFrameDataChanged]，当窗口的帧数据发生变化时通知监听器的回调。

### frameNumber

```dart
int frameNumber
```

当前帧的编号。

此数字单调递增，但不一定从某个特定值开始。

如果未提供，默认为 -1。

# GestureSettings

```dart
class GestureSettings {}
```

手势行为的平台特定配置，例如触摸容差（touch slop）。

这些设置通过 [FlutterView.gestureSettings] 提供给每个视图，在配置手势行为时应优先使用它们，而非框架常量。

`null` 字段表示平台或视图没有偏好设置，应改用后备（fallback）常量。

### GestureSettings()

```dart
GestureSettings({double? physicalTouchSlop, double? physicalDoubleTapSlop})
```

创建一个新的 [GestureSettings](https://www.yuque.com/thyname/dart.ui/gesturesettings) 值。

可考虑在现有的 settings 对象上使用 [GestureSettings.copyWith]，以确保正确设置新添加的字段。

### physicalTouchSlop

```dart
double? physicalTouchSlop
```

指针在被视为有意移动之前允许漂移的物理像素数。

如果为 `null`，则应改用框架的默认触摸容差配置。

### physicalDoubleTapSlop

```dart
double? physicalDoubleTapSlop
```

双击的第一次和第二次点击之间允许漂移多远、仍被识别为双击的物理像素数。

如果为 `null`，则应改用框架的默认双击容差配置。

### copyWith()

```dart
GestureSettings copyWith({double? physicalTouchSlop, double? physicalDoubleTapSlop})
```

基于现有值创建一个新的 [GestureSettings](https://www.yuque.com/thyname/dart.ui/gesturesettings) 对象，覆盖所有提供的字段。
