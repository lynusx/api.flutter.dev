@docImport 'editable_text.dart'; @docImport 'scroll_view.dart'; @docImport 'table.dart';

# InteractiveViewerWidgetBuilder

```dart
typedef InteractiveViewerWidgetBuilder = Widget Function(BuildContext context, Quad viewport)
```

A signature for widget builders that take a [Quad] of the current viewport.

See also:

- [InteractiveViewer.builder], whose builder is of this type.
- [WidgetBuilder], which is similar, but takes no viewport.

# InteractiveViewer

```dart
class InteractiveViewer extends StatefulWidget {}
```

A widget that enables pan and zoom interactions with its child.

{@youtube 560 315 https://www.youtube.com/watch?v=zrn7V3bMJvg}

The user can transform the child by dragging to pan or pinching to zoom.

By default, InteractiveViewer clips its child using [Clip.hardEdge]. To prevent this behavior, consider setting [clipBehavior] to [Clip.none]. When [clipBehavior] is [Clip.none], InteractiveViewer may draw outside of its original area of the screen, such as when a child is zoomed in and increases in size. However, it will not receive gestures outside of its original area. To prevent dead areas where InteractiveViewer does not receive gestures, don't set [clipBehavior] or be sure that the InteractiveViewer widget is the size of the area that should be interactive.

See also:

- The [Flutter Gallery's transformations demo](https://github.com/flutter/gallery/blob/main/lib/demos/reference/transformations_demo.dart), which includes the use of InteractiveViewer.
- The [flutter-go demo](https://github.com/justinmc/flutter-go), which includes robust positioning of an InteractiveViewer child that works for all screen sizes and child sizes.
- The [Lazy Flutter Performance Session](https://www.youtube.com/watch?v=qax_nOpgz7E), which includes the use of an InteractiveViewer to performantly view subsets of a large set of widgets using the builder constructor.

{@tool dartpad} This example shows a simple Container that can be panned and zoomed.

** See code in examples/api/lib/widgets/interactive_viewer/interactive_viewer.0.dart ** {@end-tool}

### InteractiveViewer()

```dart
InteractiveViewer({dynamic key, Clip clipBehavior = Clip.hardEdge, PanAxis panAxis = PanAxis.free, EdgeInsets boundaryMargin = EdgeInsets.zero, bool constrained = true, double maxScale = 2.5, double minScale = 0.8, double interactionEndFrictionCoefficient = _kDrag, GestureScaleEndCallback? onInteractionEnd, GestureScaleStartCallback? onInteractionStart, GestureScaleUpdateCallback? onInteractionUpdate, bool panEnabled = true, bool scaleEnabled = true, double scaleFactor = kDefaultMouseScrollToScaleFactor, TransformationController? transformationController, Alignment? alignment, bool trackpadScrollCausesScale = false, required Widget? child})
```

Create an InteractiveViewer.

### InteractiveViewer.builder()

```dart
InteractiveViewer.builder({dynamic key, Clip clipBehavior = Clip.hardEdge, PanAxis panAxis = PanAxis.free, EdgeInsets boundaryMargin = EdgeInsets.zero, double maxScale = 2.5, double minScale = 0.8, double interactionEndFrictionCoefficient = _kDrag, GestureScaleEndCallback? onInteractionEnd, GestureScaleStartCallback? onInteractionStart, GestureScaleUpdateCallback? onInteractionUpdate, bool panEnabled = true, bool scaleEnabled = true, double scaleFactor = 200.0, TransformationController? transformationController, Alignment? alignment, bool trackpadScrollCausesScale = false, required InteractiveViewerWidgetBuilder? builder})
```

Creates an InteractiveViewer for a child that is created on demand.

Can be used to render a child that changes in response to the current transformation.

See the [builder] attribute docs for an example of using it to optimize a large child.

### alignment

```dart
Alignment? alignment
```

The alignment of the child's origin, relative to the size of the box.

### clipBehavior

```dart
Clip clipBehavior
```

If set to [Clip.none], the child may extend beyond the size of the InteractiveViewer, but it will not receive gestures in these areas. Be sure that the InteractiveViewer is the desired size when using [Clip.none].

Defaults to [Clip.hardEdge].

### panAxis

```dart
PanAxis panAxis
```

When set to [PanAxis.aligned], panning is only allowed in the horizontal axis or the vertical axis, diagonal panning is not allowed.

When set to [PanAxis.vertical] or [PanAxis.horizontal] panning is only allowed in the specified axis. For example, if set to [PanAxis.vertical], panning will only be allowed in the vertical axis. And if set to [PanAxis.horizontal], panning will only be allowed in the horizontal axis.

When set to [PanAxis.free] panning is allowed in all directions.

Defaults to [PanAxis.free].

### boundaryMargin

```dart
EdgeInsets boundaryMargin
```

A margin for the visible boundaries of the child.

Any transformation that results in the viewport being able to view outside of the boundaries will be stopped at the boundary. The boundaries do not rotate with the rest of the scene, so they are always aligned with the viewport.

To produce no boundaries at all, pass infinite [EdgeInsets], such as `EdgeInsets.all(double.infinity)`.

No edge can be NaN.

Defaults to [EdgeInsets.zero], which results in boundaries that are the exact same size and position as the [child].

### builder

```dart
InteractiveViewerWidgetBuilder? builder
```

Builds the child of this widget.

Passed with the [InteractiveViewer.builder] constructor. Otherwise, the [child] parameter must be passed directly, and this is null.

{@tool dartpad} This example shows how to use builder to create a [Table] whose cell contents are only built when they are visible. Built and remove cells are logged in the console for illustration.

** See code in examples/api/lib/widgets/interactive_viewer/interactive_viewer.builder.0.dart ** {@end-tool}

See also:

- [ListView.builder], which follows a similar pattern.

### child

```dart
Widget? child
```

The child [Widget] that is transformed by InteractiveViewer.

If the [InteractiveViewer.builder] constructor is used, then this will be null, otherwise it is required.

### constrained

```dart
bool constrained
```

Whether the normal size constraints at this point in the widget tree are applied to the child.

If set to false, then the child will be given infinite constraints. This is often useful when a child should be bigger than the InteractiveViewer.

For example, for a child which is bigger than the viewport but can be panned to reveal parts that were initially offscreen, [constrained] must be set to false to allow it to size itself properly. If [constrained] is true and the child can only size itself to the viewport, then areas initially outside of the viewport will not be able to receive user interaction events. If experiencing regions of the child that are not receptive to user gestures, make sure [constrained] is false and the child is sized properly.

Defaults to true.

{@tool dartpad} This example shows how to create a pannable table. Because the table is larger than the entire screen, setting [constrained] to false is necessary to allow it to be drawn to its full size. The parts of the table that exceed the screen size can then be panned into view.

** See code in examples/api/lib/widgets/interactive_viewer/interactive_viewer.constrained.0.dart ** {@end-tool}

### panEnabled

```dart
bool panEnabled
```

If false, the user will be prevented from panning.

Defaults to true.

See also:

- [scaleEnabled], which is similar but for scale.

### scaleEnabled

```dart
bool scaleEnabled
```

If false, the user will be prevented from scaling.

Defaults to true.

See also:

- [panEnabled], which is similar but for panning.

### trackpadScrollCausesScale

```dart
bool trackpadScrollCausesScale
```

{@macro flutter.gestures.scale.trackpadScrollCausesScale}

### scaleFactor

```dart
double scaleFactor
```

Determines the amount of scale to be performed per pointer scroll.

Defaults to [kDefaultMouseScrollToScaleFactor].

Increasing this value above the default causes scaling to feel slower, while decreasing it causes scaling to feel faster.

The amount of scale is calculated as the exponential function of the [PointerScrollEvent.scrollDelta] to [scaleFactor] ratio. In the Flutter engine, the mousewheel [PointerScrollEvent.scrollDelta] is hardcoded to 20 per scroll, while a trackpad scroll can be any amount.

Affects only pointer device scrolling, not pinch to zoom.

### maxScale

```dart
double maxScale
```

The maximum allowed scale.

The scale will be clamped between this and [minScale] inclusively.

Defaults to 2.5.

Must be greater than zero and greater than [minScale].

### minScale

```dart
double minScale
```

The minimum allowed scale.

The scale will be clamped between this and [maxScale] inclusively.

Scale is also affected by [boundaryMargin]. If the scale would result in viewing beyond the boundary, then it will not be allowed. By default, boundaryMargin is EdgeInsets.zero, so scaling below 1.0 will not be allowed in most cases without first increasing the boundaryMargin.

Defaults to 0.8.

Must be a finite number greater than zero and less than [maxScale].

### interactionEndFrictionCoefficient

```dart
double interactionEndFrictionCoefficient
```

Changes the deceleration behavior after a gesture.

Defaults to 0.0000135.

Must be a finite number greater than zero.

### onInteractionEnd

```dart
GestureScaleEndCallback? onInteractionEnd
```

Called when the user ends a pan or scale gesture on the widget.

At the time this is called, the [TransformationController] will have already been updated to reflect the change caused by the interaction, though a pan may cause an inertia animation after this is called as well.

{@template flutter.widgets.InteractiveViewer.onInteractionEnd} Will be called even if the interaction is disabled with [panEnabled] or [scaleEnabled] for both touch gestures and mouse interactions.

A [GestureDetector] wrapping the InteractiveViewer will not respond to [GestureDetector.onScaleStart], [GestureDetector.onScaleUpdate], and [GestureDetector.onScaleEnd]. Use [onInteractionStart], [onInteractionUpdate], and [onInteractionEnd] to respond to those gestures. {@endtemplate}

See also:

- [onInteractionStart], which handles the start of the same interaction.
- [onInteractionUpdate], which handles an update to the same interaction.

### onInteractionStart

```dart
GestureScaleStartCallback? onInteractionStart
```

Called when the user begins a pan or scale gesture on the widget.

At the time this is called, the [TransformationController] will not have changed due to this interaction.

{@macro flutter.widgets.InteractiveViewer.onInteractionEnd}

The coordinates provided in the details' `focalPoint` and `localFocalPoint` are normal Flutter event coordinates, not InteractiveViewer scene coordinates. See [TransformationController.toScene] for how to convert these coordinates to scene coordinates relative to the child.

See also:

- [onInteractionUpdate], which handles an update to the same interaction.
- [onInteractionEnd], which handles the end of the same interaction.

### onInteractionUpdate

```dart
GestureScaleUpdateCallback? onInteractionUpdate
```

Called when the user updates a pan or scale gesture on the widget.

At the time this is called, the [TransformationController] will have already been updated to reflect the change caused by the interaction, if the interaction caused the matrix to change.

{@macro flutter.widgets.InteractiveViewer.onInteractionEnd}

The coordinates provided in the details' `focalPoint` and `localFocalPoint` are normal Flutter event coordinates, not InteractiveViewer scene coordinates. See [TransformationController.toScene] for how to convert these coordinates to scene coordinates relative to the child.

See also:

- [onInteractionStart], which handles the start of the same interaction.
- [onInteractionEnd], which handles the end of the same interaction.

### transformationController

```dart
TransformationController? transformationController
```

A [TransformationController] for the transformation performed on the child.

Whenever the child is transformed, the [Matrix4] value is updated and all listeners are notified. If the value is set, InteractiveViewer will update to respect the new value.

{@tool dartpad} This example shows how transformationController can be used to animate the transformation back to its starting position.

** See code in examples/api/lib/widgets/interactive_viewer/interactive_viewer.transformation_controller.0.dart ** {@end-tool}

See also:

- [ValueNotifier], the parent class of TransformationController.
- [TextEditingController] for an example of another similar pattern.

### getNearestPointOnLine()

```dart
Vector3 getNearestPointOnLine(Vector3 point, Vector3 l1, Vector3 l2)
```

Returns the closest point to the given point on the given line segment.

### getAxisAlignedBoundingBox()

```dart
Quad getAxisAlignedBoundingBox(Quad quad)
```

Given a quad, return its axis aligned bounding box.

### pointIsInside()

```dart
bool pointIsInside(Vector3 point, Quad quad)
```

Returns true iff the point is inside the rectangle given by the Quad, inclusively. Algorithm from https://math.stackexchange.com/a/190373.

### getNearestPointInside()

```dart
Vector3 getNearestPointInside(Vector3 point, Quad quad)
```

Get the point inside (inclusively) the given Quad that is nearest to the given Vector3.

### createState()

```dart
State<InteractiveViewer> createState()
```

# TransformationController

```dart
class TransformationController extends ValueNotifier<Matrix4> {}
```

A thin wrapper on [ValueNotifier] whose value is a [Matrix4] representing a transformation.

The [value] defaults to the identity matrix, which corresponds to no transformation.

See also:

- [InteractiveViewer.transformationController] for detailed documentation on how to use TransformationController with [InteractiveViewer].

### TransformationController()

```dart
TransformationController([Matrix4? value])
```

Create an instance of [TransformationController].

The [value] defaults to the identity matrix, which corresponds to no transformation.

### toScene()

```dart
Offset toScene(Offset viewportPoint)
```

Return the scene point at the given viewport point.

A viewport point is relative to the parent while a scene point is relative to the child, regardless of transformation. Calling toScene with a viewport point essentially returns the scene coordinate that lies underneath the viewport point given the transform.

The viewport transforms as the inverse of the child (i.e. moving the child left is equivalent to moving the viewport right).

This method is often useful when determining where an event on the parent occurs on the child. This example shows how to determine where a tap on the parent occurred on the child.

```dart
@override
Widget build(BuildContext context) {
  return GestureDetector(
    onTapUp: (TapUpDetails details) {
      _childWasTappedAt = _transformationController.toScene(
        details.localPosition,
      );
    },
    child: InteractiveViewer(
      transformationController: _transformationController,
      child: child,
    ),
  );
}
```

# PanAxis

```dart
enum PanAxis {}
```

This enum is used to specify the behavior of the [InteractiveViewer] when the user drags the viewport.

The user can only pan the viewport along the horizontal axis.

The user can only pan the viewport along the vertical axis.

The user can pan the viewport along the horizontal and vertical axes but not diagonally.

The user can pan the viewport freely in any direction.
