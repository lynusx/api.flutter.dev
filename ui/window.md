# Display

```dart
class Display {}
```

A configurable display that a [FlutterView] renders on.

Use [FlutterView.display] to get the current display for that view.

### id

```dart
int id
```

A unique identifier for this display.

This identifier is unique among a list of displays the Flutter framework is aware of, and is not derived from any platform specific identifiers for displays.

### devicePixelRatio

```dart
double devicePixelRatio
```

The device pixel ratio of this display.

This value is the same as the value of [FlutterView.devicePixelRatio] for all view objects attached to this display.

### size

```dart
Size size
```

The physical size of this display.

### refreshRate

```dart
double refreshRate
```

The refresh rate in FPS of this display.

### toString()

```dart
String toString()
```

# FlutterView

```dart
class FlutterView {}
```

A view into which a Flutter [Scene] is drawn.

Each [FlutterView] has its own layer tree that is rendered whenever [render] is called on it with a [Scene].

References to [FlutterView] objects are obtained via the [PlatformDispatcher].

## Insets and Padding

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/widgets/window_padding.mp4}

In this illustration, the black areas represent system UI that the app cannot draw over. The red area represents view padding that the view may not be able to detect gestures in and may not want to draw in. The grey area represents the system keyboard, which can cover over the bottom view padding when visible.

The [viewInsets] are the physical pixels which the operating system reserves for system UI, such as the keyboard, which would fully obscure any content drawn in that area.

The [viewPadding] are the physical pixels on each side of the display that may be partially obscured by system UI or by physical intrusions into the display, such as an overscan region on a television or a "notch" on a phone. Unlike the insets, these areas may have portions that show the user view-painted pixels without being obscured, such as a notch at the top of a phone that covers only a subset of the area. Insets, on the other hand, either partially or fully obscure the window, such as an opaque keyboard or a partially translucent status bar, which cover an area without gaps.

The [padding] property is computed from both [viewInsets] and [viewPadding]. It will allow a view inset to consume view padding where appropriate, such as when a phone's keyboard is covering the bottom view padding and so "absorbs" it.

Clients that want to position elements relative to the view padding regardless of the view insets should use the [viewPadding] property, e.g. if you wish to draw a widget at the center of the screen with respect to the iPhone "safe area" regardless of whether the keyboard is showing.

[padding] is useful for clients that want to know how much padding should be accounted for without concern for the current inset(s) state, e.g. determining whether a gesture should be considered for scrolling purposes. This value varies based on the current state of the insets. For example, a visible keyboard will consume all gestures in the bottom part of the [viewPadding] anyway, so there is no need to account for that in the [padding], which is always safe to use for such calculations.

### viewId

```dart
int viewId
```

The opaque ID for this view.

### platformDispatcher

```dart
PlatformDispatcher platformDispatcher
```

The platform dispatcher that this view is registered with, and gets its information from.

### display

```dart
Display get display
```

The [Display] this view is drawn in.

### devicePixelRatio

```dart
double get devicePixelRatio
```

The number of device pixels for each logical pixel for the screen this view is displayed on.

This number might not be a power of two. Indeed, it might not even be an integer. For example, the Nexus 6 has a device pixel ratio of 3.5.

Device pixels are also referred to as physical pixels. Logical pixels are also referred to as device-independent or resolution-independent pixels.

By definition, there are roughly 38 logical pixels per centimeter, or about 96 logical pixels per inch, of the physical display. The value returned by [devicePixelRatio] is ultimately obtained either from the hardware itself, the device drivers, or a hard-coded value stored in the operating system or firmware, and may be inaccurate, sometimes by a significant margin.

The Flutter framework operates in logical pixels, so it is rarely necessary to directly deal with this property.

When this changes, [PlatformDispatcher.onMetricsChanged] is called. When using the Flutter framework, using [MediaQuery.of] to obtain the device pixel ratio (via [MediaQueryData.devicePixelRatio]), instead of directly obtaining the [devicePixelRatio] from a [FlutterView], will automatically cause any widgets dependent on this value to rebuild when it changes, without having to listen to [PlatformDispatcher.onMetricsChanged].

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [Display.devicePixelRatio], which reports the DPR of the display. The value here is equal to the value exposed on [display].

### physicalConstraints

```dart
ViewConstraints get physicalConstraints
```

The sizing constraints in physical pixels for this view.

The view can take on any [Size] that fulfills these constraints. These constraints are typically used by an UI framework as the input for its layout algorithm to determine an appropriate size for the view. To size the view, the selected size must be provided to the [render] method and it must satisfy the constraints.

When this changes, [PlatformDispatcher.onMetricsChanged] is called.

At startup, the constraints for the view may not be known before Dart code runs. If this value is observed early in the application lifecycle, it may report constraints with all dimensions set to zero.

This value does not take into account any on-screen keyboards or other system UI. If the constraints are tight, the [padding] and [viewInsets] properties provide information about how much of each side of the view may be obscured by system UI. If the constraints are loose, this information is not known upfront.

See also:

- [physicalSize], which returns the current size of the view.

### physicalSize

```dart
Size get physicalSize
```

The current dimensions of the rectangle as last reported by the platform into which scenes rendered in this view are drawn.

If the view is configured with loose [physicalConstraints] this value may be outdated by a few frames as it only updates when the size chosen for a frame (as provided to the [render] method) is processed by the platform. Because of this, [physicalConstraints] should be used instead of this value as the root input to the layout algorithm of UI frameworks.

When this changes, [PlatformDispatcher.onMetricsChanged] is called. When using the Flutter framework, using [MediaQuery.of] to obtain the size (via [MediaQueryData.size]), instead of directly obtaining the [physicalSize] from a [FlutterView], will automatically cause any widgets dependent on the size to rebuild when the size changes, without having to listen to [PlatformDispatcher.onMetricsChanged].

At startup, the size of the view may not be known before Dart code runs. If this value is observed early in the application lifecycle, it may report [Size.zero].

This value does not take into account any on-screen keyboards or other system UI. The [padding] and [viewInsets] properties provide information about how much of each side of the view may be obscured by system UI.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.

### viewInsets

```dart
ViewPadding get viewInsets
```

The number of physical pixels on each side of the display rectangle into which the view can render, but over which the operating system will likely place system UI, such as the keyboard, that fully obscures any content.

When this property changes, [PlatformDispatcher.onMetricsChanged] is called. When using the Flutter framework, using [MediaQuery.of] to obtain the insets (via [MediaQueryData.viewInsets]), instead of directly obtaining the [viewInsets] from a [FlutterView], will automatically cause any widgets dependent on the insets to rebuild when they change, without having to listen to [PlatformDispatcher.onMetricsChanged].

The relationship between this [viewInsets], [viewPadding], and [padding] are described in more detail in the documentation for [FlutterView].

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [MediaQuery.of], a simpler mechanism for the same.
- [Scaffold], which automatically applies the view insets in material design applications.

### viewPadding

```dart
ViewPadding get viewPadding
```

The number of physical pixels on each side of the display rectangle into which the view can render, but which may be partially obscured by system UI (such as the system notification area), or physical intrusions in the display (e.g. overscan regions on television screens or phone sensor housings).

Unlike [padding], this value does not change relative to [viewInsets]. For example, on an iPhone X, it will not change in response to the soft keyboard being visible or hidden, whereas [padding] will.

When this property changes, [PlatformDispatcher.onMetricsChanged] is called. When using the Flutter framework, using [MediaQuery.of] to obtain the padding (via [MediaQueryData.viewPadding]), instead of directly obtaining the [viewPadding] from a [FlutterView], will automatically cause any widgets dependent on the padding to rebuild when it changes, without having to listen to [PlatformDispatcher.onMetricsChanged].

The relationship between this [viewInsets], [viewPadding], and [padding] are described in more detail in the documentation for [FlutterView].

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [MediaQuery.of], a simpler mechanism for the same.
- [Scaffold], which automatically applies the padding in material design applications.

### systemGestureInsets

```dart
ViewPadding get systemGestureInsets
```

The number of physical pixels on each side of the display rectangle into which the view can render, but where the operating system will consume input gestures for the sake of system navigation.

For example, an operating system might use the vertical edges of the screen, where swiping inwards from the edges takes users backward through the history of screens they previously visited.

When this property changes, [PlatformDispatcher.onMetricsChanged] is called.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [MediaQuery.of], a simpler mechanism for the same.

### padding

```dart
ViewPadding get padding
```

The number of physical pixels on each side of the display rectangle into which the view can render, but which may be partially obscured by system UI (such as the system notification area), or physical intrusions in the display (e.g. overscan regions on television screens or phone sensor housings).

This value is calculated by taking `max(0.0, FlutterView.viewPadding - FlutterView.viewInsets)`. This will treat a system IME that increases the bottom inset as consuming that much of the bottom padding. For example, on an iPhone X, [EdgeInsets.bottom] of [FlutterView.padding] is the same as [EdgeInsets.bottom] of [FlutterView.viewPadding] when the soft keyboard is not drawn (to account for the bottom soft button area), but will be `0.0` when the soft keyboard is visible.

When this changes, [PlatformDispatcher.onMetricsChanged] is called. When using the Flutter framework, using [MediaQuery.of] to obtain the padding (via [MediaQueryData.padding]), instead of directly obtaining the [padding] from a [FlutterView], will automatically cause any widgets dependent on the padding to rebuild when it changes, without having to listen to [PlatformDispatcher.onMetricsChanged].

The relationship between this [viewInsets], [viewPadding], and [padding] are described in more detail in the documentation for [FlutterView].

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [MediaQuery.of], a simpler mechanism for the same.
- [Scaffold], which automatically applies the padding in material design applications.

### gestureSettings

```dart
GestureSettings get gestureSettings
```

Additional configuration for touch gestures performed on this view.

For example, the touch slop defined in physical pixels may be provided by the gesture settings and should be preferred over the framework touch slop constant.

### displayFeatures

```dart
List<DisplayFeature> get displayFeatures
```

{@template dart.ui.ViewConfiguration.displayFeatures} Areas of the display that are obstructed by hardware features.

This list is populated only on Android. If the device has no display features, this list is empty.

The coordinate space in which the [DisplayFeature.bounds] are defined spans across the screens currently in use. This means that the space between the screens is virtually part of the Flutter view space, with the [DisplayFeature.bounds] of the display feature as an obstructed area. The [DisplayFeature.type] can be used to determine if this display feature obstructs the screen or not. For example, [DisplayFeatureType.hinge] and [DisplayFeatureType.cutout] both obstruct the display, while [DisplayFeatureType.fold] is a crease in the display.

Folding [DisplayFeature]s like the [DisplayFeatureType.hinge] and [DisplayFeatureType.fold] also have a [DisplayFeature.state] which can be used to determine the posture the device is in. {@endtemplate}

When this changes, [PlatformDispatcher.onMetricsChanged] is called.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.
- [MediaQuery.of], a simpler mechanism to access this data.

### displayCornerRadii

```dart
DisplayCornerRadii? get displayCornerRadii
```

The radii of the display corners in physical pixels.

This is currently populated only on Android API 31+. On earlier Android versions, iOS, and other platforms, this value is `null`.

### render()

```dart
void render(Scene scene, {Size? size})
```

Updates the view's rendering on the GPU with the newly provided [Scene].

This function must be called within the scope of the [PlatformDispatcher.onBeginFrame] or [PlatformDispatcher.onDrawFrame] callbacks being invoked.

If this function is called a second time during a single [PlatformDispatcher.onBeginFrame]/[PlatformDispatcher.onDrawFrame] callback sequence or called outside the scope of those callbacks, the call will be ignored.

To record graphical operations, first create a [PictureRecorder], then construct a [Canvas], passing that [PictureRecorder] to its constructor. After issuing all the graphical operations, call the [PictureRecorder.endRecording] function on the [PictureRecorder] to obtain the final [Picture] that represents the issued graphical operations.

Next, create a [SceneBuilder], and add the [Picture] to it using [SceneBuilder.addPicture]. With the [SceneBuilder.build] method you can then obtain a [Scene] object, which you can display to the user via this [render] function.

If the view is configured with loose [physicalConstraints] (i.e. [ViewConstraints.isTight] returns false) a `size` satisfying those constraints must be provided. This method does not check that the provided `size` actually meets the constraints (this should be done in a higher level), but an illegal `size` may result in undefined rendering behavior. If no `size` is provided, [physicalSize] is used instead.

See also:

- [SchedulerBinding], the Flutter framework class which manages the scheduling of frames.
- [RendererBinding], the Flutter framework class which manages layout and painting.

### updateSemantics()

```dart
void updateSemantics(SemanticsUpdate update)
```

Change the retained semantics data about this [FlutterView].

[PlatformDispatcher.setSemanticsTreeEnabled] must be called with true before sending update through this method.

This function disposes the given update, which means the semantics update cannot be used further.

### toString()

```dart
String toString()
```

# SingletonFlutterWindow

```dart
class SingletonFlutterWindow extends FlutterView {}
```

Deprecated. Will be removed in a future version of Flutter.

This class is deprecated to prepare for Flutter's upcoming support for multiple views and eventually multiple windows.

This class has been split into two classes: [FlutterView] and [PlatformDispatcher]. A [FlutterView] gives an application access to view-specific functionality while the [PlatformDispatcher] contains platform-specific functionality that applies to all views.

This class backs the global [window] singleton, which is also deprecated. See the docs on [window] for migration options.

See also:

- [FlutterView], which gives an application access to view-specific functionality.
- [PlatformDispatcher], which gives an application access to platform-specific functionality.

### onMetricsChanged

```dart
VoidCallback? get onMetricsChanged
```

A callback that is invoked whenever the [devicePixelRatio], [physicalSize], [padding], [viewInsets], [PlatformDispatcher.views], or [systemGestureInsets] values change.

{@macro dart.ui.window.accessorForwardWarning}

When using the Flutter framework, the [MediaQuery] widget exposes much of these metrics. Using [MediaQuery.of] to obtain them allows the framework to automatically rebuild widgets that depend on them, without having to manage the [onMetricsChanged] callback.

See [PlatformDispatcher.onMetricsChanged] for more information.

### onMetricsChanged

```dart
set onMetricsChanged(VoidCallback? callback)
```

### locale

```dart
Locale get locale
```

The system-reported default locale of the device.

{@template dart.ui.window.accessorForwardWarning} Accessing this value returns the value contained in the [PlatformDispatcher] singleton, so instead of getting it from here, you should consider getting it from `WidgetsBinding.instance.platformDispatcher` instead (or, when `WidgetsBinding` isn't available, from [PlatformDispatcher.instance]). The reason this value forwards to the [PlatformDispatcher] is to provide convenience for applications that only use a single main window. {@endtemplate}

This establishes the language and formatting conventions that window should, if possible, use to render their user interface.

This is the first locale selected by the user and is the user's primary locale (the locale the device UI is displayed in)

This is equivalent to `locales.first` and will provide an empty non-null locale if the [locales] list has not been set or is empty.

### locales

```dart
List<Locale> get locales
```

The full system-reported supported locales of the device.

{@macro dart.ui.window.accessorForwardWarning}

This establishes the language and formatting conventions that window should, if possible, use to render their user interface.

The list is ordered in order of priority, with lower-indexed locales being preferred over higher-indexed ones. The first element is the primary [locale].

The [onLocaleChanged] callback is called whenever this value changes.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.

### computePlatformResolvedLocale()

```dart
Locale? computePlatformResolvedLocale(List<Locale> supportedLocales)
```

Performs the platform-native locale resolution.

Each platform may return different results.

If the platform fails to resolve a locale, then this will return null.

This method returns synchronously and is a direct call to platform specific APIs without invoking method channels.

### onLocaleChanged

```dart
VoidCallback? get onLocaleChanged
```

A callback that is invoked whenever [locale] changes value.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onLocaleChanged

```dart
set onLocaleChanged(VoidCallback? callback)
```

### initialLifecycleState

```dart
String get initialLifecycleState
```

The lifecycle state immediately after dart isolate initialization.

{@macro dart.ui.window.accessorForwardWarning}

This property will not be updated as the lifecycle changes.

It is used to initialize [SchedulerBinding.lifecycleState] at startup with any buffered lifecycle state events.

### textScaleFactor

```dart
double get textScaleFactor
```

The system-reported text scale.

{@macro dart.ui.window.accessorForwardWarning}

This establishes the text scaling factor to use when rendering text, according to the user's platform preferences.

The [onTextScaleFactorChanged] callback is called whenever this value changes.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.

### nativeSpellCheckServiceDefined

```dart
bool get nativeSpellCheckServiceDefined
```

Whether the spell check service is supported on the current platform.

{@macro dart.ui.window.accessorForwardWarning}

This option is used by [EditableTextState] to define its [SpellCheckConfiguration] when spell check is enabled, but no spell check service is specified.

### supportsShowingSystemContextMenu

```dart
bool get supportsShowingSystemContextMenu
```

Whether showing system context menu is supported on the current platform.

This option is used by [AdaptiveTextSelectionToolbar] to decide whether to show system context menu, or to fallback to the default Flutter context menu.

### brieflyShowPassword

```dart
bool get brieflyShowPassword
```

Whether briefly displaying the characters as you type in obscured text fields is enabled in system settings.

See also:

- [EditableText.obscureText], which when set to true hides the text in the text field.

### alwaysUse24HourFormat

```dart
bool get alwaysUse24HourFormat
```

The setting indicating whether time should always be shown in the 24-hour format.

{@macro dart.ui.window.accessorForwardWarning}

This option is used by [showTimePicker].

### onTextScaleFactorChanged

```dart
VoidCallback? get onTextScaleFactorChanged
```

A callback that is invoked whenever [textScaleFactor] changes value.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onTextScaleFactorChanged

```dart
set onTextScaleFactorChanged(VoidCallback? callback)
```

### platformBrightness

```dart
Brightness get platformBrightness
```

The setting indicating the current brightness mode of the host platform.

{@macro dart.ui.window.accessorForwardWarning}

If the platform has no preference, [platformBrightness] defaults to [Brightness.light].

### onPlatformBrightnessChanged

```dart
VoidCallback? get onPlatformBrightnessChanged
```

A callback that is invoked whenever [platformBrightness] changes value.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onPlatformBrightnessChanged

```dart
set onPlatformBrightnessChanged(VoidCallback? callback)
```

### systemFontFamily

```dart
String? get systemFontFamily
```

The setting indicating the system font of the host platform.

{@macro dart.ui.window.accessorForwardWarning}

### onSystemFontFamilyChanged

```dart
VoidCallback? get onSystemFontFamilyChanged
```

A callback that is invoked whenever [systemFontFamily] changes value.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onSystemFontFamilyChanged

```dart
set onSystemFontFamilyChanged(VoidCallback? callback)
```

### onBeginFrame

```dart
FrameCallback? get onBeginFrame
```

A callback that is invoked to notify the window that it is an appropriate time to provide a scene using the [SceneBuilder] API and the [render] method.

{@macro dart.ui.window.accessorForwardWarning}

When possible, this is driven by the hardware VSync signal. This is only called if [scheduleFrame] has been called since the last time this callback was invoked.

The [onDrawFrame] callback is invoked immediately after [onBeginFrame], after draining any microtasks (e.g. completions of any [Future]s) queued by the [onBeginFrame] handler.

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [SchedulerBinding], the Flutter framework class which manages the scheduling of frames.
- [RendererBinding], the Flutter framework class which manages layout and painting.

### onBeginFrame

```dart
set onBeginFrame(FrameCallback? callback)
```

### onDrawFrame

```dart
VoidCallback? get onDrawFrame
```

A callback that is invoked for each frame after [onBeginFrame] has completed and after the microtask queue has been drained.

{@macro dart.ui.window.accessorForwardWarning}

This can be used to implement a second phase of frame rendering that happens after any deferred work queued by the [onBeginFrame] phase.

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [SchedulerBinding], the Flutter framework class which manages the scheduling of frames.
- [RendererBinding], the Flutter framework class which manages layout and painting.

### onDrawFrame

```dart
set onDrawFrame(VoidCallback? callback)
```

### onReportTimings

```dart
TimingsCallback? get onReportTimings
```

A callback that is invoked to report the [FrameTiming] of recently rasterized frames.

{@macro dart.ui.window.accessorForwardWarning}

It's preferred to use [SchedulerBinding.addTimingsCallback] than to use [PlatformDispatcher.onReportTimings] directly because [SchedulerBinding.addTimingsCallback] allows multiple callbacks.

This can be used to see if the window has missed frames (through [FrameTiming.buildDuration] and [FrameTiming.rasterDuration]), or high latencies (through [FrameTiming.totalSpan]).

Unlike [Timeline], the timing information here is available in the release mode (additional to the profile and the debug mode). Hence this can be used to monitor the application's performance in the wild.

{@macro dart.ui.TimingsCallback.list}

If this is null, no additional work will be done. If this is not null, Flutter spends less than 0.1ms every 1 second to report the timings (measured on iPhone6S). The 0.1ms is about 0.6% of 16ms (frame budget for 60fps), or 0.01% CPU usage per second.

### onReportTimings

```dart
set onReportTimings(TimingsCallback? callback)
```

### onPointerDataPacket

```dart
PointerDataPacketCallback? get onPointerDataPacket
```

A callback that is invoked when pointer data is available.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [GestureBinding], the Flutter framework class which manages pointer events.

### onPointerDataPacket

```dart
set onPointerDataPacket(PointerDataPacketCallback? callback)
```

### onKeyData

```dart
KeyDataCallback? get onKeyData
```

A callback that is invoked when key data is available.

The framework invokes this callback in the same zone in which the callback was set.

### onKeyData

```dart
set onKeyData(KeyDataCallback? callback)
```

### defaultRouteName

```dart
String get defaultRouteName
```

The route or path that the embedder requested when the application was launched.

{@macro dart.ui.window.accessorForwardWarning}

This will be the string "`/`" if no particular route was requested.

## Android

On Android, the initial route can be set on the [initialRoute](/javadoc/io/flutter/embedding/android/FlutterActivity.NewEngineIntentBuilder.html#initialRoute-java.lang.String-) method of the [FlutterActivity](/javadoc/io/flutter/embedding/android/FlutterActivity.html)'s intent builder.

On a standalone engine, see https://docs.flutter.dev/development/add-to-app/android/add-flutter-screen#initial-route-with-a-cached-engine.

## iOS

On iOS, the initial route can be set with the [`FlutterViewController.setInitialRoute`](/ios-embedder/interface_flutter_view_controller.html#a7f269c2da73312f856d42611cc12a33f) initializer.

On a standalone engine, see https://docs.flutter.dev/development/add-to-app/ios/add-flutter-screen#route.

See also:

- [Navigator], a widget that handles routing.
- [SystemChannels.navigation], which handles subsequent navigation requests from the embedder.

### scheduleFrame()

```dart
void scheduleFrame()
```

Requests that, at the next appropriate opportunity, the [onBeginFrame] and [onDrawFrame] callbacks be invoked.

{@template dart.ui.window.functionForwardWarning} Calling this function forwards the call to the same function on the [PlatformDispatcher] singleton, so instead of calling it here, you should consider calling it on `WidgetsBinding.instance.platformDispatcher` instead (or, when `WidgetsBinding` isn't available, on [PlatformDispatcher.instance]). The reason this function forwards to the [PlatformDispatcher] is to provide convenience for applications that only use a single main window. {@endtemplate}

See also:

- [SchedulerBinding], the Flutter framework class which manages the scheduling of frames.

### semanticsEnabled

```dart
bool get semanticsEnabled
```

Whether the user has requested that [updateSemantics] be called when the semantic contents of window changes.

{@macro dart.ui.window.accessorForwardWarning}

The [onSemanticsEnabledChanged] callback is called whenever this value changes.

### onSemanticsEnabledChanged

```dart
VoidCallback? get onSemanticsEnabledChanged
```

A callback that is invoked when the value of [semanticsEnabled] changes.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

### onSemanticsEnabledChanged

```dart
set onSemanticsEnabledChanged(VoidCallback? callback)
```

### frameData

```dart
FrameData get frameData
```

The [FrameData] object for the current frame.

### onFrameDataChanged

```dart
VoidCallback? get onFrameDataChanged
```

A callback that is invoked when the window updates the [FrameData].

### onFrameDataChanged

```dart
set onFrameDataChanged(VoidCallback? callback)
```

### accessibilityFeatures

```dart
AccessibilityFeatures get accessibilityFeatures
```

Additional accessibility features that may be enabled by the platform.

### onAccessibilityFeaturesChanged

```dart
VoidCallback? get onAccessibilityFeaturesChanged
```

A callback that is invoked when the value of [accessibilityFeatures] changes.

{@macro dart.ui.window.accessorForwardWarning}

The framework invokes this callback in the same zone in which the callback was set.

### onAccessibilityFeaturesChanged

```dart
set onAccessibilityFeaturesChanged(VoidCallback? callback)
```

### sendPlatformMessage()

```dart
void sendPlatformMessage(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

Sends a message to a platform-specific plugin.

{@macro dart.ui.window.functionForwardWarning}

The `name` parameter determines which plugin receives the message. The `data` parameter contains the message payload and is typically UTF-8 encoded JSON but can be arbitrary data. If the plugin replies to the message, `callback` will be called with the response.

The framework invokes [callback] in the same zone in which this method was called.

### onPlatformMessage

```dart
PlatformMessageCallback? get onPlatformMessage
```

Deprecated. Migrate to [ChannelBuffers.setListener] instead.

Called whenever this window receives a message from a platform-specific plugin.

{@macro dart.ui.window.accessorForwardWarning}

The `name` parameter determines which plugin sent the message. The `data` parameter is the payload and is typically UTF-8 encoded JSON but can be arbitrary data.

Message handlers must call the function given in the `callback` parameter. If the handler does not need to respond, the handler should pass null to the callback.

The framework invokes this callback in the same zone in which the callback was set.

### onPlatformMessage

```dart
set onPlatformMessage(PlatformMessageCallback? callback)
```

### setIsolateDebugName()

```dart
void setIsolateDebugName(String name)
```

Set the debug name associated with this platform dispatcher's root isolate.

{@macro dart.ui.window.accessorForwardWarning}

Normally debug names are automatically generated from the Dart port, entry point, and source file. For example: `main.dart$main-1234`.

This can be combined with flutter tools `--isolate-filter` flag to debug specific root isolates. For example: `flutter attach --isolate-filter=[name]`. Note that this does not rename any child isolates of the root.

# AccessibilityFeatures

```dart
class AccessibilityFeatures {}
```

Additional accessibility features that may be enabled by the platform.

It is not possible to enable these settings from Flutter, instead they are used by the platform to indicate that additional accessibility features are enabled.

### accessibleNavigation

```dart
bool get accessibleNavigation
```

Whether there is a running accessibility service which is changing the interaction model of the device.

For example, TalkBack on Android and VoiceOver on iOS enable this flag.

### invertColors

```dart
bool get invertColors
```

The platform is inverting the colors of the application.

### disableAnimations

```dart
bool get disableAnimations
```

The platform is requesting that animations be disabled or simplified.

### boldText

```dart
bool get boldText
```

The platform is requesting that text be rendered at a bold font weight.

Only supported on iOS and Android API 31+.

### reduceMotion

```dart
bool get reduceMotion
```

The platform is requesting that certain animations be simplified and parallax effects removed.

Only supported on iOS.

### highContrast

```dart
bool get highContrast
```

The platform is requesting that UI be rendered with darker colors.

Only supported on iOS and Android API 34+.

### onOffSwitchLabels

```dart
bool get onOffSwitchLabels
```

The platform is requesting to show on/off labels inside switches.

Only supported on iOS.

### supportsAnnounce

```dart
bool get supportsAnnounce
```

Whether the platform supports accessibility announcement API, i.e. [SemanticsService.sendAnnouncement].

Some platforms do not support or discourage the use of announcement. Using [SemanticsService.sendAnnouncement] on those platform may be ignored. Consider using other way to convey message to the user. For example, Android discourages the uses of direct message announcement, and rather encourages using other semantic properties such as [SemanticsProperties.liveRegion] to convey message to the user.

Returns `false` on platforms where announcements are deprecated or unsupported by the underlying platform.

Returns `true` on platforms where such announcements are generally supported without discouragement. (iOS, web etc)

### autoPlayAnimatedImages

```dart
bool get autoPlayAnimatedImages
```

Whether the platform allows auto-playing animated images.

Only supported on iOS.

Always returns `true` on other platforms.

### autoPlayVideos

```dart
bool get autoPlayVideos
```

Whether the platform allows auto-playing videos.

Only supported on iOS.

Always returns `true` on other platforms.

### deterministicCursor

```dart
bool get deterministicCursor
```

The platform is requesting to show deterministic (non-blinking) cursor in editable text fields.

Only supported on iOS.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# Brightness

```dart
enum Brightness {}
```

Describes the contrast of a theme or color palette.

The color is dark and will require a light text color to achieve readable contrast.

For example, the color might be dark grey, requiring white text.

The color is light and will require a dark text color to achieve readable contrast.

For example, the color might be bright white, requiring black text.

# window

```dart
SingletonFlutterWindow window
```

Deprecated. Will be removed in a future version of Flutter.

This global property is deprecated to prepare for Flutter's upcoming support for multiple views and multiple windows.

It represents the main view for applications where there is only one view, such as applications designed for single-display mobile devices. If the embedder supports multiple views, it points to the first view created which is assumed to be the main view. It throws if no view has been created yet or if the first view has been removed again.

The following options exists to migrate code that relies on accessing this deprecated property:

If a [BuildContext] is available, consider looking up the current [FlutterView] associated with that context via [View.of]. It gives access to the same functionality as this deprecated property. However, the platform-specific functionality has moved to the [PlatformDispatcher], which may be accessed from the view returned by [View.of] via [FlutterView.platformDispatcher]. Using [View.of] with a [BuildContext] is the preferred option to migrate away from this deprecated [window] property.

If no context is available to look up a [FlutterView], the [PlatformDispatcher] can be used directly for platform-specific functionality. It also maintains a list of all available [FlutterView]s in [PlatformDispatcher.views] to access view-specific functionality without a context. If possible, consider accessing the [PlatformDispatcher] via the binding (e.g. `WidgetsBinding.instance.platformDispatcher`) instead of the static singleton [PlatformDispatcher.instance]. See [PlatformDispatcher.instance] for more information about why this is preferred.

See also:

- [FlutterView], which gives an application access to view-specific functionality.
- [PlatformDispatcher], which gives an application access to platform-specific functionality.
- [PlatformDispatcher.views], for a list of all available views.

# FrameData

```dart
class FrameData {}
```

Additional data available on each flutter frame.

See also:

- [Window.frameData] and [PlatformDispatcher.frameData], which expose the frame data for the current frame.
- [PlatformDispatcher.onFrameDataChanged], which notifies listeners when a window's frame data has changed.

### frameNumber

```dart
int frameNumber
```

The number of the current frame.

This number monotonically increases, but doesn't necessarily start at a particular value.

If not provided, defaults to -1.

# GestureSettings

```dart
class GestureSettings {}
```

Platform specific configuration for gesture behavior, such as touch slop.

These settings are provided via [FlutterView.gestureSettings] to each view, and should be favored for configuring gesture behavior over the framework constants.

A `null` field indicates that the platform or view does not have a preference and the fallback constants should be used instead.

### GestureSettings()

```dart
GestureSettings({double? physicalTouchSlop, double? physicalDoubleTapSlop})
```

Create a new [GestureSettings] value.

Consider using [GestureSettings.copyWith] on an existing settings object to ensure that newly added fields are correctly set.

### physicalTouchSlop

```dart
double? physicalTouchSlop
```

The number of physical pixels a pointer is allowed to drift before it is considered an intentional movement.

If `null`, the framework's default touch slop configuration should be used instead.

### physicalDoubleTapSlop

```dart
double? physicalDoubleTapSlop
```

The number of physical pixels that the first and second tap of a double tap can drift apart to still be recognized as a double tap.

If `null`, the framework's default double tap slop configuration should be used instead.

### copyWith()

```dart
GestureSettings copyWith({double? physicalTouchSlop, double? physicalDoubleTapSlop})
```

Create a new [GestureSettings] object from an existing value, overwriting all of the provided fields.

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
