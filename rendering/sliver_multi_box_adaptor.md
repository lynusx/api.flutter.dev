@docImport 'package:flutter/widgets.dart';

@docImport 'sliver_grid.dart'; @docImport 'sliver_list.dart';

# RenderSliverBoxChildManager

```dart
abstract class RenderSliverBoxChildManager {}
```

A delegate used by [RenderSliverMultiBoxAdaptor] to manage its children.

[RenderSliverMultiBoxAdaptor] objects reify their children lazily to avoid spending resources on children that are not visible in the viewport. This delegate lets these objects create and remove children as well as estimate the total scroll offset extent occupied by the full child list.

### createChild()

```dart
void createChild(int index, {required RenderBox? after})
```

Called during layout when a new child is needed. The child should be inserted into the child list in the appropriate position, after the `after` child (at the start of the list if `after` is null). Its index and scroll offsets will automatically be set appropriately.

The `index` argument gives the index of the child to show. It is possible for negative indices to be requested. For example: if the user scrolls from child 0 to child 10, and then those children get much smaller, and then the user scrolls back up again, this method will eventually be asked to produce a child for index -1.

If no child corresponds to `index`, then do nothing.

Which child is indicated by index zero depends on the [GrowthDirection] specified in the `constraints` of the [RenderSliverMultiBoxAdaptor]. For example if the children are the alphabet, then if [SliverConstraints.growthDirection] is [GrowthDirection.forward] then index zero is A, and index 25 is Z. On the other hand if [SliverConstraints.growthDirection] is [GrowthDirection.reverse] then index zero is Z, and index 25 is A.

During a call to [createChild] it is valid to remove other children from the [RenderSliverMultiBoxAdaptor] object if they were not created during this frame and have not yet been updated during this frame. It is not valid to add any other children to this render object.

### removeChild()

```dart
void removeChild(RenderBox child)
```

Remove the given child from the child list.

Called by [RenderSliverMultiBoxAdaptor.collectGarbage], which itself is called from [RenderSliverMultiBoxAdaptor]'s `performLayout`.

The index of the given child can be obtained using the [RenderSliverMultiBoxAdaptor.indexOf] method, which reads it from the [SliverMultiBoxAdaptorParentData.index] field of the child's [RenderObject.parentData].

### estimateMaxScrollOffset()

```dart
double estimateMaxScrollOffset(SliverConstraints constraints, {int? firstIndex, int? lastIndex, double? leadingScrollOffset, double? trailingScrollOffset})
```

Called to estimate the total scrollable extents of this object.

Must return the total distance from the start of the child with the earliest possible index to the end of the child with the last possible index.

### childCount

```dart
int get childCount
```

Called to obtain a precise measure of the total number of children.

Must return the number that is one greater than the greatest `index` for which `createChild` will actually create a child.

This is used when [createChild] cannot add a child for a positive `index`, to determine the precise dimensions of the sliver. It must return an accurate and precise non-null value. It will not be called if [createChild] is always able to create a child (e.g. for an infinite list).

### estimatedChildCount

```dart
int? get estimatedChildCount
```

The best available estimate of [childCount], or null if no estimate is available.

This differs from [childCount] in that [childCount] never returns null (and must not be accessed if the child count is not yet available, meaning the [createChild] method has not been provided an index that does not create a child).

See also:

- [SliverChildDelegate.estimatedChildCount], to which this getter defers.

### didAdoptChild()

```dart
void didAdoptChild(RenderBox child)
```

Called during [RenderSliverMultiBoxAdaptor.adoptChild] or [RenderSliverMultiBoxAdaptor.move].

Subclasses must ensure that the [SliverMultiBoxAdaptorParentData.index] field of the child's [RenderObject.parentData] accurately reflects the child's index in the child list after this function returns.

### setDidUnderflow()

```dart
void setDidUnderflow(bool value)
```

Called during layout to indicate whether this object provided insufficient children for the [RenderSliverMultiBoxAdaptor] to fill the [SliverConstraints.remainingPaintExtent].

Typically called unconditionally at the start of layout with false and then later called with true when the [RenderSliverMultiBoxAdaptor] fails to create a child required to fill the [SliverConstraints.remainingPaintExtent].

Useful for subclasses to determine whether newly added children could affect the visible contents of the [RenderSliverMultiBoxAdaptor].

### didStartLayout()

```dart
void didStartLayout()
```

Called at the beginning of layout to indicate that layout is about to occur.

### didFinishLayout()

```dart
void didFinishLayout()
```

Called at the end of layout to indicate that layout is now complete.

### debugAssertChildListLocked()

```dart
bool debugAssertChildListLocked()
```

In debug mode, asserts that this manager is not expecting any modifications to the [RenderSliverMultiBoxAdaptor]'s child list.

This function always returns true.

The manager is not required to track whether it is expecting modifications to the [RenderSliverMultiBoxAdaptor]'s child list and can return true without making any assertions.

# KeepAliveParentDataMixin

```dart
mixin KeepAliveParentDataMixin implements ParentData {}
```

Parent data structure used by [RenderSliverWithKeepAliveMixin].

### keepAlive

```dart
bool keepAlive
```

Whether to keep the child alive even when it is no longer visible.

### keptAlive

```dart
bool get keptAlive
```

Whether the widget is currently being kept alive, i.e. has [keepAlive] set to true and is offscreen.

# RenderSliverWithKeepAliveMixin

```dart
mixin RenderSliverWithKeepAliveMixin implements RenderSliver {}
```

This class exists to dissociate [KeepAlive] from [RenderSliverMultiBoxAdaptor].

[RenderSliverWithKeepAliveMixin.setupParentData] must be implemented to use a parentData class that uses the right mixin or whatever is appropriate.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

Alerts the developer that the child's parentData needs to be of type [KeepAliveParentDataMixin].

# SliverMultiBoxAdaptorParentData

```dart
class SliverMultiBoxAdaptorParentData extends SliverLogicalParentData with ContainerParentDataMixin<RenderBox>, KeepAliveParentDataMixin {}
```

Parent data structure used by [RenderSliverMultiBoxAdaptor].

### index

```dart
int? index
```

The index of this child according to the [RenderSliverBoxChildManager].

### keptAlive

```dart
bool get keptAlive
```

### toString()

```dart
String toString()
```

# RenderSliverMultiBoxAdaptor

```dart
abstract class RenderSliverMultiBoxAdaptor extends RenderSliver with ContainerRenderObjectMixin<RenderBox, SliverMultiBoxAdaptorParentData>, RenderSliverHelpers, RenderSliverWithKeepAliveMixin {}
```

A sliver with multiple box children.

[RenderSliverMultiBoxAdaptor] is a base class for slivers that have multiple box children. The children are managed by a [RenderSliverBoxChildManager], which lets subclasses create children lazily during layout. Typically subclasses will create only those children that are actually needed to fill the [SliverConstraints.remainingPaintExtent].

The contract for adding and removing children from this render object is more strict than for normal render objects:

- Children can be removed except during a layout pass if they have already been laid out during that layout pass.
- Children cannot be added except during a call to [childManager], and then only if there is no child corresponding to that index (or the child corresponding to that index was first removed).

See also:

- [RenderSliverToBoxAdapter], which has a single box child.
- [RenderSliverList], which places its children in a linear array.
- [RenderSliverFixedExtentList], which places its children in a linear array with a fixed extent in the main axis.
- [RenderSliverGrid], which places its children in arbitrary positions.

### RenderSliverMultiBoxAdaptor()

```dart
RenderSliverMultiBoxAdaptor({required RenderSliverBoxChildManager childManager})
```

Creates a sliver with multiple box children.

### setupParentData()

```dart
void setupParentData(RenderObject child)
```

### childManager

```dart
RenderSliverBoxChildManager get childManager
```

The delegate that manages the children of this object.

Rather than having a concrete list of children, a [RenderSliverMultiBoxAdaptor] uses a [RenderSliverBoxChildManager] to create children during layout in order to fill the [SliverConstraints.remainingPaintExtent].

### debugChildIntegrityEnabled

```dart
bool get debugChildIntegrityEnabled
```

Indicates whether integrity check is enabled.

Setting this property to true will immediately perform an integrity check.

The integrity check consists of:

1.  Verify that the children index in childList is in ascending order.
2.  Verify that there is no dangling keepalive child as the result of [move].

### debugChildIntegrityEnabled

```dart
set debugChildIntegrityEnabled(bool enabled)
```

### adoptChild()

```dart
void adoptChild(RenderObject child)
```

### insert()

```dart
void insert(RenderBox child, {RenderBox? after})
```

### move()

```dart
void move(RenderBox child, {RenderBox? after})
```

### remove()

```dart
void remove(RenderBox child)
```

### removeAll()

```dart
void removeAll()
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

### semanticBounds

```dart
Rect get semanticBounds
```

### addInitialChild()

```dart
bool addInitialChild({int index = 0, double layoutOffset = 0.0})
```

Called during layout to create and add the child with the given index and scroll offset.

Calls [RenderSliverBoxChildManager.createChild] to actually create and add the child if necessary. The child may instead be obtained from a cache; see [SliverMultiBoxAdaptorParentData.keepAlive].

Returns false if there was no cached child and `createChild` did not add any child, otherwise returns true.

Does not layout the new child.

When this is called, there are no visible children, so no children can be removed during the call to `createChild`. No child should be added during that call either, except for the one that is created and returned by `createChild`.

### insertAndLayoutLeadingChild()

```dart
RenderBox? insertAndLayoutLeadingChild(BoxConstraints childConstraints, {bool parentUsesSize = false})
```

Called during layout to create, add, and layout the child before [firstChild].

Calls [RenderSliverBoxChildManager.createChild] to actually create and add the child if necessary. The child may instead be obtained from a cache; see [SliverMultiBoxAdaptorParentData.keepAlive].

Returns the new child or null if no child was obtained.

The child that was previously the first child, as well as any subsequent children, may be removed by this call if they have not yet been laid out during this layout pass. No child should be added during that call except for the one that is created and returned by `createChild`.

### insertAndLayoutChild()

```dart
RenderBox? insertAndLayoutChild(BoxConstraints childConstraints, {required RenderBox? after, bool parentUsesSize = false})
```

Called during layout to create, add, and layout the child after the given child.

Calls [RenderSliverBoxChildManager.createChild] to actually create and add the child if necessary. The child may instead be obtained from a cache; see [SliverMultiBoxAdaptorParentData.keepAlive].

Returns the new child. It is the responsibility of the caller to configure the child's scroll offset.

Children after the `after` child may be removed in the process. Only the new child may be added.

### calculateLeadingGarbage()

```dart
int calculateLeadingGarbage({required int firstIndex})
```

Returns the number of children preceding the `firstIndex` that need to be garbage collected.

See also:

- [collectGarbage], which takes the leading and trailing number of children to be garbage collected.
- [calculateTrailingGarbage], which similarly returns the number of trailing children to be garbage collected.

### calculateTrailingGarbage()

```dart
int calculateTrailingGarbage({required int lastIndex})
```

Returns the number of children following the `lastIndex` that need to be garbage collected.

See also:

- [collectGarbage], which takes the leading and trailing number of children to be garbage collected.
- [calculateLeadingGarbage], which similarly returns the number of leading children to be garbage collected.

### collectGarbage()

```dart
void collectGarbage(int leadingGarbage, int trailingGarbage)
```

Called after layout with the number of children that can be garbage collected at the head and tail of the child list.

Children whose [SliverMultiBoxAdaptorParentData.keepAlive] property is set to true will be removed to a cache instead of being dropped.

This method also collects any children that were previously kept alive but are now no longer necessary. As such, it should be called every time [performLayout] is run, even if the arguments are both zero.

See also:

- [calculateLeadingGarbage], which can be used to determine `leadingGarbage` here.
- [calculateTrailingGarbage], which can be used to determine `trailingGarbage` here.

### indexOf()

```dart
int indexOf(RenderBox child)
```

Returns the index of the given child, as given by the [SliverMultiBoxAdaptorParentData.index] field of the child's [parentData].

### paintExtentOf()

```dart
double paintExtentOf(RenderBox child)
```

Returns the dimension of the given child in the main axis, as given by the child's [RenderBox.size] property. This is only valid after layout.

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderBox child)
```

### childScrollOffset()

```dart
double? childScrollOffset(RenderObject child)
```

### paintsChild()

```dart
bool paintsChild(RenderBox child)
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugAssertChildListIsNonEmptyAndContiguous()

```dart
bool debugAssertChildListIsNonEmptyAndContiguous()
```

Asserts that the reified child list is not empty and has a contiguous sequence of indices.

Always returns true.

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```
