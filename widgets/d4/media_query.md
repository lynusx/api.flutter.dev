@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/semantics.dart'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart'; @docImport 'display_feature_sub_screen.dart'; @docImport 'overlay.dart'; @docImport 'safe_area.dart'; @docImport 'system_context_menu.dart'; @docImport 'view.dart';

# Orientation

```dart
enum Orientation {}
```

表示纵向还是横向。

高度大于宽度。

宽度大于高度。

# MediaQueryData

```dart
class MediaQueryData {}
```

关于媒体（例如窗口）的一部分信息。

例如，[MediaQueryData.size] 属性包含当前窗口的宽度和高度。

要获取 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中的单个属性，建议使用 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的特定属性函数，而非获取整个 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象后再访问其成员。{@macro flutter.widgets.media_query.MediaQuery.useSpecific}

要获取给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的完整当前 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，请使用 [MediaQuery.of] 函数。如果你打算使用 [copyWith] 来替换 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，并使用更新后的属性生成新对象，这会很有用。

## Insets and Padding（内嵌区域与内边距）

![padding、viewInsets 和 viewPadding 之间相互关系的示意图](https://flutter.github.io/assets-for-api-docs/assets/widgets/media_query.png)

此示意图展示了 [padding] 与 [viewPadding] 及 [viewInsets] 之间的关系，图中展示的是最简单的配置情形，即二者之差。当 viewInsets 超过 viewPadding 时（例如下方显示软键盘时），padding 会变为零而非负值。因此，padding 的计算方式为 `max(0.0, viewPadding - viewInsets)`。

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/widgets/window_padding.mp4}

在此示意图中，黑色区域表示应用程序无法在其上绘制的系统 UI。红色区域表示应用程序可能无法检测手势、也可能不想在其上绘制的视图内边距（view padding）。灰色区域表示系统键盘，当键盘可见时会遮挡底部的视图内边距。

MediaQueryData 包含三个 [EdgeInsets](https://www.yuque.com/thyname/flutter.painting/edgeinsets) 值：[padding]、[viewPadding] 和 [viewInsets]。这些值反映了设备的配置情况，会被那些需要在这些内嵌区域范围内定位内容的 Widget 使用，也可以选择性地被这些 Widget 消耗。padding 值定义了可能无法完全可见的区域，例如 iPhone X 上的显示屏"刘海"。viewInsets 值定义了完全不可见的区域，通常是因为它们被设备键盘遮挡。与 viewInsets 类似，viewPadding 不区分可能被同一物理屏幕区域遮挡的内嵌区域。例如，使用 viewPadding 属性时，无论是否显示键盘，padding 都会遵从 iPhone 的"安全区域（safe area）"。

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

viewInsets 和 viewPadding 是相互独立的值，它们均从 MediaQuery Widget 边界的边缘开始测量。二者共同决定了 [padding] 属性。由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的顶层 MediaQuery 的边界与包含该应用的窗口边界相同。

其布局会消耗 [viewInsets]、[viewPadding] 或 [padding] 所定义空间的 Widget，应将其子级包装在次级 MediaQuery Widget 中，并将这些属性按相同数量减小。[removePadding]、[removeViewPadding] 和 [removeViewInsets] 方法可用于实现这一点。

另请参阅：

- [Scaffold](https://www.yuque.com/thyname/flutter.material/scaffold)、[SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea)、[CupertinoTabScaffold](https://www.yuque.com/thyname/flutter.cupertino/cupertinotabscaffold) 和 [CupertinoPageScaffold](https://www.yuque.com/thyname/flutter.cupertino/cupertinopagescaffold)，它们均会参考 [padding]、[viewPadding] 和 [viewInsets]。

### MediaQueryData()

```dart
MediaQueryData({Size size = Size.zero, double devicePixelRatio = 1.0, double textScaleFactor = 1.0, TextScaler textScaler = _kUnspecifiedTextScaler, Brightness platformBrightness = Brightness.light, EdgeInsets padding = EdgeInsets.zero, EdgeInsets viewInsets = EdgeInsets.zero, EdgeInsets systemGestureInsets = EdgeInsets.zero, EdgeInsets viewPadding = EdgeInsets.zero, bool alwaysUse24HourFormat = false, bool accessibleNavigation = false, bool invertColors = false, bool highContrast = false, bool onOffSwitchLabels = false, bool disableAnimations = false, bool boldText = false, bool supportsAnnounce = false, NavigationMode navigationMode = NavigationMode.traditional, DeviceGestureSettings gestureSettings = const DeviceGestureSettings(touchSlop: kTouchSlop), List<ui.DisplayFeature> displayFeatures = const <ui.DisplayFeature>[], bool supportsShowingSystemContextMenu = false, double? lineHeightScaleFactorOverride, double? letterSpacingOverride, double? wordSpacingOverride, double? paragraphSpacingOverride, BorderRadius? displayCornerRadii})
```

使用显式值创建媒体查询数据。

在典型的应用程序中，很少需要直接调用此构造函数。建议使用 [MediaQueryData.fromView] 基于 [dart:ui.FlutterView] 创建数据，或使用 [MediaQueryData.copyWith] 基于某个基础 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 创建具有更新属性的新副本。

### MediaQueryData.fromWindow()

```dart
MediaQueryData.fromWindow(ui.FlutterView window)
```

已弃用。请改用 [MediaQueryData.fromView]。

此构造函数基于单一窗口假设运行。为准备支持 Flutter 即将推出的多窗口支持，该构造函数已被弃用。

### MediaQueryData.fromView()

```dart
MediaQueryData.fromView(ui.FlutterView view, {MediaQueryData? platformData})
```

基于给定的 `view` 为 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 创建数据。

如果提供了 `platformData`，则会使用它来填充新创建的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中与平台相关的部分。如果 `platformData` 为空，则会查询 `view` 的 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 来构建平台特定的数据。

直接在 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 上暴露的数据被视为视图特定数据。仅通过 [FlutterView.platformDispatcher] 属性暴露的数据被视为平台特定数据。

此方法的调用者应确保同时注册相应通知，以便在构造 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 所用的任何数据发生变化时能够更新它。需要考虑的通知包括：

- [WidgetsBindingObserver.didChangeMetrics] 或 [dart:ui.PlatformDispatcher.onMetricsChanged]，
- [WidgetsBindingObserver.didChangeAccessibilityFeatures] 或 [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged]，
- [WidgetsBindingObserver.didChangeTextScaleFactor] 或 [dart:ui.PlatformDispatcher.onTextScaleFactorChanged]，
- [WidgetsBindingObserver.didChangePlatformBrightness] 或 [dart:ui.PlatformDispatcher.onPlatformBrightnessChanged]。

只有在未提供 `platformData` 时，后三种通知才有意义。如果提供了 `platformData`，调用者应确保在其发生变化时再次调用此方法，以保持构造出的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 是最新的。

通常，[MediaQuery.of] 及其相关的 "...Of" 方法是从 Widget 中获取 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 的合适方式。此 `fromView` 构造函数主要供框架自身实现使用。

另请参阅：

- [MediaQuery.fromView]，它基于提供的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 构造 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，使其可供后代 Widget 使用，并设置相应的通知监听器以保持数据更新。

### size

```dart
Size size
```

媒体的尺寸，以逻辑像素为单位（例如屏幕的尺寸）。

逻辑像素在不同设备上的视觉尺寸大致相同。物理像素则是设备上实际硬件像素的尺寸。每个逻辑像素对应的物理像素数量由 [devicePixelRatio] 描述。

建议优先使用 [MediaQuery.sizeOf] 而非 [MediaQuery.of]`.size` 来获取尺寸，因为前者只会在 [size] 发生变化时通知，而后者会在所有 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 发生变化时通知。

对于在 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 中绘制的 Widget，不要假定 [Overlay](https://www.yuque.com/thyname/flutter.widgets/overlay) 的尺寸就是 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的尺寸。嵌套的 overlay 可以具有不同的尺寸。

## Troubleshooting（问题排查）

缓存 `MediaQuery.sizeOf(context)` 返回的尺寸并在之后使用被认为是不良实践。这会导致应用程序无法响应，并可能引发意外行为。

例如，在启动期间，尤其是在 release 模式下，首次返回的尺寸可能是 [Size.zero]。当原生平台报告实际分辨率后，该尺寸会被更新。使用 [MediaQuery.sizeOf] 可以确保当尺寸发生变化时，任何依赖该尺寸的 Widget 都会自动重建。

请参阅关于[创建响应式和自适应应用](https://docs.flutter.dev/ui/adaptive-responsive)的文章以作入门介绍。

另请参阅：

- [FlutterView.physicalSize]，以物理像素为单位返回视图的尺寸。
- [FlutterView.display]，返回显示屏的尺寸、刷新率等报告信息。
- [MediaQuery.sizeOf]，用于查找并依赖给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 所定义尺寸的方法。

### devicePixelRatio

```dart
double devicePixelRatio
```

对应外围 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 每个逻辑像素的设备像素数量。此数值可能不是 2 的幂，甚至可能不是整数。例如，Nexus 6 的设备像素比为 3.5。

此属性通常仅用作参考信息。覆盖此属性并不会重新缩放应用程序，因为 Flutter 框架及其渲染管线通常不会读取此值。

### textScaleFactor

```dart
double get textScaleFactor
```

已弃用。将在未来版本的 Flutter 中移除。请改用 [textScaler]。

每个逻辑像素对应的字体像素数量。

例如，如果文本缩放因子为 1.5，则文本将比指定字号大 50%。

另请参阅：

- [MediaQuery.textScaleFactorOf]，用于查找并依赖给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 所定义 textScaleFactor 的方法。

### textScaler

```dart
TextScaler get textScaler
```

用于布局文本内容的字体缩放策略。

如果此 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 是通过 [MediaQueryData.fromView] 构造函数创建的，则此属性反映平台首选的文本缩放策略，并可能随着用户在操作系统无障碍设置中更改缩放因子而变化。

另请参阅：

- [MediaQuery.textScalerOf]，用于查找并依赖给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 所定义 [textScaler] 的方法。
- [TextPainter](https://www.yuque.com/thyname/flutter.painting/textpainter)，用于布局和绘制文本的类。

### platformBrightness

```dart
Brightness platformBrightness
```

主机平台当前的亮度模式。

例如，从 Android Pie 开始，省电模式会要求所有应用以"深色模式"渲染。

并非所有平台都必然支持亮度模式的概念。不支持的平台会在此属性中报告 [Brightness.light]。

另请参阅：

- [MediaQuery.platformBrightnessOf]，用于查找并依赖给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 所定义 platformBrightness 的方法。

### viewInsets

```dart
EdgeInsets viewInsets
```

显示屏上被系统 UI 完全遮挡的部分，通常是被设备键盘遮挡的部分。

当移动设备的键盘可见时，`viewInsets.bottom` 对应键盘的顶部。

此值独立于 [padding] 和 [viewPadding]。viewPadding 从 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 边界的边缘开始测量。padding 是根据 viewPadding 和 viewInsets 计算得出的。由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的顶层 MediaQuery 的边界与包含该应用的窗口（通常是移动设备屏幕）边界相同。

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

另请参阅：

- [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，提供关于此属性及其与 [padding] 和 [viewPadding] 关系的更多详细信息。

### padding

```dart
EdgeInsets padding
```

显示屏上被系统 UI 部分遮挡的部分，通常是被硬件显示屏"刘海"或系统状态栏遮挡的部分。

如果你消耗了此 padding（例如通过构建一个 Widget，使其布局方式包裹或考虑了此 padding，从而使子级不再暴露于此 padding 之下），则应通过插入使用 [MediaQuery.removePadding] 工厂方法创建的新 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget，为后续的后代移除此 padding。

padding 是根据 [viewInsets] 和 [viewPadding] 的值推导得出的。

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

另请参阅：

- [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，提供关于此属性及其与 [viewInsets] 和 [viewPadding] 关系的更多详细信息。
- [SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea)，一个使用 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget 消耗此 padding，并自动将其从子级的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除的 Widget。

### viewPadding

```dart
EdgeInsets viewPadding
```

显示屏上被系统 UI 部分遮挡的部分，通常是被硬件显示屏"刘海"或系统状态栏遮挡的部分。

无论系统是否在同一物理屏幕区域报告其他遮挡情况，此值都保持不变。例如，屏幕底部的软键盘可能会覆盖并消耗与底部 padding 相同的区域，但不会影响此值。

此值独立于 [padding] 和 [viewInsets]：它们的值均从 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 边界的边缘开始测量。由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 创建的顶层 MediaQuery 的边界与包含该应用的窗口边界相同。在移动设备上，这通常是整个屏幕。

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

另请参阅：

- [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，提供关于此属性及其与 [padding] 和 [viewInsets] 关系的更多详细信息。

### systemGestureInsets

```dart
EdgeInsets systemGestureInsets
```

显示屏边缘沿线的区域，系统会在这些区域中消耗特定的输入事件，并阻止这些事件传递给应用程序。

从 Android Q 开始，从 [systemGestureInsets] 区域内开始的简单滑动手势会被系统用于页面导航，可能不会传递给应用程序。以长按开始的点按和滑动手势会传递给应用程序，但从 [systemGestureInsets] 定义区域内开始的简单按下-拖动-释放滑动手势可能不会。

应用程序应避免在系统手势内嵌区域内放置手势检测器。应用程序可以自由地在此区域内放置视觉元素。

目前，此属性预计仅在 Android Q 及更高版本上被设置为非默认值。

{@tool dartpad} 对于可能部署在启用了完整手势导航的 Android Q 设备上的应用程序，可以结合使用 [systemGestureInsets] 与 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding)，避免 [Slider](https://www.yuque.com/thyname/flutter.material/slider) 的左右边缘出现在系统手势导航保留区域内。

默认情况下，[Slider](https://www.yuque.com/thyname/flutter.material/slider) 会扩展以填满可用宽度。因此，我们对左右两侧进行了内边距填充。

** 请参阅 examples/api/lib/widgets/media_query/media_query_data.system_gesture_insets.0.dart 中的代码 ** {@end-tool}

### alwaysUse24HourFormat

```dart
bool alwaysUse24HourFormat
```

格式化时间时是否使用 24 小时制。

此标志的行为因平台而异：

- 在 Android 上，此标志直接反映名为"使用 24 小时格式"的用户设置。它适用于应用程序所使用的任何语言区域，无论是系统级语言区域还是应用程序设置的自定义语言区域。
- 在 iOS 上，当用户设置中名为"24 小时制"的选项被启用，或系统级语言区域默认使用 24 小时格式时，此标志被设为 true。
- 在 macOS 上，此标志反映当前系统语言区域的时间格式，其中已纳入系统设置中的"24 小时制"偏好设置。与 iOS 类似，这仅对系统语言区域生效；传递给应用程序的自定义语言区域会忽略 24 小时制偏好设置。
- 在 Windows 上，此标志派生自区域设置中用户的"短时间"格式；当配置的格式使用 24 小时制模式时为 true。
- 在 Linux 上，此标志反映桌面环境的时钟格式设置（如果可用），例如 GNOME 上的 `org.gnome.desktop.interface.clock-format`。对于未提供此类设置的桌面环境，默认值为 true（24 小时制）。
- 在 Web 上，此标志始终为 false。Flutter Web 引擎目前不会根据浏览器的语言区域设置填充此值，尽管浏览器通过 `Intl.DateTimeFormat.resolvedOptions().hourCycle` 暴露了首选的小时制。

### accessibleNavigation

```dart
bool accessibleNavigation
```

用户是否正在使用 TalkBack 或 VoiceOver 等无障碍服务与应用程序交互。

当此设置为 true 时，应禁用诸如超时之类的功能，或增加其最短持续时间。

另请参阅：

- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### invertColors

```dart
bool invertColors
```

操作系统当前是否正在反转平台的颜色。

此标志表示底层操作系统已经在屏幕层面执行了全局颜色反转。这并不意味着 Flutter 框架会自动反转其自身的布局绘制。

相反，此标志允许应用程序对反转做出响应。例如，可以有选择地重新反转图像、地图或视频播放内容，使其以自然颜色显示，而非呈现为底片效果。

此标志目前仅在 iOS 设备上更新。

另请参阅：

- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### highContrast

```dart
bool highContrast
```

平台是否请求前景内容与背景内容之间具有高对比度。

在 iOS 上，这对应于 设置 -> 辅助功能 中的"增强对比度"设置。在 Android 上，这对应于"高对比度文本"或类似的无障碍设置。

此标志表示操作系统已经在执行高对比度调整，或期望应用程序调整其调色板以满足更高的无障碍标准。

在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 覆盖中手动更改此值不会自动触发 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 中的主题变化。相反，[MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 会使用此值来决定是使用 [MaterialApp.highContrastTheme] 还是 [MaterialApp.highContrastDarkTheme]。

此标志目前仅在运行 iOS 13 及以上版本的 iOS 设备，以及运行 API 34 及以上版本的 Android 设备上更新。

### onOffSwitchLabels

```dart
bool onOffSwitchLabels
```

用户是否通过 设置 -> 辅助功能 -> 显示与文字大小 -> 开关标签 请求在 iOS 上的开关内部显示开/关标签。

另请参阅：

- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### disableAnimations

```dart
bool disableAnimations
```

平台是否请求尽可能禁用或减少动画。

这对应于 Android 的"移除动画"无障碍设置。

在 iOS 上，减少动态效果是通过 [dart:ui.AccessibilityFeatures.reduceMotion] 单独暴露的，不会设置此标志。

此值直接通过 [SemanticsBinding.disableAnimations] 从引擎读取。因此，框架级别的动画 API（例如 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)）会使用此值，且无法通过 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 覆盖。

在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 中手动覆盖此值不会影响框架动画（例如由 [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller) 驱动的动画）。但对于测试或需要显式读取 [MediaQueryData.disableAnimations] 的自定义 Widget 而言，覆盖此值仍然有用。

在实现自定义显式动画时，应检查此属性并相应地调整行为（例如，当其为 true 时缩短持续时间或跳过非必要动画）。

另请参阅：

- [AnimationController](https://www.yuque.com/thyname/flutter.animation/animationcontroller)，根据此设置调整其播放行为。
- [AnimationBehavior](https://www.yuque.com/thyname/flutter.animation/animationbehavior)，定义了此设置生效时动画的行为方式。
- [dart:ui.AccessibilityFeatures.disableAnimations]，此标志所依据的底层平台原始标志。
- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### boldText

```dart
bool boldText
```

平台是否请求以粗体字重绘制文本。

另请参阅：

- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### supportsAnnounce

```dart
bool supportsAnnounce
```

当前平台是否支持无障碍朗读通告（例如 [SemanticsService.sendAnnouncement]）。

在朗读通告已被弃用或底层平台不支持的平台上，返回 `false`。

在通常支持此类通告且不加限制的平台（iOS、Web 等）上，返回 `true`。

另请参阅：

- [dart:ui.PlatformDispatcher.accessibilityFeatures]，此设置的来源。

### navigationMode

```dart
NavigationMode navigationMode
```

描述平台请求的导航模式。

某些用户界面更适合使用方向键盘（DPAD）或箭头键进行导航，对于这些界面，某些 Widget 需要以不同方式处理这些方向事件。为了确定何时执行此操作，这些 Widget 会查找其上下文中生效的导航模式。

例如，在电视界面中，应设置 [NavigationMode.directional]，以便使用方向导航通过 DPAD 将焦点移出文本字段。相反，在将 [navigationMode] 设置为 [NavigationMode.traditional] 的常规桌面应用程序中，箭头键则用于移动光标而非导航。

[NavigationMode](https://www.yuque.com/thyname/flutter.widgets/navigationmode) 的取值表示对该值敏感的 Widget 子树中所使用的导航类型。

### gestureSettings

```dart
DeviceGestureSettings gestureSettings
```

此媒体查询所派生视图的手势设置。

其中包含针对手势行为的平台特定配置，例如触摸容差（touch slop）。相较于框架常量，配置手势行为时应优先使用这些设置。

### displayFeatures

```dart
List<ui.DisplayFeature> displayFeatures
```

{@macro dart.ui.ViewConfiguration.displayFeatures}

另请参阅：

- [dart:ui.DisplayFeatureType]，列出了不同类型的显示特性，并说明了它们之间的差异。
- [dart:ui.DisplayFeatureState]，列出了折叠特性（[dart:ui.DisplayFeatureType.fold] 和 [dart:ui.DisplayFeatureType.hinge]）可能的状态。

### supportsShowingSystemContextMenu

```dart
bool supportsShowingSystemContextMenu
```

是否支持显示系统上下文菜单。

例如，在 iOS 16.0 及以上版本中，为了避免在按下"粘贴"按钮时出现 iOS 剪贴板访问通知，可能会显示系统文本选择上下文菜单，而非 Flutter 绘制的上下文菜单。

另请参阅：

- [SystemContextMenuController](https://www.yuque.com/thyname/flutter.services/systemcontextmenucontroller) 和 [SystemContextMenu](https://www.yuque.com/thyname/flutter.widgets/systemcontextmenu)，当此标志指示支持时，可用于显示系统上下文菜单。

### lineHeightScaleFactorOverride

```dart
double? lineHeightScaleFactorOverride
```

覆盖文本的行高，以字号的倍数表示。

当平台未设置覆盖值时，返回 `null`。

另请参阅：

- [Text](https://www.yuque.com/thyname/flutter.widgets/text)、[SelectableText](https://www.yuque.com/thyname/flutter.material/selectabletext) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，它们的 [TextStyle.height] 和 [StrutStyle.height] 均会被 [lineHeightScaleFactorOverride] 覆盖。

### letterSpacingOverride

```dart
double? letterSpacingOverride
```

覆盖文本中每个字母之间要添加的间距量（以逻辑像素为单位）。

负值可用于使字母之间更靠近。

当平台未设置字母间距覆盖值时，返回 `null`。

另请参阅：

- [Text](https://www.yuque.com/thyname/flutter.widgets/text)、[SelectableText](https://www.yuque.com/thyname/flutter.material/selectabletext) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，它们的 [TextStyle.letterSpacing] 均会被 [letterSpacingOverride] 覆盖。

### wordSpacingOverride

```dart
double? wordSpacingOverride
```

覆盖文本中每个空白序列（即每个单词之间）要添加的间距量（以逻辑像素为单位）。

负值可用于使单词之间更靠近。

当平台未设置单词间距覆盖值时，返回 `null`。

另请参阅：

- [Text](https://www.yuque.com/thyname/flutter.widgets/text)、[SelectableText](https://www.yuque.com/thyname/flutter.material/selectabletext) 和 [EditableText](https://www.yuque.com/thyname/flutter.widgets/editabletext)，它们的 [TextStyle.wordSpacing] 均会被 [wordSpacingOverride] 覆盖。

### paragraphSpacingOverride

```dart
double? paragraphSpacingOverride
```

每个段落之后要添加的间距量（以逻辑像素为单位）。

当平台未设置段落间距覆盖值时，返回 `null`。

### displayCornerRadii

```dart
BorderRadius? displayCornerRadii
```

显示屏圆角的半径，以逻辑像素为单位。

目前仅在 Android API 31+ 上填充此值。在更早的 Android 版本、iOS 以及其他平台上，此值为 `null`。

另请参阅：

- [FlutterView.displayCornerRadii]，以物理像素为单位返回显示屏圆角半径。

### orientation

```dart
Orientation get orientation
```

媒体的方向（例如设备处于横屏还是竖屏模式）。

### copyWith()

```dart
MediaQueryData copyWith({Size? size, double? devicePixelRatio, double? textScaleFactor, TextScaler? textScaler, Brightness? platformBrightness, EdgeInsets? padding, EdgeInsets? viewPadding, EdgeInsets? viewInsets, EdgeInsets? systemGestureInsets, bool? alwaysUse24HourFormat, bool? highContrast, bool? onOffSwitchLabels, bool? disableAnimations, bool? invertColors, bool? accessibleNavigation, bool? boldText, bool? supportsAnnounce, NavigationMode? navigationMode, DeviceGestureSettings? gestureSettings, List<ui.DisplayFeature>? displayFeatures, bool? supportsShowingSystemContextMenu})
```

创建此媒体查询数据的副本，并将给定字段替换为新值。

`textScaler` 参数与 `textScaleFactor` 参数不能同时指定。

### applyTextStyleOverrides()

```dart
MediaQueryData applyTextStyleOverrides({required double? lineHeightScaleFactorOverride, required double? letterSpacingOverride, required double? wordSpacingOverride, required double? paragraphSpacingOverride})
```

创建此媒体查询数据的副本，并将 `lineHeightScaleFactorOverride`、`letterSpacingOverride`、`wordSpacingOverride` 和 `paragraphSpacingOverride` 替换为给定的值。

如果参数为空（默认值），则返回的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中对应的覆盖值将被设置为空。

另请参阅：

- [MediaQuery.applyTextStyleOverrides]，使用此方法为环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 应用文本样式覆盖。

### applyDisplayCornerRadii()

```dart
MediaQueryData applyDisplayCornerRadii(BorderRadius? displayCornerRadii)
```

创建此媒体查询数据的副本，并将 `displayCornerRadii` 替换为给定的值。

如果参数为空（默认值），则返回的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中 `displayCornerRadii` 将被设置为空。

### removePadding()

```dart
MediaQueryData removePadding({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

创建此媒体查询数据的副本，并将给定的 [padding] 替换为零。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则原样返回此 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，不做任何修改。

另请参阅：

- [MediaQuery.removePadding]，使用此方法从环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除 [padding]。
- [SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea)，既从 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除 padding，又添加一个 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget。
- [removeViewInsets]，功能相同，但针对 [viewInsets]。
- [removeViewPadding]，功能相同，但针对 [viewPadding]。

### removeViewInsets()

```dart
MediaQueryData removeViewInsets({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

创建此媒体查询数据的副本，并将给定的 [viewInsets] 替换为零。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则原样返回此 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，不做任何修改。

另请参阅：

- [MediaQuery.removeViewInsets]，使用此方法从环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除 [viewInsets]。
- [removePadding]，功能相同，但针对 [padding]。
- [removeViewPadding]，功能相同，但针对 [viewPadding]。

### removeViewPadding()

```dart
MediaQueryData removeViewPadding({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

创建此媒体查询数据的副本，并将给定的 [viewPadding] 替换为零。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则原样返回此 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，不做任何修改。

另请参阅：

- [MediaQuery.removeViewPadding]，使用此方法从环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除 [viewPadding]。
- [removePadding]，功能相同，但针对 [padding]。
- [removeViewInsets]，功能相同，但针对 [viewInsets]。

### removeDisplayFeatures()

```dart
MediaQueryData removeDisplayFeatures(Rect subScreen)
```

创建此媒体查询数据的副本，移除完全位于给定子屏幕之外的 [displayFeatures]，并将不属于该子屏幕的边上的 [padding]、[viewInsets] 和 [viewPadding] 调整为零。

如果子屏幕与可用屏幕空间重合，则返回未经修改的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)。

在调试模式下，如果给定的子屏幕超出可用屏幕空间，则会触发断言。

另请参阅：

- [DisplayFeatureSubScreen](https://www.yuque.com/thyname/flutter.widgets/displayfeaturesubscreen)，从 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除分割屏幕的显示特性，并添加一个 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget，以将子级定位到与所选子屏幕匹配的位置。

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

# MediaQuery

```dart
class MediaQuery extends InheritedModel<_MediaQueryAspect> {}
```

建立一个子树，在其中媒体查询会解析为给定的数据。

例如，要了解当前视图（例如包含你的应用程序的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)）的尺寸，可以使用 [MediaQuery.sizeOf]：`MediaQuery.sizeOf(context)`。

使用特定方法（例如 [MediaQuery.sizeOf] 或 [MediaQuery.paddingOf]）查询当前媒体时，会在该特定属性发生变化时自动重建你的 Widget。

{@template flutter.widgets.media*query.MediaQuery.useSpecific} 使用 [MediaQuery.of] 进行查询会在 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 的*任意\*字段发生变化时（例如用户旋转设备时）自动重建你的 Widget。因此，除非你关心整个 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象的变化，否则建议使用特定方法（例如：[MediaQuery.sizeOf] 和 [MediaQuery.paddingOf]），因为它们能带来更高效的重建。

如果当前作用域内没有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，则 [MediaQuery.of] 以及类似 [MediaQuery.sizeOf] 的 "...Of" 方法将抛出异常。此外，也可以使用"maybe-"变体方法（例如 [MediaQuery.maybeOf] 和 [MediaQuery.maybeSizeOf]），当作用域内没有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 时，这些方法将返回空值而非抛出异常。{@endtemplate}

{@youtube 560 315 https://www.youtube.com/watch?v=A3WrA4zAaPw}

另请参阅：

- [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 和 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp)，它们会引入一个 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，并随着当前屏幕指标的变化保持其更新。
- [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，表示这些指标的数据结构。

### MediaQuery()

```dart
MediaQuery({dynamic key, required MediaQueryData data, required Widget child})
```

创建一个向其后代提供 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 的 Widget。

### MediaQuery.removePadding()

```dart
MediaQuery.removePadding({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

创建一个新的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，继承自给定上下文中环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的数据，但移除指定的 padding。

当 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 padding 被某个 Widget 以某种方式消耗，导致该 padding 不再暴露给该 Widget 的后代或同级时，应将此 Widget 插入 Widget 树中。

[context] 参数所在作用域内必须存在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则返回的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 会原样复用环境 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，此时该操作没有太大意义。

另请参阅：

- [SafeArea](https://www.yuque.com/thyname/flutter.widgets/safearea)，既从 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中移除 padding，又添加一个 [Padding](https://www.yuque.com/thyname/flutter.widgets/padding) Widget。
- [MediaQueryData.padding]，受影响的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 属性。
- [MediaQuery.removeViewInsets]，功能相同，但针对 [MediaQueryData.viewInsets]。
- [MediaQuery.removeViewPadding]，功能相同，但针对 [MediaQueryData.viewPadding]。

### MediaQuery.removeViewInsets()

```dart
MediaQuery.removeViewInsets({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

创建一个新的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，继承自给定上下文中环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的数据，但移除指定的视图内嵌区域（view insets）。

当 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的视图内嵌区域被某个 Widget 以某种方式消耗，导致其不再暴露给该 Widget 的后代或同级时，应将此 Widget 插入 Widget 树中。

[context] 参数所在作用域内必须存在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则返回的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 会原样复用环境 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，此时该操作没有太大意义。

另请参阅：

- [MediaQueryData.viewInsets]，受影响的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 属性。
- [MediaQuery.removePadding]，功能相同，但针对 [MediaQueryData.padding]。
- [MediaQuery.removeViewPadding]，功能相同，但针对 [MediaQueryData.viewPadding]。

### MediaQuery.removeViewPadding()

```dart
MediaQuery.removeViewPadding({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

创建一个新的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，继承自给定上下文中环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的数据，但移除指定的视图内边距（view padding）。

当 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的视图内边距被某个 Widget 以某种方式消耗，导致其不再暴露给该 Widget 的后代或同级时，应将此 Widget 插入 Widget 树中。

[context] 参数所在作用域内必须存在 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)。

如果 `removeLeft`、`removeTop`、`removeRight` 和 `removeBottom` 这四个参数均为 false（默认值），则返回的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 会原样复用环境 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata)，此时该操作没有太大意义。

另请参阅：

- [MediaQueryData.viewPadding]，受影响的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 属性。
- [MediaQuery.removePadding]，功能相同，但针对 [MediaQueryData.padding]。
- [MediaQuery.removeViewInsets]，功能相同，但针对 [MediaQueryData.viewInsets]。

### applyTextStyleOverrides()

```dart
Widget applyTextStyleOverrides({Key? key, required double? lineHeightScaleFactorOverride, required double? letterSpacingOverride, required double? wordSpacingOverride, required double? paragraphSpacingOverride, required Widget child})
```

将 `child` 包装在一个 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中，并将其 [MediaQueryData.lineHeightScaleFactorOverride]、[MediaQueryData.letterSpacingOverride]、[MediaQueryData.wordSpacingOverride]、[MediaQueryData.paragraphSpacingOverride] 设置为指定的值。

如果文本样式覆盖参数为空（默认值），则更新后的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中对应的覆盖值将被设置为空。

返回的 Widget 必须插入到现有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 下方的 Widget 树中。

另请参阅：

- [MediaQueryData.lineHeightScaleFactorOverride]、[MediaQueryData.letterSpacingOverride]、[MediaQueryData.wordSpacingOverride]、[MediaQueryData.paragraphSpacingOverride]，受影响的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 属性。

### fromWindow()

```dart
Widget fromWindow({Key? key, required Widget child})
```

已弃用。请改用 [MediaQuery.fromView]。

此构造函数基于单一窗口假设运行。为准备支持 Flutter 即将推出的多窗口支持，该构造函数已被弃用。

已由 [MediaQuery.fromView] 取代，后者要求指定构造 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 所针对的 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)。例如，可以通过 [View.of] 从上下文中获取该 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview)，或从 [PlatformDispatcher.views] 中获取。

### fromView()

```dart
Widget fromView({Key? key, required FlutterView view, required Widget child})
```

将 [child] 包装在一个使用提供的 [view] 数据构建的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中。

该 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 是使用外围 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的平台特定数据以及提供的 [view] 的视图特定数据构建的。如果不存在外围 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，则平台特定数据会从与提供的 [view] 关联的 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 生成。任何通过 [PlatformDispatcher](https://www.yuque.com/thyname/dart.ui/platformdispatcher) 暴露的信息都被视为平台特定数据。直接在 [FlutterView](https://www.yuque.com/thyname/dart.ui/flutterview) 上暴露的数据（不包括其 [FlutterView.platformDispatcher] 属性）被视为视图特定数据。

当用于构建此 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的任何数据发生变化时，注入的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 会自动更新。

### withNoTextScaling()

```dart
Widget withNoTextScaling({Key? key, required Widget child})
```

将 `child` 包装在一个 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中，并将其 [MediaQueryData.textScaler] 设置为 [TextScaler.noScaling]。

返回的 Widget 必须插入到现有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 下方的 Widget 树中。

例如，这可用于防止图标字体随着用户调整平台文本缩放值而缩放。

### withClampedTextScaling()

```dart
Widget withClampedTextScaling({Key? key, double minScaleFactor = 0.0, double maxScaleFactor = double.infinity, required Widget child})
```

将 `child` 包装在一个 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 中，并对当前的 [MediaQueryData.textScaler] 应用 [TextScaler.clamp]。

返回的 Widget 必须插入到现有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 下方的 Widget 树中。

这是一个便捷函数，用于将缩放后的文本大小限制在 `[minScaleFactor * fontSize, maxScaleFactor * fontSize]` 范围内（例如，用于防止过度的文本缩放破坏 UI）。当 `minScaleFactor` 等于 `maxScaleFactor` 时，缩放器将变为 `TextScaler.linear(minScaleFactor)`。

### data

```dart
MediaQueryData data
```

包含关于当前媒体的信息。

例如，[MediaQueryData.size] 属性包含当前窗口的宽度和高度。

### of()

```dart
MediaQueryData of(BuildContext context)
```

包含给定上下文的最近该类实例中的数据。

你可以使用此函数查询当前 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象中保存的整个数据集。当其中任何信息发生变化时，你的 Widget 将被安排重建，以保持最新状态。

由于通常一个 Widget 只需要 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象属性的一个子集，因此建议使用更具体的方法（例如：[MediaQuery.sizeOf] 和 [MediaQuery.paddingOf]），因为这些方法不会在无关属性更新时导致 Widget 重建。

典型用法如下：

```dart
MediaQueryData media = MediaQuery.of(context);
```

如果作用域内没有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，此方法在 release 构建中将抛出 [TypeError](https://www.yuque.com/thyname/dart.core/typeerror) 异常，在 debug 构建中将抛出具有详细描述的 [FlutterError](https://www.yuque.com/thyname/flutter.foundation/fluttererror)。

另请参阅：

- [maybeOf]，如果找不到 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先，不会抛出异常或触发断言，而是返回空值。
- [sizeOf](https://www.yuque.com/thyname/dart.ffi/sizeof) 及其他用于获取特定值并依赖其变化的具体方法。

### maybeOf()

```dart
MediaQueryData? maybeOf(BuildContext context)
```

包含给定上下文的最近该类实例中的数据（如果存在）。

如果你希望允许作用域内没有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的情形，请使用此函数。在通常预期媒体查询始终存在的情形下，建议使用 [MediaQuery.of]。

如果作用域内没有 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery)，则此函数将返回空值。

你可以使用此函数查询当前 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象中保存的整个数据集。当其中任何信息发生变化时，你的 Widget 将被安排重建，以保持最新状态。

由于通常一个 Widget 只需要 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 对象属性的一个子集，因此建议使用更具体的方法（例如：[MediaQuery.maybeSizeOf] 和 [MediaQuery.maybePaddingOf]），因为这些方法不会在无关属性更新时导致 Widget 重建。

典型用法如下：

```dart
MediaQueryData? mediaQuery = MediaQuery.maybeOf(context);
if (mediaQuery == null) {
  // 改为执行其他操作。
}
```

另请参阅：

- [of]，如果找不到 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先则会抛出异常，而非返回空值。
- [maybeSizeOf] 及其他用于获取特定值并依赖其变化的具体方法。

### sizeOf()

```dart
Size sizeOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.size]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性发生变化时重建。

{@template flutter.widgets.media*query.MediaQuery.dontUseOf} 建议优先使用此函数，而非直接从 [of] 返回的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中获取属性，因为使用此函数只会在此特定属性发生变化时才重建 `context`，而不会在*任意\*属性发生变化时都重建。{@endtemplate}

### maybeSizeOf()

```dart
Size? maybeSizeOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.size]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性发生变化时重建。

{@template flutter.widgets.media*query.MediaQuery.dontUseMaybeOf} 建议优先使用此函数，而非直接从 [maybeOf] 返回的 [MediaQueryData](https://www.yuque.com/thyname/flutter.widgets/mediaquerydata) 中获取属性，因为使用此函数只会在此特定属性发生变化时才重建 `context`，而不会在*任意\*属性发生变化时都重建。{@endtemplate}

### widthOf()

```dart
double widthOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中 [MediaQueryData.size] 的宽度；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性宽度发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeWidthOf()

```dart
double? maybeWidthOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中 [MediaQueryData.size] 的宽度；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性宽度发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### heightOf()

```dart
double heightOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中 [MediaQueryData.size] 的高度；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性高度发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeHeightOf()

```dart
double? maybeHeightOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中 [MediaQueryData.size] 的高度；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.size] 属性高度发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### orientationOf()

```dart
Orientation orientationOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.orientation]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.orientation] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeOrientationOf()

```dart
Orientation? maybeOrientationOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.orientation]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.orientation] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### devicePixelRatioOf()

```dart
double devicePixelRatioOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.devicePixelRatio]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.devicePixelRatio] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDevicePixelRatioOf()

```dart
double? maybeDevicePixelRatioOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.devicePixelRatio]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.devicePixelRatio] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### textScaleFactorOf()

```dart
double textScaleFactorOf(BuildContext context)
```

已弃用。将在未来版本的 Flutter 中移除。请改用 [maybeTextScalerOf]。

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.textScaleFactor]；如果不存在这样的祖先，则返回 1.0。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.textScaleFactor] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeTextScaleFactorOf()

```dart
double? maybeTextScaleFactorOf(BuildContext context)
```

已弃用。将在未来版本的 Flutter 中移除。请改用 [maybeTextScalerOf]。

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.textScaleFactor]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.textScaleFactor] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### textScalerOf()

```dart
TextScaler textScalerOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.textScaler]；如果不存在这样的祖先，则返回 [TextScaler.noScaling]。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.textScaler] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeTextScalerOf()

```dart
TextScaler? maybeTextScalerOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.textScaler]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.textScaler] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### platformBrightnessOf()

```dart
Brightness platformBrightnessOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.platformBrightness]；如果不存在这样的祖先，则返回 [Brightness.light]。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.platformBrightness] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybePlatformBrightnessOf()

```dart
Brightness? maybePlatformBrightnessOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.platformBrightness]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.platformBrightness] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### paddingOf()

```dart
EdgeInsets paddingOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.padding]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.padding] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybePaddingOf()

```dart
EdgeInsets? maybePaddingOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.padding]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.padding] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### viewInsetsOf()

```dart
EdgeInsets viewInsetsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.viewInsets]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.viewInsets] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeViewInsetsOf()

```dart
EdgeInsets? maybeViewInsetsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.viewInsets]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.viewInsets] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### systemGestureInsetsOf()

```dart
EdgeInsets systemGestureInsetsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.systemGestureInsets]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.systemGestureInsets] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSystemGestureInsetsOf()

```dart
EdgeInsets? maybeSystemGestureInsetsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.systemGestureInsets]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.systemGestureInsets] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### viewPaddingOf()

```dart
EdgeInsets viewPaddingOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.viewPadding]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.viewPadding] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeViewPaddingOf()

```dart
EdgeInsets? maybeViewPaddingOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.viewPadding]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.viewPadding] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### alwaysUse24HourFormatOf()

```dart
bool alwaysUse24HourFormatOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.alwaysUse24HourFormat]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.alwaysUse24HourFormat] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeAlwaysUse24HourFormatOf()

```dart
bool? maybeAlwaysUse24HourFormatOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.alwaysUse24HourFormat]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.alwaysUse24HourFormat] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### accessibleNavigationOf()

```dart
bool accessibleNavigationOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.accessibleNavigation]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.accessibleNavigation] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeAccessibleNavigationOf()

```dart
bool? maybeAccessibleNavigationOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.accessibleNavigation]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.accessibleNavigation] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### invertColorsOf()

```dart
bool invertColorsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.invertColors]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.invertColors] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeInvertColorsOf()

```dart
bool? maybeInvertColorsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.invertColors]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.invertColors] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### highContrastOf()

```dart
bool highContrastOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.highContrast]；如果不存在这样的祖先，则返回 false。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.highContrast] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeHighContrastOf()

```dart
bool? maybeHighContrastOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.highContrast]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.highContrast] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### onOffSwitchLabelsOf()

```dart
bool onOffSwitchLabelsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.onOffSwitchLabels]；如果不存在这样的祖先，则返回 false。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.onOffSwitchLabels] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeOnOffSwitchLabelsOf()

```dart
bool? maybeOnOffSwitchLabelsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.onOffSwitchLabels]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.onOffSwitchLabels] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### disableAnimationsOf()

```dart
bool disableAnimationsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.disableAnimations]；如果不存在这样的祖先，则返回 false。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.disableAnimations] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisableAnimationsOf()

```dart
bool? maybeDisableAnimationsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.disableAnimations]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.disableAnimations] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### boldTextOf()

```dart
bool boldTextOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.boldText] 无障碍设置；如果不存在这样的祖先，则返回 false。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.boldText] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeBoldTextOf()

```dart
bool? maybeBoldTextOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.boldText] 无障碍设置；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.boldText] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### supportsAnnounceOf()

```dart
bool supportsAnnounceOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.supportsAnnounce] 无障碍设置；如果不存在这样的祖先，则返回 false。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.supportsAnnounce] 属性发生变化时重建。这一点对于 supportsAnnounce 尤为重要，因为 supportsAnnounce 的变化频率较低。在所有媒体查询数据变化时都重建与仅在 supportsAnnounce 变化时才重建之间，性能差异非常显著。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSupportsAnnounceOf()

```dart
bool? maybeSupportsAnnounceOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.supportsAnnounce] 无障碍设置；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.supportsAnnounce] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### navigationModeOf()

```dart
NavigationMode navigationModeOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.navigationMode]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.navigationMode] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeNavigationModeOf()

```dart
NavigationMode? maybeNavigationModeOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.navigationMode]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.navigationMode] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### gestureSettingsOf()

```dart
DeviceGestureSettings gestureSettingsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.gestureSettings]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.gestureSettings] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeGestureSettingsOf()

```dart
DeviceGestureSettings? maybeGestureSettingsOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.gestureSettings]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.gestureSettings] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### displayFeaturesOf()

```dart
List<ui.DisplayFeature> displayFeaturesOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.displayFeatures]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.displayFeatures] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisplayFeaturesOf()

```dart
List<ui.DisplayFeature>? maybeDisplayFeaturesOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.displayFeatures]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.displayFeatures] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### supportsShowingSystemContextMenu()

```dart
bool supportsShowingSystemContextMenu(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.supportsShowingSystemContextMenu]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.supportsShowingSystemContextMenu] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSupportsShowingSystemContextMenu()

```dart
bool? maybeSupportsShowingSystemContextMenu(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.supportsShowingSystemContextMenu]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.supportsShowingSystemContextMenu] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeLineHeightScaleFactorOverrideOf()

```dart
double? maybeLineHeightScaleFactorOverrideOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.lineHeightScaleFactorOverride]；如果不存在这样的祖先，或平台未指定覆盖值，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.lineHeightScaleFactorOverride] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeLetterSpacingOverrideOf()

```dart
double? maybeLetterSpacingOverrideOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.letterSpacingOverride]；如果不存在这样的祖先，或平台未指定覆盖值，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.letterSpacingOverride] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeWordSpacingOverrideOf()

```dart
double? maybeWordSpacingOverrideOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.wordSpacingOverride]；如果不存在这样的祖先，或平台未指定覆盖值，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.wordSpacingOverride] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeParagraphSpacingOverrideOf()

```dart
double? maybeParagraphSpacingOverrideOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.paragraphSpacingOverride]；如果不存在这样的祖先，或平台未指定覆盖值，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.paragraphSpacingOverride] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### displayCornerRadiiOf()

```dart
BorderRadius? displayCornerRadiiOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.displayCornerRadii]；如果不存在这样的祖先，则抛出异常。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.displayCornerRadii] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisplayCornerRadiiOf()

```dart
BorderRadius? maybeDisplayCornerRadiiOf(BuildContext context)
```

返回最近的 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 祖先中的 [MediaQueryData.displayCornerRadii]；如果不存在这样的祖先，则返回空值。

使用此方法会导致给定的 [context] 在祖先 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [MediaQueryData.displayCornerRadii] 属性发生变化时重建。

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### updateShouldNotify()

```dart
bool updateShouldNotify(MediaQuery oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### updateShouldNotifyDependent()

```dart
bool updateShouldNotifyDependent(MediaQuery oldWidget, Set<Object> dependencies)
```

# NavigationMode

```dart
enum NavigationMode {}
```

描述由 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 设置的导航模式。

不同的模式表示对该值敏感的 Widget 子树中所使用的导航类型。

使用 `MediaQuery.navigationModeOf(context)` 确定给定上下文中生效的导航模式。使用 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) Widget 为其后代 Widget 设置导航模式。

表示传统的键盘加鼠标导航模式。

在此导航模式下，箭头键可用于诸如移动滑块或光标之类的次要修改操作，被禁用的控件将失去焦点且不可通过遍历访问。

表示基于方向的导航模式。

此导航模式表示箭头键应保留用于导航操作，而诸如移动滑块或光标之类的次要修改操作，将使用替代绑定或被禁用。

某些行为也会受此模式影响。例如，被禁用的控件在禁用时会保留焦点，并且在被遍历时仍能够获得焦点（尽管它们仍处于禁用状态）。

# SystemTextScaler

```dart
final class SystemTextScaler extends TextScaler {}
```

一个反映用户在平台无障碍设置中字体缩放偏好的 [TextScaler](https://www.yuque.com/thyname/flutter.painting/textscaler)。

### scale()

```dart
double scale(double fontSize)
```

### textScaleFactor

```dart
double textScaleFactor
```

表示当前用户对字体缩放因子偏好设置的数值。

此数值通常用于比较各个 [SystemTextScaler](https://www.yuque.com/thyname/flutter.widgets/systemtextscaler)。当两个 [SystemTextScaler](https://www.yuque.com/thyname/flutter.widgets/systemtextscaler) 实例具有相同的 [textScaleFactor] 时，即可视为相等，因为在给定相同输入字号的情况下，它们的 [scale] 方法会产生相同的输出。但是，[textScaleFactor] 不应用于算术运算。
