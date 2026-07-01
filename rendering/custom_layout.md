@docImport 'package:flutter/widgets.dart';

@docImport 'stack.dart';

# MultiChildLayoutParentData

```dart
class MultiChildLayoutParentData extends ContainerBoxParentData<RenderBox> {}
```

[ParentData] used by [RenderCustomMultiChildLayoutBox].

### id

```dart
Object? id
```

An object representing the identity of this child.

### toString()

```dart
String toString()
```

# MultiChildLayoutDelegate

```dart
abstract class MultiChildLayoutDelegate {}
```

A delegate that controls the layout of multiple children.

Used with [CustomMultiChildLayout] (in the widgets library) and [RenderCustomMultiChildLayoutBox] (in the rendering library).

Delegates must be idempotent. Specifically, if two delegates are equal, then they must produce the same layout. To change the layout, replace the delegate with a different instance whose [shouldRelayout] returns true when given the previous instance.

Override [getSize] to control the overall size of the layout. The size of the layout cannot depend on layout properties of the children. This was a design decision to simplify the delegate implementations: This way, the delegate implementations do not have to also handle various intrinsic sizing functions if the parent's size depended on the children. If you want to build a custom layout where you define the size of that widget based on its children, then you will have to create a custom render object. See [MultiChildRenderObjectWidget] with [ContainerRenderObjectMixin] and [RenderBoxContainerDefaultsMixin] to get started or [RenderStack] for an example implementation.

Override [performLayout] to size and position the children. An implementation of [performLayout] must call [layoutChild] exactly once for each child, but it may call [layoutChild] on children in an arbitrary order. Typically a delegate will use the size returned from [layoutChild] on one child to determine the constraints for [performLayout] on another child or to determine the offset for [positionChild] for that child or another child.

Override [shouldRelayout] to determine when the layout of the children needs to be recomputed when the delegate changes.

The most efficient way to trigger a relayout is to supply a `relayout` argument to the constructor of the [MultiChildLayoutDelegate]. The custom layout will listen to this value and relayout whenever the Listenable notifies its listeners, such as when an [Animation] ticks. This allows the custom layout to avoid the build phase of the pipeline.

Each child must be wrapped in a [LayoutId] widget to assign the id that identifies it to the delegate. The [LayoutId.id] needs to be unique among the children that the [CustomMultiChildLayout] manages.

{@tool snippet}

Below is an example implementation of [performLayout] that causes one widget (the follower) to be the same size as another (the leader):

```dart
// Define your own slot numbers, depending upon the id assigned by LayoutId.
// Typical usage is to define an enum like the one below, and use those
// values as the ids.
enum _Slot {
  leader,
  follower,
}

class FollowTheLeader extends MultiChildLayoutDelegate {
  @override
  void performLayout(Size size) {
    Size leaderSize = Size.zero;

    if (hasChild(_Slot.leader)) {
      leaderSize = layoutChild(_Slot.leader, BoxConstraints.loose(size));
      positionChild(_Slot.leader, Offset.zero);
    }

    if (hasChild(_Slot.follower)) {
      layoutChild(_Slot.follower, BoxConstraints.tight(leaderSize));
      positionChild(_Slot.follower, Offset(size.width - leaderSize.width,
          size.height - leaderSize.height));
    }
  }

  @override
  bool shouldRelayout(MultiChildLayoutDelegate oldDelegate) => false;
}
```

{@end-tool}

The delegate gives the leader widget loose constraints, which means the child determines what size to be (subject to fitting within the given size). The delegate then remembers the size of that child and places it in the upper left corner.

The delegate then gives the follower widget tight constraints, forcing it to match the size of the leader widget. The delegate then places the follower widget in the bottom right corner.

The leader and follower widget will paint in the order they appear in the child list, regardless of the order in which [layoutChild] is called on them.

See also:

- [CustomMultiChildLayout], the widget that uses this delegate.
- [RenderCustomMultiChildLayoutBox], render object that uses this delegate.

### MultiChildLayoutDelegate()

```dart
MultiChildLayoutDelegate({Listenable? relayout})
```

Creates a layout delegate.

The layout will update whenever [relayout] notifies its listeners.

### hasChild()

```dart
bool hasChild(Object childId)
```

True if a non-null LayoutChild was provided for the specified id.

Call this from the [performLayout] method to determine which children are available, if the child list might vary.

This method cannot be called from [getSize] as the size is not allowed to depend on the children.

### layoutChild()

```dart
Size layoutChild(Object childId, BoxConstraints constraints)
```

Ask the child to update its layout within the limits specified by the constraints parameter. The child's size is returned.

Call this from your [performLayout] function to lay out each child. Every child must be laid out using this function exactly once each time the [performLayout] function is called.

### positionChild()

```dart
void positionChild(Object childId, Offset offset)
```

Specify the child's origin relative to this origin.

Call this from your [performLayout] function to position each child. If you do not call this for a child, its position will remain unchanged. Children initially have their position set to (0,0), i.e. the top left of the [RenderCustomMultiChildLayoutBox].

### getSize()

```dart
Size getSize(BoxConstraints constraints)
```

Override this method to return the size of this object given the incoming constraints.

The size cannot reflect the sizes of the children. If this layout has a fixed width or height the returned size can reflect that; the size will be constrained to the given constraints.

By default, attempts to size the box to the biggest size possible given the constraints.

### performLayout()

```dart
void performLayout(Size size)
```

Override this method to lay out and position all children given this widget's size.

This method must call [layoutChild] for each child. It should also specify the final position of each child with [positionChild].

### shouldRelayout()

```dart
bool shouldRelayout(MultiChildLayoutDelegate oldDelegate)
```

Override this method to return true when the children need to be laid out.

This should compare the fields of the current delegate and the given `oldDelegate` and return true if the fields are such that the layout would be different.

### toString()

```dart
String toString()
```

Override this method to include additional information in the debugging data printed by [debugDumpRenderTree] and friends.

By default, returns the [runtimeType] of the class.

# RenderCustomMultiChildLayoutBox

```dart
class RenderCustomMultiChildLayoutBox extends RenderBox with ContainerRenderObjectMixin<RenderBox, MultiChildLayoutParentData>, RenderBoxContainerDefaultsMixin<RenderBox, MultiChildLayoutParentData> {}
```

Defers the layout of multiple children to a delegate.

The delegate can determine the layout constraints for each child and can decide where to position each child. The delegate can also determine the size of the parent, but the size of the parent cannot depend on the sizes of the children.

### RenderCustomMultiChildLayoutBox()

```dart
RenderCustomMultiChildLayoutBox({List<RenderBox>? children, required MultiChildLayoutDelegate delegate})
```

Creates a render object that customizes the layout of multiple children.

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### delegate

```dart
MultiChildLayoutDelegate get delegate
```

The delegate that controls the layout of the children.

### delegate

```dart
set delegate(MultiChildLayoutDelegate newDelegate)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
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

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```
