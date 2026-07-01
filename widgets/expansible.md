@docImport 'package:flutter/material.dart';

# ExpansibleComponentBuilder

```dart
typedef ExpansibleComponentBuilder = Widget Function(BuildContext context, Animation<double> animation)
```

The type of the callback that returns the header or body of an [Expansible].

The `animation` property exposes the underlying expanding or collapsing animation, which has a value of 0 when the [Expansible] is completely collapsed and 1 when it is completely expanded. This can be used to drive animations that sync up with the expanding or collapsing animation, such as rotating an icon.

See also:

- [Expansible.headerBuilder], which is of this type.
- [Expansible.bodyBuilder], which is also of this type.

# ExpansibleBuilder

```dart
typedef ExpansibleBuilder = Widget Function(BuildContext context, Widget header, Widget body, Animation<double> animation)
```

The type of the callback that uses the header and body of an [Expansible] widget to build the widget.

The `header` property is the header returned by [Expansible.headerBuilder]. The `body` property is the body returned by [Expansible.bodyBuilder] wrapped in an [Offstage] to hide the body when the [Expansible] is collapsed.

The `animation` property exposes the underlying expanding or collapsing animation, which has a value of 0 when the [Expansible] is completely collapsed and 1 when it is completely expanded. This can be used to drive animations that sync up with the expanding or collapsing animation, such as rotating an icon.

See also:

- [Expansible.expansibleBuilder], which is of this type.

# ExpansibleController

```dart
class ExpansibleController extends ChangeNotifier {}
```

A controller for managing the expansion state of an [Expansible].

This class is a [ChangeNotifier] that notifies its listeners if the value of [isExpanded] changes.

This controller provides methods to programmatically expand or collapse the widget, and it allows external components to query the current expansion state.

The controller's [expand] and [collapse] methods cause the [Expansible] to rebuild, so they may not be called from a build method.

Remember to [dispose] of the [ExpansibleController] when it is no longer needed. This will ensure all resources used by the object are discarded.

### ExpansibleController()

```dart
ExpansibleController()
```

Creates a controller to be used with [Expansible.controller].

### isExpanded

```dart
bool get isExpanded
```

Whether the expansible widget built with this controller is in expanded state.

This property doesn't take the animation into account. It reports `true` even if the expansion animation is not completed.

To be notified when this property changes, add a listener to the controller using [ExpansibleController.addListener].

See also:

- [expand], which expands the expansible widget.
- [collapse], which collapses the expansible widget.

### expand()

```dart
void expand()
```

Expands the [Expansible] that was built with this controller.

If the widget is already in the expanded state (see [isExpanded]), calling this method has no effect.

Calling this method may cause the [Expansible] to rebuild, so it may not be called from a build method.

Calling this method will notify registered listeners of this controller that the expansion state has changed.

See also:

- [collapse], which collapses the expansible widget.
- [isExpanded] to check whether the expansible widget is expanded.

### collapse()

```dart
void collapse()
```

Collapses the [Expansible] that was built with this controller.

If the widget is already in the collapsed state (see [isExpanded]), calling this method has no effect.

Calling this method may cause the [Expansible] to rebuild, so it may not be called from a build method.

Calling this method will notify registered listeners of this controller that the expansion state has changed.

See also:

- [expand], which expands the [Expansible].
- [isExpanded] to check whether the [Expansible] is expanded.

### toggle()

```dart
void toggle()
```

Convenience method for toggling the current [isExpanded] status.

Calling this method may cause the [Expansible] to rebuild, so it may not be called from a build method.

Calling this method will notify registered listeners of this controller that the expansion state has changed.

See also:

- [expand], which expands the [Expansible].
- [collapse], which collapses the [Expansible].
- [isExpanded] to check whether the [Expansible] is expanded.

### of()

```dart
ExpansibleController of(BuildContext context)
```

Finds the [ExpansibleController] for the closest [Expansible] instance that encloses the given context.

If no [Expansible] encloses the given context, calling this method will cause an assert in debug mode, and throw an exception in release mode.

To return null if there is no [Expansible] use [maybeOf] instead.

Typical usage of the [ExpansibleController.of] function is to call it from within the `build` method of a descendant of an [Expansible].

### maybeOf()

```dart
ExpansibleController? maybeOf(BuildContext context)
```

Finds the [Expansible] from the closest instance of this class that encloses the given context and returns its [ExpansibleController].

If no [Expansible] encloses the given context then return null. To throw an exception instead, use [of] instead of this function.

See also:

- [of], a similar function to this one that throws if no [Expansible] encloses the given context.

# Expansible

```dart
class Expansible extends StatefulWidget {}
```

A [StatefulWidget] that expands and collapses.

An [Expansible] consists of a header, which is always shown, and a body, which is hidden in its collapsed state and shown in its expanded state.

The [Expansible] is expanded or collapsed with an animation driven by an [AnimationController]. When the widget is expanded, the height of its body animates from 0 to its fully expanded height.

This widget is typically used with [ListView] to create an "expand / collapse" list entry. When used with scrolling widgets like [ListView], a unique [PageStorageKey] must be specified as the [key], to enable the [Expansible] to save and restore its expanded state when it is scrolled in and out of view.

Provide [headerBuilder] and [bodyBuilder] callbacks to build the header and body widgets. An additional [expansibleBuilder] callback can be provided to further customize the layout of the widget.

The [Expansible] does not inherently toggle the expansion state. To toggle the expansion state, call [ExpansibleController.expand] and [ExpansibleController.collapse] as needed, most typically when the header returned in [headerBuilder] is tapped.

{@tool dartpad} This example demonstrates how to use the [Expansible] widget and how an [ExpansibleController] can be used to programmatically expand or collapse it.

** See code in examples/api/lib/material/expansible/expansible.0.dart ** {@end-tool}

See also:

- [ExpansionTile], a Material-styled widget that expands and collapses.

### Expansible()

```dart
Expansible({dynamic key, required ExpansibleComponentBuilder headerBuilder, required ExpansibleComponentBuilder bodyBuilder, required ExpansibleController controller, ExpansibleBuilder expansibleBuilder = _defaultExpansibleBuilder, AnimationStyle? animationStyle, Duration duration = const Duration(milliseconds: 200), Curve curve = Curves.ease, Curve? reverseCurve, bool maintainState = true})
```

Creates an instance of [Expansible].

### controller

```dart
ExpansibleController controller
```

Expands and collapses the widget.

The controller manages the expansion state and toggles the expansion.

### headerBuilder

```dart
ExpansibleComponentBuilder headerBuilder
```

Builds the always-displayed header.

Many use cases involve toggling the expansion state when this header is tapped. To toggle the expansion state, call [ExpansibleController.expand] or [ExpansibleController.collapse].

### bodyBuilder

```dart
ExpansibleComponentBuilder bodyBuilder
```

Builds the collapsible body.

When this widget is expanded, the height of its body animates from 0 to its fully extended height.

### animationStyle

```dart
AnimationStyle? animationStyle
```

Used to override the expansion animation curve and duration.

If [AnimationStyle.duration] is provided, it will be used instead of [duration]. If not provided, [duration] is used, which defaults to 200ms.

If [AnimationStyle.curve] is provided, it will be used to override [curve]. If it is null, then [curve] will be used. Otherwise, defaults to [Curves.ease].

If [AnimationStyle.reverseCurve] is provided, it will be used to override [reverseCurve]. If it is null, then [reverseCurve] will be used.

To disable the theme animation, use [AnimationStyle.noAnimation].

### duration

```dart
Duration duration
```

The duration of the expansion animation.

Defaults to a duration of 200ms.

This property is deprecated, use [animationStyle] instead.

### curve

```dart
Curve curve
```

The curve of the expansion animation.

Defaults to [Curves.ease].

This property is deprecated, use [animationStyle] instead.

### reverseCurve

```dart
Curve? reverseCurve
```

The reverse curve of the expansion animation.

If null, uses [curve] in both directions.

This property is deprecated, use [animationStyle] instead.

### maintainState

```dart
bool maintainState
```

Whether the state of the body is maintained when the widget expands or collapses.

If true, the body is kept in the tree while the widget is collapsed. Otherwise, the body is removed from the tree when the widget is collapsed and recreated upon expansion.

Defaults to true.

### expansibleBuilder

```dart
ExpansibleBuilder expansibleBuilder
```

Builds the widget with the results of [headerBuilder] and [bodyBuilder].

Defaults to placing the header and body in a [Column].

### createState()

```dart
State<StatefulWidget> createState()
```
