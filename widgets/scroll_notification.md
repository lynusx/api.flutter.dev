@docImport 'package:flutter/material.dart';

@docImport 'overscroll_indicator.dart'; @docImport 'scroll_activity.dart'; @docImport 'scroll_controller.dart'; @docImport 'scroll_physics.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'viewport.dart';

# ViewportNotificationMixin

```dart
mixin ViewportNotificationMixin on Notification {}
```

Mixin for [Notification]s that track how many [RenderAbstractViewport] they have bubbled through.

This is used by [ScrollNotification] and [OverscrollIndicatorNotification].

### depth

```dart
int get depth
```

The number of viewports that this notification has bubbled through.

Typically listeners only respond to notifications with a [depth] of zero.

Specifically, this is the number of [Widget]s representing [RenderAbstractViewport] render objects through which this notification has bubbled.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# ViewportElementMixin

```dart
mixin ViewportElementMixin on NotifiableElementMixin {}
```

A mixin that allows [Element]s containing [Viewport] like widgets to correctly modify the notification depth of a [ViewportNotificationMixin].

See also:

- [Viewport], which creates a custom [MultiChildRenderObjectElement] that mixes this in.

### onNotification()

```dart
bool onNotification(Notification notification)
```

# ScrollNotification

```dart
abstract class ScrollNotification extends LayoutChangedNotification with ViewportNotificationMixin {}
```

A [Notification] related to scrolling.

[Scrollable] widgets notify their ancestors about scrolling-related changes. The notifications have the following lifecycle:

- A [ScrollStartNotification], which indicates that the widget has started scrolling.
- Zero or more [ScrollUpdateNotification]s, which indicate that the widget has changed its scroll position, mixed with zero or more [OverscrollNotification]s, which indicate that the widget has not changed its scroll position because the change would have caused its scroll position to go outside its scroll bounds.
- Interspersed with the [ScrollUpdateNotification]s and [OverscrollNotification]s are zero or more [UserScrollNotification]s, which indicate that the user has changed the direction in which they are scrolling.
- A [ScrollEndNotification], which indicates that the widget has stopped scrolling.
- A [UserScrollNotification], with a [UserScrollNotification.direction] of [ScrollDirection.idle].

Notifications bubble up through the tree, which means a given [NotificationListener] will receive notifications for all descendant [Scrollable] widgets. To focus on notifications from the nearest [Scrollable] descendant, check that the [depth] property of the notification is zero.

When a scroll notification is received by a [NotificationListener], the listener will have already completed build and layout, and it is therefore too late for that widget to call [State.setState]. Any attempt to adjust the build or layout based on a scroll notification would result in a layout that lagged one frame behind, which is a poor user experience. Scroll notifications are therefore primarily useful for paint effects (since paint happens after layout). The [GlowingOverscrollIndicator] and [Scrollbar] widgets are examples of paint effects that use scroll notifications.

{@tool dartpad} This sample shows the difference between using a [ScrollController] or a [NotificationListener] of type [ScrollNotification] to listen to scrolling activities. Toggling the [Radio] button switches between the two. Using a [ScrollNotification] will provide details about the scrolling activity, along with the metrics of the [ScrollPosition], but not the scroll position object itself. By listening with a [ScrollController], the position object is directly accessible. Both of these types of notifications are only triggered by scrolling.

** See code in examples/api/lib/widgets/scroll_position/scroll_controller_notification.0.dart ** {@end-tool}

To drive layout based on the scroll position, consider listening to the [ScrollPosition] directly (or indirectly via a [ScrollController]). This will not notify when the [ScrollMetrics] of a given scroll position changes, such as when the window is resized, changing the dimensions of the [Viewport]. In order to listen to changes in scroll metrics, use a [NotificationListener] of type [ScrollMetricsNotification]. This type of notification differs from [ScrollNotification], as it is not associated with the activity of scrolling, but rather the dimensions of the scrollable area.

{@tool dartpad} This sample shows how a [ScrollMetricsNotification] is dispatched when the `windowSize` is changed. Press the floating action button to increase the scrollable window's size.

** See code in examples/api/lib/widgets/scroll_position/scroll_metrics_notification.0.dart ** {@end-tool}

### ScrollNotification()

```dart
ScrollNotification({required ScrollMetrics metrics, required BuildContext? context})
```

Initializes fields for subclasses.

### metrics

```dart
ScrollMetrics metrics
```

A description of a [Scrollable]'s contents, useful for modeling the state of its viewport.

### context

```dart
BuildContext? context
```

The build context of the widget that fired this notification.

This can be used to find the scrollable's render objects to determine the size of the viewport, for instance.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# ScrollStartNotification

```dart
class ScrollStartNotification extends ScrollNotification {}
```

A notification that a [Scrollable] widget has started scrolling.

See also:

- [ScrollEndNotification], which indicates that scrolling has stopped.
- [ScrollNotification], which describes the notification lifecycle.

### ScrollStartNotification()

```dart
ScrollStartNotification({required ScrollMetrics metrics, required BuildContext? context, DragStartDetails? dragDetails})
```

Creates a notification that a [Scrollable] widget has started scrolling.

### dragDetails

```dart
DragStartDetails? dragDetails
```

If the [Scrollable] started scrolling because of a drag, the details about that drag start.

Otherwise, null.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# ScrollUpdateNotification

```dart
class ScrollUpdateNotification extends ScrollNotification {}
```

A notification that a [Scrollable] widget has changed its scroll position.

See also:

- [OverscrollNotification], which indicates that a [Scrollable] widget has not changed its scroll position because the change would have caused its scroll position to go outside its scroll bounds.
- [ScrollNotification], which describes the notification lifecycle.

### ScrollUpdateNotification()

```dart
ScrollUpdateNotification({required ScrollMetrics metrics, required BuildContext context, DragUpdateDetails? dragDetails, double? scrollDelta, int? depth})
```

Creates a notification that a [Scrollable] widget has changed its scroll position.

### dragDetails

```dart
DragUpdateDetails? dragDetails
```

If the [Scrollable] changed its scroll position because of a drag, the details about that drag update.

Otherwise, null.

### scrollDelta

```dart
double? scrollDelta
```

The distance by which the [Scrollable] was scrolled, in logical pixels.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# OverscrollNotification

```dart
class OverscrollNotification extends ScrollNotification {}
```

A notification that a [Scrollable] widget has not changed its scroll position because the change would have caused its scroll position to go outside of its scroll bounds.

See also:

- [ScrollUpdateNotification], which indicates that a [Scrollable] widget has changed its scroll position.
- [ScrollNotification], which describes the notification lifecycle.

### OverscrollNotification()

```dart
OverscrollNotification({required ScrollMetrics metrics, required BuildContext context, DragUpdateDetails? dragDetails, required double overscroll, double velocity = 0.0})
```

Creates a notification that a [Scrollable] widget has changed its scroll position outside of its scroll bounds.

### dragDetails

```dart
DragUpdateDetails? dragDetails
```

If the [Scrollable] overscrolled because of a drag, the details about that drag update.

Otherwise, null.

### overscroll

```dart
double overscroll
```

The number of logical pixels that the [Scrollable] avoided scrolling.

This will be negative for overscroll on the "start" side and positive for overscroll on the "end" side.

### velocity

```dart
double velocity
```

The velocity at which the [ScrollPosition] was changing when this overscroll happened.

This will typically be 0.0 for touch-driven overscrolls, and positive for overscrolls that happened from a [BallisticScrollActivity] or [DrivenScrollActivity].

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# ScrollEndNotification

```dart
class ScrollEndNotification extends ScrollNotification {}
```

A notification that a [Scrollable] widget has stopped scrolling.

{@tool dartpad} This sample shows how you can trigger an auto-scroll, which aligns the last partially visible fixed-height list item, by listening for this notification with a [NotificationListener]. This sort of thing can also be done by listening to the [ScrollController]'s [ScrollPosition.isScrollingNotifier]. An alternative example is provided with [ScrollPosition.isScrollingNotifier].

** See code in examples/api/lib/widgets/scroll_end_notification/scroll_end_notification.0.dart ** {@end-tool}

{@tool dartpad} This example auto-scrolls one special "aligned item" sliver to the top or bottom of the viewport, whenever it's partially visible (because it overlaps the top or bottom of the viewport). This example differs from the previous one in that the layout of an individual sliver is retrieved from its [RenderSliver] via a [GlobalKey]. The example does not rely on all of the list items having the same extent.

** See code in examples/api/lib/widgets/scroll_end_notification/scroll_end_notification.1.dart ** {@end-tool} See also:

- [ScrollStartNotification], which indicates that scrolling has started.
- [ScrollNotification], which describes the notification lifecycle.

### ScrollEndNotification()

```dart
ScrollEndNotification({required ScrollMetrics metrics, required BuildContext context, DragEndDetails? dragDetails})
```

Creates a notification that a [Scrollable] widget has stopped scrolling.

### dragDetails

```dart
DragEndDetails? dragDetails
```

If the [Scrollable] stopped scrolling because of a drag, the details about that drag end.

Otherwise, null.

If a drag ends with some residual velocity, a typical [ScrollPhysics] will start a ballistic scroll, which delays the [ScrollEndNotification] until the ballistic simulation completes, at which time [dragDetails] will be null. If the residual velocity is too small to trigger ballistic scrolling, then the [ScrollEndNotification] will be dispatched immediately and [dragDetails] will be non-null.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# UserScrollNotification

```dart
class UserScrollNotification extends ScrollNotification {}
```

A notification that the user has changed the [ScrollDirection] in which they are scrolling, or have stopped scrolling.

For the direction that the [ScrollView] is oriented to, and the direction contents are being laid out in, see [AxisDirection] & [GrowthDirection].

{@macro flutter.rendering.ScrollDirection.sample}

See also:

- [ScrollNotification], which describes the notification lifecycle.

### UserScrollNotification()

```dart
UserScrollNotification({required ScrollMetrics metrics, required BuildContext context, required ScrollDirection direction})
```

Creates a notification that the user has changed the direction in which they are scrolling.

### direction

```dart
ScrollDirection direction
```

The direction in which the user is scrolling.

This does not represent the current [AxisDirection] or [GrowthDirection] of the [Viewport], which respectively represent the direction that the scroll offset is increasing in, and the direction that contents are being laid out in.

{@macro flutter.rendering.ScrollDirection.sample}

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# ScrollNotificationPredicate

```dart
typedef ScrollNotificationPredicate = bool Function(ScrollNotification notification)
```

A predicate for [ScrollNotification], used to customize widgets that listen to notifications from their children.

# defaultScrollNotificationPredicate()

```dart
bool defaultScrollNotificationPredicate(ScrollNotification notification)
```

A [ScrollNotificationPredicate] that checks whether `notification.depth == 0`, which means that the notification did not bubble through any intervening scrolling widgets.
