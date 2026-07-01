@docImport 'package:flutter/material.dart';

# OverScrollHeaderStretchConfiguration

```dart
class OverScrollHeaderStretchConfiguration {}
```

Specifies how a stretched header is to trigger an [AsyncCallback].

See also:

- [SliverAppBar], which creates a header that can be stretched into an overscroll area and trigger a callback function.

### OverScrollHeaderStretchConfiguration()

```dart
OverScrollHeaderStretchConfiguration({double stretchTriggerOffset = 100.0, AsyncCallback? onStretchTrigger})
```

Creates an object that specifies how a stretched header may activate an [AsyncCallback].

### stretchTriggerOffset

```dart
double stretchTriggerOffset
```

The offset of overscroll required to trigger the [onStretchTrigger].

### onStretchTrigger

```dart
AsyncCallback? onStretchTrigger
```

The callback function to be executed when a user over-scrolls to the offset specified by [stretchTriggerOffset].

# PersistentHeaderShowOnScreenConfiguration

```dart
class PersistentHeaderShowOnScreenConfiguration {}
```

{@template flutter.rendering.PersistentHeaderShowOnScreenConfiguration} Specifies how a pinned header or a floating header should react to [RenderObject.showOnScreen] calls. {@endtemplate}

### PersistentHeaderShowOnScreenConfiguration()

```dart
PersistentHeaderShowOnScreenConfiguration({double minShowOnScreenExtent = double.negativeInfinity, double maxShowOnScreenExtent = double.infinity})
```

Creates an object that specifies how a pinned or floating persistent header should behave in response to [RenderObject.showOnScreen] calls.

### minShowOnScreenExtent

```dart
double minShowOnScreenExtent
```

The smallest the floating header can expand to in the main axis direction, in response to a [RenderObject.showOnScreen] call, in addition to its [RenderSliverPersistentHeader.minExtent].

When a floating persistent header is told to show a [Rect] on screen, it may expand itself to accommodate the [Rect]. The minimum extent that is allowed for such expansion is either [RenderSliverPersistentHeader.minExtent] or [minShowOnScreenExtent], whichever is larger. If the persistent header's current extent is already larger than that maximum extent, it will remain unchanged.

This parameter can be set to the persistent header's `maxExtent` (or `double.infinity`) so the persistent header will always try to expand when [RenderObject.showOnScreen] is called on it.

Defaults to [double.negativeInfinity], must be less than or equal to [maxShowOnScreenExtent]. Has no effect unless the persistent header is a floating header.

### maxShowOnScreenExtent

```dart
double maxShowOnScreenExtent
```

The biggest the floating header can expand to in the main axis direction, in response to a [RenderObject.showOnScreen] call, in addition to its [RenderSliverPersistentHeader.maxExtent].

When a floating persistent header is told to show a [Rect] on screen, it may expand itself to accommodate the [Rect]. The maximum extent that is allowed for such expansion is either [RenderSliverPersistentHeader.maxExtent] or [maxShowOnScreenExtent], whichever is smaller. If the persistent header's current extent is already larger than that maximum extent, it will remain unchanged.

This parameter can be set to the persistent header's `minExtent` (or `double.negativeInfinity`) so the persistent header will never try to expand when [RenderObject.showOnScreen] is called on it.

Defaults to [double.infinity], must be greater than or equal to [minShowOnScreenExtent]. Has no effect unless the persistent header is a floating header.

# RenderSliverPersistentHeader

```dart
abstract class RenderSliverPersistentHeader extends RenderSliver with RenderObjectWithChildMixin<RenderBox>, RenderSliverHelpers {}
```

A base class for slivers that have a [RenderBox] child which scrolls normally, except that when it hits the leading edge (typically the top) of the viewport, it shrinks to a minimum size ([minExtent]).

This class primarily provides helpers for managing the child, in particular:

- [layoutChild], which applies min and max extents and a scroll offset to lay out the child. This is normally called from [performLayout].

- [childExtent], to convert the child's box layout dimensions to the sliver geometry model.

- hit testing, painting, and other details of the sliver protocol.

Subclasses must implement [performLayout], [minExtent], and [maxExtent], and typically also will implement [updateChild].

### RenderSliverPersistentHeader()

```dart
RenderSliverPersistentHeader({RenderBox? child, OverScrollHeaderStretchConfiguration? stretchConfiguration})
```

Creates a sliver that changes its size when scrolled to the start of the viewport.

This is an abstract class; this constructor only initializes the [child].

### maxExtent

```dart
double get maxExtent
```

The biggest that this render object can become, in the main axis direction.

This value should not be based on the child. If it changes, call [markNeedsLayout].

### minExtent

```dart
double get minExtent
```

The smallest that this render object can become, in the main axis direction.

If this is based on the intrinsic dimensions of the child, the child should be measured during [updateChild] and the value cached and returned here. The [updateChild] method will automatically be invoked any time the child changes its intrinsic dimensions.

### childExtent

```dart
double get childExtent
```

The dimension of the child in the main axis.

### lastShrinkOffset

```dart
double get lastShrinkOffset
```

The most recent `shrinkOffset` passed to [updateChild].

### lastOverlapsContent

```dart
bool get lastOverlapsContent
```

The most recent `overlapsContent` passed to [updateChild].

### stretchConfiguration

```dart
OverScrollHeaderStretchConfiguration? stretchConfiguration
```

Defines the parameters used to execute an [AsyncCallback] when a stretching header over-scrolls.

If [stretchConfiguration] is null then callback is not triggered.

See also:

- [SliverAppBar], which creates a header that can stretched into an overscroll area and trigger a callback function.

### updateChild()

```dart
void updateChild(double shrinkOffset, bool overlapsContent)
```

Update the child render object if necessary.

Called before the first layout, any time [markNeedsLayout] is called, and any time the scroll offset changes. The `shrinkOffset` is the difference between the [maxExtent] and the current size. Zero means the header is fully expanded, any greater number up to [maxExtent] means that the header has been scrolled by that much. The `overlapsContent` argument is true if the sliver's leading edge is beyond its normal place in the viewport contents, and false otherwise. It may still paint beyond its normal place if the [minExtent] after this call is greater than the amount of space that would normally be left.

The render object will size itself to the larger of (a) the [maxExtent] minus the child's intrinsic height and (b) the [maxExtent] minus the shrink offset.

When this method is called by [layoutChild], the [child] can be set, mutated, or replaced. (It should not be called outside [layoutChild].)

Any time this method would mutate the child, call [markNeedsLayout].

### markNeedsLayout()

```dart
void markNeedsLayout()
```

### layoutChild()

```dart
void layoutChild(double scrollOffset, double maxExtent, {bool overlapsContent = false})
```

Lays out the [child].

This is called by [performLayout]. It applies the given `scrollOffset` (which need not match the offset given by the [constraints]) and the `maxExtent` (which need not match the value returned by the [maxExtent] getter).

The `overlapsContent` argument is passed to [updateChild].

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderObject child)
```

Returns the distance from the leading _visible_ edge of the sliver to the side of the child closest to that edge, in the scroll axis direction.

For example, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.down], then this is the distance from the top of the visible portion of the sliver to the top of the child. If the child is scrolled partially off the top of the viewport, then this will be negative. On the other hand, if the [constraints] describe this sliver as having an axis direction of [AxisDirection.up], then this is the distance from the bottom of the visible portion of the sliver to the bottom of the child. In both cases, this is the direction of increasing [SliverConstraints.scrollOffset].

Calling this when the child is not visible is not valid.

The argument must be the value of the [child] property.

This must be implemented by [RenderSliverPersistentHeader] subclasses.

If there is no child, this should return 0.0.

### hitTestChildren()

```dart
bool hitTestChildren(SliverHitTestResult result, {required double mainAxisPosition, required double crossAxisPosition})
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderObject child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverScrollingPersistentHeader

```dart
abstract class RenderSliverScrollingPersistentHeader extends RenderSliverPersistentHeader {}
```

A sliver with a [RenderBox] child which scrolls normally, except that when it hits the leading edge (typically the top) of the viewport, it shrinks to a minimum size before continuing to scroll.

This sliver makes no effort to avoid overlapping other content.

### RenderSliverScrollingPersistentHeader()

```dart
RenderSliverScrollingPersistentHeader({RenderBox? child, OverScrollHeaderStretchConfiguration? stretchConfiguration})
```

Creates a sliver that shrinks when it hits the start of the viewport, then scrolls off.

### updateGeometry()

```dart
double updateGeometry()
```

Updates [geometry], and returns the new value for [childMainAxisPosition].

This is used by [performLayout].

### performLayout()

```dart
void performLayout()
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderBox child)
```

# RenderSliverPinnedPersistentHeader

```dart
abstract class RenderSliverPinnedPersistentHeader extends RenderSliverPersistentHeader {}
```

A sliver with a [RenderBox] child which never scrolls off the viewport in the positive scroll direction, and which first scrolls on at a full size but then shrinks as the viewport continues to scroll.

This sliver avoids overlapping other earlier slivers where possible.

### RenderSliverPinnedPersistentHeader()

```dart
RenderSliverPinnedPersistentHeader({RenderBox? child, OverScrollHeaderStretchConfiguration? stretchConfiguration, PersistentHeaderShowOnScreenConfiguration? showOnScreenConfiguration = const PersistentHeaderShowOnScreenConfiguration()})
```

Creates a sliver that shrinks when it hits the start of the viewport, then stays pinned there.

### showOnScreenConfiguration

```dart
PersistentHeaderShowOnScreenConfiguration? showOnScreenConfiguration
```

Specifies the persistent header's behavior when `showOnScreen` is called.

If set to null, the persistent header will delegate the `showOnScreen` call to it's parent [RenderObject].

### performLayout()

```dart
void performLayout()
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderBox child)
```

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

# FloatingHeaderSnapConfiguration

```dart
class FloatingHeaderSnapConfiguration {}
```

Specifies how a floating header is to be "snapped" (animated) into or out of view.

See also:

- [RenderSliverFloatingPersistentHeader.maybeStartSnapAnimation] and [RenderSliverFloatingPersistentHeader.maybeStopSnapAnimation], which start or stop the floating header's animation.
- [SliverAppBar], which creates a header that can be pinned, floating, and snapped into view via the corresponding parameters.

### FloatingHeaderSnapConfiguration()

```dart
FloatingHeaderSnapConfiguration({Curve curve = Curves.ease, Duration duration = const Duration(milliseconds: 300)})
```

Creates an object that specifies how a floating header is to be "snapped" (animated) into or out of view.

### curve

```dart
Curve curve
```

The snap animation curve.

### duration

```dart
Duration duration
```

The snap animation's duration.

# RenderSliverFloatingPersistentHeader

```dart
abstract class RenderSliverFloatingPersistentHeader extends RenderSliverPersistentHeader {}
```

A sliver with a [RenderBox] child which shrinks and scrolls like a [RenderSliverScrollingPersistentHeader], but immediately comes back when the user scrolls in the reverse direction.

See also:

- [RenderSliverFloatingPinnedPersistentHeader], which is similar but sticks to the start of the viewport rather than scrolling off.

### RenderSliverFloatingPersistentHeader()

```dart
RenderSliverFloatingPersistentHeader({RenderBox? child, TickerProvider? vsync, FloatingHeaderSnapConfiguration? snapConfiguration, OverScrollHeaderStretchConfiguration? stretchConfiguration, required PersistentHeaderShowOnScreenConfiguration? showOnScreenConfiguration})
```

Creates a sliver that shrinks when it hits the start of the viewport, then scrolls off, and comes back immediately when the user reverses the scroll direction.

### detach()

```dart
void detach()
```

### vsync

```dart
TickerProvider? get vsync
```

A [TickerProvider] to use when animating the scroll position.

### vsync

```dart
set vsync(TickerProvider? value)
```

### snapConfiguration

```dart
FloatingHeaderSnapConfiguration? snapConfiguration
```

Defines the parameters used to snap (animate) the floating header in and out of view.

If [snapConfiguration] is null then the floating header does not snap.

See also:

- [RenderSliverFloatingPersistentHeader.maybeStartSnapAnimation] and [RenderSliverFloatingPersistentHeader.maybeStopSnapAnimation], which start or stop the floating header's animation.
- [SliverAppBar], which creates a header that can be pinned, floating, and snapped into view via the corresponding parameters.

### showOnScreenConfiguration

```dart
PersistentHeaderShowOnScreenConfiguration? showOnScreenConfiguration
```

{@macro flutter.rendering.PersistentHeaderShowOnScreenConfiguration}

If set to null, the persistent header will delegate the `showOnScreen` call to it's parent [RenderObject].

### updateGeometry()

```dart
double updateGeometry()
```

Updates [geometry], and returns the new value for [childMainAxisPosition].

This is used by [performLayout].

### updateScrollStartDirection()

```dart
void updateScrollStartDirection(ScrollDirection direction)
```

Update the last known ScrollDirection when scrolling began.

### maybeStartSnapAnimation()

```dart
void maybeStartSnapAnimation(ScrollDirection direction)
```

If the header isn't already fully exposed, then scroll it into view.

### maybeStopSnapAnimation()

```dart
void maybeStopSnapAnimation(ScrollDirection direction)
```

If a header snap animation or a [showOnScreen] expand animation is underway then stop it.

### performLayout()

```dart
void performLayout()
```

### showOnScreen()

```dart
void showOnScreen({RenderObject? descendant, Rect? rect, Duration duration = Duration.zero, Curve curve = Curves.ease})
```

### childMainAxisPosition()

```dart
double childMainAxisPosition(RenderBox child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# RenderSliverFloatingPinnedPersistentHeader

```dart
abstract class RenderSliverFloatingPinnedPersistentHeader extends RenderSliverFloatingPersistentHeader {}
```

A sliver with a [RenderBox] child which shrinks and then remains pinned to the start of the viewport like a [RenderSliverPinnedPersistentHeader], but immediately grows when the user scrolls in the reverse direction.

See also:

- [RenderSliverFloatingPersistentHeader], which is similar but scrolls off the top rather than sticking to it.

### RenderSliverFloatingPinnedPersistentHeader()

```dart
RenderSliverFloatingPinnedPersistentHeader({RenderBox? child, dynamic vsync, FloatingHeaderSnapConfiguration? snapConfiguration, OverScrollHeaderStretchConfiguration? stretchConfiguration, PersistentHeaderShowOnScreenConfiguration? showOnScreenConfiguration})
```

Creates a sliver that shrinks when it hits the start of the viewport, then stays pinned there, and grows immediately when the user reverses the scroll direction.

### updateGeometry()

```dart
double updateGeometry()
```
