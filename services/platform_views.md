@docImport 'package:flutter/material.dart';

@docImport 'message_codecs.dart';

# PointTransformer

```dart
typedef PointTransformer = Offset Function(Offset position)
```

Converts a given point from the global coordinate system in logical pixels to the local coordinate system for a box.

Used by [AndroidViewController.pointTransformer].

# platformViewsRegistry

```dart
PlatformViewsRegistry platformViewsRegistry
```

The [PlatformViewsRegistry] responsible for generating unique identifiers for platform views.

# PlatformViewsRegistry

```dart
class PlatformViewsRegistry {}
```

A registry responsible for generating unique identifier for platform views.

A Flutter application has a single [PlatformViewsRegistry] which can be accesses through the [platformViewsRegistry] getter.

### getNextPlatformViewId()

```dart
int getNextPlatformViewId()
```

Allocates a unique identifier for a platform view.

A platform view identifier can refer to a platform view that was never created, a platform view that was disposed, or a platform view that is alive.

Typically a platform view identifier is passed to a platform view widget which creates the platform view and manages its lifecycle.

# PlatformViewCreatedCallback

```dart
typedef PlatformViewCreatedCallback = void Function(int id)
```

Callback signature for when a platform view was created.

The `id` parameter is the platform view's unique identifier.

# PlatformViewsService

```dart
class PlatformViewsService {}
```

Provides access to the platform views service.

This service allows creating and controlling platform-specific views.

### initAndroidView()

```dart
AndroidViewController initAndroidView({required int id, required String viewType, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

{@template flutter.services.PlatformViewsService.initAndroidView} Creates a controller for a new Android view.

The `id` argument is an unused unique identifier generated with [platformViewsRegistry].

The `viewType` argument is the identifier of the Android view type to be created, a factory for this view type must have been registered on the platform side. Platform view factories are typically registered by plugin code. Plugins can register a platform view factory with [PlatformViewRegistry#registerViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewRegistry.html#registerViewFactory-java.lang.String-io.flutter.plugin.platform.PlatformViewFactory-).

The `creationParams` argument will be passed as the args argument of [PlatformViewFactory#create](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html#create-android.content.Context-int-java.lang.Object-)

The `creationParamsCodec` argument is the codec used to encode `creationParams` before sending it to the platform side. It should match the codec passed to the constructor of [PlatformViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html#PlatformViewFactory-io.flutter.plugin.common.MessageCodec-). This is typically one of: [StandardMessageCodec], [JSONMessageCodec], [StringCodec], or [BinaryCodec].

The `onFocus` argument is a callback that will be invoked when the Android View asks to get the input focus.

The Android view will only be created after [AndroidViewController.setSize] is called for the first time.

If `creationParams` is non null then `creationParamsCodec` must not be null. {@endtemplate}

This attempts to use the TLHC implementation when possible. In cases where that is not supported, it falls back to using Virtual Display.

### initSurfaceAndroidView()

```dart
SurfaceAndroidViewController initSurfaceAndroidView({required int id, required String viewType, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

{@macro flutter.services.PlatformViewsService.initAndroidView}

This attempts to use the "Texture Layer Hybrid Composition (TLHC)" platform view implementation when possible. In cases where that is not supported, it falls back to using "Hybrid Composition", which is the mode used by [initExpensiveAndroidView].

### initExpensiveAndroidView()

```dart
ExpensiveAndroidViewController initExpensiveAndroidView({required int id, required String viewType, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

{@macro flutter.services.PlatformViewsService.initAndroidView}

When this factory is used, the Android view and Flutter widgets are composed at the Android view hierarchy level.

Using this method has a performance cost on devices running Android 9 (api 28) or earlier, or on underpowered devices. In most situations, you should use [initAndroidView] or [initSurfaceAndroidView] instead. Always creates a "Hybrid Composition (HC)" view.

### initHybridAndroidView()

```dart
HybridAndroidViewController initHybridAndroidView({required int id, required String viewType, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

{@macro flutter.services.PlatformViewsService.initAndroidView}

When this factory is used, the Android view and Flutter widgets are composed at the Android view hierarchy level.

This functionality is only supported on Android devices running Vulkan on API 34 or newer. Always creates a "Hybrid Composition++ (HCPP)" view.

### initUiKitView()

```dart
Future<UiKitViewController> initUiKitView({required int id, required String viewType, UiKitViewGestureBlockingPolicy gestureBlockingPolicy = .fallbackToPluginDefault, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

Factory method to create a `UiKitView`.

The `id` parameter is an unused unique identifier generated with [platformViewsRegistry].

The `viewType` parameter is the identifier of the iOS view type to be created, a factory for this view type must have been registered on the platform side. Platform view factories are typically registered by plugin code.

The `onFocus` parameter is a callback that will be invoked when the UIKit view asks to get the input focus. If `creationParams` is non null then `creationParamsCodec` must not be null.

See: https://docs.flutter.dev/platform-integration/ios/platform-views

### initAppKitView()

```dart
Future<AppKitViewController> initAppKitView({required int id, required String viewType, required TextDirection layoutDirection, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, VoidCallback? onFocus})
```

Factory method to create an `AppKitView`.

The `id` parameter is an unused unique identifier generated with [platformViewsRegistry].

The `viewType` parameter is the identifier of the iOS view type to be created, a factory for this view type must have been registered on the platform side. Platform view factories are typically registered by plugin code.

The `onFocus` parameter is a callback that will be invoked when the UIKit view asks to get the input focus. If `creationParams` is non null then `creationParamsCodec` must not be null.

# AndroidPointerProperties

```dart
class AndroidPointerProperties {}
```

Properties of an Android pointer.

A Dart version of Android's [MotionEvent.PointerProperties](https://developer.android.com/reference/android/view/MotionEvent.PointerProperties).

### AndroidPointerProperties()

```dart
AndroidPointerProperties({required int id, required int toolType})
```

Creates an [AndroidPointerProperties] object.

### id

```dart
int id
```

See Android's [MotionEvent.PointerProperties#id](https://developer.android.com/reference/android/view/MotionEvent.PointerProperties.html#id).

### toolType

```dart
int toolType
```

The type of tool used to make contact such as a finger or stylus, if known. See Android's [MotionEvent.PointerProperties#toolType](https://developer.android.com/reference/android/view/MotionEvent.PointerProperties.html#toolType).

### kToolTypeUnknown

```dart
int kToolTypeUnknown
```

Value for `toolType` when the tool type is unknown.

### kToolTypeFinger

```dart
int kToolTypeFinger
```

Value for `toolType` when the tool type is a finger.

### kToolTypeStylus

```dart
int kToolTypeStylus
```

Value for `toolType` when the tool type is a stylus.

### kToolTypeMouse

```dart
int kToolTypeMouse
```

Value for `toolType` when the tool type is a mouse.

### kToolTypeEraser

```dart
int kToolTypeEraser
```

Value for `toolType` when the tool type is an eraser.

### toString()

```dart
String toString()
```

# AndroidPointerCoords

```dart
class AndroidPointerCoords {}
```

Position information for an Android pointer.

A Dart version of Android's [MotionEvent.PointerCoords](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords).

### AndroidPointerCoords()

```dart
AndroidPointerCoords({required double orientation, required double pressure, required double size, required double toolMajor, required double toolMinor, required double touchMajor, required double touchMinor, required double x, required double y})
```

Creates an AndroidPointerCoords.

### orientation

```dart
double orientation
```

The orientation of the touch area and tool area in radians clockwise from vertical.

See Android's [MotionEvent.PointerCoords#orientation](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#orientation).

### pressure

```dart
double pressure
```

A normalized value that describes the pressure applied to the device by a finger or other tool.

See Android's [MotionEvent.PointerCoords#pressure](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#pressure).

### size

```dart
double size
```

A normalized value that describes the approximate size of the pointer touch area in relation to the maximum detectable size of the device.

See Android's [MotionEvent.PointerCoords#size](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#size).

### toolMajor

```dart
double toolMajor
```

See Android's [MotionEvent.PointerCoords#toolMajor](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#toolMajor).

### toolMinor

```dart
double toolMinor
```

See Android's [MotionEvent.PointerCoords#toolMinor](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#toolMinor).

### touchMajor

```dart
double touchMajor
```

See Android's [MotionEvent.PointerCoords#touchMajor](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#touchMajor).

### touchMinor

```dart
double touchMinor
```

See Android's [MotionEvent.PointerCoords#touchMinor](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#touchMinor).

### x

```dart
double x
```

The X component of the pointer movement.

See Android's [MotionEvent.PointerCoords#x](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#x).

### y

```dart
double y
```

The Y component of the pointer movement.

See Android's [MotionEvent.PointerCoords#y](https://developer.android.com/reference/android/view/MotionEvent.PointerCoords.html#y).

### toString()

```dart
String toString()
```

# AndroidMotionEvent

```dart
class AndroidMotionEvent {}
```

A Dart version of Android's [MotionEvent](https://developer.android.com/reference/android/view/MotionEvent).

This is used by [AndroidViewController] to describe pointer events that are forwarded to a platform view when Flutter receives an event that it determines is to be handled by that platform view rather than by another Flutter widget.

See also:

- [AndroidViewController.sendMotionEvent], which can be used to send an [AndroidMotionEvent] explicitly.

### AndroidMotionEvent()

```dart
AndroidMotionEvent({required int downTime, required int eventTime, required int action, required int pointerCount, required List<AndroidPointerProperties> pointerProperties, required List<AndroidPointerCoords> pointerCoords, required int metaState, required int buttonState, required double xPrecision, required double yPrecision, required int deviceId, required int edgeFlags, required int source, required int flags, required int motionEventId})
```

Creates an AndroidMotionEvent.

### downTime

```dart
int downTime
```

The time (in ms) when the user originally pressed down to start a stream of position events, relative to an arbitrary timeline.

See Android's [MotionEvent#getDownTime](<https://developer.android.com/reference/android/view/MotionEvent.html#getDownTime()>).

### eventTime

```dart
int eventTime
```

The time this event occurred, relative to an arbitrary timeline.

See Android's [MotionEvent#getEventTime](<https://developer.android.com/reference/android/view/MotionEvent.html#getEventTime()>).

### action

```dart
int action
```

A value representing the kind of action being performed.

See Android's [MotionEvent#getAction](<https://developer.android.com/reference/android/view/MotionEvent.html#getAction()>).

### pointerCount

```dart
int pointerCount
```

The number of pointers that are part of this event. This must be equivalent to the length of `pointerProperties` and `pointerCoords`.

See Android's [MotionEvent#getPointerCount](<https://developer.android.com/reference/android/view/MotionEvent.html#getPointerCount()>).

### pointerProperties

```dart
List<AndroidPointerProperties> pointerProperties
```

List of [AndroidPointerProperties] for each pointer that is part of this event.

### pointerCoords

```dart
List<AndroidPointerCoords> pointerCoords
```

List of [AndroidPointerCoords] for each pointer that is part of this event.

### metaState

```dart
int metaState
```

The state of any meta / modifier keys that were in effect when the event was generated.

See Android's [MotionEvent#getMetaState](<https://developer.android.com/reference/android/view/MotionEvent.html#getMetaState()>).

### buttonState

```dart
int buttonState
```

The state of all buttons that are pressed such as a mouse or stylus button.

See Android's [MotionEvent#getButtonState](<https://developer.android.com/reference/android/view/MotionEvent.html#getButtonState()>).

### xPrecision

```dart
double xPrecision
```

The precision of the X coordinates being reported, in physical pixels.

See Android's [MotionEvent#getXPrecision](<https://developer.android.com/reference/android/view/MotionEvent.html#getXPrecision()>).

### yPrecision

```dart
double yPrecision
```

The precision of the Y coordinates being reported, in physical pixels.

See Android's [MotionEvent#getYPrecision](<https://developer.android.com/reference/android/view/MotionEvent.html#getYPrecision()>).

### deviceId

```dart
int deviceId
```

See Android's [MotionEvent#getDeviceId](<https://developer.android.com/reference/android/view/MotionEvent.html#getDeviceId()>).

### edgeFlags

```dart
int edgeFlags
```

A bit field indicating which edges, if any, were touched by this MotionEvent.

See Android's [MotionEvent#getEdgeFlags](<https://developer.android.com/reference/android/view/MotionEvent.html#getEdgeFlags()>).

### source

```dart
int source
```

The source of this event (e.g a touchpad or stylus).

See Android's [MotionEvent#getSource](<https://developer.android.com/reference/android/view/MotionEvent.html#getSource()>).

### flags

```dart
int flags
```

See Android's [MotionEvent#getFlags](<https://developer.android.com/reference/android/view/MotionEvent.html#getFlags()>).

### motionEventId

```dart
int motionEventId
```

Used to identify this [MotionEvent](https://developer.android.com/reference/android/view/MotionEvent.html) uniquely in the Flutter Engine.

### toString()

```dart
String toString()
```

# AndroidViewController

```dart
abstract class AndroidViewController extends PlatformViewController {}
```

Controls an Android view that is composed using a GL texture.

Typically created with [PlatformViewsService.initAndroidView].

### kActionDown

```dart
int kActionDown
```

Action code for when a primary pointer touched the screen.

Android's [MotionEvent.ACTION_DOWN](https://developer.android.com/reference/android/view/MotionEvent#ACTION_DOWN)

### kActionUp

```dart
int kActionUp
```

Action code for when a primary pointer stopped touching the screen.

Android's [MotionEvent.ACTION_UP](https://developer.android.com/reference/android/view/MotionEvent#ACTION_UP)

### kActionMove

```dart
int kActionMove
```

Action code for when the event only includes information about pointer movement.

Android's [MotionEvent.ACTION_MOVE](https://developer.android.com/reference/android/view/MotionEvent#ACTION_MOVE)

### kActionCancel

```dart
int kActionCancel
```

Action code for when a motion event has been canceled.

Android's [MotionEvent.ACTION_CANCEL](https://developer.android.com/reference/android/view/MotionEvent#ACTION_CANCEL)

### kActionPointerDown

```dart
int kActionPointerDown
```

Action code for when a secondary pointer touched the screen.

Android's [MotionEvent.ACTION_POINTER_DOWN](https://developer.android.com/reference/android/view/MotionEvent#ACTION_POINTER_DOWN)

### kActionPointerUp

```dart
int kActionPointerUp
```

Action code for when a secondary pointer stopped touching the screen.

Android's [MotionEvent.ACTION_POINTER_UP](https://developer.android.com/reference/android/view/MotionEvent#ACTION_POINTER_UP)

### kAndroidLayoutDirectionLtr

```dart
int kAndroidLayoutDirectionLtr
```

Android's [View.LAYOUT_DIRECTION_LTR](https://developer.android.com/reference/android/view/View.html#LAYOUT_DIRECTION_LTR) value.

### kAndroidLayoutDirectionRtl

```dart
int kAndroidLayoutDirectionRtl
```

Android's [View.LAYOUT_DIRECTION_RTL](https://developer.android.com/reference/android/view/View.html#LAYOUT_DIRECTION_RTL) value.

### kInputDeviceSourceUnknown

```dart
int kInputDeviceSourceUnknown
```

Android's [InputDevice.SOURCE_UNKNOWN](https://developer.android.com/reference/android/view/InputDevice#SOURCE_UNKNOWN)

### kInputDeviceSourceTouchScreen

```dart
int kInputDeviceSourceTouchScreen
```

Android's [InputDevice.SOURCE_TOUCHSCREEN](https://developer.android.com/reference/android/view/InputDevice#SOURCE_TOUCHSCREEN)

### kInputDeviceSourceMouse

```dart
int kInputDeviceSourceMouse
```

Android's [InputDevice.SOURCE_MOUSE](https://developer.android.com/reference/android/view/InputDevice#SOURCE_MOUSE)

### kInputDeviceSourceStylus

```dart
int kInputDeviceSourceStylus
```

Android's [InputDevice.SOURCE_STYLUS](https://developer.android.com/reference/android/view/InputDevice#SOURCE_STYLUS)

### kInputDeviceSourceTouchPad

```dart
int kInputDeviceSourceTouchPad
```

Android's [InputDevice.SOURCE_TOUCHPAD](https://developer.android.com/reference/android/view/InputDevice#SOURCE_TOUCHPAD)

### viewId

```dart
int viewId
```

The unique identifier of the Android view controlled by this controller.

### pointerAction()

```dart
int pointerAction(int pointerId, int action)
```

Creates a masked Android MotionEvent action value for an indexed pointer.

### awaitingCreation

```dart
bool get awaitingCreation
```

### create()

```dart
Future<void> create({Size? size, Offset? position})
```

### setSize()

```dart
Future<Size> setSize(Size size)
```

Sizes the Android View.

[size] is the view's new size in logical pixel. It must be greater than zero.

The first time a size is set triggers the creation of the Android view.

Returns the buffer size in logical pixel that backs the texture where the platform view pixels are written to.

The buffer size may or may not be the same as [size].

As a result, consumers are expected to clip the texture using [size], while using the return value to size the texture.

### setOffset()

```dart
Future<void> setOffset(Offset off)
```

Sets the offset of the platform view.

[off] is the view's new offset in logical pixel.

On Android, this allows the Android native view to draw the a11y highlights in the same location on the screen as the platform view widget in the Flutter framework.

### textureId

```dart
int? get textureId
```

Returns the texture entry id that the Android view is rendering into.

Returns null if the Android view has not been successfully created, if it has been disposed, or if the implementation does not use textures.

### requiresViewComposition

```dart
bool get requiresViewComposition
```

True if the view requires native view composition rather than using a texture to render.

This value may change during [create], but will not change after that call's future has completed.

### sendMotionEvent()

```dart
Future<void> sendMotionEvent(AndroidMotionEvent event)
```

Sends an Android [MotionEvent](https://developer.android.com/reference/android/view/MotionEvent) to the view.

The Android MotionEvent object is created with [MotionEvent.obtain](<https://developer.android.com/reference/android/view/MotionEvent.html#obtain(long,%20long,%20int,%20float,%20float,%20float,%20float,%20int,%20float,%20float,%20int,%20int)>). See documentation of [MotionEvent.obtain](<https://developer.android.com/reference/android/view/MotionEvent.html#obtain(long,%20long,%20int,%20float,%20float,%20float,%20float,%20int,%20float,%20float,%20int,%20int)>) for description of the parameters.

See [AndroidViewController.dispatchPointerEvent] for sending a [PointerEvent].

### pointTransformer

```dart
PointTransformer get pointTransformer
```

Converts a given point from the global coordinate system in logical pixels to the local coordinate system for this box.

This is required to convert a [PointerEvent] to an [AndroidMotionEvent]. It is typically provided by using [RenderBox.globalToLocal].

### pointTransformer

```dart
set pointTransformer(PointTransformer transformer)
```

### isCreated

```dart
bool get isCreated
```

Whether the platform view has already been created.

### addOnPlatformViewCreatedListener()

```dart
void addOnPlatformViewCreatedListener(PlatformViewCreatedCallback listener)
```

Adds a callback that will get invoke after the platform view has been created.

### removeOnPlatformViewCreatedListener()

```dart
void removeOnPlatformViewCreatedListener(PlatformViewCreatedCallback listener)
```

Removes a callback added with [addOnPlatformViewCreatedListener].

### createdCallbacks

```dart
List<PlatformViewCreatedCallback> get createdCallbacks
```

The created callbacks that are invoked after the platform view has been created.

### setLayoutDirection()

```dart
Future<void> setLayoutDirection(TextDirection layoutDirection)
```

Sets the layout direction for the Android view.

### dispatchPointerEvent()

```dart
Future<void> dispatchPointerEvent(PointerEvent event)
```

Converts the [PointerEvent] and sends an Android [MotionEvent](https://developer.android.com/reference/android/view/MotionEvent) to the view.

This method can only be used if a [PointTransformer] is provided to [AndroidViewController.pointTransformer]. Otherwise, an [AssertionError] is thrown. See [AndroidViewController.sendMotionEvent] for sending a `MotionEvent` without a [PointTransformer].

The Android MotionEvent object is created with [MotionEvent.obtain](<https://developer.android.com/reference/android/view/MotionEvent.html#obtain(long,%20long,%20int,%20float,%20float,%20float,%20float,%20int,%20float,%20float,%20int,%20int)>). See documentation of [MotionEvent.obtain](<https://developer.android.com/reference/android/view/MotionEvent.html#obtain(long,%20long,%20int,%20float,%20float,%20float,%20float,%20int,%20float,%20float,%20int,%20int)>) for description of the parameters.

### clearFocus()

```dart
Future<void> clearFocus()
```

Clears the focus from the Android View if it is focused.

### dispose()

```dart
Future<void> dispose()
```

Disposes the Android view.

The [AndroidViewController] object is unusable after calling this. The identifier of the platform view cannot be reused after the view is disposed.

# SurfaceAndroidViewController

```dart
class SurfaceAndroidViewController extends AndroidViewController {}
```

Controls an Android view that is composed using a GL texture. This controller is created from the [PlatformViewsService.initSurfaceAndroidView] factory, and is defined for backward compatibility.

### textureId

```dart
int? get textureId
```

### requiresViewComposition

```dart
bool get requiresViewComposition
```

### setOffset()

```dart
Future<void> setOffset(Offset off)
```

# ExpensiveAndroidViewController

```dart
class ExpensiveAndroidViewController extends AndroidViewController {}
```

Controls an Android view that is composed using the Android view hierarchy. This controller is created from the [PlatformViewsService.initExpensiveAndroidView] factory.

### textureId

```dart
int? get textureId
```

### requiresViewComposition

```dart
bool get requiresViewComposition
```

### setOffset()

```dart
Future<void> setOffset(Offset off)
```

# HybridAndroidViewController

```dart
class HybridAndroidViewController extends AndroidViewController {}
```

Controls an Android view that is composed using the Android view hierarchy. This controller is created from the [PlatformViewsService.initHybridAndroidView] factory.

### checkIfSupported()

```dart
Future<bool> checkIfSupported()
```

Perform a runtime check to determine if HCPP mode is supported on the current device.

### textureId

```dart
int? get textureId
```

### requiresViewComposition

```dart
bool get requiresViewComposition
```

### setOffset()

```dart
Future<void> setOffset(Offset off)
```

### sendMotionEvent()

```dart
Future<void> sendMotionEvent(AndroidMotionEvent event)
```

# TextureAndroidViewController

```dart
class TextureAndroidViewController extends AndroidViewController {}
```

Controls an Android view that is rendered as a texture. This is typically used by [AndroidView] to display a View in the Android view hierarchy.

The platform view is created by calling [create] with an initial size.

The controller is typically created with [PlatformViewsService.initAndroidView].

### textureId

```dart
int? get textureId
```

### requiresViewComposition

```dart
bool get requiresViewComposition
```

### setOffset()

```dart
Future<void> setOffset(Offset off)
```

# DarwinPlatformViewController

```dart
abstract class DarwinPlatformViewController {}
```

Base class for iOS and macOS view controllers.

View controllers are used to create and interact with the UIView or NSView underlying a platform view.

### DarwinPlatformViewController()

```dart
DarwinPlatformViewController(int id, TextDirection layoutDirection)
```

Public default for subclasses to override.

### id

```dart
int id
```

The unique identifier of the iOS view controlled by this controller.

This identifier is typically generated by [PlatformViewsRegistry.getNextPlatformViewId].

### setLayoutDirection()

```dart
Future<void> setLayoutDirection(TextDirection layoutDirection)
```

Sets the layout direction for the iOS UIView.

### acceptGesture()

```dart
Future<void> acceptGesture()
```

Accept an active gesture.

When a touch sequence is happening on the embedded UIView all touch events are delayed. Calling this method releases the delayed events to the embedded UIView and makes it consume any following touch events for the pointers involved in the active gesture.

### rejectGesture()

```dart
Future<void> rejectGesture()
```

Rejects an active gesture.

When a touch sequence is happening on the embedded UIView all touch events are delayed. Calling this method drops the buffered touch events and prevents any future touch events for the pointers that are part of the active touch sequence from arriving to the embedded view.

### dispose()

```dart
Future<void> dispose()
```

Disposes the view.

The [UiKitViewController] object is unusable after calling this. The `id` of the platform view cannot be reused after the view is disposed.

# UiKitViewGestureBlockingPolicy

```dart
enum UiKitViewGestureBlockingPolicy {}
```

How touch event callbacks and gesture recognizers of a platform view are blocked.

This replaces the engine's `FlutterPlatformViewGestureRecognizersBlockingPolicy` enum in `FlutterPlugin.h`.

In iOS, a gesture recognizer (`UIGestureRecognizer`) is an object that decouples the logic for recognizing a sequence of touches (like a tap, pinch, or swipe) and acting on that recognition.

When a Flutter app embeds an iOS platform view (like a `WKWebView`), both the Flutter framework and the native iOS view receive touch events. To prevent both systems from simultaneously reacting to the same touch (e.g., a scroll gesture scrolling both a Flutter `ListView` and a native `UIScrollView`), Flutter needs a mechanism to "block" the native view's gesture recognizers when it determines that the Flutter framework should handle the gesture.

Flutter uses two mechanisms to achieve this:

1.  **Synchronous Blocking (Hit Testing):** During the initial touch (`UIResponder.touchesBegan`), Flutter performs a synchronous hit test. If the touch lands on a Flutter widget that is visually on top of the platform view, Flutter immediately blocks the native view from receiving the touch.
2.  **Asynchronous Blocking (Gesture Arena):** If the touch lands directly on the platform view, both Flutter and the native view begin tracking the gesture. Flutter's gesture arena resolves which system wins. If Flutter wins (e.g., the user is scrolling a Flutter `ListView` that contains the platform view), Flutter asynchronously cancels the native view's gesture recognizers.

The default policy ([fallbackToPluginDefault], which typically resolves to [eager]) works for most use cases. However, some native views (either from Apple or 3rd party) may have bugs where their internal gesture recognizers get stuck in a stale state if they are aggressively canceled by Flutter's asynchronous blocking. In these specific cases, you might need to change the policy to [doNotBlockGesture] or [waitUntilTouchesEnded] to work around the native view's bugs.

For more details, see: https://flutter.dev/go/ios-platform-view-touch-gesture-blocking.

Flutter blocks all the UIGestureRecognizers on the platform view as soon as it decides they should be blocked.

This policy employs a dual blocking strategy: synchronous blocking via hitTest results and asynchronous blocking managed through the framework’s gesture arena. With this policy, only the `touchesBegan` method for all the UIGestureRecognizers is guaranteed to be called.

Flutter blocks all the UIGestureRecognizers on the platform view only after touchesEnded was invoked.

This results in the platform view's UIGestureRecognizers seeing the entire touch sequence, but never recognizing the gesture (and never invoking actions). Using this policy may cause the platform view to incorrectly receive touch events that should have been blocked.

Causes iOS engine to block all the UIGestureRecognizers on the platform view if it deems the hittest shouldn't be handled by the Flutter framework.

Unlike [eager], this policy does not rely on Flutter's gesture arena. This is a workaround to address a few bugs related to platform view's gesture recognizers being stuck in a stale state. See: https://github.com/flutter/flutter/issues/175099. Using this policy may cause the platform view to incorrectly recognize a gesture that should have been blocked.

Fallback to use the policy set by the `registerViewFactory` engine API in FlutterPlugin.h.

# UiKitViewController

```dart
class UiKitViewController extends DarwinPlatformViewController {}
```

Controller for an iOS platform view.

View controllers create and interact with the underlying UIView.

Typically created with [PlatformViewsService.initUiKitView].

# AppKitViewController

```dart
class AppKitViewController extends DarwinPlatformViewController {}
```

Controller for a macOS platform view.

# PlatformViewController

```dart
abstract class PlatformViewController {}
```

An interface for controlling a single platform view.

Used by [PlatformViewSurface] to interface with the platform view it embeds.

### viewId

```dart
int get viewId
```

The viewId associated with this controller.

The viewId should always be unique and non-negative.

See also:

- [PlatformViewsRegistry], which is a helper for managing platform view IDs.

### awaitingCreation

```dart
bool get awaitingCreation
```

True if [create] has not been successfully called the platform view.

This can indicate either that [create] was never called, or that [create] was deferred for implementation-specific reasons.

A `false` return value does not necessarily indicate that the [Future] returned by [create] has completed, only that creation has been started.

### dispatchPointerEvent()

```dart
Future<void> dispatchPointerEvent(PointerEvent event)
```

Dispatches the `event` to the platform view.

### create()

```dart
Future<void> create({Size? size, Offset? position})
```

Creates the platform view with the initial [size].

[size] is the view's initial size in logical pixel. [size] can be omitted if the concrete implementation doesn't require an initial size to create the platform view.

[position] is the view's initial position in logical pixels. [position] can be omitted if the concrete implementation doesn't require an initial position.

### dispose()

```dart
Future<void> dispose()
```

Disposes the platform view.

The [PlatformViewController] is unusable after calling dispose.

### clearFocus()

```dart
Future<void> clearFocus()
```

Clears the view's focus on the platform side.
