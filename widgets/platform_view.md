@docImport 'gesture_detector.dart';

# AndroidView

```dart
class AndroidView extends StatefulWidget {}
```

Embeds an Android view in the Widget hierarchy.

Requires Android API level 23 or greater.

Embedding Android views is an expensive operation and should be avoided when a Flutter equivalent is possible.

The embedded Android view is painted just like any other Flutter widget and transformations apply to it as well.

{@template flutter.widgets.AndroidView.layout} The widget fills all available space, the parent of this object must provide bounded layout constraints. {@endtemplate}

{@template flutter.widgets.AndroidView.gestures} The widget participates in Flutter's gesture arenas, and dispatches touch events to the platform view iff it won the arena. Specific gestures that should be dispatched to the platform view can be specified in the `gestureRecognizers` constructor parameter. If the set of gesture recognizers is empty, a gesture will be dispatched to the platform view iff it was not claimed by any other gesture recognizer. {@endtemplate}

The Android view object is created using a [PlatformViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html). Plugins can register platform view factories with [PlatformViewRegistry#registerViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewRegistry.html#registerViewFactory-java.lang.String-io.flutter.plugin.platform.PlatformViewFactory-).

Registration is typically done in the plugin's registerWith method, e.g:

```java
  public static void registerWith(Registrar registrar) {
    registrar.platformViewRegistry().registerViewFactory("webview", WebViewFactory(registrar.messenger()));
  }
```

{@template flutter.widgets.AndroidView.lifetime} The platform view's lifetime is the same as the lifetime of the [State] object for this widget. When the [State] is disposed the platform view (and auxiliary resources) are lazily released (some resources are immediately released and some by platform garbage collector). A stateful widget's state is disposed when the widget is removed from the tree or when it is moved within the tree. If the stateful widget has a key and it's only moved relative to its siblings, or it has a [GlobalKey] and it's moved within the tree, it will not be disposed. {@endtemplate}

### AndroidView()

```dart
AndroidView({dynamic key, required String viewType, PlatformViewCreatedCallback? onPlatformViewCreated, PlatformViewHitTestBehavior hitTestBehavior = PlatformViewHitTestBehavior.opaque, TextDirection? layoutDirection, Set<Factory<OneSequenceGestureRecognizer>>? gestureRecognizers, dynamic creationParams, MessageCodec<dynamic>? creationParamsCodec, Clip clipBehavior = Clip.hardEdge})
```

Creates a widget that embeds an Android view.

{@template flutter.widgets.AndroidView.constructorArgs} If `creationParams` is not null then `creationParamsCodec` must not be null. {@endtemplate}

### viewType

```dart
String viewType
```

The unique identifier for Android view type to be embedded by this widget.

A [PlatformViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html) for this type must have been registered.

See also:

- [AndroidView] for an example of registering a platform view factory.

### onPlatformViewCreated

```dart
PlatformViewCreatedCallback? onPlatformViewCreated
```

{@template flutter.widgets.AndroidView.onPlatformViewCreated} Callback to invoke after the platform view has been created.

May be null. {@endtemplate}

### hitTestBehavior

```dart
PlatformViewHitTestBehavior hitTestBehavior
```

{@template flutter.widgets.AndroidView.hitTestBehavior} How this widget should behave during hit testing.

This defaults to [PlatformViewHitTestBehavior.opaque]. {@endtemplate}

### layoutDirection

```dart
TextDirection? layoutDirection
```

{@template flutter.widgets.AndroidView.layoutDirection} The text direction to use for the embedded view.

If this is null, the ambient [Directionality] is used instead. {@endtemplate}

### gestureRecognizers

```dart
Set<Factory<OneSequenceGestureRecognizer>>? gestureRecognizers
```

Which gestures should be forwarded to the Android view.

{@template flutter.widgets.AndroidView.gestureRecognizers.descHead} The gesture recognizers built by factories in this set participate in the gesture arena for each pointer that was put down on the widget. If any of these recognizers win the gesture arena, the entire pointer event sequence starting from the pointer down event will be dispatched to the platform view.

When null, an empty set of gesture recognizer factories is used, in which case a pointer event sequence will only be dispatched to the platform view if no other member of the arena claimed it. {@endtemplate}

For example, with the following setup vertical drags will not be dispatched to the Android view as the vertical drag gesture is claimed by the parent [GestureDetector].

```dart
GestureDetector(
  onVerticalDragStart: (DragStartDetails d) {},
  child: const AndroidView(
    viewType: 'webview',
  ),
)
```

To get the [AndroidView] to claim the vertical drag gestures we can pass a vertical drag gesture recognizer factory in [gestureRecognizers] e.g:

```dart
GestureDetector(
  onVerticalDragStart: (DragStartDetails details) {},
  child: SizedBox(
    width: 200.0,
    height: 100.0,
    child: AndroidView(
      viewType: 'webview',
      gestureRecognizers: <Factory<OneSequenceGestureRecognizer>>{
        Factory<OneSequenceGestureRecognizer>(
          () => EagerGestureRecognizer(),
        ),
      },
    ),
  ),
)
```

{@template flutter.widgets.AndroidView.gestureRecognizers.descFoot} A platform view can be configured to consume all pointers that were put down in its bounds by passing a factory for an [EagerGestureRecognizer] in [gestureRecognizers]. [EagerGestureRecognizer] is a special gesture recognizer that immediately claims the gesture after a pointer down event.

The [gestureRecognizers] property must not contain more than one factory with the same [Factory.type].

Changing [gestureRecognizers] results in rejection of any active gesture arenas (if the platform view is actively participating in an arena). {@endtemplate}

### creationParams

```dart
dynamic creationParams
```

Passed as the args argument of [PlatformViewFactory#create](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html#create-android.content.Context-int-java.lang.Object-)

This can be used by plugins to pass constructor parameters to the embedded Android view.

### creationParamsCodec

```dart
MessageCodec<dynamic>? creationParamsCodec
```

The codec used to encode `creationParams` before sending it to the platform side. It should match the codec passed to the constructor of [PlatformViewFactory](/javadoc/io/flutter/plugin/platform/PlatformViewFactory.html#PlatformViewFactory-io.flutter.plugin.common.MessageCodec-).

This is typically one of: [StandardMessageCodec], [JSONMessageCodec], [StringCodec], or [BinaryCodec].

This must not be null if [creationParams] is not null.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### createState()

```dart
State<AndroidView> createState()
```

# UiKitView

```dart
class UiKitView extends _DarwinView {}
```

Embeds an iOS view in the Widget hierarchy.

Embedding iOS views is an expensive operation and should be avoided when a Flutter equivalent is possible.

{@macro flutter.widgets.AndroidView.layout}

{@macro flutter.widgets.AndroidView.gestures}

{@macro flutter.widgets.AndroidView.lifetime}

Construction of UIViews is done asynchronously, before the UIView is ready this widget paints nothing while maintaining the same layout constraints.

Clipping operations on a UiKitView can result slow performance. If a conic path clipping is applied to a UIKitView, a quad path is used to approximate the clip due to limitation of Quartz.

### UiKitView()

```dart
UiKitView({dynamic key, required String viewType, UiKitViewGestureBlockingPolicy gestureBlockingPolicy = UiKitViewGestureBlockingPolicy.fallbackToPluginDefault, dynamic onPlatformViewCreated, dynamic hitTestBehavior = PlatformViewHitTestBehavior.opaque, dynamic layoutDirection, dynamic creationParams, dynamic creationParamsCodec, Set<InvalidType>? gestureRecognizers})
```

Creates a widget that embeds an iOS view.

{@macro flutter.widgets.AndroidView.constructorArgs}

### gestureBlockingPolicy

```dart
UiKitViewGestureBlockingPolicy gestureBlockingPolicy
```

The gesture blocking policy that controls touch and gesture blocking behaviors.

### createState()

```dart
State<UiKitView> createState()
```

# AppKitView

```dart
class AppKitView extends _DarwinView {}
```

Widget that contains a macOS AppKit view.

Embedding macOS views is an expensive operation and should be avoided where a Flutter equivalent is possible.

The platform view's lifetime is the same as the lifetime of the [State] object for this widget. When the [State] is disposed the platform view (and auxiliary resources) are lazily released (some resources are immediately released and some by platform garbage collector). A stateful widget's state is disposed when the widget is removed from the tree or when it is moved within the tree. If the stateful widget has a key and it's only moved relative to its siblings, or it has a [GlobalKey] and it's moved within the tree, it will not be disposed.

Construction of AppKitViews is done asynchronously, before the underlying NSView is ready this widget paints nothing while maintaining the same layout constraints.

### AppKitView()

```dart
AppKitView({dynamic key, required String viewType, dynamic onPlatformViewCreated, dynamic hitTestBehavior = PlatformViewHitTestBehavior.opaque, dynamic layoutDirection, dynamic creationParams, dynamic creationParamsCodec, Set<InvalidType>? gestureRecognizers})
```

Creates a widget that embeds a macOS AppKit NSView.

### createState()

```dart
State<AppKitView> createState()
```

# ElementCreatedCallback

```dart
typedef ElementCreatedCallback = void Function(Object element)
```

The signature of the function that gets called when the [HtmlElementView] DOM element is created.

[element] is the DOM element that was created.

This callback is called before [element] is attached to the DOM, so it can be modified as needed by the Flutter web application.

See [HtmlElementView.fromTagName] that receives a callback of this type.

{@template flutter.widgets.web.JSInterop.object} Flutter uses type `Object` so this API doesn't force any JS interop API implementation to Flutter users. This `element` can be cast to any compatible JS interop type as needed. For example: `JSAny` (from `dart:js_interop`), `HTMLElement` (from `package:web`) or any custom JS interop definition. See "Next-generation JS interop": https://dart.dev/interop/js-interop {@endtemplate}

# HtmlElementView

```dart
class HtmlElementView extends StatelessWidget {}
```

Embeds an HTML element in the Widget hierarchy in Flutter web.

The embedded HTML is laid out like any other Flutter widget and transformations (like opacity, and clipping) apply to it as well.

{@macro flutter.widgets.AndroidView.layout}

Embedding HTML is a _potentially expensive_ operation and should be avoided when a Flutter equivalent is possible. (See **`isVisible` parameter** below.) This widget is useful to integrate native HTML elements to a Flutter web app, like a `<video>` tag, or a `<div>` where a [Google Map](https://pub.dev/packages/google_maps_flutter) can be rendered.

This widget **only works on Flutter web.** To embed web content on other platforms, consider using the [`webview_flutter` plugin](https://pub.dev/packages/webview_flutter).

## Usage

There's two ways to use the `HtmlElementView` widget:

### `HtmlElementView.fromTagName`

The [HtmlElementView.fromTagName] constructor creates the HTML element specified by `tagName`, and passes it to the `onElementCreated` callback where it can be customized:

```dart
// In a `build` method...
HtmlElementView.fromTagName(
  tagName: 'div',
  onElementCreated: myOnElementCreated,
);
```

The example creates a `<div>` element, then calls the `onElementCreated` callback with the created `<div>`, so it can be customized **before** it is attached to the DOM.

(See more details about `onElementCreated` in the **Lifecycle** section below.)

### Using the `PlatformViewRegistry`

The primitives used to implement [HtmlElementView.fromTagName] are available for general use through `dart:ui_web`'s `platformViewRegistry`.

Creating an `HtmlElementView` through these primitives is a two step process:

#### 1. `registerViewFactory`

First, a `viewFactory` function needs to be registered for a given `viewType`. Flutter web will call this factory function to create the `element` that will be attached later:

```dart
import 'dart:ui_web' as ui_web;
import 'package:web/web.dart' as web;

void registerRedDivFactory() {
  ui_web.platformViewRegistry.registerViewFactory(
    'my-view-type',
    (int viewId, {Object? params}) {
      // Create and return an HTML Element from here
      final web.HTMLDivElement myDiv = web.HTMLDivElement()
        ..id = 'some_id_$viewId'
        ..style.backgroundColor = 'red'
        ..style.width = '100%'
        ..style.height = '100%';
      return myDiv;
    },
  );
}
```

`registerViewFactory` **must** be called outside of `build` methods, so the registered function is available when `build` happens.

See the different types of functions that can be used as `viewFactory`:

- [`typedef ui_web.PlatformViewFactory`](https://api.flutter.dev/flutter/dart-ui_web/PlatformViewFactory.html)
- [`typedef ui_web.ParameterizedPlatformViewFactory`](https://api.flutter.dev/flutter/dart-ui_web/ParameterizedPlatformViewFactory.html)

#### 2. `HtmlElementView` widget

Once a factory is registered, an `HtmlElementView` widget of `viewType` can be added to the widget tree, like so:

```dart
// In a `build` method...
const HtmlElementView(
  viewType: 'my-view-type',
  onPlatformViewCreated: myOnPlatformViewCreated,
  creationParams: <String, Object?>{
    'key': 'someValue',
  },
);
```

[viewType] **must** match the value used to `registerViewFactory` before.

[creationParams] (optional) will be passed to your `viewFactory` function, if it accepts them.

[onPlatformViewCreated] will be called with the `viewId` of the platform view (`element`) created by the `viewFactory`, before it gets attached to the DOM.

The `viewId` can be used to retrieve the created `element` (The same one passed to `onElementCreated` in [HtmlElementView.fromTagName]) with the `ui_web.platformViewRegistry.`[`getViewById` method](https://api.flutter.dev/flutter/dart-ui_web/PlatformViewRegistry/getViewById.html).

(See more details about `onPlatformViewCreated` in the **Lifecycle** section below.)

## Lifecycle

`HtmlElementView` widgets behave like any other Flutter stateless widget, but with an additional lifecycle method: `onPlatformViewCreated` / `onElementCreated` (depending on the constructor, see **Usage** above).

The difference between the two callbacks is the parameter they receive:

- `onPlatformViewCreated` will be called with the created `viewId` as a parameter, and needs `ui_web.platformViewRegistry.getViewById` to retrieve the created element (See [PlatformViewCreatedCallback]).
- `onElementCreated` will be called with the created `element` directly, skipping its `viewId` (See [ElementCreatedCallback]).

Both callbacks are called **after** the HTML `element` has been created, but **before** it's attached to the DOM.

### HTML Lifecycle

The Browser DOM APIs have additional HTML lifecycle callbacks for the root `element` of an `HtmlElementView`.

#### Element Attached To The DOM

It is common for JS code to locate the DOM elements they need with a selector, rather than accepting said DOM elements directly. In those cases, the `element` **must** be attached to the DOM for the selector to work.

The example below demonstrates **how to create an `onElementAttached` function** that gets called when the root `element` is attached to the DOM using a `ResizeObserver` through `package:web` from the `onElementCreated` lifecycle method:

```dart
import 'dart:js_interop';
import 'package:web/web.dart' as web;

// Called after `element` is attached to the DOM.
void onElementAttached(web.HTMLDivElement element) {
  final web.Element? located = web.document.querySelector('#someIdThatICanFindLater');
  assert(located == element, 'Wrong `element` located!');
  // Do things with `element` or `located`, or call your code now...
  element.style.backgroundColor = 'green';
}

void onElementCreated(Object element) {
  element as web.HTMLDivElement;
  element.style.backgroundColor = 'red';
  element.id = 'someIdThatICanFindLater';

  // Create the observer
  final web.ResizeObserver observer = web.ResizeObserver((
    JSArray<web.ResizeObserverEntry> entries,
    web.ResizeObserver observer,
  ) {
    if (element.isConnected) {
      // The observer is done, disconnect it.
      observer.disconnect();
      // Call our callback.
      onElementAttached(element);
    }
  }.toJS);

  // Connect the observer.
  observer.observe(element);
}
```

- Read more about [`ResizeObserver` in the MDN](https://developer.mozilla.org/en-US/docs/Web/API/Resize_Observer_API).

#### Other Observers

The example above uses a `ResizeObserver` because it can be applied directly to the `element` that is about to be attached. Another observer that could be used for this (with a little bit more code) would be a [`MutationObserver`](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver).

The `MutationObserver` requires the parent element in which the `HtmlElementView` is going to be inserted. A safe way to retrieve a parent element for the platform view is to retrieve the `hostElement` of the [FlutterView] where the `HtmlElementView` is being rendered.

The `hostElement` of the current [FlutterView] can be retrieved through:

```dart
import 'dart:js_interop';
import 'dart:ui_web' as ui_web;
import 'package:flutter/widgets.dart';

void useHostElement(BuildContext context) {
  final int flutterViewId = View.of(context).viewId;
  final JSAny? hostElement = ui_web.views.getHostElement(flutterViewId);
  // Use `package:web` with `hostElement`...
}
```

**Important:** `FlutterView.viewId` and the `viewId` parameter passed to the `viewFactory` identify **different objects**:

- `flutterViewId` (from `View.of(context)`) represents the [FlutterView] where the web app is currently rendering.
- `viewId` (passed to the `viewFactory` function) represents a unique ID for the `HtmlElementView` instance that is being attached to the app.

Read more about [FlutterView] on Flutter's API docs:

- [`View.of`](https://api.flutter.dev/flutter/widgets/View/of.html)
- [`getHostElement`](https://main-api.flutter.dev/flutter/dart-ui_web/FlutterViewManagerProxy/getHostElement.html)

## Pointer events

In order for the `HtmlElementView` contents to be interactive, they're allowed to handle `pointer-events`. This may result in Flutter missing some events because they've been handled by the `HtmlElementView`, and not seen by Flutter.

[`package:pointer_interceptor`](https://pub.dev/packages/pointer_interceptor) may help in some cases where Flutter content needs to be overlaid on top of an `HtmlElementView`. Alternatively, the `pointer-events: none` property can be set `onElementCreated`; but that will prevent **ALL** interactions with the underlying HTML content.

If the `HtmlElementView` is an `<iframe>` element, Flutter will not receive pointer events that land in the `<iframe>` (click/tap, drag, drop, etc.) In those cases, the `HtmlElementView` will seem like it's _swallowing_ the events and not participating in Flutter's gesture detection.

## `isVisible` parameter

Rendering custom HTML content (from `HtmlElementView`) in between `canvas` pixels means that the Flutter web engine needs to _split_ the canvas drawing into elements drawn _behind_ the HTML content, and those drawn _above_ it.

In the Flutter web engine, each of these _splits of the canvas to sandwich HTML content in between_ is referred to as an **overlay**.

Each _overlay_ present in a scene has implications both in memory and execution performance, and it is best to minimize their amount; browsers support a limited number of _overlays_ on a single scene at a given time.

`HtmlElementView` objects have an `isVisible` property that can be passed through `registerViewFactory`, or `fromTagName`. `isVisible` refers to whether the `HtmlElementView` will paint pixels on the screen or not.

Correctly defining this value helps the Flutter web rendering engine optimize the amount of _overlays_ it'll need to render a particular scene.

In general, `isVisible` should be left to its default value of `true`, but in some `HtmlElementView`s (like the `pointer_interceptor` or `Link` widget), it can be set to `false`, so the engine doesn't _waste_ an overlay to render Flutter content on top of views that don't paint any pixels.

### HtmlElementView()

```dart
HtmlElementView({dynamic key, required String viewType, PlatformViewCreatedCallback? onPlatformViewCreated, Object? creationParams, PlatformViewHitTestBehavior hitTestBehavior = PlatformViewHitTestBehavior.opaque})
```

Creates a platform view for Flutter web.

`viewType` identifies the type of platform view to create.

### HtmlElementView.fromTagName()

```dart
HtmlElementView.fromTagName({Key? key, required String tagName, bool isVisible = true, ElementCreatedCallback? onElementCreated, PlatformViewHitTestBehavior hitTestBehavior = PlatformViewHitTestBehavior.opaque})
```

Creates a platform view that creates a DOM element specified by [tagName].

[isVisible] indicates whether the view is visible to the user or not. Setting this to false allows the rendering pipeline to perform extra optimizations knowing that the view will not result in any pixels painted on the screen.

[onElementCreated] is called when the DOM element is created. It can be used by the app to customize the element by adding attributes and styles. This method is called _before_ the element is attached to the DOM.

### viewType

```dart
String viewType
```

The unique identifier for the HTML view type to be embedded by this widget.

A PlatformViewFactory for this type must have been registered.

### onPlatformViewCreated

```dart
PlatformViewCreatedCallback? onPlatformViewCreated
```

Callback to invoke after the platform view has been created.

This method is called _before_ the platform view is attached to the DOM.

May be null.

### creationParams

```dart
Object? creationParams
```

Passed as the 2nd argument (i.e. `params`) of the registered view factory.

### hitTestBehavior

```dart
PlatformViewHitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.AndroidView.hitTestBehavior}

### build()

```dart
Widget build(BuildContext context)
```

# PlatformViewCreationParams

```dart
class PlatformViewCreationParams {}
```

The parameters used to create a [PlatformViewController].

See also:

- [CreatePlatformViewCallback] which uses this object to create a [PlatformViewController].

### id

```dart
int id
```

The unique identifier for the new platform view.

[PlatformViewController.viewId] should match this id.

### viewType

```dart
String viewType
```

The unique identifier for the type of platform view to be embedded.

This viewType is used to tell the platform which type of view to associate with the [id].

### onPlatformViewCreated

```dart
PlatformViewCreatedCallback onPlatformViewCreated
```

Callback invoked after the platform view has been created.

### onFocusChanged

```dart
ValueChanged<bool> onFocusChanged
```

Callback invoked when the platform view's focus is changed on the platform side.

The value is true when the platform view gains focus and false when it loses focus.

# PlatformViewSurfaceFactory

```dart
typedef PlatformViewSurfaceFactory = Widget Function(BuildContext context, PlatformViewController controller)
```

A factory for a surface presenting a platform view as part of the widget hierarchy.

The returned widget should present the platform view associated with `controller`.

See also:

- [PlatformViewSurface], a common widget for presenting platform views.

# CreatePlatformViewCallback

```dart
typedef CreatePlatformViewCallback = PlatformViewController Function(PlatformViewCreationParams params)
```

Constructs a [PlatformViewController].

The [PlatformViewController.viewId] field of the created controller must match the value of the params [PlatformViewCreationParams.id] field.

See also:

- [PlatformViewLink], which links a platform view with the Flutter framework.

# PlatformViewLink

```dart
class PlatformViewLink extends StatefulWidget {}
```

Links a platform view with the Flutter framework.

Provides common functionality for embedding a platform view (e.g an android.view.View on Android) with the Flutter framework.

{@macro flutter.widgets.AndroidView.lifetime}

To implement a new platform view widget, return this widget in the `build` method. For example:

```dart
class FooPlatformView extends StatelessWidget {
  const FooPlatformView({super.key});
  @override
  Widget build(BuildContext context) {
    return PlatformViewLink(
      viewType: 'webview',
      onCreatePlatformView: createFooWebView,
      surfaceFactory: (BuildContext context, PlatformViewController controller) {
        return PlatformViewSurface(
          gestureRecognizers: gestureRecognizers,
          controller: controller,
          hitTestBehavior: PlatformViewHitTestBehavior.opaque,
        );
      },
   );
  }
}
```

The `surfaceFactory` and the `onCreatePlatformView` are only called when the state of this widget is initialized, or when the `viewType` changes.

### PlatformViewLink()

```dart
PlatformViewLink({dynamic key, required PlatformViewSurfaceFactory surfaceFactory, required CreatePlatformViewCallback onCreatePlatformView, required String viewType})
```

Construct a [PlatformViewLink] widget.

See also:

- [PlatformViewSurface] for details on the widget returned by `surfaceFactory`.
- [PlatformViewCreationParams] for how each parameter can be used when implementing `createPlatformView`.

### viewType

```dart
String viewType
```

The unique identifier for the view type to be embedded.

Typically, this viewType has already been registered on the platform side.

### createState()

```dart
State<StatefulWidget> createState()
```

# PlatformViewSurface

```dart
class PlatformViewSurface extends LeafRenderObjectWidget {}
```

Integrates a platform view with Flutter's compositor, touch, and semantics subsystems.

The compositor integration is done by adding a [PlatformViewLayer] to the layer tree. [PlatformViewSurface] isn't supported on all platforms (e.g on Android platform views can be composited by using a [TextureLayer] or [AndroidViewSurface]). Custom Flutter embedders can support [PlatformViewLayer]s by implementing a SystemCompositor.

The widget fills all available space, the parent of this object must provide bounded layout constraints.

If the associated platform view is not created the [PlatformViewSurface] does not paint any contents.

See also:

- [AndroidView] which embeds an Android platform view in the widget hierarchy using a [TextureLayer].
- [UiKitView] which embeds an iOS platform view in the widget hierarchy.

### PlatformViewSurface()

```dart
PlatformViewSurface({dynamic key, required PlatformViewController controller, required PlatformViewHitTestBehavior hitTestBehavior, required Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers})
```

Construct a [PlatformViewSurface].

### controller

```dart
PlatformViewController controller
```

The controller for the platform view integrated by this [PlatformViewSurface].

[PlatformViewController] is used for dispatching touch events to the platform view. [PlatformViewController.viewId] identifies the platform view whose contents are painted by this widget.

### gestureRecognizers

```dart
Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers
```

Which gestures should be forwarded to the PlatformView.

{@macro flutter.widgets.AndroidView.gestureRecognizers.descHead}

For example, with the following setup vertical drags will not be dispatched to the platform view as the vertical drag gesture is claimed by the parent [GestureDetector].

```dart
GestureDetector(
  onVerticalDragStart: (DragStartDetails details) { },
  child: PlatformViewSurface(
    gestureRecognizers: const <Factory<OneSequenceGestureRecognizer>>{},
    controller: _controller,
    hitTestBehavior: PlatformViewHitTestBehavior.opaque,
  ),
)
```

To get the [PlatformViewSurface] to claim the vertical drag gestures we can pass a vertical drag gesture recognizer factory in [gestureRecognizers] e.g:

```dart
GestureDetector(
  onVerticalDragStart: (DragStartDetails details) { },
  child: SizedBox(
    width: 200.0,
    height: 100.0,
    child: PlatformViewSurface(
      gestureRecognizers: <Factory<OneSequenceGestureRecognizer>>{
        Factory<OneSequenceGestureRecognizer>(
          () => EagerGestureRecognizer(),
        ),
      },
      controller: _controller,
      hitTestBehavior: PlatformViewHitTestBehavior.opaque,
    ),
  ),
)
```

{@macro flutter.widgets.AndroidView.gestureRecognizers.descFoot}

### hitTestBehavior

```dart
PlatformViewHitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.AndroidView.hitTestBehavior}

### createRenderObject()

```dart
RenderObject createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, PlatformViewRenderBox renderObject)
```

# AndroidViewSurface

```dart
class AndroidViewSurface extends StatefulWidget {}
```

Integrates an Android view with Flutter's compositor, touch, and semantics subsystems.

The compositor integration is done by adding a [TextureLayer] to the layer tree.

The parent of this object must provide bounded layout constraints.

If the associated platform view is not created, the [AndroidViewSurface] does not paint any contents.

When possible, you may want to use [AndroidView] directly, since it requires less boilerplate code than [AndroidViewSurface], and there's no difference in performance, or other trade-off(s).

See also:

- [AndroidView] which embeds an Android platform view in the widget hierarchy.
- [UiKitView] which embeds an iOS platform view in the widget hierarchy.

### AndroidViewSurface()

```dart
AndroidViewSurface({dynamic key, required AndroidViewController controller, required PlatformViewHitTestBehavior hitTestBehavior, required Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers})
```

Construct an `AndroidPlatformViewSurface`.

### controller

```dart
AndroidViewController controller
```

The controller for the platform view integrated by this [AndroidViewSurface].

See [PlatformViewSurface.controller] for details.

### gestureRecognizers

```dart
Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers
```

Which gestures should be forwarded to the PlatformView.

See [PlatformViewSurface.gestureRecognizers] for details.

### hitTestBehavior

```dart
PlatformViewHitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.AndroidView.hitTestBehavior}

### createState()

```dart
State<StatefulWidget> createState()
```

Disposes the controller in a post-frame callback, to allow other widgets to remove their listeners before the controller is disposed.
