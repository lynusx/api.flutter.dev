@docImport 'package:flutter/widgets.dart';

# PlatformViewHitTestBehavior

```dart
enum PlatformViewHitTestBehavior {}
```

How an embedded platform view behave during hit tests.

Opaque targets can be hit by hit tests, causing them to both receive events within their bounds and prevent targets visually behind them from also receiving events.

Translucent targets both receive events within their bounds and permit targets visually behind them to also receive events.

Transparent targets don't receive events within their bounds and permit targets visually behind them to receive events.

# RenderAndroidView

```dart
class RenderAndroidView extends PlatformViewRenderBox {}
```

A render object for an Android view.

Requires Android API level 23 or greater.

[RenderAndroidView] is responsible for sizing, displaying and passing touch events to an Android [View](https://developer.android.com/reference/android/view/View).

{@template flutter.rendering.RenderAndroidView.layout} The render object's layout behavior is to fill all available space, the parent of this object must provide bounded layout constraints. {@endtemplate}

{@template flutter.rendering.RenderAndroidView.gestures} The render object participates in Flutter's gesture arenas, and dispatches touch events to the platform view iff it won the arena. Specific gestures that should be dispatched to the platform view can be specified with factories in the `gestureRecognizers` constructor parameter or by calling `updateGestureRecognizers`. If the set of gesture recognizers is empty, the gesture will be dispatched to the platform view iff it was not claimed by any other gesture recognizer. {@endtemplate}

See also:

- [AndroidView] which is a widget that is used to show an Android view.
- [PlatformViewsService] which is a service for controlling platform views.

### RenderAndroidView()

```dart
RenderAndroidView({required AndroidViewController viewController, required PlatformViewHitTestBehavior hitTestBehavior, required Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers, Clip clipBehavior = Clip.hardEdge})
```

Creates a render object for an Android view.

### controller

```dart
AndroidViewController get controller
```

The Android view controller for the Android view associated with this render object.

### controller

```dart
set controller(AndroidViewController controller)
```

Sets a new Android view controller.

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### sizedByParent

```dart
bool get sizedByParent
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performResize()

```dart
void performResize()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

# RenderDarwinPlatformView

```dart
abstract class RenderDarwinPlatformView<T extends DarwinPlatformViewController> extends RenderBox {}
```

Common render-layer functionality for iOS and macOS platform views.

Provides the basic rendering logic for iOS and macOS platformviews. Subclasses shall override handleEvent in order to execute custom event logic. T represents the class of the view controller for the corresponding widget.

### RenderDarwinPlatformView()

```dart
RenderDarwinPlatformView({required T viewController, required PlatformViewHitTestBehavior hitTestBehavior, required Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers})
```

Creates a render object for a platform view.

### viewController

```dart
T get viewController
```

The unique identifier of the platform view controlled by this controller.

### viewController

```dart
set viewController(T value)
```

### hitTestBehavior

```dart
PlatformViewHitTestBehavior hitTestBehavior
```

How to behave during hit testing.

### sizedByParent

```dart
bool get sizedByParent
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {Offset? position})
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### updateGestureRecognizers()

```dart
void updateGestureRecognizers(Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers)
```

{@macro flutter.rendering.PlatformViewRenderBox.updateGestureRecognizers}

# RenderUiKitView

```dart
class RenderUiKitView extends RenderDarwinPlatformView<UiKitViewController> with NativeHitTestTarget {}
```

A render object for an iOS UIKit UIView.

[RenderUiKitView] is responsible for sizing and displaying an iOS [UIView](https://developer.apple.com/documentation/uikit/uiview).

UIViews are added as subviews of the FlutterView and are composited by Quartz.

The viewController is typically generated by [PlatformViewsRegistry.getNextPlatformViewId], the UIView must have been created by calling [PlatformViewsService.initUiKitView].

{@macro flutter.rendering.RenderAndroidView.layout}

{@macro flutter.rendering.RenderAndroidView.gestures}

See also:

- [UiKitView], which is a widget that is used to show a UIView.
- [PlatformViewsService], which is a service for controlling platform views.

### RenderUiKitView()

```dart
RenderUiKitView({required dynamic viewController, required PlatformViewHitTestBehavior hitTestBehavior, required Set<InvalidType> gestureRecognizers})
```

Creates a render object for an iOS UIView.

### updateGestureRecognizers()

```dart
void updateGestureRecognizers(Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers)
```

{@macro flutter.rendering.PlatformViewRenderBox.updateGestureRecognizers}

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

### detach()

```dart
void detach()
```

### dispose()

```dart
void dispose()
```

# RenderAppKitView

```dart
class RenderAppKitView extends RenderDarwinPlatformView<AppKitViewController> {}
```

A render object for a macOS platform view.

### RenderAppKitView()

```dart
RenderAppKitView({required dynamic viewController, required PlatformViewHitTestBehavior hitTestBehavior, required Set<InvalidType> gestureRecognizers})
```

Creates a render object for a macOS AppKitView.

### updateGestureRecognizers()

```dart
void updateGestureRecognizers(Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers)
```

# PlatformViewRenderBox

```dart
class PlatformViewRenderBox extends RenderBox with _PlatformViewGestureMixin {}
```

A render object for embedding a platform view.

[PlatformViewRenderBox] presents a platform view by adding a [PlatformViewLayer] layer, integrates it with the gesture arenas system and adds relevant semantic nodes to the semantics tree.

### PlatformViewRenderBox()

```dart
PlatformViewRenderBox({required PlatformViewController controller, required PlatformViewHitTestBehavior hitTestBehavior, required Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers})
```

Creating a render object for a [PlatformViewSurface].

### controller

```dart
PlatformViewController get controller
```

The controller for this render object.

### controller

```dart
set controller(PlatformViewController controller)
```

Setting this value to a new value will result in a repaint.

### updateGestureRecognizers()

```dart
void updateGestureRecognizers(Set<Factory<OneSequenceGestureRecognizer>> gestureRecognizers)
```

{@template flutter.rendering.PlatformViewRenderBox.updateGestureRecognizers} Updates which gestures should be forwarded to the platform view.

Gesture recognizers created by factories in this set participate in the gesture arena for each pointer that was put down on the render box. If any of the recognizers on this list wins the gesture arena, the entire pointer event sequence starting from the pointer down event will be dispatched to the Android view.

The `gestureRecognizers` property must not contain more than one factory with the same [Factory.type].

Setting a new set of gesture recognizer factories with the same [Factory.type]s as the current set has no effect, because the factories' constructors would have already been called with the previous set. {@endtemplate}

Any active gesture arena the `PlatformView` participates in is rejected when the set of gesture recognizers is changed.

### sizedByParent

```dart
bool get sizedByParent
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```
