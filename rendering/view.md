@docImport 'package:flutter/semantics.dart'; @docImport 'package:flutter/widgets.dart'; @docImport 'package:flutter_test/flutter_test.dart';

# ViewConfiguration

```dart
class ViewConfiguration {}
```

The layout constraints for the root render object.

### ViewConfiguration()

```dart
ViewConfiguration({BoxConstraints physicalConstraints = const BoxConstraints(maxWidth: 0, maxHeight: 0), BoxConstraints logicalConstraints = const BoxConstraints(maxWidth: 0, maxHeight: 0), double devicePixelRatio = 1.0})
```

Creates a view configuration.

By default, the view has [logicalConstraints] and [physicalConstraints] with all dimensions set to zero (i.e. the view is forced to [Size.zero]) and a [devicePixelRatio] of 1.0.

[ViewConfiguration.fromView] is a more convenient way for deriving a [ViewConfiguration] from a given [ui.FlutterView].

### ViewConfiguration.fromView()

```dart
ViewConfiguration.fromView(ui.FlutterView view)
```

Creates a view configuration for the provided [ui.FlutterView].

### logicalConstraints

```dart
BoxConstraints logicalConstraints
```

The constraints of the output surface in logical pixel.

The constraints are passed to the child of the root render object.

### physicalConstraints

```dart
BoxConstraints physicalConstraints
```

The constraints of the output surface in physical pixel.

These constraints are enforced in [toPhysicalSize] when translating the logical size of the root render object back to physical pixels for the [ui.FlutterView.render] method.

### devicePixelRatio

```dart
double devicePixelRatio
```

The pixel density of the output surface.

### toMatrix()

```dart
Matrix4 toMatrix()
```

Creates a transformation matrix that applies the [devicePixelRatio].

The matrix translates points from the local coordinate system of the app (in logical pixels) to the global coordinate system of the [ui.FlutterView] (in physical pixels).

### shouldUpdateMatrix()

```dart
bool shouldUpdateMatrix(ViewConfiguration oldConfiguration)
```

Returns whether [toMatrix] would return a different value for this configuration than it would for the given `oldConfiguration`.

### toPhysicalSize()

```dart
Size toPhysicalSize(Size logicalSize)
```

Transforms the provided [Size] in logical pixels to physical pixels.

The [ui.FlutterView.render] method accepts only sizes in physical pixels, but the framework operates in logical pixels. This method is used to transform the logical size calculated for a [RenderView] back to a physical size suitable to be passed to [ui.FlutterView.render].

By default, this method just multiplies the provided [Size] with the [devicePixelRatio] and constraints the results to the [physicalConstraints].

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

# RenderView

```dart
class RenderView extends RenderObject with RenderObjectWithChildMixin<RenderBox> {}
```

The root of the render tree.

The view represents the total output surface of the render tree and handles bootstrapping the rendering pipeline. The view has a unique child [RenderBox], which is required to fill the entire output surface.

This object must be bootstrapped in a specific order:

1.  First, set the [configuration] (either in the constructor or after construction).
2.  Second, [attach] the object to a [PipelineOwner].
3.  Third, use [prepareInitialFrame] to bootstrap the layout and paint logic.

After the bootstrapping is complete, the [compositeFrame] method may be used to obtain the rendered output.

### RenderView()

```dart
RenderView({RenderBox? child, ViewConfiguration? configuration, required ui.FlutterView view})
```

Creates the root of the render tree.

Typically created by the binding (e.g., [RendererBinding]).

Providing a [configuration] is optional, but a configuration must be set before calling [prepareInitialFrame]. This decouples creating the [RenderView] object from configuring it. Typically, the object is created by the [View] widget and configured by the [RendererBinding] when the [RenderView] is registered with it by the [View] widget.

### size

```dart
Size get size
```

The current layout size of the view.

### configuration

```dart
ViewConfiguration get configuration
```

The constraints used for the root layout.

Typically, this configuration is set by the [RendererBinding], when the [RenderView] is registered with it. It will also update the configuration if necessary. Therefore, if used in conjunction with the [RendererBinding] this property must not be set manually as the [RendererBinding] will just override it.

For tests that want to change the size of the view, set [TestFlutterView.physicalSize] on the appropriate [TestFlutterView] (typically [WidgetTester.view]) instead of setting a configuration directly on the [RenderView].

A [configuration] must be set (either directly or by passing one to the constructor) before calling [prepareInitialFrame].

### configuration

```dart
set configuration(ViewConfiguration value)
```

### hasConfiguration

```dart
bool get hasConfiguration
```

Whether a [configuration] has been set.

This must be true before calling [prepareInitialFrame].

### constraints

```dart
BoxConstraints get constraints
```

### flutterView

```dart
ui.FlutterView get flutterView
```

The [ui.FlutterView] into which this [RenderView] will render.

### automaticSystemUiAdjustment

```dart
bool automaticSystemUiAdjustment
```

Whether Flutter should automatically compute the desired system UI.

When this setting is enabled, Flutter will hit-test the layer tree at the top and bottom of the screen on each frame looking for an [AnnotatedRegionLayer] with an instance of a [SystemUiOverlayStyle]. The hit-test result from the top of the screen provides the status bar settings and the hit-test result from the bottom of the screen provides the system nav bar settings.

If there is no [AnnotatedRegionLayer] on the bottom, the hit-test result from the top provides the system nav bar settings. If there is no [AnnotatedRegionLayer] on the top, the hit-test result from the bottom provides the system status bar settings.

Setting this to false does not cause previous automatic adjustments to be reset, nor does setting it to true cause the app to update immediately.

If you want to imperatively set the system ui style instead, it is recommended that [automaticSystemUiAdjustment] is set to false.

See also:

- [AnnotatedRegion], for placing [SystemUiOverlayStyle] in the layer tree.
- [SystemChrome.setSystemUIOverlayStyle], for imperatively setting the system ui style.

### prepareInitialFrame()

```dart
void prepareInitialFrame()
```

Bootstrap the rendering pipeline by preparing the first frame.

This should only be called once. It is typically called immediately after setting the [configuration] the first time (whether by passing one to the constructor, or setting it directly). The [configuration] must have been set before calling this method, and the [RenderView] must have been attached to a [PipelineOwner] using [attach].

This does not actually schedule the first frame. Call [PipelineOwner.requestVisualUpdate] on the [owner] to do that.

This should be called before using any methods that rely on the [layer] being initialized, such as [compositeFrame].

This method calls [scheduleInitialLayout] and [scheduleInitialPaint].

### debugAssertDoesMeetConstraints()

```dart
void debugAssertDoesMeetConstraints()
```

### performResize()

```dart
void performResize()
```

### performLayout()

```dart
void performLayout()
```

### hitTest()

```dart
bool hitTest(HitTestResult result, {required Offset position})
```

Determines the set of render objects located at the given position.

Returns true if the given point is contained in this render object or one of its descendants. Adds any render objects that contain the point to the given hit test result.

The [position] argument is in the coordinate system of the render view, which is to say, in logical pixels. This is not necessarily the same coordinate system as that expected by the root [Layer], which will normally be in physical (device) pixels.

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### compositeFrame()

```dart
void compositeFrame()
```

Uploads the composited layer tree to the engine.

Actually causes the output of the rendering pipeline to appear on screen.

Before calling this method, the [owner] must be set by calling [attach], the [configuration] must be set to a non-null value, and the [prepareInitialFrame] method must have been called.

### updateSemantics()

```dart
void updateSemantics(ui.SemanticsUpdate update)
```

Sends the provided [ui.SemanticsUpdate] to the [ui.FlutterView] associated with this [RenderView].

A [ui.SemanticsUpdate] is produced by a [SemanticsOwner] during the [EnginePhase.flushSemantics] phase.

### paintBounds

```dart
Rect get paintBounds
```

### semanticBounds

```dart
Rect get semanticBounds
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugAddPaintCallback()

```dart
void debugAddPaintCallback(DebugPaintCallback callback)
```

Registers a [DebugPaintCallback] that is called every time a [RenderView] repaints in debug mode.

The callback may paint a debug overlay on top of the content of the [RenderView] provided to the callback. Callbacks are invoked in the order they were registered in.

Neither registering a callback nor the continued presence of a callback changes how often [RenderView]s are repainted. It is up to the owner of the callback to call [markNeedsPaint] on any [RenderView] for which it wants to update the painted overlay.

Does nothing in release mode.

### debugRemovePaintCallback()

```dart
void debugRemovePaintCallback(DebugPaintCallback callback)
```

Removes a callback registered with [debugAddPaintCallback].

It does not schedule a frame to repaint the [RenderView]s without the overlay painted by the removed callback. It is up to the owner of the callback to call [markNeedsPaint] on the relevant [RenderView]s to repaint them without the overlay.

Does nothing in release mode.

# DebugPaintCallback

```dart
typedef DebugPaintCallback = void Function(PaintingContext context, Offset offset, RenderView renderView)
```

A callback for painting a debug overlay on top of the provided [RenderView].

Used by [RenderView.debugAddPaintCallback] and [RenderView.debugRemovePaintCallback].
