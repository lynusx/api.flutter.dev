@docImport 'package:flutter/widgets.dart';

@docImport 'stack.dart';

# FlowPaintingContext

```dart
abstract class FlowPaintingContext {}
```

A context in which a [FlowDelegate] paints.

Provides information about the current size of the container and the children and a mechanism for painting children.

See also:

- [FlowDelegate]
- [Flow]
- [RenderFlow]

### size

```dart
Size get size
```

The size of the container in which the children can be painted.

### childCount

```dart
int get childCount
```

The number of children available to paint.

### getChildSize()

```dart
Size? getChildSize(int i)
```

The size of the [i]th child.

If [i] is negative or exceeds [childCount], returns null.

### paintChild()

```dart
void paintChild(int i, {Matrix4 transform, double opacity = 1.0})
```

Paint the [i]th child using the given transform.

The child will be painted in a coordinate system that concatenates the container's coordinate system with the given transform. The origin of the parent's coordinate system is the upper left corner of the parent, with x increasing rightward and y increasing downward.

The container will clip the children to its bounds.

# FlowDelegate

```dart
abstract class FlowDelegate {}
```

A delegate that controls the appearance of a flow layout.

Flow layouts are optimized for moving children around the screen using transformation matrices. For optimal performance, construct the [FlowDelegate] with an [Animation] that ticks whenever the delegate wishes to change the transformation matrices for the children and avoid rebuilding the [Flow] widget itself every animation frame.

See also:

- [Flow]
- [RenderFlow]

### FlowDelegate()

```dart
FlowDelegate({Listenable? repaint})
```

The flow will repaint whenever [repaint] notifies its listeners.

### getSize()

```dart
Size getSize(BoxConstraints constraints)
```

Override to control the size of the container for the children.

By default, the flow will be as large as possible. If this function returns a size that does not respect the given constraints, the size will be adjusted to be as close to the returned size as possible while still respecting the constraints.

If this function depends on information other than the given constraints, override [shouldRelayout] to indicate when the container should relayout.

### getConstraintsForChild()

```dart
BoxConstraints getConstraintsForChild(int i, BoxConstraints constraints)
```

Override to control the layout constraints given to each child.

By default, the children will receive the given constraints, which are the constraints used to size the container. The children need not respect the given constraints, but they are required to respect the returned constraints. For example, the incoming constraints might require the container to have a width of exactly 100.0 and a height of exactly 100.0, but this function might give the children looser constraints that let them be larger or smaller than 100.0 by 100.0.

If this function depends on information other than the given constraints, override [shouldRelayout] to indicate when the container should relayout.

### paintChildren()

```dart
void paintChildren(FlowPaintingContext context)
```

Override to paint the children of the flow.

Children can be painted in any order, but each child can be painted at most once. Although the container clips the children to its own bounds, it is more efficient to skip painting a child altogether rather than having it paint entirely outside the container's clip.

To paint a child, call [FlowPaintingContext.paintChild] on the given [FlowPaintingContext] (the `context` argument). The given context is valid only within the scope of this function call and contains information (such as the size of the container) that is useful for picking transformation matrices for the children.

If this function depends on information other than the given context, override [shouldRepaint] to indicate when the container should relayout.

### shouldRelayout()

```dart
bool shouldRelayout(FlowDelegate oldDelegate)
```

Override this method to return true when the children need to be laid out. This should compare the fields of the current delegate and the given oldDelegate and return true if the fields are such that the layout would be different.

### shouldRepaint()

```dart
bool shouldRepaint(FlowDelegate oldDelegate)
```

Override this method to return true when the children need to be repainted. This should compare the fields of the current delegate and the given oldDelegate and return true if the fields are such that paintChildren would act differently.

The delegate can also trigger a repaint if the delegate provides the repaint animation argument to this object's constructor and that animation ticks. Triggering a repaint using this animation-based mechanism is more efficient than rebuilding the [Flow] widget to change its delegate.

The flow container might repaint even if this function returns false, for example if layout triggers painting (e.g., if [shouldRelayout] returns true).

### toString()

```dart
String toString()
```

Override this method to include additional information in the debugging data printed by [debugDumpRenderTree] and friends.

By default, returns the [runtimeType] of the class.

# FlowParentData

```dart
class FlowParentData extends ContainerBoxParentData<RenderBox> {}
```

Parent data for use with [RenderFlow].

The [offset] property is ignored by [RenderFlow] and is always set to [Offset.zero]. Children of a [RenderFlow] are positioned using a transformation matrix, which is private to the [RenderFlow]. To set the matrix, use the [FlowPaintingContext.paintChild] function from an override of the [FlowDelegate.paintChildren] function.

# RenderFlow

```dart
class RenderFlow extends RenderBox with ContainerRenderObjectMixin<RenderBox, FlowParentData>, RenderBoxContainerDefaultsMixin<RenderBox, FlowParentData> implements FlowPaintingContext {}
```

Implements the flow layout algorithm.

Flow layouts are optimized for repositioning children using transformation matrices.

The flow container is sized independently from the children by the [FlowDelegate.getSize] function of the delegate. The children are then sized independently given the constraints from the [FlowDelegate.getConstraintsForChild] function.

Rather than positioning the children during layout, the children are positioned using transformation matrices during the paint phase using the matrices from the [FlowDelegate.paintChildren] function. The children are thus repositioned efficiently by repainting the flow, skipping layout.

The most efficient way to trigger a repaint of the flow is to supply a repaint argument to the constructor of the [FlowDelegate]. The flow will listen to this animation and repaint whenever the animation ticks, avoiding both the build and layout phases of the pipeline.

See also:

- [FlowDelegate]
- [RenderStack]

### RenderFlow()

```dart
RenderFlow({List<RenderBox>? children, required FlowDelegate delegate, Clip clipBehavior = Clip.hardEdge})
```

Creates a render object for a flow layout.

For optimal performance, consider using children that return true from [isRepaintBoundary].

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### delegate

```dart
FlowDelegate get delegate
```

The delegate that controls the transformation matrices of the children.

### delegate

```dart
set delegate(FlowDelegate newDelegate)
```

When the delegate is changed to a new delegate with the same runtimeType as the old delegate, this object will call the delegate's [FlowDelegate.shouldRelayout] and [FlowDelegate.shouldRepaint] functions to determine whether the new delegate requires this object to update its layout or painting.

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### isRepaintBoundary

```dart
bool get isRepaintBoundary
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### performLayout()

```dart
void performLayout()
```

### getChildSize()

```dart
Size? getChildSize(int i)
```

### paintChild()

```dart
void paintChild(int i, {Matrix4? transform, double opacity = 1.0})
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### dispose()

```dart
void dispose()
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```
