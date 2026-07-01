@docImport 'dart:ui'; @docImport 'package:flutter/animation.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'adapter.dart'; @docImport 'app_lifecycle_listener.dart'; @docImport 'basic.dart'; @docImport 'focus_scope.dart'; @docImport 'media_query.dart'; @docImport 'navigator.dart'; @docImport 'pop_scope.dart';

# WidgetsBindingObserver

```dart
abstract mixin class WidgetsBindingObserver {}
```

Interface for classes that register with the Widgets layer binding.

This can be used by any class, not just widgets. It provides an interface which is used by [WidgetsBinding.addObserver] and [WidgetsBinding.removeObserver] to notify objects of changes in the environment, such as changes to the device metrics or accessibility settings. It is used to implement features such as [MediaQuery].

This class can be extended directly, or mixed in, to get default behaviors for all of the handlers. Alternatively it can be used with the `implements` keyword, in which case all the handlers must be implemented (and the analyzer will list those that have been omitted).

To start receiving notifications, call `WidgetsBinding.instance.addObserver` with a reference to the object implementing the [WidgetsBindingObserver] interface. To avoid memory leaks, call `WidgetsBinding.instance.removeObserver` to unregister the object when it reaches the end of its lifecycle.

{@tool dartpad} This sample shows how to implement parts of the [State] and [WidgetsBindingObserver] protocols necessary to react to application lifecycle messages. See [didChangeAppLifecycleState].

To respond to other notifications, replace the [didChangeAppLifecycleState] method in this example with other methods from this class.

** See code in examples/api/lib/widgets/binding/widget_binding_observer.0.dart ** {@end-tool}

### didPopRoute()

```dart
Future<bool> didPopRoute()
```

Called when the system tells the app to pop the current route, such as after a system back button press or back gesture.

Observers are notified in registration order until one returns true. If none return true, the application quits.

Observers are expected to return true if they were able to handle the notification, for example by closing an active dialog box, and false otherwise. The [WidgetsApp] widget uses this mechanism to notify the [Navigator] widget that it should pop its current route if possible.

This method exposes the `popRoute` notification from [SystemChannels.navigation].

{@macro flutter.widgets.AndroidPredictiveBack}

### handleStartBackGesture()

```dart
bool handleStartBackGesture(PredictiveBackEvent backEvent)
```

Called at the start of a predictive back gesture.

Observers are notified in registration order until one returns true or all observers have been notified. If an observer returns true then that observer, and only that observer, will be notified of subsequent events in this same gesture (for example [handleUpdateBackGestureProgress], etc.).

Observers are expected to return true if they were able to handle the notification, for example by starting a predictive back animation, and false otherwise. [PredictiveBackPageTransitionsBuilder] uses this mechanism to listen for predictive back gestures.

If all observers indicate they are not handling this back gesture by returning false, then a navigation pop will result when [handleCommitBackGesture] is called, as in a non-predictive system back gesture.

Currently, this is only used on Android devices that support the predictive back feature.

### handleUpdateBackGestureProgress()

```dart
void handleUpdateBackGestureProgress(PredictiveBackEvent backEvent)
```

Called when a predictive back gesture moves.

The observer which was notified of this gesture's [handleStartBackGesture] is the same observer notified for this.

Currently, this is only used on Android devices that support the predictive back feature.

### handleCommitBackGesture()

```dart
void handleCommitBackGesture()
```

Called when a predictive back gesture is finished successfully, indicating that the current route should be popped.

The observer which was notified of this gesture's [handleStartBackGesture] is the same observer notified for this. If there is none, then a navigation pop will result, as in a non-predictive system back gesture.

Currently, this is only used on Android devices that support the predictive back feature.

### handleCancelBackGesture()

```dart
void handleCancelBackGesture()
```

Called when a predictive back gesture is canceled, indicating that no navigation should occur.

The observer which was notified of this gesture's [handleStartBackGesture] is the same observer notified for this.

Currently, this is only used on Android devices that support the predictive back feature.

### handleStatusBarTap()

```dart
void handleStatusBarTap()
```

Called when the user taps the status bar on iOS, to scroll a scroll view to the top.

This event should usually only be handled by at most one scroll view, so implementer(s) of this callback must coordinate to determine the most suitable scroll view for handling this event.

This callback is only called on iOS. The default implementation provided by [WidgetsBindingObserver] does nothing.

See also:

- [Scaffold] and [CupertinoPageScaffold] which use this callback to implement iOS scroll-to-top.

### didPushRoute()

```dart
Future<bool> didPushRoute(String route)
```

Called when the host tells the application to push a new route onto the navigator.

Observers are expected to return true if they were able to handle the notification. Observers are notified in registration order until one returns true.

This method exposes the `pushRoute` notification from [SystemChannels.navigation].

### didPushRouteInformation()

```dart
Future<bool> didPushRouteInformation(RouteInformation routeInformation)
```

Called when the host tells the application to push a new [RouteInformation] and a restoration state onto the router.

Observers are expected to return true if they were able to handle the notification. Observers are notified in registration order until one returns true.

This method exposes the `pushRouteInformation` notification from [SystemChannels.navigation].

The default implementation is to call the [didPushRoute] directly with the string constructed from [RouteInformation.uri]'s path and query parameters.

### didChangeMetrics()

```dart
void didChangeMetrics()
```

Called when the application's dimensions change. For example, when a phone is rotated.

This method exposes notifications from [dart:ui.PlatformDispatcher.onMetricsChanged].

{@tool snippet}

This [StatefulWidget] implements the parts of the [State] and [WidgetsBindingObserver] protocols necessary to react when the device is rotated (or otherwise changes dimensions).

```dart
class MetricsReactor extends StatefulWidget {
  const MetricsReactor({ super.key });

  @override
  State<MetricsReactor> createState() => _MetricsReactorState();
}

class _MetricsReactorState extends State<MetricsReactor> with WidgetsBindingObserver {
  late Size _lastSize;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    // [View.of] exposes the view from `WidgetsBinding.instance.platformDispatcher.views`
    // into which this widget is drawn.
    _lastSize = View.of(context).physicalSize;
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeMetrics() {
    setState(() { _lastSize = View.of(context).physicalSize; });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Current size: $_lastSize');
  }
}
```

{@end-tool}

In general, this is unnecessary as the layout system takes care of automatically recomputing the application geometry when the application size changes.

See also:

- [MediaQuery.sizeOf], which provides a similar service with less boilerplate.

### didChangeTextScaleFactor()

```dart
void didChangeTextScaleFactor()
```

Called when the platform's text scale factor changes.

This typically happens as the result of the user changing system preferences, and it should affect all of the text sizes in the application.

This method exposes notifications from [dart:ui.PlatformDispatcher.onTextScaleFactorChanged].

{@tool snippet}

```dart
class TextScaleFactorReactor extends StatefulWidget {
  const TextScaleFactorReactor({super.key});

  @override
  State<TextScaleFactorReactor> createState() => _TextScaleFactorReactorState();
}

class _TextScaleFactorReactorState extends State<TextScaleFactorReactor>
    with WidgetsBindingObserver {
  double _lastTextScaleFactor =
      WidgetsBinding.instance.platformDispatcher.textScaleFactor;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeTextScaleFactor() {
    setState(() {
      _lastTextScaleFactor =
          WidgetsBinding.instance.platformDispatcher.textScaleFactor;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Current scale factor: $_lastTextScaleFactor');
  }
}
```

{@end-tool}

See also:

- [MediaQuery.textScaleFactorOf], which provides a similar service with less boilerplate.

### didChangePlatformBrightness()

```dart
void didChangePlatformBrightness()
```

Called when the platform brightness changes.

This method exposes notifications from [dart:ui.PlatformDispatcher.onPlatformBrightnessChanged].

See also:

- [MediaQuery.platformBrightnessOf], which provides a similar service with less boilerplate.

### didChangeLocales()

```dart
void didChangeLocales(List<Locale>? locales)
```

Called when the system tells the app that the user's locale has changed. For example, if the user changes the system language settings.

This method exposes notifications from [dart:ui.PlatformDispatcher.onLocaleChanged].

### didChangeAppLifecycleState()

```dart
void didChangeAppLifecycleState(AppLifecycleState state)
```

Called when the system puts the app in the background or returns the app to the foreground.

An example of implementing this method is provided in the class-level documentation for the [WidgetsBindingObserver] class.

This method exposes notifications from [SystemChannels.lifecycle].

See also:

- [AppLifecycleListener], an alternative API for responding to application lifecycle changes.

### didChangeViewFocus()

```dart
void didChangeViewFocus(ViewFocusEvent event)
```

Called whenever the [PlatformDispatcher] receives a notification that the focus state on a view has changed.

The [event] contains the view ID for the view that changed its focus state.

The view ID of the [FlutterView] in which a particular [BuildContext] resides can be retrieved with `View.of(context).viewId`, so that it may be compared with the view ID in the `event` to see if the event pertains to the given context.

### didRequestAppExit()

```dart
Future<AppExitResponse> didRequestAppExit()
```

Called when a request is received from the system to exit the application.

If any observer responds with [AppExitResponse.cancel], it will cancel the exit. All observers will be asked before exiting.

{@macro flutter.services.binding.ServicesBinding.requestAppExit}

See also:

- [ServicesBinding.exitApplication] for a function to call that will request that the application exits.

### didHaveMemoryPressure()

```dart
void didHaveMemoryPressure()
```

Called when the system is running low on memory.

This method exposes the `memoryPressure` notification from [SystemChannels.system].

### didChangeAccessibilityFeatures()

```dart
void didChangeAccessibilityFeatures()
```

Called when the system changes the set of currently active accessibility features.

This method exposes notifications from [dart:ui.PlatformDispatcher.onAccessibilityFeaturesChanged].

# WidgetsBinding

```dart
mixin WidgetsBinding on BindingBase, ServicesBinding, SchedulerBinding, GestureBinding, RendererBinding, SemanticsBinding {}
```

The glue between the widgets layer and the Flutter engine.

The [WidgetsBinding] manages a single [Element] tree rooted at [rootElement]. Calling [runApp] (which indirectly calls [attachRootWidget]) bootstraps that element tree.

## Relationship to render trees

Multiple render trees may be associated with the element tree. Those are managed by the underlying [RendererBinding].

The element tree is segmented into two types of zones: rendering zones and non-rendering zones.

A rendering zone is a part of the element tree that is backed by a render tree and it describes the pixels that are drawn on screen. For elements in this zone, [Element.renderObject] never returns null because the elements are all associated with [RenderObject]s. Almost all widgets can be placed in a rendering zone; notable exceptions are the [View] widget, [ViewCollection] widget, and [RootWidget].

A non-rendering zone is a part of the element tree that is not backed by a render tree. For elements in this zone, [Element.renderObject] returns null because the elements are not associated with any [RenderObject]s. Only widgets that do not produce a [RenderObject] can be used in this zone because there is no render tree to attach the render object to. In other words, [RenderObjectWidget]s cannot be used in this zone. Typically, one would find [InheritedWidget]s, [View]s, and [ViewCollection]s in this zone to inject data across rendering zones into the tree and to organize the rendering zones (and by extension their associated render trees) into a unified element tree.

The root of the element tree at [rootElement] starts a non-rendering zone. Within a non-rendering zone, the [View] widget is used to start a rendering zone by bootstrapping a render tree. Within a rendering zone, the [ViewAnchor] can be used to start a new non-rendering zone.

To figure out if an element is in a rendering zone it may walk up the tree calling [Element.debugExpectsRenderObjectForSlot] on its ancestors. If it reaches an element that returns false, it is in a non-rendering zone. If it reaches a [RenderObjectElement] ancestor it is in a rendering zone.

### initInstances()

```dart
void initInstances()
```

### instance

```dart
WidgetsBinding get instance
```

The current [WidgetsBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### debugShowWidgetInspectorOverride

```dart
bool get debugShowWidgetInspectorOverride
```

If true, forces the widget inspector to be visible.

Overrides the `debugShowWidgetInspector` value set in [WidgetsApp].

Used by the `debugShowWidgetInspector` debugging extension.

The inspector allows the selection of a location on your device or emulator and view what widgets and render objects associated with it. An outline of the selected widget and some summary information is shown on device and more detailed information is shown in the IDE or DevTools.

### debugShowWidgetInspectorOverride

```dart
set debugShowWidgetInspectorOverride(bool value)
```

### debugShowWidgetInspectorOverrideNotifier

```dart
ValueNotifier<bool> get debugShowWidgetInspectorOverrideNotifier
```

Notifier for [debugShowWidgetInspectorOverride].

### debugWidgetInspectorSelectionOnTapEnabled

```dart
ValueNotifier<bool> get debugWidgetInspectorSelectionOnTapEnabled
```

The notifier for whether or not taps on the device are treated as widget selections when the widget inspector is enabled.

- If true, taps in the app are intercepted by the widget inspector.
- If false, taps in the app are not intercepted by the widget inspector.

### debugExcludeRootWidgetInspector

```dart
bool get debugExcludeRootWidgetInspector
```

If true, [WidgetInspector] will not be automatically injected into the widget tree.

This overrides the behavior where [WidgetInspector] is added to the widget tree created by [WidgetsApp] when the `debugShowWidgetInspector` value is set in [WidgetsApp] or [debugShowWidgetInspectorOverride] is set to true.

Used by tools that want more control over which widgets can be selected and highlighted by the widget inspector by manually injecting instances of [WidgetInspector].

### debugExcludeRootWidgetInspector

```dart
set debugExcludeRootWidgetInspector(bool value)
```

### resetInternalState()

```dart
void resetInternalState()
```

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### buildOwner

```dart
BuildOwner? get buildOwner
```

The [BuildOwner] in charge of executing the build pipeline for the widget tree rooted at this binding.

### focusManager

```dart
FocusManager get focusManager
```

The object in charge of the focus tree.

Rarely used directly. Instead, consider using [FocusScope.of] to obtain the [FocusScopeNode] for a given [BuildContext].

See [FocusManager] for more details.

### platformMenuDelegate

```dart
PlatformMenuDelegate platformMenuDelegate
```

A delegate that communicates with a platform plugin for serializing and managing platform-rendered menu bars created by [PlatformMenuBar].

This is set by default to a [DefaultPlatformMenuDelegate] instance in [initInstances].

### addObserver()

```dart
void addObserver(WidgetsBindingObserver observer)
```

Registers the given object as a binding observer. Binding observers are notified when various application events occur, for example when the system locale changes. Generally, one widget in the widget tree registers itself as a binding observer, and converts the system state into inherited widgets.

For example, the [WidgetsApp] widget registers as a binding observer and passes the screen size to a [MediaQuery] widget each time it is built, which enables other widgets to use the [MediaQuery.sizeOf] static method and (implicitly) the [InheritedWidget] mechanism to be notified whenever the screen size changes (e.g. whenever the screen rotates).

See also:

- [removeObserver], to release the resources reserved by this method.
- [WidgetsBindingObserver], which has an example of using this method.

### removeObserver()

```dart
bool removeObserver(WidgetsBindingObserver observer)
```

Unregisters the given observer. This should be used sparingly as it is relatively expensive (O(N) in the number of registered observers).

See also:

- [addObserver], for the method that adds observers in the first place.
- [WidgetsBindingObserver], which has an example of using this method.

### handleRequestAppExit()

```dart
Future<AppExitResponse> handleRequestAppExit()
```

### handleMetricsChanged()

```dart
void handleMetricsChanged()
```

### handleTextScaleFactorChanged()

```dart
void handleTextScaleFactorChanged()
```

### handlePlatformBrightnessChanged()

```dart
void handlePlatformBrightnessChanged()
```

### handleAccessibilityFeaturesChanged()

```dart
void handleAccessibilityFeaturesChanged()
```

### handleLocaleChanged()

```dart
void handleLocaleChanged()
```

Called when the system locale changes.

Calls [dispatchLocalesChanged] to notify the binding observers.

See [dart:ui.PlatformDispatcher.onLocaleChanged].

### dispatchLocalesChanged()

```dart
void dispatchLocalesChanged(List<Locale>? locales)
```

Notify all the observers that the locale has changed (using [WidgetsBindingObserver.didChangeLocales]), giving them the `locales` argument.

This is called by [handleLocaleChanged] when the [PlatformDispatcher.onLocaleChanged] notification is received.

### dispatchAccessibilityFeaturesChanged()

```dart
void dispatchAccessibilityFeaturesChanged()
```

Notify all the observers that the active set of [AccessibilityFeatures] has changed (using [WidgetsBindingObserver.didChangeAccessibilityFeatures]), giving them the `features` argument.

This is called by [handleAccessibilityFeaturesChanged] when the [PlatformDispatcher.onAccessibilityFeaturesChanged] notification is received.

### handlePopRoute()

```dart
Future<bool> handlePopRoute()
```

Called when the system pops the current route.

This first notifies the binding observers (using [WidgetsBindingObserver.didPopRoute]), in registration order, until one returns true, meaning that it was able to handle the request (e.g. by closing a dialog box). If none return true, then the application is shut down by calling [SystemNavigator.pop].

[WidgetsApp] uses this in conjunction with a [Navigator] to cause the back button to close dialog boxes, return from modal pages, and so forth.

This method exposes the `popRoute` notification from [SystemChannels.navigation].

{@template flutter.widgets.AndroidPredictiveBack}

## Handling backs ahead of time

Not all system backs will result in a call to this method. Some are handled entirely by the system without informing the Flutter framework.

Android API 33+ introduced a feature called predictive back, which allows the user to peek behind the current app or route during a back gesture and then decide to cancel or commit the back. Flutter enables or disables this feature ahead of time, before a back gesture occurs, and back gestures that trigger predictive back are handled entirely by the system and do not trigger this method here in the framework.

By default, the framework communicates when it would like to handle system back gestures using [SystemNavigator.setFrameworkHandlesBack] in [WidgetsApp]. This is done automatically based on the status of the [Navigator] stack and the state of any [PopScope] widgets present. Developers can manually set this by calling the method directly or by using [NavigationNotification]. {@endtemplate}

### handlePushRoute()

```dart
Future<bool> handlePushRoute(String route)
```

Called when the host tells the app to push a new route onto the navigator.

This notifies the binding observers (using [WidgetsBindingObserver.didPushRoute]), in registration order, until one returns true, meaning that it was able to handle the request (e.g. by opening a dialog box). If none return true, then nothing happens.

This method exposes the `pushRoute` notification from [SystemChannels.navigation].

### handleAppLifecycleStateChanged()

```dart
void handleAppLifecycleStateChanged(AppLifecycleState state)
```

### handleViewFocusChanged()

```dart
void handleViewFocusChanged(ViewFocusEvent event)
```

### handleMemoryPressure()

```dart
void handleMemoryPressure()
```

### firstFrameRasterized

```dart
bool get firstFrameRasterized
```

Whether the Flutter engine has rasterized the first frame.

Usually, the time that a frame is rasterized is very close to the time that it gets presented on the display. Specifically, rasterization is the last expensive phase of a frame that's still in Flutter's control.

See also:

- [waitUntilFirstFrameRasterized], the future when [firstFrameRasterized] becomes true.

### waitUntilFirstFrameRasterized

```dart
Future<void> get waitUntilFirstFrameRasterized
```

A future that completes when the Flutter engine has rasterized the first frame.

Usually, the time that a frame is rasterized is very close to the time that it gets presented on the display. Specifically, rasterization is the last expensive phase of a frame that's still in Flutter's control.

See also:

- [firstFrameRasterized], whether this future has completed or not.

### debugDidSendFirstFrameEvent

```dart
bool get debugDidSendFirstFrameEvent
```

Whether the first frame has finished building.

This value can also be obtained over the VM service protocol as `ext.flutter.didSendFirstFrameEvent`.

See also:

- [firstFrameRasterized], whether the first frame has finished rendering.

### debugBuildingDirtyElements

```dart
bool debugBuildingDirtyElements
```

Whether we are currently in a frame. This is used to verify that frames are not scheduled redundantly.

This is public so that test frameworks can change it.

This flag is not used in release builds.

### drawFrame()

```dart
void drawFrame()
```

Pump the build and rendering pipeline to generate a frame.

This method is called by [handleDrawFrame], which itself is called automatically by the engine when it is time to lay out and paint a frame.

Each frame consists of the following phases:

1.  The animation phase: The [handleBeginFrame] method, which is registered with [PlatformDispatcher.onBeginFrame], invokes all the transient frame callbacks registered with [scheduleFrameCallback], in registration order. This includes all the [Ticker] instances that are driving [AnimationController] objects, which means all of the active [Animation] objects tick at this point.

2.  Microtasks: After [handleBeginFrame] returns, any microtasks that got scheduled by transient frame callbacks get to run. This typically includes callbacks for futures from [Ticker]s and [AnimationController]s that completed this frame.

After [handleBeginFrame], [handleDrawFrame], which is registered with [PlatformDispatcher.onDrawFrame], is called, which invokes all the persistent frame callbacks, of which the most notable is this method, [drawFrame], which proceeds as follows:

3.  The build phase: All the dirty [Element]s in the widget tree are rebuilt (see [State.build]). See [State.setState] for further details on marking a widget dirty for building. See [BuildOwner] for more information on this step.

4.  The layout phase: All the dirty [RenderObject]s in the system are laid out (see [RenderObject.performLayout]). See [RenderObject.markNeedsLayout] for further details on marking an object dirty for layout.

5.  The compositing bits phase: The compositing bits on any dirty [RenderObject] objects are updated. See [RenderObject.markNeedsCompositingBitsUpdate].

6.  The paint phase: All the dirty [RenderObject]s in the system are repainted (see [RenderObject.paint]). This generates the [Layer] tree. See [RenderObject.markNeedsPaint] for further details on marking an object dirty for paint.

7.  The compositing phase: The layer tree is turned into a [Scene] and sent to the GPU.

8.  The semantics phase: All the dirty [RenderObject]s in the system have their semantics updated (see [RenderObject.assembleSemanticsNode]). This generates the [SemanticsNode] tree. See [RenderObject.markNeedsSemanticsUpdate] for further details on marking an object dirty for semantics.

For more details on steps 4-8, see [PipelineOwner].

9. The finalization phase in the widgets layer: The widgets tree is finalized. This causes [State.dispose] to be invoked on any objects that were removed from the widgets tree this frame. See [BuildOwner.finalizeTree] for more details.

10. The finalization phase in the scheduler layer: After [drawFrame] returns, [handleDrawFrame] then invokes post-frame callbacks (registered with [addPostFrameCallback]).

### rootElement

```dart
Element? get rootElement
```

The [Element] that is at the root of the element tree hierarchy.

This is initialized the first time [runApp] is called.

### renderViewElement

```dart
Element? get renderViewElement
```

Deprecated. Will be removed in a future version of Flutter.

Use [rootElement] instead.

### framesEnabled

```dart
bool get framesEnabled
```

### wrapWithDefaultView()

```dart
Widget wrapWithDefaultView(Widget rootWidget)
```

Used by [runApp] to wrap the provided `rootWidget` in the default [View].

The [View] determines into what [FlutterView] the app is rendered into. This is currently [PlatformDispatcher.implicitView] from [platformDispatcher]. This method will throw a [StateError] if the [PlatformDispatcher.implicitView] is null.

The `rootWidget` widget provided to this method must not already be wrapped in a [View].

### scheduleAttachRootWidget()

```dart
void scheduleAttachRootWidget(Widget rootWidget)
```

Schedules a [Timer] for attaching the root widget.

This is called by [runApp] to configure the widget tree. Consider using [attachRootWidget] if you want to build the widget tree synchronously.

### attachRootWidget()

```dart
void attachRootWidget(Widget rootWidget)
```

Takes a widget and attaches it to the [rootElement], creating it if necessary.

This is called by [runApp] to configure the widget tree.

See also:

- [RenderObjectToWidgetAdapter.attachToRenderTree], which inflates a widget and attaches it to the render tree.

### attachToBuildOwner()

```dart
void attachToBuildOwner(RootWidget widget)
```

Called by [attachRootWidget] to attach the provided [RootWidget] to the [buildOwner].

This creates the [rootElement], if necessary, or re-uses an existing one.

This method is rarely called directly, but it can be useful in tests to restore the element tree to a previous version by providing the [RootWidget] of that version (see [WidgetTester.restartAndRestore] for an exemplary use case).

### isRootWidgetAttached

```dart
bool get isRootWidgetAttached
```

Whether the [rootElement] has been initialized.

This will be false until [runApp] is called (or [WidgetTester.pumpWidget] is called in the context of a [TestWidgetsFlutterBinding]).

### performReassemble()

```dart
Future<void> performReassemble()
```

### computePlatformResolvedLocale()

```dart
Locale? computePlatformResolvedLocale(List<Locale> supportedLocales)
```

Computes the locale the current platform would resolve to.

This method is meant to be used as part of a [WidgetsApp.localeListResolutionCallback]. Since this method may return null, a Flutter/dart algorithm should still be provided as a fallback in case a native resolved locale cannot be determined or if the native resolved locale is undesirable.

This method may return a null [Locale] if the platform does not support native locale resolution, or if the resolution failed.

The first `supportedLocale` is treated as the default locale and will be returned if no better match is found.

Android and iOS are currently supported.

On Android, the algorithm described in https://developer.android.com/guide/topics/resources/multilingual-support is used to determine the resolved locale. Depending on the android version of the device, either the modern (>= API 24) or legacy (< API 24) algorithm will be used.

On iOS, the result of `preferredLocalizationsFromArray` method of `NSBundle` is returned. See: https://developer.apple.com/documentation/foundation/nsbundle/1417249-preferredlocalizationsfromarray?language=objc for details on the used method.

iOS treats script code as necessary for a match, so a user preferred locale of `zh_Hans_CN` will not resolve to a supported locale of `zh_CN`.

Since implementation may vary by platform and has potential to be heavy, it is recommended to cache the results of this method if the value is used multiple times.

Second-best (and n-best) matching locales should be obtained by calling this method again with the matched locale of the first call omitted from `supportedLocales`.

### windowingOwner

```dart
WindowingOwner get windowingOwner
```

The [WindowingOwner] is responsible for creating and managing [BaseWindowController]s.

The default [WindowingOwner] supports macOS, Linux, and Windows.

A custom [WindowingOwner] can be provided by the setter.

{@template flutter.widgets.binding.window.experimental} Do not use this API in production applications or packages published to pub.dev. Flutter will make breaking changes to this API, even in patch versions.

This API throws an [UnsupportedError] error unless Flutter’s windowing feature is enabled by [isWindowingEnabled].

See: https://github.com/flutter/flutter/issues/30701. {@endtemplate}

### windowingOwner

```dart
set windowingOwner(WindowingOwner owner)
```

Sets the [WindowingOwner].

The default [WindowingOwner] supports macOS, Linux, and Windows.

This setter can be used to provide a custom [WindowingOwner].

{@macro flutter.widgets.binding.window.experimental}

# runApp()

```dart
void runApp(Widget app)
```

Inflate the given widget and attach it to the view.

The [runApp] method renders the provided `app` widget into the [PlatformDispatcher.implicitView] by wrapping it in a [View] widget, which will bootstrap the render tree for the app. Apps that want to control which [FlutterView] they render into can use [runWidget] instead.

The widget is given constraints during layout that force it to fill the entire view. If you wish to align your widget to one side of the view (e.g., the top), consider using the [Align] widget. If you wish to center your widget, you can also use the [Center] widget.

Calling [runApp] again will detach the previous root widget from the view and attach the given widget in its place. The new widget tree is compared against the previous widget tree and any differences are applied to the underlying render tree, similar to what happens when a [StatefulWidget] rebuilds after calling [State.setState].

Initializes the binding using [WidgetsFlutterBinding] if necessary.

{@template flutter.widgets.runApp.shutdown}

## Application shutdown

This widget tree is not torn down when the application shuts down, because there is no way to predict when that will happen. For example, a user could physically remove power from their device, or the application could crash unexpectedly, or the malware on the device could forcibly terminate the process.

Applications are responsible for ensuring that they are well-behaved even in the face of a rapid unscheduled termination.

To listen for platform shutdown messages (and other lifecycle changes), consider the [AppLifecycleListener] API. {@endtemplate}

To artificially cause the entire widget tree to be disposed, consider calling [runApp] with a widget such as [SizedBox.shrink].

{@template flutter.widgets.runApp.dismissal}

## Dismissing Flutter UI via platform native methods

An application may have both Flutter and non-Flutter UI in it. If the application calls non-Flutter methods to remove Flutter based UI such as platform native API to manipulate the platform native navigation stack, the framework does not know if the developer intends to eagerly free resources or not. The widget tree remains mounted and ready to render as soon as it is displayed again. {@endtemplate}

To release resources more eagerly, establish a [platform channel](https://flutter.dev/to/platform-channels) and use it to call [runApp] with a widget such as [SizedBox.shrink] when the framework should dispose of the active widget tree.

See also:

- [runWidget], which bootstraps a widget tree without assuming the [FlutterView] into which it will be rendered.
- [WidgetsBinding.attachRootWidget], which creates the root widget for the widget hierarchy.
- [RenderObjectToWidgetAdapter.attachToRenderTree], which creates the root element for the element hierarchy.
- [WidgetsBinding.handleBeginFrame], which pumps the widget pipeline to ensure the widget, element, and render trees are all built.

# runWidget()

```dart
void runWidget(Widget app)
```

Inflate the given widget and bootstrap the widget tree.

Unlike [runApp], this method does not define a [FlutterView] into which the provided `app` widget is rendered into. It is up to the caller to include at least one [View] widget in the provided `app` widget that will bootstrap a render tree and define the [FlutterView] into which content is rendered. [RenderObjectWidget]s without an ancestor [View] widget will result in an exception. Apps that want to render into the default view without dealing with view management should consider calling [runApp] instead.

{@tool snippet} The sample shows how to utilize [runWidget] to specify the [FlutterView] into which the `MyApp` widget will be drawn:

```dart
runWidget(
  View(
    view: myFlutterView,
    child: const MyApp(),
  ),
);
```

{@end-tool}

Calling [runWidget] again will detach the previous root widget and attach the given widget in its place. The new widget tree is compared against the previous widget tree and any differences are applied to the underlying render tree, similar to what happens when a [StatefulWidget] rebuilds after calling [State.setState].

Initializes the binding using [WidgetsFlutterBinding] if necessary.

{@macro flutter.widgets.runApp.shutdown}

To artificially cause the entire widget tree to be disposed, consider calling [runWidget] with a [ViewCollection] that does not specify any [ViewCollection.views].

{@macro flutter.widgets.runApp.dismissal}

To release resources more eagerly, establish a [platform channel](https://flutter.dev/to/platform-channels) and use it to remove the [View] whose widget resources should be released from the `app` widget tree provided to [runWidget].

See also:

- [runApp], which bootstraps a widget tree and renders it into a default [FlutterView].
- [WidgetsBinding.attachRootWidget], which creates the root widget for the widget hierarchy.
- [RenderObjectToWidgetAdapter.attachToRenderTree], which creates the root element for the element hierarchy.
- [WidgetsBinding.handleBeginFrame], which pumps the widget pipeline to ensure the widget, element, and render trees are all built.

# debugDumpApp()

```dart
void debugDumpApp()
```

Print a string representation of the currently running app.

# RootWidget

```dart
class RootWidget extends Widget {}
```

A widget for the root of the widget tree.

Exposes an [attach] method to attach the widget tree to a [BuildOwner]. That method also bootstraps the element tree.

Used by [WidgetsBinding.attachRootWidget] (which is indirectly called by [runApp]) to bootstrap applications.

### RootWidget()

```dart
RootWidget({dynamic key, Widget? child, String? debugShortDescription})
```

Creates a [RootWidget].

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### debugShortDescription

```dart
String? debugShortDescription
```

A short description of this widget used by debugging aids.

### createElement()

```dart
RootElement createElement()
```

### attach()

```dart
RootElement attach(BuildOwner owner, [RootElement? element])
```

Inflate this widget and attaches it to the provided [BuildOwner].

If `element` is null, this function will create a new element. Otherwise, the given element will have an update scheduled to switch to this widget.

Used by [WidgetsBinding.attachToBuildOwner] (which is indirectly called by [runApp]) to bootstrap applications.

### toStringShort()

```dart
String toStringShort()
```

# RootElement

```dart
class RootElement extends Element with RootElementMixin {}
```

The root of the element tree.

This element class is the instantiation of a [RootWidget]. It can be used only as the root of an [Element] tree (it cannot be mounted into another [Element]; its parent must be null).

In typical usage, it will be instantiated for a [RootWidget] by calling [RootWidget.attach]. In this usage, it is normally instantiated by the bootstrapping logic in the [WidgetsFlutterBinding] singleton created by [runApp].

### RootElement()

```dart
RootElement(RootWidget widget)
```

Creates a [RootElement] for the provided [RootWidget].

### visitChildren()

```dart
void visitChildren(ElementVisitor visitor)
```

### forgetChild()

```dart
void forgetChild(Element child)
```

### mount()

```dart
void mount(Element? parent, Object? newSlot)
```

### update()

```dart
void update(RootWidget newWidget)
```

### performRebuild()

```dart
void performRebuild()
```

### debugDoingBuild

```dart
bool get debugDoingBuild
```

### debugExpectsRenderObjectForSlot()

```dart
bool debugExpectsRenderObjectForSlot(Object? slot)
```

# WidgetsFlutterBinding

```dart
class WidgetsFlutterBinding extends BindingBase with GestureBinding, SchedulerBinding, ServicesBinding, PaintingBinding, SemanticsBinding, RendererBinding, WidgetsBinding {}
```

A concrete binding for applications based on the Widgets framework.

This is the glue that binds the framework to the Flutter engine.

When using the widgets framework, this binding, or one that implements the same interfaces, must be used. The following mixins are used to implement this binding:

- [GestureBinding], which implements the basics of hit testing.
- [SchedulerBinding], which introduces the concepts of frames.
- [ServicesBinding], which provides access to the plugin subsystem.
- [PaintingBinding], which enables decoding images.
- [SemanticsBinding], which supports accessibility.
- [RendererBinding], which handles the render tree.
- [WidgetsBinding], which handles the widget tree.

### ensureInitialized()

```dart
WidgetsBinding ensureInitialized()
```

Returns an instance of the binding that implements [WidgetsBinding]. If no binding has yet been initialized, the [WidgetsFlutterBinding] class is used to create and initialize one.

You only need to call this method if you need the binding to be initialized before calling [runApp].

In the `flutter_test` framework, [testWidgets] initializes the binding instance to a [TestWidgetsFlutterBinding], not a [WidgetsFlutterBinding]. See [TestWidgetsFlutterBinding.ensureInitialized].
