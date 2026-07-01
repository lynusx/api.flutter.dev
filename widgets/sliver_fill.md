@docImport 'nested_scroll_view.dart'; @docImport 'scroll_physics.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver_prototype_extent_list.dart';

# SliverFillViewport

```dart
class SliverFillViewport extends StatelessWidget {}
```

A sliver that contains multiple box children that each fills the viewport.

_To learn more about slivers, see [CustomScrollView.slivers]._

[SliverFillViewport] places its children in a linear array along the main axis. Each child is sized to fill the viewport, both in the main and cross axis.

See also:

- [SliverFixedExtentList], which has a configurable [SliverFixedExtentList.itemExtent].
- [SliverPrototypeExtentList], which is similar to [SliverFixedExtentList] except that it uses a prototype list item instead of a pixel value to define the main axis extent of each item.
- [SliverList], which does not require its children to have the same extent in the main axis.

### SliverFillViewport()

```dart
SliverFillViewport({dynamic key, required SliverChildDelegate delegate, double viewportFraction = 1.0, bool padEnds = true, bool allowImplicitScrolling = true})
```

Creates a sliver whose box children that each fill the viewport.

### viewportFraction

```dart
double viewportFraction
```

The fraction of the viewport that each child should fill in the main axis.

If this fraction is less than 1.0, more than one child will be visible at once. If this fraction is greater than 1.0, each child will be larger than the viewport in the main axis.

### padEnds

```dart
bool padEnds
```

Whether to add padding to both ends of the list.

If this is set to true and [viewportFraction] < 1.0, padding will be added such that the first and last child slivers will be in the center of the viewport when scrolled all the way to the start or end, respectively. You may want to set this to false if this [SliverFillViewport] is not the only widget along this main axis, such as in a [CustomScrollView] with multiple children.

If [viewportFraction] is greater than one, this option has no effect. Defaults to true.

### delegate

```dart
SliverChildDelegate delegate
```

{@macro flutter.widgets.SliverMultiBoxAdaptorWidget.delegate}

### allowImplicitScrolling

```dart
bool allowImplicitScrolling
```

{@macro flutter.widgets.PageView.allowImplicitScrolling}

### build()

```dart
Widget build(BuildContext context)
```

# SliverFillRemaining

```dart
class SliverFillRemaining extends StatelessWidget {}
```

A sliver that contains a single box child that fills the remaining space in the viewport.

_To learn more about slivers, see [CustomScrollView.slivers]._

[SliverFillRemaining] will size its [child] to fill the viewport in the cross axis. The extent of the sliver and its child's size in the main axis is computed conditionally, described in further detail below.

Typically this will be the last sliver in a viewport, since (by definition) there is never any room for anything beyond this sliver.

## Main Axis Extent

### When [SliverFillRemaining] has a scrollable child

The [hasScrollBody] flag indicates whether the sliver's child has a scrollable body. This value is never null, and defaults to true. A common example of this use is a [NestedScrollView]. In this case, the sliver will size its child to fill the maximum available extent. [SliverFillRemaining] will not constrain the scrollable area, as it could potentially have an infinite depth. This is also true for use cases such as a [ScrollView] when [ScrollView.shrinkWrap] is true.

### When [SliverFillRemaining] does not have a scrollable child

When [hasScrollBody] is set to false, the child's size is taken into account when considering the extent to which it should fill the space. The extent to which the preceding slivers have been scrolled is also taken into account in deciding how to layout this sliver.

[SliverFillRemaining] will size its [child] to fill the viewport in the main axis if that space is larger than the child's extent, and the amount of space that has been scrolled beforehand has not exceeded the main axis extent of the viewport.

{@tool dartpad} In this sample the [SliverFillRemaining] sizes its [child] to fill the remaining extent of the viewport in both axes. The icon is centered in the sliver, and would be in any computed extent for the sliver.

** See code in examples/api/lib/widgets/sliver_fill/sliver_fill_remaining.0.dart ** {@end-tool}

[SliverFillRemaining] will defer to the size of its [child] if the child's size exceeds the remaining space in the viewport.

{@tool dartpad} In this sample the [SliverFillRemaining] defers to the size of its [child] because the child's extent exceeds that of the remaining extent of the viewport's main axis.

** See code in examples/api/lib/widgets/sliver_fill/sliver_fill_remaining.1.dart ** {@end-tool}

[SliverFillRemaining] will defer to the size of its [child] if the [SliverConstraints.precedingScrollExtent] exceeded the length of the viewport's main axis.

{@tool dartpad} In this sample the [SliverFillRemaining] defers to the size of its [child] because the [SliverConstraints.precedingScrollExtent] has gone beyond that of the viewport's main axis.

** See code in examples/api/lib/widgets/sliver_fill/sliver_fill_remaining.2.dart ** {@end-tool}

For [ScrollPhysics] that allow overscroll, such as [BouncingScrollPhysics], setting the [fillOverscroll] flag to true allows the size of the [child] to _stretch_, filling the overscroll area. It does this regardless of the path chosen to provide the child's size.

{@animation 250 500 https://flutter.github.io/assets-for-api-docs/assets/widgets/sliver_fill_remaining_fill_overscroll.mp4}

{@tool dartpad} In this sample the [SliverFillRemaining]'s child stretches to fill the overscroll area when [fillOverscroll] is true. This sample also features a button that is pinned to the bottom of the sliver, regardless of size or overscroll behavior. Try switching [fillOverscroll] to see the difference.

This sample only shows the overscroll behavior on devices that support overscroll.

** See code in examples/api/lib/widgets/sliver_fill/sliver_fill_remaining.3.dart ** {@end-tool}

See also:

- [SliverFillViewport], which sizes its children based on the size of the viewport, regardless of what else is in the scroll view.
- [SliverList], which shows a list of variable-sized children in a viewport.

### SliverFillRemaining()

```dart
SliverFillRemaining({dynamic key, Widget? child, bool hasScrollBody = true, bool fillOverscroll = false})
```

Creates a sliver that fills the remaining space in the viewport.

### child

```dart
Widget? child
```

Box child widget that fills the remaining space in the viewport.

The main [SliverFillRemaining] documentation contains more details.

### hasScrollBody

```dart
bool hasScrollBody
```

Indicates whether the child has a scrollable body, this value cannot be null.

Defaults to true such that the child will extend beyond the viewport and scroll, as seen in [NestedScrollView].

Setting this value to false will allow the child to fill the remainder of the viewport and not extend further. However, if the [SliverConstraints.precedingScrollExtent] and/or the [child]'s extent exceeds the size of the viewport, the sliver will defer to the child's size rather than overriding it.

### fillOverscroll

```dart
bool fillOverscroll
```

Indicates whether the child should stretch to fill the overscroll area created by certain scroll physics, such as iOS' default scroll physics. This flag is only relevant when [hasScrollBody] is false.

Defaults to false, meaning that the default behavior is for the child to maintain its size and not extend into the overscroll area.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
