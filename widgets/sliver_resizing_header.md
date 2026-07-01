@docImport 'pinned_header_sliver.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver_floating_header.dart'; @docImport 'sliver_persistent_header.dart';

# SliverResizingHeader

```dart
class SliverResizingHeader extends StatelessWidget {}
```

A sliver that is pinned to the start of its [CustomScrollView] and reacts to scrolling by resizing between the intrinsic sizes of its min and max extent prototypes.

The minimum and maximum sizes of this sliver are defined by [minExtentPrototype] and [maxExtentPrototype], a pair of widgets that are laid out once. You can use [SizedBox] widgets to define the size limits.

If the [minExtentPrototype] is null, then the default minimum extent is 0. If [maxExtentPrototype] is null then the default maximum extent is based on the child's intrinsic size.

This sliver is preferable to the general purpose [SliverPersistentHeader] for its relatively narrow use case because there's no need to create a [SliverPersistentHeaderDelegate] or to predict the header's minimum or maximum size.

{@tool dartpad} This sample shows how this sliver's two extent prototype properties can be used to create a resizing header whose minimum and maximum sizes match small and large configurations of the same header widget.

** See code in examples/api/lib/widgets/sliver/sliver_resizing_header.0.dart ** {@end-tool}

See also:

- [PinnedHeaderSliver] - which just pins the header at the top of the [CustomScrollView].
- [SliverFloatingHeader] - which animates the header in and out of view in response to downward and upwards scrolls.
- [SliverPersistentHeader] - a general purpose header that can be configured as a pinned, resizing, or floating header.

### SliverResizingHeader()

```dart
SliverResizingHeader({dynamic key, Widget? minExtentPrototype, Widget? maxExtentPrototype, Widget? child})
```

Create a pinned header sliver that reacts to scrolling by resizing between the intrinsic sizes of the min and max extent prototypes.

### minExtentPrototype

```dart
Widget? minExtentPrototype
```

Laid out once to define the minimum size of this sliver along the [CustomScrollView.scrollDirection] axis.

If null, the minimum size of the sliver is 0.

This widget is never made visible.

### maxExtentPrototype

```dart
Widget? maxExtentPrototype
```

Laid out once to define the maximum size of this sliver along the [CustomScrollView.scrollDirection] axis.

If null, the maximum extent of the sliver is based on the child's intrinsic size.

This widget is never made visible.

### child

```dart
Widget? child
```

The widget contained by this sliver.

### build()

```dart
Widget build(BuildContext context)
```
