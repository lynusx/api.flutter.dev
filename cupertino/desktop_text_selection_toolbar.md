@docImport 'package:flutter/material.dart';

@docImport 'adaptive_text_selection_toolbar.dart'; @docImport 'desktop_text_selection_toolbar_button.dart';

# CupertinoDesktopTextSelectionToolbar

```dart
class CupertinoDesktopTextSelectionToolbar extends StatelessWidget {}
```

A macOS-style text selection toolbar.

Typically displays buttons for text manipulation, e.g. copying and pasting text.

Tries to position itself as closely as possible to [anchor] while remaining fully inside the viewport.

See also:

- [CupertinoAdaptiveTextSelectionToolbar], where this is used to build the toolbar for desktop platforms.
- [AdaptiveTextSelectionToolbar], where this is used to build the toolbar on macOS.
- [DesktopTextSelectionToolbar], which is similar but builds a Material-style desktop toolbar.

### CupertinoDesktopTextSelectionToolbar()

```dart
CupertinoDesktopTextSelectionToolbar({dynamic key, required Offset anchor, required List<Widget> children})
```

Creates a const instance of CupertinoTextSelectionToolbar.

### anchor

```dart
Offset anchor
```

{@macro flutter.material.DesktopTextSelectionToolbar.anchor}

### children

```dart
List<Widget> children
```

{@macro flutter.material.TextSelectionToolbar.children}

See also:

- [CupertinoDesktopTextSelectionToolbarButton], which builds a default macOS-style text selection toolbar text button.

### build()

```dart
Widget build(BuildContext context)
```
