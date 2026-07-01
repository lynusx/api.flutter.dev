@docImport 'package:flutter/material.dart';

# TextSelectionToolbarAnchors

```dart
class TextSelectionToolbarAnchors {}
```

The position information for a text selection toolbar.

Typically, a menu will attempt to position itself at [primaryAnchor], and if that's not possible, then it will use [secondaryAnchor] instead, if it exists.

See also:

- [AdaptiveTextSelectionToolbar.anchors], which is of this type.

### TextSelectionToolbarAnchors()

```dart
TextSelectionToolbarAnchors({required Offset primaryAnchor, Offset? secondaryAnchor})
```

Creates an instance of [TextSelectionToolbarAnchors] directly from the anchor points.

### TextSelectionToolbarAnchors.fromSelection()

```dart
TextSelectionToolbarAnchors.fromSelection({required RenderBox renderBox, required double startGlyphHeight, required double endGlyphHeight, required List<TextSelectionPoint> selectionEndpoints})
```

Creates an instance of [TextSelectionToolbarAnchors] for some selection.

### getSelectionRect()

```dart
Rect getSelectionRect(RenderBox renderBox, double startGlyphHeight, double endGlyphHeight, List<TextSelectionPoint> selectionEndpoints)
```

Returns the [Rect] covering the given selection in the given [RenderBox] in global coordinates.

### primaryAnchor

```dart
Offset primaryAnchor
```

The location that the toolbar should attempt to position itself at.

If the toolbar doesn't fit at this location, use [secondaryAnchor] if it exists.

### secondaryAnchor

```dart
Offset? secondaryAnchor
```

The fallback position that should be used if [primaryAnchor] doesn't work.
