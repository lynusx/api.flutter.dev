@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'basic.dart';

# TextSelectionToolbarLayoutDelegate

```dart
class TextSelectionToolbarLayoutDelegate extends SingleChildLayoutDelegate {}
```

A [SingleChildLayoutDelegate] for use with [CustomSingleChildLayout] that positions its child above [anchorAbove] if it fits, or otherwise below [anchorBelow].

Primarily intended for use with toolbars or context menus.

See also:

- [TextSelectionToolbar], which uses this to position itself.
- [CupertinoTextSelectionToolbar], which also uses this to position itself.

### TextSelectionToolbarLayoutDelegate()

```dart
TextSelectionToolbarLayoutDelegate({required Offset anchorAbove, required Offset anchorBelow, bool? fitsAbove})
```

Creates an instance of TextSelectionToolbarLayoutDelegate.

The [fitsAbove] parameter is optional; if omitted, it will be calculated.

### anchorAbove

```dart
Offset anchorAbove
```

{@macro flutter.material.TextSelectionToolbar.anchorAbove}

Should be provided in local coordinates.

### anchorBelow

```dart
Offset anchorBelow
```

{@macro flutter.material.TextSelectionToolbar.anchorAbove}

Should be provided in local coordinates.

### fitsAbove

```dart
bool? fitsAbove
```

Whether or not the child should be considered to fit above anchorAbove.

Typically used to force the child to be drawn at anchorAbove even when it doesn't fit, such as when the Material [TextSelectionToolbar] draws an open overflow menu.

If not provided, it will be calculated.

### centerOn()

```dart
double centerOn(double position, double width, double max)
```

Return the distance from zero that centers `width` as closely as possible to `position` from zero while fitting between zero and `max`.

### getConstraintsForChild()

```dart
BoxConstraints getConstraintsForChild(BoxConstraints constraints)
```

### getPositionForChild()

```dart
Offset getPositionForChild(Size size, Size childSize)
```

### shouldRelayout()

```dart
bool shouldRelayout(TextSelectionToolbarLayoutDelegate oldDelegate)
```
