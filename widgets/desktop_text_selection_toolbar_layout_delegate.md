@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'text_selection_toolbar_layout_delegate.dart';

# DesktopTextSelectionToolbarLayoutDelegate

```dart
class DesktopTextSelectionToolbarLayoutDelegate extends SingleChildLayoutDelegate {}
```

Positions the toolbar at [anchor] if it fits, otherwise moves it so that it just fits fully on-screen.

See also:

- [desktopTextSelectionControls], which uses this to position itself.
- [cupertinoDesktopTextSelectionControls], which uses this to position itself.
- [TextSelectionToolbarLayoutDelegate], which does a similar layout for the mobile text selection toolbars.

### DesktopTextSelectionToolbarLayoutDelegate()

```dart
DesktopTextSelectionToolbarLayoutDelegate({required Offset anchor})
```

Creates an instance of TextSelectionToolbarLayoutDelegate.

### anchor

```dart
Offset anchor
```

The point at which to render the menu, if possible.

Should be provided in local coordinates.

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
bool shouldRelayout(DesktopTextSelectionToolbarLayoutDelegate oldDelegate)
```
