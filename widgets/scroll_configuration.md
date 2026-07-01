@docImport 'package:flutter/material.dart';

@docImport 'list_wheel_scroll_view.dart'; @docImport 'page_view.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_view.dart';

# AndroidOverscrollIndicator

```dart
enum AndroidOverscrollIndicator {}
```

Types of overscroll indicators supported by [TargetPlatform.android].

Utilizes a [StretchingOverscrollIndicator], which transforms the contents of a [ScrollView] when overscrolled.

Utilizes a [GlowingOverscrollIndicator], painting a glowing semi circle on top of the [ScrollView] in response to overscrolling.

# ScrollBehavior

```dart
class ScrollBehavior {}
```

Describes how [Scrollable] widgets should behave.

{@template flutter.widgets.scrollBehavior} Used by [ScrollConfiguration] to configure the [Scrollable] widgets in a subtree.

This class can be extended to further customize a [ScrollBehavior] for a subtree. For example, overriding [ScrollBehavior.getScrollPhysics] sets the default [ScrollPhysics] for [Scrollable]s that inherit this [ScrollConfiguration]. Overriding [ScrollBehavior.buildOverscrollIndicator] can be used to add or change the default [GlowingOverscrollIndicator] decoration, while [ScrollBehavior.buildScrollbar] can be changed to modify the default [Scrollbar].

When looking to easily toggle the default decorations, you can use [ScrollBehavior.copyWith] instead of creating your own [ScrollBehavior] class. The `scrollbar` and `overscrollIndicator` flags can turn these decorations off. {@endtemplate}

See also:

- [ScrollConfiguration], the inherited widget that controls how [Scrollable] widgets behave in a subtree.

### ScrollBehavior()

```dart
ScrollBehavior()
```

Creates a description of how [Scrollable] widgets should behave.

### copyWith()

```dart
ScrollBehavior copyWith({bool? scrollbars, bool? overscroll, Set<PointerDeviceKind>? dragDevices, MultitouchDragStrategy? multitouchDragStrategy, Set<LogicalKeyboardKey>? pointerAxisModifiers, ScrollPhysics? physics, TargetPlatform? platform, ScrollViewKeyboardDismissBehavior? keyboardDismissBehavior})
```

Creates a copy of this ScrollBehavior, making it possible to easily toggle `scrollbar` and `overscrollIndicator` effects.

This is used by widgets like [PageView] and [ListWheelScrollView] to override the current [ScrollBehavior] and manage how they are decorated. Widgets such as these have the option to provide a [ScrollBehavior] on the widget level, like [PageView.scrollBehavior], in order to change the default.

### getPlatform()

```dart
TargetPlatform getPlatform(BuildContext context)
```

The platform whose scroll physics should be implemented.

Defaults to the current platform.

### dragDevices

```dart
Set<PointerDeviceKind> get dragDevices
```

The device kinds that the scrollable will accept drag gestures from.

By default only [PointerDeviceKind.touch], [PointerDeviceKind.stylus], [PointerDeviceKind.invertedStylus], and [PointerDeviceKind.trackpad] are configured to create drag gestures. Enabling this for [PointerDeviceKind.mouse] will make it difficult or impossible to select text in scrollable containers and is not recommended.

### getMultitouchDragStrategy()

```dart
MultitouchDragStrategy getMultitouchDragStrategy(BuildContext context)
```

{@macro flutter.gestures.monodrag.DragGestureRecognizer.multitouchDragStrategy}

By default, [MultitouchDragStrategy.latestPointer] is configured to create drag gestures for non-Apple platforms, and [MultitouchDragStrategy.averageBoundaryPointers] for Apple platforms.

### pointerAxisModifiers

```dart
Set<LogicalKeyboardKey> get pointerAxisModifiers
```

A set of [LogicalKeyboardKey]s that, when any or all are pressed in combination with a [PointerDeviceKind.mouse] pointer scroll event, will flip the axes of the scroll input.

This will for example, result in the input of a vertical mouse wheel, to move the [ScrollPosition] of a [ScrollView] with an [Axis.horizontal] scroll direction.

If other keys exclusive of this set are pressed during a scroll event, in conjunction with keys from this set, the scroll input will still be flipped.

Defaults to [LogicalKeyboardKey.shiftLeft], [LogicalKeyboardKey.shiftRight].

### buildScrollbar()

```dart
Widget buildScrollbar(BuildContext context, Widget child, ScrollableDetails details)
```

Applies a [RawScrollbar] to the child widget on desktop platforms.

### buildOverscrollIndicator()

```dart
Widget buildOverscrollIndicator(BuildContext context, Widget child, ScrollableDetails details)
```

Applies a [GlowingOverscrollIndicator] to the child widget on [TargetPlatform.android] and [TargetPlatform.fuchsia].

### velocityTrackerBuilder()

```dart
GestureVelocityTrackerBuilder velocityTrackerBuilder(BuildContext context)
```

Specifies the type of velocity tracker to use in the descendant [Scrollable]s' drag gesture recognizers, for estimating the velocity of a drag gesture.

This can be used to, for example, apply different fling velocity estimation methods on different platforms, in order to match the platform's native behavior.

Typically, the provided [GestureVelocityTrackerBuilder] should return a fresh velocity tracker. If null is returned, [Scrollable] creates a new [VelocityTracker] to track the newly added pointer that may develop into a drag gesture.

The default implementation provides a new [IOSScrollViewFlingVelocityTracker] on iOS and macOS for each new pointer, and a new [VelocityTracker] on other platforms for each new pointer.

### getScrollPhysics()

```dart
ScrollPhysics getScrollPhysics(BuildContext context)
```

The scroll physics to use for the platform given by [getPlatform].

Defaults to [RangeMaintainingScrollPhysics] mixed with [BouncingScrollPhysics] on iOS and [ClampingScrollPhysics] on Android.

### shouldNotify()

```dart
bool shouldNotify(ScrollBehavior oldDelegate)
```

Called whenever a [ScrollConfiguration] is rebuilt with a new [ScrollBehavior] of the same [runtimeType].

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false.

If this method returns true, all the widgets that inherit from the [ScrollConfiguration] will rebuild using the new [ScrollBehavior]. If this method returns false, the rebuilds might be optimized away.

### getKeyboardDismissBehavior()

```dart
ScrollViewKeyboardDismissBehavior getKeyboardDismissBehavior(BuildContext context)
```

The default keyboard dismissal behavior for [ScrollView] widgets.

Defaults to [ScrollViewKeyboardDismissBehavior.manual].

### toString()

```dart
String toString()
```

# ScrollConfiguration

```dart
class ScrollConfiguration extends InheritedWidget {}
```

Controls how [Scrollable] widgets behave in a subtree.

The scroll configuration determines the [ScrollPhysics] and viewport decorations used by descendants of [child].

### ScrollConfiguration()

```dart
ScrollConfiguration({dynamic key, required ScrollBehavior behavior, required Widget child})
```

Creates a widget that controls how [Scrollable] widgets behave in a subtree.

### behavior

```dart
ScrollBehavior behavior
```

How [Scrollable] widgets that are descendants of [child] should behave.

### of()

```dart
ScrollBehavior of(BuildContext context)
```

The [ScrollBehavior] for [Scrollable] widgets in the given [BuildContext].

If no [ScrollConfiguration] widget is in scope of the given `context`, a default [ScrollBehavior] instance is returned.

### updateShouldNotify()

```dart
bool updateShouldNotify(ScrollConfiguration oldWidget)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
