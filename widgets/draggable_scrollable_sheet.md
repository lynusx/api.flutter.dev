@docImport 'package:flutter/material.dart'; @docImport 'package:flutter_test/flutter_test.dart';

@docImport 'primary_scroll_controller.dart'; @docImport 'scroll_configuration.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'single_child_scroll_view.dart'; @docImport 'viewport.dart';

# ScrollableWidgetBuilder

```dart
typedef ScrollableWidgetBuilder = Widget Function(BuildContext context, ScrollController scrollController)
```

The signature of a method that provides a [BuildContext] and [ScrollController] for building a widget that may overflow the draggable [Axis] of the containing area.

This builder is used when a widget is expected to have a scrollable child widget, and a vertical gesture needs to trigger scrolling and some other behavior during that same gesture.

For example, users of [DraggableScrollableSheet] should apply the [scrollController] to a [ScrollView] subclass, such as a [SingleChildScrollView], [ListView] or [GridView], to have the whole sheet be draggable.

# DraggableScrollableController

```dart
class DraggableScrollableController extends ChangeNotifier {}
```

Controls a [DraggableScrollableSheet].

Draggable scrollable controllers are typically stored as member variables in [State] objects and are reused in each [State.build]. Controllers can only be used to control one sheet at a time. A controller can be reused with a new sheet if the previous sheet has been disposed.

The controller's methods cannot be used until after the controller has been passed into a [DraggableScrollableSheet] and the sheet has run initState.

A [DraggableScrollableController] is a [Listenable]. It notifies its listeners whenever an attached sheet changes sizes. It does not notify its listeners when a sheet is first attached or when an attached sheet's parameters change without affecting the sheet's current size. It does not fire when [pixels] changes without [size] changing. For example, if the constraints provided to an attached sheet change.

### DraggableScrollableController()

```dart
DraggableScrollableController()
```

Creates a controller for [DraggableScrollableSheet].

### size

```dart
double get size
```

Get the current size (as a fraction of the parent height) of the attached sheet.

### pixels

```dart
double get pixels
```

Get the current pixel height of the attached sheet.

### sizeToPixels()

```dart
double sizeToPixels(double size)
```

Convert a sheet's size (fractional value of parent container height) to pixels.

### isAttached

```dart
bool get isAttached
```

Returns Whether any [DraggableScrollableController] objects have attached themselves to the [DraggableScrollableSheet].

If this is false, then members that interact with the [ScrollPosition], such as [sizeToPixels], [size], [animateTo], and [jumpTo], must not be called.

### pixelsToSize()

```dart
double pixelsToSize(double pixels)
```

Convert a sheet's pixel height to size (fractional value of parent container height).

### animateTo()

```dart
Future<void> animateTo(double size, {required Duration duration, required Curve curve})
```

Animates the attached sheet from its current size to the given [size], a fractional value of the parent container's height.

Any active sheet animation is canceled. If the sheet's internal scrollable is currently animating (e.g. responding to a user fling), that animation is canceled as well.

An animation will be interrupted whenever the user attempts to scroll manually, whenever another activity is started, or when the sheet hits its max or min size (e.g. if you animate to 1 but the max size is .8, the animation will stop playing when it reaches .8).

The duration must not be zero. To jump to a particular value without an animation, use [jumpTo].

The sheet will not snap after calling [animateTo] even if [DraggableScrollableSheet.snap] is true. Snapping only occurs after user drags.

When calling [animateTo] in widget tests, `await`ing the returned [Future] may cause the test to hang and timeout. Instead, use [WidgetTester.pumpAndSettle].

### jumpTo()

```dart
void jumpTo(double size)
```

Jumps the attached sheet from its current size to the given [size], a fractional value of the parent container's height.

If [size] is outside of a the attached sheet's min or max child size, [jumpTo] will jump the sheet to the nearest valid size instead.

Any active sheet animation is canceled. If the sheet's inner scrollable is currently animating (e.g. responding to a user fling), that animation is canceled as well.

The sheet will not snap after calling [jumpTo] even if [DraggableScrollableSheet.snap] is true. Snapping only occurs after user drags.

### reset()

```dart
void reset()
```

Reset the attached sheet to its initial size (see: [DraggableScrollableSheet.initialChildSize]).

# DraggableScrollableSheet

```dart
class DraggableScrollableSheet extends StatefulWidget {}
```

A container for a [Scrollable] that responds to drag gestures by resizing the scrollable until a limit is reached, and then scrolling.

{@youtube 560 315 https://www.youtube.com/watch?v=Hgw819mL_78}

This widget can be dragged along the vertical axis between its [minChildSize], which defaults to `0.25` and [maxChildSize], which defaults to `1.0`. These sizes are percentages of the height of the parent container.

The widget coordinates resizing and scrolling of the widget returned by builder as the user drags along the horizontal axis.

The widget will initially be displayed at its initialChildSize which defaults to `0.5`, meaning half the height of its parent. Dragging will work between the range of minChildSize and maxChildSize (as percentages of the parent container's height) as long as the builder creates a widget which uses the provided [ScrollController]. If the widget created by the [ScrollableWidgetBuilder] does not use the provided [ScrollController], the sheet will remain at the initialChildSize.

By default, the widget will stay at whatever size the user drags it to. To make the widget snap to specific sizes whenever they lift their finger during a drag, set [snap] to `true`. The sheet will snap between [minChildSize] and [maxChildSize]. Use [snapSizes] to add more sizes for the sheet to snap between.

The snapping effect is only applied on user drags. Programmatically manipulating the sheet size via [DraggableScrollableController.animateTo] or [DraggableScrollableController.jumpTo] will ignore [snap] and [snapSizes].

By default, the widget will expand its non-occupied area to fill available space in the parent. If this is not desired, e.g. because the parent wants to position sheet based on the space it is taking, the [expand] property may be set to false.

{@tool dartpad}

This is a sample widget which shows a [ListView] that has 25 [ListTile]s. It starts out as taking up half the body of the [Scaffold], and can be dragged up to the full height of the scaffold or down to 25% of the height of the scaffold. Upon reaching full height, the list contents will be scrolled up or down, until they reach the top of the list again and the user drags the sheet back down.

On desktop and web running on desktop platforms, dragging to scroll with a mouse is disabled by default to align with the natural behavior found in other desktop applications.

This behavior is dictated by the [ScrollBehavior], and can be changed by adding [PointerDeviceKind.mouse] to [ScrollBehavior.dragDevices]. For more info on this, please refer to https://docs.flutter.dev/release/breaking-changes/default-scroll-behavior-drag

Alternatively, this example illustrates how to add a drag handle for desktop applications.

** See code in examples/api/lib/widgets/draggable_scrollable_sheet/draggable_scrollable_sheet.0.dart ** {@end-tool}

### DraggableScrollableSheet()

```dart
DraggableScrollableSheet({dynamic key, double initialChildSize = 0.5, double minChildSize = 0.25, double maxChildSize = 1.0, bool expand = true, bool snap = false, List<double>? snapSizes, Duration? snapAnimationDuration, DraggableScrollableController? controller, bool shouldCloseOnMinExtent = true, required ScrollableWidgetBuilder builder})
```

Creates a widget that can be dragged and scrolled in a single gesture.

### initialChildSize

```dart
double initialChildSize
```

The initial fractional value of the parent container's height to use when displaying the widget.

Rebuilding the sheet with a new [initialChildSize] will only move the sheet to the new value if the sheet has not yet been dragged since it was first built or since the last call to [DraggableScrollableActuator.reset].

The default value is `0.5`.

### minChildSize

```dart
double minChildSize
```

The minimum fractional value of the parent container's height to use when displaying the widget.

The default value is `0.25`.

### maxChildSize

```dart
double maxChildSize
```

The maximum fractional value of the parent container's height to use when displaying the widget.

The default value is `1.0`.

### expand

```dart
bool expand
```

Whether the widget should expand to fill the available space in its parent or not.

In most cases, this should be true. However, in the case of a parent widget that will position this one based on its desired size (such as a [Center]), this should be set to false.

The default value is true.

### snap

```dart
bool snap
```

Whether the widget should snap between [snapSizes] when the user lifts their finger during a drag.

If the user's finger was still moving when they lifted it, the widget will snap to the next snap size (see [snapSizes]) in the direction of the drag. If their finger was still, the widget will snap to the nearest snap size.

Snapping is not applied when the sheet is programmatically moved by calling [DraggableScrollableController.animateTo] or [DraggableScrollableController.jumpTo].

Rebuilding the sheet with snap newly enabled will immediately trigger a snap unless the sheet has not yet been dragged away from [initialChildSize] since first being built or since the last call to [DraggableScrollableActuator.reset].

### snapSizes

```dart
List<double>? snapSizes
```

A list of target sizes that the widget should snap to.

Snap sizes are fractional values of the parent container's height. They must be listed in increasing order and be between [minChildSize] and [maxChildSize].

The [minChildSize] and [maxChildSize] are implicitly included in snap sizes and do not need to be specified here. For example, `snapSizes = [.5]` will result in a sheet that snaps between [minChildSize], `.5`, and [maxChildSize].

Any modifications to the [snapSizes] list will not take effect until the `build` function containing this widget is run again.

Rebuilding with a modified or new list will trigger a snap unless the sheet has not yet been dragged away from [initialChildSize] since first being built or since the last call to [DraggableScrollableActuator.reset].

### snapAnimationDuration

```dart
Duration? snapAnimationDuration
```

Defines a duration for the snap animations.

If it's not set, then the animation duration is the distance to the snap target divided by the velocity of the widget.

### controller

```dart
DraggableScrollableController? controller
```

A controller that can be used to programmatically control this sheet.

### shouldCloseOnMinExtent

```dart
bool shouldCloseOnMinExtent
```

Whether the sheet, when dragged (or flung) to its minimum size, should cause its parent sheet to close.

Set on emitted [DraggableScrollableNotification]s. It is up to parent classes to properly read and handle this value.

### builder

```dart
ScrollableWidgetBuilder builder
```

The builder that creates a child to display in this widget, which will use the provided [ScrollController] to enable dragging and scrolling of the contents.

### createState()

```dart
State<DraggableScrollableSheet> createState()
```

# DraggableScrollableNotification

```dart
class DraggableScrollableNotification extends Notification with ViewportNotificationMixin {}
```

A [Notification] related to the extent, which is the size, and scroll offset, which is the position of the child list, of the [DraggableScrollableSheet].

[DraggableScrollableSheet] widgets notify their ancestors when the size of the sheet changes. When the extent of the sheet changes via a drag, this notification bubbles up through the tree, which means a given [NotificationListener] will receive notifications for all descendant [DraggableScrollableSheet] widgets. To focus on notifications from the nearest [DraggableScrollableSheet] descendant, check that the [depth] property of the notification is zero.

When an extent notification is received by a [NotificationListener], the listener will already have completed build and layout, and it is therefore too late for that widget to call [State.setState]. Any attempt to adjust the build or layout based on an extent notification would result in a layout that lagged one frame behind, which is a poor user experience. Extent notifications are used primarily to drive animations. The [Scaffold] widget listens for extent notifications and responds by driving animations for the [FloatingActionButton] as the bottom sheet scrolls up.

### DraggableScrollableNotification()

```dart
DraggableScrollableNotification({required double extent, required double minExtent, required double maxExtent, required double initialExtent, required BuildContext context, bool shouldCloseOnMinExtent = true})
```

Creates a notification that the extent of a [DraggableScrollableSheet] has changed.

All parameters are required. The [minExtent] must be >= 0. The [maxExtent] must be <= 1.0. The [extent] must be between [minExtent] and [maxExtent].

### extent

```dart
double extent
```

The current value of the extent, between [minExtent] and [maxExtent].

### minExtent

```dart
double minExtent
```

The minimum value of [extent], which is >= 0.

### maxExtent

```dart
double maxExtent
```

The maximum value of [extent].

### initialExtent

```dart
double initialExtent
```

The initially requested value for [extent].

### context

```dart
BuildContext context
```

The build context of the widget that fired this notification.

This can be used to find the sheet's render objects to determine the size of the viewport, for instance. A listener can only assume this context is live when it first gets the notification.

### shouldCloseOnMinExtent

```dart
bool shouldCloseOnMinExtent
```

Whether the widget that fired this notification, when dragged (or flung) to minExtent, should cause its parent sheet to close.

It is up to parent classes to properly read and handle this value.

### debugFillDescription()

```dart
void debugFillDescription(List<String> description)
```

# DraggableScrollableActuator

```dart
class DraggableScrollableActuator extends StatefulWidget {}
```

A widget that can notify a descendent [DraggableScrollableSheet] that it should reset its position to the initial state.

The [Scaffold] uses this widget to notify a persistent bottom sheet that the user has tapped back if the sheet has started to cover more of the body than when at its initial position. This is important for users of assistive technology, where dragging may be difficult to communicate.

This is just a wrapper on top of [DraggableScrollableController]. It is primarily useful for controlling a sheet in a part of the widget tree that the current code does not control (e.g. library code trying to affect a sheet in library users' code). Generally, it's easier to control the sheet directly by creating a controller and passing the controller to the sheet in its constructor (see [DraggableScrollableSheet.controller]).

### DraggableScrollableActuator()

```dart
DraggableScrollableActuator({dynamic key, required Widget child})
```

Creates a widget that can notify descendent [DraggableScrollableSheet]s to reset to their initial position.

The [child] parameter is required.

### child

```dart
Widget child
```

This child's [DraggableScrollableSheet] descendant will be reset when the [reset] method is applied to a context that includes it.

### reset()

```dart
bool reset(BuildContext context)
```

Notifies any descendant [DraggableScrollableSheet] that it should reset to its initial position.

Returns `true` if a [DraggableScrollableActuator] is available and some [DraggableScrollableSheet] is listening for updates, `false` otherwise.

### createState()

```dart
State<DraggableScrollableActuator> createState()
```
