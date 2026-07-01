@docImport 'scroll_position.dart';

# TwoDimensionalScrollView

```dart
abstract class TwoDimensionalScrollView extends StatelessWidget {}
```

A widget that combines a [TwoDimensionalScrollable] and a [TwoDimensionalViewport] to create an interactive scrolling pane of content in both vertical and horizontal dimensions.

A two-way scrollable widget consist of three pieces:

1.  A [TwoDimensionalScrollable] widget, which listens for various user gestures and implements the interaction design for scrolling.
2.  A [TwoDimensionalViewport] widget, which implements the visual design for scrolling by displaying only a portion of the widgets inside the scroll view.
3.  A [TwoDimensionalChildDelegate], which provides the children visible in the scroll view.

[TwoDimensionalScrollView] helps orchestrate these pieces by creating the [TwoDimensionalScrollable] and deferring to its subclass to implement [buildViewport], which builds a subclass of [TwoDimensionalViewport]. The [TwoDimensionalChildDelegate] is provided by the [delegate] parameter.

A [TwoDimensionalScrollView] has two different [ScrollPosition]s, one for each [Axis]. This means that there are also two unique [ScrollController]s for these positions. To provide a ScrollController to access the ScrollPosition, use the [ScrollableDetails.controller] property of the associated axis that is provided to this scroll view.

### TwoDimensionalScrollView()

```dart
TwoDimensionalScrollView({dynamic key, bool? primary, Axis mainAxis = Axis.vertical, ScrollableDetails verticalDetails = const ScrollableDetails.vertical(), ScrollableDetails horizontalDetails = const ScrollableDetails.horizontal(), required TwoDimensionalChildDelegate delegate, double? cacheExtent, CacheExtentStyle? cacheExtentStyle, ScrollCacheExtent? scrollCacheExtent, DiagonalDragBehavior diagonalDragBehavior = DiagonalDragBehavior.none, DragStartBehavior dragStartBehavior = DragStartBehavior.start, ScrollViewKeyboardDismissBehavior? keyboardDismissBehavior, Clip clipBehavior = Clip.hardEdge, HitTestBehavior hitTestBehavior = HitTestBehavior.opaque})
```

Creates a widget that scrolls in both dimensions.

The [primary] argument is associated with the [mainAxis]. The main axis [ScrollableDetails.controller] must be null if [primary] is configured for that axis. If [primary] is true, the nearest [PrimaryScrollController] surrounding the widget is attached to the scroll position of that axis.

### delegate

```dart
TwoDimensionalChildDelegate delegate
```

A delegate that provides the children for the [TwoDimensionalScrollView].

### cacheExtent

```dart
double? cacheExtent
```

{@macro flutter.rendering.RenderViewportBase.cacheExtent}

### cacheExtentStyle

```dart
CacheExtentStyle? cacheExtentStyle
```

{@macro flutter.rendering.RenderViewportBase.cacheExtentStyle}

### scrollCacheExtent

```dart
ScrollCacheExtent? scrollCacheExtent
```

{@macro flutter.rendering.RenderViewportBase.scrollCacheExtent}

### diagonalDragBehavior

```dart
DiagonalDragBehavior diagonalDragBehavior
```

Whether scrolling gestures should lock to one axes, allow free movement in both axes, or be evaluated on a weighted scale.

Defaults to [DiagonalDragBehavior.none], locking axes to receive input one at a time.

### primary

```dart
bool? primary
```

{@macro flutter.widgets.scroll_view.primary}

### mainAxis

```dart
Axis mainAxis
```

The main axis of the two.

Used to determine how to apply [primary] when true.

This value should also be provided to the subclass of [TwoDimensionalViewport], where it is used to determine paint order of children.

### verticalDetails

```dart
ScrollableDetails verticalDetails
```

The configuration of the vertical Scrollable.

These [ScrollableDetails] can be used to set the [AxisDirection], [ScrollController], [ScrollPhysics] and more for the vertical axis.

### horizontalDetails

```dart
ScrollableDetails horizontalDetails
```

The configuration of the horizontal Scrollable.

These [ScrollableDetails] can be used to set the [AxisDirection], [ScrollController], [ScrollPhysics] and more for the horizontal axis.

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### keyboardDismissBehavior

```dart
ScrollViewKeyboardDismissBehavior? keyboardDismissBehavior
```

{@macro flutter.widgets.scroll_view.keyboardDismissBehavior}

If [keyboardDismissBehavior] is null then it will fallback to the inherited [ScrollBehavior.getKeyboardDismissBehavior].

### hitTestBehavior

```dart
HitTestBehavior hitTestBehavior
```

{@macro flutter.widgets.scrollable.hitTestBehavior}

This value applies to both axes.

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### buildViewport()

```dart
Widget buildViewport(BuildContext context, ViewportOffset verticalOffset, ViewportOffset horizontalOffset)
```

Build the two dimensional viewport.

Subclasses may override this method to change how the viewport is built, likely a subclass of [TwoDimensionalViewport].

The `verticalOffset` and `horizontalOffset` arguments are the values obtained from [TwoDimensionalScrollable.viewportBuilder].

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
