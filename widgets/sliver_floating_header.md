@docImport 'pinned_header_sliver.dart'; @docImport 'scroll_view.dart'; @docImport 'sliver_persistent_header.dart'; @docImport 'sliver_resizing_header.dart';

# FloatingHeaderSnapMode

```dart
enum FloatingHeaderSnapMode {}
```

Specifies how a partially visible [SliverFloatingHeader] animates into a view when a user scroll gesture ends.

During a user scroll gesture the header and the rest of the scrollable content move in sync. If the header is partially visible when the scroll gesture ends, [SliverFloatingHeader.snapMode] specifies if the header should [FloatingHeaderSnapMode.overlay] the scrollable's content as it expands until it's completely visible, or if the content should scroll out of the way as the header expands.

At the end of a user scroll gesture, the [SliverFloatingHeader] will expand over the scrollable's content.

At the end of a user scroll gesture, the [SliverFloatingHeader] will expand and the scrollable's content will continue to scroll out of the way.

# SliverFloatingHeader

```dart
class SliverFloatingHeader extends StatefulWidget {}
```

A sliver that shows its [child] when the user scrolls forward and hides it when the user scrolls backwards.

This sliver is preferable to the general purpose [SliverPersistentHeader] for its relatively narrow use case because there's no need to create a [SliverPersistentHeaderDelegate] or to predict the header's size.

{@tool dartpad} This example shows how to create a SliverFloatingHeader.

** See code in examples/api/lib/widgets/sliver/sliver_floating_header.0.dart ** {@end-tool}

See also:

- [PinnedHeaderSliver] - which just pins the header at the top of the [CustomScrollView].
- [SliverResizingHeader] - which similarly pins the header at the top of the [CustomScrollView] but reacts to scrolling by resizing the header between its minimum and maximum extent limits.
- [SliverPersistentHeader] - a general purpose header that can be configured as a pinned, resizing, or floating header.

### SliverFloatingHeader()

```dart
SliverFloatingHeader({dynamic key, AnimationStyle? animationStyle, FloatingHeaderSnapMode? snapMode, required Widget child})
```

Create a floating header sliver that animates into view when the user scrolls forward, and disappears the user starts scrolling in the opposite direction.

### animationStyle

```dart
AnimationStyle? animationStyle
```

Non null properties override the default durations (300ms) and curves (Curves.easeInOut) for subsequent header animations.

The reverse duration and curve apply to the animation that hides the header.

### snapMode

```dart
FloatingHeaderSnapMode? snapMode
```

Specifies how a partially visible [SliverFloatingHeader] animates into a view when a user scroll gesture ends.

The default is [FloatingHeaderSnapMode.overlay]. This parameter doesn't modify an animation in progress, just subsequent animations.

### child

```dart
Widget child
```

The widget contained by this sliver.

### createState()

```dart
State<SliverFloatingHeader> createState()
```
