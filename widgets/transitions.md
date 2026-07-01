@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/widgets.dart';

# AnimatedWidget

```dart
abstract class AnimatedWidget extends StatefulWidget {}
```

A widget that rebuilds when the given [Listenable] changes value.

{@youtube 560 315 https://www.youtube.com/watch?v=LKKgYpC-EPQ}

[AnimatedWidget] is most commonly used with [Animation] objects, which are [Listenable], but it can be used with any [Listenable], including [ChangeNotifier] and [ValueNotifier].

[AnimatedWidget] is most useful for widgets that are otherwise stateless. To use [AnimatedWidget], subclass it and implement the build function.

{@tool dartpad} This code defines a widget called `Spinner` that spins a green square continually. It is built with an [AnimatedWidget].

** See code in examples/api/lib/widgets/transitions/animated_widget.0.dart ** {@end-tool}

For more complex case involving additional state, consider using [AnimatedBuilder] or [ListenableBuilder].

## Relationship to [ImplicitlyAnimatedWidget]s

[AnimatedWidget]s (and their subclasses) take an explicit [Listenable] as argument, which is usually an [Animation] derived from an [AnimationController]. In most cases, the lifecycle of that [AnimationController] has to be managed manually by the developer. In contrast to that, [ImplicitlyAnimatedWidget]s (and their subclasses) automatically manage their own internal [AnimationController] making those classes easier to use as no external [Animation] has to be provided by the developer. If you only need to set a target value for the animation and configure its duration/curve, consider using (a subclass of) [ImplicitlyAnimatedWidget]s instead of (a subclass of) this class.

## Common animated widgets

A number of animated widgets ship with the framework. They are usually named `FooTransition`, where `Foo` is the name of the non-animated version of that widget. The subclasses of this class should not be confused with subclasses of [ImplicitlyAnimatedWidget] (see above), which are usually named `AnimatedFoo`. Commonly used animated widgets include:

- [ListenableBuilder], which uses a builder pattern that is useful for complex [Listenable] use cases.
- [AnimatedBuilder], which uses a builder pattern that is useful for complex [Animation] use cases.
- [AlignTransition], which is an animated version of [Align].
- [DecoratedBoxTransition], which is an animated version of [DecoratedBox].
- [DefaultTextStyleTransition], which is an animated version of [DefaultTextStyle].
- [PositionedTransition], which is an animated version of [Positioned].
- [RelativePositionedTransition], which is an animated version of [Positioned].
- [RotationTransition], which animates the rotation of a widget.
- [ScaleTransition], which animates the scale of a widget.
- [SizeTransition], which animates its own size.
- [SlideTransition], which animates the position of a widget relative to its normal position.
- [FadeTransition], which is an animated version of [Opacity].
- [AnimatedModalBarrier], which is an animated version of [ModalBarrier].

### AnimatedWidget()

```dart
AnimatedWidget({dynamic key, required Listenable listenable})
```

Creates a widget that rebuilds when the given listenable changes.

The [listenable] argument is required.

### listenable

```dart
Listenable listenable
```

The [Listenable] to which this widget is listening.

Commonly an [Animation] or a [ChangeNotifier].

### build()

```dart
Widget build(BuildContext context)
```

Override this method to build widgets that depend on the state of the listenable (e.g., the current value of the animation).

### createState()

```dart
State<AnimatedWidget> createState()
```

Subclasses typically do not override this method.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DelegatedTransitionBuilder

```dart
typedef DelegatedTransitionBuilder = Widget? Function(BuildContext context, Animation<double> animation, Animation<double> secondaryAnimation, bool allowSnapshotting, Widget? child)
```

Signature for a builder used to control a page's exit transition.

When a new route enters the stack, the `animation` argument is typically used to control the enter and exit transition of the topmost route. The exit transition of the route just below the new route is controlled with the `secondaryAnimation`, which also controls the transition of the old route when the topmost route is popped off the stack.

Typically used as the argument for [ModalRoute.delegatedTransition].

# SlideTransition

```dart
class SlideTransition extends AnimatedWidget {}
```

Animates the position of a widget relative to its normal position.

The translation is expressed as an [Offset] scaled to the child's size. For example, an [Offset] with a `dx` of 0.25 will result in a horizontal translation of one quarter the width of the child.

By default, the offsets are applied in the coordinate system of the canvas (so positive x offsets move the child towards the right). If a [textDirection] is provided, then the offsets are applied in the reading direction, so in right-to-left text, positive x offsets move towards the left, and in left-to-right text, positive x offsets move towards the right.

Here's an illustration of the [SlideTransition] widget, with its [position] animated by a [CurvedAnimation] set to [Curves.elasticIn]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/slide_transition.mp4}

{@tool dartpad} The following code implements the [SlideTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/slide_transition.0.dart ** {@end-tool}

See also:

- [AlignTransition], an animated version of an [Align] that animates its [Align.alignment] property.
- [PositionedTransition], a widget that animates its child from a start position to an end position over the lifetime of the animation.
- [RelativePositionedTransition], a widget that transitions its child's position based on the value of a rectangle relative to a bounding box.

### SlideTransition()

```dart
SlideTransition({dynamic key, required Animation<Offset> position, bool transformHitTests = true, TextDirection? textDirection, Widget? child})
```

Creates a fractional translation transition.

### position

```dart
Animation<Offset> get position
```

The animation that controls the position of the child.

If the current value of the position animation is `(dx, dy)`, the child will be translated horizontally by `width * dx` and vertically by `height * dy`, after applying the [textDirection] if available.

### textDirection

```dart
TextDirection? textDirection
```

The direction to use for the x offset described by the [position].

If [textDirection] is null, the x offset is applied in the coordinate system of the canvas (so positive x offsets move the child towards the right).

If [textDirection] is [TextDirection.rtl], the x offset is applied in the reading direction such that x offsets move the child towards the left.

If [textDirection] is [TextDirection.ltr], the x offset is applied in the reading direction such that x offsets move the child towards the right.

### transformHitTests

```dart
bool transformHitTests
```

Whether hit testing should be affected by the slide animation.

If false, hit testing will proceed as if the child was not translated at all. Setting this value to false is useful for fast animations where you expect the user to commonly interact with the child widget in its final location and you want the user to benefit from "muscle memory".

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# TransformCallback

```dart
typedef TransformCallback = Matrix4 Function(double animationValue)
```

Signature for the callback to [MatrixTransition.onTransform].

Computes a [Matrix4] to be used in the [MatrixTransition] transformed widget from the [MatrixTransition.animation] value.

# MatrixTransition

```dart
class MatrixTransition extends AnimatedWidget {}
```

Animates the [Matrix4] of a transformed widget.

The [onTransform] callback computes a [Matrix4] from the animated value, it is called every time the [animation] changes its value.

{@tool dartpad} The following example implements a [MatrixTransition] with a rotation around the Y axis, with a 3D perspective skew.

** See code in examples/api/lib/widgets/transitions/matrix_transition.0.dart ** {@end-tool}

See also:

- [ScaleTransition], which animates the scale of a widget, by providing a matrix which scales along the X and Y axis.
- [RotationTransition], which animates the rotation of a widget, by providing a matrix which rotates along the Z axis.

### MatrixTransition()

```dart
MatrixTransition({dynamic key, required Animation<double> animation, required TransformCallback onTransform, Alignment alignment = Alignment.center, FilterQuality? filterQuality, Widget? child})
```

Creates a matrix transition.

The [alignment] argument defaults to [Alignment.center].

### onTransform

```dart
TransformCallback onTransform
```

The callback to compute a [Matrix4] from the [animation]. It's called every time [animation] changes its value.

### animation

```dart
Animation<double> get animation
```

The animation that controls the matrix of the child.

The matrix will be computed from the animation with the [onTransform] callback.

### alignment

```dart
Alignment alignment
```

The alignment of the origin of the coordinate system in which the transform takes place, relative to the size of the box.

For example, to set the origin of the transform to bottom middle, you can use an alignment of (0.0, 1.0).

### filterQuality

```dart
FilterQuality? filterQuality
```

The filter quality with which to apply the transform as a bitmap operation.

When the animation is stopped (either in [AnimationStatus.dismissed] or [AnimationStatus.completed]), the filter quality argument will be ignored.

{@macro flutter.widgets.Transform.optional.FilterQuality}

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# ScaleTransition

```dart
class ScaleTransition extends MatrixTransition {}
```

Animates the scale of a transformed widget.

Here's an illustration of the [ScaleTransition] widget, with it's [scale] animated by a [CurvedAnimation] set to [Curves.fastOutSlowIn]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/scale_transition.mp4}

{@tool dartpad} The following code implements the [ScaleTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/scale_transition.0.dart ** {@end-tool}

See also:

- [PositionedTransition], a widget that animates its child from a start position to an end position over the lifetime of the animation.
- [RelativePositionedTransition], a widget that transitions its child's position based on the value of a rectangle relative to a bounding box.
- [SizeTransition], a widget that animates its own size and clips and aligns its child.

### ScaleTransition()

```dart
ScaleTransition({dynamic key, required Animation<double> scale, dynamic alignment = Alignment.center, dynamic filterQuality, Widget? child})
```

Creates a scale transition.

The [alignment] argument defaults to [Alignment.center].

### scale

```dart
Animation<double> get scale
```

The animation that controls the scale of the child.

# RotationTransition

```dart
class RotationTransition extends MatrixTransition {}
```

Animates the rotation of a widget.

Here's an illustration of the [RotationTransition] widget, with it's [turns] animated by a [CurvedAnimation] set to [Curves.elasticOut]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/rotation_transition.mp4}

{@tool dartpad} The following code implements the [RotationTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/rotation_transition.0.dart ** {@end-tool}

See also:

- [ScaleTransition], a widget that animates the scale of a transformed widget.
- [SizeTransition], a widget that animates its own size and clips and aligns its child.

### RotationTransition()

```dart
RotationTransition({dynamic key, required Animation<double> turns, dynamic alignment = Alignment.center, dynamic filterQuality, Widget? child})
```

Creates a rotation transition.

### turns

```dart
Animation<double> get turns
```

The animation that controls the rotation of the child.

# SizeTransition

```dart
class SizeTransition extends AnimatedWidget {}
```

Animates its own size and clips and aligns its child.

[SizeTransition] acts as a [ClipRect] that animates either its width or its height, depending upon the value of [axis]. The alignment of the child is specified by the [alignment].

Like most widgets, [SizeTransition] will conform to the constraints it is given, so be sure to put it in a context where it can change size. For instance, if you place it into a [Container] with a fixed size, then the [SizeTransition] will not be able to change size, and will appear to do nothing.

Here's an illustration of the [SizeTransition] widget, with it's [sizeFactor] animated by a [CurvedAnimation] set to [Curves.fastOutSlowIn]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/size_transition.mp4}

{@tool dartpad} This code defines a widget that uses [SizeTransition] to change the size of [FlutterLogo] continually. It is built with a [Scaffold] where the internal widget has space to change its size.

** See code in examples/api/lib/widgets/transitions/size_transition.0.dart ** {@end-tool}

See also:

- [AnimatedCrossFade], for a widget that automatically animates between the sizes of two children, fading between them.
- [ScaleTransition], a widget that scales the size of the child instead of clipping it.
- [PositionedTransition], a widget that animates its child from a start position to an end position over the lifetime of the animation.
- [RelativePositionedTransition], a widget that transitions its child's position based on the value of a rectangle relative to a bounding box.

### SizeTransition()

```dart
SizeTransition({dynamic key, Axis axis = Axis.vertical, required Animation<double> sizeFactor, double? axisAlignment, AlignmentGeometry? alignment, double? fixedCrossAxisSizeFactor, Widget? child})
```

Creates a size transition.

The [axis] argument defaults to [Axis.vertical]. The [alignment] defaults to [Alignment.center], which centers the child within the parent during the transition.

### axis

```dart
Axis axis
```

[Axis.horizontal] if [sizeFactor] modifies the width, otherwise [Axis.vertical].

### sizeFactor

```dart
Animation<double> get sizeFactor
```

The animation that controls the (clipped) size of the child.

The width or height (depending on the [axis] value) of this widget will be its intrinsic width or height multiplied by [sizeFactor]'s value at the current point in the animation.

If the value of [sizeFactor] is less than one, the child will be clipped in the appropriate axis.

### axisAlignment

```dart
double? axisAlignment
```

Describes how to align the child along the axis that [sizeFactor] is modifying.

A value of -1.0 indicates the top when [axis] is [Axis.vertical], and the start when [axis] is [Axis.horizontal]. The start is on the left when the text direction in effect is [TextDirection.ltr] and on the right when it is [TextDirection.rtl].

A value of 1.0 indicates the bottom or end, depending upon the [axis].

A value of 0.0 (the default) indicates the center for either [axis] value.

This property has been deprecated and superseded by [alignment]. Existing usages can be migrated to [alignment] as follows:

- If [axis] is [Axis.horizontal], replace with `Alignment(axisAlignment ?? 0.0, -1.0)`.
- If [axis] is [Axis.vertical], replace with `Alignment(-1.0, axisAlignment ?? 0.0)`.

### alignment

```dart
AlignmentGeometry? alignment
```

The alignment of the child within the parent during the transition.

### fixedCrossAxisSizeFactor

```dart
double? fixedCrossAxisSizeFactor
```

The factor by which to multiply the cross axis size of the child.

If the value of [fixedCrossAxisSizeFactor] is less than one, the child will be clipped along the appropriate axis.

If `null` (the default), the cross axis size is as large as the parent.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# FadeTransition

```dart
class FadeTransition extends SingleChildRenderObjectWidget {}
```

Animates the opacity of a widget.

For a widget that automatically animates between the sizes of two children, fading between them, see [AnimatedCrossFade].

{@youtube 560 315 https://www.youtube.com/watch?v=rLwWVbv3xDQ}

Here's an illustration of the [FadeTransition] widget, with it's [opacity] animated by a [CurvedAnimation] set to [Curves.fastOutSlowIn]:

{@tool dartpad} The following code implements the [FadeTransition] using the Flutter logo:

** See code in examples/api/lib/widgets/transitions/fade_transition.0.dart ** {@end-tool}

## Hit testing

Setting the [opacity] to zero does not prevent hit testing from being applied to the descendants of the [FadeTransition] widget. This can be confusing for the user, who may not see anything, and may believe the area of the interface where the [FadeTransition] is hiding a widget to be non-interactive.

With certain widgets, such as [Flow], that compute their positions only when they are painted, this can actually lead to bugs (from unexpected geometry to exceptions), because those widgets are not painted by the [FadeTransition] widget at all when the [opacity] animation reaches zero.

To avoid such problems, it is generally a good idea to combine this widget with an [IgnorePointer] that one enables when the [opacity] animation reaches zero. This prevents interactions with any children in the subtree when the [child] is not visible. For performance reasons, when implementing this, care should be taken not to rebuild the relevant widget (e.g. by calling [State.setState]) except at the transition point.

See also:

- [Opacity], which does not animate changes in opacity.
- [AnimatedOpacity], which animates changes in opacity without taking an explicit [Animation] argument.
- [SliverFadeTransition], the sliver version of this widget.

### FadeTransition()

```dart
FadeTransition({dynamic key, required Animation<double> opacity, bool alwaysIncludeSemantics = false, Widget? child})
```

Creates an opacity transition.

### opacity

```dart
Animation<double> opacity
```

The animation that controls the opacity of the child.

If the current value of the opacity animation is v, the child will be painted with an opacity of v. For example, if v is 0.5, the child will be blended 50% with its background. Similarly, if v is 0.0, the child will be completely transparent.

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

Whether the semantic information of the children is always included.

Defaults to false.

When true, regardless of the opacity settings the child semantic information is exposed as if the widget were fully visible. This is useful in cases where labels may be hidden during animations that would otherwise contribute relevant semantics.

### createRenderObject()

```dart
RenderAnimatedOpacity createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderAnimatedOpacity renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverFadeTransition

```dart
class SliverFadeTransition extends SingleChildRenderObjectWidget {}
```

Animates the opacity of a sliver widget.

{@tool dartpad} Creates a [CustomScrollView] with a [SliverFixedExtentList] that uses a [SliverFadeTransition] to fade the list in and out.

** See code in examples/api/lib/widgets/transitions/sliver_fade_transition.0.dart ** {@end-tool}

Here's an illustration of the [FadeTransition] widget, the [RenderBox] equivalent widget, with it's [opacity] animated by a [CurvedAnimation] set to [Curves.fastOutSlowIn]:

{@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/fade_transition.mp4}

## Hit testing

Setting the [opacity] to zero does not prevent hit testing from being applied to the descendants of the [SliverFadeTransition] widget. This can be confusing for the user, who may not see anything, and may believe the area of the interface where the [SliverFadeTransition] is hiding a widget to be non-interactive.

With certain widgets, such as [Flow], that compute their positions only when they are painted, this can actually lead to bugs (from unexpected geometry to exceptions), because those widgets are not painted by the [SliverFadeTransition] widget at all when the [opacity] animation reaches zero.

To avoid such problems, it is generally a good idea to combine this widget with a [SliverIgnorePointer] that one enables when the [opacity] animation reaches zero. This prevents interactions with any children in the subtree when the sliver is not visible. For performance reasons, when implementing this, care should be taken not to rebuild the relevant widget (e.g. by calling [State.setState]) except at the transition point.

See also:

- [SliverOpacity], which does not animate changes in opacity.
- [FadeTransition], the box version of this widget.

### SliverFadeTransition()

```dart
SliverFadeTransition({dynamic key, required Animation<double> opacity, bool alwaysIncludeSemantics = false, Widget? sliver})
```

Creates an opacity transition.

### opacity

```dart
Animation<double> opacity
```

The animation that controls the opacity of the sliver child.

If the current value of the opacity animation is v, the child will be painted with an opacity of v. For example, if v is 0.5, the child will be blended 50% with its background. Similarly, if v is 0.0, the child will be completely transparent.

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

Whether the semantic information of the sliver child is always included.

Defaults to false.

When true, regardless of the opacity settings the sliver child's semantic information is exposed as if the widget were fully visible. This is useful in cases where labels may be hidden during animations that would otherwise contribute relevant semantics.

### createRenderObject()

```dart
RenderSliverAnimatedOpacity createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderSliverAnimatedOpacity renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RelativeRectTween

```dart
class RelativeRectTween extends Tween<RelativeRect> {}
```

An interpolation between two relative rects.

This class specializes the interpolation of [Tween<RelativeRect>] to use [RelativeRect.lerp].

See [Tween] for a discussion on how to use interpolation objects.

### RelativeRectTween()

```dart
RelativeRectTween({dynamic begin, dynamic end})
```

Creates a [RelativeRect] tween.

The [begin] and [end] properties may be null; the null value is treated as [RelativeRect.fill].

### lerp()

```dart
RelativeRect lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# PositionedTransition

```dart
class PositionedTransition extends AnimatedWidget {}
```

Animated version of [Positioned] which takes a specific [Animation<RelativeRect>] to transition the child's position from a start position to an end position over the lifetime of the animation.

Only works if it's the child of a [Stack].

Here's an illustration of the [PositionedTransition] widget, with it's [rect] animated by a [CurvedAnimation] set to [Curves.elasticInOut]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/positioned_transition.mp4}

{@tool dartpad} The following code implements the [PositionedTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/positioned_transition.0.dart ** {@end-tool}

See also:

- [AnimatedPositioned], which transitions a child's position without taking an explicit [Animation] argument.
- [RelativePositionedTransition], a widget that transitions its child's position based on the value of a rectangle relative to a bounding box.
- [SlideTransition], a widget that animates the position of a widget relative to its normal position.
- [AlignTransition], an animated version of an [Align] that animates its [Align.alignment] property.
- [ScaleTransition], a widget that animates the scale of a transformed widget.
- [SizeTransition], a widget that animates its own size and clips and aligns its child.

### PositionedTransition()

```dart
PositionedTransition({dynamic key, required Animation<RelativeRect> rect, required Widget child})
```

Creates a transition for [Positioned].

### rect

```dart
Animation<RelativeRect> get rect
```

The animation that controls the child's size and position.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# RelativePositionedTransition

```dart
class RelativePositionedTransition extends AnimatedWidget {}
```

Animated version of [Positioned] which transitions the child's position based on the value of [rect] relative to a bounding box with the specified [size].

Only works if it's the child of a [Stack].

Here's an illustration of the [RelativePositionedTransition] widget, with it's [rect] animated by a [CurvedAnimation] set to [Curves.elasticInOut]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/relative_positioned_transition.mp4}

{@tool dartpad} The following code implements the [RelativePositionedTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/relative_positioned_transition.0.dart ** {@end-tool}

See also:

- [PositionedTransition], a widget that animates its child from a start position to an end position over the lifetime of the animation.
- [AlignTransition], an animated version of an [Align] that animates its [Align.alignment] property.
- [ScaleTransition], a widget that animates the scale of a transformed widget.
- [SizeTransition], a widget that animates its own size and clips and aligns its child.
- [SlideTransition], a widget that animates the position of a widget relative to its normal position.

### RelativePositionedTransition()

```dart
RelativePositionedTransition({dynamic key, required Animation<Rect?> rect, required Size size, required Widget child})
```

Create an animated version of [Positioned].

Each frame, the [Positioned] widget will be configured to represent the current value of the [rect] argument assuming that the stack has the given [size].

### rect

```dart
Animation<Rect?> get rect
```

The animation that controls the child's size and position.

If the animation returns a null [Rect], the rect is assumed to be [Rect.zero].

See also:

- [size], which gets the size of the box that the [Positioned] widget's offsets are relative to.

### size

```dart
Size size
```

The [Positioned] widget's offsets are relative to a box of this size whose origin is 0,0.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# DecoratedBoxTransition

```dart
class DecoratedBoxTransition extends AnimatedWidget {}
```

Animated version of a [DecoratedBox] that animates the different properties of its [Decoration].

Here's an illustration of the [DecoratedBoxTransition] widget, with it's [decoration] animated by a [CurvedAnimation] set to [Curves.decelerate]: {@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/decorated_box_transition.mp4}

{@tool dartpad} The following code implements the [DecoratedBoxTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/decorated_box_transition.0.dart ** {@end-tool}

See also:

- [DecoratedBox], which also draws a [Decoration] but is not animated.
- [AnimatedContainer], a more full-featured container that also animates on decoration using an internal animation.

### DecoratedBoxTransition()

```dart
DecoratedBoxTransition({dynamic key, required Animation<Decoration> decoration, DecorationPosition position = DecorationPosition.background, required Widget child})
```

Creates an animated [DecoratedBox] whose [Decoration] animation updates the widget.

See also:

- [DecoratedBox.new]

### decoration

```dart
Animation<Decoration> decoration
```

Animation of the decoration to paint.

Can be created using a [DecorationTween] interpolating typically between two [BoxDecoration].

### position

```dart
DecorationPosition position
```

Whether to paint the box decoration behind or in front of the child.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# AlignTransition

```dart
class AlignTransition extends AnimatedWidget {}
```

Animated version of an [Align] that animates its [Align.alignment] property.

Here's an illustration of the [DecoratedBoxTransition] widget, with it's [DecoratedBoxTransition.decoration] animated by a [CurvedAnimation] set to [Curves.decelerate]:

{@animation 300 378 https://flutter.github.io/assets-for-api-docs/assets/widgets/align_transition.mp4}

{@tool dartpad} The following code implements the [AlignTransition] as seen in the video above:

** See code in examples/api/lib/widgets/transitions/align_transition.0.dart ** {@end-tool}

See also:

- [AnimatedAlign], which animates changes to the [alignment] without taking an explicit [Animation] argument.
- [PositionedTransition], a widget that animates its child from a start position to an end position over the lifetime of the animation.
- [RelativePositionedTransition], a widget that transitions its child's position based on the value of a rectangle relative to a bounding box.
- [SizeTransition], a widget that animates its own size and clips and aligns its child.
- [SlideTransition], a widget that animates the position of a widget relative to its normal position.

### AlignTransition()

```dart
AlignTransition({dynamic key, required Animation<AlignmentGeometry> alignment, required Widget child, double? widthFactor, double? heightFactor})
```

Creates an animated [Align] whose [AlignmentGeometry] animation updates the widget.

See also:

- [Align.new].

### alignment

```dart
Animation<AlignmentGeometry> get alignment
```

The animation that controls the child's alignment.

### widthFactor

```dart
double? widthFactor
```

If non-null, the child's width factor, see [Align.widthFactor].

### heightFactor

```dart
double? heightFactor
```

If non-null, the child's height factor, see [Align.heightFactor].

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# DefaultTextStyleTransition

```dart
class DefaultTextStyleTransition extends AnimatedWidget {}
```

Animated version of a [DefaultTextStyle] that animates the different properties of its [TextStyle].

{@tool dartpad} The following code implements the [DefaultTextStyleTransition] that shows a transition between thick blue font and thin red font.

** See code in examples/api/lib/widgets/transitions/default_text_style_transition.0.dart ** {@end-tool}

See also:

- [AnimatedDefaultTextStyle], which animates changes in text style without taking an explicit [Animation] argument.
- [DefaultTextStyle], which also defines a [TextStyle] for its descendants but is not animated.

### DefaultTextStyleTransition()

```dart
DefaultTextStyleTransition({dynamic key, required Animation<TextStyle> style, required Widget child, TextAlign? textAlign, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, int? maxLines})
```

Creates an animated [DefaultTextStyle] whose [TextStyle] animation updates the widget.

### style

```dart
Animation<TextStyle> get style
```

The animation that controls the descendants' text style.

### textAlign

```dart
TextAlign? textAlign
```

How the text should be aligned horizontally.

### softWrap

```dart
bool softWrap
```

Whether the text should break at soft line breaks.

See [DefaultTextStyle.softWrap] for more details.

### overflow

```dart
TextOverflow overflow
```

How visual overflow should be handled.

### maxLines

```dart
int? maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary.

See [DefaultTextStyle.maxLines] for more details.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### build()

```dart
Widget build(BuildContext context)
```

# ListenableBuilder

```dart
class ListenableBuilder extends AnimatedWidget {}
```

A general-purpose widget for building a widget subtree when a [Listenable] changes.

[ListenableBuilder] is useful for more complex widgets that wish to listen to changes in other objects as part of a larger build function. To use [ListenableBuilder], construct the widget and pass it a [builder] function.

Any subtype of [Listenable] (such as a [ChangeNotifier], [ValueNotifier], or [Animation]) can be used with a [ListenableBuilder] to rebuild only certain parts of a widget when the [Listenable] notifies its listeners. Although they have identical implementations, if an [Animation] is being listened to, consider using an [AnimatedBuilder] instead for better readability.

{@tool dartpad} The following example uses a subclass of [ChangeNotifier] to hold the application model's state, in this case, a counter. A [ListenableBuilder] is then used to update the rendering (a [Text] widget) whenever the model changes.

** See code in examples/api/lib/widgets/transitions/listenable_builder.2.dart ** {@end-tool}

{@tool dartpad} This version is identical, but using a [ValueNotifier] instead of a dedicated subclass of [ChangeNotifier]. This works well when there is only a single immutable value to be tracked.

** See code in examples/api/lib/widgets/transitions/listenable_builder.1.dart ** {@end-tool}

## Performance optimizations

{@template flutter.widgets.transitions.ListenableBuilder.optimizations} If the [builder] function contains a subtree that does not depend on the [listenable], it is more efficient to build that subtree once instead of rebuilding it on every change of the [listenable].

Performance is therefore improved by specifying any widgets that don't need to change using the prebuilt [child] attribute. The [ListenableBuilder] passes this [child] back to the [builder] callback so that it can be incorporated into the build.

Using this pre-built [child] is entirely optional, but can improve performance significantly in some cases and is therefore a good practice. {@endtemplate}

{@tool dartpad} This example shows how a [ListenableBuilder] can be used to listen to a [FocusNode] (which is also a [ChangeNotifier]) to see when a subtree has focus, and modify a decoration when its focus state changes. Only the [Container] is rebuilt when the [FocusNode] changes; the rest of the tree (notably the [Focus] widget) remain unchanged from frame to frame.

** See code in examples/api/lib/widgets/transitions/listenable_builder.0.dart ** {@end-tool}

See also:

- [AnimatedBuilder], which has the same functionality, but is named more appropriately for a builder triggered by [Animation]s.
- [ValueListenableBuilder], which is specialized for [ValueNotifier]s and reports the new value in its builder callback.

### ListenableBuilder()

```dart
ListenableBuilder({dynamic key, required dynamic listenable, required TransitionBuilder builder, Widget? child})
```

Creates a builder that responds to changes in [listenable].

### listenable

```dart
Listenable get listenable
```

The [Listenable] supplied to the constructor.

{@tool dartpad} In this example, the [listenable] is a [ChangeNotifier] subclass that encapsulates a list. The [ListenableBuilder] is rebuilt each time an item is added to the list.

** See code in examples/api/lib/widgets/transitions/listenable_builder.3.dart ** {@end-tool}

See also:

- [AnimatedBuilder], a widget with identical functionality commonly used with [Animation] [Listenable]s for better readability.

### builder

```dart
TransitionBuilder builder
```

Called every time the [listenable] notifies about a change.

The child given to the builder should typically be part of the returned widget tree.

### child

```dart
Widget? child
```

The child widget to pass to the [builder].

{@macro flutter.widgets.transitions.ListenableBuilder.optimizations}

### build()

```dart
Widget build(BuildContext context)
```

# AnimatedBuilder

```dart
class AnimatedBuilder extends ListenableBuilder {}
```

A general-purpose widget for building animations.

[AnimatedBuilder] is useful for more complex widgets that wish to include an animation as part of a larger build function. To use [AnimatedBuilder], construct the widget and pass it a builder function.

For simple cases without additional state, consider using [AnimatedWidget].

{@youtube 560 315 https://www.youtube.com/watch?v=N-RiyZlv8v8}

Despite the name, [AnimatedBuilder] is not limited to [Animation]s, any subtype of [Listenable] (such as [ChangeNotifier] or [ValueNotifier]) can be used to trigger rebuilds. Although they have identical implementations, if an [Animation] is not being listened to, consider using a [ListenableBuilder] for better readability.

## Performance optimizations

{@template flutter.widgets.transitions.AnimatedBuilder.optimizations} If the [builder] function contains a subtree that does not depend on the animation passed to the constructor, it's more efficient to build that subtree once instead of rebuilding it on every animation tick.

If a pre-built subtree is passed as the [child] parameter, the [AnimatedBuilder] will pass it back to the [builder] function so that it can be incorporated into the build.

Using this pre-built child is entirely optional, but can improve performance significantly in some cases and is therefore a good practice. {@endtemplate}

{@tool dartpad} This code defines a widget that spins a green square continually. It is built with an [AnimatedBuilder] and makes use of the [child] feature to avoid having to rebuild the [Container] each time.

** See code in examples/api/lib/widgets/transitions/animated_builder.0.dart ** {@end-tool}

See also:

- [ListenableBuilder], a widget with similar functionality, but named more appropriately for a builder triggered on changes in [Listenable]s that aren't [Animation]s.
- [TweenAnimationBuilder], which animates a property to a target value without requiring manual management of an [AnimationController].

### AnimatedBuilder()

```dart
AnimatedBuilder({dynamic key, required Listenable animation, required Widget Function(BuildContext, Widget?) builder, Widget? child})
```

Creates an animated builder.

The [animation] and [builder] arguments are required.

### animation

```dart
Listenable get animation
```

The [Listenable] supplied to the constructor (typically an [Animation]).

Also accessible through the [listenable] getter.

See also:

- [ListenableBuilder], a widget with similar functionality commonly used with [Listenable]s (such as [ChangeNotifier]) for better readability when the [animation] isn't an [Animation].

### listenable

```dart
Listenable get listenable
```

The [Listenable] supplied to the constructor (typically an [Animation]).

Also accessible through the [animation] getter.

See also:

- [ListenableBuilder], a widget with identical functionality commonly used with non-animation [Listenable]s for readability.

### builder

```dart
TransitionBuilder get builder
```

Called every time the [animation] notifies about a change.

The child given to the builder should typically be part of the returned widget tree.
