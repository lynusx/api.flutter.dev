@docImport 'dart:ui'; @docImport 'package:flutter/material.dart';

@docImport 'scroll_position.dart'; @docImport 'scrollable.dart'; @docImport 'viewport.dart';

# ScrollMetrics

```dart
mixin ScrollMetrics {}
```

A description of a [Scrollable]'s contents, useful for modeling the state of its viewport.

This class defines a current position, [pixels], and a range of values considered "in bounds" for that position. The range has a minimum value at [minScrollExtent] and a maximum value at [maxScrollExtent] (inclusive). The viewport scrolls in the direction and axis described by [axisDirection] and [axis].

The [outOfRange] getter will return true if [pixels] is outside this defined range. The [atEdge] getter will return true if the [pixels] position equals either the [minScrollExtent] or the [maxScrollExtent].

The dimensions of the viewport in the given [axis] are described by [viewportDimension].

The above values are also exposed in terms of [extentBefore], [extentInside], and [extentAfter], which may be more useful for use cases such as scroll bars; for example, see [Scrollbar].

{@tool dartpad} This sample shows how a [ScrollMetricsNotification] is dispatched when the [ScrollMetrics] changed as a result of resizing the [Viewport]. Press the floating action button to increase the scrollable window's size.

** See code in examples/api/lib/widgets/scroll_position/scroll_metrics_notification.0.dart ** {@end-tool}

See also:

- [FixedScrollMetrics], which is an immutable object that implements this interface.

### copyWith()

```dart
ScrollMetrics copyWith({double? minScrollExtent, double? maxScrollExtent, double? pixels, double? viewportDimension, AxisDirection? axisDirection, double? devicePixelRatio})
```

Creates a [ScrollMetrics] that has the same properties as this object.

This is useful if this object is mutable, but you want to get a snapshot of the current state.

The named arguments allow the values to be adjusted in the process. This is useful to examine hypothetical situations, for example "would applying this delta unmodified take the position [outOfRange]?".

### minScrollExtent

```dart
double get minScrollExtent
```

The minimum in-range value for [pixels].

The actual [pixels] value might be [outOfRange].

This value is typically less than or equal to [maxScrollExtent]. It can be negative infinity, if the scroll is unbounded.

### maxScrollExtent

```dart
double get maxScrollExtent
```

The maximum in-range value for [pixels].

The actual [pixels] value might be [outOfRange].

This value is typically greater than or equal to [minScrollExtent]. It can be infinity, if the scroll is unbounded.

For scrollables that lazily construct their contents, such as [ListView.builder], this value can be an estimate that changes as more children are laid out.

### hasContentDimensions

```dart
bool get hasContentDimensions
```

Whether the [minScrollExtent] and the [maxScrollExtent] properties are available.

### pixels

```dart
double get pixels
```

The current scroll position, in logical pixels along the [axisDirection].

### hasPixels

```dart
bool get hasPixels
```

Whether the [pixels] property is available.

### viewportDimension

```dart
double get viewportDimension
```

The extent of the viewport along the [axisDirection].

### hasViewportDimension

```dart
bool get hasViewportDimension
```

Whether the [viewportDimension] property is available.

### axisDirection

```dart
AxisDirection get axisDirection
```

The direction in which the scroll view scrolls.

### axis

```dart
Axis get axis
```

The axis in which the scroll view scrolls.

### outOfRange

```dart
bool get outOfRange
```

Whether the [pixels] value is outside the [minScrollExtent] and [maxScrollExtent].

### atEdge

```dart
bool get atEdge
```

Whether the [pixels] value is exactly at the [minScrollExtent] or the [maxScrollExtent].

### extentBefore

```dart
double get extentBefore
```

The quantity of content conceptually "above" the viewport in the scrollable. This is the content above the content described by [extentInside].

### extentInside

```dart
double get extentInside
```

The quantity of content conceptually "inside" the viewport in the scrollable (including empty space if the total amount of content is less than the [viewportDimension]).

The value is typically the extent of the viewport ([viewportDimension]) when [outOfRange] is false. It can be less when overscrolling.

The value is always non-negative, and less than or equal to [viewportDimension].

### extentAfter

```dart
double get extentAfter
```

The quantity of content conceptually "below" the viewport in the scrollable. This is the content below the content described by [extentInside].

### extentTotal

```dart
double get extentTotal
```

The total quantity of content available.

This is the sum of [extentBefore], [extentInside], and [extentAfter], modulo any rounding errors.

### devicePixelRatio

```dart
double get devicePixelRatio
```

The [FlutterView.devicePixelRatio] of the view that the [Scrollable] associated with this metrics object is drawn into.

# FixedScrollMetrics

```dart
class FixedScrollMetrics with ScrollMetrics {}
```

An immutable snapshot of values associated with a [Scrollable] viewport.

For details, see [ScrollMetrics], which defines this object's interfaces.

{@tool dartpad} This sample shows how a [ScrollMetricsNotification] is dispatched when the [ScrollMetrics] changed as a result of resizing the [Viewport]. Press the floating action button to increase the scrollable window's size.

** See code in examples/api/lib/widgets/scroll_position/scroll_metrics_notification.0.dart ** {@end-tool}

### FixedScrollMetrics()

```dart
FixedScrollMetrics({required double? minScrollExtent, required double? maxScrollExtent, required double? pixels, required double? viewportDimension, required AxisDirection axisDirection, required double devicePixelRatio})
```

Creates an immutable snapshot of values associated with a [Scrollable] viewport.

### minScrollExtent

```dart
double get minScrollExtent
```

### maxScrollExtent

```dart
double get maxScrollExtent
```

### hasContentDimensions

```dart
bool get hasContentDimensions
```

### pixels

```dart
double get pixels
```

### hasPixels

```dart
bool get hasPixels
```

### viewportDimension

```dart
double get viewportDimension
```

### hasViewportDimension

```dart
bool get hasViewportDimension
```

### axisDirection

```dart
AxisDirection axisDirection
```

### devicePixelRatio

```dart
double devicePixelRatio
```

### toString()

```dart
String toString()
```
