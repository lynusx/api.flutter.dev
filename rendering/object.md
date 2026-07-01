@docImport 'dart:ui';

@docImport 'package:flutter/widgets.dart';

@docImport 'box.dart'; @docImport 'paragraph.dart'; @docImport 'proxy_box.dart'; @docImport 'view.dart'; @docImport 'viewport.dart';

# ParentData

```dart
class ParentData {}
```

Base class for data associated with a [RenderObject] by its parent.

Some render objects wish to store data on their children, such as the children's input parameters to the parent's layout algorithm or the children's position relative to other children.

See also:

- [RenderObject.setupParentData], which [RenderObject] subclasses may override to attach specific types of parent data to children.

### detach()

```dart
void detach()
```

Called when the RenderObject is removed from the tree.

### toString()

```dart
String toString()
```

# PaintingContextCallback

```dart
typedef PaintingContextCallback = void Function(PaintingContext context, Offset offset)
```

Signature for painting into a [PaintingContext].

The `offset` argument is the offset from the origin of the coordinate system of the [PaintingContext.canvas] to the coordinate system of the callee.

Used by many of the methods of [PaintingContext].

# PaintingContext

```dart
class PaintingContext extends ClipContext {}
```

A place to paint.

Rather than holding a canvas directly, [RenderObject]s paint using a painting context. The painting context has a [Canvas], which receives the individual draw operations, and also has functions for painting child render objects.

When painting a child render object, the canvas held by the painting context can change because the draw operations issued before and after painting the child might be recorded in separate compositing layers. For this reason, do not hold a reference to the canvas across operations that might paint child render objects.

New [PaintingContext] objects are created automatically when using [PaintingContext.repaintCompositedChild] and [pushLayer].

### PaintingContext()

```dart
PaintingContext(ContainerLayer _containerLayer, Rect estimatedBounds)
```

Creates a painting context.

Typically only called by [PaintingContext.repaintCompositedChild] and [pushLayer].

### estimatedBounds

```dart
Rect estimatedBounds
```

An estimate of the bounds within which the painting context's [canvas] will record painting commands. This can be useful for debugging.

The canvas will allow painting outside these bounds.

The [estimatedBounds] rectangle is in the [canvas] coordinate system.

### repaintCompositedChild()

```dart
void repaintCompositedChild(RenderObject child, {bool debugAlsoPaintedParent = false})
```

Repaint the given render object.

The render object must be attached to a [PipelineOwner], must have a composited layer, and must be in need of painting. The render object's layer, if any, is re-used, along with any layers in the subtree that don't need to be repainted.

See also:

- [RenderObject.isRepaintBoundary], which determines if a [RenderObject] has a composited layer.

### updateLayerProperties()

```dart
void updateLayerProperties(RenderObject child)
```

Update the composited layer of [child] without repainting its children.

The render object must be attached to a [PipelineOwner], must have a composited layer, and must be in need of a composited layer update but not in need of painting. The render object's layer is re-used, and none of its children are repaint or their layers updated.

See also:

- [RenderObject.isRepaintBoundary], which determines if a [RenderObject] has a composited layer.

### debugInstrumentRepaintCompositedChild()

```dart
void debugInstrumentRepaintCompositedChild(RenderObject child, {bool debugAlsoPaintedParent = false, required PaintingContext customContext})
```

In debug mode, repaint the given render object using a custom painting context that can record the results of the painting operation in addition to performing the regular paint of the child.

See also:

- [repaintCompositedChild], for repainting a composited child without instrumentation.

### paintChild()

```dart
void paintChild(RenderObject child, Offset offset)
```

Paint a child [RenderObject].

If the child has its own composited layer, the child will be composited into the layer subtree associated with this painting context. Otherwise, the child will be painted into the current PictureLayer for this context.

### appendLayer()

```dart
void appendLayer(Layer layer)
```

Adds a layer to the recording requiring that the recording is already stopped.

Do not call this function directly: call [addLayer] or [pushLayer] instead. This function is called internally when all layers not generated from the [canvas] are added.

Subclasses that need to customize how layers are added should override this method.

### recorder

```dart
ui.PictureRecorder get recorder
```

The recorder that is being used by this [PaintingContext] to record interactions with the [Canvas].

It's fragile to hold a reference to the recorder returned by this getter as it can change at any time.

### canvas

```dart
Canvas get canvas
```

The canvas on which to paint.

The current canvas can change whenever you paint a child using this context, which means it's fragile to hold a reference to the canvas returned by this getter.

### addCompositionCallback()

```dart
VoidCallback addCompositionCallback(CompositionCallback callback)
```

Adds a [CompositionCallback] for the current [ContainerLayer] used by this context.

Composition callbacks are called whenever the layer tree containing the current layer of this painting context gets composited, or when it gets detached and will not be rendered again. This happens regardless of whether the layer is added via retained rendering or not.

{@macro flutter.rendering.Layer.compositionCallbacks}

See also:

- [Layer.addCompositionCallback].

### stopRecordingIfNeeded()

```dart
void stopRecordingIfNeeded()
```

Stop recording to a canvas if recording has started.

Do not call this function directly: functions in this class will call this method as needed. This function is called internally to ensure that recording is stopped before adding layers or finalizing the results of a paint.

Subclasses that need to customize how recording to a canvas is performed should override this method to save the results of the custom canvas recordings.

### setIsComplexHint()

```dart
void setIsComplexHint()
```

Hints that the painting in the current layer is complex and would benefit from caching.

If this hint is not set, the compositor will apply its own heuristics to decide whether the current layer is complex enough to benefit from caching.

Calling this ensures a [Canvas] is available. Only draw calls on the current canvas will be hinted; the hint is not propagated to new canvases created after a new layer is added to the painting context (e.g. with [addLayer] or [pushLayer]).

### setWillChangeHint()

```dart
void setWillChangeHint()
```

Hints that the painting in the current layer is likely to change next frame.

This hint tells the compositor not to cache the current layer because the cache will not be used in the future. If this hint is not set, the compositor will apply its own heuristics to decide whether the current layer is likely to be reused in the future.

Calling this ensures a [Canvas] is available. Only draw calls on the current canvas will be hinted; the hint is not propagated to new canvases created after a new layer is added to the painting context (e.g. with [addLayer] or [pushLayer]).

### addLayer()

```dart
void addLayer(Layer layer)
```

Adds a composited leaf layer to the recording.

After calling this function, the [canvas] property will change to refer to a new [Canvas] that draws on top of the given layer.

A [RenderObject] that uses this function is very likely to require its [RenderObject.alwaysNeedsCompositing] property to return true. That informs ancestor render objects that this render object will include a composited layer, which, for example, causes them to use composited clips.

See also:

- [pushLayer], for adding a layer and painting further contents within it.

### pushLayer()

```dart
void pushLayer(ContainerLayer childLayer, PaintingContextCallback painter, Offset offset, {Rect? childPaintBounds})
```

Appends the given layer to the recording, and calls the `painter` callback with that layer, providing the `childPaintBounds` as the estimated paint bounds of the child. The `childPaintBounds` can be used for debugging but have no effect on painting.

The given layer must be an unattached orphan. (Providing a newly created object, rather than reusing an existing layer, satisfies that requirement.)

{@template flutter.rendering.PaintingContext.pushLayer.offset} The `offset` is the offset to pass to the `painter`. In particular, it is not an offset applied to the layer itself. Layers conceptually by default have no position or size, though they can transform their contents. For example, an [OffsetLayer] applies an offset to its children. {@endtemplate}

If the `childPaintBounds` are not specified then the current layer's paint bounds are used. This is appropriate if the child layer does not apply any transformation or clipping to its contents. The `childPaintBounds`, if specified, must be in the coordinate system of the new layer (i.e. as seen by its children after it applies whatever transform to its contents), and should not go outside the current layer's paint bounds.

See also:

- [addLayer], for pushing a layer without painting further contents within it.

### createChildContext()

```dart
PaintingContext createChildContext(ContainerLayer childLayer, Rect bounds)
```

Creates a painting context configured to paint into [childLayer].

The `bounds` are estimated paint bounds for debugging purposes.

### pushClipRect()

```dart
ClipRectLayer? pushClipRect(bool needsCompositing, Offset offset, Rect clipRect, PaintingContextCallback painter, {Clip clipBehavior = Clip.hardEdge, ClipRectLayer? oldLayer})
```

Clip further painting using a rectangle.

{@template flutter.rendering.PaintingContext.pushClipRect.needsCompositing} The `needsCompositing` argument specifies whether the child needs compositing. Typically this matches the value of [RenderObject.needsCompositing] for the caller. If false, this method returns null, indicating that a layer is no longer necessary. If a render object calling this method stores the `oldLayer` in its [RenderObject.layer] field, it should set that field to null.

When `needsCompositing` is false, this method will use a more efficient way to apply the layer effect than actually creating a layer. {@endtemplate}

{@template flutter.rendering.PaintingContext.pushClipRect.offset} The `offset` argument is the offset from the origin of the canvas' coordinate system to the origin of the caller's coordinate system. {@endtemplate}

The `clipRect` is the rectangle (in the caller's coordinate system) to use to clip the painting done by [painter]. It should not include the `offset`.

The `painter` callback will be called while the `clipRect` is applied. It is called synchronously during the call to [pushClipRect].

The `clipBehavior` argument controls how the rectangle is clipped.

{@template flutter.rendering.PaintingContext.pushClipRect.oldLayer} For the `oldLayer` argument, specify the layer created in the previous frame. This gives the engine more information for performance optimizations. Typically this is the value of [RenderObject.layer] that a render object creates once, then reuses for all subsequent frames until a layer is no longer needed (e.g. the render object no longer needs compositing) or until the render object changes the type of the layer (e.g. from opacity layer to a clip rect layer). {@endtemplate}

### pushClipRRect()

```dart
ClipRRectLayer? pushClipRRect(bool needsCompositing, Offset offset, Rect bounds, RRect clipRRect, PaintingContextCallback painter, {Clip clipBehavior = Clip.antiAlias, ClipRRectLayer? oldLayer})
```

Clip further painting using a rounded rectangle.

{@macro flutter.rendering.PaintingContext.pushClipRect.needsCompositing}

{@macro flutter.rendering.PaintingContext.pushClipRect.offset}

The `bounds` argument is used to specify the region of the canvas (in the caller's coordinate system) into which `painter` will paint.

The `clipRRect` argument specifies the rounded-rectangle (in the caller's coordinate system) to use to clip the painting done by `painter`. It should not include the `offset`.

The `painter` callback will be called while the `clipRRect` is applied. It is called synchronously during the call to [pushClipRRect].

The `clipBehavior` argument controls how the rounded rectangle is clipped.

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

### pushClipRSuperellipse()

```dart
ClipRSuperellipseLayer? pushClipRSuperellipse(bool needsCompositing, Offset offset, Rect bounds, RSuperellipse clipRSuperellipse, PaintingContextCallback painter, {Clip clipBehavior = Clip.antiAlias, ClipRSuperellipseLayer? oldLayer})
```

Clip further painting using a rounded superellipse.

{@macro flutter.rendering.PaintingContext.pushClipRect.needsCompositing}

{@macro flutter.rendering.PaintingContext.pushClipRect.offset}

The `bounds` argument is used to specify the region of the canvas (in the caller's coordinate system) into which `painter` will paint.

The `clipRSuperellipse` argument specifies the rounded-superellipse (in the caller's coordinate system) to use to clip the painting done by `painter`. It should not include the `offset`.

The `painter` callback will be called while the `clipRSuperellipse` is applied. It is called synchronously during the call to [pushClipRSuperellipse].

The `clipBehavior` argument controls how the rounded rectangle is clipped.

Hit tests are performed based on the bounding box of the [RSuperellipse].

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

### pushClipPath()

```dart
ClipPathLayer? pushClipPath(bool needsCompositing, Offset offset, Rect bounds, Path clipPath, PaintingContextCallback painter, {Clip clipBehavior = Clip.antiAlias, ClipPathLayer? oldLayer})
```

Clip further painting using a path.

{@macro flutter.rendering.PaintingContext.pushClipRect.needsCompositing}

{@macro flutter.rendering.PaintingContext.pushClipRect.offset}

The `bounds` argument is used to specify the region of the canvas (in the caller's coordinate system) into which `painter` will paint.

The `clipPath` argument specifies the [Path] (in the caller's coordinate system) to use to clip the painting done by `painter`. It should not include the `offset`.

The `painter` callback will be called while the `clipPath` is applied. It is called synchronously during the call to [pushClipPath].

The `clipBehavior` argument controls how the path is clipped.

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

### pushColorFilter()

```dart
ColorFilterLayer pushColorFilter(Offset offset, ColorFilter colorFilter, PaintingContextCallback painter, {ColorFilterLayer? oldLayer})
```

Blend further painting with a color filter.

{@macro flutter.rendering.PaintingContext.pushLayer.offset}

The `colorFilter` argument is the [ColorFilter] value to use when blending the painting done by `painter`.

The `painter` callback will be called while the `colorFilter` is applied. It is called synchronously during the call to [pushColorFilter].

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

A [RenderObject] that uses this function is very likely to require its [RenderObject.alwaysNeedsCompositing] property to return true. That informs ancestor render objects that this render object will include a composited layer, which, for example, causes them to use composited clips.

### pushTransform()

```dart
TransformLayer? pushTransform(bool needsCompositing, Offset offset, Matrix4 transform, PaintingContextCallback painter, {TransformLayer? oldLayer})
```

Transform further painting using a matrix.

{@macro flutter.rendering.PaintingContext.pushClipRect.needsCompositing}

The `offset` argument is the offset to pass to `painter` and the offset to the origin used by `transform`.

The `transform` argument is the [Matrix4] with which to transform the coordinate system while calling `painter`. It should not include `offset`. It is applied effectively after applying `offset`.

The `painter` callback will be called while the `transform` is applied. It is called synchronously during the call to [pushTransform].

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

### pushOpacity()

```dart
OpacityLayer pushOpacity(Offset offset, int alpha, PaintingContextCallback painter, {OpacityLayer? oldLayer})
```

Blend further painting with an alpha value.

The `offset` argument indicates an offset to apply to all the children (the rendering created by `painter`).

The `alpha` argument is the alpha value to use when blending the painting done by `painter`. An alpha value of 0 means the painting is fully transparent and an alpha value of 255 means the painting is fully opaque.

The `painter` callback will be called while the `alpha` is applied. It is called synchronously during the call to [pushOpacity].

{@macro flutter.rendering.PaintingContext.pushClipRect.oldLayer}

A [RenderObject] that uses this function is very likely to require its [RenderObject.alwaysNeedsCompositing] property to return true. That informs ancestor render objects that this render object will include a composited layer, which, for example, causes them to use composited clips.

### toString()

```dart
String toString()
```

# Constraints

```dart
abstract class Constraints {}
```

An abstract set of layout constraints.

Concrete layout models (such as box) will create concrete subclasses to communicate layout constraints between parents and children.

## Writing a Constraints subclass

When creating a new [RenderObject] subclass with a new layout protocol, one will usually need to create a new [Constraints] subclass to express the input to the layout algorithms.

A [Constraints] subclass should be immutable (all fields final). There are several members to implement, in addition to whatever fields, constructors, and helper methods one may find useful for a particular layout protocol:

- The [isTight] getter, which should return true if the object represents a case where the [RenderObject] class has no choice for how to lay itself out. For example, [BoxConstraints] returns true for [isTight] when both the minimum and maximum widths and the minimum and maximum heights are equal.

- The [isNormalized] getter, which should return true if the object represents its data in its canonical form. Sometimes, it is possible for fields to be redundant with each other, such that several different representations have the same implications. For example, a [BoxConstraints] instance with its minimum width greater than its maximum width is equivalent to one where the maximum width is set to that minimum width (`2<w<1` is equivalent to `2<w<2`, since minimum constraints have priority). This getter is used by the default implementation of [debugAssertIsValid].

- The [debugAssertIsValid] method, which should assert if there's anything wrong with the constraints object. (We use this approach rather than asserting in constructors so that our constructors can be `const` and so that it is possible to create invalid constraints temporarily while building valid ones.) See the implementation of [BoxConstraints.debugAssertIsValid] for an example of the detailed checks that can be made.

- The [==] operator and the [hashCode] getter, so that constraints can be compared for equality. If a render object is given constraints that are equal, then the rendering library will avoid laying the object out again if it is not dirty.

- The [toString] method, which should describe the constraints so that they appear in a usefully readable form in the output of [debugDumpRenderTree].

### Constraints()

```dart
Constraints()
```

Abstract const constructor. This constructor enables subclasses to provide const constructors so that they can be used in const expressions.

### isTight

```dart
bool get isTight
```

Whether there is exactly one size possible given these constraints.

### isNormalized

```dart
bool get isNormalized
```

Whether the constraint is expressed in a consistent manner.

### debugAssertIsValid()

```dart
bool debugAssertIsValid({bool isAppliedConstraint = false, InformationCollector? informationCollector})
```

Asserts that the constraints are valid.

This might involve checks more detailed than [isNormalized].

For example, the [BoxConstraints] subclass verifies that the constraints are not [double.nan].

If the `isAppliedConstraint` argument is true, then even stricter rules are enforced. This argument is set to true when checking constraints that are about to be applied to a [RenderObject] during layout, as opposed to constraints that may be further affected by other constraints. For example, the asserts for verifying the validity of [RenderConstrainedBox.additionalConstraints] do not set this argument, but the asserts for verifying the argument passed to the [RenderObject.layout] method do.

The `informationCollector` argument takes an optional callback which is called when an exception is to be thrown. The collected information is then included in the message after the error line.

Returns the same as [isNormalized] if asserts are disabled.

# RenderObjectVisitor

```dart
typedef RenderObjectVisitor = void Function(RenderObject child)
```

Signature for a function that is called for each [RenderObject].

Used by [RenderObject.visitChildren] and [RenderObject.visitChildrenForSemantics].

# LayoutCallback

```dart
typedef LayoutCallback<T extends Constraints> = void Function(T constraints)
```

Signature for a function that is called during layout.

Used by [RenderObject.invokeLayoutCallback].

# PipelineOwner

```dart
base class PipelineOwner with DiagnosticableTreeMixin {}
```

The pipeline owner manages the rendering pipeline.

The pipeline owner provides an interface for driving the rendering pipeline and stores the state about which render objects have requested to be visited in each stage of the pipeline. To flush the pipeline, call the following functions in order:

1.  [flushLayout] updates any render objects that need to compute their layout. During this phase, the size and position of each render object is calculated. Render objects might dirty their painting or compositing state during this phase.
2.  [flushCompositingBits] updates any render objects that have dirty compositing bits. During this phase, each render object learns whether any of its children require compositing. This information is used during the painting phase when selecting how to implement visual effects such as clipping. If a render object has a composited child, it needs to use a [Layer] to create the clip in order for the clip to apply to the composited child (which will be painted into its own [Layer]).
3.  [flushPaint] visits any render objects that need to paint. During this phase, render objects get a chance to record painting commands into [PictureLayer]s and construct other composited [Layer]s.
4.  Finally, if semantics are enabled, [flushSemantics] will compile the semantics for the render objects. This semantic information is used by assistive technology to improve the accessibility of the render tree.

The [RendererBinding] holds the pipeline owner for the render objects that are visible on screen. You can create other pipeline owners to manage off-screen objects, which can flush their pipelines independently of the on-screen render objects.

[PipelineOwner]s can be organized in a tree to manage multiple render trees, where each [PipelineOwner] is responsible for one of the render trees. To build or modify the tree, call [adoptChild] or [dropChild]. During each of the different flush phases described above, a [PipelineOwner] will first perform the phase on the nodes it manages in its own render tree before calling the same flush method on its children. No assumption must be made about the order in which child [PipelineOwner]s are flushed.

A [PipelineOwner] may also be [attach]ed to a [PipelineManifold], which gives it access to platform functionality usually exposed by the bindings without tying it to a specific binding implementation. All [PipelineOwner]s in a given tree must be attached to the same [PipelineManifold]. This happens automatically during [adoptChild].

### PipelineOwner()

```dart
PipelineOwner({VoidCallback? onNeedVisualUpdate, VoidCallback? onSemanticsOwnerCreated, SemanticsUpdateCallback? onSemanticsUpdate, VoidCallback? onSemanticsOwnerDisposed})
```

Creates a pipeline owner.

Typically created by the binding (e.g., [RendererBinding]), but can be created separately from the binding to drive off-screen render objects through the rendering pipeline.

### onNeedVisualUpdate

```dart
VoidCallback? onNeedVisualUpdate
```

Called when a render object associated with this pipeline owner wishes to update its visual appearance.

Typical implementations of this function will schedule a task to flush the various stages of the pipeline. This function might be called multiple times in quick succession. Implementations should take care to discard duplicate calls quickly.

When the [PipelineOwner] is attached to a [PipelineManifold] and [onNeedVisualUpdate] is provided, the [onNeedVisualUpdate] callback is invoked instead of calling [PipelineManifold.requestVisualUpdate].

### onSemanticsOwnerCreated

```dart
VoidCallback? onSemanticsOwnerCreated
```

Called whenever this pipeline owner creates a semantics object.

Typical implementations will schedule the creation of the initial semantics tree.

### onSemanticsUpdate

```dart
SemanticsUpdateCallback? onSemanticsUpdate
```

Called whenever this pipeline owner's semantics owner emits a [SemanticsUpdate].

Typical implementations will delegate the [SemanticsUpdate] to a [FlutterView] that can handle the [SemanticsUpdate].

### onSemanticsOwnerDisposed

```dart
VoidCallback? onSemanticsOwnerDisposed
```

Called whenever this pipeline owner disposes its semantics owner.

Typical implementations will tear down the semantics tree.

### requestVisualUpdate()

```dart
void requestVisualUpdate()
```

Calls [onNeedVisualUpdate] if [onNeedVisualUpdate] is not null.

Used to notify the pipeline owner that an associated render object wishes to update its visual appearance.

### rootNode

```dart
RenderObject? get rootNode
```

The unique object managed by this pipeline that has no parent.

### rootNode

```dart
set rootNode(RenderObject? value)
```

### nodesNeedingLayout

```dart
Iterable<RenderObject> get nodesNeedingLayout
```

The [RenderObject]s representing relayout boundaries which need to be laid out in the next [flushLayout] pass.

Relayout boundaries are added when they are marked for layout. Subclasses of [PipelineOwner] may use them to invalidate caches or otherwise make performance optimizations. Since nodes may be marked for layout at any time, they are best checked during [flushLayout].

Relayout boundaries owned by child [PipelineOwner]s are not included here.

Boundaries appear in an arbitrary order, and may appear multiple times.

### debugDoingLayout

```dart
bool get debugDoingLayout
```

Whether this pipeline is currently in the layout phase.

Specifically, whether [flushLayout] is currently running.

Only valid when asserts are enabled; in release builds, this always returns false.

### flushLayout()

```dart
void flushLayout()
```

Update the layout information for all dirty render objects.

This function is one of the core stages of the rendering pipeline. Layout information is cleaned prior to painting so that render objects will appear on screen in their up-to-date locations.

See [RendererBinding] for an example of how this function is used.

### flushCompositingBits()

```dart
void flushCompositingBits()
```

Updates the [RenderObject.needsCompositing] bits.

Called as part of the rendering pipeline after [flushLayout] and before [flushPaint].

### nodesNeedingPaint

```dart
Iterable<RenderObject> get nodesNeedingPaint
```

The [RenderObject]s which need to be painted in the next [flushPaint] pass.

[RenderObject]s marked with [RenderObject.isRepaintBoundary] are added when they are marked needing paint. Subclasses of [PipelineOwner] may use them to invalidate caches or otherwise make performance optimizations. Since nodes may be marked for layout at any time, they are best checked during [flushPaint].

Marked children of child [PipelineOwner]s are not included here.

### debugDoingPaint

```dart
bool get debugDoingPaint
```

Whether this pipeline is currently in the paint phase.

Specifically, whether [flushPaint] is currently running.

Only valid when asserts are enabled. In release builds, this always returns false.

### flushPaint()

```dart
void flushPaint()
```

Update the display lists for all render objects.

This function is one of the core stages of the rendering pipeline. Painting occurs after layout and before the scene is recomposited so that scene is composited with up-to-date display lists for every render object.

See [RendererBinding] for an example of how this function is used.

### semanticsOwner

```dart
SemanticsOwner? get semanticsOwner
```

The object that is managing semantics for this pipeline owner, if any.

An owner is created by [ensureSemantics] or when the [PipelineManifold] to which this owner is connected has [PipelineManifold.semanticsEnabled] set to true. The owner is valid for as long as [PipelineManifold.semanticsEnabled] remains true or while there are outstanding [SemanticsHandle]s from calls to [ensureSemantics]. The [semanticsOwner] field will revert to null once both conditions are no longer met.

When [semanticsOwner] is null, the [PipelineOwner] skips all steps relating to semantics.

### debugOutstandingSemanticsHandles

```dart
int get debugOutstandingSemanticsHandles
```

Deprecated.

Use [SemanticsBinding.debugOutstandingSemanticsHandles] instead. This API is broken because an outstanding semantics handle on a given pipeline owner doesn't mean that semantics are actually produced.

### ensureSemantics()

```dart
SemanticsHandle ensureSemantics({VoidCallback? listener})
```

Deprecated.

Call [SemanticsBinding.ensureSemantics] instead and optionally add a listener to [PipelineOwner.semanticsOwner]. This API is broken as calling it does not guarantee that semantics are produced.

### flushSemantics()

```dart
void flushSemantics()
```

Update the semantics for render objects marked as needing a semantics update.

Initially, only the root node, as scheduled by [RenderObject.scheduleInitialSemantics], needs a semantics update.

This function is one of the core stages of the rendering pipeline. The semantics are compiled after painting and only after [RenderObject.scheduleInitialSemantics] has been called.

See [RendererBinding] for an example of how this function is used.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### attach()

```dart
void attach(PipelineManifold manifold)
```

Mark this [PipelineOwner] as attached to the given [PipelineManifold].

Typically, this is only called directly on the root [PipelineOwner]. Children are automatically attached to their parent's [PipelineManifold] when [adoptChild] is called.

### detach()

```dart
void detach()
```

Mark this [PipelineOwner] as detached.

Typically, this is only called directly on the root [PipelineOwner]. Children are automatically detached from their parent's [PipelineManifold] when [dropChild] is called.

### adoptChild()

```dart
void adoptChild(PipelineOwner child)
```

Adds `child` to this [PipelineOwner].

During the phases of frame production (see [RendererBinding.drawFrame]), the parent [PipelineOwner] will complete a phase for the nodes it owns directly before invoking the flush method corresponding to the current phase on its child [PipelineOwner]s. For example, during layout, the parent [PipelineOwner] will first lay out its own nodes before calling [flushLayout] on its children. During paint, it will first paint its own nodes before calling [flushPaint] on its children. This order also applies for all the other phases.

No assumptions must be made about the order in which child [PipelineOwner]s are flushed.

No new children may be added after the [PipelineOwner] has started calling [flushLayout] on any of its children until the end of the current frame.

To remove a child, call [dropChild].

### dropChild()

```dart
void dropChild(PipelineOwner child)
```

Removes a child [PipelineOwner] previously added via [adoptChild].

This node will cease to call the flush methods on the `child` during frame production.

No children may be removed after the [PipelineOwner] has started calling [flushLayout] on any of its children until the end of the current frame.

### visitChildren()

```dart
void visitChildren(PipelineOwnerVisitor visitor)
```

Calls `visitor` for each immediate child of this [PipelineOwner].

See also:

- [adoptChild] to add a child.
- [dropChild] to remove a child.

### dispose()

```dart
void dispose()
```

Release any resources held by this pipeline owner.

Prior to calling this method the pipeline owner must be removed from the pipeline owner tree, i.e. it must have neither a parent nor any children (see [dropChild]). It also must be [detach]ed from any [PipelineManifold].

The object is no longer usable after calling dispose.

# PipelineOwnerVisitor

```dart
typedef PipelineOwnerVisitor = void Function(PipelineOwner child)
```

Signature for the callback to [PipelineOwner.visitChildren].

The argument is the child being visited.

# PipelineManifold

```dart
abstract class PipelineManifold implements Listenable {}
```

Manages a tree of [PipelineOwner]s.

All [PipelineOwner]s within a tree are attached to the same [PipelineManifold], which gives them access to shared functionality such as requesting a visual update (by calling [requestVisualUpdate]). As such, the [PipelineManifold] gives the [PipelineOwner]s access to functionality usually provided by the bindings without tying the [PipelineOwner]s to a particular binding implementation.

The root of the [PipelineOwner] tree is attached to a [PipelineManifold] by passing the manifold to [PipelineOwner.attach]. Children are attached to the same [PipelineManifold] as their parent when they are adopted via [PipelineOwner.adoptChild].

[PipelineOwner]s can register listeners with the [PipelineManifold] to be informed when certain values provided by the [PipelineManifold] change.

### semanticsEnabled

```dart
bool get semanticsEnabled
```

Whether [PipelineOwner]s connected to this [PipelineManifold] should collect semantics information and produce a semantics tree.

The [PipelineManifold] notifies its listeners (managed with [addListener] and [removeListener]) when this property changes its value.

See also:

- [SemanticsBinding.semanticsEnabled], which [PipelineManifold] implementations typically use to back this property.

### requestVisualUpdate()

```dart
void requestVisualUpdate()
```

Called by a [PipelineOwner] connected to this [PipelineManifold] when a [RenderObject] associated with that pipeline owner wishes to update its visual appearance.

Typical implementations of this function will schedule a task to flush the various stages of the pipeline. This function might be called multiple times in quick succession. Implementations should take care to discard duplicate calls quickly.

A [PipelineOwner] connected to this [PipelineManifold] will call [PipelineOwner.onNeedVisualUpdate] instead of this method if it has been configured with a non-null [PipelineOwner.onNeedVisualUpdate] callback.

See also:

- [SchedulerBinding.ensureVisualUpdate], which [PipelineManifold] implementations typically call to implement this method.

# RenderObject

```dart
abstract class RenderObject with DiagnosticableTreeMixin implements HitTestTarget {}
```

An object in the render tree.

The [RenderObject] class hierarchy is the core of the rendering library's reason for being.

{@youtube 560 315 https://www.youtube.com/watch?v=zmbmrw07qBc}

[RenderObject]s have a [parent], and have a slot called [parentData] in which the parent [RenderObject] can store child-specific data, for example, the child position. The [RenderObject] class also implements the basic layout and paint protocols.

The [RenderObject] class, however, does not define a child model (e.g. whether a node has zero, one, or more children). It also doesn't define a coordinate system (e.g. whether children are positioned in Cartesian coordinates, in polar coordinates, etc) or a specific layout protocol (e.g. whether the layout is width-in-height-out, or constraint-in-size-out, or whether the parent sets the size and position of the child before or after the child lays out, etc; or indeed whether the children are allowed to read their parent's [parentData] slot).

The [RenderBox] subclass introduces the opinion that the layout system uses Cartesian coordinates.

## Lifecycle

A [RenderObject] must [dispose] when it is no longer needed. The creator of the object is responsible for disposing of it. Typically, the creator is a [RenderObjectElement], and that element will dispose the object it creates when it is unmounted.

[RenderObject]s are responsible for cleaning up any expensive resources they hold when [dispose] is called, such as [Picture] or [Image] objects. This includes any [Layer]s that the render object has directly created. The base implementation of dispose will nullify the [layer] property. Subclasses must also nullify any other layer(s) it directly creates.

## Writing a RenderObject subclass

In most cases, subclassing [RenderObject] itself is overkill, and [RenderBox] would be a better starting point. However, if a render object doesn't want to use a Cartesian coordinate system, then it should indeed inherit from [RenderObject] directly. This allows it to define its own layout protocol by using a new subclass of [Constraints] rather than using [BoxConstraints], and by potentially using an entirely new set of objects and values to represent the result of the output rather than just a [Size]. This increased flexibility comes at the cost of not being able to rely on the features of [RenderBox]. For example, [RenderBox] implements an intrinsic sizing protocol that allows you to measure a child without fully laying it out, in such a way that if that child changes size, the parent will be laid out again (to take into account the new dimensions of the child). This is a subtle and bug-prone feature to get right.

Most aspects of writing a [RenderBox] apply to writing a [RenderObject] as well, and therefore the discussion at [RenderBox] is recommended background reading. The main differences are around layout and hit testing, since those are the aspects that [RenderBox] primarily specializes.

### Layout

A layout protocol begins with a subclass of [Constraints]. See the discussion at [Constraints] for more information on how to write a [Constraints] subclass.

The [performLayout] method should take the [constraints], and apply them. The output of the layout algorithm is fields set on the object that describe the geometry of the object for the purposes of the parent's layout. For example, with [RenderBox] the output is the [RenderBox.size] field. This output should only be read by the parent if the parent specified `parentUsesSize` as true when calling [layout] on the child.

Anytime anything changes on a render object that would affect the layout of that object, it should call [markNeedsLayout].

### Hit Testing

Hit testing is even more open-ended than layout. There is no method to override, you are expected to provide one.

The general behavior of your hit-testing method should be similar to the behavior described for [RenderBox]. The main difference is that the input need not be an [Offset]. You are also allowed to use a different subclass of [HitTestEntry] when adding entries to the [HitTestResult]. When the [handleEvent] method is called, the same object that was added to the [HitTestResult] will be passed in, so it can be used to track information like the precise coordinate of the hit, in whatever coordinate system is used by the new layout protocol.

### Adapting from one protocol to another

In general, the root of a Flutter render object tree is a [RenderView]. This object has a single child, which must be a [RenderBox]. Thus, if you want to have a custom [RenderObject] subclass in the render tree, you have two choices: you either need to replace the [RenderView] itself, or you need to have a [RenderBox] that has your class as its child. (The latter is the much more common case.)

This [RenderBox] subclass converts from the box protocol to the protocol of your class.

In particular, this means that for hit testing it overrides [RenderBox.hitTest], and calls whatever method you have in your class for hit testing.

Similarly, it overrides [performLayout] to create a [Constraints] object appropriate for your class and passes that to the child's [layout] method.

### Layout interactions between render objects

In general, the layout of a render object should only depend on the output of its child's layout, and then only if `parentUsesSize` is set to true in the [layout] call. Furthermore, if it is set to true, the parent must call the child's [layout] if the child is to be rendered, because otherwise the parent will not be notified when the child changes its layout outputs.

It is possible to set up render object protocols that transfer additional information. For example, in the [RenderBox] protocol you can query your children's intrinsic dimensions and baseline geometry. However, if this is done then it is imperative that the child call [markNeedsLayout] on the parent any time that additional information changes, if the parent used it in the last layout phase. For an example of how to implement this, see the [RenderBox.markNeedsLayout] method. It overrides [RenderObject.markNeedsLayout] so that if a parent has queried the intrinsic or baseline information, it gets marked dirty whenever the child's geometry changes.

### RenderObject()

```dart
RenderObject()
```

Initializes internal fields for subclasses.

### reassemble()

```dart
void reassemble()
```

Cause the entire subtree rooted at the given [RenderObject] to be marked dirty for layout, paint, etc, so that the effects of a hot reload can be seen, or so that the effect of changing a global debug flag (such as [debugPaintSizeEnabled]) can be applied.

This is called by the [RendererBinding] in response to the `ext.flutter.reassemble` hook, which is used by development tools when the application code has changed, to cause the widget tree to pick up any changed implementations.

This is expensive and should not be called except during development.

See also:

- [BindingBase.reassembleApplication]

### debugDisposed

```dart
bool? get debugDisposed
```

Whether this has been disposed.

If asserts are disabled, this property is always null.

### dispose()

```dart
void dispose()
```

Release any resources held by this render object.

The object that creates a RenderObject is in charge of disposing it. If this render object has created any children directly, it must dispose of those children in this method as well. It must not dispose of any children that were created by some other object, such as a [RenderObjectElement]. Those children will be disposed when that element unmounts, which may be delayed if the element is moved to another part of the tree.

Implementations of this method must end with a call to the inherited method, as in `super.dispose()`.

The object is no longer usable after calling dispose.

### parentData

```dart
ParentData? parentData
```

Data for use by the parent render object.

The parent data is used by the render object that lays out this object (typically this object's parent in the render tree) to store information relevant to itself and to any other nodes who happen to know exactly what the data means. The parent data is opaque to the child.

- The parent data field must not be directly set, except by calling [setupParentData] on the parent node.
- The parent data can be set before the child is added to the parent, by calling [setupParentData] on the future parent node.
- The conventions for using the parent data depend on the layout protocol used between the parent and child. For example, in box layout, the parent data is completely opaque but in sector layout the child is permitted to read some fields of the parent data.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

Override to setup parent data correctly for your children.

You can call this function to set up the parent data for child before the child is added to the parent's child list.

### depth

```dart
int get depth
```

The depth of this render object in the render tree.

The depth of nodes in a tree monotonically increases as you traverse down the tree: a node always has a [depth] greater than its ancestors. There's no guarantee regarding depth between siblings.

The [depth] of a child can be more than one greater than the [depth] of the parent, because the [depth] values are never decreased: all that matters is that it's greater than the parent. Consider a tree with a root node A, a child B, and a grandchild C. Initially, A will have [depth] 0, B [depth] 1, and C [depth] 2. If C is moved to be a child of A, sibling of B, then the numbers won't change. C's [depth] will still be 2.

The depth of a node is used to ensure that nodes are processed in depth order. The [depth] is automatically maintained by the [adoptChild] and [dropChild] methods.

### redepthChild()

```dart
void redepthChild(RenderObject child)
```

Adjust the [depth] of the given [child] to be greater than this node's own [depth].

Only call this method from overrides of [redepthChildren].

### redepthChildren()

```dart
void redepthChildren()
```

Adjust the [depth] of this node's children, if any.

Override this method in subclasses with child nodes to call [redepthChild] for each child. Do not call this method directly.

### parent

```dart
RenderObject? get parent
```

The parent of this render object in the render tree.

The [parent] of the root node in the render tree is null.

### adoptChild()

```dart
void adoptChild(RenderObject child)
```

Called by subclasses when they decide a render object is a child.

Only for use by subclasses when changing their child lists. Calling this in other cases will lead to an inconsistent tree and probably cause crashes.

### dropChild()

```dart
void dropChild(RenderObject child)
```

Called by subclasses when they decide a render object is no longer a child.

Only for use by subclasses when changing their child lists. Calling this in other cases will lead to an inconsistent tree and probably cause crashes.

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

Calls visitor for each immediate child of this render object.

Override in subclasses with children and call the visitor for each child.

### debugCreator

```dart
Object? debugCreator
```

The object responsible for creating this render object.

Used in debug messages.

See also:

- [DebugCreator], which the [widgets] library uses as values for this field.

### debugDoingThisResize

```dart
bool get debugDoingThisResize
```

Whether [performResize] for this render object is currently running.

Only valid when asserts are enabled. In release builds, always returns false.

### debugDoingThisLayout

```dart
bool get debugDoingThisLayout
```

Whether [performLayout] for this render object is currently running.

Only valid when asserts are enabled. In release builds, always returns false.

### debugActiveLayout

```dart
RenderObject? get debugActiveLayout
```

The render object that is actively computing layout.

Only valid when asserts are enabled. In release builds, always returns null.

### debugCanParentUseSize

```dart
bool get debugCanParentUseSize
```

Whether the parent render object is permitted to use this render object's size.

Determined by the `parentUsesSize` parameter to [layout].

Only valid when asserts are enabled. In release builds, throws.

### debugLayoutParent

```dart
RenderObject? get debugLayoutParent
```

The [RenderObject] that's expected to call [layout] on this [RenderObject] in its [performLayout] implementation.

This method is used to implement an assert that ensures the render subtree actively performing layout can not get accidentally mutated. It's only implemented in debug mode and always returns null in release mode.

The default implementation returns [parent] and overriding is rarely needed. A [RenderObject] subclass that expects its [RenderObject.performLayout] to be called from a different [RenderObject] that's not its [parent] should override this property to return the actual layout parent.

### owner

```dart
PipelineOwner? get owner
```

The owner for this render object (null if unattached).

The entire render tree that this render object belongs to will have the same owner.

### attached

```dart
bool get attached
```

Whether the render tree this render object belongs to is attached to a [PipelineOwner].

This becomes true during the call to [attach].

This becomes false during the call to [detach].

### attach()

```dart
void attach(PipelineOwner owner)
```

Mark this render object as attached to the given owner.

Typically called only from the [parent]'s [attach] method, and by the [owner] to mark the root of a tree as attached.

Subclasses with children should override this method to [attach] all their children to the same [owner] after calling the inherited method, as in `super.attach(owner)`.

### detach()

```dart
void detach()
```

Mark this render object as detached from its [PipelineOwner].

Typically called only from the [parent]'s [detach], and by the [owner] to mark the root of a tree as detached.

Subclasses with children should override this method to [detach] all their children after calling the inherited method, as in `super.detach()`.

### debugNeedsLayout

```dart
bool get debugNeedsLayout
```

Whether this render object's layout information is dirty.

This is only set in debug mode. In general, render objects should not need to condition their runtime behavior on whether they are dirty or not, since they should only be marked dirty immediately prior to being laid out and painted. Always returns false in non-debug builds.

It is intended to be used by tests and asserts.

### debugDoingThisLayoutWithCallback

```dart
bool get debugDoingThisLayoutWithCallback
```

Whether [invokeLayoutCallback] for this render object is currently running.

### constraints

```dart
Constraints get constraints
```

The layout constraints most recently supplied by the parent.

If layout has not yet happened, accessing this getter will throw a [StateError] exception.

### debugAssertDoesMeetConstraints()

```dart
void debugAssertDoesMeetConstraints()
```

Verify that the object's constraints are being met. Override this function in a subclass to verify that your state matches the constraints object. This function is only called when asserts are enabled (i.e. in debug mode) and only when needsLayout is false. If the constraints are not met, it should assert or throw an exception.

### debugCheckingIntrinsics

```dart
bool debugCheckingIntrinsics
```

When true, a debug method ([debugAssertDoesMeetConstraints], for instance) is currently executing asserts for verifying the consistent behavior of intrinsic dimensions methods.

This is typically set by framework debug methods. It is read by tests to selectively ignore custom layout callbacks. It should not be set outside of intrinsic-checking debug methods, and should not be checked in release mode (where it will always be false).

### markNeedsLayout()

```dart
void markNeedsLayout()
```

Mark this render object's layout information as dirty, and either register this object with its [PipelineOwner], or defer to the parent, depending on whether this object is a relayout boundary or not respectively.

## Background

Rather than eagerly updating layout information in response to writes into a render object, we instead mark the layout information as dirty, which schedules a visual update. As part of the visual update, the rendering pipeline updates the render object's layout information.

This mechanism batches the layout work so that multiple sequential writes are coalesced, removing redundant computation.

If a render object's parent indicates that it uses the size of one of its render object children when computing its layout information, this function, when called for the child, will also mark the parent as needing layout. In that case, since both the parent and the child need to have their layout recomputed, the pipeline owner is only notified about the parent; when the parent is laid out, it will call the child's [layout] method and thus the child will be laid out as well.

Once [markNeedsLayout] has been called on a render object, [debugNeedsLayout] returns true for that render object until just after the pipeline owner has called [layout] on the render object.

## Special cases

Some subclasses of [RenderObject], notably [RenderBox], have other situations in which the parent needs to be notified if the child is dirtied (e.g., if the child's intrinsic dimensions or baseline changes). Such subclasses override markNeedsLayout and either call `super.markNeedsLayout()`, in the normal case, or call [markParentNeedsLayout], in the case where the parent needs to be laid out as well as the child.

If [sizedByParent] has changed, calls [markNeedsLayoutForSizedByParentChange] instead of [markNeedsLayout].

### markParentNeedsLayout()

```dart
void markParentNeedsLayout()
```

Mark this render object's layout information as dirty, and then defer to the parent.

This function should only be called from [markNeedsLayout] or [markNeedsLayoutForSizedByParentChange] implementations of subclasses that introduce more reasons for deferring the handling of dirty layout to the parent. See [markNeedsLayout] for details.

Only call this if [parent] is not null.

### markNeedsLayoutForSizedByParentChange()

```dart
void markNeedsLayoutForSizedByParentChange()
```

Mark this render object's layout information as dirty (like [markNeedsLayout]), and additionally also handle any necessary work to handle the case where [sizedByParent] has changed value.

This should be called whenever [sizedByParent] might have changed.

Only call this if [parent] is not null.

### scheduleInitialLayout()

```dart
void scheduleInitialLayout()
```

Bootstrap the rendering pipeline by scheduling the very first layout.

Requires this render object to be attached and that this render object is the root of the render tree.

See [RenderView] for an example of how this function is used.

### layout()

```dart
void layout(Constraints constraints, {bool parentUsesSize = false})
```

Compute the layout for this render object.

This method is the main entry point for parents to ask their children to update their layout information. The parent passes a constraints object, which informs the child as to which layouts are permissible. The child is required to obey the given constraints.

If the parent reads information computed during the child's layout, the parent must pass true for `parentUsesSize`. In that case, the parent will be marked as needing layout whenever the child is marked as needing layout because the parent's layout information depends on the child's layout information. If the parent uses the default value (false) for `parentUsesSize`, the child can change its layout information (subject to the given constraints) without informing the parent.

Subclasses should not override [layout] directly. Instead, they should override [performResize] and/or [performLayout]. The [layout] method delegates the actual work to [performResize] and [performLayout].

The parent's [performLayout] method should call the [layout] of all its children unconditionally. It is the [layout] method's responsibility (as implemented here) to return early if the child does not need to do any work to update its layout information.

### debugResetSize()

```dart
void debugResetSize()
```

If a subclass has a "size" (the state controlled by `parentUsesSize`, whatever it is in the subclass, e.g. the actual `size` property of [RenderBox]), and the subclass verifies that in debug mode this "size" property isn't used when [debugCanParentUseSize] isn't set, then that subclass should override [debugResetSize] to reapply the current values of [debugCanParentUseSize] to that state.

### sizedByParent

```dart
bool get sizedByParent
```

Whether the constraints are the only input to the sizing algorithm (in particular, child nodes have no impact).

Returning false is always correct, but returning true can be more efficient when computing the size of this render object because we don't need to recompute the size if the constraints don't change.

Typically, subclasses will always return the same value. If the value can change, then, when it does change, the subclass should make sure to call [markNeedsLayoutForSizedByParentChange].

Subclasses that return true must not change the dimensions of this render object in [performLayout]. Instead, that work should be done by [performResize] or - for subclasses of [RenderBox] - in [RenderBox.computeDryLayout].

### performResize()

```dart
void performResize()
```

{@template flutter.rendering.RenderObject.performResize} Updates the render objects size using only the constraints.

Do not call this function directly: call [layout] instead. This function is called by [layout] when there is actually work to be done by this render object during layout. The layout constraints provided by your parent are available via the [constraints] getter.

This function is called only if [sizedByParent] is true. {@endtemplate}

Subclasses that set [sizedByParent] to true should override this method to compute their size. Subclasses of [RenderBox] should consider overriding [RenderBox.computeDryLayout] instead.

### performLayout()

```dart
void performLayout()
```

Do the work of computing the layout for this render object.

Do not call this function directly: call [layout] instead. This function is called by [layout] when there is actually work to be done by this render object during layout. The layout constraints provided by your parent are available via the [constraints] getter.

If [sizedByParent] is true, then this function should not actually change the dimensions of this render object. Instead, that work should be done by [performResize]. If [sizedByParent] is false, then this function should both change the dimensions of this render object and instruct its children to layout.

In implementing this function, you must call [layout] on each of your children, passing true for parentUsesSize if your layout information is dependent on your child's layout information. Passing true for parentUsesSize ensures that this render object will undergo layout if the child undergoes layout. Otherwise, the child can change its layout information without informing this render object.

Some special [RenderObject] subclasses (such as the one used by [OverlayPortal.overlayChildLayoutBuilder]) call [applyPaintTransform] in their [performLayout] implementation. To ensure such [RenderObject]s get the up-to-date paint transform, [RenderObject] subclasses should typically update the paint transform (as reported by [applyPaintTransform]) in this method instead of [paint].

### invokeLayoutCallback()

```dart
void invokeLayoutCallback<T extends Constraints>(LayoutCallback<T> callback)
```

Allows mutations to be made to this object's child list (and any descendants) as well as to any other dirty nodes in the render tree owned by the same [PipelineOwner] as this object. The `callback` argument is invoked synchronously, and the mutations are allowed only during that callback's execution.

This exists to allow child lists to be built on-demand during layout (e.g. based on the object's size), and to enable nodes to be moved around the tree as this happens (e.g. to handle [GlobalKey] reparenting), while still ensuring that any particular node is only laid out once per frame.

Calling this function disables a number of assertions that are intended to catch likely bugs. As such, using this function is generally discouraged.

This function can only be called during layout.

### debugDoingThisPaint

```dart
bool get debugDoingThisPaint
```

Whether [paint] for this render object is currently running.

Only valid when asserts are enabled. In release builds, always returns false.

### debugActivePaint

```dart
RenderObject? get debugActivePaint
```

The render object that is actively painting.

Only valid when asserts are enabled. In release builds, always returns null.

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

Whether this render object repaints separately from its parent.

Override this in subclasses to indicate that instances of your class ought to repaint independently. For example, render objects that repaint frequently might want to repaint themselves without requiring their parent to repaint.

If this getter returns true, the [paintBounds] are applied to this object and all descendants. The framework invokes [RenderObject.updateCompositedLayer] to create an [OffsetLayer] and assigns it to the [layer] field. Render objects that declare themselves as repaint boundaries must not replace the layer created by the framework.

If the value of this getter changes, [markNeedsCompositingBitsUpdate] must be called.

See [RepaintBoundary] for more information about how repaint boundaries function.

### debugRegisterRepaintBoundaryPaint()

```dart
void debugRegisterRepaintBoundaryPaint({bool includedParent = true, bool includedChild = false})
```

Called, in debug mode, if [isRepaintBoundary] is true, when either the this render object or its parent attempt to paint.

This can be used to record metrics about whether the node should actually be a repaint boundary.

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

Whether this render object always needs compositing.

Override this in subclasses to indicate that your paint function always creates at least one composited layer. For example, videos should return true if they use hardware decoders.

You must call [markNeedsCompositingBitsUpdate] if the value of this getter changes. (This is implied when [adoptChild] or [dropChild] are called.)

### updateCompositedLayer()

```dart
OffsetLayer updateCompositedLayer({required OffsetLayer? oldLayer})
```

Update the composited layer owned by this render object.

This method is called by the framework when [isRepaintBoundary] is true.

If [oldLayer] is `null`, this method must return a new [OffsetLayer] (or subtype thereof). If [oldLayer] is not `null`, then this method must reuse the layer instance that is provided - it is an error to create a new layer in this instance. The layer will be disposed by the framework when either the render object is disposed or if it is no longer a repaint boundary.

The [OffsetLayer.offset] property will be managed by the framework and must not be updated by this method.

If a property of the composited layer needs to be updated, the render object must call [markNeedsCompositedLayerUpdate] which will schedule this method to be called without repainting children. If this widget was marked as needing to paint and needing a composited layer update, this method is only called once.

### layer

```dart
ContainerLayer? get layer
```

The compositing layer that this render object uses to repaint.

If this render object is not a repaint boundary, it is the responsibility of the [paint] method to populate this field. If [needsCompositing] is true, this field may be populated with the root-most layer used by the render object implementation. When repainting, instead of creating a new layer the render object may update the layer stored in this field for better performance. It is also OK to leave this field as null and create a new layer on every repaint, but without the performance benefit. If [needsCompositing] is false, this field must be set to null either by never populating this field, or by setting it to null when the value of [needsCompositing] changes from true to false.

If a new layer is created and stored in some other field on the render object, the render object must use a [LayerHandle] to store it. A layer handle will prevent the layer from being disposed before the render object is finished with it, and it will also make sure that the layer gets appropriately disposed when the render object creates a replacement or nulls it out. The render object must null out the [LayerHandle.layer] in its [dispose] method.

If this render object is a repaint boundary, the framework automatically creates an [OffsetLayer] and populates this field prior to calling the [paint] method. The [paint] method must not replace the value of this field.

### layer

```dart
set layer(ContainerLayer? newLayer)
```

### debugLayer

```dart
ContainerLayer? get debugLayer
```

In debug mode, the compositing layer that this render object uses to repaint.

This getter is intended for debugging purposes only. In release builds, it always returns null. In debug builds, it returns the layer even if the layer is dirty.

For production code, consider [layer].

### markNeedsCompositingBitsUpdate()

```dart
void markNeedsCompositingBitsUpdate()
```

Mark the compositing state for this render object as dirty.

This is called to indicate that the value for [needsCompositing] needs to be recomputed during the next [PipelineOwner.flushCompositingBits] engine phase.

When the subtree is mutated, we need to recompute our [needsCompositing] bit, and some of our ancestors need to do the same (in case ours changed in a way that will change theirs). To this end, [adoptChild] and [dropChild] call this method, and, as necessary, this method calls the parent's, etc, walking up the tree to mark all the nodes that need updating.

This method does not schedule a rendering frame, because since it cannot be the case that _only_ the compositing bits changed, something else will have scheduled a frame for us.

### needsCompositing

```dart
bool get needsCompositing
```

Whether we or one of our descendants has a compositing layer.

If this node needs compositing as indicated by this bit, then all ancestor nodes will also need compositing.

Only legal to call after [PipelineOwner.flushLayout] and [PipelineOwner.flushCompositingBits] have been called.

### debugNeedsPaint

```dart
bool get debugNeedsPaint
```

Whether this render object's paint information is dirty.

This is only set in debug mode. In general, render objects should not need to condition their runtime behavior on whether they are dirty or not, since they should only be marked dirty immediately prior to being laid out and painted. Always returns false in non-debug builds.

It is intended to be used by tests and asserts.

It is possible (and indeed, quite common) for [debugNeedsPaint] to be false and [debugNeedsLayout] to be true. The render object will still be repainted in the next frame when this is the case, because the [markNeedsPaint] method is implicitly called by the framework after a render object is laid out, prior to the paint phase.

### debugNeedsCompositedLayerUpdate

```dart
bool get debugNeedsCompositedLayerUpdate
```

Whether this render object's layer information is dirty.

This is only set in debug mode. In general, render objects should not need to condition their runtime behavior on whether they are dirty or not, since they should only be marked dirty immediately prior to being laid out and painted. Always returns false in non-debug builds.

It is intended to be used by tests and asserts.

### markNeedsPaint()

```dart
void markNeedsPaint()
```

Mark this render object as having changed its visual appearance.

Rather than eagerly updating this render object's display list in response to writes, we instead mark the render object as needing to paint, which schedules a visual update. As part of the visual update, the rendering pipeline will give this render object an opportunity to update its display list.

This mechanism batches the painting work so that multiple sequential writes are coalesced, removing redundant computation.

Once [markNeedsPaint] has been called on a render object, [debugNeedsPaint] returns true for that render object until just after the pipeline owner has called [paint] on the render object.

See also:

- [RepaintBoundary], to scope a subtree of render objects to their own layer, thus limiting the number of nodes that [markNeedsPaint] must mark dirty.

### markNeedsCompositedLayerUpdate()

```dart
void markNeedsCompositedLayerUpdate()
```

Mark this render object as having changed a property on its composited layer.

Render objects that have a composited layer have [isRepaintBoundary] equal to true may update the properties of that composited layer without repainting their children. If this render object is a repaint boundary but does not yet have a composited layer created for it, this method will instead mark the nearest repaint boundary parent as needing to be painted.

If this method is called on a render object that is not a repaint boundary or is a repaint boundary but hasn't been composited yet, it is equivalent to calling [markNeedsPaint].

See also:

- [RenderOpacity], which uses this method when its opacity is updated to update the layer opacity without repainting children.

### scheduleInitialPaint()

```dart
void scheduleInitialPaint(ContainerLayer rootLayer)
```

Bootstrap the rendering pipeline by scheduling the very first paint.

Requires that this render object is attached, is the root of the render tree, and has a composited layer.

See [RenderView] for an example of how this function is used.

### replaceRootLayer()

```dart
void replaceRootLayer(OffsetLayer rootLayer)
```

Replace the layer. This is only valid for the root of a render object subtree (whatever object [scheduleInitialPaint] was called on).

This might be called if, e.g., the device pixel ratio changed.

### paintBounds

```dart
Rect get paintBounds
```

An estimate of the bounds within which this render object will paint. Useful for debugging flags such as [debugPaintLayerBordersEnabled].

These are also the bounds used by [showOnScreen] to make a [RenderObject] visible on screen.

### debugPaint()

```dart
void debugPaint(PaintingContext context, Offset offset)
```

Override this method to paint debugging information.

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

Paint this render object into the given context at the given offset.

Subclasses should override this method to provide a visual appearance for themselves. The render object's local coordinate system is axis-aligned with the coordinate system of the context's canvas and the render object's local origin (i.e, x=0 and y=0) is placed at the given offset in the context's canvas.

Do not call this function directly. If you wish to paint yourself, call [markNeedsPaint] instead to schedule a call to this function. If you wish to paint one of your children, call [PaintingContext.paintChild] on the given `context`.

When painting one of your children (via a paint child function on the given context), the current canvas held by the context might change because draw operations before and after painting children might need to be recorded on separate compositing layers.

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

Applies the transform that would be applied when painting the given child to the given matrix.

Used by coordinate conversion functions ([getTransformTo], for example) to translate coordinates local to one render object into coordinates local to another render object.

Some RenderObjects will provide a zeroed out matrix in this method, indicating that the child should not paint anything or respond to hit tests currently. A parent may supply a non-zero matrix even though it does not paint its child currently, for example if the parent is a [RenderOffstage] with `offstage` set to true. In both of these cases, the parent must return `false` from [paintsChild].

### paintsChild()

```dart
bool paintsChild(RenderObject child)
```

Whether the given child would be painted if [paint] were called.

Some RenderObjects skip painting their children if they are configured to not produce any visible effects. For example, a [RenderOffstage] with its `offstage` property set to true, or a [RenderOpacity] with its opacity value set to zero.

In these cases, the parent may still supply a non-zero matrix in [applyPaintTransform] to inform callers about where it would paint the child if the child were painted at all. Alternatively, the parent may supply a zeroed out matrix if it would not otherwise be able to determine a valid matrix for the child and thus cannot meaningfully determine where the child would paint.

### getTransformTo()

```dart
Matrix4 getTransformTo(RenderObject? target)
```

{@template flutter.rendering.RenderObject.getTransformTo} Applies the paint transform from this [RenderObject] to the `target` [RenderObject].

Returns a matrix that maps the local paint coordinate system to the coordinate system of `target`, or a [Matrix4.zero] if the paint transform can not be computed.

This method throws an exception when the `target` is not in the same render tree as this [RenderObject], as the behavior is undefined.

This method ignores [RenderObject.paintsChild]. This means it will still try to compute the paint transform even if this [RenderObject] or `target` is currently not visible.

If `target` is null, this method returns a matrix that maps from the local paint coordinate system to the coordinate system of the [PipelineOwner.rootNode]. {@endtemplate}

For the render tree owned by the [RendererBinding] (i.e. for the main render tree displayed on the device) this means that this method maps to the global coordinate system in logical pixels. To get physical pixels, use [applyPaintTransform] from the [RenderView] to further transform the coordinate.

### describeApproximatePaintClip()

```dart
Rect? describeApproximatePaintClip(RenderObject child)
```

Returns a rect in this object's coordinate system that describes the approximate bounding box of the clip rect that would be applied to the given child during the paint phase, if any.

Returns null if the child would not be clipped.

This is used in the semantics phase to avoid including children that are not physically visible.

RenderObjects that respect a [Clip] behavior when painting _must_ respect that same behavior when describing this value. For example, if passing [Clip.none] to [PaintingContext.pushClipRect] as the `clipBehavior`, then the implementation of this method must return null.

### describeSemanticsClip()

```dart
Rect? describeSemanticsClip(RenderObject? child)
```

Returns a rect in this object's coordinate system that describes which [SemanticsNode]s produced by the `child` should be included in the semantics tree. [SemanticsNode]s from the `child` that are positioned outside of this rect will be dropped. Child [SemanticsNode]s that are positioned inside this rect, but outside of [describeApproximatePaintClip] will be included in the tree marked as hidden. Child [SemanticsNode]s that are inside of both rect will be included in the tree as regular nodes.

This method only returns a non-null value if the semantics clip rect is different from the rect returned by [describeApproximatePaintClip]. If the semantics clip rect and the paint clip rect are the same, this method returns null.

A viewport would typically implement this method to include semantic nodes in the semantics tree that are currently hidden just before the leading or just after the trailing edge. These nodes have to be included in the semantics tree to implement implicit accessibility scrolling on iOS where the viewport scrolls implicitly when moving the accessibility focus from the last visible node in the viewport to the first hidden one.

See also:

- [RenderViewportBase.cacheExtent], used by viewports to extend their semantics clip beyond their approximate paint clip.

### scheduleInitialSemantics()

```dart
void scheduleInitialSemantics()
```

Bootstrap the semantics reporting mechanism by marking this node as needing a semantics update.

Requires that this render object is attached, and is the root of the render tree.

See [RendererBinding] for an example of how this function is used.

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

Report the semantics of this node, for example for accessibility purposes.

This method should be overridden by subclasses that have interesting semantic information.

The given [SemanticsConfiguration] object is mutable and should be annotated in a manner that describes the current state. No reference should be kept to that object; mutating it outside of the context of the [describeSemanticsConfiguration] call (for example as a result of asynchronous computation) will at best have no useful effect and at worse will cause crashes as the data will be in an inconsistent state.

{@tool snippet}

The following snippet will describe the node as a button that responds to tap actions.

```dart
abstract class SemanticButtonRenderObject extends RenderObject {
  @override
  void describeSemanticsConfiguration(SemanticsConfiguration config) {
    super.describeSemanticsConfiguration(config);
    config
      ..onTap = _handleTap
      ..label = 'I am a button'
      ..isButton = true;
  }

  void _handleTap() {
    // Do something.
  }
}
```

{@end-tool}

### sendSemanticsEvent()

```dart
void sendSemanticsEvent(SemanticsEvent semanticsEvent)
```

Sends a [SemanticsEvent] associated with this render object's [SemanticsNode].

If this render object has no semantics information, the first parent render object with a non-null semantic node is used.

If semantics are disabled, no events are dispatched.

See [SemanticsNode.sendEvent] for a full description of the behavior.

### semanticBounds

```dart
Rect get semanticBounds
```

The bounding box, in the local coordinate system, of this object, for accessibility purposes.

### debugNeedsSemanticsUpdate

```dart
bool get debugNeedsSemanticsUpdate
```

Whether the semantics of this render object is dirty and await the update.

Always returns false in release mode.

### debugSemantics

```dart
SemanticsNode? get debugSemantics
```

The semantics of this render object.

Exposed only for testing and debugging. To learn about the semantics of render objects in production, obtain a [SemanticsHandle] from [PipelineOwner.ensureSemantics].

Only valid in debug and profile mode. In release builds, always returns null.

### clearSemantics()

```dart
void clearSemantics()
```

Removes all semantics from this render object and its descendants.

Should only be called on objects whose [parent] is not a [RenderObject].

Override this method if you instantiate new [SemanticsNode]s in an overridden [assembleSemanticsNode] method, to dispose of those nodes.

### markNeedsSemanticsUpdate()

```dart
void markNeedsSemanticsUpdate()
```

Mark this node as needing an update to its semantics description.

This must be called whenever the semantics configuration of this [RenderObject] as annotated by [describeSemanticsConfiguration] changes in any way to update the semantics tree.

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

Called when collecting the semantics of this node.

The implementation has to return the children in paint order skipping all children that are not semantically relevant (e.g. because they are invisible).

The default implementation mirrors the behavior of [visitChildren] (which is supposed to walk all the children).

### assembleSemanticsNode()

```dart
void assembleSemanticsNode(SemanticsNode node, SemanticsConfiguration config, Iterable<SemanticsNode> children)
```

Assemble the [SemanticsNode] for this [RenderObject].

If [describeSemanticsConfiguration] sets [SemanticsConfiguration.isSemanticBoundary] to true, this method is called with the `node` created for this [RenderObject], the `config` to be applied to that node and the `children` [SemanticsNode]s that descendants of this RenderObject have generated.

By default, the method will annotate `node` with `config` and add the `children` to it.

Subclasses can override this method to add additional [SemanticsNode]s to the tree. If new [SemanticsNode]s are instantiated in this method they must be disposed in [clearSemantics].

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

Override this method to handle pointer events that hit this render object.

### toStringShort()

```dart
String toStringShort()
```

Returns a human understandable name.

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

### toStringDeep()

```dart
String toStringDeep({String prefixLineOne = '', String? prefixOtherLines = '', DiagnosticLevel minLevel = DiagnosticLevel.debug, int wrapWidth = 65})
```

Returns a description of the tree rooted at this node. If the prefix argument is provided, then every line in the output will be prefixed by that string.

### toStringShallow()

```dart
String toStringShallow({String joiner = ', ', DiagnosticLevel minLevel = DiagnosticLevel.debug})
```

Returns a one-line detailed description of the render object. This description is often somewhat long.

This includes the same information for this RenderObject as given by [toStringDeep], but does not recurse to any children.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

Attempt to make (a portion of) this or a descendant [RenderObject] visible on screen.

If `descendant` is provided, that [RenderObject] is made visible. If `descendant` is omitted, this [RenderObject] is made visible.

The optional `rect` parameter describes which area of that [RenderObject] should be shown on screen. If `rect` is null, the entire [RenderObject] (as defined by its [paintBounds]) will be revealed. The `rect` parameter is interpreted relative to the coordinate system of `descendant` if that argument is provided and relative to this [RenderObject] otherwise.

The `duration` parameter can be set to a non-zero value to bring the target object on screen in an animation defined by `curve`.

See also:

- [RenderViewportBase.showInViewport], which [RenderViewportBase] and [SingleChildScrollView] delegate this method to.

### describeForError()

```dart
DiagnosticsNode describeForError(String name, {DiagnosticsTreeStyle style = DiagnosticsTreeStyle.shallow})
```

Adds a debug representation of a [RenderObject] optimized for including in error messages.

The default [style] of [DiagnosticsTreeStyle.shallow] ensures that all of the properties of the render object are included in the error output but none of the children of the object are.

You should always include a RenderObject in an error message if it is the [RenderObject] causing the failure or contract violation of the error.

# RenderObjectWithChildMixin

```dart
mixin RenderObjectWithChildMixin<ChildType extends RenderObject> on RenderObject {}
```

Generic mixin for render objects with one child.

Provides a child model for a render object subclass that has a unique child, which is accessible via the [child] getter.

This mixin is typically used to implement render objects created in a [SingleChildRenderObjectWidget].

### debugValidateChild()

```dart
bool debugValidateChild(RenderObject child)
```

Checks whether the given render object has the correct [runtimeType] to be a child of this render object.

Does nothing if assertions are disabled.

Always returns true.

### child

```dart
ChildType? get child
```

The render object's unique child.

### child

```dart
set child(ChildType? value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# RenderObjectWithLayoutCallbackMixin

```dart
mixin RenderObjectWithLayoutCallbackMixin on RenderObject {}
```

A mixin for managing [RenderObject] with a [layoutCallback], which will be invoked during this [RenderObject]'s layout process if scheduled using [scheduleLayoutCallback].

A layout callback is typically a callback that mutates the [RenderObject]'s render subtree during the [RenderObject]'s layout process. When an ancestor [RenderObject] chooses to skip laying out this [RenderObject] in its [performLayout] implementation (for example, for performance reasons, an [Overlay] may skip laying out an offstage [OverlayEntry] while keeping it in the tree), normally the [layoutCallback] will not be invoked because the [layout] method will not be called. This can be undesirable when the [layoutCallback] involves rebuilding dirty widgets (most notably, the [LayoutBuilder] widget). Unlike render subtrees, typically all dirty widgets (even off-screen ones) in a widget tree must be rebuilt. This mixin makes sure once scheduled, the [layoutCallback] method will be invoked even if it's skipped by an ancestor [RenderObject], unless this [RenderObject] has never been laid out.

Subclasses must not invoke the layout callback directly. Instead, call [runLayoutCallback] in the [performLayout] implementation.

See also:

- [LayoutBuilder] and [SliverLayoutBuilder], which use the mixin.

### layoutCallback()

```dart
void layoutCallback()
```

The layout callback to be invoked during [performLayout].

This method should not be invoked directly. Instead, call [runLayoutCallback] in the [performLayout] implementation. This callback will be invoked using [invokeLayoutCallback].

### runLayoutCallback()

```dart
void runLayoutCallback()
```

Invokes [layoutCallback] with [invokeLayoutCallback].

This method must be called in [performLayout], typically as early as possible before any layout work is done, to avoid re-dirtying any child [RenderObject]s.

### scheduleLayoutCallback()

```dart
void scheduleLayoutCallback()
```

Informs the framework that the layout callback has been updated and must be invoked again when this [RenderObject] is ready for layout, even when an ancestor [RenderObject] chooses to skip laying out this render subtree.

# ContainerParentDataMixin

```dart
mixin ContainerParentDataMixin<ChildType extends RenderObject> on ParentData {}
```

Parent data to support a doubly-linked list of children.

The children can be traversed using [nextSibling] or [previousSibling], which can be called on the parent data of the render objects obtained via [ContainerRenderObjectMixin.firstChild] or [ContainerRenderObjectMixin.lastChild].

### previousSibling

```dart
ChildType? previousSibling
```

The previous sibling in the parent's child list.

### nextSibling

```dart
ChildType? nextSibling
```

The next sibling in the parent's child list.

### detach()

```dart
void detach()
```

Clear the sibling pointers.

# ContainerRenderObjectMixin

```dart
mixin ContainerRenderObjectMixin<ChildType extends RenderObject, ParentDataType extends ContainerParentDataMixin<ChildType>> on RenderObject {}
```

Generic mixin for render objects with a list of children.

Provides a child model for a render object subclass that has a doubly-linked list of children.

The [ChildType] specifies the type of the children (extending [RenderObject]), e.g. [RenderBox].

[ParentDataType] stores parent container data on its child render objects. It must extend [ContainerParentDataMixin], which provides the interface for visiting children. This data is populated by [RenderObject.setupParentData] implemented by the class using this mixin.

When using [RenderBox] as the child type, you will usually want to make use of [RenderBoxContainerDefaultsMixin] and extend [ContainerBoxParentData] for the parent data.

Moreover, this is a required mixin for render objects returned to [MultiChildRenderObjectWidget].

See also:

- [SlottedContainerRenderObjectMixin], which organizes its children in different named slots.

### childCount

```dart
int get childCount
```

The number of children.

### debugValidateChild()

```dart
bool debugValidateChild(RenderObject child)
```

Checks whether the given render object has the correct [runtimeType] to be a child of this render object.

Does nothing if assertions are disabled.

Always returns true.

### insert()

```dart
void insert(ChildType child, {ChildType? after})
```

Insert child into this render object's child list after the given child.

If `after` is null, then this inserts the child at the start of the list, and the child becomes the new [firstChild].

### add()

```dart
void add(ChildType child)
```

Append child to the end of this render object's child list.

### addAll()

```dart
void addAll(List<ChildType>? children)
```

Add all the children to the end of this render object's child list.

### remove()

```dart
void remove(ChildType child)
```

Remove this child from the child list.

Requires the child to be present in the child list.

### removeAll()

```dart
void removeAll()
```

Remove all their children from this render object's child list.

More efficient than removing them individually.

### move()

```dart
void move(ChildType child, {ChildType? after})
```

Move the given `child` in the child list to be after another child.

More efficient than removing and re-adding the child. Requires the child to already be in the child list at some position. Pass null for `after` to move the child to the start of the child list.

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### firstChild

```dart
ChildType? get firstChild
```

The first child in the child list.

### lastChild

```dart
ChildType? get lastChild
```

The last child in the child list.

### childBefore()

```dart
ChildType? childBefore(ChildType child)
```

The previous child before the given child in the child list.

### childAfter()

```dart
ChildType? childAfter(ChildType child)
```

The next child after the given child in the child list.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# RelayoutWhenSystemFontsChangeMixin

```dart
mixin RelayoutWhenSystemFontsChangeMixin on RenderObject {}
```

Mixin for [RenderObject] that will call [systemFontsDidChange] whenever the system fonts change.

System fonts can change when the OS installs or removes a font. Use this mixin if the [RenderObject] uses [TextPainter] or [Paragraph] to correctly update the text when it happens.

### systemFontsDidChange()

```dart
void systemFontsDidChange()
```

A callback that is called when system fonts have changed.

The framework defers the invocation of the callback to the [SchedulerPhase.transientCallbacks] phase to ensure that the [RenderObject]'s text layout is still valid when user interactions are in progress (which usually take place during the [SchedulerPhase.idle] phase).

By default, [markNeedsLayout] is called on the [RenderObject] implementing this mixin.

Subclass should override this method to clear any extra cache that depend on font-related metrics.

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

# SemanticsAnnotationsMixin

```dart
mixin SemanticsAnnotationsMixin on RenderObject {}
```

A mixin for [RenderObject]s that want to annotate the [SemanticsNode] for their subtree.

### initSemanticsAnnotations()

```dart
void initSemanticsAnnotations({required SemanticsProperties properties, required bool container, required bool explicitChildNodes, required bool excludeSemantics, required bool blockUserActions, required Locale? localeForSubtree, required TextDirection? textDirection})
```

Initializes the semantics annotations for this mixin.

### properties

```dart
SemanticsProperties get properties
```

All of the [SemanticsProperties] for this [SemanticsAnnotationsMixin].

### properties

```dart
set properties(SemanticsProperties value)
```

### container

```dart
bool get container
```

If 'container' is true, this [RenderObject] will introduce a new node in the semantics tree. Otherwise, the semantics will be merged with the semantics of any ancestors.

Whether descendants of this [RenderObject] can add their semantic information to the [SemanticsNode] introduced by this configuration is controlled by [explicitChildNodes].

### container

```dart
set container(bool value)
```

### explicitChildNodes

```dart
bool get explicitChildNodes
```

Whether descendants of this [RenderObject] are allowed to add semantic information to the [SemanticsNode] annotated by this widget.

When set to false descendants are allowed to annotate [SemanticsNode]s of their parent with the semantic information they want to contribute to the semantic tree. When set to true the only way for descendants to contribute semantic information to the semantic tree is to introduce new explicit [SemanticsNode]s to the tree.

This setting is often used in combination with [SemanticsConfiguration.isSemanticBoundary] to create semantic boundaries that are either writable or not for children.

### explicitChildNodes

```dart
set explicitChildNodes(bool value)
```

### excludeSemantics

```dart
bool get excludeSemantics
```

Whether descendants of this [RenderObject] should have their semantic information ignored.

When this flag is set to true, all child semantics nodes are ignored. This can be used as a convenience for cases where a child is wrapped in an [ExcludeSemantics] widget and then another [Semantics] widget.

### excludeSemantics

```dart
set excludeSemantics(bool value)
```

### blockUserActions

```dart
bool get blockUserActions
```

Whether to block user interactions for the semantics subtree.

Setting this true prevents user from activating pointer related [SemanticsAction]s, such as [SemanticsAction.tap] or [SemanticsAction.longPress].

### blockUserActions

```dart
set blockUserActions(bool value)
```

### localeForSubtree

```dart
Locale? get localeForSubtree
```

The [Locale] for the semantics subtree.

Setting this to null will inherit locale from ancestor semantics node.

### localeForSubtree

```dart
set localeForSubtree(Locale? value)
```

### textDirection

```dart
TextDirection? get textDirection
```

If non-null, sets the [SemanticsNode.textDirection] semantic to the given value.

This must not be null if [SemanticsProperties.attributedLabel], [SemanticsProperties.attributedHint], [SemanticsProperties.attributedValue], [SemanticsProperties.attributedIncreasedValue], or [SemanticsProperties.attributedDecreasedValue] are not null.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

# debugDumpRenderObjectSemanticsTree()

```dart
void debugDumpRenderObjectSemanticsTree()
```

Dumps the render object semantics tree.

# DiagnosticsDebugCreator

```dart
class DiagnosticsDebugCreator extends DiagnosticsProperty<Object> {}
```

A class that creates [DiagnosticsNode] by wrapping [RenderObject.debugCreator].

Attach a [DiagnosticsDebugCreator] into [FlutterErrorDetails.informationCollector] when a [RenderObject.debugCreator] is available. This will lead to improved error message.

### DiagnosticsDebugCreator()

```dart
DiagnosticsDebugCreator(Object value)
```

Create a [DiagnosticsProperty] with its [value] initialized to input [RenderObject.debugCreator].
