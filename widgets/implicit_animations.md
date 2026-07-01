@docImport 'package:flutter/material.dart';

@docImport 'animated_cross_fade.dart'; @docImport 'animated_size.dart'; @docImport 'animated_switcher.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver.dart'; @docImport 'tween_animation_builder.dart';

# BoxConstraintsTween

```dart
class BoxConstraintsTween extends Tween<BoxConstraints> {}
```

An interpolation between two [BoxConstraints].

This class specializes the interpolation of [Tween<BoxConstraints>] to use [BoxConstraints.lerp].

See [Tween] for a discussion on how to use interpolation objects.

### BoxConstraintsTween()

```dart
BoxConstraintsTween({dynamic begin, dynamic end})
```

Creates a [BoxConstraints] tween.

The [begin] and [end] properties may be null; the null value is treated as a tight constraint of zero size.

### lerp()

```dart
BoxConstraints lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# DecorationTween

```dart
class DecorationTween extends Tween<Decoration> {}
```

An interpolation between two [Decoration]s.

This class specializes the interpolation of [Tween<BoxConstraints>] to use [Decoration.lerp].

For [ShapeDecoration]s which know how to [ShapeDecoration.lerpTo] or [ShapeDecoration.lerpFrom] each other, this will produce a smooth interpolation between decorations.

See also:

- [Tween] for a discussion on how to use interpolation objects.
- [ShapeDecoration], [RoundedRectangleBorder], [CircleBorder], and [StadiumBorder] for examples of shape borders that can be smoothly interpolated.
- [BoxBorder] for a border that can only be smoothly interpolated between other [BoxBorder]s.

### DecorationTween()

```dart
DecorationTween({dynamic begin, dynamic end})
```

Creates a decoration tween.

The [begin] and [end] properties may be null. If both are null, then the result is always null. If [end] is not null, then its lerping logic is used (via [Decoration.lerpTo]). Otherwise, [begin]'s lerping logic is used (via [Decoration.lerpFrom]).

### lerp()

```dart
Decoration lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# EdgeInsetsTween

```dart
class EdgeInsetsTween extends Tween<EdgeInsets> {}
```

An interpolation between two [EdgeInsets]s.

This class specializes the interpolation of [Tween<EdgeInsets>] to use [EdgeInsets.lerp].

See [Tween] for a discussion on how to use interpolation objects.

See also:

- [EdgeInsetsGeometryTween], which interpolates between two [EdgeInsetsGeometry] objects.

### EdgeInsetsTween()

```dart
EdgeInsetsTween({dynamic begin, dynamic end})
```

Creates an [EdgeInsets] tween.

The [begin] and [end] properties may be null; the null value is treated as an [EdgeInsets] with no inset.

### lerp()

```dart
EdgeInsets lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# EdgeInsetsGeometryTween

```dart
class EdgeInsetsGeometryTween extends Tween<EdgeInsetsGeometry> {}
```

An interpolation between two [EdgeInsetsGeometry]s.

This class specializes the interpolation of [Tween<EdgeInsetsGeometry>] to use [EdgeInsetsGeometry.lerp].

See [Tween] for a discussion on how to use interpolation objects.

See also:

- [EdgeInsetsTween], which interpolates between two [EdgeInsets] objects.

### EdgeInsetsGeometryTween()

```dart
EdgeInsetsGeometryTween({dynamic begin, dynamic end})
```

Creates an [EdgeInsetsGeometry] tween.

The [begin] and [end] properties may be null; the null value is treated as an [EdgeInsetsGeometry] with no inset.

### lerp()

```dart
EdgeInsetsGeometry lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# BorderRadiusTween

```dart
class BorderRadiusTween extends Tween<BorderRadius?> {}
```

An interpolation between two [BorderRadius]s.

This class specializes the interpolation of [Tween<BorderRadius>] to use [BorderRadius.lerp].

See [Tween] for a discussion on how to use interpolation objects.

### BorderRadiusTween()

```dart
BorderRadiusTween({dynamic begin, dynamic end})
```

Creates a [BorderRadius] tween.

The [begin] and [end] properties may be null; the null value is treated as a right angle (no radius).

### lerp()

```dart
BorderRadius? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# BorderTween

```dart
class BorderTween extends Tween<Border?> {}
```

An interpolation between two [Border]s.

This class specializes the interpolation of [Tween<Border>] to use [Border.lerp].

See [Tween] for a discussion on how to use interpolation objects.

### BorderTween()

```dart
BorderTween({dynamic begin, dynamic end})
```

Creates a [Border] tween.

The [begin] and [end] properties may be null; the null value is treated as having no border.

### lerp()

```dart
Border? lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# Matrix4Tween

```dart
class Matrix4Tween extends Tween<Matrix4> {}
```

An interpolation between two [Matrix4]s.

This class specializes the interpolation of [Tween<Matrix4>] to be appropriate for transformation matrices.

Currently this class works only for translations.

See [Tween] for a discussion on how to use interpolation objects.

### Matrix4Tween()

```dart
Matrix4Tween({dynamic begin, dynamic end})
```

Creates a [Matrix4] tween.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### lerp()

```dart
Matrix4 lerp(double t)
```

# TextStyleTween

```dart
class TextStyleTween extends Tween<TextStyle> {}
```

An interpolation between two [TextStyle]s.

This class specializes the interpolation of [Tween<TextStyle>] to use [TextStyle.lerp].

This will not work well if the styles don't set the same fields.

See [Tween] for a discussion on how to use interpolation objects.

### TextStyleTween()

```dart
TextStyleTween({dynamic begin, dynamic end})
```

Creates a text style tween.

The [begin] and [end] properties must be non-null before the tween is first used, but the arguments can be null if the values are going to be filled in later.

### lerp()

```dart
TextStyle lerp(double t)
```

Returns the value this variable has at the given animation clock value.

# ImplicitlyAnimatedWidget

```dart
abstract class ImplicitlyAnimatedWidget extends StatefulWidget {}
```

An abstract class for building widgets that animate changes to their properties.

Widgets of this type will not animate when they are first added to the widget tree. Rather, when they are rebuilt with different values, they will respond to those _changes_ by animating the changes over a specified [duration].

Which properties are animated is left up to the subclass. Subclasses' [State]s must extend [ImplicitlyAnimatedWidgetState] and provide a way to visit the relevant fields to animate.

## Relationship to [AnimatedWidget]s

[ImplicitlyAnimatedWidget]s (and their subclasses) automatically animate changes in their properties whenever they change. For this, they create and manage their own internal [AnimationController]s to power the animation. While these widgets are simple to use and don't require you to manually manage the lifecycle of an [AnimationController], they are also somewhat limited: Besides the target value for the animated property, developers can only choose a [duration] and [curve] for the animation. If you require more control over the animation (e.g. you want to stop it somewhere in the middle), consider using an [AnimatedWidget] or one of its subclasses. These widgets take an [Animation] as an argument to power the animation. This gives the developer full control over the animation at the cost of requiring you to manually manage the underlying [AnimationController].

## Common implicitly animated widgets

A number of implicitly animated widgets ship with the framework. They are usually named `AnimatedFoo`, where `Foo` is the name of the non-animated version of that widget. Commonly used implicitly animated widgets include:

- [TweenAnimationBuilder], which animates any property expressed by a [Tween] to a specified target value.
- [AnimatedAlign], which is an implicitly animated version of [Align].
- [AnimatedContainer], which is an implicitly animated version of [Container].
- [AnimatedDefaultTextStyle], which is an implicitly animated version of [DefaultTextStyle].
- [AnimatedScale], which is an implicitly animated version of [Transform.scale].
- [AnimatedRotation], which is an implicitly animated version of [Transform.rotate].
- [AnimatedSlide], which implicitly animates the position of a widget relative to its normal position.
- [AnimatedOpacity], which is an implicitly animated version of [Opacity].
- [AnimatedPadding], which is an implicitly animated version of [Padding].
- [AnimatedPhysicalModel], which is an implicitly animated version of [PhysicalModel].
- [AnimatedPositioned], which is an implicitly animated version of [Positioned].
- [AnimatedPositionedDirectional], which is an implicitly animated version of [PositionedDirectional].
- [AnimatedTheme], which is an implicitly animated version of [Theme].
- [AnimatedCrossFade], which cross-fades between two given children and animates itself between their sizes.
- [AnimatedSize], which automatically transitions its size over a given duration.
- [AnimatedSwitcher], which fades from one widget to another.

### ImplicitlyAnimatedWidget()

```dart
ImplicitlyAnimatedWidget({dynamic key, Curve curve = Curves.linear, required Duration duration, VoidCallback? onEnd})
```

Initializes fields for subclasses.

### curve

```dart
Curve curve
```

The curve to apply when animating the parameters of this container.

### duration

```dart
Duration duration
```

The duration over which to animate the parameters of this container.

### onEnd

```dart
VoidCallback? onEnd
```

Called every time an animation completes.

This can be useful to trigger additional actions (e.g. another animation) at the end of the current animation.

### createState()

```dart
ImplicitlyAnimatedWidgetState<ImplicitlyAnimatedWidget> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TweenConstructor

```dart
typedef TweenConstructor<T extends Object> = Tween<T> Function(T targetValue)
```

Signature for a [Tween] factory.

This is the type of one of the arguments of [TweenVisitor], the signature used by [AnimatedWidgetBaseState.forEachTween].

Instances of this function are expected to take a value and return a tween beginning at that value.

# TweenVisitor

```dart
typedef TweenVisitor<T extends Object> = Tween<T>? Function(Tween<T>? tween, T targetValue, TweenConstructor<T> constructor)
```

Signature for callbacks passed to [ImplicitlyAnimatedWidgetState.forEachTween].

{@template flutter.widgets.TweenVisitor.arguments} The `tween` argument should contain the current tween value. This will initially be null when the state is first initialized.

The `targetValue` argument should contain the value toward which the state is animating. For instance, if the state is animating its widget's opacity value, then this argument should contain the widget's current opacity value.

The `constructor` argument should contain a function that takes a value (the widget's value being animated) and returns a tween beginning at that value.

{@endtemplate}

`forEachTween()` is expected to update its tween value to the return value of this visitor.

The `<T>` parameter specifies the type of value that's being animated.

# ImplicitlyAnimatedWidgetState

```dart
abstract class ImplicitlyAnimatedWidgetState<T extends ImplicitlyAnimatedWidget> extends State<T> with SingleTickerProviderStateMixin<T> {}
```

A base class for the `State` of widgets with implicit animations.

[ImplicitlyAnimatedWidgetState] requires that subclasses respond to the animation themselves. If you would like `setState()` to be called automatically as the animation changes, use [AnimatedWidgetBaseState].

Properties that subclasses choose to animate are represented by [Tween] instances. Subclasses must implement the [forEachTween] method to allow [ImplicitlyAnimatedWidgetState] to iterate through the widget's fields and animate them.

### controller

```dart
AnimationController controller
```

The animation controller driving this widget's implicit animations.

### animation

```dart
Animation<double> get animation
```

The animation driving this widget's implicit animations.

### initState()

```dart
void initState()
```

### didUpdateWidget()

```dart
void didUpdateWidget(T oldWidget)
```

### dispose()

```dart
void dispose()
```

### forEachTween()

```dart
void forEachTween(TweenVisitor<dynamic> visitor)
```

Visits each tween controlled by this state with the specified `visitor` function.

### Subclass responsibility

Properties to be animated are represented by [Tween] member variables in the state. For each such tween, [forEachTween] implementations are expected to call `visitor` with the appropriate arguments and store the result back into the member variable. The arguments to `visitor` are as follows:

{@macro flutter.widgets.TweenVisitor.arguments}

### When this method will be called

[forEachTween] is initially called during [initState]. It is expected that the visitor's `tween` argument will be set to null, causing the visitor to call its `constructor` argument to construct the tween for the first time. The resulting tween will have its `begin` value set to the target value and will have its `end` value set to null. The animation will not be started.

When this state's [widget] is updated (thus triggering the [didUpdateWidget] method to be called), [forEachTween] will be called again to check if the target value has changed. If the target value has changed, signaling that the [animation] should start, then the visitor will update the tween's `start` and `end` values accordingly, and the animation will be started.

### Other member variables

Subclasses that contain properties based on tweens created by [forEachTween] should override [didUpdateTweens] to update those properties. Dependent properties should not be updated within [forEachTween].

{@tool snippet}

This sample implements an implicitly animated widget's `State`. The widget animates between colors whenever `widget.targetColor` changes.

```dart
class MyWidgetState extends AnimatedWidgetBaseState<MyWidget> {
  ColorTween? _colorTween;

  @override
  Widget build(BuildContext context) {
    return Text(
      'Hello World',
      // Computes the value of the text color at any given time.
      style: TextStyle(color: _colorTween?.evaluate(animation)),
    );
  }

  @override
  void forEachTween(TweenVisitor<dynamic> visitor) {
    // Update the tween using the provided visitor function.
    _colorTween = visitor(
      // The latest tween value. Can be `null`.
      _colorTween,
      // The color value toward which we are animating.
      widget.targetColor,
      // A function that takes a color value and returns a tween
      // beginning at that value.
      (dynamic value) => ColorTween(begin: value as Color?),
    ) as ColorTween?;

    // We could have more tweens than one by using the visitor
    // multiple times.
  }
}
```

{@end-tool}

### didUpdateTweens()

```dart
void didUpdateTweens()
```

Optional hook for subclasses that runs after all tweens have been updated via [forEachTween].

Any properties that depend upon tweens created by [forEachTween] should be updated within [didUpdateTweens], not within [forEachTween].

This method will be called both:

1.  After the tweens are _initially_ constructed (by the `constructor` argument to the [TweenVisitor] that's passed to [forEachTween]). In this case, the tweens are likely to contain only a [Tween.begin] value and not a [Tween.end].

2.  When the state's [widget] is updated, and one or more of the tweens visited by [forEachTween] specifies a target value that's different than the widget's current value, thus signaling that the [animation] should run. In this case, the [Tween.begin] value for each tween will an evaluation of the tween against the current [animation], and the [Tween.end] value for each tween will be the target value.

# AnimatedWidgetBaseState

```dart
abstract class AnimatedWidgetBaseState<T extends ImplicitlyAnimatedWidget> extends ImplicitlyAnimatedWidgetState<T> {}
```

A base class for widgets with implicit animations that need to rebuild their widget tree as the animation runs.

This class calls [build] each frame that the animation ticks. For a variant that does not rebuild each frame, consider subclassing [ImplicitlyAnimatedWidgetState] directly.

Subclasses must implement the [forEachTween] method to allow [AnimatedWidgetBaseState] to iterate through the subclasses' widget's fields and animate them.

### initState()

```dart
void initState()
```

# AnimatedContainer

```dart
class AnimatedContainer extends ImplicitlyAnimatedWidget {}
```

Animated version of [Container] that gradually changes its values over a period of time.

The [AnimatedContainer] will automatically animate between the old and new values of properties when they change using the provided curve and duration. Properties that are null are not animated. Its child and descendants are not animated.

This class is useful for generating simple implicit transitions between different parameters to [Container] with its internal [AnimationController]. For more complex animations, you'll likely want to use a subclass of [AnimatedWidget] such as the [DecoratedBoxTransition] or use your own [AnimationController].

{@youtube 560 315 https://www.youtube.com/watch?v=yI-8QHpGIP4}

{@tool dartpad} The following example (depicted above) transitions an AnimatedContainer between two states. It adjusts the `height`, `width`, `color`, and [alignment] properties when tapped.

** See code in examples/api/lib/widgets/implicit_animations/animated_container.0.dart ** {@end-tool}

See also:

- [AnimatedPadding], which is a subset of this widget that only supports animating the [padding].
- The [catalog of layout widgets](https://flutter.dev/widgets/layout/).
- [AnimatedPositioned], which, as a child of a [Stack], automatically transitions its child's position over a given duration whenever the given position changes.
- [AnimatedAlign], which automatically transitions its child's position over a given duration whenever the given [AnimatedAlign.alignment] changes.
- [AnimatedSwitcher], which switches out a child for a new one with a customizable transition.
- [AnimatedCrossFade], which fades between two children and interpolates their sizes.

### AnimatedContainer()

```dart
AnimatedContainer({dynamic key, AlignmentGeometry? alignment, EdgeInsetsGeometry? padding, Color? color, Decoration? decoration, Decoration? foregroundDecoration, double? width, double? height, BoxConstraints? constraints, EdgeInsetsGeometry? margin, Matrix4? transform, AlignmentGeometry? transformAlignment, Widget? child, Clip clipBehavior = Clip.none, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a container that animates its parameters implicitly.

### child

```dart
Widget? child
```

The [child] contained by the container.

If null, and if the [constraints] are unbounded or also null, the container will expand to fill all available space in its parent, unless the parent provides unbounded constraints, in which case the container will attempt to be as small as possible.

{@macro flutter.widgets.ProxyWidget.child}

### alignment

```dart
AlignmentGeometry? alignment
```

Align the [child] within the container.

If non-null, the container will expand to fill its parent and position its child within itself according to the given value. If the incoming constraints are unbounded, then the child will be shrink-wrapped instead.

Ignored if [child] is null.

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### padding

```dart
EdgeInsetsGeometry? padding
```

Empty space to inscribe inside the [decoration]. The [child], if any, is placed inside this padding.

### decoration

```dart
Decoration? decoration
```

The decoration to paint behind the [child].

A shorthand for specifying just a solid color is available in the constructor: set the `color` argument instead of the `decoration` argument.

### foregroundDecoration

```dart
Decoration? foregroundDecoration
```

The decoration to paint in front of the child.

### constraints

```dart
BoxConstraints? constraints
```

Additional constraints to apply to the child.

The constructor `width` and `height` arguments are combined with the `constraints` argument to set this property.

The [padding] goes inside the constraints.

### margin

```dart
EdgeInsetsGeometry? margin
```

Empty space to surround the [decoration] and [child].

### transform

```dart
Matrix4? transform
```

The transformation matrix to apply before painting the container.

### transformAlignment

```dart
AlignmentGeometry? transformAlignment
```

The alignment of the origin, relative to the size of the container, if [transform] is specified.

When [transform] is null, the value of this property is ignored.

See also:

- [Transform.alignment], which is set by this property.

### clipBehavior

```dart
Clip clipBehavior
```

The clip behavior when [AnimatedContainer.decoration] is not null.

Defaults to [Clip.none]. Must be [Clip.none] if [decoration] is null.

Unlike other properties of [AnimatedContainer], changes to this property apply immediately and have no animation.

If a clip is to be applied, the [Decoration.getClipPath] method for the provided decoration must return a clip path. (This is not supported by all decorations; the default implementation of that method throws an [UnsupportedError].)

### createState()

```dart
AnimatedWidgetBaseState<AnimatedContainer> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPadding

```dart
class AnimatedPadding extends ImplicitlyAnimatedWidget {}
```

Animated version of [Padding] which automatically transitions the indentation over a given duration whenever the given inset changes.

{@youtube 560 315 https://www.youtube.com/watch?v=PY2m0fhGNz4}

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_padding.mp4}

{@tool dartpad} The following code implements the [AnimatedPadding] widget, using a [curve] of [Curves.easeInOut].

** See code in examples/api/lib/widgets/implicit_animations/animated_padding.0.dart ** {@end-tool}

See also:

- [AnimatedContainer], which can transition more values at once.
- [AnimatedAlign], which automatically transitions its child's position over a given duration whenever the given [AnimatedAlign.alignment] changes.

### AnimatedPadding()

```dart
AnimatedPadding({dynamic key, required EdgeInsetsGeometry padding, Widget? child, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that insets its child by a value that animates implicitly.

### padding

```dart
EdgeInsetsGeometry padding
```

The amount of space by which to inset the child.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPadding> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedAlign

```dart
class AnimatedAlign extends ImplicitlyAnimatedWidget {}
```

Animated version of [Align] which automatically transitions the child's position over a given duration whenever the given [alignment] changes.

Here's an illustration of what this can look like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_align.mp4}

For the animation, you can choose a [curve] as well as a [duration] and the widget will automatically animate to the new target [alignment]. If you require more control over the animation (e.g. if you want to stop it mid-animation), consider using an [AlignTransition] instead, which takes a provided [Animation] as argument. While that allows you to fine-tune the animation, it also requires more development overhead as you have to manually manage the lifecycle of the underlying [AnimationController].

{@tool dartpad} The following code implements the [AnimatedAlign] widget, using a [curve] of [Curves.fastOutSlowIn].

** See code in examples/api/lib/widgets/implicit_animations/animated_align.0.dart ** {@end-tool}

See also:

- [AnimatedContainer], which can transition more values at once.
- [AnimatedPadding], which can animate the padding instead of the alignment.
- [AnimatedSlide], which can animate the translation of child by a given offset relative to its size.
- [AnimatedPositioned], which, as a child of a [Stack], automatically transitions its child's position over a given duration whenever the given position changes.

### AnimatedAlign()

```dart
AnimatedAlign({dynamic key, required AlignmentGeometry alignment, Widget? child, double? heightFactor, double? widthFactor, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that positions its child by an alignment that animates implicitly.

### alignment

```dart
AlignmentGeometry alignment
```

How to align the child.

The x and y values of the [Alignment] control the horizontal and vertical alignment, respectively. An x value of -1.0 means that the left edge of the child is aligned with the left edge of the parent whereas an x value of 1.0 means that the right edge of the child is aligned with the right edge of the parent. Other values interpolate (and extrapolate) linearly. For example, a value of 0.0 means that the center of the child is aligned with the center of the parent.

See also:

- [Alignment], which has more details and some convenience constants for common positions.
- [AlignmentDirectional], which has a horizontal coordinate orientation that depends on the [TextDirection].

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### heightFactor

```dart
double? heightFactor
```

If non-null, sets its height to the child's height multiplied by this factor.

Must be greater than or equal to 0.0, defaults to null.

### widthFactor

```dart
double? widthFactor
```

If non-null, sets its width to the child's width multiplied by this factor.

Must be greater than or equal to 0.0, defaults to null.

### createState()

```dart
AnimatedWidgetBaseState<AnimatedAlign> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPositioned

```dart
class AnimatedPositioned extends ImplicitlyAnimatedWidget {}
```

Animated version of [Positioned] which automatically transitions the child's position over a given duration whenever the given position changes.

{@youtube 560 315 https://www.youtube.com/watch?v=hC3s2YdtWt8}

Only works if it's the child of a [Stack].

This widget is a good choice if the _size_ of the child would end up changing as a result of this animation. If the size is intended to remain the same, with only the _position_ changing over time, then consider [SlideTransition] instead. [SlideTransition] only triggers a repaint each frame of the animation, whereas [AnimatedPositioned] will trigger a relayout as well.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_positioned.mp4}

For the animation, you can choose a [curve] as well as a [duration] and the widget will automatically animate to the new target position. If you require more control over the animation (e.g. if you want to stop it mid-animation), consider using a [PositionedTransition] instead, which takes a provided [Animation] as an argument. While that allows you to fine-tune the animation, it also requires more development overhead as you have to manually manage the lifecycle of the underlying [AnimationController].

{@tool dartpad} The following example transitions an AnimatedPositioned between two states. It adjusts the `height`, `width`, and [Positioned] properties when tapped.

** See code in examples/api/lib/widgets/implicit_animations/animated_positioned.0.dart ** {@end-tool}

See also:

- [AnimatedPositionedDirectional], which adapts to the ambient [Directionality] (the same as this widget, but for animating [PositionedDirectional]).

### AnimatedPositioned()

```dart
AnimatedPositioned({dynamic key, required Widget child, double? left, double? top, double? right, double? bottom, double? width, double? height, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates its position implicitly.

Only two out of the three horizontal values ([left], [right], [width]), and only two out of the three vertical values ([top], [bottom], [height]), can be set. In each case, at least one of the three must be null.

### AnimatedPositioned.fromRect()

```dart
AnimatedPositioned.fromRect({dynamic key, required Widget child, required Rect rect, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates the rectangle it occupies implicitly.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### left

```dart
double? left
```

The offset of the child's left edge from the left of the stack.

### top

```dart
double? top
```

The offset of the child's top edge from the top of the stack.

### right

```dart
double? right
```

The offset of the child's right edge from the right of the stack.

### bottom

```dart
double? bottom
```

The offset of the child's bottom edge from the bottom of the stack.

### width

```dart
double? width
```

The child's width.

Only two out of the three horizontal values ([left], [right], [width]) can be set. The third must be null.

### height

```dart
double? height
```

The child's height.

Only two out of the three vertical values ([top], [bottom], [height]) can be set. The third must be null.

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPositioned> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPositionedDirectional

```dart
class AnimatedPositionedDirectional extends ImplicitlyAnimatedWidget {}
```

Animated version of [PositionedDirectional] which automatically transitions the child's position over a given duration whenever the given position changes.

The ambient [Directionality] is used to determine whether [start] is to the left or to the right.

Only works if it's the child of a [Stack].

This widget is a good choice if the _size_ of the child would end up changing as a result of this animation. If the size is intended to remain the same, with only the _position_ changing over time, then consider [SlideTransition] instead. [SlideTransition] only triggers a repaint each frame of the animation, whereas [AnimatedPositionedDirectional] will trigger a relayout as well. ([SlideTransition] is also text-direction-aware.)

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_positioned_directional.mp4}

See also:

- [AnimatedPositioned], which specifies the widget's position visually (the same as this widget, but for animating [Positioned]).

### AnimatedPositionedDirectional()

```dart
AnimatedPositionedDirectional({dynamic key, required Widget child, double? start, double? top, double? end, double? bottom, double? width, double? height, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates its position implicitly.

Only two out of the three horizontal values ([start], [end], [width]), and only two out of the three vertical values ([top], [bottom], [height]), can be set. In each case, at least one of the three must be null.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### start

```dart
double? start
```

The offset of the child's start edge from the start of the stack.

### top

```dart
double? top
```

The offset of the child's top edge from the top of the stack.

### end

```dart
double? end
```

The offset of the child's end edge from the end of the stack.

### bottom

```dart
double? bottom
```

The offset of the child's bottom edge from the bottom of the stack.

### width

```dart
double? width
```

The child's width.

Only two out of the three horizontal values ([start], [end], [width]) can be set. The third must be null.

### height

```dart
double? height
```

The child's height.

Only two out of the three vertical values ([top], [bottom], [height]) can be set. The third must be null.

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPositionedDirectional> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedScale

```dart
class AnimatedScale extends ImplicitlyAnimatedWidget {}
```

Animated version of [Transform.scale] which automatically transitions the child's scale over a given duration whenever the given scale changes.

{@tool snippet}

This code defines a widget that uses [AnimatedScale] to change the size of [FlutterLogo] gradually to a new scale whenever the button is pressed.

```dart
class LogoScale extends StatefulWidget {
  const LogoScale({super.key});

  @override
  State<LogoScale> createState() => LogoScaleState();
}

class LogoScaleState extends State<LogoScale> {
  double scale = 1.0;

  void _changeScale() {
    setState(() => scale = scale == 1.0 ? 3.0 : 1.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ElevatedButton(
          onPressed: _changeScale,
          child: const Text('Scale Logo'),
        ),
        Padding(
          padding: const EdgeInsets.all(50),
          child: AnimatedScale(
            scale: scale,
            duration: const Duration(seconds: 2),
            child: const FlutterLogo(),
          ),
        ),
      ],
    );
  }
}
```

{@end-tool}

See also:

- [AnimatedRotation], for animating the rotation of a child.
- [AnimatedSize], for animating the resize of a child based on changes in layout.
- [AnimatedSlide], for animating the translation of a child by a given offset relative to its size.
- [ScaleTransition], an explicitly animated version of this widget, where an [Animation] is provided by the caller instead of being built in.

### AnimatedScale()

```dart
AnimatedScale({dynamic key, Widget? child, required double scale, Alignment alignment = Alignment.center, FilterQuality? filterQuality, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates its scale implicitly.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### scale

```dart
double scale
```

The target scale.

### alignment

```dart
Alignment alignment
```

The alignment of the origin of the coordinate system in which the scale takes place, relative to the size of the box.

For example, to set the origin of the scale to bottom middle, you can use an alignment of (0.0, 1.0).

### filterQuality

```dart
FilterQuality? filterQuality
```

The filter quality with which to apply the transform as a bitmap operation.

{@macro flutter.widgets.Transform.optional.FilterQuality}

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedScale> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedRotation

```dart
class AnimatedRotation extends ImplicitlyAnimatedWidget {}
```

Animated version of [Transform.rotate] which automatically transitions the child's rotation over a given duration whenever the given rotation changes.

{@tool snippet}

This code defines a widget that uses [AnimatedRotation] to rotate a [FlutterLogo] gradually by an eighth of a turn (45 degrees) with each press of the button.

```dart
class LogoRotate extends StatefulWidget {
  const LogoRotate({super.key});

  @override
  State<LogoRotate> createState() => LogoRotateState();
}

class LogoRotateState extends State<LogoRotate> {
  double turns = 0.0;

  void _changeRotation() {
    setState(() => turns += 1.0 / 8.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ElevatedButton(
          onPressed: _changeRotation,
          child: const Text('Rotate Logo'),
        ),
        Padding(
          padding: const EdgeInsets.all(50),
          child: AnimatedRotation(
            turns: turns,
            duration: const Duration(seconds: 1),
            child: const FlutterLogo(),
          ),
        ),
      ],
    );
  }
}
```

{@end-tool}

See also:

- [AnimatedScale], for animating the scale of a child.
- [RotationTransition], an explicitly animated version of this widget, where an [Animation] is provided by the caller instead of being built in.

### AnimatedRotation()

```dart
AnimatedRotation({dynamic key, Widget? child, required double turns, Alignment alignment = Alignment.center, FilterQuality? filterQuality, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates its rotation implicitly.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### turns

```dart
double turns
```

The animation that controls the rotation of the child.

If the current value of the turns animation is v, the child will be rotated v * 2 * pi radians before being painted.

### alignment

```dart
Alignment alignment
```

The alignment of the origin of the coordinate system in which the rotation takes place, relative to the size of the box.

For example, to set the origin of the rotation to bottom middle, you can use an alignment of (0.0, 1.0).

### filterQuality

```dart
FilterQuality? filterQuality
```

The filter quality with which to apply the transform as a bitmap operation.

{@macro flutter.widgets.Transform.optional.FilterQuality}

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedRotation> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedSlide

```dart
class AnimatedSlide extends ImplicitlyAnimatedWidget {}
```

Widget which automatically transitions the child's offset relative to its normal position whenever the given offset changes.

The translation is expressed as an [Offset] scaled to the child's size. For example, an [Offset] with a `dx` of 0.25 will result in a horizontal translation of one quarter the width of the child.

{@tool dartpad} This code defines a widget that uses [AnimatedSlide] to translate a [FlutterLogo] up or down and right or left by dragging the X and Y axis sliders.

** See code in examples/api/lib/widgets/implicit_animations/animated_slide.0.dart ** {@end-tool}

See also:

- [AnimatedPositioned], which, as a child of a [Stack], automatically transitions its child's position over a given duration whenever the given position changes.
- [AnimatedAlign], which automatically transitions its child's position over a given duration whenever the given [AnimatedAlign.alignment] changes.

### AnimatedSlide()

```dart
AnimatedSlide({dynamic key, Widget? child, required Offset offset, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates its offset translation implicitly.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### offset

```dart
Offset offset
```

The target offset. The child will be translated horizontally by `width * dx` and vertically by `height * dy`

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedSlide> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedOpacity

```dart
class AnimatedOpacity extends ImplicitlyAnimatedWidget {}
```

Animated version of [Opacity] which automatically transitions the child's opacity over a given duration whenever the given opacity changes.

{@youtube 560 315 https://www.youtube.com/watch?v=QZAvjqOqiLY}

Animating an opacity is relatively expensive because it requires painting the child into an intermediate buffer.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_opacity.mp4}

{@tool snippet}

```dart
class LogoFade extends StatefulWidget {
  const LogoFade({super.key});

  @override
  State<LogoFade> createState() => LogoFadeState();
}

class LogoFadeState extends State<LogoFade> {
  double opacityLevel = 1.0;

  void _changeOpacity() {
    setState(() => opacityLevel = opacityLevel == 0 ? 1.0 : 0.0);
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        AnimatedOpacity(
          opacity: opacityLevel,
          duration: const Duration(seconds: 3),
          child: const FlutterLogo(),
        ),
        ElevatedButton(
          onPressed: _changeOpacity,
          child: const Text('Fade Logo'),
        ),
      ],
    );
  }
}
```

{@end-tool}

## Hit testing

Setting the [opacity] to zero does not prevent hit testing from being applied to the descendants of the [AnimatedOpacity] widget. This can be confusing for the user, who may not see anything, and may believe the area of the interface where the [AnimatedOpacity] is hiding a widget to be non-interactive.

With certain widgets, such as [Flow], that compute their positions only when they are painted, this can actually lead to bugs (from unexpected geometry to exceptions), because those widgets are not painted by the [AnimatedOpacity] widget at all when the [opacity] animation reaches zero.

To avoid such problems, it is generally a good idea to use an [IgnorePointer] widget when setting the [opacity] to zero. This prevents interactions with any children in the subtree when the [child] is animating away.

See also:

- [AnimatedCrossFade], for fading between two children.
- [AnimatedSwitcher], for fading between many children in sequence.
- [FadeTransition], an explicitly animated version of this widget, where an [Animation] is provided by the caller instead of being built in.
- [SliverAnimatedOpacity], for automatically transitioning a _sliver's_ opacity over a given duration whenever the given opacity changes.

### AnimatedOpacity()

```dart
AnimatedOpacity({dynamic key, Widget? child, required double opacity, dynamic curve, required Duration duration, dynamic onEnd, bool alwaysIncludeSemantics = false})
```

Creates a widget that animates its opacity implicitly.

The [opacity] argument must be between zero and one, inclusive.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### opacity

```dart
double opacity
```

The target opacity.

An opacity of 1.0 is fully opaque. An opacity of 0.0 is fully transparent (i.e., invisible).

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

Whether the semantic information of the children is always included.

Defaults to false.

When true, regardless of the opacity settings the child semantic information is exposed as if the widget were fully visible. This is useful in cases where labels may be hidden during animations that would otherwise contribute relevant semantics.

### createState()

```dart
ImplicitlyAnimatedWidgetState<AnimatedOpacity> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverAnimatedOpacity

```dart
class SliverAnimatedOpacity extends ImplicitlyAnimatedWidget {}
```

Animated version of [SliverOpacity] which automatically transitions the sliver child's opacity over a given duration whenever the given opacity changes.

Animating an opacity is relatively expensive because it requires painting the sliver child into an intermediate buffer.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn].

{@tool dartpad} Creates a [CustomScrollView] with a [SliverFixedExtentList] and a [FloatingActionButton]. Pressing the button animates the lists' opacity.

** See code in examples/api/lib/widgets/implicit_animations/sliver_animated_opacity.0.dart ** {@end-tool}

## Hit testing

Setting the [opacity] to zero does not prevent hit testing from being applied to the descendants of the [SliverAnimatedOpacity] widget. This can be confusing for the user, who may not see anything, and may believe the area of the interface where the [SliverAnimatedOpacity] is hiding a widget to be non-interactive.

With certain widgets, such as [Flow], that compute their positions only when they are painted, this can actually lead to bugs (from unexpected geometry to exceptions), because those widgets are not painted by the [SliverAnimatedOpacity] widget at all when the [opacity] animation reaches zero.

To avoid such problems, it is generally a good idea to use a [SliverIgnorePointer] widget when setting the [opacity] to zero. This prevents interactions with any children in the subtree when the [sliver] is animating away.

See also:

- [SliverFadeTransition], an explicitly animated version of this widget, where an [Animation] is provided by the caller instead of being built in.
- [AnimatedOpacity], for automatically transitioning a box child's opacity over a given duration whenever the given opacity changes.

### SliverAnimatedOpacity()

```dart
SliverAnimatedOpacity({dynamic key, Widget? sliver, required double opacity, dynamic curve, required Duration duration, dynamic onEnd, bool alwaysIncludeSemantics = false})
```

Creates a widget that animates its opacity implicitly.

The [opacity] argument must be between zero and one, inclusive.

### sliver

```dart
Widget? sliver
```

The sliver below this widget in the tree.

### opacity

```dart
double opacity
```

The target opacity.

An opacity of 1.0 is fully opaque. An opacity of 0.0 is fully transparent (i.e., invisible).

### alwaysIncludeSemantics

```dart
bool alwaysIncludeSemantics
```

Whether the semantic information of the children is always included.

Defaults to false.

When true, regardless of the opacity settings the sliver child's semantic information is exposed as if the widget were fully visible. This is useful in cases where labels may be hidden during animations that would otherwise contribute relevant semantics.

### createState()

```dart
ImplicitlyAnimatedWidgetState<SliverAnimatedOpacity> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedDefaultTextStyle

```dart
class AnimatedDefaultTextStyle extends ImplicitlyAnimatedWidget {}
```

Animated version of [DefaultTextStyle] which automatically transitions the default text style (the text style to apply to descendant [Text] widgets without explicit style) over a given duration whenever the given style changes.

The [textAlign], [softWrap], [overflow], [maxLines], [textWidthBasis] and [textHeightBehavior] properties are not animated and take effect immediately when changed.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.elasticInOut]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_default_text_style.mp4}

For the animation, you can choose a [curve] as well as a [duration] and the widget will automatically animate to the new default text style. If you require more control over the animation (e.g. if you want to stop it mid-animation), consider using a [DefaultTextStyleTransition] instead, which takes a provided [Animation] as argument. While that allows you to fine-tune the animation, it also requires more development overhead as you have to manually manage the lifecycle of the underlying [AnimationController].

### AnimatedDefaultTextStyle()

```dart
AnimatedDefaultTextStyle({dynamic key, required Widget child, required TextStyle style, TextAlign? textAlign, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, int? maxLines, TextWidthBasis textWidthBasis = TextWidthBasis.parent, ui.TextHeightBehavior? textHeightBehavior, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates the default text style implicitly.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### style

```dart
TextStyle style
```

The target text style.

When this property is changed, the style will be animated over [duration] time.

### textAlign

```dart
TextAlign? textAlign
```

How the text should be aligned horizontally.

This property takes effect immediately when changed, it is not animated.

### softWrap

```dart
bool softWrap
```

Whether the text should break at soft line breaks.

This property takes effect immediately when changed, it is not animated.

See [DefaultTextStyle.softWrap] for more details.

### overflow

```dart
TextOverflow overflow
```

How visual overflow should be handled.

This property takes effect immediately when changed, it is not animated.

### maxLines

```dart
int? maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary.

This property takes effect immediately when changed, it is not animated.

See [DefaultTextStyle.maxLines] for more details.

### textWidthBasis

```dart
TextWidthBasis textWidthBasis
```

The strategy to use when calculating the width of the Text.

See [TextWidthBasis] for possible values and their implications.

### textHeightBehavior

```dart
ui.TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedDefaultTextStyle> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedPhysicalModel

```dart
class AnimatedPhysicalModel extends ImplicitlyAnimatedWidget {}
```

Animated version of [PhysicalModel].

The [borderRadius] and [elevation] are animated.

The [color] is animated if the [animateColor] property is set; otherwise, the color changes immediately at the start of the animation for the other two properties. This allows the color to be animated independently (e.g. because it is being driven by an [AnimatedTheme]).

The [shape] is not animated.

Here's an illustration of what using this widget looks like, using a [curve] of [Curves.fastOutSlowIn]. {@animation 250 266 https://flutter.github.io/assets-for-api-docs/assets/widgets/animated_physical_model.mp4}

### AnimatedPhysicalModel()

```dart
AnimatedPhysicalModel({dynamic key, required Widget child, BoxShape shape = BoxShape.rectangle, Clip clipBehavior = Clip.none, BorderRadius? borderRadius, double elevation = 0.0, required Color color, bool animateColor = true, required Color shadowColor, bool animateShadowColor = true, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that animates the properties of a [PhysicalModel].

The [elevation] must be non-negative.

Animating [color] is optional and is controlled by the [animateColor] flag.

Animating [shadowColor] is optional and is controlled by the [animateShadowColor] flag.

### child

```dart
Widget child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### shape

```dart
BoxShape shape
```

The type of shape.

This property is not animated.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### borderRadius

```dart
BorderRadius? borderRadius
```

The target border radius of the rounded corners for a rectangle shape.

If null, treated as [BorderRadius.zero].

### elevation

```dart
double elevation
```

The target z-coordinate relative to the parent at which to place this physical object.

The value will always be non-negative.

### color

```dart
Color color
```

The target background color.

### animateColor

```dart
bool animateColor
```

Whether the color should be animated.

### shadowColor

```dart
Color shadowColor
```

The target shadow color.

### animateShadowColor

```dart
bool animateShadowColor
```

Whether the shadow color should be animated.

### createState()

```dart
AnimatedWidgetBaseState<AnimatedPhysicalModel> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# AnimatedFractionallySizedBox

```dart
class AnimatedFractionallySizedBox extends ImplicitlyAnimatedWidget {}
```

Animated version of [FractionallySizedBox] which automatically transitions the child's size over a given duration whenever the given [widthFactor] or [heightFactor] changes, as well as the position whenever the given [alignment] changes.

For the animation, you can choose a [curve] as well as a [duration] and the widget will automatically animate to the new target [widthFactor] or [heightFactor].

{@tool dartpad} The following example transitions an [AnimatedFractionallySizedBox] between two states. It adjusts the [heightFactor], [widthFactor], and [alignment] properties when tapped, using a [curve] of [Curves.fastOutSlowIn]

** See code in examples/api/lib/widgets/implicit_animations/animated_fractionally_sized_box.0.dart ** {@end-tool}

See also:

- [AnimatedAlign], which is an implicitly animated version of [Align].
- [AnimatedContainer], which can transition more values at once.
- [AnimatedSlide], which can animate the translation of child by a given offset relative to its size.
- [AnimatedPositioned], which, as a child of a [Stack], automatically transitions its child's position over a given duration whenever the given position changes.

### AnimatedFractionallySizedBox()

```dart
AnimatedFractionallySizedBox({dynamic key, AlignmentGeometry alignment = Alignment.center, Widget? child, double? heightFactor, double? widthFactor, dynamic curve, required Duration duration, dynamic onEnd})
```

Creates a widget that sizes its child to a fraction of the total available space that animates implicitly, and positions its child by an alignment that animates implicitly.

If non-null, the [widthFactor] and [heightFactor] arguments must be non-negative.

### child

```dart
Widget? child
```

The widget below this widget in the tree.

{@macro flutter.widgets.ProxyWidget.child}

### heightFactor

```dart
double? heightFactor
```

{@macro flutter.widgets.basic.fractionallySizedBox.heightFactor}

### widthFactor

```dart
double? widthFactor
```

{@macro flutter.widgets.basic.fractionallySizedBox.widthFactor}

### alignment

```dart
AlignmentGeometry alignment
```

{@macro flutter.widgets.basic.fractionallySizedBox.alignment}

### createState()

```dart
AnimatedWidgetBaseState<AnimatedFractionallySizedBox> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
