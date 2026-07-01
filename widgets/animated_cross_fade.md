@docImport 'package:flutter/material.dart';

@docImport 'animated_switcher.dart'; @docImport 'implicit_animations.dart';

# CrossFadeState

```dart
enum CrossFadeState {}
```

Specifies which of two children to show. See [AnimatedCrossFade].

The child that is shown will fade in, while the other will fade out.

Show the first child ([AnimatedCrossFade.firstChild]) and hide the second ([AnimatedCrossFade.secondChild]]).

Show the second child ([AnimatedCrossFade.secondChild]) and hide the first ([AnimatedCrossFade.firstChild]).

# AnimatedCrossFadeBuilder

```dart
typedef AnimatedCrossFadeBuilder = Widget Function(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey)
```

Signature for the [AnimatedCrossFade.layoutBuilder] callback.

The `topChild` is the child fading in, which is normally drawn on top. The `bottomChild` is the child fading out, normally drawn on the bottom.

For good performance, the returned widget tree should contain both the `topChild` and the `bottomChild`; the depth of the tree, and the types of the widgets in the tree, from the returned widget to each of the children should be the same; and where there is a widget with multiple children, the top child and the bottom child should be keyed using the provided `topChildKey` and `bottomChildKey` keys respectively.

{@tool snippet}

```dart
Widget defaultLayoutBuilder(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey) {
  return Stack(
    children: <Widget>[
      Positioned(
        key: bottomChildKey,
        left: 0.0,
        top: 0.0,
        right: 0.0,
        child: bottomChild,
      ),
      Positioned(
        key: topChildKey,
        child: topChild,
      )
    ],
  );
}
```

{@end-tool}

# AnimatedCrossFade

```dart
class AnimatedCrossFade extends StatefulWidget {}
```

A widget that cross-fades between two given children and animates itself between their sizes.

{@youtube 560 315 https://www.youtube.com/watch?v=PGK2UUAyE54}

The animation is controlled through the [crossFadeState] parameter. [firstCurve] and [secondCurve] represent the opacity curves of the two children. The [firstCurve] is inverted, i.e. it fades out when providing a growing curve like [Curves.linear]. The [sizeCurve] is the curve used to animate between the size of the fading-out child and the size of the fading-in child.

This widget is intended to be used to fade a pair of widgets with the same width. In the case where the two children have different heights, the animation crops overflowing children during the animation by aligning their top edge, which means that the bottom will be clipped.

The animation is automatically triggered when an existing [AnimatedCrossFade] is rebuilt with a different value for the [crossFadeState] property.

{@tool snippet}

This code fades between two representations of the Flutter logo. It depends on a boolean field `_first`; when `_first` is true, the first logo is shown, otherwise the second logo is shown. When the field changes state, the [AnimatedCrossFade] widget cross-fades between the two forms of the logo over three seconds.

```dart
AnimatedCrossFade(
  duration: const Duration(seconds: 3),
  firstChild: const FlutterLogo(style: FlutterLogoStyle.horizontal, size: 100.0),
  secondChild: const FlutterLogo(style: FlutterLogoStyle.stacked, size: 100.0),
  crossFadeState: _first ? CrossFadeState.showFirst : CrossFadeState.showSecond,
)
```

{@end-tool}

See also:

- [AnimatedOpacity], which fades between nothing and a single child.
- [AnimatedSwitcher], which switches out a child for a new one with a customizable transition, supporting multiple cross-fades at once.
- [AnimatedSize], the lower-level widget which [AnimatedCrossFade] uses to automatically change size.

### AnimatedCrossFade()

```dart
AnimatedCrossFade({dynamic key, required Widget firstChild, required Widget secondChild, Curve firstCurve = Curves.linear, Curve secondCurve = Curves.linear, Curve sizeCurve = Curves.linear, AlignmentGeometry alignment = Alignment.topCenter, required CrossFadeState crossFadeState, required Duration duration, Duration? reverseDuration, AnimatedCrossFadeBuilder layoutBuilder = defaultLayoutBuilder, bool excludeBottomFocus = true, Clip clipBehavior = Clip.hardEdge, VoidCallback? onEnd})
```

Creates a cross-fade animation widget.

The [duration] of the animation is the same for all components (fade in, fade out, and size), and you can pass [Interval]s instead of [Curve]s in order to have finer control, e.g., creating an overlap between the fades.

### firstChild

```dart
Widget firstChild
```

The child that is visible when [crossFadeState] is [CrossFadeState.showFirst]. It fades out when transitioning [crossFadeState] from [CrossFadeState.showFirst] to [CrossFadeState.showSecond] and vice versa.

### secondChild

```dart
Widget secondChild
```

The child that is visible when [crossFadeState] is [CrossFadeState.showSecond]. It fades in when transitioning [crossFadeState] from [CrossFadeState.showFirst] to [CrossFadeState.showSecond] and vice versa.

### crossFadeState

```dart
CrossFadeState crossFadeState
```

The child that will be shown when the animation has completed.

### duration

```dart
Duration duration
```

The duration of the whole orchestrated animation.

### reverseDuration

```dart
Duration? reverseDuration
```

The duration of the whole orchestrated animation when running in reverse.

If not supplied, this defaults to [duration].

### firstCurve

```dart
Curve firstCurve
```

The fade curve of the first child.

Defaults to [Curves.linear].

### secondCurve

```dart
Curve secondCurve
```

The fade curve of the second child.

Defaults to [Curves.linear].

### sizeCurve

```dart
Curve sizeCurve
```

The curve of the animation between the two children's sizes.

Defaults to [Curves.linear].

### alignment

```dart
AlignmentGeometry alignment
```

How the children should be aligned while the size is animating.

Defaults to [Alignment.topCenter].

See also:

- [Alignment], a class with convenient constants typically used to specify an [AlignmentGeometry].
- [AlignmentDirectional], like [Alignment] for specifying alignments relative to text direction.

### layoutBuilder

```dart
AnimatedCrossFadeBuilder layoutBuilder
```

A builder that positions the [firstChild] and [secondChild] widgets.

The widget returned by this method is wrapped in an [AnimatedSize].

By default, this uses [AnimatedCrossFade.defaultLayoutBuilder], which uses a [Stack] and aligns the `bottomChild` to the top of the stack while providing the `topChild` as the non-positioned child to fill the provided constraints. This works well when the [AnimatedCrossFade] is in a position to change size and when the children are not flexible. However, if the children are less fussy about their sizes (for example a [CircularProgressIndicator] inside a [Center]), or if the [AnimatedCrossFade] is being forced to a particular size, then it can result in the widgets jumping about when the cross-fade state is changed.

### excludeBottomFocus

```dart
bool excludeBottomFocus
```

When true, this is equivalent to wrapping the bottom widget with an [ExcludeFocus] widget while it is at the bottom of the cross-fade stack.

Defaults to true. When it is false, the bottom widget in the cross-fade stack can remain in focus until the top widget requests focus. This is useful for animating between different [TextField]s so the keyboard remains open during the cross-fade animation.

### clipBehavior

```dart
Clip clipBehavior
```

Controls whether the content is clipped during the cross-fade transition.

During the size transition between [firstChild] and [secondChild], the content is clipped by default to prevent it from overflowing the bounding box of the animating widget.

Set this to [Clip.none] to disable clipping entirely. This can be useful for widgets with shadows or visual effects that extend beyond their bounds.

Defaults to [Clip.hardEdge].

### onEnd

```dart
VoidCallback? onEnd
```

Called every time an animation completes.

This can be useful to trigger additional actions (e.g. another animation) at the end of the current animation.

### defaultLayoutBuilder()

```dart
Widget defaultLayoutBuilder(Widget topChild, Key topChildKey, Widget bottomChild, Key bottomChildKey)
```

The default layout algorithm used by [AnimatedCrossFade].

The top child is placed in a stack that sizes itself to match the top child. The bottom child is positioned at the top of the same stack, sized to fit its width but without forcing the height. The stack is then clipped.

This is the default value for [layoutBuilder]. It implements [AnimatedCrossFadeBuilder].

### createState()

```dart
State<AnimatedCrossFade> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
