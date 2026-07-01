@docImport 'package:flutter/rendering.dart';

@docImport 'scroll_controller.dart'; @docImport 'scroll_physics.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_position_with_single_context.dart'; @docImport 'scrollable.dart';

# ScrollActivityDelegate

```dart
abstract class ScrollActivityDelegate {}
```

A backend for a [ScrollActivity].

Used by subclasses of [ScrollActivity] to manipulate the scroll view that they are acting upon.

See also:

- [ScrollActivity], which uses this class as its delegate.
- [ScrollPositionWithSingleContext], the main implementation of this interface.

### axisDirection

```dart
AxisDirection get axisDirection
```

The direction in which the scroll view scrolls.

### setPixels()

```dart
double setPixels(double pixels)
```

Update the scroll position to the given pixel value.

Returns the overscroll, if any. See [ScrollPosition.setPixels] for more information.

### applyUserOffset()

```dart
void applyUserOffset(double delta)
```

Updates the scroll position by the given amount.

Appropriate for when the user is directly manipulating the scroll position, for example by dragging the scroll view. Typically applies [ScrollPhysics.applyPhysicsToUserOffset] and other transformations that are appropriate for user-driving scrolling.

### goIdle()

```dart
void goIdle()
```

Terminate the current activity and start an idle activity.

### goBallistic()

```dart
void goBallistic(double velocity)
```

Terminate the current activity and start a ballistic activity with the given velocity.

# ScrollActivity

```dart
abstract class ScrollActivity {}
```

Base class for scrolling activities like dragging and flinging.

See also:

- [ScrollPosition], which uses [ScrollActivity] objects to manage the [ScrollPosition] of a [Scrollable].

### ScrollActivity()

```dart
ScrollActivity(ScrollActivityDelegate _delegate)
```

Initializes [delegate] for subclasses.

### delegate

```dart
ScrollActivityDelegate get delegate
```

The delegate that this activity will use to actuate the scroll view.

### updateDelegate()

```dart
void updateDelegate(ScrollActivityDelegate value)
```

Updates the activity's link to the [ScrollActivityDelegate].

This should only be called when an activity is being moved from a defunct (or about-to-be defunct) [ScrollActivityDelegate] object to a new one.

### resetActivity()

```dart
void resetActivity()
```

Called by the [ScrollActivityDelegate] when it has changed type (for example, when changing from an Android-style scroll position to an iOS-style scroll position). If this activity can differ between the two modes, then it should tell the position to restart that activity appropriately.

For example, [BallisticScrollActivity]'s implementation calls [ScrollActivityDelegate.goBallistic].

### dispatchScrollStartNotification()

```dart
void dispatchScrollStartNotification(ScrollMetrics metrics, BuildContext? context)
```

Dispatch a [ScrollStartNotification] with the given metrics.

### dispatchScrollUpdateNotification()

```dart
void dispatchScrollUpdateNotification(ScrollMetrics metrics, BuildContext context, double scrollDelta)
```

Dispatch a [ScrollUpdateNotification] with the given metrics and scroll delta.

### dispatchOverscrollNotification()

```dart
void dispatchOverscrollNotification(ScrollMetrics metrics, BuildContext context, double overscroll)
```

Dispatch an [OverscrollNotification] with the given metrics and overscroll.

### dispatchScrollEndNotification()

```dart
void dispatchScrollEndNotification(ScrollMetrics metrics, BuildContext context)
```

Dispatch a [ScrollEndNotification] with the given metrics and overscroll.

### applyNewDimensions()

```dart
void applyNewDimensions()
```

Called when the scroll view that is performing this activity changes its metrics.

### shouldIgnorePointer

```dart
bool get shouldIgnorePointer
```

Whether the scroll view should ignore pointer events while performing this activity.

See also:

- [isScrolling], which describes whether the activity is considered to represent user interaction or not.

### isScrolling

```dart
bool get isScrolling
```

Whether performing this activity constitutes scrolling.

Used, for example, to determine whether the user scroll direction (see [ScrollPosition.userScrollDirection]) is [ScrollDirection.idle].

See also:

- [shouldIgnorePointer], which controls whether pointer events are allowed while the activity is live.
- [UserScrollNotification], which exposes this status.

### velocity

```dart
double get velocity
```

If applicable, the velocity at which the scroll offset is currently independently changing (i.e. without external stimuli such as a dragging gestures) in logical pixels per second for this activity.

### dispose()

```dart
void dispose()
```

Called when the scroll view stops performing this activity.

### toString()

```dart
String toString()
```

# IdleScrollActivity

```dart
class IdleScrollActivity extends ScrollActivity {}
```

A scroll activity that does nothing.

When a scroll view is not scrolling, it is performing the idle activity.

If the [Scrollable] changes dimensions, this activity triggers a ballistic activity to restore the view.

### IdleScrollActivity()

```dart
IdleScrollActivity(ScrollActivityDelegate delegate)
```

Creates a scroll activity that does nothing.

### applyNewDimensions()

```dart
void applyNewDimensions()
```

### shouldIgnorePointer

```dart
bool get shouldIgnorePointer
```

### isScrolling

```dart
bool get isScrolling
```

### velocity

```dart
double get velocity
```

# ScrollHoldController

```dart
abstract class ScrollHoldController {}
```

Interface for holding a [Scrollable] stationary.

An object that implements this interface is returned by [ScrollPosition.hold]. It holds the scrollable stationary until an activity is started or the [cancel] method is called.

### cancel()

```dart
void cancel()
```

Release the [Scrollable], potentially letting it go ballistic if necessary.

# HoldScrollActivity

```dart
class HoldScrollActivity extends ScrollActivity implements ScrollHoldController {}
```

A scroll activity that does nothing but can be released to resume normal idle behavior.

This is used while the user is touching the [Scrollable] but before the touch has become a [Drag].

For the purposes of [ScrollNotification]s, this activity does not constitute scrolling, and does not prevent the user from interacting with the contents of the [Scrollable] (unlike when a drag has begun or there is a scroll animation underway).

### HoldScrollActivity()

```dart
HoldScrollActivity({required ScrollActivityDelegate delegate, VoidCallback? onHoldCanceled})
```

Creates a scroll activity that does nothing.

### onHoldCanceled

```dart
VoidCallback? onHoldCanceled
```

Called when [dispose] is called.

### shouldIgnorePointer

```dart
bool get shouldIgnorePointer
```

### isScrolling

```dart
bool get isScrolling
```

### velocity

```dart
double get velocity
```

### cancel()

```dart
void cancel()
```

### dispose()

```dart
void dispose()
```

# ScrollDragController

```dart
class ScrollDragController implements Drag {}
```

Scrolls a scroll view as the user drags their finger across the screen.

See also:

- [DragScrollActivity], which is the activity the scroll view performs while a drag is underway.

### ScrollDragController()

```dart
ScrollDragController({required ScrollActivityDelegate delegate, required DragStartDetails details, VoidCallback? onDragCanceled, double? carriedVelocity, double? motionStartDistanceThreshold})
```

Creates an object that scrolls a scroll view as the user drags their finger across the screen.

### delegate

```dart
ScrollActivityDelegate get delegate
```

The object that will actuate the scroll view as the user drags.

### onDragCanceled

```dart
VoidCallback? onDragCanceled
```

Called when [dispose] is called.

### carriedVelocity

```dart
double? carriedVelocity
```

Velocity that was present from a previous [ScrollActivity] when this drag began.

### motionStartDistanceThreshold

```dart
double? motionStartDistanceThreshold
```

Amount of pixels in either direction the drag has to move by to start scroll movement again after each time scrolling came to a stop.

### momentumRetainStationaryDurationThreshold

```dart
Duration momentumRetainStationaryDurationThreshold
```

Maximum amount of time interval the drag can have consecutive stationary pointer update events before losing the momentum carried from a previous scroll activity.

### momentumRetainVelocityThresholdFactor

```dart
double momentumRetainVelocityThresholdFactor
```

The minimum amount of velocity needed to apply the [carriedVelocity] at the end of a drag. Expressed as a factor. For example with a [carriedVelocity] of 2000, we will need a velocity of at least 1000 to apply the [carriedVelocity] as well. If the velocity does not meet the threshold, the [carriedVelocity] is lost. Decided by fair eyeballing with the scroll_overlay platform test.

### motionStoppedDurationThreshold

```dart
Duration motionStoppedDurationThreshold
```

Maximum amount of time interval the drag can have consecutive stationary pointer update events before needing to break the [motionStartDistanceThreshold] to start motion again.

### updateDelegate()

```dart
void updateDelegate(ScrollActivityDelegate value)
```

Updates the controller's link to the [ScrollActivityDelegate].

This should only be called when a controller is being moved from a defunct (or about-to-be defunct) [ScrollActivityDelegate] object to a new one.

### update()

```dart
void update(DragUpdateDetails details)
```

### end()

```dart
void end(DragEndDetails details)
```

### cancel()

```dart
void cancel()
```

### dispose()

```dart
void dispose()
```

Called by the delegate when it is no longer sending events to this object.

### lastDetails

```dart
dynamic get lastDetails
```

The most recently observed [DragStartDetails], [DragUpdateDetails], or [DragEndDetails] object.

### toString()

```dart
String toString()
```

# DragScrollActivity

```dart
class DragScrollActivity extends ScrollActivity {}
```

The activity a scroll view performs when the user drags their finger across the screen.

See also:

- [ScrollDragController], which listens to the [Drag] and actually scrolls the scroll view.

### DragScrollActivity()

```dart
DragScrollActivity(ScrollActivityDelegate delegate, ScrollDragController controller)
```

Creates an activity for when the user drags their finger across the screen.

### dispatchScrollStartNotification()

```dart
void dispatchScrollStartNotification(ScrollMetrics metrics, BuildContext? context)
```

### dispatchScrollUpdateNotification()

```dart
void dispatchScrollUpdateNotification(ScrollMetrics metrics, BuildContext context, double scrollDelta)
```

### dispatchOverscrollNotification()

```dart
void dispatchOverscrollNotification(ScrollMetrics metrics, BuildContext context, double overscroll)
```

### dispatchScrollEndNotification()

```dart
void dispatchScrollEndNotification(ScrollMetrics metrics, BuildContext context)
```

### shouldIgnorePointer

```dart
bool get shouldIgnorePointer
```

### isScrolling

```dart
bool get isScrolling
```

### velocity

```dart
double get velocity
```

### dispose()

```dart
void dispose()
```

### toString()

```dart
String toString()
```

# BallisticScrollActivity

```dart
class BallisticScrollActivity extends ScrollActivity {}
```

The activity a scroll view performs after being set into motion.

For example, a [BallisticScrollActivity] is used when the user lifts their finger off the screen after a [DragScrollActivity], to continue the scrolling motion starting from the current velocity.

[BallisticScrollActivity] is also used to restore a scroll view to a valid scroll offset when the geometry of the scroll view changes. In these situations, the [Simulation] typically starts with a zero velocity.

The scrolling will be driven by the given [Simulation]. If a [BallisticScrollActivity] is in progress when the scroll metrics change, then the activity will be replaced with a new ballistic activity starting from the current velocity (see [ScrollPhysics.createBallisticSimulation]). To ensure the user perceives smooth motion across such a change, the simulation should typically be the result of [ScrollPhysics.createBallisticSimulation] for the scroll physics of the scroll view.

See also:

- [DrivenScrollActivity], which drives a scroll view through a given animation, without resetting to a ballistic simulation when scroll metrics change.

### BallisticScrollActivity()

```dart
BallisticScrollActivity(ScrollActivityDelegate delegate, Simulation simulation, TickerProvider vsync, bool shouldIgnorePointer)
```

Creates an activity that sets into motion a scroll view.

The simulation should typically be the result of [ScrollPhysics.createBallisticSimulation] for the scroll physics of the scroll view.

### resetActivity()

```dart
void resetActivity()
```

### applyNewDimensions()

```dart
void applyNewDimensions()
```

### applyMoveTo()

```dart
bool applyMoveTo(double value)
```

Move the position to the given location.

If the new position was fully applied, returns true. If there was any overflow, returns false.

The default implementation calls [ScrollActivityDelegate.setPixels] and returns true if the overflow was zero.

### dispatchOverscrollNotification()

```dart
void dispatchOverscrollNotification(ScrollMetrics metrics, BuildContext context, double overscroll)
```

### shouldIgnorePointer

```dart
bool shouldIgnorePointer
```

### isScrolling

```dart
bool get isScrolling
```

### velocity

```dart
double get velocity
```

### dispose()

```dart
void dispose()
```

### toString()

```dart
String toString()
```

# DrivenScrollActivity

```dart
class DrivenScrollActivity extends ScrollActivity {}
```

An activity that drives a scroll view through a given animation.

For example, a [DrivenScrollActivity] is used to implement [ScrollController.animateTo].

The scrolling will be driven by the given animation parameters or the given [Simulation].

Unlike a [BallisticScrollActivity], if a [DrivenScrollActivity] is in progress when the scroll metrics change, the activity will continue with its original animation.

See also:

- [BallisticScrollActivity], which sets into motion a scroll view.

### DrivenScrollActivity()

```dart
DrivenScrollActivity(ScrollActivityDelegate delegate, {required double from, required double to, required Duration duration, required Curve curve, required TickerProvider vsync})
```

Creates an activity that drives a scroll view through an animation given by animation parameters.

### DrivenScrollActivity.simulation()

```dart
DrivenScrollActivity.simulation(ScrollActivityDelegate delegate, Simulation simulation, {required TickerProvider vsync})
```

Creates an activity that drives a scroll view through an animation given by a [Simulation].

### done

```dart
Future<void> get done
```

A [Future] that completes when the activity stops.

For example, this [Future] will complete if the animation reaches the end or if the user interacts with the scroll view in way that causes the animation to stop before it reaches the end.

### applyMoveTo()

```dart
bool applyMoveTo(double value)
```

Move the position to the given location.

If the new position was fully applied, returns true. If there was any overflow, returns false.

The default implementation calls [ScrollActivityDelegate.setPixels] and returns true if the overflow was zero.

### dispatchOverscrollNotification()

```dart
void dispatchOverscrollNotification(ScrollMetrics metrics, BuildContext context, double overscroll)
```

### shouldIgnorePointer

```dart
bool get shouldIgnorePointer
```

### isScrolling

```dart
bool get isScrolling
```

### velocity

```dart
double get velocity
```

### dispose()

```dart
void dispose()
```

### toString()

```dart
String toString()
```
