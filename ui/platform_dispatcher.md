# VoidCallback

```dart
typedef VoidCallback = void Function()
```

Signature of callbacks that have no arguments and return no data.

# FrameCallback

```dart
typedef FrameCallback = void Function(Duration duration)
```

Signature for [PlatformDispatcher.onBeginFrame].

The `duration` argument is the point at which the current frame interval began, expressed as a duration since some epoch. The epoch in all frames will be the same, but it may not match [DateTime]'s epoch.

For any two frames `a` and `b` such that the frame number of `a` is less than the frame number of `b`, the duration argument for `a` will be less than or equal to the duration argument for `b`.

# TimingsCallback

```dart
typedef TimingsCallback = void Function(List<FrameTiming> timings)
```

Signature for [PlatformDispatcher.onReportTimings].

{@template dart.ui.TimingsCallback.list} The callback takes a list of [FrameTiming] because it may not be immediately triggered after each frame. Instead, Flutter tries to batch frames together and send all their timings at once to decrease the overhead (as this is available in the release mode). The list is sorted in ascending order of time (earliest frame first). The timing of any frame will be sent within about 1 second (100ms if in the profile/debug mode) even if there are no later frames to batch. The timing of the first frame will be sent immediately without batching. {@endtemplate}

# PointerDataPacketCallback

```dart
typedef PointerDataPacketCallback = void Function(PointerDataPacket packet)
```

Signature for [PlatformDispatcher.onPointerDataPacket].

# KeyDataCallback

```dart
typedef KeyDataCallback = bool Function(KeyData data)
```

Signature for [PlatformDispatcher.onKeyData].

The callback should return true if the key event has been handled by the framework and should not be propagated further.

# SemanticsActionEventCallback

```dart
typedef SemanticsActionEventCallback = void Function(SemanticsActionEvent action)
```

Signature for [PlatformDispatcher.onSemanticsActionEvent].

# HitTestCallback

```dart
typedef HitTestCallback = HitTestResponse Function(HitTestRequest request)
```

Signature for [PlatformDispatcher.onHitTest].

# PlatformMessageResponseCallback

```dart
typedef PlatformMessageResponseCallback = void Function(ByteData? data)
```

Signature for responses to platform messages.

Used as a parameter to [PlatformDispatcher.sendPlatformMessage] and [PlatformDispatcher.onPlatformMessage].

# PlatformMessageCallback

```dart
typedef PlatformMessageCallback = void Function(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

Deprecated. Migrate to [ChannelBuffers.setListener] instead.

Signature for [PlatformDispatcher.onPlatformMessage].

# ErrorCallback

```dart
typedef ErrorCallback = bool Function(Object exception, StackTrace stackTrace)
```

Signature for [PlatformDispatcher.onError].

If this method returns false, the engine may use some fallback method to provide information about the error.

After calling this method, the process or the VM may terminate. Some severe unhandled errors may not be able to call this method either, such as Dart compilation errors or process terminating errors.

# RootIsolateToken

```dart
class RootIsolateToken {}
```

A token that represents a root isolate.

### instance

```dart
RootIsolateToken? instance
```

The token for the root isolate that is executing this Dart code. If this Dart code is not executing on a root isolate [instance] will be null.

# PlatformDispatcher

```dart
class PlatformDispatcher {}
```

Platform event dispatcher singleton.

The most basic interface to the host operating system's interface.

This is the central entry point for platform messages and configuration events from the platform.

It exposes the core scheduler API, the input event callback, the graphics drawing API, and other such core services.

It manages the list of the application's [views] as well as the [configuration] of various platform attributes.

Consider avoiding static references to this singleton through [PlatformDispatcher.instance] and instead prefer using a binding for dependency resolution such as `WidgetsBinding.instance.platformDispatcher`. See [PlatformDispatcher.instance] for more information about why this is preferred.

### instance

```dart
PlatformDispatcher get instance
```

The [PlatformDispatcher] singleton.

Consider avoiding static references to this singleton through [PlatformDispatcher.instance] and instead prefer using a binding for dependency resolution such as `WidgetsBinding.instance.platformDispatcher`.

Static access of this object means that Flutter has few, if any options to fake or mock the given object in tests. Even in cases where Dart offers special language constructs to forcefully shadow such properties, those mechanisms would only be reasonable for tests and they would not be reasonable for a future of Flutter where we legitimately want to select an appropriate implementation at runtime.

The only place that `WidgetsBinding.instance.platformDispatcher` is inappropriate is if access to these APIs is required before the binding is initialized by invoking `runApp()` or `WidgetsFlutterBinding.instance.ensureInitialized()`. In that case, it is necessary (though unfortunate) to use the [PlatformDispatcher.instance] object statically.

### onPlatformConfigurationChanged

```dart
VoidCallback? get onPlatformConfigurationChanged
```

Called when the platform configuration changes.

The engine invokes this callback in the same zone in which the callback was set.

### onPlatformConfigurationChanged

```dart
set onPlatformConfigurationChanged(VoidCallback? callback)
```

### displays

```dart
Iterable<Display> get displays
```

The current list of displays.

If any of their configurations change, [onMetricsChanged] will be called.

To get the display for a [FlutterView], use [FlutterView.display].

Platforms may limit what information is available to the application with regard to secondary displays and/or displays that do not have an active application window.

Presently, on Android and Web this collection will only contain the display that the current window is on. On iOS, it will only contains the main display on the phone or tablet. On Desktops other than Linux, it will contain only a main display with a valid refresh rate but invalid size and device pixel ratio values.

### views

```dart
Iterable<FlutterView> get views
```

The current list of views, including top level platform windows used by the application.

If any of their configurations change, [onMetricsChanged] will be called.

### view()

```dart
FlutterView? view({required int id})
```

Returns the [FlutterView] with the provided ID if one exists, or null otherwise.

### implicitView

```dart
FlutterView? get implicitView
```

The [FlutterView] provided by the engine if the platform is unable to create windows, or, for backwards compatibility.

If the platform provides an implicit view, it can be used to bootstrap the framework. This is common for platforms designed for single-view applications like mobile devices with a single display.

Applications and libraries must not rely on this property being set as it may be null depending on the engine's configuration. Instead, consider using [View.of] to lookup the [FlutterView] the current [BuildContext] is drawing into.

While the properties on the referenced [FlutterView] may change, the reference itself is guaranteed to never change over the lifetime of the application: if this property is null at startup, it will remain so throughout the entire lifetime of the application. If it points to a specific [FlutterView], it will continue to point to the same view until the application is shut down (although the engine may replace or remove the underlying backing surface of the view at its discretion).

See also:

- [View.of], for accessing the current view.
- [PlatformDispatcher.views] for a list of all [FlutterView]s provided by the platform.

### onMetricsChanged

```dart
VoidCallback? get onMetricsChanged
```

A callback that is invoked whenever the [ViewConfiguration] of any of the [views] changes.

For example when the device is rotated or when the application is resized (e.g. when showing applications side-by-side on Android), `onMetricsChanged` is called.

The engine invokes this callback in the same zone in which the callback was set.

The framework registers with this callback and updates the layout appropriately.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to register for notifications when this is called.
- [MediaQuery.of], a simpler mechanism for the same.

### onMetricsChanged

```dart
set onMetricsChanged(VoidCallback? callback)
```

### engineId

```dart
int? get engineId
```

Opaque engine identifier for the engine running current isolate. Can be used in native code to retrieve the engine instance. The identifier is valid while the isolate is running.

### onViewFocusChange

```dart
ViewFocusChangeCallback? get onViewFocusChange
```

A callback invoked immediately after the focus is transitioned across [FlutterView]s.

When the platform moves the focus from one [FlutterView] to another, this callback is invoked indicating the new view that has focus and the direction in which focus was received. For example, if focus is moved to the [FlutterView] with ID 2 in the forward direction (could be the result of pressing tab) the callback receives a [ViewFocusEvent] with [ViewFocusState.focused] and [ViewFocusDirection.forward].

Typically, receivers of this event respond by moving the focus to the first focusable widget inside the [FlutterView] with ID 2. If a view receives focus in the backward direction (could be the result of pressing shift + tab), typically the last focusable widget inside that view is focused.

The platform may remove focus from a [FlutterView]. For example, on the web, the browser can move focus to another element, or to the browser's built-in UI. On desktop, the operating system can switch to another window (e.g. using Alt + Tab on Windows). In scenarios like these, [onViewFocusChange] will be invoked with [ViewFocusState.unfocused] and [ViewFocusDirection.undefined].

Receivers typically respond to this event by removing all focus indications from the app.

Apps can also programmatically request to move the focus to a desired [FlutterView] by calling [requestViewFocusChange].

The callback is invoked in the same zone in which the callback was set.

See also:

- [requestViewFocusChange] to programmatically instruct the platform to move focus to a different [FlutterView].
- [ViewFocusState] for a list of allowed focus transitions.
- [ViewFocusDirection] for a list of allowed focus directions.
- [ViewFocusEvent], which is the event object provided to the callback.

### onViewFocusChange

```dart
set onViewFocusChange(ViewFocusChangeCallback? callback)
```

### requestViewFocusChange()

```dart
void requestViewFocusChange({required int viewId, required ViewFocusState state, required ViewFocusDirection direction})
```

Requests a focus change of the [FlutterView] with ID [viewId].

If an app would like to request the engine to move focus, in forward direction, to the [FlutterView] with ID 1 it should call this method with [ViewFocusState.focused] and [ViewFocusDirection.forward].

There is no need to call this method if the view in question already has focus as it won't have any effect.

A call to this method will lead to the engine calling [onViewFocusChange] if the request is successfully fulfilled.

See also:

- [onViewFocusChange], a callback to subscribe to view focus change events.

### onBeginFrame

```dart
FrameCallback? get onBeginFrame
```

A callback invoked when any view begins a frame.

A callback that is invoked to notify the application that it is an appropriate time to provide a scene using the [SceneBuilder] API and the [FlutterView.render] method.

When possible, this is driven by the hardware VSync signal of the attached screen with the highest VSync rate. This is only called if [PlatformDispatcher.scheduleFrame] has been called since the last time this callback was invoked.

### onBeginFrame

```dart
set onBeginFrame(FrameCallback? callback)
```

### onDrawFrame

```dart
VoidCallback? get onDrawFrame
```

A callback that is invoked for each frame after [onBeginFrame] has completed and after the microtask queue has been drained.

This can be used to implement a second phase of frame rendering that happens after any deferred work queued by the [onBeginFrame] phase.

### onDrawFrame

```dart
set onDrawFrame(VoidCallback? callback)
```

### onPointerDataPacket

```dart
PointerDataPacketCallback? get onPointerDataPacket
```

A callback that is invoked when pointer data is available.

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

The callback should return true if the key event has been handled by the framework and should not be propagated further.

### onKeyData

```dart
set onKeyData(KeyDataCallback? callback)
```

### onReportTimings

```dart
TimingsCallback? get onReportTimings
```

A callback that is invoked to report the [FrameTiming] of recently rasterized frames.

It's preferred to use [SchedulerBinding.addTimingsCallback] than to use [onReportTimings] directly because [SchedulerBinding.addTimingsCallback] allows multiple callbacks.

This can be used to see if the application has missed frames (through [FrameTiming.buildDuration] and [FrameTiming.rasterDuration]), or high latencies (through [FrameTiming.totalSpan]).

Unlike [Timeline], the timing information here is available in the release mode (additional to the profile and the debug mode). Hence this can be used to monitor the application's performance in the wild.

{@macro dart.ui.TimingsCallback.list}

If this is null, no additional work will be done. If this is not null, Flutter spends less than 0.1ms every 1 second to report the timings (measured on iPhone6S). The 0.1ms is about 0.6% of 16ms (frame budget for 60fps), or 0.01% CPU usage per second.

### onReportTimings

```dart
set onReportTimings(TimingsCallback? callback)
```

### sendPlatformMessage()

```dart
void sendPlatformMessage(String name, ByteData? data, PlatformMessageResponseCallback? callback)
```

Sends a message to a platform-specific plugin.

The `name` parameter determines which plugin receives the message. The `data` parameter contains the message payload and is typically UTF-8 encoded JSON but can be arbitrary data. If the plugin replies to the message, `callback` will be called with the response.

The framework invokes [callback] in the same zone in which this method was called.

### sendPortPlatformMessage()

```dart
void sendPortPlatformMessage(String name, ByteData? data, int identifier, SendPort port)
```

Sends a message to a platform-specific plugin via a [SendPort].

This operates similarly to [sendPlatformMessage] but is used when sending messages from background isolates. The [port] parameter allows Flutter to know which isolate to send the result to. The [name] parameter is the name of the channel communication will happen on. The [data] parameter is the payload of the message. The [identifier] parameter is a unique integer assigned to the message.

### registerBackgroundIsolate()

```dart
void registerBackgroundIsolate(RootIsolateToken token)
```

Registers the current isolate with the isolate identified with by the [token]. This is required if platform channels are to be used on a background isolate.

### setSemanticsTreeEnabled()

```dart
void setSemanticsTreeEnabled(bool enabled)
```

Informs the engine whether the framework is generating a semantics tree.

Only framework knows when semantics tree should be generated. It uses this method to notify the engine whether the framework will generate a semantics tree.

In the case where platforms want to enable semantics, e.g. when assistive technologies are enabled, it notifies framework through [onSemanticsEnabledChanged].

After this has been set to true, platforms are expected to prepare for accepting semantics update sent via [FlutterView.updateSemantics]. When this is set to false, platforms may dispose any resources associated with processing semantics as no further semantics updates will be sent via [FlutterView.updateSemantics].

One must call this method with true before sending update through [updateSemantics].

### onPlatformMessage

```dart
PlatformMessageCallback? get onPlatformMessage
```

Deprecated. Migrate to [ChannelBuffers.setListener] instead.

Called whenever this platform dispatcher receives a message from a platform-specific plugin.

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

Normally debug names are automatically generated from the Dart port, entry point, and source file. For example: `main.dart$main-1234`.

This can be combined with flutter tools `--isolate-filter` flag to debug specific root isolates. For example: `flutter attach --isolate-filter=[name]`. Note that this does not rename any child isolates of the root.

### requestDartPerformanceMode()

```dart
void requestDartPerformanceMode(DartPerformanceMode mode)
```

Requests the Dart VM to adjusts the GC heuristics based on the requested `performance_mode`.

This operation is a no-op of web. The request to change a performance may be ignored by the engine or not resolve in a predictable way.

See [DartPerformanceMode] for more information on individual performance modes.

### getPersistentIsolateData()

```dart
ByteData? getPersistentIsolateData()
```

The embedder can specify data that the isolate can request synchronously on launch. This accessor fetches that data.

This data is persistent for the duration of the Flutter application and is available even after isolate restarts. Because of this lifecycle, the size of this data must be kept to a minimum.

For asynchronous communication between the embedder and isolate, a platform channel may be used.

### scheduleFrame()

```dart
void scheduleFrame()
```

Requests that, at the next appropriate opportunity, the [onBeginFrame] and [onDrawFrame] callbacks be invoked.

See also:

- [SchedulerBinding], the Flutter framework class which manages the scheduling of frames.
- [scheduleWarmUpFrame], which should only be used to schedule warm up frames.

### scheduleWarmUpFrame()

```dart
void scheduleWarmUpFrame({required VoidCallback beginFrame, required VoidCallback drawFrame})
```

Schedule a frame to run as soon as possible, rather than waiting for the engine to request a frame in response to a system "Vsync" signal.

The application can call this method as soon as it starts up so that the first frame (which is likely to be quite expensive) can start a few extra milliseconds earlier. Using it in other situations might lead to unintended results, such as screen tearing. Depending on platforms and situations, the warm up frame might or might not be actually rendered onto the screen.

For more introduction to the warm up frame, see [SchedulerBinding.scheduleWarmUpFrame].

This method uses the provided callbacks as the begin frame callback and the draw frame callback instead of [onBeginFrame] and [onDrawFrame].

See also:

- [SchedulerBinding.scheduleWarmUpFrame], which uses this method, and introduces the warm up frame in more details.
- [scheduleFrame], which schedules the frame at the next appropriate opportunity and should be used to render regular frames.

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

The framework invokes this callback in the same zone in which the callback was set.

### onAccessibilityFeaturesChanged

```dart
set onAccessibilityFeaturesChanged(VoidCallback? callback)
```

### updateSemantics()

```dart
void updateSemantics(SemanticsUpdate update)
```

Change the retained semantics data about this platform dispatcher.

If [semanticsEnabled] is true, the user has requested that this function be called whenever the semantic content of this platform dispatcher changes.

In either case, this function disposes the given update, which means the semantics update cannot be used further.

### locale

```dart
Locale get locale
```

The system-reported default locale of the device.

This establishes the language and formatting conventions that application should, if possible, use to render their user interface.

This is the first locale selected by the user and is the user's primary locale (the locale the device UI is displayed in)

This is equivalent to `locales.first`, except that it will provide an undefined (using the language tag "und") non-null locale if the [locales] list has not been set or is empty.

### setApplicationLocale()

```dart
void setApplicationLocale(Locale locale)
```

Sets the locale for the application in engine.

This is typically called by framework to set the locale based on which locale the Flutter app actually uses.

### locales

```dart
List<Locale> get locales
```

The full system-reported supported locales of the device.

This establishes the language and formatting conventions that application should, if possible, use to render their user interface.

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

This property will not be updated as the lifecycle changes.

It is used to initialize [SchedulerBinding.lifecycleState] at startup with any buffered lifecycle state events.

### alwaysUse24HourFormat

```dart
bool get alwaysUse24HourFormat
```

The setting indicating whether time should always be shown in the 24-hour format.

This option is used by [showTimePicker].

### lineHeightScaleFactorOverride

```dart
double? get lineHeightScaleFactorOverride
```

The system-suggested height of the text, as a multiple of the font size.

This value takes precedence over any text height specified at the application level. For example, at framework level, in the [TextStyle] for [Text], [SelectableText], and [EditableText] widgets, this value overrides the existing value of [TextStyle.height] and [StrutStyle.height].

Returns null when no override has been set by the system.

If this value changes, [onMetricsChanged] will be called.

### letterSpacingOverride

```dart
double? get letterSpacingOverride
```

The system-suggested amount of additional space (in logical pixels) to add between each letter.

A negative value can be used to bring the letters closer.

This value takes precedence over any text letter spacing specified at the application level. For example, at framework level, in the [TextStyle] for [Text], [SelectableText], and [EditableText] widgets, this value overrides the existing value of [TextStyle.letterSpacing].

Returns null when no override has been set by the system.

If this value changes, [onMetricsChanged] will be called.

### wordSpacingOverride

```dart
double? get wordSpacingOverride
```

The system-suggested amount of additional space (in logical pixels) to add between each sequence of white-space (i.e. between each word).

A negative value can be used to bring the words closer.

This value takes precedence over any text word spacing specified at the application level. For example, at framework level, in the [TextStyle] for [Text], [SelectableText], and [EditableText] widgets, this value overrides the existing value of [TextStyle.wordSpacing].

Returns null when no override has been set by the system.

If this value changes, [onMetricsChanged] will be called.

### paragraphSpacingOverride

```dart
double? get paragraphSpacingOverride
```

The system-suggested amount of additional space (in logical pixels) to add following each paragraph in text.

This value takes precedence over any text paragraph spacing specified at the application level.

Returns null when no override has been set by the system.

If this value changes, [onMetricsChanged] will be called.

### textScaleFactor

```dart
double get textScaleFactor
```

The system-reported text scale.

This establishes the text scaling factor to use when rendering text, according to the user's platform preferences.

The [onTextScaleFactorChanged] callback is called whenever this value changes.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this value changes.

### onTextScaleFactorChanged

```dart
VoidCallback? get onTextScaleFactorChanged
```

A callback that is invoked whenever [textScaleFactor] changes value.

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onTextScaleFactorChanged

```dart
set onTextScaleFactorChanged(VoidCallback? callback)
```

### nativeSpellCheckServiceDefined

```dart
bool get nativeSpellCheckServiceDefined
```

Whether the spell check service is supported on the current platform.

This option is used by [EditableTextState] to define its [SpellCheckConfiguration] when a default spell check service is requested.

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

### platformBrightness

```dart
Brightness get platformBrightness
```

The setting indicating the current brightness mode of the host platform. If the platform has no preference, [platformBrightness] defaults to [Brightness.light].

### onPlatformBrightnessChanged

```dart
VoidCallback? get onPlatformBrightnessChanged
```

A callback that is invoked whenever [platformBrightness] changes value.

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

The setting indicating the current system font of the host platform.

### onSystemFontFamilyChanged

```dart
VoidCallback? get onSystemFontFamilyChanged
```

A callback that is invoked whenever [systemFontFamily] changes value.

The framework invokes this callback in the same zone in which the callback was set.

See also:

- [WidgetsBindingObserver], for a mechanism at the widgets layer to observe when this callback is invoked.

### onSystemFontFamilyChanged

```dart
set onSystemFontFamilyChanged(VoidCallback? callback)
```

### semanticsEnabled

```dart
bool get semanticsEnabled
```

Whether the user has requested that updateSemantics be called when the semantic contents of a view changes.

The [onSemanticsEnabledChanged] callback is called whenever this value changes.

### onSemanticsEnabledChanged

```dart
VoidCallback? get onSemanticsEnabledChanged
```

A callback that is invoked when the value of [semanticsEnabled] changes.

The framework invokes this callback in the same zone in which the callback was set.

### onSemanticsEnabledChanged

```dart
set onSemanticsEnabledChanged(VoidCallback? callback)
```

### onSemanticsActionEvent

```dart
SemanticsActionEventCallback? get onSemanticsActionEvent
```

A callback that is invoked whenever the user requests an action to be performed on a semantics node.

This callback is used when the user expresses the action they wish to perform based on the semantics node supplied by updateSemantics.

The framework invokes this callback in the same zone in which the callback was set.

### onSemanticsActionEvent

```dart
set onSemanticsActionEvent(SemanticsActionEventCallback? callback)
```

### onHitTest

```dart
HitTestCallback? get onHitTest
```

A callback invoked when the platform wants to hit test a [FlutterView].

For example, this is used by iOS to determine if a gesture hits a [UIKitView].

### onHitTest

```dart
set onHitTest(HitTestCallback? callback)
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

### onError

```dart
ErrorCallback? get onError
```

A callback that is invoked when an unhandled error occurs in the root isolate.

This callback must return `true` if it has handled the error. Otherwise, it must return `false` and a fallback mechanism such as printing to stderr will be used, as configured by the specific platform embedding via `Settings::unhandled_exception_callback`.

The VM or the process may exit or become unresponsive after calling this callback. The callback will not be called for exceptions that cause the VM or process to terminate or become unresponsive before the callback can be invoked.

This callback is not directly invoked by errors in child isolates of the root isolate. Programs that create new isolates must listen for errors on those isolates and forward the errors to the root isolate.

### onError

```dart
set onError(ErrorCallback? callback)
```

### defaultRouteName

```dart
String get defaultRouteName
```

The route or path that the embedder requested when the application was launched.

This will be the string "`/`" if no particular route was requested.

## Android

On Android, calling [`FlutterView.setInitialRoute`](/javadoc/io/flutter/view/FlutterView.html#setInitialRoute-java.lang.String-) will set this value. The value must be set sufficiently early, i.e. before the [runApp] call is executed in Dart, for this to have any effect on the framework. The `createFlutterView` method in your `FlutterActivity` subclass is a suitable time to set the value. The application's `AndroidManifest.xml` file must also be updated to have a suitable [`<intent-filter>`](https://developer.android.com/guide/topics/manifest/intent-filter-element.html).

## iOS

On iOS, calling [`FlutterViewController.setInitialRoute`](/ios-embedder/interface_flutter_view_controller.html#a7f269c2da73312f856d42611cc12a33f) will set this value. The value must be set sufficiently early, i.e. before the [runApp] call is executed in Dart, for this to have any effect on the framework. The `application:didFinishLaunchingWithOptions:` method is a suitable time to set this value.

See also:

- [Navigator], a widget that handles routing.
- [SystemChannels.navigation], which handles subsequent navigation requests from the embedder.

### scaleFontSize()

```dart
double scaleFontSize(double unscaledFontSize)
```

Computes the scaled font size from the given `unscaledFontSize`, according to the user's platform preferences.

Many platforms allow users to scale text globally for better readability. Given the font size the app developer specified in logical pixels, this method converts it to the preferred font size (also in logical pixels) that accounts for platform-wide text scaling. The return value is always non-negative.

The scaled value of the same font size input may change if the user changes the text scaling preference (in system settings for example). The [onTextScaleFactorChanged] callback can be used to monitor such changes.

Instead of directly calling this method, applications should typically use [MediaQuery.textScalerOf] to retrive the scaled font size in a widget tree, so text in the app resizes properly when the text scaling preference changes.

# SystemColor

```dart
final class SystemColor {}
```

A color specified in the operating system UI color palette.

As of the current release, system colors are supported on web only. To check if the current platform supports system colors, use the static [platformProvidesSystemColors] field. If the field is `false`, other functions in this class will throw [UnsupportedError].

This class is typically used in conjunction with [AccessibilityFeatures.highContrast]. In particular, on Windows, when a user enables high-contrast mode, they may also pick specific colors that should be used by application user interfaces. While it is common for applications to use custom color themes and design languages, in high-contrast mode it is recommended that widgets use system-specified colors to make content more legible for users.

The "light" system colors are available through [SystemColor.light], and the "dark" system colors are available through [SystemColor.dark].

Example:

```dart
import 'dart:ui';

Color getSystemAccentColor() {
  Color? systemAccentColor;
  if (SystemColor.platformProvidesSystemColors) {
    if (PlatformDispatcher.instance.platformBrightness == Brightness.light) {
      systemAccentColor = SystemColor.light.accentColor.value;
    } else {
      systemAccentColor = SystemColor.dark.accentColor.value;
    }
  }

  return systemAccentColor ?? const Color(0xFF007AFF);
}
```

See also:

- https://drafts.csswg.org/css-color/#css-system-colors
- https://developer.mozilla.org/en-US/docs/Web/CSS/system-color
- https://developer.mozilla.org/en-US/docs/Web/CSS/@media/forced-colors

### SystemColor()

```dart
SystemColor({required String name, Color? value})
```

Creates an instance of a system color.

[name] is the name of the color. System colors provided by [SystemColorPalette], such as [SystemColorPalette.accentColor] and [SystemColorPalette.buttonText], use standard names defined by the [W3C CSS specification](https://drafts.csswg.org/css-color/#css-system-colors).

[value] is the color value, if this color name is supported, and null if it's unsupported.

### name

```dart
String name
```

Standard system color name, as defined by W3C CSS specification.

System color names in Flutter are case-sensitive. This is so that color names can be easily used as [Map] keys. This is in contrast to CSS, where system color names are not case-sensitive. That is, specifying `background-color: aCcEnTcOlOr` is equivalent to specifying `background-color: AccentColor`.

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### value

```dart
Color? value
```

The color value used for the color named [name], if supported.

If [isSupported] is false, the [value] is null. If [isSupported] is true, the [value] is not null.

### isSupported

```dart
bool get isSupported
```

Returns true if the current platform provides the system color with the given [name].

See also:

- [platformProvidesSystemColors], which returns whether the current platform provides system colors.

### platformProvidesSystemColors

```dart
bool get platformProvidesSystemColors
```

Returns true if the current platform provides system colors.

As of the current release, system colors are supported on web only.

See also:

- [isSupported], which returns whether a specific color is supported.

### light

```dart
SystemColorPalette light
```

A palette of system colors for light mode.

### dark

```dart
SystemColorPalette dark
```

A palette of system colors for dark mode.

# SystemColorPalette

```dart
final class SystemColorPalette {}
```

A palette of system colors specified in the operating system for a given [brightness].

The getters in this class, such as [accentColor] and [buttonText], provide standard system colors defined by the [W3C CSS specification](https://drafts.csswg.org/css-color/#css-system-colors).

### brightness

```dart
Brightness brightness
```

The brightness mode for which this palette is defined.

### accentColor

```dart
SystemColor get accentColor
```

Returns system color named "AccentColor".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### accentColorText

```dart
SystemColor get accentColorText
```

Returns system color named "AccentColorText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### activeText

```dart
SystemColor get activeText
```

Returns system color named "ActiveText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonBorder

```dart
SystemColor get buttonBorder
```

Returns system color named "ButtonBorder".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonFace

```dart
SystemColor get buttonFace
```

Returns system color named "ButtonFace".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### buttonText

```dart
SystemColor get buttonText
```

Returns system color named "ButtonText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### canvas

```dart
SystemColor get canvas
```

Returns system color named "Canvas".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### canvasText

```dart
SystemColor get canvasText
```

Returns system color named "CanvasText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### field

```dart
SystemColor get field
```

Returns system color named "Field".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### fieldText

```dart
SystemColor get fieldText
```

Returns system color named "FieldText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### grayText

```dart
SystemColor get grayText
```

Returns system color named "GrayText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### highlight

```dart
SystemColor get highlight
```

Returns system color named "Highlight".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### highlightText

```dart
SystemColor get highlightText
```

Returns system color named "HighlightText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### linkText

```dart
SystemColor get linkText
```

Returns system color named "LinkText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### mark

```dart
SystemColor get mark
```

Returns system color named "Mark".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### markText

```dart
SystemColor get markText
```

Returns system color named "MarkText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### selectedItem

```dart
SystemColor get selectedItem
```

Returns system color named "SelectedItem".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### selectedItemText

```dart
SystemColor get selectedItemText
```

Returns system color named "SelectedItemText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

### visitedText

```dart
SystemColor get visitedText
```

Returns system color named "VisitedText".

See also:

- https://drafts.csswg.org/css-color/#css-system-colors

# FramePhase

```dart
enum FramePhase {}
```

Various important time points in the lifetime of a frame.

[FrameTiming] records a timestamp of each phase for performance analysis.

The timestamp of the vsync signal given by the operating system.

See also [FrameTiming.vsyncOverhead].

When the UI thread starts building a frame.

See also [FrameTiming.buildDuration].

When the UI thread finishes building a frame.

See also [FrameTiming.buildDuration].

When the raster thread starts rasterizing a frame.

See also [FrameTiming.rasterDuration].

When the raster thread finishes rasterizing a frame.

See also [FrameTiming.rasterDuration].

When the raster thread finished rasterizing a frame in wall-time.

This is useful for correlating time raster finish time with the system clock to integrate with other profiling tools.

# FrameTiming

```dart
class FrameTiming {}
```

Time-related performance metrics of a frame.

If you're using the whole Flutter framework, please use [SchedulerBinding.addTimingsCallback] to get this. It's preferred over using [PlatformDispatcher.onReportTimings] directly because [SchedulerBinding.addTimingsCallback] allows multiple callbacks. If [SchedulerBinding] is unavailable, then see [PlatformDispatcher.onReportTimings] for how to get this.

The metrics in debug mode (`flutter run` without any flags) may be very different from those in profile and release modes due to the debug overhead. Therefore it's recommended to only monitor and analyze performance metrics in profile and release modes.

### FrameTiming()

```dart
FrameTiming({required int vsyncStart, required int buildStart, required int buildFinish, required int rasterStart, required int rasterFinish, required int rasterFinishWallTime, int layerCacheCount = 0, int layerCacheBytes = 0, int pictureCacheCount = 0, int pictureCacheBytes = 0, int frameNumber = -1})
```

Construct [FrameTiming] with raw timestamps in microseconds.

This constructor is used for unit test only. Real [FrameTiming]s should be retrieved from [PlatformDispatcher.onReportTimings].

If the [frameNumber] is not provided, it defaults to `-1`.

### timestampInMicroseconds()

```dart
int timestampInMicroseconds(FramePhase phase)
```

This is a raw timestamp in microseconds from some epoch. The epoch in all [FrameTiming] is the same, but it may not match [DateTime]'s epoch.

### buildDuration

```dart
Duration get buildDuration
```

The duration to build the frame on the UI thread.

The build starts approximately when [PlatformDispatcher.onBeginFrame] is called. The [Duration] in the [PlatformDispatcher.onBeginFrame] callback is exactly the `Duration(microseconds: timestampInMicroseconds(FramePhase.buildStart))`.

The build finishes when [FlutterView.render] is called.

{@template dart.ui.FrameTiming.fps_smoothness_milliseconds} To ensure smooth animations of X fps, this should not exceed 1000/X milliseconds. {@endtemplate} {@template dart.ui.FrameTiming.fps_milliseconds} That's about 16ms for 60fps, and 8ms for 120fps. {@endtemplate}

### rasterDuration

```dart
Duration get rasterDuration
```

The duration to rasterize the frame on the raster thread.

{@macro dart.ui.FrameTiming.fps_smoothness_milliseconds} {@macro dart.ui.FrameTiming.fps_milliseconds}

### vsyncOverhead

```dart
Duration get vsyncOverhead
```

The duration between receiving the vsync signal and starting building the frame.

### totalSpan

```dart
Duration get totalSpan
```

The timespan between vsync start and raster finish.

To achieve the lowest latency on an X fps display, this should not exceed 1000/X milliseconds. {@macro dart.ui.FrameTiming.fps_milliseconds}

See also [vsyncOverhead], [buildDuration] and [rasterDuration].

### layerCacheCount

```dart
int get layerCacheCount
```

The number of layers stored in the raster cache during the frame.

See also [layerCacheBytes], [pictureCacheCount] and [pictureCacheBytes].

### layerCacheBytes

```dart
int get layerCacheBytes
```

The number of bytes of image data used to cache layers during the frame.

See also [layerCacheCount], [layerCacheMegabytes], [pictureCacheCount] and [pictureCacheBytes].

### layerCacheMegabytes

```dart
double get layerCacheMegabytes
```

The number of megabytes of image data used to cache layers during the frame.

See also [layerCacheCount], [layerCacheBytes], [pictureCacheCount] and [pictureCacheBytes].

### pictureCacheCount

```dart
int get pictureCacheCount
```

The number of pictures stored in the raster cache during the frame.

See also [layerCacheCount], [layerCacheBytes] and [pictureCacheBytes].

### pictureCacheBytes

```dart
int get pictureCacheBytes
```

The number of bytes of image data used to cache pictures during the frame.

See also [layerCacheCount], [layerCacheBytes], [pictureCacheCount] and [pictureCacheMegabytes].

### pictureCacheMegabytes

```dart
double get pictureCacheMegabytes
```

The number of megabytes of image data used to cache pictures during the frame.

See also [layerCacheCount], [layerCacheBytes], [pictureCacheCount] and [pictureCacheBytes].

### frameNumber

```dart
int get frameNumber
```

The frame key associated with this frame measurement.

### toString()

```dart
String toString()
```

# AppLifecycleState

```dart
enum AppLifecycleState {}
```

States that an application can be in once it is running.

States not supported on a platform will be synthesized by the framework when transitioning between states which are supported, so that all implementations share the same state machine.

The initial value for the state is the [detached] state, updated to the current state (usually [resumed]) as soon as the first lifecycle update is received from the platform.

For historical and name collision reasons, Flutter's application state names do not correspond one to one with the state names on all platforms. On Android, for instance, when the OS calls [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>), Flutter will enter the [inactive] state, but when Android calls [`Activity.onStop`](<https://developer.android.com/reference/android/app/Activity#onStop()>), Flutter enters the [paused] state. See the individual state's documentation for descriptions of what they mean on each platform.

The current application state can be obtained from [SchedulerBinding.instance.lifecycleState], and changes to the state can be observed by creating an [AppLifecycleListener], or by using a [WidgetsBindingObserver] by overriding the [WidgetsBindingObserver.didChangeAppLifecycleState] method.

Applications should not rely on always receiving all possible notifications.

For example, if the application is killed with a task manager, a kill signal, the user pulls the power from the device, or there is a rapid unscheduled disassembly of the device, no notification will be sent before the application is suddenly terminated, and some states may be skipped.

See also:

- [AppLifecycleListener], an object used observe the lifecycle state that provides state transition callbacks.
- [WidgetsBindingObserver], for a mechanism to observe the lifecycle state from the widgets layer.
- iOS's [UIKit activity lifecycle](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle?language=objc) documentation.
- Android's [activity lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle) documentation.
- macOS's [AppKit activity lifecycle](https://developer.apple.com/documentation/appkit/nsapplicationdelegate?language=objc) documentation.

The application is still hosted by a Flutter engine but is detached from any host views.

The application defaults to this state before it initializes, and can be in this state (applicable on Android, iOS, and web) after all views have been detached.

When the application is in this state, the engine is running without a view.

This state is only entered on iOS, Android, and web, although on all platforms it is the default state before the application begins running.

On all platforms, this state indicates that the application is in the default running mode for a running application that has input focus and is visible.

On Android, this state corresponds to the Flutter host view having focus ([`Activity.onWindowFocusChanged`](<https://developer.android.com/reference/android/app/Activity#onWindowFocusChanged(boolean)>) was called with true) while in Android's "resumed" state. It is possible for the Flutter app to be in the [inactive] state while still being in Android's ["onResume"](https://developer.android.com/guide/components/activities/activity-lifecycle) state if the app has lost focus ([`Activity.onWindowFocusChanged`](<https://developer.android.com/reference/android/app/Activity#onWindowFocusChanged(boolean)>) was called with false), but hasn't had [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>) called on it.

On iOS and macOS, this corresponds to the app running in the foreground active state.

At least one view of the application is visible, but none have input focus. The application is otherwise running normally.

On non-web desktop platforms, this corresponds to an application that is not in the foreground, but still has visible windows.

On the web, this corresponds to an application that is running in a window or tab that does not have input focus.

On iOS and macOS, this state corresponds to the Flutter host view running in the foreground inactive state. Apps transition to this state when in a phone call, when responding to a TouchID request, when entering the app switcher or the control center, or when the UIViewController hosting the Flutter app is transitioning.

On Android, this corresponds to the Flutter host view running in Android's paused state (i.e. [`Activity.onPause`](<https://developer.android.com/reference/android/app/Activity#onPause()>) has been called), or in Android's "resumed" state (i.e. [`Activity.onResume`](<https://developer.android.com/reference/android/app/Activity#onResume()>) has been called) but does not have window focus. Examples of when apps transition to this state include when the app is partially obscured or another activity is focused, a app running in a split screen that isn't the current app, an app interrupted by a phone call, a picture-in-picture app, a system dialog, another view. It will also be inactive when the notification window shade is down, or the application switcher is visible.

On Android and iOS, apps in this state should assume that they may be [hidden] and [paused] at any time.

All views of an application are hidden, either because the application is about to be paused (on iOS and Android), or because it has been minimized or placed on a desktop that is no longer visible (on non-web desktop), or is running in a window or tab that is no longer visible (on the web).

On iOS and Android, in order to keep the state machine the same on all platforms, a transition to this state is synthesized before the [paused] state is entered when coming from [inactive], and before the [inactive] state is entered when coming from [paused]. This allows cross-platform implementations that want to know when an app is conceptually "hidden" to only write one handler.

The application is not currently visible to the user, and not responding to user input.

When the application is in this state, the engine will not call the [PlatformDispatcher.onBeginFrame] and [PlatformDispatcher.onDrawFrame] callbacks.

This state is only entered on iOS and Android.

# AppExitResponse

```dart
enum AppExitResponse {}
```

The possible responses to a request to exit the application.

The request is typically responded to by creating an [AppLifecycleListener] and supplying an [AppLifecycleListener.onExitRequested] callback, or by overriding [WidgetsBindingObserver.didRequestAppExit].

Exiting the application can proceed.

Cancel the exit: do not exit the application.

# AppExitType

```dart
enum AppExitType {}
```

The type of application exit to perform when calling [ServicesBinding.exitApplication].

Requests that the application start an orderly exit, sending a request back to the framework through the [WidgetsBinding]. If that responds with [AppExitResponse.exit], then proceed with the same steps as a [required] exit. If that responds with [AppExitResponse.cancel], then the exit request is canceled and the application continues executing normally.

A non-cancelable orderly exit request. The engine will shut down the engine and call the native UI toolkit's exit API.

If you need an even faster and more dangerous exit, then call `dart:io`'s `exit()` directly, and even the native toolkit's exit API won't be called. This is quite dangerous, though, since it's possible that the engine will crash because it hasn't been properly shut down, causing the app to crash on exit.

# ViewPadding

```dart
class ViewPadding {}
```

A representation of distances for each of the four edges of a rectangle, used to encode the view insets and padding that applications should place around their user interface, as exposed by [FlutterView.viewInsets] and [FlutterView.padding]. View insets and padding are preferably read via [MediaQuery.of].

For a generic class that represents distances around a rectangle, see the [EdgeInsets] class.

See also:

- [WidgetsBindingObserver], for a widgets layer mechanism to receive notifications when the padding changes.
- [MediaQuery.of], for the preferred mechanism for accessing these values.
- [Scaffold], which automatically applies the padding in material design applications.

### left

```dart
double left
```

The distance from the left edge to the first unpadded pixel, in physical pixels.

### top

```dart
double top
```

The distance from the top edge to the first unpadded pixel, in physical pixels.

### right

```dart
double right
```

The distance from the right edge to the first unpadded pixel, in physical pixels.

### bottom

```dart
double bottom
```

The distance from the bottom edge to the first unpadded pixel, in physical pixels.

### zero

```dart
ViewPadding zero
```

A view padding that has zeros for each edge.

### toString()

```dart
String toString()
```

# WindowPadding

```dart
typedef WindowPadding = ViewPadding
```

Deprecated. Will be removed in a future version of Flutter.

Use [ViewPadding] instead.

# ViewConstraints

```dart
class ViewConstraints {}
```

Immutable layout constraints for [FlutterView]s.

Similar to [BoxConstraints], a [Size] respects a [ViewConstraints] if, and only if, all of the following relations hold:

- [minWidth] <= [Size.width] <= [maxWidth]
- [minHeight] <= [Size.height] <= [maxHeight]

The constraints themselves must satisfy these relations:

- 0.0 <= [minWidth] <= [maxWidth] <= [double.infinity]
- 0.0 <= [minHeight] <= [maxHeight] <= [double.infinity]

For each constraint, [double.infinity] is a legal value.

For a generic class that represents these kind of constraints, see the [BoxConstraints] class.

### ViewConstraints()

```dart
ViewConstraints({double minWidth = 0.0, double maxWidth = double.infinity, double minHeight = 0.0, double maxHeight = double.infinity})
```

Creates view constraints with the given constraints.

### ViewConstraints.tight()

```dart
ViewConstraints.tight(Size size)
```

Creates view constraints that is respected only by the given size.

### minWidth

```dart
double minWidth
```

The minimum width that satisfies the constraints.

### maxWidth

```dart
double maxWidth
```

The maximum width that satisfies the constraints.

Might be [double.infinity].

### minHeight

```dart
double minHeight
```

The minimum height that satisfies the constraints.

### maxHeight

```dart
double maxHeight
```

The maximum height that satisfies the constraints.

Might be [double.infinity].

### isSatisfiedBy()

```dart
bool isSatisfiedBy(Size size)
```

Whether the given size satisfies the constraints.

### isTight

```dart
bool get isTight
```

Whether there is exactly one size that satisfies the constraints.

### operator /()

```dart
ViewConstraints operator /(double factor)
```

Scales each constraint parameter by the inverse of the given factor.

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

# DisplayFeature

```dart
class DisplayFeature {}
```

Area of the display that may be obstructed by a hardware feature.

This is populated only on Android.

The [bounds] are measured in logical pixels. On devices with two screens the coordinate system starts with (0,0) in the top-left corner of the left or top screen and expands to include both screens and the visual space between them.

The [type] describes the behaviour and if [DisplayFeature] obstructs the display. For example, [DisplayFeatureType.hinge] and [DisplayFeatureType.cutout] both obstruct the display, while [DisplayFeatureType.fold] does not.

![Device with a hinge display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_hinge.png)

![Device with a fold display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_fold.png)

![Device with a cutout display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_cutout.png)

The [state] contains information about the posture for foldable features ([DisplayFeatureType.hinge] and [DisplayFeatureType.fold]). The posture is the shape of the display, for example [DisplayFeatureState.postureFlat] or [DisplayFeatureState.postureHalfOpened]. For [DisplayFeatureType.cutout], the state is not used and has the [DisplayFeatureState.unknown] value.

### DisplayFeature()

```dart
DisplayFeature({required Rect bounds, required DisplayFeatureType type, required DisplayFeatureState state})
```

### bounds

```dart
Rect bounds
```

The area of the flutter view occupied by this display feature, measured in logical pixels.

On devices with two screens, the Flutter view spans from the top-left corner of the left or top screen to the bottom-right corner of the right or bottom screen, including the visual area occupied by any display feature. Bounds of display features are reported in this coordinate system.

For example, on a dual screen device in portrait mode:

- [Rect.left] gives you the size of left screen, in logical pixels.
- [Rect.right] gives you the size of the left screen + the hinge width.

### type

```dart
DisplayFeatureType type
```

Type of display feature, e.g. hinge, fold, cutout.

### state

```dart
DisplayFeatureState state
```

Posture of display feature, which is populated only for folds and hinges.

For cutouts, this is [DisplayFeatureState.unknown]

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

# DisplayFeatureType

```dart
enum DisplayFeatureType {}
```

Type of [DisplayFeature], describing the [DisplayFeature] behaviour and if it obstructs the display.

Some types of [DisplayFeature], like [DisplayFeatureType.fold], can be reported without actually impeding drawing on the screen. They are useful for knowing where the display is bent or has a crease. The [DisplayFeature.bounds] can be 0-width in such cases.

The shape formed by the screens for types [DisplayFeatureType.fold] and [DisplayFeatureType.hinge] is called the posture and is exposed in [DisplayFeature.state]. For example, the [DisplayFeatureState.postureFlat] posture means the screens form a flat surface.

![Device with a hinge display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_hinge.png)

![Device with a fold display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_fold.png)

![Device with a cutout display feature](https://flutter.github.io/assets-for-api-docs/assets/hardware/display_feature_cutout.png)

[DisplayFeature] type is new and not yet known to Flutter.

A fold in the flexible screen without a physical gap.

The bounds for this display feature type indicate where the display makes a crease.

A physical separation with a hinge that allows two display panels to fold.

A non-displaying area of the screen, usually housing cameras or sensors.

# DisplayFeatureState

```dart
enum DisplayFeatureState {}
```

State of the display feature, which contains information about the posture for foldable features.

The posture is the shape made by the parts of the flexible screen or physical screen panels. They are inspired by and similar to [Android Postures](https://developer.android.com/guide/topics/ui/foldables#postures).

- For [DisplayFeatureType.fold]s & [DisplayFeatureType.hinge]s, the state is the posture.
- For [DisplayFeatureType.cutout]s, the state is not used and has the [DisplayFeatureState.unknown] value.

The display feature is a [DisplayFeatureType.cutout] or this state is new and not yet known to Flutter.

The foldable device is completely open.

The screen space that is presented to the user is flat.

Fold angle is in an intermediate position between opened and closed state.

There is a non-flat angle between parts of the flexible screen or between physical screen panels such that the screens start to face each other.

# DisplayCornerRadii

```dart
class DisplayCornerRadii {}
```

A set of radii for the four corners of the display.

This class represents the curvature of the display corners. The radii values are defined in physical pixels.

If a corner is square (not rounded), the radius is 0.0.

This is currently populated only on Android API 31+.

### DisplayCornerRadii()

```dart
DisplayCornerRadii({required double topLeft, required double topRight, required double bottomRight, required double bottomLeft})
```

Creates a [DisplayCornerRadii].

### topLeft

```dart
double topLeft
```

The radius of the top-left corner of the display, in physical pixels.

### topRight

```dart
double topRight
```

The radius of the top-right corner of the display, in physical pixels.

### bottomRight

```dart
double bottomRight
```

The radius of the bottom-right corner of the display, in physical pixels.

### bottomLeft

```dart
double bottomLeft
```

The radius of the bottom-left corner of the display, in physical pixels.

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

# Locale

```dart
class Locale {}
```

An identifier used to select a user's language and formatting preferences.

This represents a [Unicode Language Identifier](https://www.unicode.org/reports/tr35/#Unicode_language_identifier) (i.e. without Locale extensions), except variants are not supported.

Locales are canonicalized according to the "preferred value" entries in the [IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry). For example, `const Locale('he')` and `const Locale('iw')` are equal and both have the [languageCode] `he`, because `iw` is a deprecated language subtag that was replaced by the subtag `he`.

See also:

- [PlatformDispatcher.locale], which specifies the system's currently selected [Locale].

### Locale()

```dart
Locale(String _languageCode, [String? _countryCode])
```

Creates a new Locale object. The first argument is the primary language subtag, the second is the region (also referred to as 'country') subtag.

For example:

```dart
const Locale swissFrench = Locale('fr', 'CH');
const Locale canadianFrench = Locale('fr', 'CA');
```

The primary language subtag must not be null. The region subtag is optional. When there is no region/country subtag, the parameter should be omitted or passed `null` instead of an empty-string.

The subtag values are _case sensitive_ and must be one of the valid subtags according to CLDR supplemental data: [language](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml), [region](https://github.com/unicode-org/cldr/blob/master/common/validity/region.xml). The primary language subtag must be at least two and at most eight lowercase letters, but not four letters. The region subtag must be two uppercase letters or three digits. See the [Unicode Language Identifier](https://www.unicode.org/reports/tr35/#Unicode_language_identifier) specification.

Validity is not checked by default, but some methods may throw away invalid data.

See also:

- [Locale.fromSubtags], which also allows a [scriptCode] to be specified.

### Locale.fromSubtags()

```dart
Locale.fromSubtags({String languageCode = 'und', String? scriptCode, String? countryCode})
```

Creates a new Locale object.

The keyword arguments specify the subtags of the Locale.

The subtag values are _case sensitive_ and must be valid subtags according to CLDR supplemental data: [language](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml), [script](https://github.com/unicode-org/cldr/blob/master/common/validity/script.xml) and [region](https://github.com/unicode-org/cldr/blob/master/common/validity/region.xml) for each of languageCode, scriptCode and countryCode respectively.

The [languageCode] subtag is optional. When there is no language subtag, the parameter should be omitted or set to "und". When not supplied, the [languageCode] defaults to "und", an undefined language code.

The [countryCode] subtag is optional. When there is no country subtag, the parameter should be omitted or passed `null` instead of an empty-string.

Validity is not checked by default, but some methods may throw away invalid data.

### languageCode

```dart
String get languageCode
```

The primary language subtag for the locale.

This must not be null. It may be 'und', representing 'undefined'.

This is expected to be string registered in the [IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) with the type "language". The string specified must match the case of the string in the registry.

Language subtags that are deprecated in the registry and have a preferred code are changed to their preferred code. For example, `const Locale('he')` and `const Locale('iw')` are equal, and both have the [languageCode] `he`, because `iw` is a deprecated language subtag that was replaced by the subtag `he`.

This must be a valid Unicode Language subtag as listed in [Unicode CLDR supplemental data](https://github.com/unicode-org/cldr/blob/master/common/validity/language.xml).

See also:

- [Locale.fromSubtags], which describes the conventions for creating [Locale] objects.

### scriptCode

```dart
String? scriptCode
```

The script subtag for the locale.

This may be null, indicating that there is no specified script subtag.

This must be a valid Unicode Language Identifier script subtag as listed in [Unicode CLDR supplemental data](https://github.com/unicode-org/cldr/blob/master/common/validity/script.xml).

See also:

- [Locale.fromSubtags], which describes the conventions for creating [Locale] objects.

### countryCode

```dart
String? get countryCode
```

The region subtag for the locale.

This may be null, indicating that there is no specified region subtag.

This is expected to be string registered in the [IANA Language Subtag Registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) with the type "region". The string specified must match the case of the string in the registry.

Region subtags that are deprecated in the registry and have a preferred code are changed to their preferred code. For example, `const Locale('de', 'DE')` and `const Locale('de', 'DD')` are equal, and both have the [countryCode] `DE`, because `DD` is a deprecated language subtag that was replaced by the subtag `DE`.

See also:

- [Locale.fromSubtags], which describes the conventions for creating [Locale] objects.

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

Returns a string representing the locale.

This identifier happens to be a valid Unicode Locale Identifier using underscores as separator, however it is intended to be used for debugging purposes only. For parsable results, use [toLanguageTag] instead.

### toLanguageTag()

```dart
String toLanguageTag()
```

Returns a syntactically valid Unicode BCP47 Locale Identifier.

Some examples of such identifiers: "en", "es-419", "hi-Deva-IN" and "zh-Hans-CN". See http://www.unicode.org/reports/tr35/ for technical details.

# DartPerformanceMode

```dart
enum DartPerformanceMode {}
```

Various performance modes for tuning the Dart VM's GC performance.

For the editor of this enum, please keep the order in sync with `Dart_PerformanceMode` in [dart_api.h](https://github.com/dart-lang/sdk/blob/main/runtime/include/dart_api.h#L1302).

This is the default mode that the Dart VM is in.

Optimize for low latency, at the expense of throughput and memory overhead by performing work in smaller batches (requiring more overhead) or by delaying work (requiring more memory). An embedder should not remain in this mode indefinitely.

Optimize for high throughput, at the expense of latency and memory overhead by performing work in larger batches with more intervening growth.

Optimize for low memory, at the expensive of throughput and latency by more frequently performing work.

# SemanticsActionEvent

```dart
class SemanticsActionEvent {}
```

An event to request a [SemanticsAction] of [type] to be performed on the [SemanticsNode] identified by [nodeId] owned by the [FlutterView] identified by [viewId].

Used by [SemanticsBinding.performSemanticsAction].

### SemanticsActionEvent()

```dart
SemanticsActionEvent({required SemanticsAction type, required int viewId, required int nodeId, Object? arguments})
```

Creates a [SemanticsActionEvent].

### type

```dart
SemanticsAction type
```

The type of action to be performed.

### viewId

```dart
int viewId
```

The id of the [FlutterView] the [SemanticsNode] identified by [nodeId] is associated with.

### nodeId

```dart
int nodeId
```

The id of the [SemanticsNode] on which the action is to be performed.

### arguments

```dart
Object? arguments
```

Optional arguments for the action.

### copyWith()

```dart
SemanticsActionEvent copyWith({SemanticsAction? type, int? viewId, int? nodeId, Object? arguments = _noArgumentPlaceholder})
```

Create a clone of the [SemanticsActionEvent] but with provided parameters replaced.

# ViewFocusChangeCallback

```dart
typedef ViewFocusChangeCallback = void Function(ViewFocusEvent viewFocusEvent)
```

Signature for [PlatformDispatcher.onViewFocusChange].

# ViewFocusEvent

```dart
final class ViewFocusEvent {}
```

An event for the engine to communicate view focus changes to the app.

This value will be typically passed to the [PlatformDispatcher.onViewFocusChange] callback.

### ViewFocusEvent()

```dart
ViewFocusEvent({required int viewId, required ViewFocusState state, required ViewFocusDirection direction})
```

Creates a [ViewFocusChange].

### viewId

```dart
int viewId
```

The ID of the [FlutterView] that experienced a focus change.

### state

```dart
ViewFocusState state
```

The state focus changed to.

### direction

```dart
ViewFocusDirection direction
```

The direction focus changed to.

### toString()

```dart
String toString()
```

# ViewFocusState

```dart
enum ViewFocusState {}
```

Represents the focus state of a given [FlutterView].

When focus is lost, the view's focus state changes to [ViewFocusState.unfocused].

When focus is gained, the view's focus state changes to [ViewFocusState.focused].

Valid transitions within a view are:

- [ViewFocusState.focused] to [ViewFocusState.unfocused].
- [ViewFocusState.unfocused] to [ViewFocusState.focused].

See also:

- [ViewFocusDirection], that specifies the focus direction.
- [ViewFocusEvent], that conveys information about a [FlutterView] focus change.

Specifies that a view does not have platform focus.

Specifies that a view has platform focus.

# ViewFocusDirection

```dart
enum ViewFocusDirection {}
```

Represents the direction in which the focus transitioned across [FlutterView]s.

See also:

- [ViewFocusState], that specifies the current focus state of a [FlutterView].
- [ViewFocusEvent], that conveys information about a [FlutterView] focus change.

Indicates the focus transition did not have a direction.

This is typically associated with focus being programmatically requested or when focus is lost.

Indicates the focus transition was performed in a forward direction.

This is typically result of the user pressing tab.

Indicates the focus transition was performed in a backward direction.

This is typically result of the user pressing shift + tab.

# HitTestRequest

```dart
class HitTestRequest {}
```

A request to evaluate the content of a view at a specific position.

See also:

- [PlatformDispatcher.onHitTest], the callback that the platform invokes to hit test a view at a specific position.
- [HitTestResponse], the result of a hit test request.

### HitTestRequest()

```dart
HitTestRequest({required FlutterView view, required Offset offset})
```

Creates a hit test request.

### view

```dart
FlutterView view
```

The view that should be hit tested.

### offset

```dart
Offset offset
```

The position in the [view] that should be hit tested.

# HitTestResponse

```dart
class HitTestResponse {}
```

The results of hit testing a view at a specific position.

See also:

- [PlatformDispatcher.onHitTest], the callback that the platform invokes to hit test a view at a specific position.
- [HitTestRequest], the request to hit test a view at a specific position.

### HitTestResponse()

```dart
HitTestResponse({required bool hasPlatformView})
```

Creates a hit test response.

### empty

```dart
HitTestResponse empty
```

A response with no hit entries.

### hasPlatformView

```dart
bool hasPlatformView
```

Whether the hit test result contains a platform view.

See also:

- [NativeHitTestTarget], the Flutter framework mixin that represents a hit test target backed by a platform view.
