@docImport 'package:flutter/material.dart';

@docImport 'container.dart'; @docImport 'scroll_view.dart';

# DecoratedSliver

```dart
class DecoratedSliver extends SingleChildRenderObjectWidget {}
```

A sliver widget that paints a [Decoration] either before or after its child paints.

Unlike [DecoratedBox], this widget expects its child to be a sliver, and must be placed in a widget that expects a sliver.

If the child sliver has infinite [SliverGeometry.scrollExtent], then we only draw the decoration down to the bottom [SliverGeometry.cacheExtent], and it is necessary to ensure that the bottom border does not creep above the top of the bottom cache. This can happen if the bottom has a border radius larger than the extent of the cache area.

Commonly used with [BoxDecoration].

{@tool dartpad} This sample shows a radial gradient that draws a moon on a night sky:

** See code in examples/api/lib/widgets/sliver/decorated_sliver.0.dart ** {@end-tool}

{@tool dartpad} This example demonstrates how the [CustomScrollView.clipBehavior] impacts a decorated sliver's appearance.

The [Switch] determines whether clipping is enabled, and the [Slider] adjusts the height of window.

** See code in examples/api/lib/widgets/sliver/decorated_sliver.1.dart ** {@end-tool}

This widget does not apply any additional clipping to its [child]. To clip a child based on the [Decoration]'s shape, consider using a [ClipPath] widget.

See also:

- [DecoratedBox], the version of this class that works with RenderBox widgets.
- [Decoration], which you can extend to provide other effects with [DecoratedSliver].
- [CustomPaint], another way to draw custom effects from the widget layer.

### DecoratedSliver()

```dart
DecoratedSliver({dynamic key, required Decoration decoration, DecorationPosition position = DecorationPosition.background, Widget? sliver})
```

Creates a widget that paints a [Decoration].

By default the decoration paints behind the child.

### decoration

```dart
Decoration decoration
```

What decoration to paint.

Commonly a [BoxDecoration].

### position

```dart
DecorationPosition position
```

Whether to paint the box decoration behind or in front of the child.

### createRenderObject()

```dart
RenderDecoratedSliver createRenderObject(BuildContext context)
```

### updateRenderObject()

```dart
void updateRenderObject(BuildContext context, RenderDecoratedSliver renderObject)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
