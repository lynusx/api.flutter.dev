@docImport 'package:flutter/widgets.dart';

@docImport 'sliver_list.dart';

# RenderSliverFillViewport

```dart
class RenderSliverFillViewport extends RenderSliverFixedExtentBoxAdaptor {}
```

A sliver that contains multiple box children that each fill the viewport.

[RenderSliverFillViewport] places its children in a linear array along the main axis. Each child is sized to fill the viewport, both in the main and cross axis. A [viewportFraction] factor can be provided to size the children to a multiple of the viewport's main axis dimension (typically a fraction less than 1.0).

See also:

- [RenderSliverFillRemaining], which sizes the children based on the remaining space rather than the viewport itself.
- [RenderSliverFixedExtentList], which has a configurable [itemExtent].
- [RenderSliverList], which does not require its children to have the same extent in the main axis.

### RenderSliverFillViewport()

```dart
RenderSliverFillViewport({required RenderSliverBoxChildManager childManager, double viewportFraction = 1.0, bool allowImplicitScrolling = true})
```

Creates a sliver that contains multiple box children that each fill the viewport.

### itemExtent

```dart
double get itemExtent
```

### viewportFraction

```dart
double get viewportFraction
```

The fraction of the viewport that each child should fill in the main axis.

If this fraction is less than 1.0, more than one child will be visible at once. If this fraction is greater than 1.0, each child will be larger than the viewport in the main axis.

### viewportFraction

```dart
set viewportFraction(double value)
```

### allowImplicitScrolling

```dart
bool get allowImplicitScrolling
```

{@macro flutter.widgets.PageView.allowImplicitScrolling}

This is typically used by assistive technologies, such as screen readers.

### allowImplicitScrolling

```dart
set allowImplicitScrolling(bool value)
```

### visitChildrenForSemantics()

```dart
void visitChildrenForSemantics(RenderObjectVisitor visitor)
```

# RenderSliverFillRemainingWithScrollable

```dart
class RenderSliverFillRemainingWithScrollable extends RenderSliverSingleBoxAdapter {}
```

A sliver that contains a single box child that contains a scrollable and fills the viewport.

[RenderSliverFillRemainingWithScrollable] sizes its child to fill the viewport in the cross axis and to fill the remaining space in the viewport in the main axis.

Typically this will be the last sliver in a viewport, since (by definition) there is never any room for anything beyond this sliver.

See also:

- [NestedScrollView], which uses this sliver for the inner scrollable.
- [RenderSliverFillRemaining], which lays out its non-scrollable child slightly different than this widget.
- [RenderSliverFillRemainingAndOverscroll], which incorporates the overscroll into the remaining space to fill.
- [RenderSliverFillViewport], which sizes its children based on the size of the viewport, regardless of what else is in the scroll view.
- [RenderSliverList], which shows a list of variable-sized children in a viewport.

### RenderSliverFillRemainingWithScrollable()

```dart
RenderSliverFillRemainingWithScrollable({RenderBox? child})
```

Creates a [RenderSliver] that wraps a scrollable [RenderBox] which is sized to fit the remaining space in the viewport.

### performLayout()

```dart
void performLayout()
```

# RenderSliverFillRemaining

```dart
class RenderSliverFillRemaining extends RenderSliverSingleBoxAdapter {}
```

A sliver that contains a single box child that is non-scrollable and fills the remaining space in the viewport.

[RenderSliverFillRemaining] sizes its child to fill the viewport in the cross axis and to fill the remaining space in the viewport in the main axis.

Typically this will be the last sliver in a viewport, since (by definition) there is never any room for anything beyond this sliver.

See also:

- [RenderSliverFillRemainingWithScrollable], which lays out its scrollable child slightly different than this widget.
- [RenderSliverFillRemainingAndOverscroll], which incorporates the overscroll into the remaining space to fill.
- [RenderSliverFillViewport], which sizes its children based on the size of the viewport, regardless of what else is in the scroll view.
- [RenderSliverList], which shows a list of variable-sized children in a viewport.

### RenderSliverFillRemaining()

```dart
RenderSliverFillRemaining({RenderBox? child})
```

Creates a [RenderSliver] that wraps a non-scrollable [RenderBox] which is sized to fit the remaining space in the viewport.

### performLayout()

```dart
void performLayout()
```

# RenderSliverFillRemainingAndOverscroll

```dart
class RenderSliverFillRemainingAndOverscroll extends RenderSliverSingleBoxAdapter {}
```

A sliver that contains a single box child that is non-scrollable and fills the remaining space in the viewport including any overscrolled area.

[RenderSliverFillRemainingAndOverscroll] sizes its child to fill the viewport in the cross axis and to fill the remaining space in the viewport in the main axis with the overscroll area included.

Typically this will be the last sliver in a viewport, since (by definition) there is never any room for anything beyond this sliver.

See also:

- [RenderSliverFillRemainingWithScrollable], which lays out its scrollable child without overscroll.
- [RenderSliverFillRemaining], which lays out its non-scrollable child without overscroll.
- [RenderSliverFillViewport], which sizes its children based on the size of the viewport, regardless of what else is in the scroll view.
- [RenderSliverList], which shows a list of variable-sized children in a viewport.

### RenderSliverFillRemainingAndOverscroll()

```dart
RenderSliverFillRemainingAndOverscroll({RenderBox? child})
```

Creates a [RenderSliver] that wraps a non-scrollable [RenderBox] which is sized to fit the remaining space plus any overscroll in the viewport.

### performLayout()

```dart
void performLayout()
```
