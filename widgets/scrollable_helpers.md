@docImport 'package:flutter/material.dart';

@docImport 'overscroll_indicator.dart'; @docImport 'viewport.dart';

# ScrollableDetails

```dart
class ScrollableDetails {}
```

Describes the aspects of a Scrollable widget to inform inherited widgets like [ScrollBehavior] for decorating or enumerate the properties of combined Scrollables, such as [TwoDimensionalScrollable].

Decorations like [GlowingOverscrollIndicator]s and [Scrollbar]s require information about the Scrollable in order to be initialized.

### ScrollableDetails()

```dart
ScrollableDetails({required AxisDirection direction, ScrollController? controller, ScrollPhysics? physics, Clip? clipBehavior, Clip? decorationClipBehavior})
```

Creates a set of details describing the [Scrollable].

### ScrollableDetails.vertical()

```dart
ScrollableDetails.vertical({bool reverse = false, ScrollController? controller, ScrollPhysics? physics, Clip? decorationClipBehavior})
```

A constructor specific to a [Scrollable] with an [Axis.vertical].

### ScrollableDetails.horizontal()

```dart
ScrollableDetails.horizontal({bool reverse = false, ScrollController? controller, ScrollPhysics? physics, Clip? decorationClipBehavior})
```

A constructor specific to a [Scrollable] with an [Axis.horizontal].

### direction

```dart
AxisDirection direction
```

{@macro flutter.widgets.Scrollable.axisDirection}

### controller

```dart
ScrollController? controller
```

{@macro flutter.widgets.Scrollable.controller}

### physics

```dart
ScrollPhysics? physics
```

{@macro flutter.widgets.Scrollable.physics}

### decorationClipBehavior

```dart
Clip? decorationClipBehavior
```

{@macro flutter.material.Material.clipBehavior}

This can be used by [MaterialScrollBehavior] to clip a [StretchingOverscrollIndicator].

This [Clip] does not affect the [Viewport.clipBehavior], but is rather passed from the same value by [Scrollable] so that decorators like [StretchingOverscrollIndicator] honor the same clip.

Defaults to null.

### clipBehavior

```dart
Clip? get clipBehavior
```

Deprecated getter for [decorationClipBehavior].

### copyWith()

```dart
ScrollableDetails copyWith({AxisDirection? direction, ScrollController? controller, ScrollPhysics? physics, Clip? decorationClipBehavior})
```

Copy the current [ScrollableDetails] with the given values replacing the current values.

### toString()

```dart
String toString()
```

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

# EdgeDraggingAutoScroller

```dart
class EdgeDraggingAutoScroller {}
```

An auto scroller that scrolls the [scrollable] if a drag gesture drags close to its edge.

The scroll velocity is controlled by the [velocityScalar]:

velocity = (distance of overscroll) * [velocityScalar].

### EdgeDraggingAutoScroller()

```dart
EdgeDraggingAutoScroller(ScrollableState scrollable, {VoidCallback? onScrollViewScrolled, required double velocityScalar})
```

Creates a auto scroller that scrolls the [scrollable].

### scrollable

```dart
ScrollableState scrollable
```

The [Scrollable] this auto scroller is scrolling.

### onScrollViewScrolled

```dart
VoidCallback? onScrollViewScrolled
```

Called when a scroll view is scrolled.

The scroll view may be scrolled multiple times in a row until the drag target no longer triggers the auto scroll. This callback will be called in between each scroll.

### velocityScalar

```dart
double velocityScalar
```

{@template flutter.widgets.EdgeDraggingAutoScroller.velocityScalar} The velocity scalar per pixel over scroll.

It represents how the velocity scale with the over scroll distance. The auto-scroll velocity = (distance of overscroll) * velocityScalar. {@endtemplate}

### scrolling

```dart
bool get scrolling
```

Whether the auto scroll is in progress.

### startAutoScrollIfNecessary()

```dart
void startAutoScrollIfNecessary(Rect dragTarget)
```

Starts the auto scroll if the [dragTarget] is close to the edge.

The scroll starts to scroll the [scrollable] if the target rect is close to the edge of the [scrollable]; otherwise, it remains stationary.

If the scrollable is already scrolling, calling this method updates the previous dragTarget to the new value and continues scrolling if necessary.

If the [scrollable]'s [ScrollableState.resolvedPhysics] refuses user-driven scrolling (for example [NeverScrollableScrollPhysics]), no auto scroll is started and any in-flight auto scroll is stopped.

### stopAutoScroll()

```dart
void stopAutoScroll()
```

Stop any ongoing auto scrolling.

# ScrollIncrementCalculator

```dart
typedef ScrollIncrementCalculator = double Function(ScrollIncrementDetails details)
```

A typedef for a function that can calculate the offset for a type of scroll increment given a [ScrollIncrementDetails].

This function is used as the type for [Scrollable.incrementCalculator], which is called from a [ScrollAction].

# ScrollIncrementType

```dart
enum ScrollIncrementType {}
```

Describes the type of scroll increment that will be performed by a [ScrollAction] on a [Scrollable].

This is used to configure a [ScrollIncrementDetails] object to pass to a [ScrollIncrementCalculator] function on a [Scrollable].

{@template flutter.widgets.ScrollIncrementType.intent} This indicates the _intent_ of the scroll, not necessarily the size. Not all scrollable areas will have the concept of a "line" or "page", but they can respond to the different standard key bindings that cause scrolling, which are bound to keys that people use to indicate a "line" scroll (e.g. control-arrowDown keys) or a "page" scroll (e.g. pageDown key). It is recommended that at least the relative magnitudes of the scrolls match expectations. {@endtemplate}

Indicates that the [ScrollIncrementCalculator] should return the scroll distance it should move when the user requests to scroll by a "line".

The distance a "line" scrolls refers to what should happen when the key binding for "scroll down/up by a line" is triggered. It's up to the [ScrollIncrementCalculator] function to decide what that means for a particular scrollable.

Indicates that the [ScrollIncrementCalculator] should return the scroll distance it should move when the user requests to scroll by a "page".

The distance a "page" scrolls refers to what should happen when the key binding for "scroll down/up by a page" is triggered. It's up to the [ScrollIncrementCalculator] function to decide what that means for a particular scrollable.

# ScrollIncrementDetails

```dart
class ScrollIncrementDetails {}
```

A details object that describes the type of scroll increment being requested of a [ScrollIncrementCalculator] function, as well as the current metrics for the scrollable.

### ScrollIncrementDetails()

```dart
ScrollIncrementDetails({required ScrollIncrementType type, required ScrollMetrics metrics})
```

A const constructor for a [ScrollIncrementDetails].

### type

```dart
ScrollIncrementType type
```

The type of scroll this is (e.g. line, page, etc.).

{@macro flutter.widgets.ScrollIncrementType.intent}

### metrics

```dart
ScrollMetrics metrics
```

The current metrics of the scrollable that is being scrolled.

# ScrollIntent

```dart
class ScrollIntent extends Intent {}
```

An [Intent] that represents scrolling the nearest scrollable by an amount appropriate for the [type] specified.

The actual amount of the scroll is determined by the [Scrollable.incrementCalculator], or by its defaults if that is not specified.

### ScrollIntent()

```dart
ScrollIntent({required AxisDirection direction, ScrollIncrementType type = ScrollIncrementType.line})
```

Creates a const [ScrollIntent] that requests scrolling in the given [direction], with the given [type].

### direction

```dart
AxisDirection direction
```

The direction in which to scroll the scrollable containing the focused widget.

### type

```dart
ScrollIncrementType type
```

The type of scrolling that is intended.

# ScrollAction

```dart
class ScrollAction extends ContextAction<ScrollIntent> {}
```

An [Action] that scrolls the relevant [Scrollable] by the amount configured in the [ScrollIntent] given to it.

If a Scrollable cannot be found above the given [BuildContext], the [PrimaryScrollController] will be considered for default handling of [ScrollAction]s.

If [Scrollable.incrementCalculator] is null for the scrollable, the default for a [ScrollIntent.type] set to [ScrollIncrementType.page] is 80% of the size of the scroll window, and for [ScrollIncrementType.line], 50 logical pixels.

### isEnabled()

```dart
bool isEnabled(ScrollIntent intent, [BuildContext? context])
```

### getDirectionalIncrement()

```dart
double getDirectionalIncrement(ScrollableState state, ScrollIntent intent)
```

Find out how much of an increment to move by, taking the different directions into account.

### invoke()

```dart
void invoke(ScrollIntent intent, [BuildContext? context])
```
