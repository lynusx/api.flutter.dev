@docImport 'package:flutter/widgets.dart';

@docImport 'proxy_sliver.dart'; @docImport 'sliver.dart';

# RenderProxyBox

```dart
class RenderProxyBox extends RenderBox with RenderObjectWithChildMixin<RenderBox>, RenderProxyBoxMixin<RenderBox> {}
```

A base class for render boxes that resemble their children.

A proxy box has a single child and mimics all the properties of that child by calling through to the child for each function in the render box protocol. For example, a proxy box determines its size by asking its child to layout with the same constraints and then matching the size.

A proxy box isn't useful on its own because you might as well just replace the proxy box with its child. However, RenderProxyBox is a useful base class for render objects that wish to mimic most, but not all, of the properties of their child.

See also:

- [RenderProxySliver], a base class for render slivers that resemble their children.

### RenderProxyBox()

```dart
RenderProxyBox([RenderBox? child])
```

Creates a proxy render box.

Proxy render boxes are rarely created directly because they proxy the render box protocol to [child]. Instead, consider using one of the subclasses.

# RenderProxyBoxMixin

```dart
mixin RenderProxyBoxMixin<T extends RenderBox> on RenderBox, RenderObjectWithChildMixin<T> {}
```

Implementation of [RenderProxyBox].

Use this mixin in situations where the proxying behavior of [RenderProxyBox] is desired but inheriting from [RenderProxyBox] is impractical (e.g. because you want to inherit from a different class).

If a class already inherits from [RenderProxyBox] and also uses this mixin, you can safely delete the use of the mixin.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### computeSizeForNoChild()

```dart
Size computeSizeForNoChild(BoxConstraints constraints)
```

Calculate the size the [RenderProxyBox] would have under the given [BoxConstraints] for the case where it does not have a child.

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

# HitTestBehavior

```dart
enum HitTestBehavior {}
```

How to behave during hit tests.

Targets that defer to their children receive events within their bounds only if one of their children is hit by the hit test.

Opaque targets can be hit by hit tests, causing them to both receive events within their bounds and prevent targets visually behind them from also receiving events.

Translucent targets both receive events within their bounds and permit targets visually behind them to also receive events.

# RenderProxyBoxWithHitTestBehavior

```dart
abstract class RenderProxyBoxWithHitTestBehavior extends RenderProxyBox {}
```

A RenderProxyBox subclass that allows you to customize the hit-testing behavior.

### RenderProxyBoxWithHitTestBehavior()

```dart
RenderProxyBoxWithHitTestBehavior({HitTestBehavior behavior = HitTestBehavior.deferToChild, RenderBox? child})
```

Initializes member variables for subclasses.

By default, the [behavior] is [HitTestBehavior.deferToChild].

### behavior

```dart
HitTestBehavior behavior
```

How to behave during hit testing when deciding how the hit test propagates to children and whether to consider targets behind this one.

Defaults to [HitTestBehavior.deferToChild].

See [HitTestBehavior] for the allowed values and their meanings.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderConstrainedBox

```dart
class RenderConstrainedBox extends RenderProxyBox {}
```

Imposes additional constraints on its child.

A render constrained box proxies most functions in the render box protocol to its child, except that when laying out its child, it tightens the constraints provided by its parent by enforcing the [additionalConstraints] as well.

For example, if you wanted [child] to have a minimum height of 50.0 logical pixels, you could use `const BoxConstraints(minHeight: 50.0)` as the [additionalConstraints].

### RenderConstrainedBox()

```dart
RenderConstrainedBox({RenderBox? child, required BoxConstraints additionalConstraints})
```

Creates a render box that constrains its child.

The [additionalConstraints] argument must be valid.

### additionalConstraints

```dart
BoxConstraints get additionalConstraints
```

Additional constraints to apply to [child] during layout.

### additionalConstraints

```dart
set additionalConstraints(BoxConstraints value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderLimitedBox

```dart
class RenderLimitedBox extends RenderProxyBox {}
```

Constrains the child's [BoxConstraints.maxWidth] and [BoxConstraints.maxHeight] if they're otherwise unconstrained.

This has the effect of giving the child a natural dimension in unbounded environments. For example, by providing a [maxHeight] to a widget that normally tries to be as big as possible, the widget will normally size itself to fit its parent, but when placed in a vertical list, it will take on the given height.

This is useful when composing widgets that normally try to match their parents' size, so that they behave reasonably in lists (which are unbounded).

### RenderLimitedBox()

```dart
RenderLimitedBox({RenderBox? child, double maxWidth = double.infinity, double maxHeight = double.infinity})
```

Creates a render box that imposes a maximum width or maximum height on its child if the child is otherwise unconstrained.

The [maxWidth] and [maxHeight] arguments not be null and must be non-negative.

### maxWidth

```dart
double get maxWidth
```

The value to use for maxWidth if the incoming maxWidth constraint is infinite.

### maxWidth

```dart
set maxWidth(double value)
```

### maxHeight

```dart
double get maxHeight
```

The value to use for maxHeight if the incoming maxHeight constraint is infinite.

### maxHeight

```dart
set maxHeight(double value)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderAspectRatio

```dart
class RenderAspectRatio extends RenderProxyBox {}
```

Attempts to size the child to a specific aspect ratio.

The render object first tries the largest width permitted by the layout constraints. The height of the render object is determined by applying the given aspect ratio to the width, expressed as a ratio of width to height.

For example, a 16:9 width:height aspect ratio would have a value of 16.0/9.0. If the maximum width is infinite, the initial width is determined by applying the aspect ratio to the maximum height.

Now consider a second example, this time with an aspect ratio of 2.0 and layout constraints that require the width to be between 0.0 and 100.0 and the height to be between 0.0 and 100.0. We'll select a width of 100.0 (the biggest allowed) and a height of 50.0 (to match the aspect ratio).

In that same situation, if the aspect ratio is 0.5, we'll also select a width of 100.0 (still the biggest allowed) and we'll attempt to use a height of 200.0. Unfortunately, that violates the constraints because the child can be at most 100.0 pixels tall. The render object will then take that value and apply the aspect ratio again to obtain a width of 50.0. That width is permitted by the constraints and the child receives a width of 50.0 and a height of 100.0. If the width were not permitted, the render object would continue iterating through the constraints. If the render object does not find a feasible size after consulting each constraint, the render object will eventually select a size for the child that meets the layout constraints but fails to meet the aspect ratio constraints.

### RenderAspectRatio()

```dart
RenderAspectRatio({RenderBox? child, required double aspectRatio})
```

Creates as render object with a specific aspect ratio.

The [aspectRatio] argument must be a finite, positive value.

### aspectRatio

```dart
double get aspectRatio
```

The aspect ratio to attempt to use.

The aspect ratio is expressed as a ratio of width to height. For example, a 16:9 width:height aspect ratio would have a value of 16.0/9.0.

### aspectRatio

```dart
set aspectRatio(double value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderIntrinsicWidth

```dart
class RenderIntrinsicWidth extends RenderProxyBox {}
```

Sizes its child to the child's maximum intrinsic width.

This class is useful, for example, when unlimited width is available and you would like a child that would otherwise attempt to expand infinitely to instead size itself to a more reasonable width.

The constraints that this object passes to its child will adhere to the parent's constraints, so if the constraints are not large enough to satisfy the child's maximum intrinsic width, then the child will get less width than it otherwise would. Likewise, if the minimum width constraint is larger than the child's maximum intrinsic width, the child will be given more width than it otherwise would.

If [stepWidth] is non-null, the child's width will be snapped to a multiple of the [stepWidth]. Similarly, if [stepHeight] is non-null, the child's height will be snapped to a multiple of the [stepHeight].

This class is relatively expensive, because it adds a speculative layout pass before the final layout phase. Avoid using it where possible. In the worst case, this render object can result in a layout that is O(N²) in the depth of the tree.

See also:

- [Align], a widget that aligns its child within itself. This can be used to loosen the constraints passed to the [RenderIntrinsicWidth], allowing the [RenderIntrinsicWidth]'s child to be smaller than that of its parent.
- [Row], which when used with [CrossAxisAlignment.stretch] can be used to loosen just the width constraints that are passed to the [RenderIntrinsicWidth], allowing the [RenderIntrinsicWidth]'s child's width to be smaller than that of its parent.

### RenderIntrinsicWidth()

```dart
RenderIntrinsicWidth({double? stepWidth, double? stepHeight, RenderBox? child})
```

Creates a render object that sizes itself to its child's intrinsic width.

If [stepWidth] is non-null it must be > 0.0. Similarly If [stepHeight] is non-null it must be > 0.0.

### stepWidth

```dart
double? get stepWidth
```

If non-null, force the child's width to be a multiple of this value.

This value must be null or > 0.0.

### stepWidth

```dart
set stepWidth(double? value)
```

### stepHeight

```dart
double? get stepHeight
```

If non-null, force the child's height to be a multiple of this value.

This value must be null or > 0.0.

### stepHeight

```dart
set stepHeight(double? value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderIntrinsicHeight

```dart
class RenderIntrinsicHeight extends RenderProxyBox {}
```

Sizes its child to the child's intrinsic height.

This class is useful, for example, when unlimited height is available and you would like a child that would otherwise attempt to expand infinitely to instead size itself to a more reasonable height.

The constraints that this object passes to its child will adhere to the parent's constraints, so if the constraints are not large enough to satisfy the child's maximum intrinsic height, then the child will get less height than it otherwise would. Likewise, if the minimum height constraint is larger than the child's maximum intrinsic height, the child will be given more height than it otherwise would.

This class is relatively expensive, because it adds a speculative layout pass before the final layout phase. Avoid using it where possible. In the worst case, this render object can result in a layout that is O(N²) in the depth of the tree.

See also:

- [Align], a widget that aligns its child within itself. This can be used to loosen the constraints passed to the [RenderIntrinsicHeight], allowing the [RenderIntrinsicHeight]'s child to be smaller than that of its parent.
- [Column], which when used with [CrossAxisAlignment.stretch] can be used to loosen just the height constraints that are passed to the [RenderIntrinsicHeight], allowing the [RenderIntrinsicHeight]'s child's height to be smaller than that of its parent.

### RenderIntrinsicHeight()

```dart
RenderIntrinsicHeight({RenderBox? child})
```

Creates a render object that sizes itself to its child's intrinsic height.

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

# RenderIgnoreBaseline

```dart
class RenderIgnoreBaseline extends RenderProxyBox {}
```

Excludes the child from baseline computations in the parent.

### RenderIgnoreBaseline()

```dart
RenderIgnoreBaseline({RenderBox? child})
```

Create a render object that causes the parent to ignore the child for baseline computations.

### computeDistanceToActualBaseline()

```dart
Null computeDistanceToActualBaseline(TextBaseline baseline)
```

### computeDryBaseline()

```dart
Null computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

# RenderOpacity

```dart
class RenderOpacity extends RenderProxyBox {}
```

Makes its child partially transparent.

This class paints its child into an intermediate buffer and then blends the child back into the scene partially transparent.

For values of opacity other than 0.0 and 1.0, this class is relatively expensive because it requires painting the child into an intermediate buffer. For the value 0.0, the child is not painted at all. For the value 1.0, the child is painted immediately without an intermediate buffer.

### RenderOpacity()

```dart
RenderOpacity({double opacity = 1.0, bool alwaysIncludeSemantics = false, RenderBox? child})
```

Creates a partially transparent render object.

The [opacity] argument must be between 0.0 and 1.0, inclusive.

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### opacity

```dart
double get opacity
```

The fraction to scale the child's alpha value.

An opacity of 1.0 is fully opaque. An opacity of 0.0 is fully transparent (i.e., invisible).

Values 1.0 and 0.0 are painted with a fast path. Other values require painting the child into an intermediate buffer, which is expensive.

### opacity

```dart
set opacity(double value)
```

### alwaysIncludeSemantics

```dart
bool get alwaysIncludeSemantics
```

Whether child semantics are included regardless of the opacity.

If false, semantics are excluded when [opacity] is 0.0.

Defaults to false.

### alwaysIncludeSemantics

```dart
set alwaysIncludeSemantics(bool value)
```

### paintsChild()

```dart
bool paintsChild(RenderBox child)
```

### updateCompositedLayer()

```dart
OffsetLayer updateCompositedLayer({required OpacityLayer? oldLayer})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderAnimatedOpacityMixin

```dart
mixin RenderAnimatedOpacityMixin<T extends RenderObject> on RenderObjectWithChildMixin<T> {}
```

Implementation of [RenderAnimatedOpacity] and [RenderSliverAnimatedOpacity].

This mixin allows the logic of animating opacity to be used with different layout models, e.g. the way that [RenderAnimatedOpacity] uses it for [RenderBox] and [RenderSliverAnimatedOpacity] uses it for [RenderSliver].

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### updateCompositedLayer()

```dart
OffsetLayer updateCompositedLayer({required OpacityLayer? oldLayer})
```

### opacity

```dart
Animation<double> get opacity
```

The animation that drives this render object's opacity.

An opacity of 1.0 is fully opaque. An opacity of 0.0 is fully transparent (i.e., invisible).

To change the opacity of a child in a static manner, not animated, consider [RenderOpacity] instead.

This getter cannot be read until the value has been set. It should be set by the constructor of the class in which this mixin is included.

### opacity

```dart
set opacity(Animation<double> value)
```

### alwaysIncludeSemantics

```dart
bool get alwaysIncludeSemantics
```

Whether child semantics are included regardless of the opacity.

If false, semantics are excluded when [opacity] is 0.0.

Defaults to false.

This getter cannot be read until the value has been set. It should be set by the constructor of the class in which this mixin is included.

### alwaysIncludeSemantics

```dart
set alwaysIncludeSemantics(bool value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### paintsChild()

```dart
bool paintsChild(RenderObject child)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderAnimatedOpacity

```dart
class RenderAnimatedOpacity extends RenderProxyBox with RenderAnimatedOpacityMixin<RenderBox> {}
```

Makes its child partially transparent, driven from an [Animation].

This is a variant of [RenderOpacity] that uses an [Animation<double>] rather than a [double] to control the opacity.

### RenderAnimatedOpacity()

```dart
RenderAnimatedOpacity({required Animation<double> opacity, bool alwaysIncludeSemantics = false, RenderBox? child})
```

Creates a partially transparent render object.

# ShaderCallback

```dart
typedef ShaderCallback = Shader Function(Rect bounds)
```

Signature for a function that creates a [Shader] for a given [Rect].

Used by [RenderShaderMask] and the [ShaderMask] widget.

# RenderShaderMask

```dart
class RenderShaderMask extends RenderProxyBox {}
```

Applies a mask generated by a [Shader] to its child.

For example, [RenderShaderMask] can be used to gradually fade out the edge of a child by using a [ui.Gradient.linear] mask.

### RenderShaderMask()

```dart
RenderShaderMask({RenderBox? child, required ShaderCallback shaderCallback, BlendMode blendMode = BlendMode.modulate})
```

Creates a render object that applies a mask generated by a [Shader] to its child.

### layer

```dart
ShaderMaskLayer? get layer
```

### shaderCallback

```dart
ShaderCallback get shaderCallback
```

Called to creates the [Shader] that generates the mask.

The shader callback is called with the current size of the child so that it can customize the shader to the size and location of the child.

The rectangle will always be at the origin when called by [RenderShaderMask].

### shaderCallback

```dart
set shaderCallback(ShaderCallback value)
```

### blendMode

```dart
BlendMode get blendMode
```

The [BlendMode] to use when applying the shader to the child.

The default, [BlendMode.modulate], is useful for applying an alpha blend to the child. Other blend modes can be used to create other effects.

### blendMode

```dart
set blendMode(BlendMode value)
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

# RenderBackdropFilter

```dart
class RenderBackdropFilter extends RenderProxyBox {}
```

Applies a filter to the existing painted content and then paints [child].

This effect is relatively expensive, especially if the filter is non-local, such as a blur.

### RenderBackdropFilter()

```dart
RenderBackdropFilter({RenderBox? child, ui.ImageFilter? filter, ImageFilterConfig? filterConfig, BlendMode blendMode = BlendMode.srcOver, bool enabled = true, BackdropKey? backdropKey})
```

Creates a backdrop filter.

Exactly one of [filter] or [filterConfig] must be provided. Providing both or neither will result in an assertion error.

The [blendMode] argument defaults to [BlendMode.srcOver].

### layer

```dart
BackdropFilterLayer? get layer
```

### enabled

```dart
bool get enabled
```

Whether or not the backdrop filter operation will be applied to the child.

### enabled

```dart
set enabled(bool value)
```

### filter

```dart
ui.ImageFilter get filter
```

The image filter to apply to the existing painted content.

For example, consider using [ui.ImageFilter.blur] to create a backdrop blur effect.

The [filter] property is equivalent to [filterConfig] (with the help of the [ImageFilterConfig.new] constructor), except for features only supported by [ImageFilterConfig] (such as the `bounds` parameter in [ImageFilterConfig.blur]).

Assigning a filter via this setter will overwrite any existing [filterConfig].

This getter should only be called when the filter is assigned via the [filter] setter, otherwise it will throw an assertion error.

### filter

```dart
set filter(ui.ImageFilter value)
```

### filterConfig

```dart
ImageFilterConfig get filterConfig
```

The configuration for the image filter to apply to the existing painted content.

For example, consider using [ImageFilterConfig.blur] to create a backdrop blur effect.

The [filterConfig] property is equivalent to [filter] (with the help of the [ImageFilterConfig.new] constructor), except for features only supported by [ImageFilterConfig] (such as the `bounds` parameter in [ImageFilterConfig.blur]).

Assigning a new [filterConfig] will overwrite any existing filter assigned via the [filter] setter.

### filterConfig

```dart
set filterConfig(ImageFilterConfig value)
```

### blendMode

```dart
BlendMode get blendMode
```

The blend mode to use to apply the filtered background content onto the background surface.

{@macro flutter.widgets.BackdropFilter.blendMode}

### blendMode

```dart
set blendMode(BlendMode value)
```

### backdropKey

```dart
BackdropKey? get backdropKey
```

The backdrop key that identifies the [BackdropGroup] this filter will read from.

The default value for the backdrop key is `null`.

### backdropKey

```dart
set backdropKey(BackdropKey? value)
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# CustomClipper

```dart
abstract class CustomClipper<T> extends Listenable {}
```

An interface for providing custom clips.

This class is used by a number of clip widgets (e.g., [ClipRect] and [ClipPath]).

The [getClip] method is called whenever the custom clip needs to be updated.

The [shouldReclip] method is called when a new instance of the class is provided, to check if the new instance actually represents different information.

The most efficient way to update the clip provided by this class is to supply a `reclip` argument to the constructor of the [CustomClipper]. The custom object will listen to this animation and update the clip whenever the animation ticks, avoiding both the build and layout phases of the pipeline.

See also:

- [ClipRect], which can be customized with a [CustomClipper<Rect>].
- [ClipRRect], which can be customized with a [CustomClipper<RRect>].
- [ClipOval], which can be customized with a [CustomClipper<Rect>].
- [ClipPath], which can be customized with a [CustomClipper<Path>].
- [ShapeBorderClipper], for specifying a clip path using a [ShapeBorder].

### CustomClipper()

```dart
CustomClipper({Listenable? reclip})
```

Creates a custom clipper.

The clipper will update its clip whenever [reclip] notifies its listeners.

### addListener()

```dart
void addListener(VoidCallback listener)
```

Register a closure to be notified when it is time to reclip.

The [CustomClipper] implementation merely forwards to the same method on the [Listenable] provided to the constructor in the `reclip` argument, if it was not null.

### removeListener()

```dart
void removeListener(VoidCallback listener)
```

Remove a previously registered closure from the list of closures that the object notifies when it is time to reclip.

The [CustomClipper] implementation merely forwards to the same method on the [Listenable] provided to the constructor in the `reclip` argument, if it was not null.

### getClip()

```dart
T getClip(Size size)
```

Returns a description of the clip given that the render object being clipped is of the given size.

### getApproximateClipRect()

```dart
Rect getApproximateClipRect(Size size)
```

Returns an approximation of the clip returned by [getClip], as an axis-aligned Rect. This is used by the semantics layer to determine whether widgets should be excluded.

By default, this returns a rectangle that is the same size as the RenderObject. If getClip returns a shape that is roughly the same size as the RenderObject (e.g. it's a rounded rectangle with very small arcs in the corners), then this may be adequate.

### shouldReclip()

```dart
bool shouldReclip(CustomClipper<T> oldClipper)
```

Called whenever a new instance of the custom clipper delegate class is provided to the clip object, or any time that a new clip object is created with a new instance of the custom clipper delegate class (which amounts to the same thing, because the latter is implemented in terms of the former).

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If the method returns false, then the [getClip] call might be optimized away.

It's possible that the [getClip] method will get called even if [shouldReclip] returns false or if the [shouldReclip] method is never called at all (e.g. if the box changes size).

### toString()

```dart
String toString()
```

# ShapeBorderClipper

```dart
class ShapeBorderClipper extends CustomClipper<Path> {}
```

A [CustomClipper] that clips to the outer path of a [ShapeBorder].

### ShapeBorderClipper()

```dart
ShapeBorderClipper({required ShapeBorder shape, TextDirection? textDirection})
```

Creates a [ShapeBorder] clipper.

The [textDirection] argument must be provided non-null if [shape] has a text direction dependency (for example if it is expressed in terms of "start" and "end" instead of "left" and "right"). It may be null if the border will not need the text direction to paint itself.

### shape

```dart
ShapeBorder shape
```

The shape border whose outer path this clipper clips to.

### textDirection

```dart
TextDirection? textDirection
```

The text direction to use for getting the outer path for [shape].

[ShapeBorder]s can depend on the text direction (e.g having a "dent" towards the start of the shape).

### getClip()

```dart
Path getClip(Size size)
```

Returns the outer path of [shape] as the clip.

### shouldReclip()

```dart
bool shouldReclip(CustomClipper<Path> oldClipper)
```

# RenderClipRect

```dart
class RenderClipRect extends _RenderCustomClip<Rect> {}
```

Clips its child using a rectangle.

By default, [RenderClipRect] prevents its child from painting outside its bounds, but the size and location of the clip rect can be customized using a custom [clipper].

### RenderClipRect()

```dart
RenderClipRect({RenderBox? child, CustomClipper<InvalidType>? clipper, dynamic clipBehavior})
```

Creates a rectangular clip.

If [clipper] is null, the clip will match the layout size and position of the child.

If [clipBehavior] is [Clip.none], no clipping will be applied.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

# RenderClipRRect

```dart
class RenderClipRRect extends _RenderCustomClip<RRect> {}
```

Clips its child using a rounded rectangle.

By default, [RenderClipRRect] uses its own bounds as the base rectangle for the clip, but the size and location of the clip can be customized using a custom [clipper].

### RenderClipRRect()

```dart
RenderClipRRect({RenderBox? child, BorderRadiusGeometry borderRadius = BorderRadius.zero, CustomClipper<InvalidType>? clipper, dynamic clipBehavior, TextDirection? textDirection})
```

Creates a rounded-rectangular clip.

The [borderRadius] defaults to [BorderRadius.zero], i.e. a rectangle with right-angled corners.

If [clipper] is non-null, then [borderRadius] is ignored.

If [clipBehavior] is [Clip.none], no clipping will be applied.

### borderRadius

```dart
BorderRadiusGeometry get borderRadius
```

The border radius of the rounded corners.

Values are clamped so that horizontal and vertical radii sums do not exceed width/height.

This value is ignored if [clipper] is non-null.

### borderRadius

```dart
set borderRadius(BorderRadiusGeometry value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [borderRadius].

### textDirection

```dart
set textDirection(TextDirection? value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

# RenderClipRSuperellipse

```dart
class RenderClipRSuperellipse extends _RenderCustomClip<RSuperellipse> {}
```

Clips its child using a rounded superellipse.

By default, [RenderClipRSuperellipse] uses its own bounds as the base rectangle for the clip, but the size and location of the clip can be customized using a custom [clipper].

Hit tests are performed based on the bounding box of the RSuperellipse.

### RenderClipRSuperellipse()

```dart
RenderClipRSuperellipse({RenderBox? child, BorderRadiusGeometry borderRadius = BorderRadius.zero, CustomClipper<InvalidType>? clipper, dynamic clipBehavior, TextDirection? textDirection})
```

Creates a rounded-superellipse clip.

The [borderRadius] defaults to [BorderRadius.zero], i.e. a rectangle with right-angled corners.

If [clipBehavior] is [Clip.none], no clipping will be applied.

### borderRadius

```dart
BorderRadiusGeometry get borderRadius
```

The border radius of the rounded corners.

Values are clamped so that horizontal and vertical radii sums do not exceed width/height.

This value is ignored if [clipper] is non-null.

### borderRadius

```dart
set borderRadius(BorderRadiusGeometry value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [borderRadius].

### textDirection

```dart
set textDirection(TextDirection? value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

# RenderClipOval

```dart
class RenderClipOval extends _RenderCustomClip<Rect> {}
```

Clips its child using an oval.

By default, inscribes an axis-aligned oval into its layout dimensions and prevents its child from painting outside that oval, but the size and location of the clip oval can be customized using a custom [clipper].

### RenderClipOval()

```dart
RenderClipOval({RenderBox? child, CustomClipper<InvalidType>? clipper, dynamic clipBehavior})
```

Creates an oval-shaped clip.

If [clipper] is null, the oval will be inscribed into the layout size and position of the child.

If [clipBehavior] is [Clip.none], no clipping will be applied.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

# RenderClipPath

```dart
class RenderClipPath extends _RenderCustomClip<Path> {}
```

Clips its child using a path.

Takes a delegate whose primary method returns a path that should be used to prevent the child from painting outside the path.

Clipping to a path is expensive. Certain shapes have more optimized render objects:

- To clip to a rectangle, consider [RenderClipRect].
- To clip to an oval or circle, consider [RenderClipOval].
- To clip to a rounded rectangle, consider [RenderClipRRect].

### RenderClipPath()

```dart
RenderClipPath({RenderBox? child, CustomClipper<InvalidType>? clipper, dynamic clipBehavior})
```

Creates a path clip.

If [clipper] is null, the clip will be a rectangle that matches the layout size and location of the child. However, rather than use this default, consider using a [RenderClipRect], which can achieve the same effect more efficiently.

If [clipBehavior] is [Clip.none], no clipping will be applied.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugPaintSize()

```dart
void debugPaintSize(PaintingContext context, Offset offset)
```

# RenderPhysicalModel

```dart
class RenderPhysicalModel extends _RenderPhysicalModelBase<RRect> {}
```

Creates a physical model layer that clips its child to a rounded rectangle.

A physical model layer casts a shadow based on its [elevation].

### RenderPhysicalModel()

```dart
RenderPhysicalModel({RenderBox? child, BoxShape shape = BoxShape.rectangle, dynamic clipBehavior, BorderRadius? borderRadius, double elevation = 0.0, required dynamic color, dynamic shadowColor = const Color(0xFF000000)})
```

Creates a rounded-rectangular clip.

The [color] is required.

The [elevation] parameter must be non-negative.

### shape

```dart
BoxShape get shape
```

The shape of the layer.

Defaults to [BoxShape.rectangle]. The [borderRadius] affects the corners of the rectangle.

### shape

```dart
set shape(BoxShape value)
```

### borderRadius

```dart
BorderRadius? get borderRadius
```

The border radius of the rounded corners.

Values are clamped so that horizontal and vertical radii sums do not exceed width/height.

This property is ignored if the [shape] is not [BoxShape.rectangle].

The value null is treated like [BorderRadius.zero].

### borderRadius

```dart
set borderRadius(BorderRadius? value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder description)
```

# RenderPhysicalShape

```dart
class RenderPhysicalShape extends _RenderPhysicalModelBase<Path> {}
```

Creates a physical shape layer that clips its child to a [Path].

A physical shape layer casts a shadow based on its [elevation].

See also:

- [RenderPhysicalModel], which is optimized for rounded rectangles and circles.

### RenderPhysicalShape()

```dart
RenderPhysicalShape({RenderBox? child, required CustomClipper<InvalidType> clipper, dynamic clipBehavior, double elevation = 0.0, required dynamic color, dynamic shadowColor = const Color(0xFF000000)})
```

Creates an arbitrary shape clip.

The [color] and [clipper] parameters are required.

The [elevation] parameter must be non-negative.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder description)
```

# DecorationPosition

```dart
enum DecorationPosition {}
```

Where to paint a box decoration.

Paint the box decoration behind the children.

Paint the box decoration in front of the children.

# RenderDecoratedBox

```dart
class RenderDecoratedBox extends RenderProxyBox {}
```

Paints a [Decoration] either before or after its child paints.

### RenderDecoratedBox()

```dart
RenderDecoratedBox({required Decoration decoration, DecorationPosition position = DecorationPosition.background, ImageConfiguration configuration = ImageConfiguration.empty, RenderBox? child})
```

Creates a decorated box.

The [decoration], [position], and [configuration] arguments must not be null. By default the decoration paints behind the child.

The [ImageConfiguration] will be passed to the decoration (with the size filled in) to let it resolve images.

### decoration

```dart
Decoration get decoration
```

What decoration to paint.

Commonly a [BoxDecoration].

### decoration

```dart
set decoration(Decoration value)
```

### position

```dart
DecorationPosition get position
```

Whether to paint the box decoration behind or in front of the child.

### position

```dart
set position(DecorationPosition value)
```

### configuration

```dart
ImageConfiguration get configuration
```

The settings to pass to the decoration when painting, so that it can resolve images appropriately. See [ImageProvider.resolve] and [BoxPainter.paint].

The [ImageConfiguration.textDirection] field is also used by direction-sensitive [Decoration]s for painting and hit-testing.

### configuration

```dart
set configuration(ImageConfiguration value)
```

### detach()

```dart
void detach()
```

### dispose()

```dart
void dispose()
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderTransform

```dart
class RenderTransform extends RenderProxyBox {}
```

Applies a transformation before painting its child.

### RenderTransform()

```dart
RenderTransform({required Matrix4 transform, Offset? origin, AlignmentGeometry? alignment, TextDirection? textDirection, bool transformHitTests = true, FilterQuality? filterQuality, RenderBox? child})
```

Creates a render object that transforms its child.

### origin

```dart
Offset? get origin
```

The origin of the coordinate system (relative to the upper left corner of this render object) in which to apply the matrix.

Setting an origin is equivalent to conjugating the transform matrix by a translation. This property is provided just for convenience.

### origin

```dart
set origin(Offset? value)
```

### alignment

```dart
AlignmentGeometry? get alignment
```

The alignment of the origin, relative to the size of the box.

This is equivalent to setting an origin based on the size of the box. If it is specified at the same time as an offset, both are applied.

An [AlignmentDirectional.centerStart] value is the same as an [Alignment] whose [Alignment.x] value is `-1.0` if [textDirection] is [TextDirection.ltr], and `1.0` if [textDirection] is [TextDirection.rtl]. Similarly [AlignmentDirectional.centerEnd] is the same as an [Alignment] whose [Alignment.x] value is `1.0` if [textDirection] is [TextDirection.ltr], and `-1.0` if [textDirection] is [TextDirection.rtl].

### alignment

```dart
set alignment(AlignmentGeometry? value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [alignment].

This may be changed to null, but only after [alignment] has been changed to a value that does not depend on the direction.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### transformHitTests

```dart
bool transformHitTests
```

When set to true, hit tests are performed based on the position of the child as it is painted. When set to false, hit tests are performed ignoring the transformation.

[applyPaintTransform], and therefore [localToGlobal] and [globalToLocal], always honor the transformation, regardless of the value of this property.

### transform

```dart
set transform(Matrix4 value)
```

The matrix to transform the child by during painting. The provided value is copied on assignment.

There is no getter for [transform], because [Matrix4] is mutable, and mutations outside of the control of the render object could not reliably be reflected in the rendering.

### filterQuality

```dart
FilterQuality? get filterQuality
```

The filter quality with which to apply the transform as a bitmap operation.

{@macro flutter.widgets.Transform.optional.FilterQuality}

### filterQuality

```dart
set filterQuality(FilterQuality? value)
```

### setIdentity()

```dart
void setIdentity()
```

Sets the transform to the identity matrix.

### rotateX()

```dart
void rotateX(double radians)
```

Concatenates a rotation about the x axis into the transform.

### rotateY()

```dart
void rotateY(double radians)
```

Concatenates a rotation about the y axis into the transform.

### rotateZ()

```dart
void rotateZ(double radians)
```

Concatenates a rotation about the z axis into the transform.

### translate()

```dart
void translate(double x, [double y = 0.0, double z = 0.0])
```

Concatenates a translation by (x, y, z) into the transform.

### scale()

```dart
void scale(double x, [double? y, double? z])
```

Concatenates a scale into the transform.

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderFittedBox

```dart
class RenderFittedBox extends RenderProxyBox {}
```

Scales and positions its child within itself according to [fit].

### RenderFittedBox()

```dart
RenderFittedBox({BoxFit fit = BoxFit.contain, AlignmentGeometry alignment = Alignment.center, TextDirection? textDirection, RenderBox? child, Clip clipBehavior = Clip.none})
```

Scales and positions its child within itself.

### fit

```dart
BoxFit get fit
```

How to inscribe the child into the space allocated during layout.

### fit

```dart
set fit(BoxFit value)
```

### alignment

```dart
AlignmentGeometry get alignment
```

How to align the child within its parent's bounds.

An alignment of (0.0, 0.0) aligns the child to the top-left corner of its parent's bounds. An alignment of (1.0, 0.5) aligns the child to the middle of the right edge of its parent's bounds.

If this is set to an [AlignmentDirectional] object, then [textDirection] must not be null.

### alignment

```dart
set alignment(AlignmentGeometry value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The text direction with which to resolve [alignment].

This may be changed to null, but only after [alignment] has been changed to a value that does not depend on the direction.

### textDirection

```dart
set textDirection(TextDirection? value)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paintsChild()

```dart
bool paintsChild(RenderBox child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderFractionalTranslation

```dart
class RenderFractionalTranslation extends RenderProxyBox {}
```

Applies a translation transformation before painting its child.

The translation is expressed as an [Offset] scaled to the child's size. For example, an [Offset] with a `dx` of 0.25 will result in a horizontal translation of one quarter the width of the child.

Hit tests will only be detected inside the bounds of the [RenderFractionalTranslation], even if the contents are offset such that they overflow.

### RenderFractionalTranslation()

```dart
RenderFractionalTranslation({required Offset translation, bool transformHitTests = true, RenderBox? child})
```

Creates a render object that translates its child's painting.

### translation

```dart
Offset get translation
```

The translation to apply to the child, scaled to the child's size.

For example, an [Offset] with a `dx` of 0.25 will result in a horizontal translation of one quarter the width of the child.

### translation

```dart
set translation(Offset value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### transformHitTests

```dart
bool transformHitTests
```

When set to true, hit tests are performed based on the position of the child as it is painted. When set to false, hit tests are performed ignoring the transformation.

applyPaintTransform(), and therefore localToGlobal() and globalToLocal(), always honor the transformation, regardless of the value of this property.

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# PointerDownEventListener

```dart
typedef PointerDownEventListener = void Function(PointerDownEvent event)
```

Signature for listening to [PointerDownEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerMoveEventListener

```dart
typedef PointerMoveEventListener = void Function(PointerMoveEvent event)
```

Signature for listening to [PointerMoveEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerUpEventListener

```dart
typedef PointerUpEventListener = void Function(PointerUpEvent event)
```

Signature for listening to [PointerUpEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerCancelEventListener

```dart
typedef PointerCancelEventListener = void Function(PointerCancelEvent event)
```

Signature for listening to [PointerCancelEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerPanZoomStartEventListener

```dart
typedef PointerPanZoomStartEventListener = void Function(PointerPanZoomStartEvent event)
```

Signature for listening to [PointerPanZoomStartEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerPanZoomUpdateEventListener

```dart
typedef PointerPanZoomUpdateEventListener = void Function(PointerPanZoomUpdateEvent event)
```

Signature for listening to [PointerPanZoomUpdateEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerPanZoomEndEventListener

```dart
typedef PointerPanZoomEndEventListener = void Function(PointerPanZoomEndEvent event)
```

Signature for listening to [PointerPanZoomEndEvent] events.

Used by [Listener] and [RenderPointerListener].

# PointerSignalEventListener

```dart
typedef PointerSignalEventListener = void Function(PointerSignalEvent event)
```

Signature for listening to [PointerSignalEvent] events.

Used by [Listener] and [RenderPointerListener].

# RenderPointerListener

```dart
class RenderPointerListener extends RenderProxyBoxWithHitTestBehavior {}
```

Calls callbacks in response to common pointer events.

It responds to events that can construct gestures, such as when the pointer is pointer is pressed and moved, and then released or canceled.

It does not respond to events that are exclusive to mouse, such as when the mouse enters and exits a region without pressing any buttons. For these events, use [RenderMouseRegion].

If it has a child, defers to the child for sizing behavior.

If it does not have a child, grows to fit the parent-provided constraints.

### RenderPointerListener()

```dart
RenderPointerListener({PointerDownEventListener? onPointerDown, PointerMoveEventListener? onPointerMove, PointerUpEventListener? onPointerUp, PointerHoverEventListener? onPointerHover, PointerCancelEventListener? onPointerCancel, PointerPanZoomStartEventListener? onPointerPanZoomStart, PointerPanZoomUpdateEventListener? onPointerPanZoomUpdate, PointerPanZoomEndEventListener? onPointerPanZoomEnd, PointerSignalEventListener? onPointerSignal, HitTestBehavior behavior, RenderBox? child})
```

Creates a render object that forwards pointer events to callbacks.

The [behavior] argument defaults to [HitTestBehavior.deferToChild].

### onPointerDown

```dart
PointerDownEventListener? onPointerDown
```

Called when a pointer comes into contact with the screen (for touch pointers), or has its button pressed (for mouse pointers) at this widget's location.

### onPointerMove

```dart
PointerMoveEventListener? onPointerMove
```

Called when a pointer that triggered an [onPointerDown] changes position.

### onPointerUp

```dart
PointerUpEventListener? onPointerUp
```

Called when a pointer that triggered an [onPointerDown] is no longer in contact with the screen.

### onPointerHover

```dart
PointerHoverEventListener? onPointerHover
```

Called when a pointer that has not an [onPointerDown] changes position.

### onPointerCancel

```dart
PointerCancelEventListener? onPointerCancel
```

Called when the input from a pointer that triggered an [onPointerDown] is no longer directed towards this receiver.

### onPointerPanZoomStart

```dart
PointerPanZoomStartEventListener? onPointerPanZoomStart
```

Called when a pan/zoom begins such as from a trackpad gesture.

### onPointerPanZoomUpdate

```dart
PointerPanZoomUpdateEventListener? onPointerPanZoomUpdate
```

Called when a pan/zoom is updated.

### onPointerPanZoomEnd

```dart
PointerPanZoomEndEventListener? onPointerPanZoomEnd
```

Called when a pan/zoom finishes.

### onPointerSignal

```dart
PointerSignalEventListener? onPointerSignal
```

Called when a pointer signal occurs over this object.

### computeSizeForNoChild()

```dart
Size computeSizeForNoChild(BoxConstraints constraints)
```

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderMouseRegion

```dart
class RenderMouseRegion extends RenderProxyBoxWithHitTestBehavior implements MouseTrackerAnnotation {}
```

Calls callbacks in response to pointer events that are exclusive to mice.

It responds to events that are related to hovering, i.e. when the mouse enters, exits (with or without pressing buttons), or moves over a region without pressing buttons.

It does not respond to common events that construct gestures, such as when the pointer is pressed, moved, then released or canceled. For these events, use [RenderPointerListener].

If it has a child, it defers to the child for sizing behavior.

If it does not have a child, it grows to fit the parent-provided constraints.

See also:

- [MouseRegion], a widget that listens to hover events using [RenderMouseRegion].

### RenderMouseRegion()

```dart
RenderMouseRegion({PointerEnterEventListener? onEnter, PointerHoverEventListener? onHover, PointerExitEventListener? onExit, MouseCursor cursor = MouseCursor.defer, bool validForMouseTracker = true, bool opaque = true, RenderBox? child, HitTestBehavior? hitTestBehavior = HitTestBehavior.opaque})
```

Creates a render object that forwards pointer events to callbacks.

All parameters are optional. By default this method creates an opaque mouse region with no callbacks and cursor being [MouseCursor.defer].

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### handleEvent()

```dart
void handleEvent(PointerEvent event, HitTestEntry entry)
```

### opaque

```dart
bool get opaque
```

Whether this object should prevent [RenderMouseRegion]s visually behind it from detecting the pointer, thus affecting how their [onHover], [onEnter], and [onExit] behave.

If [opaque] is true, this object will absorb the mouse pointer and prevent this object's siblings (or any other objects that are not ancestors or descendants of this object) from detecting the mouse pointer even when the pointer is within their areas.

If [opaque] is false, this object will not affect how [RenderMouseRegion]s behind it behave, which will detect the mouse pointer as long as the pointer is within their areas.

This defaults to true.

### opaque

```dart
set opaque(bool value)
```

### hitTestBehavior

```dart
HitTestBehavior? get hitTestBehavior
```

How to behave during hit testing.

This defaults to [HitTestBehavior.opaque] if null.

### hitTestBehavior

```dart
set hitTestBehavior(HitTestBehavior? value)
```

### onEnter

```dart
PointerEnterEventListener? onEnter
```

### onHover

```dart
PointerHoverEventListener? onHover
```

Triggered when a pointer has moved onto or within the region without buttons pressed.

This callback is not triggered by the movement of the object.

### onExit

```dart
PointerExitEventListener? onExit
```

### cursor

```dart
MouseCursor get cursor
```

### cursor

```dart
set cursor(MouseCursor value)
```

### validForMouseTracker

```dart
bool get validForMouseTracker
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### computeSizeForNoChild()

```dart
Size computeSizeForNoChild(BoxConstraints constraints)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderRepaintBoundary

```dart
class RenderRepaintBoundary extends RenderProxyBox {}
```

Creates a separate display list for its child.

This render object creates a separate display list for its child, which can improve performance if the subtree repaints at different times than the surrounding parts of the tree. Specifically, when the child does not repaint but its parent does, we can re-use the display list we recorded previously. Similarly, when the child repaints but the surround tree does not, we can re-record its display list without re-recording the display list for the surround tree.

In some cases, it is necessary to place _two_ (or more) repaint boundaries to get a useful effect. Consider, for example, an e-mail application that shows an unread count and a list of e-mails. Whenever a new e-mail comes in, the list would update, but so would the unread count. If only one of these two parts of the application was behind a repaint boundary, the entire application would repaint each time. On the other hand, if both were behind a repaint boundary, a new e-mail would only change those two parts of the application and the rest of the application would not repaint.

To tell if a particular RenderRepaintBoundary is useful, run your application in debug mode, interacting with it in typical ways, and then call [debugDumpRenderTree]. Each RenderRepaintBoundary will include the ratio of cases where the repaint boundary was useful vs the cases where it was not. These counts can also be inspected programmatically using [debugAsymmetricPaintCount] and [debugSymmetricPaintCount] respectively.

### RenderRepaintBoundary()

```dart
RenderRepaintBoundary({RenderBox? child})
```

Creates a repaint boundary around [child].

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### toImage()

```dart
Future<ui.Image> toImage({double pixelRatio = 1.0})
```

Capture an image of the current state of this render object and its children.

The returned [ui.Image] has uncompressed raw RGBA bytes in the dimensions of the render object, multiplied by the [pixelRatio].

To use [toImage], the render object must have gone through the paint phase (i.e. [debugNeedsPaint] must be false).

The [pixelRatio] describes the scale between the logical pixels and the size of the output image. It is independent of the [dart:ui.FlutterView.devicePixelRatio] for the device, so specifying 1.0 (the default) will give you a 1:1 mapping between logical pixels and the output pixels in the image.

{@tool snippet}

The following is an example of how to go from a `GlobalKey` on a `RepaintBoundary` to a PNG:

```dart
class PngHome extends StatefulWidget {
  const PngHome({super.key});

  @override
  State<PngHome> createState() => _PngHomeState();
}

class _PngHomeState extends State<PngHome> {
  GlobalKey globalKey = GlobalKey();

  Future<void> _capturePng() async {
    final RenderRepaintBoundary boundary = globalKey.currentContext!.findRenderObject()! as RenderRepaintBoundary;
    final ui.Image image = await boundary.toImage();
    final ByteData? byteData = await image.toByteData(format: ui.ImageByteFormat.png);
    final Uint8List pngBytes = byteData!.buffer.asUint8List();
    print(pngBytes);
  }

  @override
  Widget build(BuildContext context) {
    return RepaintBoundary(
      key: globalKey,
      child: Center(
        child: TextButton(
          onPressed: _capturePng,
          child: const Text('Hello World', textDirection: TextDirection.ltr),
        ),
      ),
    );
  }
}
```

{@end-tool}

See also:

- [OffsetLayer.toImage] for a similar API at the layer level.
- [dart:ui.Scene.toImage] for more information about the image returned.

### toImageSync()

```dart
ui.Image toImageSync({double pixelRatio = 1.0})
```

Capture an image of the current state of this render object and its children synchronously.

The returned [ui.Image] has uncompressed raw RGBA bytes in the dimensions of the render object, multiplied by the [pixelRatio].

To use [toImageSync], the render object must have gone through the paint phase (i.e. [debugNeedsPaint] must be false).

The [pixelRatio] describes the scale between the logical pixels and the size of the output image. It is independent of the [dart:ui.FlutterView.devicePixelRatio] for the device, so specifying 1.0 (the default) will give you a 1:1 mapping between logical pixels and the output pixels in the image.

This API functions like [toImage], except that rasterization begins eagerly on the raster thread and the image is returned before this is completed.

{@tool snippet}

The following is an example of how to go from a `GlobalKey` on a `RepaintBoundary` to an image handle:

```dart
class ImageCaptureHome extends StatefulWidget {
  const ImageCaptureHome({super.key});

  @override
  State<ImageCaptureHome> createState() => _ImageCaptureHomeState();
}

class _ImageCaptureHomeState extends State<ImageCaptureHome> {
  GlobalKey globalKey = GlobalKey();

  void _captureImage() {
    final RenderRepaintBoundary boundary = globalKey.currentContext!.findRenderObject()! as RenderRepaintBoundary;
    final ui.Image image = boundary.toImageSync();
    print('Image dimensions: ${image.width}x${image.height}');
  }

  @override
  Widget build(BuildContext context) {
    return RepaintBoundary(
      key: globalKey,
      child: Center(
        child: TextButton(
          onPressed: _captureImage,
          child: const Text('Hello World', textDirection: TextDirection.ltr),
        ),
      ),
    );
  }
}
```

{@end-tool}

See also:

- [OffsetLayer.toImageSync] for a similar API at the layer level.
- [dart:ui.Scene.toImageSync] for more information about the image returned.

### debugSymmetricPaintCount

```dart
int get debugSymmetricPaintCount
```

The number of times that this render object repainted at the same time as its parent. Repaint boundaries are only useful when the parent and child paint at different times. When both paint at the same time, the repaint boundary is redundant, and may be actually making performance worse.

Only valid when asserts are enabled. In release builds, always returns zero.

Can be reset using [debugResetMetrics]. See [debugAsymmetricPaintCount] for the corresponding count of times where only the parent or only the child painted.

### debugAsymmetricPaintCount

```dart
int get debugAsymmetricPaintCount
```

The number of times that either this render object repainted without the parent being painted, or the parent repainted without this object being painted. When a repaint boundary is used at a seam in the render tree where the parent tends to repaint at entirely different times than the child, it can improve performance by reducing the number of paint operations that have to be recorded each frame.

Only valid when asserts are enabled. In release builds, always returns zero.

Can be reset using [debugResetMetrics]. See [debugSymmetricPaintCount] for the corresponding count of times where both the parent and the child painted together.

### debugResetMetrics()

```dart
void debugResetMetrics()
```

Resets the [debugSymmetricPaintCount] and [debugAsymmetricPaintCount] counts to zero.

Only valid when asserts are enabled. Does nothing in release builds.

### debugRegisterRepaintBoundaryPaint()

```dart
void debugRegisterRepaintBoundaryPaint({bool includedParent = true, bool includedChild = false})
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderIgnorePointer

```dart
class RenderIgnorePointer extends RenderProxyBox {}
```

A render object that is invisible during hit testing.

When [ignoring] is true, this render object (and its subtree) is invisible to hit testing. It still consumes space during layout and paints its child as usual. It just cannot be the target of located events, because its render object returns false from [hitTest].

## Semantics

Using this class may also affect how the semantics subtree underneath is collected.

{@macro flutter.widgets.IgnorePointer.semantics}

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

See also:

- [RenderAbsorbPointer], which takes the pointer events but prevents any nodes in the subtree from seeing them.

### RenderIgnorePointer()

```dart
RenderIgnorePointer({RenderBox? child, bool ignoring = true, bool? ignoringSemantics})
```

Creates a render object that is invisible to hit testing.

### ignoring

```dart
bool get ignoring
```

Whether this render object is ignored during hit testing.

Regardless of whether this render object is ignored during hit testing, it will still consume space during layout and be visible during painting.

{@macro flutter.widgets.IgnorePointer.semantics}

### ignoring

```dart
set ignoring(bool value)
```

### ignoringSemantics

```dart
bool? get ignoringSemantics
```

Whether the semantics of this render object is ignored when compiling the semantics tree.

{@macro flutter.widgets.IgnorePointer.ignoringSemantics}

See [SemanticsNode] for additional information about the semantics tree.

### ignoringSemantics

```dart
set ignoringSemantics(bool? value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderOffstage

```dart
class RenderOffstage extends RenderProxyBox {}
```

Lays the child out as if it was in the tree, but without painting anything, without making the child available for hit testing, and without taking any room in the parent.

### RenderOffstage()

```dart
RenderOffstage({bool offstage = true, RenderBox? child})
```

Creates an offstage render object.

### offstage

```dart
bool get offstage
```

Whether the child is hidden from the rest of the tree.

If true, the child is laid out as if it was in the tree, but without painting anything, without making the child available for hit testing, and without taking any room in the parent.

If false, the child is included in the tree as normal.

### offstage

```dart
set offstage(bool value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDistanceToActualBaseline()

```dart
double? computeDistanceToActualBaseline(TextBaseline baseline)
```

### sizedByParent

```dart
bool get sizedByParent
```

### computeDryBaseline()

```dart
double? computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
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
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### paintsChild()

```dart
bool paintsChild(RenderBox child)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# RenderAbsorbPointer

```dart
class RenderAbsorbPointer extends RenderProxyBox {}
```

A render object that absorbs pointers during hit testing.

When [absorbing] is true, this render object prevents its subtree from receiving pointer events by terminating hit testing at itself. It still consumes space during layout and paints its child as usual. It just prevents its children from being the target of located events, because its render object returns true from [hitTest].

## Semantics

Using this class may also affect how the semantics subtree underneath is collected.

{@macro flutter.widgets.AbsorbPointer.semantics}

{@macro flutter.widgets.AbsorbPointer.ignoringSemantics}

See also:

- [RenderIgnorePointer], which has the opposite effect: removing the subtree from considering entirely for the purposes of hit testing.

### RenderAbsorbPointer()

```dart
RenderAbsorbPointer({RenderBox? child, bool absorbing = true, bool? ignoringSemantics})
```

Creates a render object that absorbs pointers during hit testing.

### absorbing

```dart
bool get absorbing
```

Whether this render object absorbs pointers during hit testing.

Regardless of whether this render object absorbs pointers during hit testing, it will still consume space during layout and be visible during painting.

{@macro flutter.widgets.AbsorbPointer.semantics}

### absorbing

```dart
set absorbing(bool value)
```

### ignoringSemantics

```dart
bool? get ignoringSemantics
```

Whether the semantics of this render object is ignored when compiling the semantics tree.

{@macro flutter.widgets.AbsorbPointer.ignoringSemantics}

See [SemanticsNode] for additional information about the semantics tree.

### ignoringSemantics

```dart
set ignoringSemantics(bool? value)
```

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderMetaData

```dart
class RenderMetaData extends RenderProxyBoxWithHitTestBehavior {}
```

Holds opaque meta data in the render tree.

Useful for decorating the render tree with information that will be consumed later. For example, you could store information in the render tree that will be used when the user interacts with the render tree but has no visual impact prior to the interaction.

### RenderMetaData()

```dart
RenderMetaData({dynamic metaData, HitTestBehavior behavior, RenderBox? child})
```

Creates a render object that hold opaque meta data.

The [behavior] argument defaults to [HitTestBehavior.deferToChild].

### metaData

```dart
dynamic metaData
```

Opaque meta data ignored by the render tree.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSemanticsGestureHandler

```dart
class RenderSemanticsGestureHandler extends RenderProxyBoxWithHitTestBehavior {}
```

Listens for the specified gestures from the semantics server (e.g. an accessibility tool).

### RenderSemanticsGestureHandler()

```dart
RenderSemanticsGestureHandler({RenderBox? child, GestureTapCallback? onTap, GestureLongPressCallback? onLongPress, GestureDragUpdateCallback? onHorizontalDragUpdate, GestureDragUpdateCallback? onVerticalDragUpdate, double scrollFactor = 0.8, HitTestBehavior behavior})
```

Creates a render object that listens for specific semantic gestures.

### validActions

```dart
Set<SemanticsAction>? get validActions
```

If non-null, the set of actions to allow. Other actions will be omitted, even if their callback is provided.

For example, if [onTap] is non-null but [validActions] does not contain [SemanticsAction.tap], then the semantic description of this node will not claim to support taps.

This is normally used to filter the actions made available by [onHorizontalDragUpdate] and [onVerticalDragUpdate]. Normally, these make both the right and left, or up and down, actions available. For example, if [onHorizontalDragUpdate] is set but [validActions] only contains [SemanticsAction.scrollLeft], then the [SemanticsAction.scrollRight] action will be omitted.

### validActions

```dart
set validActions(Set<SemanticsAction>? value)
```

### onTap

```dart
GestureTapCallback? get onTap
```

Called when the user taps on the render object.

### onTap

```dart
set onTap(GestureTapCallback? value)
```

### onLongPress

```dart
GestureLongPressCallback? get onLongPress
```

Called when the user presses on the render object for a long period of time.

### onLongPress

```dart
set onLongPress(GestureLongPressCallback? value)
```

### onHorizontalDragUpdate

```dart
GestureDragUpdateCallback? get onHorizontalDragUpdate
```

Called when the user scrolls to the left or to the right.

### onHorizontalDragUpdate

```dart
set onHorizontalDragUpdate(GestureDragUpdateCallback? value)
```

### onVerticalDragUpdate

```dart
GestureDragUpdateCallback? get onVerticalDragUpdate
```

Called when the user scrolls up or down.

### onVerticalDragUpdate

```dart
set onVerticalDragUpdate(GestureDragUpdateCallback? value)
```

### scrollFactor

```dart
double scrollFactor
```

The fraction of the dimension of this render box to use when scrolling. For example, if this is 0.8 and the box is 200 pixels wide, then when a left-scroll action is received from the accessibility system, it will translate into a 160 pixel leftwards drag.

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSemanticsAnnotations

```dart
class RenderSemanticsAnnotations extends RenderProxyBox with SemanticsAnnotationsMixin {}
```

Add annotations to the [SemanticsNode] for this subtree.

### RenderSemanticsAnnotations()

```dart
RenderSemanticsAnnotations({RenderBox? child, required SemanticsProperties properties, bool container = false, bool explicitChildNodes = false, bool excludeSemantics = false, bool blockUserActions = false, Locale? localeForSubtree, TextDirection? textDirection})
```

Creates a render object that attaches a semantic annotation.

If the [SemanticsProperties.attributedLabel] is not null, the [textDirection] must also not be null.

# RenderBlockSemantics

```dart
class RenderBlockSemantics extends RenderProxyBox {}
```

Causes the semantics of all earlier render objects below the same semantic boundary to be dropped.

This is useful in a stack where an opaque mask should prevent interactions with the render objects painted below the mask.

### RenderBlockSemantics()

```dart
RenderBlockSemantics({RenderBox? child, bool blocking = true})
```

Create a render object that blocks semantics for nodes below it in paint order.

### blocking

```dart
bool get blocking
```

Whether this render object is blocking semantics of previously painted [RenderObject]s below a common semantics boundary from the semantic tree.

### blocking

```dart
set blocking(bool value)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderMergeSemantics

```dart
class RenderMergeSemantics extends RenderProxyBox {}
```

Causes the semantics of all descendants to be merged into this node such that the entire subtree becomes a single leaf in the semantics tree.

Useful for combining the semantics of multiple render objects that form part of a single conceptual widget, e.g. a checkbox, a label, and the gesture detector that goes with them.

### RenderMergeSemantics()

```dart
RenderMergeSemantics({RenderBox? child})
```

Creates a render object that merges the semantics from its descendants.

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

# RenderExcludeSemantics

```dart
class RenderExcludeSemantics extends RenderProxyBox {}
```

Excludes this subtree from the semantic tree.

When [excluding] is true, this render object (and its subtree) is excluded from the semantic tree.

Useful e.g. for hiding text that is redundant with other text next to it (e.g. text included only for the visual effect).

### RenderExcludeSemantics()

```dart
RenderExcludeSemantics({RenderBox? child, bool excluding = true})
```

Creates a render object that ignores the semantics of its subtree.

### excluding

```dart
bool get excluding
```

Whether this render object is excluded from the semantic tree.

### excluding

```dart
set excluding(bool value)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderIndexedSemantics

```dart
class RenderIndexedSemantics extends RenderProxyBox {}
```

A render objects that annotates semantics with an index.

Certain widgets will automatically provide a child index for building semantics. For example, the [ScrollView] uses the index of the first visible child semantics node to determine the [SemanticsConfiguration.scrollIndex].

See also:

- [CustomScrollView], for an explanation of scroll semantics.

### RenderIndexedSemantics()

```dart
RenderIndexedSemantics({RenderBox? child, required int index})
```

Creates a render object that annotates the child semantics with an index.

### index

```dart
int get index
```

The index used to annotated child semantics.

### index

```dart
set index(int value)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderLeaderLayer

```dart
class RenderLeaderLayer extends RenderProxyBox {}
```

Provides an anchor for a [RenderFollowerLayer].

See also:

- [CompositedTransformTarget], the corresponding widget.
- [LeaderLayer], the layer that this render object creates.

### RenderLeaderLayer()

```dart
RenderLeaderLayer({required LayerLink link, RenderBox? child})
```

Creates a render object that uses a [LeaderLayer].

### link

```dart
LayerLink get link
```

The link object that connects this [RenderLeaderLayer] with one or more [RenderFollowerLayer]s.

The object must not be associated with another [RenderLeaderLayer] that is also being painted.

### link

```dart
set link(LayerLink value)
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### performLayout()

```dart
void performLayout()
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderFollowerLayer

```dart
class RenderFollowerLayer extends RenderProxyBox {}
```

Transform the child so that its origin is [offset] from the origin of the [RenderLeaderLayer] with the same [LayerLink].

The [RenderLeaderLayer] in question must be earlier in the paint order.

Hit testing on descendants of this render object will only work if the target position is within the box that this render object's parent considers to be hittable.

See also:

- [CompositedTransformFollower], the corresponding widget.
- [FollowerLayer], the layer that this render object creates.

### RenderFollowerLayer()

```dart
RenderFollowerLayer({required LayerLink link, bool showWhenUnlinked = true, Offset offset = Offset.zero, Alignment leaderAnchor = Alignment.topLeft, Alignment followerAnchor = Alignment.topLeft, RenderBox? child})
```

Creates a render object that uses a [FollowerLayer].

### link

```dart
LayerLink get link
```

The link object that connects this [RenderFollowerLayer] with a [RenderLeaderLayer] earlier in the paint order.

### link

```dart
set link(LayerLink value)
```

### showWhenUnlinked

```dart
bool get showWhenUnlinked
```

Whether to show the render object's contents when there is no corresponding [RenderLeaderLayer] with the same [link].

When the render object is linked, the child is positioned such that it has the same global position as the linked [RenderLeaderLayer].

When the render object is not linked, then: if [showWhenUnlinked] is true, the child is visible and not repositioned; if it is false, then child is hidden, and its hit testing is also disabled.

### showWhenUnlinked

```dart
set showWhenUnlinked(bool value)
```

### offset

```dart
Offset get offset
```

The offset to apply to the origin of the linked [RenderLeaderLayer] to obtain this render object's origin.

### offset

```dart
set offset(Offset value)
```

### leaderAnchor

```dart
Alignment get leaderAnchor
```

The anchor point on the linked [RenderLeaderLayer] that [followerAnchor] will line up with.

{@template flutter.rendering.RenderFollowerLayer.leaderAnchor} For example, when [leaderAnchor] and [followerAnchor] are both [Alignment.topLeft], this [RenderFollowerLayer] will be top left aligned with the linked [RenderLeaderLayer]. When [leaderAnchor] is [Alignment.bottomLeft] and [followerAnchor] is [Alignment.topLeft], this [RenderFollowerLayer] will be left aligned with the linked [RenderLeaderLayer], and its top edge will line up with the [RenderLeaderLayer]'s bottom edge. {@endtemplate}

Defaults to [Alignment.topLeft].

### leaderAnchor

```dart
set leaderAnchor(Alignment value)
```

### followerAnchor

```dart
Alignment get followerAnchor
```

The anchor point on this [RenderFollowerLayer] that will line up with [followerAnchor] on the linked [RenderLeaderLayer].

{@macro flutter.rendering.RenderFollowerLayer.leaderAnchor}

Defaults to [Alignment.topLeft].

### followerAnchor

```dart
set followerAnchor(Alignment value)
```

### detach()

```dart
void detach()
```

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### layer

```dart
FollowerLayer? get layer
```

The layer we created when we were last painted.

### getCurrentTransform()

```dart
Matrix4 getCurrentTransform()
```

Return the transform that was used in the last composition phase, if any.

If the [FollowerLayer] has not yet been created, was never composited, or was unable to determine the transform (see [FollowerLayer.getLastTransform]), this returns the identity matrix (see [Matrix4.identity].

### hitTest()

```dart
bool hitTest(BoxHitTestResult result, {required Offset position})
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderAnnotatedRegion

```dart
class RenderAnnotatedRegion<T extends Object> extends RenderProxyBox {}
```

Render object which inserts an [AnnotatedRegionLayer] into the layer tree.

See also:

- [Layer.find], for an example of how this value is retrieved.
- [AnnotatedRegionLayer], the layer this render object creates.

### RenderAnnotatedRegion()

```dart
RenderAnnotatedRegion({required T value, required bool sized, RenderBox? child})
```

Creates a new [RenderAnnotatedRegion] to insert [value] into the layer tree.

If [sized] is true, the layer is provided with the size of this render object to clip the results of [Layer.find].

Neither [value] nor [sized] can be null.

### value

```dart
T get value
```

A value which can be retrieved using [Layer.find].

### value

```dart
set value(T newValue)
```

### sized

```dart
bool get sized
```

Whether the render object will pass its [size] to the [AnnotatedRegionLayer].

### sized

```dart
set sized(bool value)
```

### alwaysNeedsCompositing

```dart
bool alwaysNeedsCompositing
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```
