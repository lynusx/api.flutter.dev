@docImport 'dart:developer';

@docImport 'package:flutter/scheduler.dart'; @docImport 'package:flutter/widgets.dart';

@docImport 'binding.dart'; @docImport 'layer.dart'; @docImport 'proxy_box.dart'; @docImport 'shifted_box.dart'; @docImport 'view.dart';

# debugPaintSizeEnabled

```dart
bool debugPaintSizeEnabled
```

Causes each RenderBox to paint a box around its bounds, and some extra boxes, such as [RenderPadding], to draw construction lines.

The edges of the boxes are painted as a one-pixel-thick `const Color(0xFF00FFFF)` outline.

Spacing is painted as a solid `const Color(0x90909090)` area.

Padding is filled in solid `const Color(0x900090FF)`, with the inner edge outlined in `const Color(0xFF0090FF)`, using [debugPaintPadding].

# debugPaintBaselinesEnabled

```dart
bool debugPaintBaselinesEnabled
```

Causes each RenderBox to paint a line at each of its baselines.

# debugPaintTextLayoutBoxes

```dart
bool debugPaintTextLayoutBoxes
```

Causes each RenderParagraph to paint the layout boxes of its text.

{@macro flutter.painting.textPainter.debugPaintTextLayoutBoxes}

See also:

- [debugPaintBaselinesEnabled] which helps debug text alignment.

# debugPaintLayerBordersEnabled

```dart
bool debugPaintLayerBordersEnabled
```

Causes each Layer to paint a box around its bounds.

# debugPaintPointersEnabled

```dart
bool debugPaintPointersEnabled
```

Causes objects like [RenderPointerListener] to flash while they are being tapped. This can be useful to see how large the hit box is, e.g. when debugging buttons that are harder to hit than expected.

For details on how to support this in your [RenderBox] subclass, see [RenderBox.debugHandleEvent].

# debugRepaintRainbowEnabled

```dart
bool debugRepaintRainbowEnabled
```

Overlay a rotating set of colors when repainting layers in debug mode.

See also:

- [RepaintBoundary], which can be used to contain repaints when unchanged areas are being excessively repainted.

# debugRepaintTextRainbowEnabled

```dart
bool debugRepaintTextRainbowEnabled
```

Overlay a rotating set of colors when repainting text in debug mode.

# debugCurrentRepaintColor

```dart
HSVColor debugCurrentRepaintColor
```

The current color to overlay when repainting a layer.

This is used by painting debug code that implements [debugRepaintRainbowEnabled] or [debugRepaintTextRainbowEnabled].

The value is incremented by [RenderView.compositeFrame] if either of those flags is enabled.

# debugPrintMarkNeedsLayoutStacks

```dart
bool debugPrintMarkNeedsLayoutStacks
```

Log the call stacks that mark render objects as needing layout.

For sanity, this only logs the stack traces of cases where an object is added to the list of nodes needing layout. This avoids printing multiple redundant stack traces as a single [RenderObject.markNeedsLayout] call walks up the tree.

# debugPrintMarkNeedsPaintStacks

```dart
bool debugPrintMarkNeedsPaintStacks
```

Log the call stacks that mark render objects as needing paint.

# debugPrintLayouts

```dart
bool debugPrintLayouts
```

Log the dirty render objects that are laid out each frame.

Combined with [debugPrintBeginFrameBanner], this allows you to distinguish layouts triggered by the initial mounting of a render tree (e.g. in a call to [runApp]) from the regular layouts triggered by the pipeline.

Combined with [debugPrintMarkNeedsLayoutStacks], this lets you watch a render object's dirty/clean lifecycle.

See also:

- [debugProfileLayoutsEnabled], which does something similar for layout but using the timeline view.
- [debugProfilePaintsEnabled], which does something similar for painting but using the timeline view.
- [debugPrintRebuildDirtyWidgets], which does something similar for widgets being rebuilt.
- The discussion at [RendererBinding.drawFrame].

# debugCheckIntrinsicSizes

```dart
bool debugCheckIntrinsicSizes
```

Check the intrinsic sizes of each [RenderBox] during layout.

By default this is turned off since these checks are expensive. If you are implementing your own children of [RenderBox] with custom intrinsics, turn this on in your unit tests for additional validations.

# debugProfileLayoutsEnabled

```dart
bool debugProfileLayoutsEnabled
```

Adds [Timeline] events for every [RenderObject] layout.

The timing information this flag exposes is not representative of the actual cost of layout, because the overhead of adding timeline events is significant relative to the time each object takes to lay out. However, it can expose unexpected layout behavior in the timeline.

In debug builds, additional information is included in the trace (such as the properties of render objects being laid out). Collecting this data is expensive and further makes these traces non-representative of actual performance. This data is omitted in profile builds.

For more information about performance debugging in Flutter, see <https://docs.flutter.dev/perf/ui-performance>.

See also:

- [debugPrintLayouts], which does something similar for layout but using console output.
- [debugProfileBuildsEnabled], which does something similar for widgets being rebuilt.
- [debugProfilePaintsEnabled], which does something similar for painting.
- [debugEnhanceLayoutTimelineArguments], which enhances the trace with debugging information related to [RenderObject] layouts.

# debugProfilePaintsEnabled

```dart
bool debugProfilePaintsEnabled
```

Adds [Timeline] events for every [RenderObject] painted.

The timing information this flag exposes is not representative of actual paints, because the overhead of adding timeline events is significant relative to the time each object takes to paint. However, it can expose unexpected painting in the timeline.

In debug builds, additional information is included in the trace (such as the properties of render objects being painted). Collecting this data is expensive and further makes these traces non-representative of actual performance. This data is omitted in profile builds.

For more information about performance debugging in Flutter, see <https://docs.flutter.dev/perf/ui-performance>.

See also:

- [debugProfileBuildsEnabled], which does something similar for widgets being rebuilt, and [debugPrintRebuildDirtyWidgets], its console equivalent.
- [debugProfileLayoutsEnabled], which does something similar for layout, and [debugPrintLayouts], its console equivalent.
- The discussion at [RendererBinding.drawFrame].
- [RepaintBoundary], which can be used to contain repaints when unchanged areas are being excessively repainted.
- [debugEnhancePaintTimelineArguments], which enhances the trace with debugging information related to [RenderObject] paints.

# debugEnhanceLayoutTimelineArguments

```dart
bool debugEnhanceLayoutTimelineArguments
```

Adds debugging information to [Timeline] events related to [RenderObject] layouts.

This flag will only add [Timeline] event arguments for debug builds. Additional arguments will be added for the "LAYOUT" timeline event and for all [RenderObject] layout [Timeline] events, which are the events that are added when [debugProfileLayoutsEnabled] is true. The debugging information that will be added in trace arguments includes stats around [RenderObject] dirty states and [RenderObject] diagnostic information (i.e. [RenderObject] properties).

See also:

- [debugProfileLayoutsEnabled], which adds [Timeline] events for every [RenderObject] layout.
- [debugEnhancePaintTimelineArguments], which does something similar for events related to [RenderObject] paints.
- [debugEnhanceBuildTimelineArguments], which does something similar for events related to [Widget] builds.

# debugEnhancePaintTimelineArguments

```dart
bool debugEnhancePaintTimelineArguments
```

Adds debugging information to [Timeline] events related to [RenderObject] paints.

This flag will only add [Timeline] event arguments for debug builds. Additional arguments will be added for the "PAINT" timeline event and for all [RenderObject] paint [Timeline] events, which are the [Timeline] events that are added when [debugProfilePaintsEnabled] is true. The debugging information that will be added in trace arguments includes stats around [RenderObject] dirty states and [RenderObject] diagnostic information (i.e. [RenderObject] properties).

See also:

- [debugProfilePaintsEnabled], which adds [Timeline] events for every [RenderObject] paint.
- [debugEnhanceLayoutTimelineArguments], which does something similar for events related to [RenderObject] layouts.
- [debugEnhanceBuildTimelineArguments], which does something similar for events related to [Widget] builds.

# ProfilePaintCallback

```dart
typedef ProfilePaintCallback = void Function(RenderObject renderObject)
```

Signature for [debugOnProfilePaint] implementations.

# debugOnProfilePaint

```dart
ProfilePaintCallback? debugOnProfilePaint
```

Callback invoked for every [RenderObject] painted each frame.

This callback is only invoked in debug builds.

See also:

- [debugProfilePaintsEnabled], which does something similar but adds [dart:developer.Timeline] events instead of invoking a callback.
- [debugOnRebuildDirtyWidget], which does something similar for widgets being built.
- [WidgetInspectorService], which uses the [debugOnProfilePaint] callback to generate aggregate profile statistics describing what paints occurred when the `ext.flutter.inspector.trackRepaintWidgets` service extension is enabled.

# debugDisableClipLayers

```dart
bool debugDisableClipLayers
```

Setting to true will cause all clipping effects from the layer tree to be ignored.

Can be used to debug whether objects being clipped are painting excessively in clipped areas. Can also be used to check whether excessive use of clipping is affecting performance.

This will not reduce the number of [Layer] objects created; the compositing strategy is unaffected. It merely causes the clipping layers to be skipped when building the scene.

# debugDisablePhysicalShapeLayers

```dart
bool debugDisablePhysicalShapeLayers
```

Setting to true will cause all physical modeling effects from the layer tree, such as shadows from elevations, to be ignored.

Can be used to check whether excessive use of physical models is affecting performance.

This will not reduce the number of [Layer] objects created; the compositing strategy is unaffected. It merely causes the physical shape layers to be skipped when building the scene.

# debugDisableOpacityLayers

```dart
bool debugDisableOpacityLayers
```

Setting to true will cause all opacity effects from the layer tree to be ignored.

An optimization to not paint the child at all when opacity is 0 will still remain.

Can be used to check whether excessive use of opacity effects is affecting performance.

This will not reduce the number of [Layer] objects created; the compositing strategy is unaffected. It merely causes the opacity layers to be skipped when building the scene.

# debugPaintPadding()

```dart
void debugPaintPadding(Canvas canvas, Rect outerRect, Rect? innerRect, {double outlineWidth = 2.0})
```

Paint a diagram showing the given area as padding.

The `innerRect` argument represents the position of the child, if any.

When `innerRect` is null, the method draws the entire `outerRect` in a grayish color representing _spacing_.

When `innerRect` is non-null, the method draws the padding region around the `innerRect` in a tealish color, with a solid outline around the inner region.

This method is used by [RenderPadding.debugPaintSize] when [debugPaintSizeEnabled] is true.

# debugAssertAllRenderVarsUnset()

```dart
bool debugAssertAllRenderVarsUnset(String reason, {bool debugCheckIntrinsicSizesOverride = false})
```

Returns true if none of the rendering library debug variables have been changed.

This function is used by the test framework to ensure that debug variables haven't been inadvertently changed.

See [the rendering library](rendering/rendering-library.html) for a complete list.

The `debugCheckIntrinsicSizesOverride` argument can be provided to override the expected value for [debugCheckIntrinsicSizes]. (This exists because the test framework itself overrides this value in some cases.)

# debugCheckHasBoundedAxis()

```dart
bool debugCheckHasBoundedAxis(Axis axis, BoxConstraints constraints)
```

Returns true if the given [Axis] is bounded within the given [BoxConstraints] in both the main and cross axis, throwing an exception otherwise.

This is used by viewports during `performLayout` and `computeDryLayout` because bounded constraints are required in order to layout their children.
