@docImport 'package:flutter/services.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'binding.dart'; @docImport 'object.dart'; @docImport 'performance_overlay.dart'; @docImport 'proxy_box.dart'; @docImport 'view.dart';

# AnnotationEntry

```dart
class AnnotationEntry<T> {}
```

Information collected for an annotation that is found in the layer tree.

See also:

- [Layer.findAnnotations], which create and use objects of this class.

### AnnotationEntry()

```dart
AnnotationEntry({required T annotation, required Offset localPosition})
```

Create an entry of found annotation by providing the object and related information.

### annotation

```dart
T annotation
```

The annotation object that is found.

### localPosition

```dart
Offset localPosition
```

The target location described by the local coordinate space of the annotation object.

### toString()

```dart
String toString()
```

# AnnotationResult

```dart
class AnnotationResult<T> {}
```

Information collected about a list of annotations that are found in the layer tree.

See also:

- [AnnotationEntry], which are members of this class.
- [Layer.findAllAnnotations], and [Layer.findAnnotations], which create and use an object of this class.

### add()

```dart
void add(AnnotationEntry<T> entry)
```

Add a new entry to the end of the result.

Usually, entries should be added in order from most specific to least specific, typically during an upward walk of the tree.

### entries

```dart
Iterable<AnnotationEntry<T>> get entries
```

An unmodifiable list of [AnnotationEntry] objects recorded.

The first entry is the most specific, typically the one at the leaf of tree.

### annotations

```dart
Iterable<T> get annotations
```

An unmodifiable list of annotations recorded.

The first entry is the most specific, typically the one at the leaf of tree.

It is similar to [entries] but does not contain other information.

# Layer

```dart
abstract class Layer with DiagnosticableTreeMixin {}
```

A composited layer.

During painting, the render tree generates a tree of composited layers that are uploaded into the engine and displayed by the compositor. This class is the base class for all composited layers.

Most layers can have their properties mutated, and layers can be moved to different parents. The scene must be explicitly recomposited after such changes are made; the layer tree does not maintain its own dirty state.

To composite the tree, create a [ui.SceneBuilder] object using [RendererBinding.createSceneBuilder], pass it to the root [Layer] object's [addToScene] method, and then call [ui.SceneBuilder.build] to obtain a [ui.Scene]. A [ui.Scene] can then be painted using [ui.FlutterView.render].

## Memory

Layers retain resources between frames to speed up rendering. A layer will retain these resources until all [LayerHandle]s referring to the layer have nulled out their references.

Layers must not be used after disposal. If a RenderObject needs to maintain a layer for later usage, it must create a handle to that layer. This is handled automatically for the [RenderObject.layer] property, but additional layers must use their own [LayerHandle].

{@tool snippet}

This [RenderObject] is a repaint boundary that pushes an additional [ClipRectLayer].

```dart
class ClippingRenderObject extends RenderBox {
  final LayerHandle<ClipRectLayer> _clipRectLayer = LayerHandle<ClipRectLayer>();

  @override
  bool get isRepaintBoundary => true; // The [layer] property will be used.

  @override
  void paint(PaintingContext context, Offset offset) {
    _clipRectLayer.layer = context.pushClipRect(
      needsCompositing,
      offset,
      Offset.zero & size,
      super.paint,
      oldLayer: _clipRectLayer.layer,
    );
  }

  @override
  void dispose() {
    _clipRectLayer.layer = null;
    super.dispose();
  }
}
```

{@end-tool} See also:

- [RenderView.compositeFrame], which implements this recomposition protocol for painting [RenderObject] trees on the display.

### Layer()

```dart
Layer()
```

Creates an instance of Layer.

### subtreeHasCompositionCallbacks

```dart
bool get subtreeHasCompositionCallbacks
```

Whether the subtree rooted at this layer has any composition callback observers.

This only evaluates to true if the subtree rooted at this node has observers. For example, it may evaluate to true on a parent node but false on a child if the parent has observers but the child does not.

See also:

- [Layer.addCompositionCallback].

### supportsRasterization()

```dart
bool supportsRasterization()
```

Whether or not this layer, or any child layers, can be rasterized with [ui.Scene.toImage] or [ui.Scene.toImageSync].

If `false`, calling the above methods may yield an image which is incomplete.

This value may change throughout the lifetime of the object, as the child layers themselves are added or removed.

### describeClipBounds()

```dart
Rect? describeClipBounds()
```

Describes the clip that would be applied to contents of this layer, if any.

### addCompositionCallback()

```dart
VoidCallback addCompositionCallback(CompositionCallback callback)
```

Adds a callback for when the layer tree that this layer is part of gets composited, or when it is detached and will not be rendered again.

This callback will fire even if an ancestor layer is added with retained rendering, meaning that it will fire even if this layer gets added to the scene via some call to [ui.SceneBuilder.addRetained] on one of its ancestor layers.

The callback receives a reference to this layer. The recipient must not mutate the layer during the scope of the callback, but may traverse the tree to find information about the current transform or clip. The layer may not be [attached] anymore in this state, but even if it is detached it may still have an also detached parent it can visit.

If new callbacks are added or removed within the [callback], the new callbacks will fire (or stop firing) on the _next_ compositing event.

{@template flutter.rendering.Layer.compositionCallbacks} Composition callbacks are useful in place of pushing a layer that would otherwise try to observe the layer tree without actually affecting compositing. For example, a composition callback may be used to observe the total transform and clip of the current container layer to determine whether a render object drawn into it is visible or not.

Calling the returned callback will remove [callback] from the composition callbacks. {@endtemplate}

### debugDisposed

```dart
bool get debugDisposed
```

If asserts are enabled, returns whether [dispose] has been called since the last time any retained resources were created.

Throws an exception if asserts are disabled.

### debugHandleCount

```dart
int get debugHandleCount
```

Returns the number of objects holding a [LayerHandle] to this layer.

This method throws if asserts are disabled.

### dispose()

```dart
void dispose()
```

Clears any retained resources that this layer holds.

This method must dispose resources such as [ui.EngineLayer] and [ui.Picture] objects. The layer is still usable after this call, but any graphics related resources it holds will need to be recreated.

This method _only_ disposes resources for this layer. For example, if it is a [ContainerLayer], it does not dispose resources of any children. However, [ContainerLayer]s do remove any children they have when this method is called, and if this layer was the last holder of a removed child handle, the child may recursively clean up its resources.

This method automatically gets called when all outstanding [LayerHandle]s are disposed. [LayerHandle] objects are typically held by the [parent] layer of this layer and any [RenderObject]s that participated in creating it.

After calling this method, the object is unusable.

### parent

```dart
ContainerLayer? get parent
```

This layer's parent in the layer tree.

The [parent] of the root node in the layer tree is null.

Only subclasses of [ContainerLayer] can have children in the layer tree. All other layer classes are used for leaves in the layer tree.

### markNeedsAddToScene()

```dart
void markNeedsAddToScene()
```

Mark that this layer has changed and [addToScene] needs to be called.

### debugMarkClean()

```dart
void debugMarkClean()
```

Mark that this layer is in sync with engine.

This is for debugging and testing purposes only. In release builds this method has no effect.

### alwaysNeedsAddToScene

```dart
bool get alwaysNeedsAddToScene
```

Subclasses may override this to true to disable retained rendering.

### debugSubtreeNeedsAddToScene

```dart
bool? get debugSubtreeNeedsAddToScene
```

Whether this or any descendant layer in the subtree needs [addToScene].

This is for debug and test purpose only. It only becomes valid after calling [updateSubtreeNeedsAddToScene].

### engineLayer

```dart
ui.EngineLayer? get engineLayer
```

Stores the engine layer created for this layer in order to reuse engine resources across frames for better app performance.

This value may be passed to [ui.SceneBuilder.addRetained] to communicate to the engine that nothing in this layer or any of its descendants changed. The native engine could, for example, reuse the texture rendered in a previous frame. The web engine could, for example, reuse the HTML DOM nodes created for a previous frame.

This value may be passed as `oldLayer` argument to a "push" method to communicate to the engine that a layer is updating a previously rendered layer. The web engine could, for example, update the properties of previously rendered HTML DOM nodes rather than creating new nodes.

### engineLayer

```dart
set engineLayer(ui.EngineLayer? value)
```

Sets the engine layer used to render this layer.

Typically this field is set to the value returned by [addToScene], which in turn returns the engine layer produced by one of [ui.SceneBuilder]'s "push" methods, such as [ui.SceneBuilder.pushOpacity].

### updateSubtreeNeedsAddToScene()

```dart
void updateSubtreeNeedsAddToScene()
```

Traverses the layer subtree starting from this layer and determines whether it needs [addToScene].

A layer needs [addToScene] if any of the following is true:

- [alwaysNeedsAddToScene] is true.
- [markNeedsAddToScene] has been called.
- Any of its descendants need [addToScene].

[ContainerLayer] overrides this method to recursively call it on its children.

### owner

```dart
Object? get owner
```

The owner for this layer (null if unattached).

The entire layer tree that this layer belongs to will have the same owner.

Typically the owner is a [RenderView].

### attached

```dart
bool get attached
```

Whether the layer tree containing this layer is attached to an owner.

This becomes true during the call to [attach].

This becomes false during the call to [detach].

### attach()

```dart
void attach(Object owner)
```

Mark this layer as attached to the given owner.

Typically called only from the [parent]'s [attach] method, and by the [owner] to mark the root of a tree as attached.

Subclasses with children should override this method to [attach] all their children to the same [owner] after calling the inherited method, as in `super.attach(owner)`.

### detach()

```dart
void detach()
```

Mark this layer as detached from its owner.

Typically called only from the [parent]'s [detach], and by the [owner] to mark the root of a tree as detached.

Subclasses with children should override this method to [detach] all their children after calling the inherited method, as in `super.detach()`.

### depth

```dart
int get depth
```

The depth of this layer in the layer tree.

The depth of nodes in a tree monotonically increases as you traverse down the tree. There's no guarantee regarding depth between siblings.

The depth is used to ensure that nodes are processed in depth order.

### redepthChildren()

```dart
void redepthChildren()
```

Adjust the [depth] of this node's children, if any.

Override this method in subclasses with child nodes to call [ContainerLayer.redepthChild] for each child. Do not call this method directly.

### nextSibling

```dart
Layer? get nextSibling
```

This layer's next sibling in the parent layer's child list.

### previousSibling

```dart
Layer? get previousSibling
```

This layer's previous sibling in the parent layer's child list.

### remove()

```dart
void remove()
```

Removes this layer from its parent layer's child list.

This has no effect if the layer's parent is already null.

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

Search this layer and its subtree for annotations of type `S` at the location described by `localPosition`.

This method is called by the default implementation of [find] and [findAllAnnotations]. Override this method to customize how the layer should search for annotations, or if the layer has its own annotations to add.

The default implementation always returns `false`, which means neither the layer nor its children has annotations, and the annotation search is not absorbed either (see below for explanation).

## About layer annotations

{@template flutter.rendering.Layer.findAnnotations.aboutAnnotations} An annotation is an optional object of any type that can be carried with a layer. An annotation can be found at a location as long as the owner layer contains the location and is walked to.

The annotations are searched by first visiting each child recursively, then this layer, resulting in an order from visually front to back. Annotations must meet the given restrictions, such as type and position.

The common way for a value to be found here is by pushing an [AnnotatedRegionLayer] into the layer tree, or by adding the desired annotation by overriding [findAnnotations]. {@endtemplate}

## Parameters and return value

The [result] parameter is where the method outputs the resulting annotations. New annotations found during the walk are added to the tail.

The [onlyFirst] parameter indicates that, if true, the search will stop when it finds the first qualified annotation; otherwise, it will walk the entire subtree.

The return value indicates the opacity of this layer and its subtree at this position. If it returns true, then this layer's parent should skip the children behind this layer. In other words, it is opaque to this type of annotation and has absorbed the search so that its siblings behind it are not aware of the search. If the return value is false, then the parent might continue with other siblings.

The return value does not affect whether the parent adds its own annotations; in other words, if a layer is supposed to add an annotation, it will always add it even if its children are opaque to this type of annotation. However, the opacity that the parents return might be affected by their children, hence making all of its ancestors opaque to this type of annotation.

### find()

```dart
S? find<S extends Object>(Offset localPosition)
```

Search this layer and its subtree for the first annotation of type `S` under the point described by `localPosition`.

Returns null if no matching annotations are found.

By default this method calls [findAnnotations] with `onlyFirst: true` and returns the annotation of the first result. Prefer overriding [findAnnotations] instead of this method, because during an annotation search, only [findAnnotations] is recursively called, while custom behavior in this method is ignored.

## About layer annotations

{@macro flutter.rendering.Layer.findAnnotations.aboutAnnotations}

See also:

- [findAllAnnotations], which is similar but returns all annotations found at the given position.
- [AnnotatedRegionLayer], for placing values in the layer tree.

### findAllAnnotations()

```dart
AnnotationResult<S> findAllAnnotations<S extends Object>(Offset localPosition)
```

Search this layer and its subtree for all annotations of type `S` under the point described by `localPosition`.

Returns a result with empty entries if no matching annotations are found.

By default this method calls [findAnnotations] with `onlyFirst: false` and returns the annotations of its result. Prefer overriding [findAnnotations] instead of this method, because during an annotation search, only [findAnnotations] is recursively called, while custom behavior in this method is ignored.

## About layer annotations

{@macro flutter.rendering.Layer.findAnnotations.aboutAnnotations}

See also:

- [find], which is similar but returns the first annotation found at the given position.
- [AnnotatedRegionLayer], for placing values in the layer tree.

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

Override this method to upload this layer to the engine.

### debugCreator

```dart
Object? debugCreator
```

The object responsible for creating this layer.

Defaults to the value of [RenderObject.debugCreator] for the render object that created this layer. Used in debug messages.

### toStringShort()

```dart
String toStringShort()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LayerHandle

```dart
class LayerHandle<T extends Layer> {}
```

A handle to prevent a [Layer]'s platform graphics resources from being disposed.

[Layer] objects retain native resources such as [ui.EngineLayer]s and [ui.Picture] objects. These objects may in turn retain large chunks of texture memory, either directly or indirectly.

The layer's native resources must be retained as long as there is some object that can add it to a scene. Typically, this is either its [Layer.parent] or an undisposed [RenderObject] that will append it to a [ContainerLayer]. Layers automatically hold a handle to their children, and RenderObjects automatically hold a handle to their [RenderObject.layer] as well as any [PictureLayer]s that they paint into using the [PaintingContext.canvas]. A layer automatically releases its resources once at least one handle has been acquired and all handles have been disposed. [RenderObject]s that create additional layer objects must manually manage the handles for that layer similarly to the implementation of [RenderObject.layer].

A handle is automatically managed for [RenderObject.layer].

If a [RenderObject] creates layers in addition to its [RenderObject.layer] and it intends to reuse those layers separately from [RenderObject.layer], it must create a handle to that layer and dispose of it when the layer is no longer needed. For example, if it re-creates or nulls out an existing layer in [RenderObject.paint], it should dispose of the handle to the old layer. It should also dispose of any layer handles it holds in [RenderObject.dispose].

To dispose of a layer handle, set its [layer] property to null.

### LayerHandle()

```dart
LayerHandle([T? _layer])
```

Create a new layer handle, optionally referencing a [Layer].

### layer

```dart
T? get layer
```

The [Layer] whose resources this object keeps alive.

Setting a new value or null will dispose the previously held layer if there are no other open handles to that layer.

### layer

```dart
set layer(T? layer)
```

### toString()

```dart
String toString()
```

# PictureLayer

```dart
class PictureLayer extends Layer {}
```

A composited layer containing a [ui.Picture].

Picture layers are always leaves in the layer tree. They are also responsible for disposing of the [ui.Picture] object they hold. This is typically done when their parent and all [RenderObject]s that participated in painting the picture have been disposed.

### PictureLayer()

```dart
PictureLayer(Rect canvasBounds)
```

Creates a leaf layer for the layer tree.

### canvasBounds

```dart
Rect canvasBounds
```

The bounds that were used for the canvas that drew this layer's [picture].

This is purely advisory. It is included in the information dumped with [debugDumpLayerTree] (which can be triggered by pressing "L" when using "flutter run" at the console), which can help debug why certain drawing commands are being culled.

### picture

```dart
ui.Picture? get picture
```

The picture recorded for this layer.

The picture's coordinate system matches this layer's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### picture

```dart
set picture(ui.Picture? picture)
```

### isComplexHint

```dart
bool get isComplexHint
```

Hints that the painting in this layer is complex and would benefit from caching.

If this hint is not set, the compositor will apply its own heuristics to decide whether the this layer is complex enough to benefit from caching.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### isComplexHint

```dart
set isComplexHint(bool value)
```

### willChangeHint

```dart
bool get willChangeHint
```

Hints that the painting in this layer is likely to change next frame.

This hint tells the compositor not to cache this layer because the cache will not be used in the future. If this hint is not set, the compositor will apply its own heuristics to decide whether this layer is likely to be reused in the future.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### willChangeHint

```dart
set willChangeHint(bool value)
```

### dispose()

```dart
void dispose()
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

# TextureLayer

```dart
class TextureLayer extends Layer {}
```

A composited layer that maps a backend texture to a rectangle.

Backend textures are images that can be applied (mapped) to an area of the Flutter view. They are created, managed, and updated using a platform-specific texture registry. This is typically done by a plugin that integrates with host platform video player, camera, or OpenGL APIs, or similar image sources.

A texture layer refers to its backend texture using an integer ID. Texture IDs are obtained from the texture registry and are scoped to the Flutter view. Texture IDs may be reused after deregistration, at the discretion of the registry. The use of texture IDs currently unknown to the registry will silently result in a blank rectangle.

Once inserted into the layer tree, texture layers are repainted autonomously as dictated by the backend (e.g. on arrival of a video frame). Such repainting generally does not involve executing Dart code.

Texture layers are always leaves in the layer tree.

See also:

- [TextureRegistry](/javadoc/io/flutter/view/TextureRegistry.html) for how to create and manage backend textures on Android.
- [TextureRegistry Protocol](/ios-embedder/protocol_flutter_texture_registry-p.html) for how to create and manage backend textures on iOS.

### TextureLayer()

```dart
TextureLayer({required Rect rect, required int textureId, bool freeze = false, ui.FilterQuality filterQuality = ui.FilterQuality.low})
```

Creates a texture layer bounded by [rect] and with backend texture identified by [textureId], if [freeze] is true new texture frames will not be populated to the texture, and use [filterQuality] to set layer's [FilterQuality].

### rect

```dart
Rect rect
```

Bounding rectangle of this layer.

### textureId

```dart
int textureId
```

The identity of the backend texture.

### freeze

```dart
bool freeze
```

When true the texture will not be updated with new frames.

This is used for resizing embedded Android views: when resizing there is a short period during which the framework cannot tell if the newest texture frame has the previous or new size; to work around this, the framework "freezes" the texture just before resizing the Android view and un-freezes it when it is certain that a frame with the new size is ready.

### filterQuality

```dart
ui.FilterQuality filterQuality
```

{@macro flutter.widgets.Texture.filterQuality}

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

# PlatformViewLayer

```dart
class PlatformViewLayer extends Layer {}
```

A layer that shows an embedded [UIView](https://developer.apple.com/documentation/uikit/uiview) on iOS.

### PlatformViewLayer()

```dart
PlatformViewLayer({required Rect rect, required int viewId})
```

Creates a platform view layer.

### rect

```dart
Rect rect
```

Bounding rectangle of this layer in the global coordinate space.

### viewId

```dart
int viewId
```

The unique identifier of the UIView displayed on this layer.

A UIView with this identifier must have been created by [PlatformViewsService.initUiKitView].

### supportsRasterization()

```dart
bool supportsRasterization()
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

# PerformanceOverlayLayer

```dart
class PerformanceOverlayLayer extends Layer {}
```

A layer that indicates to the compositor that it should display certain performance statistics within it.

Performance overlay layers are always leaves in the layer tree.

### PerformanceOverlayLayer()

```dart
PerformanceOverlayLayer({required Rect overlayRect, required int optionsMask})
```

Creates a layer that displays a performance overlay.

### overlayRect

```dart
Rect get overlayRect
```

The rectangle in this layer's coordinate system that the overlay should occupy.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### overlayRect

```dart
set overlayRect(Rect value)
```

### optionsMask

```dart
int optionsMask
```

The mask is created by shifting 1 by the index of the specific [PerformanceOverlayOption] to enable.

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

# CompositionCallback

```dart
typedef CompositionCallback = void Function(Layer layer)
```

The signature of the callback added in [Layer.addCompositionCallback].

# ContainerLayer

```dart
class ContainerLayer extends Layer {}
```

A composited layer that has a list of children.

A [ContainerLayer] instance merely takes a list of children and inserts them into the composited rendering in order. There are subclasses of [ContainerLayer] which apply more elaborate effects in the process.

### firstChild

```dart
Layer? get firstChild
```

The first composited layer in this layer's child list.

### lastChild

```dart
Layer? get lastChild
```

The last composited layer in this layer's child list.

### hasChildren

```dart
bool get hasChildren
```

Returns whether this layer has at least one child layer.

### supportsRasterization()

```dart
bool supportsRasterization()
```

### buildScene()

```dart
ui.Scene buildScene(ui.SceneBuilder builder)
```

Consider this layer as the root and build a scene (a tree of layers) in the engine.

### dispose()

```dart
void dispose()
```

### updateSubtreeNeedsAddToScene()

```dart
void updateSubtreeNeedsAddToScene()
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### attach()

```dart
void attach(Object owner)
```

### detach()

```dart
void detach()
```

### append()

```dart
void append(Layer child)
```

Adds the given layer to the end of this layer's child list.

### redepthChildren()

```dart
void redepthChildren()
```

### redepthChild()

```dart
void redepthChild(Layer child)
```

Adjust the [depth] of the given [child] to be greater than this node's own [depth].

Only call this method from overrides of [redepthChildren].

### removeAllChildren()

```dart
void removeAllChildren()
```

Removes all of this layer's children from its child list.

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### addChildrenToScene()

```dart
void addChildrenToScene(ui.SceneBuilder builder)
```

Uploads all of this layer's children to the engine.

This method is typically used by [addToScene] to insert the children into the scene. Subclasses of [ContainerLayer] typically override [addToScene] to apply effects to the scene using the [ui.SceneBuilder] API, then insert their children using [addChildrenToScene], then reverse the aforementioned effects before returning from [addToScene].

### applyTransform()

```dart
void applyTransform(Layer? child, Matrix4 transform)
```

Applies the transform that would be applied when compositing the given child to the given matrix.

Specifically, this should apply the transform that is applied to child's _origin_. When using [applyTransform] with a chain of layers, results will be unreliable unless the deepest layer in the chain collapses the `layerOffset` in [addToScene] to zero, meaning that it passes [Offset.zero] to its children, and bakes any incoming `layerOffset` into the [ui.SceneBuilder] as (for instance) a transform (which is then also included in the transformation applied by [applyTransform]).

For example, if [addToScene] applies the `layerOffset` and then passes [Offset.zero] to the children, then it should be included in the transform applied here, whereas if [addToScene] just passes the `layerOffset` to the child, then it should not be included in the transform applied here.

This method is only valid immediately after [addToScene] has been called, before any of the properties have been changed.

The default implementation does nothing, since [ContainerLayer], by default, composites its children at the origin of the [ContainerLayer] itself.

The `child` argument should generally not be null, since in principle a layer could transform each child independently. However, certain layers may explicitly allow null as a value, for example if they know that they transform all their children identically.

Used by [FollowerLayer] to transform its child to a [LeaderLayer]'s position.

### depthFirstIterateChildren()

```dart
List<Layer> depthFirstIterateChildren()
```

Returns the descendants of this layer in depth first order.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# OffsetLayer

```dart
class OffsetLayer extends ContainerLayer {}
```

A layer that is displayed at an offset from its parent layer.

Offset layers are key to efficient repainting because they are created by repaint boundaries in the [RenderObject] tree (see [RenderObject.isRepaintBoundary]). When a render object that is a repaint boundary is asked to paint at given offset in a [PaintingContext], the render object first checks whether it needs to repaint itself. If not, it reuses its existing [OffsetLayer] (and its entire subtree) by mutating its [offset] property, cutting off the paint walk.

### OffsetLayer()

```dart
OffsetLayer({Offset offset = Offset.zero})
```

Creates an offset layer.

By default, [offset] is zero. It must be non-null before the compositing phase of the pipeline.

### offset

```dart
Offset get offset
```

Offset from parent in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

The [offset] property must be non-null before the compositing phase of the pipeline.

### offset

```dart
set offset(Offset value)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### applyTransform()

```dart
void applyTransform(Layer? child, Matrix4 transform)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### toImage()

```dart
Future<ui.Image> toImage(Rect bounds, {double pixelRatio = 1.0})
```

Capture an image of the current state of this layer and its children.

The returned [ui.Image] has uncompressed raw RGBA bytes, will be offset by the top-left corner of [bounds], and have dimensions equal to the size of [bounds] multiplied by [pixelRatio].

The [pixelRatio] describes the scale between the logical pixels and the size of the output image. It is independent of the [dart:ui.FlutterView.devicePixelRatio] for the device, so specifying 1.0 (the default) will give you a 1:1 mapping between logical pixels and the output pixels in the image.

This API functions like [toImageSync], except that it only returns after rasterization is complete.

See also:

- [RenderRepaintBoundary.toImage] for a similar API at the render object level.
- [dart:ui.Scene.toImage] for more information about the image returned.

### toImageSync()

```dart
ui.Image toImageSync(Rect bounds, {double pixelRatio = 1.0})
```

Capture an image of the current state of this layer and its children.

The returned [ui.Image] has uncompressed raw RGBA bytes, will be offset by the top-left corner of [bounds], and have dimensions equal to the size of [bounds] multiplied by [pixelRatio].

The [pixelRatio] describes the scale between the logical pixels and the size of the output image. It is independent of the [dart:ui.FlutterView.devicePixelRatio] for the device, so specifying 1.0 (the default) will give you a 1:1 mapping between logical pixels and the output pixels in the image.

This API functions like [toImage], except that rasterization begins eagerly on the raster thread and the image is returned before this is completed.

See also:

- [RenderRepaintBoundary.toImage] for a similar API at the render object level.
- [dart:ui.Scene.toImage] for more information about the image returned.

# ClipRectLayer

```dart
class ClipRectLayer extends ContainerLayer {}
```

A composite layer that clips its children using a rectangle.

When debugging, setting [debugDisableClipLayers] to true will cause this layer to be skipped (directly replaced by its children). This can be helpful to track down the cause of performance problems.

### ClipRectLayer()

```dart
ClipRectLayer({Rect? clipRect, Clip clipBehavior = Clip.hardEdge})
```

Creates a layer with a rectangular clip.

The [clipRect] argument must not be null before the compositing phase of the pipeline.

The [clipBehavior] argument must not be [Clip.none].

### clipRect

```dart
Rect? get clipRect
```

The rectangle to clip in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### clipRect

```dart
set clipRect(Rect? value)
```

### describeClipBounds()

```dart
Rect? describeClipBounds()
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@template flutter.rendering.ClipRectLayer.clipBehavior} Controls how to clip.

Must not be set to null or [Clip.none]. {@endtemplate}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipRRectLayer

```dart
class ClipRRectLayer extends ContainerLayer {}
```

A composite layer that clips its children using a rounded rectangle.

When debugging, setting [debugDisableClipLayers] to true will cause this layer to be skipped (directly replaced by its children). This can be helpful to track down the cause of performance problems.

### ClipRRectLayer()

```dart
ClipRRectLayer({RRect? clipRRect, Clip clipBehavior = Clip.antiAlias})
```

Creates a layer with a rounded-rectangular clip.

The [clipRRect] and [clipBehavior] properties must be non-null before the compositing phase of the pipeline.

### clipRRect

```dart
RRect? get clipRRect
```

The rounded-rect to clip in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### clipRRect

```dart
set clipRRect(RRect? value)
```

### describeClipBounds()

```dart
Rect? describeClipBounds()
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

Defaults to [Clip.antiAlias].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipRSuperellipseLayer

```dart
class ClipRSuperellipseLayer extends ContainerLayer {}
```

A composite layer that clips its children using a rounded superellipse.

When debugging, setting [debugDisableClipLayers] to true will cause this layer to be skipped (directly replaced by its children). This can be helpful to track down the cause of performance problems.

Hit tests are performed based on the bounding box of the rounded superellipse.

### ClipRSuperellipseLayer()

```dart
ClipRSuperellipseLayer({RSuperellipse? clipRSuperellipse, Clip clipBehavior = Clip.antiAlias})
```

Creates a layer with a rounded-rectangular clip.

The [clipRSuperellipse] and [clipBehavior] properties must be non-null before the compositing phase of the pipeline.

### clipRSuperellipse

```dart
RSuperellipse? get clipRSuperellipse
```

The rounded-rect to clip in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### clipRSuperellipse

```dart
set clipRSuperellipse(RSuperellipse? value)
```

### describeClipBounds()

```dart
Rect? describeClipBounds()
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

Defaults to [Clip.antiAlias].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ClipPathLayer

```dart
class ClipPathLayer extends ContainerLayer {}
```

A composite layer that clips its children using a path.

When debugging, setting [debugDisableClipLayers] to true will cause this layer to be skipped (directly replaced by its children). This can be helpful to track down the cause of performance problems.

### ClipPathLayer()

```dart
ClipPathLayer({Path? clipPath, Clip clipBehavior = Clip.antiAlias})
```

Creates a layer with a path-based clip.

The [clipPath] and [clipBehavior] properties must be non-null before the compositing phase of the pipeline.

### clipPath

```dart
Path? get clipPath
```

The path to clip in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### clipPath

```dart
set clipPath(Path? value)
```

### describeClipBounds()

```dart
Rect? describeClipBounds()
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.rendering.ClipRectLayer.clipBehavior}

Defaults to [Clip.antiAlias].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ColorFilterLayer

```dart
class ColorFilterLayer extends ContainerLayer {}
```

A composite layer that applies a [ColorFilter] to its children.

### ColorFilterLayer()

```dart
ColorFilterLayer({ColorFilter? colorFilter})
```

Creates a layer that applies a [ColorFilter] to its children.

The [colorFilter] property must be non-null before the compositing phase of the pipeline.

### colorFilter

```dart
ColorFilter? get colorFilter
```

The color filter to apply to children.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### colorFilter

```dart
set colorFilter(ColorFilter? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ImageFilterLayer

```dart
class ImageFilterLayer extends OffsetLayer {}
```

A composite layer that applies an [ui.ImageFilter] to its children.

### ImageFilterLayer()

```dart
ImageFilterLayer({ui.ImageFilter? imageFilter, dynamic offset})
```

Creates a layer that applies an [ui.ImageFilter] to its children.

The [imageFilter] property must be non-null before the compositing phase of the pipeline.

### imageFilter

```dart
ui.ImageFilter? get imageFilter
```

The image filter to apply to children.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### imageFilter

```dart
set imageFilter(ui.ImageFilter? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TransformLayer

```dart
class TransformLayer extends OffsetLayer {}
```

A composited layer that applies a given transformation matrix to its children.

This class inherits from [OffsetLayer] to make it one of the layers that can be used at the root of a [RenderObject] hierarchy.

### TransformLayer()

```dart
TransformLayer({Matrix4? transform, dynamic offset})
```

Creates a transform layer.

The [transform] and [offset] properties must be non-null before the compositing phase of the pipeline.

### transform

```dart
Matrix4? get transform
```

The matrix to apply.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

This transform is applied before [offset], if both are set.

The [transform] property must be non-null before the compositing phase of the pipeline.

### transform

```dart
set transform(Matrix4? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### applyTransform()

```dart
void applyTransform(Layer? child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# OpacityLayer

```dart
class OpacityLayer extends OffsetLayer {}
```

A composited layer that makes its children partially transparent.

When debugging, setting [debugDisableOpacityLayers] to true will cause this layer to be skipped (directly replaced by its children). This can be helpful to track down the cause of performance problems.

Try to avoid an [OpacityLayer] with no children. Remove that layer if possible to save some tree walks.

### OpacityLayer()

```dart
OpacityLayer({int? alpha, dynamic offset})
```

Creates an opacity layer.

The [alpha] property must be non-null before the compositing phase of the pipeline.

### alpha

```dart
int? get alpha
```

The amount to multiply into the alpha channel.

The opacity is expressed as an integer from 0 to 255, where 0 is fully transparent and 255 is fully opaque.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### alpha

```dart
set alpha(int? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ShaderMaskLayer

```dart
class ShaderMaskLayer extends ContainerLayer {}
```

A composited layer that applies a shader to its children.

The shader is only applied inside the given [maskRect]. The shader itself uses the top left of the [maskRect] as its origin.

The [maskRect] does not affect the positions of any child layers.

### ShaderMaskLayer()

```dart
ShaderMaskLayer({Shader? shader, Rect? maskRect, BlendMode? blendMode})
```

Creates a shader mask layer.

The [shader], [maskRect], and [blendMode] properties must be non-null before the compositing phase of the pipeline.

### shader

```dart
Shader? get shader
```

The shader to apply to the children.

The origin of the shader (e.g. of the coordinate system used by the `from` and `to` arguments to [ui.Gradient.linear]) is at the top left of the [maskRect].

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

See also:

- [ui.Gradient] and [ui.ImageShader], two shader types that can be used.

### shader

```dart
set shader(Shader? value)
```

### maskRect

```dart
Rect? get maskRect
```

The position and size of the shader.

The [shader] is only rendered inside this rectangle, using the top left of the rectangle as its origin.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### maskRect

```dart
set maskRect(Rect? value)
```

### blendMode

```dart
BlendMode? get blendMode
```

The blend mode to apply when blending the shader with the children.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### blendMode

```dart
set blendMode(BlendMode? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# BackdropKey

```dart
final class BackdropKey {}
```

A backdrop key uniquely identifies the backdrop that a [BackdropFilterLayer] samples from.

When multiple backdrop filters share the same key, the Flutter engine can more efficiently perform the backdrop operations.

Instead of using a backdrop key directly, consider using a [BackdropGroup] and the [BackdropFilter.grouped] constructor. The framework will automatically group child backdrop filters that use the `.grouped` constructor when they are placed as children of a [BackdropGroup].

For more information, see [BackdropFilter].

### BackdropKey()

```dart
BackdropKey()
```

Create a new [BackdropKey].

# BackdropFilterLayer

```dart
class BackdropFilterLayer extends ContainerLayer {}
```

A composited layer that applies a filter to the existing contents of the scene.

### BackdropFilterLayer()

```dart
BackdropFilterLayer({ui.ImageFilter? filter, BlendMode blendMode = BlendMode.srcOver})
```

Creates a backdrop filter layer.

The [filter] property must be non-null before the compositing phase of the pipeline.

The [blendMode] property defaults to [BlendMode.srcOver].

### filter

```dart
ui.ImageFilter? get filter
```

The filter to apply to the existing contents of the scene.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### filter

```dart
set filter(ui.ImageFilter? value)
```

### blendMode

```dart
BlendMode get blendMode
```

The blend mode to use to apply the filtered background content onto the background surface.

The default value of this property is [BlendMode.srcOver]. {@macro flutter.widgets.BackdropFilter.blendMode}

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### blendMode

```dart
set blendMode(BlendMode value)
```

### backdropKey

```dart
BackdropKey? get backdropKey
```

The backdrop key that identifies the [BackdropGroup] this filter will apply to.

The default value for the backdrop key is `null`, meaning that it's not part of a [BackdropGroup].

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

### backdropKey

```dart
set backdropKey(BackdropKey? value)
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# LayerLink

```dart
class LayerLink {}
```

An object that a [LeaderLayer] can register with.

An instance of this class should be provided as the [LeaderLayer.link] and the [FollowerLayer.link] properties to cause the [FollowerLayer] to follow the [LeaderLayer].

See also:

- [CompositedTransformTarget], the widget that creates a [LeaderLayer].
- [CompositedTransformFollower], the widget that creates a [FollowerLayer].
- [RenderLeaderLayer] and [RenderFollowerLayer], the corresponding render objects.

### leader

```dart
LeaderLayer? get leader
```

The [LeaderLayer] connected to this link.

### leaderSize

```dart
Size? leaderSize
```

The total size of the content of the connected [LeaderLayer].

Generally this should be set by the [RenderObject] that paints on the registered [LeaderLayer] (for instance a [RenderLeaderLayer] that shares this link with its followers). This size may be outdated before and during layout.

### toString()

```dart
String toString({DiagnosticLevel minLevel = DiagnosticLevel.info})
```

# LeaderLayer

```dart
class LeaderLayer extends ContainerLayer {}
```

A composited layer that can be followed by a [FollowerLayer].

This layer collapses the accumulated offset into a transform and passes [Offset.zero] to its child layers in the [addToScene]/[addChildrenToScene] methods, so that [applyTransform] will work reliably.

### LeaderLayer()

```dart
LeaderLayer({required LayerLink link, Offset offset = Offset.zero})
```

Creates a leader layer.

The [link] property must not have been provided to any other [LeaderLayer] layers that are [attached] to the layer tree at the same time.

The [offset] property must be non-null before the compositing phase of the pipeline.

### link

```dart
LayerLink get link
```

The object with which this layer should register.

The link will be established when this layer is [attach]ed, and will be cleared when this layer is [detach]ed.

### link

```dart
set link(LayerLink value)
```

### offset

```dart
Offset get offset
```

Offset from parent in the parent's coordinate system.

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

The [offset] property must be non-null before the compositing phase of the pipeline.

### offset

```dart
set offset(Offset value)
```

### attach()

```dart
void attach(Object owner)
```

### detach()

```dart
void detach()
```

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### applyTransform()

```dart
void applyTransform(Layer? child, Matrix4 transform)
```

Applies the transform that would be applied when compositing the given child to the given matrix.

See [ContainerLayer.applyTransform] for details.

The `child` argument may be null, as the same transform is applied to all children.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# FollowerLayer

```dart
class FollowerLayer extends ContainerLayer {}
```

A composited layer that applies a transformation matrix to its children such that they are positioned to match a [LeaderLayer].

If any of the ancestors of this layer have a degenerate matrix (e.g. scaling by zero), then the [FollowerLayer] will not be able to transform its child to the coordinate space of the [LeaderLayer].

A [linkedOffset] property can be provided to further offset the child layer from the leader layer, for example if the child is to follow the linked layer at a distance rather than directly overlapping it.

### FollowerLayer()

```dart
FollowerLayer({required LayerLink link, bool? showWhenUnlinked = true, Offset? unlinkedOffset = Offset.zero, Offset? linkedOffset = Offset.zero})
```

Creates a follower layer.

The [unlinkedOffset], [linkedOffset], and [showWhenUnlinked] properties must be non-null before the compositing phase of the pipeline.

### link

```dart
LayerLink link
```

The link to the [LeaderLayer].

The same object should be provided to a [LeaderLayer] that is earlier in the layer tree. When this layer is composited, it will apply a transform that moves its children to match the position of the [LeaderLayer].

### showWhenUnlinked

```dart
bool? showWhenUnlinked
```

Whether to show the layer's contents when the [link] does not point to a [LeaderLayer].

When the layer is linked, children layers are positioned such that they have the same global position as the linked [LeaderLayer].

When the layer is not linked, then: if [showWhenUnlinked] is true, children are positioned as if the [FollowerLayer] was a [ContainerLayer]; if it is false, then children are hidden.

The [showWhenUnlinked] property must be non-null before the compositing phase of the pipeline.

### unlinkedOffset

```dart
Offset? unlinkedOffset
```

Offset from parent in the parent's coordinate system, used when the layer is not linked to a [LeaderLayer].

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

The [unlinkedOffset] property must be non-null before the compositing phase of the pipeline.

See also:

- [linkedOffset], for when the layers are linked.

### linkedOffset

```dart
Offset? linkedOffset
```

Offset from the origin of the leader layer to the origin of the child layers, used when the layer is linked to a [LeaderLayer].

The scene must be explicitly recomposited after this property is changed (as described at [Layer]).

The [linkedOffset] property must be non-null before the compositing phase of the pipeline.

See also:

- [unlinkedOffset], for when the layer is not linked.

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

### getLastTransform()

```dart
Matrix4? getLastTransform()
```

The transform that was used during the last composition phase.

If the [link] was not linked to a [LeaderLayer], or if this layer has a degenerate matrix applied, then this will be null.

This method returns a new [Matrix4] instance each time it is invoked.

### alwaysNeedsAddToScene

```dart
bool get alwaysNeedsAddToScene
```

{@template flutter.rendering.FollowerLayer.alwaysNeedsAddToScene} This disables retained rendering.

A [FollowerLayer] copies changes from a [LeaderLayer] that could be anywhere in the Layer tree, and that leader layer could change without notifying the follower layer. Therefore we have to always call a follower layer's [addToScene]. In order to call follower layer's [addToScene], leader layer's [addToScene] must be called first so leader layer must also be considered as [alwaysNeedsAddToScene]. {@endtemplate}

### addToScene()

```dart
void addToScene(ui.SceneBuilder builder)
```

### applyTransform()

```dart
void applyTransform(Layer? child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnnotatedRegionLayer

```dart
class AnnotatedRegionLayer<T extends Object> extends ContainerLayer {}
```

A composited layer which annotates its children with a value. Pushing this layer to the tree is the common way of adding an annotation.

An annotation is an optional object of any type that, when attached with a layer, can be retrieved using [Layer.find] or [Layer.findAllAnnotations] with a position. The search process is done recursively, controlled by a concept of being opaque to a type of annotation, explained in the document of [Layer.findAnnotations].

When an annotation search arrives, this layer defers the same search to each of this layer's children, respecting their opacity. Then it adds this layer's annotation if all of the following restrictions are met:

{@template flutter.rendering.AnnotatedRegionLayer.restrictions}

- The target type must be identical to the annotated type `T`.
- If [size] is provided, the target position must be contained within the rectangle formed by [size] and [offset]. {@endtemplate}

This layer is opaque to a type of annotation if any child is also opaque, or if [opaque] is true and the layer's annotation is added.

### AnnotatedRegionLayer()

```dart
AnnotatedRegionLayer(T value, {Size? size, Offset? offset, bool opaque = false})
```

Creates a new layer that annotates its children with [value].

### value

```dart
T value
```

The annotated object, which is added to the result if all restrictions are met.

### size

```dart
Size? size
```

The size of the annotated object.

If [size] is provided, then the annotation is found only if the target position is contained by the rectangle formed by [size] and [offset]. Otherwise no such restriction is applied, and clipping can only be done by the ancestor layers.

### offset

```dart
Offset offset
```

The position of the annotated object.

The [offset] defaults to [Offset.zero] if not provided, and is ignored if [size] is not set.

The [offset] only offsets the clipping rectangle, and does not affect how the painting or annotation search is propagated to its children.

### opaque

```dart
bool opaque
```

Whether the annotation of this layer should be opaque during an annotation search of type `T`, preventing siblings visually behind it from being searched.

If [opaque] is true, and this layer does add its annotation [value], then the layer will always be opaque during the search.

If [opaque] is false, or if this layer does not add its annotation, then the opacity of this layer will be the one returned by the children, meaning that it will be opaque if any child is opaque.

The [opaque] defaults to false.

The [opaque] is effectively useless during [Layer.find] (more specifically, [Layer.findAnnotations] with `onlyFirst: true`), since the search process then skips the remaining tree after finding the first annotation.

See also:

- [Layer.findAnnotations], which explains the concept of being opaque to a type of annotation as the return value.
- [HitTestBehavior], which controls similar logic when hit-testing in the render tree.

### findAnnotations()

```dart
bool findAnnotations<S extends Object>(AnnotationResult<S> result, Offset localPosition, {required bool onlyFirst})
```

Searches the subtree for annotations of type `S` at the location `localPosition`, then adds the annotation [value] if applicable.

This method always searches its children, and if any child returns `true`, the remaining children are skipped. Regardless of what the children return, this method then adds this layer's annotation if all of the following restrictions are met:

{@macro flutter.rendering.AnnotatedRegionLayer.restrictions}

This search process respects `onlyFirst`, meaning that when `onlyFirst` is true, the search will stop when it finds the first annotation from the children, and the layer's own annotation is checked only when none is given by the children.

The return value is true if any child returns `true`, or if [opaque] is true and the layer's annotation is added.

For explanation of layer annotations, parameters and return value, refer to [Layer.findAnnotations].

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
