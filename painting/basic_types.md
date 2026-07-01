@docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart';

@docImport 'text_span.dart'; @docImport 'text_style.dart';

# RenderComparison

```dart
enum RenderComparison {}
```

The description of the difference between two objects, in the context of how it will affect the rendering.

Used by [TextSpan.compareTo] and [TextStyle.compareTo].

The values in this enum are ordered such that they are in increasing order of cost. A value with index N implies all the values with index less than N. For example, [layout] (index 3) implies [paint] (2).

The two objects are identical (meaning deeply equal, not necessarily [dart:core.identical]).

The two objects are identical for the purpose of layout, but may be different in other ways.

For example, maybe some event handlers changed.

The two objects are different but only in ways that affect paint, not layout.

For example, only the color is changed.

[RenderObject.markNeedsPaint] would be necessary to handle this kind of change in a render object.

The two objects are different in ways that affect layout (and therefore paint).

For example, the size is changed.

This is the most drastic level of change possible.

[RenderObject.markNeedsLayout] would be necessary to handle this kind of change in a render object.

# Axis

```dart
enum Axis {}
```

The two cardinal directions in two dimensions.

The axis is always relative to the current coordinate space. This means, for example, that a [horizontal] axis might actually be diagonally from top right to bottom left, due to some local [Transform] applied to the scene.

See also:

- [AxisDirection], which is a directional version of this enum (with values like left and right, rather than just horizontal).
- [TextDirection], which disambiguates between left-to-right horizontal content and right-to-left horizontal content.

Left and right.

See also:

- [TextDirection], which disambiguates between left-to-right horizontal content and right-to-left horizontal content.

Up and down.

# flipAxis()

```dart
Axis flipAxis(Axis direction)
```

Returns the opposite of the given [Axis].

Specifically, returns [Axis.horizontal] for [Axis.vertical], and vice versa.

See also:

- [flipAxisDirection], which does the same thing for [AxisDirection] values.

# VerticalDirection

```dart
enum VerticalDirection {}
```

A direction in which boxes flow vertically.

This is used by the flex algorithm (e.g. [Column]) to decide in which direction to draw boxes.

This is also used to disambiguate `start` and `end` values (e.g. [MainAxisAlignment.start] or [CrossAxisAlignment.end]).

See also:

- [TextDirection], which controls the same thing but horizontally.

Boxes should start at the bottom and be stacked vertically towards the top.

The "start" is at the bottom, the "end" is at the top.

Boxes should start at the top and be stacked vertically towards the bottom.

The "start" is at the top, the "end" is at the bottom.

# AxisDirection

```dart
enum AxisDirection {}
```

A direction along either the horizontal or vertical [Axis] in which the origin, or zero position, is determined.

This value relates to the direction in which the scroll offset increases from the origin. This value does not represent the direction of user input that may be modifying the scroll offset, such as from a drag. For the active scrolling direction, see [ScrollDirection].

{@tool dartpad} This sample shows a [CustomScrollView], with [Radio] buttons in the [AppBar.bottom] that change the [AxisDirection] to illustrate different configurations.

** See code in examples/api/lib/painting/axis_direction/axis_direction.0.dart ** {@end-tool}

See also:

- [ScrollDirection], the direction of active scrolling, relative to the positive scroll offset axis given by an [AxisDirection] and a [GrowthDirection].
- [GrowthDirection], the direction in which slivers and their content are ordered, relative to the scroll offset axis as specified by [AxisDirection].
- [CustomScrollView.anchor], the relative position of the zero scroll offset in a viewport and inflection point for [AxisDirection]s of the same cardinal [Axis].
- [axisDirectionIsReversed], which returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

A direction in the [Axis.vertical] where zero is at the bottom and positive values are above it: `⇈`

Alphabetical content with a [GrowthDirection.forward] would have the A at the bottom and the Z at the top.

For example, the behavior of a [ListView] with [ListView.reverse] set to true would have this axis direction.

See also:

- [axisDirectionIsReversed], which returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

A direction in the [Axis.horizontal] where zero is on the left and positive values are to the right of it: `⇉`

Alphabetical content with a [GrowthDirection.forward] would have the A on the left and the Z on the right. This is the ordinary reading order for a horizontal set of tabs in an English application, for example.

For example, the behavior of a [ListView] with [ListView.scrollDirection] set to [Axis.horizontal] would have this axis direction.

See also:

- [axisDirectionIsReversed], which returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

A direction in the [Axis.vertical] where zero is at the top and positive values are below it: `⇊`

Alphabetical content with a [GrowthDirection.forward] would have the A at the top and the Z at the bottom. This is the ordinary reading order for a vertical list.

For example, the default behavior of a [ListView] would have this axis direction.

See also:

- [axisDirectionIsReversed], which returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

A direction in the [Axis.horizontal] where zero is to the right and positive values are to the left of it: `⇇`

Alphabetical content with a [GrowthDirection.forward] would have the A at the right and the Z at the left. This is the ordinary reading order for a horizontal set of tabs in a Hebrew application, for example.

For example, the behavior of a [ListView] with [ListView.scrollDirection] set to [Axis.horizontal] and [ListView.reverse] set to true would have this axis direction.

See also:

- [axisDirectionIsReversed], which returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

# axisDirectionToAxis()

```dart
Axis axisDirectionToAxis(AxisDirection axisDirection)
```

Returns the [Axis] that contains the given [AxisDirection].

Specifically, returns [Axis.vertical] for [AxisDirection.up] and [AxisDirection.down] and returns [Axis.horizontal] for [AxisDirection.left] and [AxisDirection.right].

# textDirectionToAxisDirection()

```dart
AxisDirection textDirectionToAxisDirection(TextDirection textDirection)
```

Returns the [AxisDirection] in which reading occurs in the given [TextDirection].

Specifically, returns [AxisDirection.left] for [TextDirection.rtl] and [AxisDirection.right] for [TextDirection.ltr].

# flipAxisDirection()

```dart
AxisDirection flipAxisDirection(AxisDirection axisDirection)
```

Returns the opposite of the given [AxisDirection].

Specifically, returns [AxisDirection.up] for [AxisDirection.down] (and vice versa), as well as [AxisDirection.left] for [AxisDirection.right] (and vice versa).

See also:

- [flipAxis], which does the same thing for [Axis] values.

# axisDirectionIsReversed()

```dart
bool axisDirectionIsReversed(AxisDirection axisDirection)
```

Returns whether traveling along the given axis direction visits coordinates along that axis in numerically decreasing order.

Specifically, returns true for [AxisDirection.up] and [AxisDirection.left] and false for [AxisDirection.down] and [AxisDirection.right].
