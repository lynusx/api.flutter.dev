@docImport 'page_view.dart'; @docImport 'scroll_position.dart'; @docImport 'scroll_view.dart'; @docImport 'scrollable.dart'; @docImport 'sliver.dart';

# Viewport

```dart
class Viewport extends MultiChildRenderObjectWidget {}
```

A widget through which a portion of larger content can be viewed, typically in combination with a [Scrollable].

[Viewport] is the visual workhorse of the scrolling machinery. It displays a subset of its children according to its own dimensions and the given [offset]. As the offset varies, different children are visible through the viewport.

[Viewport] hosts a bidirectional list of slivers, anchored on a [center] sliver, which is placed at the zero scroll offset. The center widget is displayed in the viewport according to the [anchor] property.

Slivers that are earlier in the child list than [center] are displayed in reverse order in the reverse [axisDirection] starting from the [center]. For example, if the [axisDirection] is [AxisDirection.down], the first sliver before [center] is placed above the [center]. The slivers that are later in the child list than [center] are placed in order in the [axisDirection]. For example, in the preceding scenario, the first sliver after [center] is placed below the [center].

[Viewport] cannot contain box children directly. Instead, use a [SliverList], [SliverFixedExtentList], [SliverGrid], or a [SliverToBoxAdapter], for example.

See also:

- [ListView], [PageView], [GridView], and [CustomScrollView], which combine [Scrollable] and [Viewport] into widgets that are easier to use.
- [SliverToBoxAdapter], which allows a box widget to be placed inside a sliver context (the opposite of this widget).
- [ShrinkWrappingViewport], a variant of [Viewport] that shrink-wraps its contents along the main axis.
- [ViewportElementMixin], which should be mixed in to the [Element] type used by viewport-like widgets to correctly handle scroll notifications.

### Viewport()

```dart
Viewport({dynamic key, AxisDirection axisDirection = AxisDirection.down, AxisDirection? crossAxisDirection, double anchor = 0.0, required ViewportOffset offset, Key? center, double? cacheExtent, CacheExtentStyle cacheExtentStyle = CacheExtentStyle.pixel, ScrollCacheExtent? scrollCacheExtent, SliverPaintOrder paintOrder = SliverPaintOrder.firstIsTop, Clip clipBehavior = Clip.hardEdge, List<Widget> slivers = const <Widget>[]})
```

Creates a widget that is bigger on the inside.

The viewport listens to the [offset], which means you do not need to rebuild this widget when the [offset] changes.

### axisDirection

```dart
AxisDirection axisDirection
```

The direction in which the [offset]'s [ViewportOffset.pixels] increases.

For example, if the [axisDirection] is [AxisDirection.down], a scroll offset of zero is at the top of the viewport and increases towards the bottom of the viewport.

### crossAxisDirection

```dart
AxisDirection? crossAxisDirection
```

The direction in which child should be laid out in the cross axis.

If the [axisDirection] is [AxisDirection.down] or [AxisDirection.up], this property defaults to [AxisDirection.left] if the ambient [Directionality] is [TextDirection.rtl] and [AxisDirection.right] if the ambient [Directionality] is [TextDirection.ltr].

If the [axisDirection] is [AxisDirection.left] or [AxisDirection.right], this property defaults to [AxisDirection.down].

### anchor

```dart
double anchor
```

The relative position of the zero scroll offset.

For example, if [anchor] is 0.5 and the [axisDirection] is [AxisDirection.down] or [AxisDirection.up], then the zero scroll offset is vertically centered within the viewport. If the [anchor] is 1.0, and the [axisDirection] is [AxisDirection.right], then the zero scroll offset is on the left edge of the viewport.

{@macro flutter.rendering.GrowthDirection.sample}

### offset

```dart
ViewportOffset offset
```

Which part of the content inside the viewport should be visible.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### center

```dart
Key? center
```

The first child in the [GrowthDirection.forward] growth direction.

Children after [center] will be placed in the [axisDirection] relative to the [center]. Children before [center] will be placed in the opposite of the [axisDirection] relative to the [center].

The [center] must be the key of a child of the viewport.

{@macro flutter.rendering.GrowthDirection.sample}

### cacheExtent

```dart
double? cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

See also:

- [cacheExtentStyle], which controls the units of the [cacheExtent].

### cacheExtentStyle

```dart
CacheExtentStyle cacheExtentStyle
```

{@macro flutter.rendering.RenderViewportBase.cacheExtentStyle}

### scrollCacheExtent

```dart
ScrollCacheExtent? scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### paintOrder

```dart
SliverPaintOrder paintOrder
```

{@macro flutter.rendering.RenderViewportBase.paintOrder}

Defaults to [SliverPaintOrder.firstIsTop].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### getDefaultCrossAxisDirection()

```dart
AxisDirection getDefaultCrossAxisDirection(BuildContext context, AxisDirection axisDirection)
```

Given a [BuildContext] and an [AxisDirection], determine the correct cross axis direction.

This depends on the [Directionality] if the `axisDirection` is vertical; otherwise, the default cross axis direction is downwards.

### createRenderObject()

```dart
RenderViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderViewport renderObject)
```

### createElement()

```dart
MultiChildRenderObjectElement createElement()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ShrinkWrappingViewport

```dart
class ShrinkWrappingViewport extends MultiChildRenderObjectWidget {}
```

A widget that is bigger on the inside and shrink wraps its children in the main axis.

[ShrinkWrappingViewport] displays a subset of its children according to its own dimensions and the given [offset]. As the offset varies, different children are visible through the viewport.

[ShrinkWrappingViewport] differs from [Viewport] in that [Viewport] expands to fill the main axis whereas [ShrinkWrappingViewport] sizes itself to match its children in the main axis. This shrink wrapping behavior is expensive because the children, and hence the viewport, could potentially change size whenever the [offset] changes (e.g., because of a collapsing header).

[ShrinkWrappingViewport] cannot contain box children directly. Instead, use a [SliverList], [SliverFixedExtentList], [SliverGrid], or a [SliverToBoxAdapter], for example.

See also:

- [ListView], [PageView], [GridView], and [CustomScrollView], which combine [Scrollable] and [ShrinkWrappingViewport] into widgets that are easier to use.
- [SliverToBoxAdapter], which allows a box widget to be placed inside a sliver context (the opposite of this widget).
- [Viewport], a viewport that does not shrink-wrap its contents.

### ShrinkWrappingViewport()

```dart
ShrinkWrappingViewport({dynamic key, AxisDirection axisDirection = AxisDirection.down, AxisDirection? crossAxisDirection, required ViewportOffset offset, SliverPaintOrder paintOrder = SliverPaintOrder.firstIsTop, Clip clipBehavior = Clip.hardEdge, double? cacheExtent, CacheExtentStyle cacheExtentStyle = CacheExtentStyle.pixel, ScrollCacheExtent? scrollCacheExtent, List<Widget> slivers = const <Widget>[]})
```

Creates a widget that is bigger on the inside and shrink wraps its children in the main axis.

The viewport listens to the [offset], which means you do not need to rebuild this widget when the [offset] changes.

### axisDirection

```dart
AxisDirection axisDirection
```

The direction in which the [offset]'s [ViewportOffset.pixels] increases.

For example, if the [axisDirection] is [AxisDirection.down], a scroll offset of zero is at the top of the viewport and increases towards the bottom of the viewport.

### crossAxisDirection

```dart
AxisDirection? crossAxisDirection
```

The direction in which child should be laid out in the cross axis.

If the [axisDirection] is [AxisDirection.down] or [AxisDirection.up], this property defaults to [AxisDirection.left] if the ambient [Directionality] is [TextDirection.rtl] and [AxisDirection.right] if the ambient [Directionality] is [TextDirection.ltr].

If the [axisDirection] is [AxisDirection.left] or [AxisDirection.right], this property defaults to [AxisDirection.down].

### offset

```dart
ViewportOffset offset
```

Which part of the content inside the viewport should be visible.

The [ViewportOffset.pixels] value determines the scroll offset that the viewport uses to select which part of its content to display. As the user scrolls the viewport, this value changes, which changes the content that is displayed.

Typically a [ScrollPosition].

### paintOrder

```dart
SliverPaintOrder paintOrder
```

{@macro flutter.rendering.RenderViewportBase.paintOrder}

Defaults to [SliverPaintOrder.firstIsTop].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### cacheExtent

```dart
double? cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

See also:

- [cacheExtentStyle], which controls the units of the [cacheExtent].

### cacheExtentStyle

```dart
CacheExtentStyle cacheExtentStyle
```

{@macro flutter.rendering.RenderViewportBase.cacheExtentStyle}

### scrollCacheExtent

```dart
ScrollCacheExtent? scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### createRenderObject()

```dart
RenderShrinkWrappingViewport createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderShrinkWrappingViewport renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
