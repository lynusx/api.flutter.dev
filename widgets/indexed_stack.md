@docImport 'animated_cross_fade.dart'; @docImport 'animated_switcher.dart'; @docImport 'implicit_animations.dart'; @docImport 'navigator.dart'; @docImport 'transitions.dart';

# IndexedStack

```dart
class IndexedStack extends StatelessWidget {}
```

A [Stack] that shows a single child from a list of children.

The displayed child is the one with the given [index]. The stack is always as big as the largest child.

If value is null, then nothing is displayed.

{@youtube 560 315 https://www.youtube.com/watch?v=_O0PPD1Xfbk}

{@tool dartpad} This example shows a [IndexedStack] widget being used to lay out one card at a time from a series of cards, each keeping their respective states.

** See code in examples/api/lib/widgets/basic/indexed_stack.0.dart ** {@end-tool}

See also:

- [Stack], for more details about stacks.
- The [catalog of layout widgets](https://flutter.dev/widgets/layout/).

### IndexedStack()

```dart
IndexedStack({dynamic key, AlignmentGeometry alignment = AlignmentDirectional.topStart, TextDirection? textDirection, Clip clipBehavior = Clip.hardEdge, StackFit sizing = StackFit.loose, int? index = 0, List<Widget> children = const <Widget>[]})
```

Creates a [Stack] widget that paints a single child.

### alignment

```dart
AlignmentGeometry alignment
```

How to align the non-positioned and partially-positioned children in the stack.

Defaults to [AlignmentDirectional.topStart].

See [Stack.alignment] for more information.

### textDirection

```dart
TextDirection? textDirection
```

The text direction with which to resolve [alignment].

Defaults to the ambient [Directionality].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### sizing

```dart
StackFit sizing
```

How to size the non-positioned children in the stack.

Defaults to [StackFit.loose].

See [Stack.fit] for more information.

### index

```dart
int? index
```

The index of the child to show.

If this is null, none of the children will be shown.

### children

```dart
List<Widget> children
```

The child widgets of the stack.

Only the child at index [index] will be shown.

See [Stack.children] for more information.

### build()

```dart
Widget build(BuildContext context)
```

# Visibility

```dart
class Visibility extends StatelessWidget {}
```

Whether to show or hide a child.

By default, the [visible] property controls whether the [child] is included in the subtree or not; when it is not [visible], the [replacement] child (typically a zero-sized box) is included instead.

A variety of flags can be used to tweak exactly how the child is hidden. (Changing the flags dynamically is discouraged, as it can cause the [child] subtree to be rebuilt, with any state in the subtree being discarded. Typically, only the [visible] flag is changed dynamically.)

These widgets provide some of the facets of this one:

- [Opacity], which can stop its child from being painted.
- [Offstage], which can stop its child from being laid out or painted.
- [TickerMode], which can stop its child from being animated.
- [ExcludeSemantics], which can hide the child from accessibility tools.
- [IgnorePointer], which can disable touch interactions with the child.

Using this widget is not necessary to hide children. The simplest way to hide a child is just to not include it, or, if a child _must_ be given (e.g. because the parent is a [StatelessWidget]) then to use [SizedBox.shrink] instead of the child that would otherwise be included.

See also:

- [AnimatedSwitcher], which can fade from one child to the next as the subtree changes.
- [AnimatedCrossFade], which can fade between two specific children.
- [SliverVisibility], the sliver equivalent of this widget.

### Visibility()

```dart
Visibility({dynamic key, required Widget child, Widget replacement = const SizedBox.shrink(), bool visible = true, bool maintainState = false, bool maintainAnimation = false, bool maintainSize = false, bool maintainSemantics = false, bool maintainInteractivity = false, bool maintainFocusability = false})
```

Control whether the given [child] is [visible].

The [maintainSemantics] and [maintainInteractivity] arguments can only be set if [maintainSize] is set.

The [maintainSize] argument can only be set if [maintainAnimation] is set.

The [maintainAnimation] argument can only be set if [maintainState] is set.

### Visibility.maintain()

```dart
Visibility.maintain({dynamic key, required Widget child, bool visible = true})
```

Control whether the given [child] is [visible].

This is equivalent to the default [Visibility] constructor with all "maintain" fields set to true. This constructor should be used in place of an [Opacity] widget that only takes on values of `0.0` or `1.0`, as it avoids extra compositing when fully opaque.

### child

```dart
Widget child
```

The widget to show or hide, as controlled by [visible].

{@macro flutter.widgets.ProxyWidget.child}

### replacement

```dart
Widget replacement
```

The widget to use when the child is not [visible], assuming that none of the `maintain` flags (in particular, [maintainState]) are set.

The normal behavior is to replace the widget with a zero by zero box ([SizedBox.shrink]).

See also:

- [AnimatedCrossFade], which can animate between two children.

### visible

```dart
bool visible
```

Switches between showing the [child] or hiding it.

The `maintain` flags should be set to the same values regardless of the state of the [visible] property, otherwise they will not operate correctly (specifically, the state will be lost regardless of the state of [maintainState] whenever any of the `maintain` flags are changed, since doing so will result in a subtree shape change).

Unless [maintainState] is set, the [child] subtree will be disposed (removed from the tree) while hidden.

### maintainState

```dart
bool maintainState
```

Whether to maintain the [State] objects of the [child] subtree when it is not [visible].

Keeping the state of the subtree is potentially expensive (because it means all the objects are still in memory; their resources are not released). It should only be maintained if it cannot be recreated on demand. One example of when the state would be maintained is if the child subtree contains a [Navigator], since that widget maintains elaborate state that cannot be recreated on the fly.

If this property is true, an [Offstage] widget is used to hide the child instead of replacing it with [replacement].

If this property is false, then [maintainAnimation] must also be false.

If this property is false, then [maintainFocusability] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

### maintainAnimation

```dart
bool maintainAnimation
```

Whether to maintain animations within the [child] subtree when it is not [visible].

To set this, [maintainState] must also be set.

Keeping animations active when the widget is not visible is even more expensive than only maintaining the state.

One example when this might be useful is if the subtree is animating its layout in time with an [AnimationController], and the result of that layout is being used to influence some other logic. If this flag is false, then any [AnimationController]s hosted inside the [child] subtree will be muted while the [visible] flag is false.

If this property is true, no [TickerMode] widget is used.

If this property is false, then [maintainSize] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

### maintainSize

```dart
bool maintainSize
```

Whether to maintain space for where the widget would have been.

To set this, [maintainAnimation] and [maintainState] must also be set.

Maintaining the size when the widget is not [visible] is not notably more expensive than just keeping animations running without maintaining the size, and may in some circumstances be slightly cheaper if the subtree is simple and the [visible] property is frequently toggled, since it avoids triggering a layout change when the [visible] property is toggled. If the [child] subtree is not trivial then it is significantly cheaper to not even keep the state (see [maintainState]).

If this property is false, [Offstage] is used.

If this property is false, then [maintainSemantics] and [maintainInteractivity] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

See also:

- [AnimatedOpacity] and [FadeTransition], which apply animations to the opacity for a more subtle effect.

### maintainSemantics

```dart
bool maintainSemantics
```

Whether to maintain the semantics for the widget when it is hidden (e.g. for accessibility).

To set this, [maintainSize] must also be set.

By default, with [maintainSemantics] set to false, the [child] is not visible to accessibility tools when it is hidden from the user. If this flag is set to true, then accessibility tools will report the widget as if it was present.

### maintainInteractivity

```dart
bool maintainInteractivity
```

Whether to allow the widget to be interactive when hidden.

To set this, [maintainSize] must also be set.

By default, with [maintainInteractivity] set to false, touch events cannot reach the [child] when it is hidden from the user. If this flag is set to true, then touch events will nonetheless be passed through.

### maintainFocusability

```dart
bool maintainFocusability
```

Whether to allow the widget to receive focus when hidden. Only in effect if [visible] is false.

To set this to true, [maintainState] must also be set to true.

By default, with [maintainFocusability] set to false, focus events cannot reach the [child] when this widget is not [visible] because an [ExcludeFocus] widget is used to exclude the child subtree from the focus tree. If this flag is set to true, then focus events will reach the child subtree.

### of()

```dart
bool of(BuildContext context)
```

Tells the visibility state of an element in the tree based off its ancestor [Visibility] elements.

If there's one or more [Visibility] widgets in the ancestor tree, this will return true if and only if all of those widgets have [visible] set to true. If there is no [Visibility] widget in the ancestor tree of the specified build context, this will return true.

This will register a dependency from the specified context on any [Visibility] elements in the ancestor tree, such that if any of their visibilities changes, the specified context will be rebuilt.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# SliverVisibility

```dart
class SliverVisibility extends StatelessWidget {}
```

Whether to show or hide a sliver child.

By default, the [visible] property controls whether the [sliver] is included in the subtree or not; when it is not [visible], the [replacementSliver] is included instead.

A variety of flags can be used to tweak exactly how the sliver is hidden. (Changing the flags dynamically is discouraged, as it can cause the [sliver] subtree to be rebuilt, with any state in the subtree being discarded. Typically, only the [visible] flag is changed dynamically.)

These widgets provide some of the facets of this one:

- [SliverOpacity], which can stop its sliver child from being painted.
- [SliverOffstage], which can stop its sliver child from being laid out or painted.
- [TickerMode], which can stop its child from being animated.
- [ExcludeSemantics], which can hide the child from accessibility tools.
- [SliverIgnorePointer], which can disable touch interactions with the sliver child.

Using this widget is not necessary to hide children. The simplest way to hide a child is just to not include it. If a child _must_ be given (e.g. because the parent is a [StatelessWidget]), then including a childless [SliverToBoxAdapter] instead of the child that would otherwise be included is typically more efficient than using [SliverVisibility].

See also:

- [Visibility], the equivalent widget for boxes.

### SliverVisibility()

```dart
SliverVisibility({dynamic key, required Widget sliver, Widget replacementSliver = const SliverToBoxAdapter(), bool visible = true, bool maintainState = false, bool maintainAnimation = false, bool maintainSize = false, bool maintainSemantics = false, bool maintainInteractivity = false})
```

Control whether the given [sliver] is [visible].

The [maintainSemantics] and [maintainInteractivity] arguments can only be set if [maintainSize] is set.

The [maintainSize] argument can only be set if [maintainAnimation] is set.

The [maintainAnimation] argument can only be set if [maintainState] is set.

### SliverVisibility.maintain()

```dart
SliverVisibility.maintain({dynamic key, required Widget sliver, Widget replacementSliver = const SliverToBoxAdapter(), bool visible = true})
```

Control whether the given [sliver] is [visible].

This is equivalent to the default [SliverVisibility] constructor with all "maintain" fields set to true. This constructor should be used in place of a [SliverOpacity] widget that only takes on values of `0.0` or `1.0`, as it avoids extra compositing when fully opaque.

### sliver

```dart
Widget sliver
```

The sliver to show or hide, as controlled by [visible].

### replacementSliver

```dart
Widget replacementSliver
```

The widget to use when the sliver child is not [visible], assuming that none of the `maintain` flags (in particular, [maintainState]) are set.

The normal behavior is to replace the widget with a childless [SliverToBoxAdapter], which by default has a geometry of [SliverGeometry.zero].

### visible

```dart
bool visible
```

Switches between showing the [sliver] or hiding it.

The `maintain` flags should be set to the same values regardless of the state of the [visible] property, otherwise they will not operate correctly (specifically, the state will be lost regardless of the state of [maintainState] whenever any of the `maintain` flags are changed, since doing so will result in a subtree shape change).

Unless [maintainState] is set, the [sliver] subtree will be disposed (removed from the tree) while hidden.

### maintainState

```dart
bool maintainState
```

Whether to maintain the [State] objects of the [sliver] subtree when it is not [visible].

Keeping the state of the subtree is potentially expensive (because it means all the objects are still in memory; their resources are not released). It should only be maintained if it cannot be recreated on demand. One example of when the state would be maintained is if the sliver subtree contains a [Navigator], since that widget maintains elaborate state that cannot be recreated on the fly.

If this property is true, a [SliverOffstage] widget is used to hide the sliver instead of replacing it with [replacementSliver].

If this property is false, then [maintainAnimation] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

### maintainAnimation

```dart
bool maintainAnimation
```

Whether to maintain animations within the [sliver] subtree when it is not [visible].

To set this, [maintainState] must also be set.

Keeping animations active when the widget is not visible is even more expensive than only maintaining the state.

One example when this might be useful is if the subtree is animating its layout in time with an [AnimationController], and the result of that layout is being used to influence some other logic. If this flag is false, then any [AnimationController]s hosted inside the [sliver] subtree will be muted while the [visible] flag is false.

If this property is true, no [TickerMode] widget is used.

If this property is false, then [maintainSize] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

### maintainSize

```dart
bool maintainSize
```

Whether to maintain space for where the sliver would have been.

To set this, [maintainAnimation] must also be set.

Maintaining the size when the sliver is not [visible] is not notably more expensive than just keeping animations running without maintaining the size, and may in some circumstances be slightly cheaper if the subtree is simple and the [visible] property is frequently toggled, since it avoids triggering a layout change when the [visible] property is toggled. If the [sliver] subtree is not trivial then it is significantly cheaper to not even keep the state (see [maintainState]).

If this property is false, [SliverOffstage] is used.

If this property is false, then [maintainSemantics] and [maintainInteractivity] must also be false.

Dynamically changing this value may cause the current state of the subtree to be lost (and a new instance of the subtree, with new [State] objects, to be immediately created if [visible] is true).

### maintainSemantics

```dart
bool maintainSemantics
```

Whether to maintain the semantics for the sliver when it is hidden (e.g. for accessibility).

To set this, [maintainSize] must also be set.

By default, with [maintainSemantics] set to false, the [sliver] is not visible to accessibility tools when it is hidden from the user. If this flag is set to true, then accessibility tools will report the widget as if it was present.

### maintainInteractivity

```dart
bool maintainInteractivity
```

Whether to allow the sliver to be interactive when hidden.

To set this, [maintainSize] must also be set.

By default, with [maintainInteractivity] set to false, touch events cannot reach the [sliver] when it is hidden from the user. If this flag is set to true, then touch events will nonetheless be passed through.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
