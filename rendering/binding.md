@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart';

@docImport 'layer.dart';

# RendererBinding

```dart
mixin RendererBinding on BindingBase, ServicesBinding, SchedulerBinding, GestureBinding, SemanticsBinding, HitTestable {}
```

The glue between the render trees and the Flutter engine.

The [RendererBinding] manages multiple independent render trees. Each render tree is rooted in a [RenderView] that must be added to the binding via [addRenderView] to be considered during frame production, hit testing, etc. Furthermore, the render tree must be managed by a [PipelineOwner] that is part of the pipeline owner tree rooted at [rootPipelineOwner].

Adding [PipelineOwner]s and [RenderView]s to this binding in the way described above is left as a responsibility for a higher level abstraction. The widgets library, for example, introduces the [View] widget, which registers its [RenderView] and [PipelineOwner] with this binding.

### initInstances()

```dart
void initInstances()
```

### instance

```dart
RendererBinding get instance
```

The current [RendererBinding], if one has been created.

Provides access to the features exposed by this mixin. The binding must be initialized before using this getter; this is typically done by calling [runApp] or [WidgetsFlutterBinding.ensureInitialized].

### initServiceExtensions()

```dart
void initServiceExtensions()
```

### mouseTracker

```dart
MouseTracker get mouseTracker
```

The object that manages state about currently connected mice, for hover notification.

### pipelineOwner

```dart
PipelineOwner pipelineOwner
```

Deprecated. Will be removed in a future version of Flutter.

This is typically the owner of the render tree bootstrapped by [runApp] and rooted in [renderView]. It maintains dirty state for layout, composite, paint, and accessibility semantics for that tree.

However, by default, the [pipelineOwner] does not participate in frame production because it is not automatically attached to the [rootPipelineOwner] or any of its descendants. It is also not automatically associated with the [renderView]. This is left as a responsibility for a higher level abstraction. The [WidgetsBinding], for example, wires this up in [WidgetsBinding.wrapWithDefaultView], which is called indirectly from [runApp].

Apps, that don't use the [WidgetsBinding] or don't call [runApp] (or [WidgetsBinding.wrapWithDefaultView]) must manually add this pipeline owner to the pipeline owner tree rooted at [rootPipelineOwner] and assign a [RenderView] to it if the they want to use this deprecated property.

Instead of accessing this deprecated property, consider interacting with the root of the [PipelineOwner] tree (exposed in [rootPipelineOwner]) or instead of accessing the [SemanticsOwner] of any [PipelineOwner] consider interacting with the [SemanticsBinding] (exposed via [SemanticsBinding.instance]) directly.

### renderView

```dart
RenderView renderView
```

Deprecated. Will be removed in a future version of Flutter.

This is typically the root of the render tree bootstrapped by [runApp].

However, by default this render view is not associated with any [PipelineOwner] and therefore isn't considered during frame production. It is also not registered with this binding via [addRenderView]. Wiring this up is left as a responsibility for a higher level. The [WidgetsBinding], for example, sets this up in [WidgetsBinding.wrapWithDefaultView], which is called indirectly from [runApp].

Apps that don't use the [WidgetsBinding] or don't call [runApp] (or [WidgetsBinding.wrapWithDefaultView]) must manually assign a [PipelineOwner] to this [RenderView], make sure the pipeline owner is part of the pipeline owner tree rooted at [rootPipelineOwner], and call [addRenderView] if they want to use this deprecated property.

Instead of interacting with this deprecated property, consider using [renderViews] instead, which contains all [RenderView]s managed by the binding.

### createRootPipelineOwner()

```dart
PipelineOwner createRootPipelineOwner()
```

Creates the [PipelineOwner] that serves as the root of the pipeline owner tree ([rootPipelineOwner]).

{@template flutter.rendering.createRootPipelineOwner} By default, the root pipeline owner is not setup to manage a render tree and its [PipelineOwner.rootNode] must not be assigned. If necessary, [createRootPipelineOwner] may be overridden to create a root pipeline owner configured to manage its own render tree.

In typical use, child pipeline owners are added to the root pipeline owner (via [PipelineOwner.adoptChild]). Those children typically do each manage their own [RenderView] and produce distinct render trees which render their content into the [FlutterView] associated with that [RenderView]. {@endtemplate}

### rootPipelineOwner

```dart
PipelineOwner get rootPipelineOwner
```

The [PipelineOwner] that is the root of the PipelineOwner tree.

{@macro flutter.rendering.createRootPipelineOwner}

### renderViews

```dart
Iterable<RenderView> get renderViews
```

The [RenderView]s managed by this binding.

A [RenderView] is added by [addRenderView] and removed by [removeRenderView].

### addRenderView()

```dart
void addRenderView(RenderView view)
```

Adds a [RenderView] to this binding.

The binding will interact with the [RenderView] in the following ways:

- setting and updating [RenderView.configuration],
- calling [RenderView.compositeFrame] when it is time to produce a new frame, and
- forwarding relevant pointer events to the [RenderView] for hit testing.

To remove a [RenderView] from the binding, call [removeRenderView].

### removeRenderView()

```dart
void removeRenderView(RenderView view)
```

Removes a [RenderView] previously added with [addRenderView] from the binding.

### createViewConfigurationFor()

```dart
ViewConfiguration createViewConfigurationFor(RenderView renderView)
```

Returns a [ViewConfiguration] configured for the provided [RenderView] based on the current environment.

This is called during [addRenderView] and also in response to changes to the system metrics to update all [renderViews] added to the binding.

Bindings can override this method to change what size or device pixel ratio the [RenderView] will use. For example, the testing framework uses this to force the display into 800x600 when a test is run on the device using `flutter run`.

### createSceneBuilder()

```dart
ui.SceneBuilder createSceneBuilder()
```

Create a [SceneBuilder].

This hook enables test bindings to instrument the rendering layer.

This is used by the [RenderView] to create the [SceneBuilder] that is passed to the [Layer] system to render the scene.

### createPictureRecorder()

```dart
ui.PictureRecorder createPictureRecorder()
```

Create a [PictureRecorder].

This hook enables test bindings to instrument the rendering layer.

This is used by the [PaintingContext] to create the [PictureRecorder]s used when painting [RenderObject]s into [Picture]s passed to [PictureLayer]s.

### createCanvas()

```dart
Canvas createCanvas(ui.PictureRecorder recorder)
```

Create a [Canvas] from a [PictureRecorder].

This hook enables test bindings to instrument the rendering layer.

This is used by the [PaintingContext] after creating a [PictureRecorder] using [createPictureRecorder].

### handleMetricsChanged()

```dart
void handleMetricsChanged()
```

Called when the system metrics change.

See [dart:ui.PlatformDispatcher.onMetricsChanged].

### handleTextScaleFactorChanged()

```dart
void handleTextScaleFactorChanged()
```

Called when the platform text scale factor changes.

See [dart:ui.PlatformDispatcher.onTextScaleFactorChanged].

### handlePlatformBrightnessChanged()

```dart
void handlePlatformBrightnessChanged()
```

Called when the platform brightness changes.

The current platform brightness can be queried from a Flutter binding or from a [MediaQuery] widget. The latter is preferred from widgets because it causes the widget to be automatically rebuilt when the brightness changes.

{@tool snippet} Querying [MediaQuery.platformBrightnessOf] directly. Preferred.

```dart
final Brightness brightness = MediaQuery.platformBrightnessOf(context);
```

{@end-tool}

{@tool snippet} Querying [PlatformDispatcher.platformBrightness].

```dart
final Brightness brightness = WidgetsBinding.instance.platformDispatcher.platformBrightness;
```

{@end-tool}

See [dart:ui.PlatformDispatcher.onPlatformBrightnessChanged].

### initMouseTracker()

```dart
void initMouseTracker([MouseTracker? tracker])
```

Creates a [MouseTracker] which manages state about currently connected mice, for hover notification.

Used by testing framework to reinitialize the mouse tracker between tests.

### dispatchEvent()

```dart
void dispatchEvent(PointerEvent event, HitTestResult? hitTestResult)
```

### performSemanticsAction()

```dart
void performSemanticsAction(SemanticsActionEvent action)
```

### getRectOfSemanticsNodeInViewCoordinates()

```dart
ui.Rect? getRectOfSemanticsNodeInViewCoordinates(int viewId, int nodeId)
```

### sendFramesToEngine

```dart
bool get sendFramesToEngine
```

Whether frames produced by [drawFrame] are sent to the engine.

If false the framework will do all the work to produce a frame, but the frame is never sent to the engine to actually appear on screen.

See also:

- [deferFirstFrame], which defers when the first frame is sent to the engine.

### deferFirstFrame()

```dart
void deferFirstFrame()
```

Tell the framework to not send the first frames to the engine until there is a corresponding call to [allowFirstFrame].

Call this to perform asynchronous initialization work before the first frame is rendered (which takes down the splash screen). The framework will still do all the work to produce frames, but those frames are never sent to the engine and will not appear on screen.

Calling this has no effect after the first frame has been sent to the engine.

### allowFirstFrame()

```dart
void allowFirstFrame()
```

Called after [deferFirstFrame] to tell the framework that it is ok to send the first frame to the engine now.

For best performance, this method should only be called while the [schedulerPhase] is [SchedulerPhase.idle].

This method may only be called once for each corresponding call to [deferFirstFrame].

### resetFirstFrameSent()

```dart
void resetFirstFrameSent()
```

Call this to pretend that no frames have been sent to the engine yet.

This is useful for tests that want to call [deferFirstFrame] and [allowFirstFrame] since those methods only have an effect if no frames have been sent to the engine yet.

### drawFrame()

```dart
void drawFrame()
```

Pump the rendering pipeline to generate a frame.

This method is called by [handleDrawFrame], which itself is called automatically by the engine when it is time to lay out and paint a frame.

Each frame consists of the following phases:

1.  The animation phase: The [handleBeginFrame] method, which is registered with [PlatformDispatcher.onBeginFrame], invokes all the transient frame callbacks registered with [scheduleFrameCallback], in registration order. This includes all the [Ticker] instances that are driving [AnimationController] objects, which means all of the active [Animation] objects tick at this point.

2.  Microtasks: After [handleBeginFrame] returns, any microtasks that got scheduled by transient frame callbacks get to run. This typically includes callbacks for futures from [Ticker]s and [AnimationController]s that completed this frame.

After [handleBeginFrame], [handleDrawFrame], which is registered with [dart:ui.PlatformDispatcher.onDrawFrame], is called, which invokes all the persistent frame callbacks, of which the most notable is this method, [drawFrame], which proceeds as follows:

3.  The layout phase: All the dirty [RenderObject]s in the system are laid out (see [RenderObject.performLayout]). See [RenderObject.markNeedsLayout] for further details on marking an object dirty for layout.

4.  The compositing bits phase: The compositing bits on any dirty [RenderObject] objects are updated. See [RenderObject.markNeedsCompositingBitsUpdate].

5.  The paint phase: All the dirty [RenderObject]s in the system are repainted (see [RenderObject.paint]). This generates the [Layer] tree. See [RenderObject.markNeedsPaint] for further details on marking an object dirty for paint.

6.  The compositing phase: The layer tree is turned into a [Scene] and sent to the GPU.

7.  The semantics phase: All the dirty [RenderObject]s in the system have their semantics updated. This generates the [SemanticsNode] tree. See [RenderObject.markNeedsSemanticsUpdate] for further details on marking an object dirty for semantics.

For more details on steps 3-7, see [PipelineOwner].

8.  The finalization phase: After [drawFrame] returns, [handleDrawFrame] then invokes post-frame callbacks (registered with [addPostFrameCallback]).

Some bindings (for example, the [WidgetsBinding]) add extra steps to this list (for example, see [WidgetsBinding.drawFrame]).

### performReassemble()

```dart
Future<void> performReassemble()
```

### hitTestInView()

```dart
void hitTestInView(HitTestResult result, Offset position, int viewId)
```

# debugDumpRenderTree()

```dart
void debugDumpRenderTree()
```

Prints a textual representation of the render trees.

{@template flutter.rendering.debugDumpRenderTree} It prints the trees associated with every [RenderView] in [RendererBinding.renderViews], separated by two blank lines. {@endtemplate}

# debugDumpLayerTree()

```dart
void debugDumpLayerTree()
```

Prints a textual representation of the layer trees.

{@macro flutter.rendering.debugDumpRenderTree}

# debugDumpSemanticsTree()

```dart
void debugDumpSemanticsTree([DebugSemanticsDumpOrder childOrder = DebugSemanticsDumpOrder.traversalOrder])
```

Prints a textual representation of the semantics trees.

{@macro flutter.rendering.debugDumpRenderTree}

Semantics trees are only constructed when semantics are enabled (see [SemanticsBinding.semanticsEnabled]). If a semantics tree is not available, a notice about the missing semantics tree is printed instead.

The order in which the children of a [SemanticsNode] will be printed is controlled by the [childOrder] parameter.

# debugDumpPipelineOwnerTree()

```dart
void debugDumpPipelineOwnerTree()
```

Prints a textual representation of the [PipelineOwner] tree rooted at [RendererBinding.rootPipelineOwner].

# RenderingFlutterBinding

```dart
class RenderingFlutterBinding extends BindingBase with GestureBinding, SchedulerBinding, ServicesBinding, SemanticsBinding, PaintingBinding, RendererBinding {}
```

A concrete binding for applications that use the Rendering framework directly. This is the glue that binds the framework to the Flutter engine.

When using the rendering framework directly, this binding, or one that implements the same interfaces, must be used. The following mixins are used to implement this binding:

- [GestureBinding], which implements the basics of hit testing.
- [SchedulerBinding], which introduces the concepts of frames.
- [ServicesBinding], which provides access to the plugin subsystem.
- [SemanticsBinding], which supports accessibility.
- [PaintingBinding], which enables decoding images.
- [RendererBinding], which handles the render tree.

You would only use this binding if you are writing to the rendering layer directly. If you are writing to a higher-level library, such as the Flutter Widgets library, then you would use that layer's binding (see [WidgetsFlutterBinding]).

The [RenderingFlutterBinding] can manage multiple render trees. Each render tree is rooted in a [RenderView] that must be added to the binding via [addRenderView] to be consider during frame production, hit testing, etc. Furthermore, the render tree must be managed by a [PipelineOwner] that is part of the pipeline owner tree rooted at [rootPipelineOwner].

Adding [PipelineOwner]s and [RenderView]s to this binding in the way described above is left as a responsibility for a higher level abstraction. The binding does not own any [RenderView]s directly.

### ensureInitialized()

```dart
RendererBinding ensureInitialized()
```

Returns an instance of the binding that implements [RendererBinding]. If no binding has yet been initialized, the [RenderingFlutterBinding] class is used to create and initialize one.

You need to call this method before using the rendering framework if you are using it directly. If you are using the widgets framework, see [WidgetsFlutterBinding.ensureInitialized].
