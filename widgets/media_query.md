@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/semantics.dart'; @docImport 'package:flutter/services.dart';

@docImport 'app.dart'; @docImport 'display_feature_sub_screen.dart'; @docImport 'overlay.dart'; @docImport 'safe_area.dart'; @docImport 'system_context_menu.dart'; @docImport 'view.dart';

# Orientation

```dart
enum Orientation {}
```

Whether in portrait or landscape.

Taller than wide.

Wider than tall.

# MediaQueryData

```dart
class MediaQueryData {}
```

Information about a piece of media (e.g., a window).

For example, the [MediaQueryData.size] property contains the width and height of the current window.

To obtain individual attributes in a [MediaQueryData], prefer to use the attribute-specific functions of [MediaQuery] over obtaining the entire [MediaQueryData] and accessing its members. {@macro flutter.widgets.media_query.MediaQuery.useSpecific}

To obtain the entire current [MediaQueryData] for a given [BuildContext], use the [MediaQuery.of] function. This can be useful if you are going to use [copyWith] to replace the [MediaQueryData] with one with an updated property.

## Insets and Padding

![A diagram of padding, viewInsets, and viewPadding in correlation with each other](https://flutter.github.io/assets-for-api-docs/assets/widgets/media_query.png)

This diagram illustrates how [padding] relates to [viewPadding] and [viewInsets], shown here in its simplest configuration, as the difference between the two. In cases when the viewInsets exceed the viewPadding, like when a software keyboard is shown below, padding goes to zero rather than a negative value. Therefore, padding is calculated by taking `max(0.0, viewPadding - viewInsets)`.

{@animation 300 300 https://flutter.github.io/assets-for-api-docs/assets/widgets/window_padding.mp4}

In this diagram, the black areas represent system UI that the app cannot draw over. The red area represents view padding that the application may not be able to detect gestures in and may not want to draw in. The grey area represents the system keyboard, which can cover over the bottom view padding when visible.

MediaQueryData includes three [EdgeInsets] values: [padding], [viewPadding], and [viewInsets]. These values reflect the configuration of the device and are used and optionally consumed by widgets that position content within these insets. The padding value defines areas that might not be completely visible, like the display "notch" on the iPhone X. The viewInsets value defines areas that aren't visible at all, typically because they're obscured by the device's keyboard. Similar to viewInsets, viewPadding does not differentiate padding in areas that may be obscured. For example, by using the viewPadding property, padding would defer to the iPhone "safe area" regardless of whether a keyboard is showing.

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

The viewInsets and viewPadding are independent values, they're measured from the edges of the MediaQuery widget's bounds. Together they inform the [padding] property. The bounds of the top level MediaQuery created by [WidgetsApp] are the same as the window that contains the app.

Widgets whose layouts consume space defined by [viewInsets], [viewPadding], or [padding] should enclose their children in secondary MediaQuery widgets that reduce those properties by the same amount. The [removePadding], [removeViewPadding], and [removeViewInsets] methods are useful for this.

See also:

- [Scaffold], [SafeArea], [CupertinoTabScaffold], and [CupertinoPageScaffold], all of which are informed by [padding], [viewPadding], and [viewInsets].

### MediaQueryData()

```dart
MediaQueryData({Size size = Size.zero, double devicePixelRatio = 1.0, double textScaleFactor = 1.0, TextScaler textScaler = _kUnspecifiedTextScaler, Brightness platformBrightness = Brightness.light, EdgeInsets padding = EdgeInsets.zero, EdgeInsets viewInsets = EdgeInsets.zero, EdgeInsets systemGestureInsets = EdgeInsets.zero, EdgeInsets viewPadding = EdgeInsets.zero, bool alwaysUse24HourFormat = false, bool accessibleNavigation = false, bool invertColors = false, bool highContrast = false, bool onOffSwitchLabels = false, bool disableAnimations = false, bool boldText = false, bool supportsAnnounce = false, NavigationMode navigationMode = NavigationMode.traditional, DeviceGestureSettings gestureSettings = const DeviceGestureSettings(touchSlop: kTouchSlop), List<ui.DisplayFeature> displayFeatures = const <ui.DisplayFeature>[], bool supportsShowingSystemContextMenu = false, double? lineHeightScaleFactorOverride, double? letterSpacingOverride, double? wordSpacingOverride, double? paragraphSpacingOverride, BorderRadius? displayCornerRadii})
```

Creates data for a media query with explicit values.

In a typical application, calling this constructor directly is rarely needed. Consider using [MediaQueryData.fromView] to create data based on a [dart:ui.FlutterView], or [MediaQueryData.copyWith] to create a new copy of [MediaQueryData] with updated properties from a base [MediaQueryData].

### MediaQueryData.fromWindow()

```dart
MediaQueryData.fromWindow(ui.FlutterView window)
```

Deprecated. Use [MediaQueryData.fromView] instead.

This constructor was operating on a single window assumption. In preparation for Flutter's upcoming multi-window support, it has been deprecated.

### MediaQueryData.fromView()

```dart
MediaQueryData.fromView(ui.FlutterView view, {MediaQueryData? platformData})
```

Creates data for a [MediaQuery] based on the given `view`.

If provided, the `platformData` is used to fill in the platform-specific aspects of the newly created [MediaQueryData]. If `platformData` is null, the `view`'s [PlatformDispatcher] is consulted to construct the platform-specific data.

Data which is exposed directly on the [FlutterView] is considered view-specific. Data which is only exposed via the [FlutterView.platformDispatcher] property is considered platform-specific.

Callers of this method should ensure that they also register for notifications so that the [MediaQueryData] can be updated when any data used to construct it changes. Notifications to consider are:

- [WidgetsBindingObserver.didChangeMetrics] or [dart:ui.PlatformDispatcher.onMetricsChanged],
- [WidgetsBindingObserver.didChangeAccessibilityFeatures] or [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged],
- [WidgetsBindingObserver.didChangeTextScaleFactor] or [dart:ui.PlatformDispatcher.onTextScaleFactorChanged],
- [WidgetsBindingObserver.didChangePlatformBrightness] or [dart:ui.PlatformDispatcher.onPlatformBrightnessChanged].

The last three notifications are only relevant if no `platformData` is provided. If `platformData` is provided, callers should ensure to call this method again when it changes to keep the constructed [MediaQueryData] updated.

In general, [MediaQuery.of], and its associated "...Of" methods, are the appropriate way to obtain [MediaQueryData] from a widget. This `fromView` constructor is primarily for use in the implementation of the framework itself.

See also:

- [MediaQuery.fromView], which constructs [MediaQueryData] from a provided [FlutterView], makes it available to descendant widgets, and sets up the appropriate notification listeners to keep the data updated.

### size

```dart
Size size
```

The size of the media in logical pixels (e.g, the size of the screen).

Logical pixels are roughly the same visual size across devices. Physical pixels are the size of the actual hardware pixels on the device. The number of physical pixels per logical pixel is described by the [devicePixelRatio].

Prefer using [MediaQuery.sizeOf] over [MediaQuery.of]`.size` to get the size, since the former will only notify of changes in [size], while the latter will notify for all [MediaQueryData] changes.

For widgets drawn in an [Overlay], do not assume that the size of the [Overlay] is the size of the [MediaQuery]'s size. Nested overlays can have different sizes.

## Troubleshooting

It is considered bad practice to cache and later use the size returned by `MediaQuery.sizeOf(context)`. It will make the application non-responsive and might lead to unexpected behaviors.

For instance, during startup, especially in release mode, the first returned size might be [Size.zero]. The size will be updated when the native platform reports the actual resolution. Using [MediaQuery.sizeOf] will ensure that when the size changes, any widgets depending on the size are automatically rebuilt.

See the article on [Creating responsive and adaptive apps](https://docs.flutter.dev/ui/adaptive-responsive) for an introduction.

See also:

- [FlutterView.physicalSize], which returns the size of the view in physical pixels.
- [FlutterView.display], which returns reports display information like size, and refresh rate.
- [MediaQuery.sizeOf], a method to find and depend on the size defined for a [BuildContext].

### devicePixelRatio

```dart
double devicePixelRatio
```

The number of device pixels for each logical pixel of the encompassing [FlutterView]. This number might not be a power of two. Indeed, it might not even be an integer. For example, the Nexus 6 has a device pixel ratio of 3.5.

This property is typically only informational. Overriding this property does not rescale the app as the Flutter framework or its rendering pipeline usually does not read this value.

### textScaleFactor

```dart
double get textScaleFactor
```

Deprecated. Will be removed in a future version of Flutter. Use [textScaler] instead.

The number of font pixels for each logical pixel.

For example, if the text scale factor is 1.5, text will be 50% larger than the specified font size.

See also:

- [MediaQuery.textScaleFactorOf], a method to find and depend on the textScaleFactor defined for a [BuildContext].

### textScaler

```dart
TextScaler get textScaler
```

The font scaling strategy to use for laying out textual contents.

If this [MediaQueryData] is created by the [MediaQueryData.fromView] constructor, this property reflects the platform's preferred text scaling strategy, and may change as the user changes the scaling factor in the operating system's accessibility settings.

See also:

- [MediaQuery.textScalerOf], a method to find and depend on the [textScaler] defined for a [BuildContext].
- [TextPainter], a class that lays out and paints text.

### platformBrightness

```dart
Brightness platformBrightness
```

The current brightness mode of the host platform.

For example, starting in Android Pie, battery saver mode asks all apps to render in a "dark mode".

Not all platforms necessarily support a concept of brightness mode. Those platforms will report [Brightness.light] in this property.

See also:

- [MediaQuery.platformBrightnessOf], a method to find and depend on the platformBrightness defined for a [BuildContext].

### viewInsets

```dart
EdgeInsets viewInsets
```

The parts of the display that are completely obscured by system UI, typically by the device's keyboard.

When a mobile device's keyboard is visible `viewInsets.bottom` corresponds to the top of the keyboard.

This value is independent of the [padding] and [viewPadding]. viewPadding is measured from the edges of the [MediaQuery] widget's bounds. Padding is calculated based on the viewPadding and viewInsets. The bounds of the top level MediaQuery created by [WidgetsApp] are the same as the window (often the mobile device screen) that contains the app.

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

See also:

- [FlutterView], which provides some additional detail about this property and how it relates to [padding] and [viewPadding].

### padding

```dart
EdgeInsets padding
```

The parts of the display that are partially obscured by system UI, typically by the hardware display "notches" or the system status bar.

If you consumed this padding (e.g. by building a widget that envelops or accounts for this padding in its layout in such a way that children are no longer exposed to this padding), you should remove this padding for subsequent descendants in the widget tree by inserting a new [MediaQuery] widget using the [MediaQuery.removePadding] factory.

Padding is derived from the values of [viewInsets] and [viewPadding].

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

See also:

- [FlutterView], which provides some additional detail about this property and how it relates to [viewInsets] and [viewPadding].
- [SafeArea], a widget that consumes this padding with a [Padding] widget and automatically removes it from the [MediaQuery] for its child.

### viewPadding

```dart
EdgeInsets viewPadding
```

The parts of the display that are partially obscured by system UI, typically by the hardware display "notches" or the system status bar.

This value remains the same regardless of whether the system is reporting other obstructions in the same physical area of the screen. For example, a software keyboard on the bottom of the screen that may cover and consume the same area that requires bottom padding will not affect this value.

This value is independent of the [padding] and [viewInsets]: their values are measured from the edges of the [MediaQuery] widget's bounds. The bounds of the top level MediaQuery created by [WidgetsApp] are the same as the window that contains the app. On mobile devices, this will typically be the full screen.

{@youtube 560 315 https://www.youtube.com/watch?v=ceCo8U0XHqw}

See also:

- [FlutterView], which provides some additional detail about this property and how it relates to [padding] and [viewInsets].

### systemGestureInsets

```dart
EdgeInsets systemGestureInsets
```

The areas along the edges of the display where the system consumes certain input events and blocks delivery of those events to the app.

Starting with Android Q, simple swipe gestures that start within the [systemGestureInsets] areas are used by the system for page navigation and may not be delivered to the app. Taps and swipe gestures that begin with a long-press are delivered to the app, but simple press-drag-release swipe gestures which begin within the area defined by [systemGestureInsets] may not be.

Apps should avoid locating gesture detectors within the system gesture insets area. Apps should feel free to put visual elements within this area.

This property is currently only expected to be set to a non-default value on Android starting with version Q.

{@tool dartpad} For apps that might be deployed on Android Q devices with full gesture navigation enabled, use [systemGestureInsets] with [Padding] to avoid having the left and right edges of the [Slider] from appearing within the area reserved for system gesture navigation.

By default, [Slider]s expand to fill the available width. So, we pad the left and right sides.

** See code in examples/api/lib/widgets/media_query/media_query_data.system_gesture_insets.0.dart ** {@end-tool}

### alwaysUse24HourFormat

```dart
bool alwaysUse24HourFormat
```

Whether to use 24-hour format when formatting time.

The behavior of this flag is different across platforms:

- On Android this flag is reported directly from the user settings called "Use 24-hour format". It applies to any locale used by the application, whether it is the system-wide locale, or the custom locale set by the application.
- On iOS this flag is set to true when the user setting called "24-Hour Time" is set or the system-wide locale's default uses 24-hour formatting.
- On macOS this flag reflects the current system locale's time format, which incorporates the "24-Hour Time" preference in System Settings. As on iOS, this only takes effect for the system locale; a custom locale passed to the application will ignore the 24-hour preference.
- On Windows this flag is derived from the user's "Short time" format in the Region settings; it is true when the configured format uses a 24-hour pattern.
- On Linux this flag reflects the desktop environment's clock-format setting where available (for example, `org.gnome.desktop.interface.clock-format` on GNOME). On desktops that do not expose such a setting, it defaults to true (24-hour).
- On Web this flag is always false. The Flutter web engine does not currently populate it from the browser's locale settings, even though the browser exposes a preferred hour cycle via `Intl.DateTimeFormat.resolvedOptions().hourCycle`.

### accessibleNavigation

```dart
bool accessibleNavigation
```

Whether the user is using an accessibility service like TalkBack or VoiceOver to interact with the application.

When this setting is true, features such as timeouts should be disabled or have minimum durations increased.

See also:

- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### invertColors

```dart
bool invertColors
```

Whether the operating system is currently inverting the colors of the platform.

This flag indicates that the underlying OS is already performing a global color inversion at the screen level. It does not mean the Flutter framework will automatically invert its own layout painting.

Instead, this flag allows the application to react to the inversion. For example, by selectively re-inverting images, maps, or video playback so that they display with natural colors instead of looking like a film negative.

This flag is currently only updated on iOS devices.

See also:

- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### highContrast

```dart
bool highContrast
```

Whether the platform is requesting a high contrast between foreground and background content.

On iOS, this corresponds to the "Increase Contrast" setting in Settings -> Accessibility. On Android, this corresponds to the "High contrast text" or similar accessibility settings.

This flag indicates that the operating system is already performing high-contrast adjustments or expects the application to adjust its color palette to meet higher accessibility standards.

Changing this value manually in a [MediaQuery] override will not automatically trigger a theme change in [MaterialApp]. Instead, [MaterialApp] uses this value to decide whether to use [MaterialApp.highContrastTheme] or [MaterialApp.highContrastDarkTheme].

This flag is currently only updated on iOS devices running iOS 13+ and Android devices running API 34+.

### onOffSwitchLabels

```dart
bool onOffSwitchLabels
```

Whether the user requested to show on/off labels inside switches on iOS, via Settings -> Accessibility -> Display & Text Size -> On/Off Labels.

See also:

- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### disableAnimations

```dart
bool disableAnimations
```

Whether the platform is requesting that animations be disabled or reduced as much as possible.

This corresponds to Android's "Remove animations" accessibility setting.

On iOS, reduced motion is exposed separately via [dart:ui.AccessibilityFeatures.reduceMotion] and does not set this flag.

This value is read directly from the engine via [SemanticsBinding.disableAnimations]. As a result, it is used by framework-level animation APIs such as [AnimationController] and cannot be overridden using [MediaQuery].

Manually overriding this value in a [MediaQuery] widget will not affect framework animations (for example those driven by [AnimationController]). However, it can still be useful for testing or for custom widgets that explicitly read [MediaQueryData.disableAnimations].

When implementing custom explicit animations, you should check this property and adjust behavior accordingly (for example, by reducing duration or skipping non-essential animations when it is true).

See also:

- [AnimationController], which adjusts its playback behavior based on this setting.
- [AnimationBehavior], which defines how animations behave when this setting is active.
- [dart:ui.AccessibilityFeatures.disableAnimations], the underlying primitive flag provided by the platform.
- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### boldText

```dart
bool boldText
```

Whether the platform is requesting that text be drawn with a bold font weight.

See also:

- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### supportsAnnounce

```dart
bool supportsAnnounce
```

Whether accessibility announcements (like [SemanticsService.sendAnnouncement]) are supported on the current platform.

Returns `false` on platforms where announcements are deprecated or unsupported by the underlying platform.

Returns `true` on platforms where such announcements are generally supported without discouragement. (iOS, web etc)

See also:

- [dart:ui.PlatformDispatcher.accessibilityFeatures], where the setting originates.

### navigationMode

```dart
NavigationMode navigationMode
```

Describes the navigation mode requested by the platform.

Some user interfaces are better navigated using a directional pad (DPAD) or arrow keys, and for those interfaces, some widgets need to handle these directional events differently. In order to know when to do that, these widgets will look for the navigation mode in effect for their context.

For instance, in a television interface, [NavigationMode.directional] should be set, so that directional navigation is used to navigate away from a text field using the DPAD. In contrast, on a regular desktop application with the [navigationMode] set to [NavigationMode.traditional], the arrow keys are used to move the cursor instead of navigating away.

The [NavigationMode] values indicate the type of navigation to be used in a widget subtree for those widgets sensitive to it.

### gestureSettings

```dart
DeviceGestureSettings gestureSettings
```

The gesture settings for the view this media query is derived from.

This contains platform specific configuration for gesture behavior, such as touch slop. These settings should be favored for configuring gesture behavior over the framework constants.

### displayFeatures

```dart
List<ui.DisplayFeature> displayFeatures
```

{@macro dart.ui.ViewConfiguration.displayFeatures}

See also:

- [dart:ui.DisplayFeatureType], which lists the different types of display features and explains the differences between them.
- [dart:ui.DisplayFeatureState], which lists the possible states for folding features ([dart:ui.DisplayFeatureType.fold] and [dart:ui.DisplayFeatureType.hinge]).

### supportsShowingSystemContextMenu

```dart
bool supportsShowingSystemContextMenu
```

Whether showing the system context menu is supported.

For example, on iOS 16.0 and above, the system text selection context menu may be shown instead of the Flutter-drawn context menu in order to avoid the iOS clipboard access notification when the "Paste" button is pressed.

See also:

- [SystemContextMenuController] and [SystemContextMenu], which may be used to show the system context menu when this flag indicates it's supported.

### lineHeightScaleFactorOverride

```dart
double? lineHeightScaleFactorOverride
```

Overrides the height of the text, as a multiple of the font size.

Returns `null` when the platform has not set an override for text height.

See also:

- [Text], [SelectableText], and [EditableText], all of whose [TextStyle.height] and [StrutStyle.height] are overridden by [lineHeightScaleFactorOverride].

### letterSpacingOverride

```dart
double? letterSpacingOverride
```

Overrides the amount of space (in logical pixels) to add between each letter in a piece of text.

A negative value can be used to bring the letters closer.

Returns `null` when the platform has not set an override for text letter spacing.

See also:

- [Text], [SelectableText], and [EditableText], all of whose [TextStyle.letterSpacing] is overridden by [letterSpacingOverride].

### wordSpacingOverride

```dart
double? wordSpacingOverride
```

Overrides the amount of space (in logical pixels) to add at each sequence of white-space (i.e. between each word) in a piece of text.

A negative value can be used to bring the words closer.

Returns `null` when the platform has not set an override for text word spacing.

See also:

- [Text], [SelectableText], and [EditableText], all of whose [TextStyle.wordSpacing] is overridden by [wordSpacingOverride].

### paragraphSpacingOverride

```dart
double? paragraphSpacingOverride
```

The amount of space (in logical pixels) to add following each paragraph in a piece of text.

Returns `null` when the platform has not set an override for text paragraph spacing.

### displayCornerRadii

```dart
BorderRadius? displayCornerRadii
```

The radii of the display corners in logical pixels.

This is currently populated only on Android API 31+. On earlier Android versions, iOS, and other platforms, this value is `null`.

See also:

- [FlutterView.displayCornerRadii], which returns the display corner radii in physical pixels.

### orientation

```dart
Orientation get orientation
```

The orientation of the media (e.g., whether the device is in landscape or portrait mode).

### copyWith()

```dart
MediaQueryData copyWith({Size? size, double? devicePixelRatio, double? textScaleFactor, TextScaler? textScaler, Brightness? platformBrightness, EdgeInsets? padding, EdgeInsets? viewPadding, EdgeInsets? viewInsets, EdgeInsets? systemGestureInsets, bool? alwaysUse24HourFormat, bool? highContrast, bool? onOffSwitchLabels, bool? disableAnimations, bool? invertColors, bool? accessibleNavigation, bool? boldText, bool? supportsAnnounce, NavigationMode? navigationMode, DeviceGestureSettings? gestureSettings, List<ui.DisplayFeature>? displayFeatures, bool? supportsShowingSystemContextMenu})
```

Creates a copy of this media query data but with the given fields replaced with the new values.

The `textScaler` parameter and `textScaleFactor` parameter must not be both specified.

### applyTextStyleOverrides()

```dart
MediaQueryData applyTextStyleOverrides({required double? lineHeightScaleFactorOverride, required double? letterSpacingOverride, required double? wordSpacingOverride, required double? paragraphSpacingOverride})
```

Creates a copy of this media query data but with the `lineHeightScaleFactorOverride`, `letterSpacingOverride`, `wordSpacingOverride`, and `paragraphSpacingOverride` replaced with the given values.

If an argument is null (the default), then this [MediaQueryData] is returned with the corresponding override set to null.

See also:

- [MediaQuery.applyTextStyleOverrides], which uses this method to apply text style overrides to the ambient [MediaQuery].

### applyDisplayCornerRadii()

```dart
MediaQueryData applyDisplayCornerRadii(BorderRadius? displayCornerRadii)
```

Creates a copy of this media query data but with the `displayCornerRadii` replaced with the given value.

If the argument is null (the default), then this [MediaQueryData] is returned with the `displayCornerRadii` set to null.

### removePadding()

```dart
MediaQueryData removePadding({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

Creates a copy of this media query data but with the given [padding]s replaced with zero.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then this [MediaQueryData] is returned unmodified.

See also:

- [MediaQuery.removePadding], which uses this method to remove [padding] from the ambient [MediaQuery].
- [SafeArea], which both removes the padding from the [MediaQuery] and adds a [Padding] widget.
- [removeViewInsets], the same thing but for [viewInsets].
- [removeViewPadding], the same thing but for [viewPadding].

### removeViewInsets()

```dart
MediaQueryData removeViewInsets({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

Creates a copy of this media query data but with the given [viewInsets] replaced with zero.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then this [MediaQueryData] is returned unmodified.

See also:

- [MediaQuery.removeViewInsets], which uses this method to remove [viewInsets] from the ambient [MediaQuery].
- [removePadding], the same thing but for [padding].
- [removeViewPadding], the same thing but for [viewPadding].

### removeViewPadding()

```dart
MediaQueryData removeViewPadding({bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false})
```

Creates a copy of this media query data but with the given [viewPadding] replaced with zero.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then this [MediaQueryData] is returned unmodified.

See also:

- [MediaQuery.removeViewPadding], which uses this method to remove [viewPadding] from the ambient [MediaQuery].
- [removePadding], the same thing but for [padding].
- [removeViewInsets], the same thing but for [viewInsets].

### removeDisplayFeatures()

```dart
MediaQueryData removeDisplayFeatures(Rect subScreen)
```

Creates a copy of this media query data by removing [displayFeatures] that are completely outside the given sub-screen and adjusting the [padding], [viewInsets] and [viewPadding] to be zero on the sides that are not included in the sub-screen.

Returns unmodified [MediaQueryData] if the sub-screen coincides with the available screen space.

Asserts in debug mode, if the given sub-screen is outside the available screen space.

See also:

- [DisplayFeatureSubScreen], which removes the display features that split the screen, from the [MediaQuery] and adds a [Padding] widget to position the child to match the selected sub-screen.

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

Establishes a subtree in which media queries resolve to the given data.

For example, to learn the size of the current view (e.g., the [FlutterView] containing your app), you can use [MediaQuery.sizeOf]: `MediaQuery.sizeOf(context)`.

Querying the current media using specific methods (for example, [MediaQuery.sizeOf] or [MediaQuery.paddingOf]) will cause your widget to rebuild automatically whenever that specific property changes.

{@template flutter.widgets.media_query.MediaQuery.useSpecific} Querying using [MediaQuery.of] will cause your widget to rebuild automatically whenever _any_ field of the [MediaQueryData] changes (e.g., if the user rotates their device). Therefore, unless you are concerned with the entire [MediaQueryData] object changing, prefer using the specific methods (for example: [MediaQuery.sizeOf] and [MediaQuery.paddingOf]), as it will rebuild more efficiently.

If no [MediaQuery] is in scope then [MediaQuery.of] and the "...Of" methods similar to [MediaQuery.sizeOf] will throw an exception. Alternatively, the "maybe-" variant methods (such as [MediaQuery.maybeOf] and [MediaQuery.maybeSizeOf]) can be used, which return null, instead of throwing, when no [MediaQuery] is in scope. {@endtemplate}

{@youtube 560 315 https://www.youtube.com/watch?v=A3WrA4zAaPw}

See also:

- [WidgetsApp] and [MaterialApp], which introduce a [MediaQuery] and keep it up to date with the current screen metrics as they change.
- [MediaQueryData], the data structure that represents the metrics.

### MediaQuery()

```dart
MediaQuery({dynamic key, required MediaQueryData data, required Widget child})
```

Creates a widget that provides [MediaQueryData] to its descendants.

### MediaQuery.removePadding()

```dart
MediaQuery.removePadding({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

Creates a new [MediaQuery] that inherits from the ambient [MediaQuery] from the given context, but removes the specified padding.

This should be inserted into the widget tree when the [MediaQuery] padding is consumed by a widget in such a way that the padding is no longer exposed to the widget's descendants or siblings.

The [context] argument must have a [MediaQuery] in scope.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then the returned [MediaQuery] reuses the ambient [MediaQueryData] unmodified, which is not particularly useful.

See also:

- [SafeArea], which both removes the padding from the [MediaQuery] and adds a [Padding] widget.
- [MediaQueryData.padding], the affected property of the [MediaQueryData].
- [MediaQuery.removeViewInsets], the same thing but for [MediaQueryData.viewInsets].
- [MediaQuery.removeViewPadding], the same thing but for [MediaQueryData.viewPadding].

### MediaQuery.removeViewInsets()

```dart
MediaQuery.removeViewInsets({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

Creates a new [MediaQuery] that inherits from the ambient [MediaQuery] from the given context, but removes the specified view insets.

This should be inserted into the widget tree when the [MediaQuery] view insets are consumed by a widget in such a way that the view insets are no longer exposed to the widget's descendants or siblings.

The [context] argument must have a [MediaQuery] in scope.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then the returned [MediaQuery] reuses the ambient [MediaQueryData] unmodified, which is not particularly useful.

See also:

- [MediaQueryData.viewInsets], the affected property of the [MediaQueryData].
- [MediaQuery.removePadding], the same thing but for [MediaQueryData.padding].
- [MediaQuery.removeViewPadding], the same thing but for [MediaQueryData.viewPadding].

### MediaQuery.removeViewPadding()

```dart
MediaQuery.removeViewPadding({dynamic key, required BuildContext context, bool removeLeft = false, bool removeTop = false, bool removeRight = false, bool removeBottom = false, required Widget child})
```

Creates a new [MediaQuery] that inherits from the ambient [MediaQuery] from the given context, but removes the specified view padding.

This should be inserted into the widget tree when the [MediaQuery] view padding is consumed by a widget in such a way that the view padding is no longer exposed to the widget's descendants or siblings.

The [context] argument must have a [MediaQuery] in scope.

If all four of the `removeLeft`, `removeTop`, `removeRight`, and `removeBottom` arguments are false (the default), then the returned [MediaQuery] reuses the ambient [MediaQueryData] unmodified, which is not particularly useful.

See also:

- [MediaQueryData.viewPadding], the affected property of the [MediaQueryData].
- [MediaQuery.removePadding], the same thing but for [MediaQueryData.padding].
- [MediaQuery.removeViewInsets], the same thing but for [MediaQueryData.viewInsets].

### applyTextStyleOverrides()

```dart
Widget applyTextStyleOverrides({Key? key, required double? lineHeightScaleFactorOverride, required double? letterSpacingOverride, required double? wordSpacingOverride, required double? paragraphSpacingOverride, required Widget child})
```

Wraps the `child` in a [MediaQuery] with its [MediaQueryData.lineHeightScaleFactorOverride], [MediaQueryData.letterSpacingOverride], [MediaQueryData.wordSpacingOverride], [MediaQueryData.paragraphSpacingOverride] set to the specified values.

If a text style override argument is null (the default), then the corresponding override in the updated [MediaQueryData] is set to null.

The returned widget must be inserted in a widget tree below an existing [MediaQuery] widget.

See also:

- [MediaQueryData.lineHeightScaleFactorOverride], [MediaQueryData.letterSpacingOverride], [MediaQueryData.wordSpacingOverride], [MediaQueryData.paragraphSpacingOverride], the affected properties of the [MediaQueryData].

### fromWindow()

```dart
Widget fromWindow({Key? key, required Widget child})
```

Deprecated. Use [MediaQuery.fromView] instead.

This constructor was operating on a single window assumption. In preparation for Flutter's upcoming multi-window support, it has been deprecated.

Replaced by [MediaQuery.fromView], which requires specifying the [FlutterView] the [MediaQuery] is constructed for. The [FlutterView] can, for example, be obtained from the context via [View.of] or from [PlatformDispatcher.views].

### fromView()

```dart
Widget fromView({Key? key, required FlutterView view, required Widget child})
```

Wraps the [child] in a [MediaQuery] which is built using data from the provided [view].

The [MediaQuery] is constructed using the platform-specific data of the surrounding [MediaQuery] and the view-specific data of the provided [view]. If no surrounding [MediaQuery] exists, the platform-specific data is generated from the [PlatformDispatcher] associated with the provided [view]. Any information that's exposed via the [PlatformDispatcher] is considered platform-specific. Data exposed directly on the [FlutterView] (excluding its [FlutterView.platformDispatcher] property) is considered view-specific.

The injected [MediaQuery] automatically updates when any of the data used to construct it changes.

### withNoTextScaling()

```dart
Widget withNoTextScaling({Key? key, required Widget child})
```

Wraps the `child` in a [MediaQuery] with its [MediaQueryData.textScaler] set to [TextScaler.noScaling].

The returned widget must be inserted in a widget tree below an existing [MediaQuery] widget.

This can be used to prevent, for example, icon fonts from scaling as the user adjusts the platform's text scaling value.

### withClampedTextScaling()

```dart
Widget withClampedTextScaling({Key? key, double minScaleFactor = 0.0, double maxScaleFactor = double.infinity, required Widget child})
```

Wraps the `child` in a [MediaQuery] and applies [TextScaler.clamp] on the current [MediaQueryData.textScaler].

The returned widget must be inserted in a widget tree below an existing [MediaQuery] widget.

This is a convenience function to restrict the range of the scaled text size to `[minScaleFactor * fontSize, maxScaleFactor * fontSize]` (to prevent excessive text scaling that would break the UI, for example). When `minScaleFactor` equals `maxScaleFactor`, the scaler becomes `TextScaler.linear(minScaleFactor)`.

### data

```dart
MediaQueryData data
```

Contains information about the current media.

For example, the [MediaQueryData.size] property contains the width and height of the current window.

### of()

```dart
MediaQueryData of(BuildContext context)
```

The data from the closest instance of this class that encloses the given context.

You can use this function to query the entire set of data held in the current [MediaQueryData] object. When any of that information changes, your widget will be scheduled to be rebuilt, keeping your widget up-to-date.

Since it is typical that the widget only requires a subset of properties of the [MediaQueryData] object, prefer using the more specific methods (for example: [MediaQuery.sizeOf] and [MediaQuery.paddingOf]), as those methods will not cause a widget to rebuild when unrelated properties are updated.

Typical usage is as follows:

```dart
MediaQueryData media = MediaQuery.of(context);
```

If there is no [MediaQuery] in scope, this method will throw a [TypeError] exception in release builds, and throw a descriptive [FlutterError] in debug builds.

See also:

- [maybeOf], which doesn't throw or assert if it doesn't find a [MediaQuery] ancestor. It returns null instead.
- [sizeOf] and other specific methods for retrieving and depending on changes of a specific value.

### maybeOf()

```dart
MediaQueryData? maybeOf(BuildContext context)
```

The data from the closest instance of this class that encloses the given context, if any.

Use this function if you want to allow situations where no [MediaQuery] is in scope. Prefer using [MediaQuery.of] in situations where a media query is always expected to exist.

If there is no [MediaQuery] in scope, then this function will return null.

You can use this function to query the entire set of data held in the current [MediaQueryData] object. When any of that information changes, your widget will be scheduled to be rebuilt, keeping your widget up-to-date.

Since it is typical that the widget only requires a subset of properties of the [MediaQueryData] object, prefer using the more specific methods (for example: [MediaQuery.maybeSizeOf] and [MediaQuery.maybePaddingOf]), as those methods will not cause a widget to rebuild when unrelated properties are updated.

Typical usage is as follows:

```dart
MediaQueryData? mediaQuery = MediaQuery.maybeOf(context);
if (mediaQuery == null) {
  // Do something else instead.
}
```

See also:

- [of], which will throw if it doesn't find a [MediaQuery] ancestor, instead of returning null.
- [maybeSizeOf] and other specific methods for retrieving and depending on changes of a specific value.

### sizeOf()

```dart
Size sizeOf(BuildContext context)
```

Returns [MediaQueryData.size] from the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@template flutter.widgets.media_query.MediaQuery.dontUseOf} Prefer using this function over getting the attribute directly from the [MediaQueryData] returned from [of], because using this function will only rebuild the `context` when this specific attribute changes, not when _any_ attribute changes. {@endtemplate}

### maybeSizeOf()

```dart
Size? maybeSizeOf(BuildContext context)
```

Returns [MediaQueryData.size] from the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@template flutter.widgets.media_query.MediaQuery.dontUseMaybeOf} Prefer using this function over getting the attribute directly from the [MediaQueryData] returned from [maybeOf], because using this function will only rebuild the `context` when this specific attribute changes, not when _any_ attribute changes. {@endtemplate}

### widthOf()

```dart
double widthOf(BuildContext context)
```

Returns width of [MediaQueryData.size] from the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the width of [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeWidthOf()

```dart
double? maybeWidthOf(BuildContext context)
```

Returns width of [MediaQueryData.size] from the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the width of [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### heightOf()

```dart
double heightOf(BuildContext context)
```

Returns height of [MediaQueryData.size] from the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the height of [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeHeightOf()

```dart
double? maybeHeightOf(BuildContext context)
```

Returns height of [MediaQueryData.size] from the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the height of [MediaQueryData.size] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### orientationOf()

```dart
Orientation orientationOf(BuildContext context)
```

Returns [MediaQueryData.orientation] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.orientation] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeOrientationOf()

```dart
Orientation? maybeOrientationOf(BuildContext context)
```

Returns [MediaQueryData.orientation] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.orientation] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### devicePixelRatioOf()

```dart
double devicePixelRatioOf(BuildContext context)
```

Returns [MediaQueryData.devicePixelRatio] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.devicePixelRatio] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDevicePixelRatioOf()

```dart
double? maybeDevicePixelRatioOf(BuildContext context)
```

Returns [MediaQueryData.devicePixelRatio] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.devicePixelRatio] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### textScaleFactorOf()

```dart
double textScaleFactorOf(BuildContext context)
```

Deprecated. Will be removed in a future version of Flutter. Use [maybeTextScalerOf] instead.

Returns [MediaQueryData.textScaleFactor] for the nearest [MediaQuery] ancestor or 1.0, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.textScaleFactor] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeTextScaleFactorOf()

```dart
double? maybeTextScaleFactorOf(BuildContext context)
```

Deprecated. Will be removed in a future version of Flutter. Use [maybeTextScalerOf] instead.

Returns [MediaQueryData.textScaleFactor] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.textScaleFactor] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### textScalerOf()

```dart
TextScaler textScalerOf(BuildContext context)
```

Returns the [MediaQueryData.textScaler] for the nearest [MediaQuery] ancestor or [TextScaler.noScaling] if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.textScaler] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeTextScalerOf()

```dart
TextScaler? maybeTextScalerOf(BuildContext context)
```

Returns the [MediaQueryData.textScaler] for the nearest [MediaQuery] ancestor or null if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.textScaler] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### platformBrightnessOf()

```dart
Brightness platformBrightnessOf(BuildContext context)
```

Returns [MediaQueryData.platformBrightness] for the nearest [MediaQuery] ancestor or [Brightness.light], if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.platformBrightness] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybePlatformBrightnessOf()

```dart
Brightness? maybePlatformBrightnessOf(BuildContext context)
```

Returns [MediaQueryData.platformBrightness] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.platformBrightness] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### paddingOf()

```dart
EdgeInsets paddingOf(BuildContext context)
```

Returns [MediaQueryData.padding] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.padding] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybePaddingOf()

```dart
EdgeInsets? maybePaddingOf(BuildContext context)
```

Returns [MediaQueryData.padding] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.padding] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### viewInsetsOf()

```dart
EdgeInsets viewInsetsOf(BuildContext context)
```

Returns [MediaQueryData.viewInsets] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.viewInsets] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeViewInsetsOf()

```dart
EdgeInsets? maybeViewInsetsOf(BuildContext context)
```

Returns [MediaQueryData.viewInsets] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.viewInsets] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### systemGestureInsetsOf()

```dart
EdgeInsets systemGestureInsetsOf(BuildContext context)
```

Returns [MediaQueryData.systemGestureInsets] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.systemGestureInsets] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSystemGestureInsetsOf()

```dart
EdgeInsets? maybeSystemGestureInsetsOf(BuildContext context)
```

Returns [MediaQueryData.systemGestureInsets] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.systemGestureInsets] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### viewPaddingOf()

```dart
EdgeInsets viewPaddingOf(BuildContext context)
```

Returns [MediaQueryData.viewPadding] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.viewPadding] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeViewPaddingOf()

```dart
EdgeInsets? maybeViewPaddingOf(BuildContext context)
```

Returns [MediaQueryData.viewPadding] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.viewPadding] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### alwaysUse24HourFormatOf()

```dart
bool alwaysUse24HourFormatOf(BuildContext context)
```

Returns [MediaQueryData.alwaysUse24HourFormat] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.alwaysUse24HourFormat] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeAlwaysUse24HourFormatOf()

```dart
bool? maybeAlwaysUse24HourFormatOf(BuildContext context)
```

Returns [MediaQueryData.alwaysUse24HourFormat] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.alwaysUse24HourFormat] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### accessibleNavigationOf()

```dart
bool accessibleNavigationOf(BuildContext context)
```

Returns [MediaQueryData.accessibleNavigation] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.accessibleNavigation] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeAccessibleNavigationOf()

```dart
bool? maybeAccessibleNavigationOf(BuildContext context)
```

Returns [MediaQueryData.accessibleNavigation] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.accessibleNavigation] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### invertColorsOf()

```dart
bool invertColorsOf(BuildContext context)
```

Returns [MediaQueryData.invertColors] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.invertColors] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeInvertColorsOf()

```dart
bool? maybeInvertColorsOf(BuildContext context)
```

Returns [MediaQueryData.invertColors] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.invertColors] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### highContrastOf()

```dart
bool highContrastOf(BuildContext context)
```

Returns [MediaQueryData.highContrast] for the nearest [MediaQuery] ancestor or false, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.highContrast] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeHighContrastOf()

```dart
bool? maybeHighContrastOf(BuildContext context)
```

Returns [MediaQueryData.highContrast] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.highContrast] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### onOffSwitchLabelsOf()

```dart
bool onOffSwitchLabelsOf(BuildContext context)
```

Returns [MediaQueryData.onOffSwitchLabels] for the nearest [MediaQuery] ancestor or false, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.onOffSwitchLabels] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeOnOffSwitchLabelsOf()

```dart
bool? maybeOnOffSwitchLabelsOf(BuildContext context)
```

Returns [MediaQueryData.onOffSwitchLabels] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.onOffSwitchLabels] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### disableAnimationsOf()

```dart
bool disableAnimationsOf(BuildContext context)
```

Returns [MediaQueryData.disableAnimations] for the nearest [MediaQuery] ancestor or false, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.disableAnimations] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisableAnimationsOf()

```dart
bool? maybeDisableAnimationsOf(BuildContext context)
```

Returns [MediaQueryData.disableAnimations] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.disableAnimations] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### boldTextOf()

```dart
bool boldTextOf(BuildContext context)
```

Returns the [MediaQueryData.boldText] accessibility setting for the nearest [MediaQuery] ancestor or false, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.boldText] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeBoldTextOf()

```dart
bool? maybeBoldTextOf(BuildContext context)
```

Returns the [MediaQueryData.boldText] accessibility setting for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.boldText] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### supportsAnnounceOf()

```dart
bool supportsAnnounceOf(BuildContext context)
```

Returns the [MediaQueryData.supportsAnnounce] accessibility setting for the nearest [MediaQuery] ancestor or false, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.supportsAnnounce] property of the ancestor [MediaQuery] changes. This is especially important for supportsAnnounce because supportsAnnounce has a low frequency change rate. The performance difference between rebuilding for all media query data changes and only rebuilding for supportsAnnounce is a dramatic difference.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSupportsAnnounceOf()

```dart
bool? maybeSupportsAnnounceOf(BuildContext context)
```

Returns the [MediaQueryData.supportsAnnounce] accessibility setting for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.supportsAnnounce] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### navigationModeOf()

```dart
NavigationMode navigationModeOf(BuildContext context)
```

Returns [MediaQueryData.navigationMode] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.navigationMode] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeNavigationModeOf()

```dart
NavigationMode? maybeNavigationModeOf(BuildContext context)
```

Returns [MediaQueryData.navigationMode] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.navigationMode] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### gestureSettingsOf()

```dart
DeviceGestureSettings gestureSettingsOf(BuildContext context)
```

Returns [MediaQueryData.gestureSettings] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.gestureSettings] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeGestureSettingsOf()

```dart
DeviceGestureSettings? maybeGestureSettingsOf(BuildContext context)
```

Returns [MediaQueryData.gestureSettings] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.gestureSettings] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### displayFeaturesOf()

```dart
List<ui.DisplayFeature> displayFeaturesOf(BuildContext context)
```

Returns [MediaQueryData.displayFeatures] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.displayFeatures] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisplayFeaturesOf()

```dart
List<ui.DisplayFeature>? maybeDisplayFeaturesOf(BuildContext context)
```

Returns [MediaQueryData.displayFeatures] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.displayFeatures] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### supportsShowingSystemContextMenu()

```dart
bool supportsShowingSystemContextMenu(BuildContext context)
```

Returns [MediaQueryData.supportsShowingSystemContextMenu] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.supportsShowingSystemContextMenu] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeSupportsShowingSystemContextMenu()

```dart
bool? maybeSupportsShowingSystemContextMenu(BuildContext context)
```

Returns [MediaQueryData.supportsShowingSystemContextMenu] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.supportsShowingSystemContextMenu] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeLineHeightScaleFactorOverrideOf()

```dart
double? maybeLineHeightScaleFactorOverrideOf(BuildContext context)
```

Returns the [MediaQueryData.lineHeightScaleFactorOverride] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists or if the platform has not specified an override.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.lineHeightScaleFactorOverride] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeLetterSpacingOverrideOf()

```dart
double? maybeLetterSpacingOverrideOf(BuildContext context)
```

Returns the [MediaQueryData.letterSpacingOverride] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists or if the platform has not specified an override.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.letterSpacingOverride] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeWordSpacingOverrideOf()

```dart
double? maybeWordSpacingOverrideOf(BuildContext context)
```

Returns the [MediaQueryData.wordSpacingOverride] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists or if the platform has not specified an override.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.wordSpacingOverride] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### maybeParagraphSpacingOverrideOf()

```dart
double? maybeParagraphSpacingOverrideOf(BuildContext context)
```

Returns the [MediaQueryData.paragraphSpacingOverride] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists or if the platform has not specified an override.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.paragraphSpacingOverride] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseMaybeOf}

### displayCornerRadiiOf()

```dart
BorderRadius? displayCornerRadiiOf(BuildContext context)
```

Returns [MediaQueryData.displayCornerRadii] for the nearest [MediaQuery] ancestor or throws an exception, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.displayCornerRadii] property of the ancestor [MediaQuery] changes.

{@macro flutter.widgets.media_query.MediaQuery.dontUseOf}

### maybeDisplayCornerRadiiOf()

```dart
BorderRadius? maybeDisplayCornerRadiiOf(BuildContext context)
```

Returns [MediaQueryData.displayCornerRadii] for the nearest [MediaQuery] ancestor or null, if no such ancestor exists.

Use of this method will cause the given [context] to rebuild any time that the [MediaQueryData.displayCornerRadii] property of the ancestor [MediaQuery] changes.

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

Describes the navigation mode to be set by a [MediaQuery] widget.

The different modes indicate the type of navigation to be used in a widget subtree for those widgets sensitive to it.

Use `MediaQuery.navigationModeOf(context)` to determine the navigation mode in effect for the given context. Use a [MediaQuery] widget to set the navigation mode for its descendant widgets.

This indicates a traditional keyboard-and-mouse navigation modality.

This navigation mode is where the arrow keys can be used for secondary modification operations, like moving sliders or cursors, and disabled controls will lose focus and not be traversable.

This indicates a directional-based navigation mode.

This navigation mode indicates that arrow keys should be reserved for navigation operations, and secondary modifications operations, like moving sliders or cursors, will use alternative bindings or be disabled.

Some behaviors are also affected by this mode. For instance, disabled controls will retain focus when disabled, and will be able to receive focus (although they remain disabled) when traversed.

# SystemTextScaler

```dart
final class SystemTextScaler extends TextScaler {}
```

A [TextScaler] that reflects the user's font scale preferences from the platform's accessibility settings.

### scale()

```dart
double scale(double fontSize)
```

### textScaleFactor

```dart
double textScaleFactor
```

A value that represents the current user preference for the scaling factor for fonts.

This numeric value is typically used to compare [SystemTextScaler]s. Two [SystemTextScaler] instances with the same [textScaleFactor] are considered equal as their [scale] methods produce the same output when given the same input font size. However, [textScaleFactor] should not be used in arithmetic operations.

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
