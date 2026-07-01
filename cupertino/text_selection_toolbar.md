@docImport 'package:flutter/material.dart';

# CupertinoToolbarBuilder

```dart
typedef CupertinoToolbarBuilder = Widget Function(BuildContext context, Offset anchorAbove, Offset anchorBelow, Widget child)
```

The type for a Function that builds a toolbar's container with the given child.

The anchor is provided in global coordinates.

See also:

- [CupertinoTextSelectionToolbar.toolbarBuilder], which is of this type.
- [TextSelectionToolbar.toolbarBuilder], which is similar, but for an Material-style toolbar.

# CupertinoTextSelectionToolbar

```dart
class CupertinoTextSelectionToolbar extends StatelessWidget {}
```

An iOS-style text selection toolbar.

Typically displays buttons for text manipulation, e.g. copying and pasting text.

Tries to position itself above [anchorAbove], but if it doesn't fit, then it positions itself below [anchorBelow].

If any children don't fit in the menu, an overflow menu will automatically be created.

See also:

- [AdaptiveTextSelectionToolbar], which builds the toolbar for the current platform.
- [TextSelectionToolbar], which is similar, but builds an Android-style toolbar.

### CupertinoTextSelectionToolbar()

```dart
CupertinoTextSelectionToolbar({dynamic key, required Offset anchorAbove, required Offset anchorBelow, required List<Widget> children, CupertinoToolbarBuilder toolbarBuilder = _defaultToolbarBuilder})
```

Creates an instance of CupertinoTextSelectionToolbar.

### anchorAbove

```dart
Offset anchorAbove
```

{@macro flutter.material.TextSelectionToolbar.anchorAbove}

### anchorBelow

```dart
Offset anchorBelow
```

{@macro flutter.material.TextSelectionToolbar.anchorBelow}

### children

```dart
List<Widget> children
```

{@macro flutter.material.TextSelectionToolbar.children}

See also:

- [CupertinoTextSelectionToolbarButton], which builds a default Cupertino-style text selection toolbar text button.

### toolbarBuilder

```dart
CupertinoToolbarBuilder toolbarBuilder
```

{@macro flutter.material.TextSelectionToolbar.toolbarBuilder}

The given anchor and isAbove can be used to position an arrow, as in the default Cupertino toolbar.

### kToolbarScreenPadding

```dart
double kToolbarScreenPadding
```

Minimal padding from all edges of the selection toolbar to all edges of the viewport.

See also:

- [SpellCheckSuggestionsToolbar], which uses this same value for its padding from the edges of the viewport.
- [TextSelectionToolbar], which uses this same value as well.

### build()

```dart
Widget build(BuildContext context)
```
