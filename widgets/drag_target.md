@docImport 'scrollable.dart';

# DragTargetWillAccept

```dart
typedef DragTargetWillAccept<T> = bool Function(T? data)
```

Signature for determining whether the given data will be accepted by a [DragTarget].

Used by [DragTarget.onWillAccept].

# DragTargetWillAcceptWithDetails

```dart
typedef DragTargetWillAcceptWithDetails<T> = bool Function(DragTargetDetails<T> details)
```

Signature for determining whether the given data will be accepted by a [DragTarget], based on provided information.

Used by [DragTarget.onWillAcceptWithDetails].

# DragTargetAccept

```dart
typedef DragTargetAccept<T> = void Function(T data)
```

Signature for causing a [DragTarget] to accept the given data.

Used by [DragTarget.onAccept].

# DragTargetAcceptWithDetails

```dart
typedef DragTargetAcceptWithDetails<T> = void Function(DragTargetDetails<T> details)
```

Signature for determining information about the acceptance by a [DragTarget].

Used by [DragTarget.onAcceptWithDetails].

# DragTargetBuilder

```dart
typedef DragTargetBuilder<T> = Widget Function(BuildContext context, List<T?> candidateData, List<dynamic> rejectedData)
```

Signature for building children of a [DragTarget].

The `candidateData` argument contains the list of drag data that is hovering over this [DragTarget] and that has passed [DragTarget.onWillAcceptWithDetails]. The `rejectedData` argument contains the list of drag data that is hovering over this [DragTarget] and that will not be accepted by the [DragTarget].

Used by [DragTarget.builder].

# DragUpdateCallback

```dart
typedef DragUpdateCallback = void Function(DragUpdateDetails details)
```

Signature for when a [Draggable] is dragged across the screen.

Used by [Draggable.onDragUpdate].

# DraggableCanceledCallback

```dart
typedef DraggableCanceledCallback = void Function(Velocity velocity, Offset offset)
```

Signature for when a [Draggable] is dropped without being accepted by a [DragTarget].

Used by [Draggable.onDraggableCanceled].

# DragEndCallback

```dart
typedef DragEndCallback = void Function(DraggableDetails details)
```

Signature for when the draggable is dropped.

The velocity and offset at which the pointer was moving when the draggable was dropped is available in the [DraggableDetails]. Also included in the `details` is whether the draggable's [DragTarget] accepted it.

Used by [Draggable.onDragEnd].

# DragTargetLeave

```dart
typedef DragTargetLeave<T> = void Function(T? data)
```

Signature for when a [Draggable] leaves a [DragTarget].

Used by [DragTarget.onLeave].

# DragTargetMove

```dart
typedef DragTargetMove<T> = void Function(DragTargetDetails<T> details)
```

Signature for when a [Draggable] moves within a [DragTarget].

Used by [DragTarget.onMove].

# DragAnchorStrategy

```dart
typedef DragAnchorStrategy = Offset Function(Draggable<Object> draggable, BuildContext context, Offset position)
```

Signature for the strategy that determines the drag start point of a [Draggable].

Used by [Draggable.dragAnchorStrategy].

There are two built-in strategies:

- [childDragAnchorStrategy], which displays the feedback anchored at the position of the original child.

- [pointerDragAnchorStrategy], which displays the feedback anchored at the position of the touch that started the drag.

# childDragAnchorStrategy()

```dart
Offset childDragAnchorStrategy(Draggable<Object> draggable, BuildContext context, Offset position)
```

Display the feedback anchored at the position of the original child.

If feedback is identical to the child, then this means the feedback will exactly overlap the original child when the drag starts.

This is the default [DragAnchorStrategy].

See also:

- [DragAnchorStrategy], the typedef that this function implements.
- [Draggable.dragAnchorStrategy], for which this is a built-in value.

# pointerDragAnchorStrategy()

```dart
Offset pointerDragAnchorStrategy(Draggable<Object> draggable, BuildContext context, Offset position)
```

Display the feedback anchored at the position of the touch that started the drag.

If feedback is identical to the child, then this means the top left of the feedback will be under the finger when the drag starts. This will likely not exactly overlap the original child, e.g. if the child is big and the touch was not centered. This mode is useful when the feedback is transformed so as to move the feedback to the left by half its width, and up by half its width plus the height of the finger, since then it appears as if putting the finger down makes the touch feedback appear above the finger. (It feels weird for it to appear offset from the original child if it's anchored to the child and not the finger.)

See also:

- [DragAnchorStrategy], the typedef that this function implements.
- [Draggable.dragAnchorStrategy], for which this is a built-in value.

# Draggable

```dart
class Draggable<T extends Object> extends StatefulWidget {}
```

A widget that can be dragged from to a [DragTarget].

When a draggable widget recognizes the start of a drag gesture, it displays a [feedback] widget that tracks the user's finger across the screen. If the user lifts their finger while on top of a [DragTarget], that target is given the opportunity to accept the [data] carried by the draggable.

The [ignoringFeedbackPointer] defaults to true, which means that the [feedback] widget ignores the pointer during hit testing. Similarly, [ignoringFeedbackSemantics] defaults to true, and the [feedback] also ignores semantics when building the semantics tree.

On multitouch devices, multiple drags can occur simultaneously because there can be multiple pointers in contact with the device at once. To limit the number of simultaneous drags, use the [maxSimultaneousDrags] property. The default is to allow an unlimited number of simultaneous drags.

This widget displays [child] when zero drags are under way. If [childWhenDragging] is non-null, this widget instead displays [childWhenDragging] when one or more drags are underway. Otherwise, this widget always displays [child].

{@youtube 560 315 https://www.youtube.com/watch?v=q4x2G_9-Mu0}

{@tool dartpad} The following example has a [Draggable] widget along with a [DragTarget] in a row demonstrating an incremented `acceptedData` integer value when you drag the element to the target.

** See code in examples/api/lib/widgets/drag_target/draggable.0.dart ** {@end-tool}

See also:

- [DragTarget]
- [LongPressDraggable]

### Draggable()

```dart
Draggable({dynamic key, required Widget child, required Widget feedback, T? data, Axis? axis, Widget? childWhenDragging, Offset feedbackOffset = Offset.zero, DragAnchorStrategy dragAnchorStrategy = childDragAnchorStrategy, Axis? affinity, int? maxSimultaneousDrags, VoidCallback? onDragStarted, DragUpdateCallback? onDragUpdate, DraggableCanceledCallback? onDraggableCanceled, DragEndCallback? onDragEnd, VoidCallback? onDragCompleted, bool ignoringFeedbackSemantics = true, bool ignoringFeedbackPointer = true, bool rootOverlay = false, HitTestBehavior hitTestBehavior = HitTestBehavior.deferToChild, AllowedButtonsFilter? allowedButtonsFilter})
```

Creates a widget that can be dragged to a [DragTarget].

If [maxSimultaneousDrags] is non-null, it must be non-negative.

### data

```dart
T? data
```

The data that will be dropped by this draggable.

### axis

```dart
Axis? axis
```

The [Axis] to restrict this draggable's movement, if specified.

When axis is set to [Axis.horizontal], this widget can only be dragged horizontally. Behavior is similar for [Axis.vertical].

Defaults to allowing drag on both [Axis.horizontal] and [Axis.vertical].

When null, allows drag on both [Axis.horizontal] and [Axis.vertical].

For the direction of gestures this widget competes with to start a drag event, see [Draggable.affinity].

### child

```dart
Widget child
```

The widget below this widget in the tree.

This widget displays [child] when zero drags are under way. If [childWhenDragging] is non-null, this widget instead displays [childWhenDragging] when one or more drags are underway. Otherwise, this widget always displays [child].

The [feedback] widget is shown under the pointer when a drag is under way.

To limit the number of simultaneous drags on multitouch devices, see [maxSimultaneousDrags].

{@macro flutter.widgets.ProxyWidget.child}

### childWhenDragging

```dart
Widget? childWhenDragging
```

The widget to display instead of [child] when one or more drags are under way.

If this is null, then this widget will always display [child] (and so the drag source representation will not change while a drag is under way).

The [feedback] widget is shown under the pointer when a drag is under way.

To limit the number of simultaneous drags on multitouch devices, see [maxSimultaneousDrags].

### feedback

```dart
Widget feedback
```

The widget to show under the pointer when a drag is under way.

See [child] and [childWhenDragging] for information about what is shown at the location of the [Draggable] itself when a drag is under way.

### feedbackOffset

```dart
Offset feedbackOffset
```

The feedbackOffset can be used to set the hit test target point for the purposes of finding a drag target. It is especially useful if the feedback is transformed compared to the child.

### dragAnchorStrategy

```dart
DragAnchorStrategy dragAnchorStrategy
```

A strategy that is used by this draggable to get the anchor offset when it is dragged.

The anchor offset refers to the distance between the users' fingers and the [feedback] widget when this draggable is dragged.

This property's value is a function that implements [DragAnchorStrategy]. There are two built-in functions that can be used:

- [childDragAnchorStrategy], which displays the feedback anchored at the position of the original child.

- [pointerDragAnchorStrategy], which displays the feedback anchored at the position of the touch that started the drag.

Defaults to [childDragAnchorStrategy].

### ignoringFeedbackSemantics

```dart
bool ignoringFeedbackSemantics
```

Whether the semantics of the [feedback] widget is ignored when building the semantics tree.

This value should be set to false when the [feedback] widget is intended to be the same object as the [child]. Placing a [GlobalKey] on this widget will ensure semantic focus is kept on the element as it moves in and out of the feedback position.

Defaults to true.

### ignoringFeedbackPointer

```dart
bool ignoringFeedbackPointer
```

Whether the [feedback] widget is ignored during hit testing.

Regardless of whether this widget is ignored during hit testing, it will still consume space during layout and be visible during painting.

Defaults to true.

### affinity

```dart
Axis? affinity
```

Controls how this widget competes with other gestures to initiate a drag.

If affinity is null, this widget initiates a drag as soon as it recognizes a tap down gesture, regardless of any directionality. If affinity is horizontal (or vertical), then this widget will compete with other horizontal (or vertical, respectively) gestures.

For example, if this widget is placed in a vertically scrolling region and has horizontal affinity, pointer motion in the vertical direction will result in a scroll and pointer motion in the horizontal direction will result in a drag. Conversely, if the widget has a null or vertical affinity, pointer motion in any direction will result in a drag rather than in a scroll because the draggable widget, being the more specific widget, will out-compete the [Scrollable] for vertical gestures.

For the directions this widget can be dragged in after the drag event starts, see [Draggable.axis].

### maxSimultaneousDrags

```dart
int? maxSimultaneousDrags
```

How many simultaneous drags to support.

When null, no limit is applied. Set this to 1 if you want to only allow the drag source to have one item dragged at a time. Set this to 0 if you want to prevent the draggable from actually being dragged.

If you set this property to 1, consider supplying an "empty" widget for [childWhenDragging] to create the illusion of actually moving [child].

### onDragStarted

```dart
VoidCallback? onDragStarted
```

Called when the draggable starts being dragged.

### onDragUpdate

```dart
DragUpdateCallback? onDragUpdate
```

Called when the draggable is dragged.

This function will only be called while this widget is still mounted to the tree (i.e. [State.mounted] is true), and if this widget has actually moved.

### onDraggableCanceled

```dart
DraggableCanceledCallback? onDraggableCanceled
```

Called when the draggable is dropped without being accepted by a [DragTarget].

This function might be called after this widget has been removed from the tree. For example, if a drag was in progress when this widget was removed from the tree and the drag ended up being canceled, this callback will still be called. For this reason, implementations of this callback might need to check [State.mounted] to check whether the state receiving the callback is still in the tree.

### onDragCompleted

```dart
VoidCallback? onDragCompleted
```

Called when the draggable is dropped and accepted by a [DragTarget].

This function might be called after this widget has been removed from the tree. For example, if a drag was in progress when this widget was removed from the tree and the drag ended up completing, this callback will still be called. For this reason, implementations of this callback might need to check [State.mounted] to check whether the state receiving the callback is still in the tree.

### onDragEnd

```dart
DragEndCallback? onDragEnd
```

Called when the draggable is dropped.

The velocity and offset at which the pointer was moving when it was dropped is available in the [DraggableDetails]. Also included in the `details` is whether the draggable's [DragTarget] accepted it.

This function will only be called while this widget is still mounted to the tree (i.e. [State.mounted] is true).

### rootOverlay

```dart
bool rootOverlay
```

Whether the feedback widget will be put on the root [Overlay].

When false, the feedback widget will be put on the closest [Overlay]. When true, the [feedback] widget will be put on the farthest (aka root) [Overlay].

Defaults to false.

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

How to behave during hit test.

Defaults to [HitTestBehavior.deferToChild].

### allowedButtonsFilter

```dart
AllowedButtonsFilter? allowedButtonsFilter
```

{@macro flutter.gestures.multidrag._allowedButtonsFilter}

### createRecognizer()

```dart
MultiDragGestureRecognizer createRecognizer(GestureMultiDragStartCallback onStart)
```

Creates a gesture recognizer that recognizes the start of the drag.

Subclasses can override this function to customize when they start recognizing a drag.

### createState()

```dart
State<Draggable<T>> createState()
```

# LongPressDraggable

```dart
class LongPressDraggable<T extends Object> extends Draggable<T> {}
```

Makes its child draggable starting from long press.

See also:

- [Draggable], similar to the [LongPressDraggable] widget but happens immediately.
- [DragTarget], a widget that receives data when a [Draggable] widget is dropped.

### LongPressDraggable()

```dart
LongPressDraggable({dynamic key, required Widget child, required Widget feedback, T? data, dynamic axis, Widget? childWhenDragging, dynamic feedbackOffset, InvalidType Function(Draggable<Object>, BuildContext, InvalidType) dragAnchorStrategy, int? maxSimultaneousDrags, dynamic onDragStarted, void Function(InvalidType)? onDragUpdate, void Function(InvalidType, InvalidType)? onDraggableCanceled, void Function(DraggableDetails)? onDragEnd, dynamic onDragCompleted, bool hapticFeedbackOnStart = true, bool ignoringFeedbackSemantics, bool ignoringFeedbackPointer, Duration delay = kLongPressTimeout, dynamic allowedButtonsFilter, dynamic hitTestBehavior, bool rootOverlay})
```

Creates a widget that can be dragged starting from long press.

If [maxSimultaneousDrags] is non-null, it must be non-negative.

### hapticFeedbackOnStart

```dart
bool hapticFeedbackOnStart
```

Whether haptic feedback should be triggered on drag start.

### delay

```dart
Duration delay
```

The duration that a user has to press down before a long press is registered.

Defaults to [kLongPressTimeout].

### createRecognizer()

```dart
DelayedMultiDragGestureRecognizer createRecognizer(GestureMultiDragStartCallback onStart)
```

# DraggableDetails

```dart
class DraggableDetails {}
```

Represents the details when a specific pointer event occurred on the [Draggable].

This includes the [Velocity] at which the pointer was moving and [Offset] when the draggable event occurred, and whether its [DragTarget] accepted it.

Also, this is the details object for callbacks that use [DragEndCallback].

### DraggableDetails()

```dart
DraggableDetails({bool wasAccepted = false, required Velocity velocity, required Offset offset})
```

Creates details for a [DraggableDetails].

If [wasAccepted] is not specified, it will default to `false`.

The [velocity] or [offset] arguments must not be `null`.

### wasAccepted

```dart
bool wasAccepted
```

Determines whether the [DragTarget] accepted this draggable.

### velocity

```dart
Velocity velocity
```

The velocity at which the pointer was moving when the specific pointer event occurred on the draggable.

### offset

```dart
Offset offset
```

The global position when the specific pointer event occurred on the draggable.

# DragTargetDetails

```dart
class DragTargetDetails<T> {}
```

Represents the details when a pointer event occurred on the [DragTarget].

### DragTargetDetails()

```dart
DragTargetDetails({required T data, required Offset offset})
```

Creates details for a [DragTarget] callback.

### data

```dart
T data
```

The data that was dropped onto this [DragTarget].

### offset

```dart
Offset offset
```

The global position when the specific pointer event occurred on the draggable.

# DragTarget

```dart
class DragTarget<T extends Object> extends StatefulWidget {}
```

A widget that receives data when a [Draggable] widget is dropped.

When a draggable is dragged on top of a drag target, the drag target is asked whether it will accept the data the draggable is carrying. If the user does drop the draggable on top of the drag target (and the drag target has indicated that it will accept the draggable's data), then the drag target is asked to accept the draggable's data.

See also:

- [Draggable]
- [LongPressDraggable]

### DragTarget()

```dart
DragTarget({dynamic key, required DragTargetBuilder<T> builder, DragTargetWillAccept<T>? onWillAccept, DragTargetWillAcceptWithDetails<T>? onWillAcceptWithDetails, DragTargetAccept<T>? onAccept, DragTargetAcceptWithDetails<T>? onAcceptWithDetails, DragTargetLeave<T>? onLeave, DragTargetMove<T>? onMove, HitTestBehavior hitTestBehavior = HitTestBehavior.translucent})
```

Creates a widget that receives drags.

### builder

```dart
DragTargetBuilder<T> builder
```

Called to build the contents of this widget.

The builder can build different widgets depending on what is being dragged into this drag target.

[onWillAccept] or [onWillAcceptWithDetails] is called when a draggable enters the target. If true, then the data will appear in `candidateData`, else in `rejectedData`.

Typically the builder will check `candidateData` and `rejectedData` and build a widget that indicates the result of dropping the `candidateData` onto this target.

The `candidateData` and `rejectedData` are [List] types to support multiple simultaneous drags.

If unexpected `null` values in `candidateData` or `rejectedData`, ensure that the `data` argument of the [Draggable] is not `null`.

### onWillAccept

```dart
DragTargetWillAccept<T>? onWillAccept
```

Called to determine whether this widget is interested in receiving a given piece of data being dragged over this drag target.

Called when a piece of data enters the target. This will be followed by either [onAccept] and [onAcceptWithDetails], if the data is dropped, or [onLeave], if the drag leaves the target.

Equivalent to [onWillAcceptWithDetails], but only includes the data.

Must not be provided if [onWillAcceptWithDetails] is provided.

### onWillAcceptWithDetails

```dart
DragTargetWillAcceptWithDetails<T>? onWillAcceptWithDetails
```

Called to determine whether this widget is interested in receiving a given piece of data being dragged over this drag target.

Called when a piece of data enters the target. This will be followed by either [onAccept] and [onAcceptWithDetails], if the data is dropped, or [onLeave], if the drag leaves the target.

Equivalent to [onWillAccept], but with information, including the data, in a [DragTargetDetails].

Must not be provided if [onWillAccept] is provided.

### onAccept

```dart
DragTargetAccept<T>? onAccept
```

Called when an acceptable piece of data was dropped over this drag target. It will not be called if `data` is `null`.

Equivalent to [onAcceptWithDetails], but only includes the data.

### onAcceptWithDetails

```dart
DragTargetAcceptWithDetails<T>? onAcceptWithDetails
```

Called when an acceptable piece of data was dropped over this drag target. It will not be called if `data` is `null`.

Equivalent to [onAccept], but with information, including the data, in a [DragTargetDetails].

### onLeave

```dart
DragTargetLeave<T>? onLeave
```

Called when a given piece of data being dragged over this target leaves the target.

### onMove

```dart
DragTargetMove<T>? onMove
```

Called when a [Draggable] moves within this [DragTarget]. It will not be called if `data` is `null`.

This includes entering and leaving the target.

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

How to behave during hit testing.

Defaults to [HitTestBehavior.translucent].

### createState()

```dart
State<DragTarget<T>> createState()
```
