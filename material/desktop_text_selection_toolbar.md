@docImport 'adaptive_text_selection_toolbar.dart'; @docImport 'desktop_text_selection_toolbar_button.dart';

# DesktopTextSelectionToolbar

```dart
class DesktopTextSelectionToolbar extends StatelessWidget {}
```

A Material-style desktop text selection toolbar.

Typically displays buttons for text manipulation, e.g. copying and pasting text.

Tries to position its top left corner as closely as possible to [anchor] while remaining fully inside the viewport.

See also:

- [AdaptiveTextSelectionToolbar], which builds the toolbar for the current platform.
- [TextSelectionToolbar], which is similar, but builds an Android-style toolbar.

### DesktopTextSelectionToolbar()

```dart
DesktopTextSelectionToolbar({dynamic key, required Offset anchor, required List<Widget> children})
```

Creates a const instance of DesktopTextSelectionToolbar.

### anchor

```dart
Offset anchor
```

{@template flutter.material.DesktopTextSelectionToolbar.anchor} The point where the toolbar will attempt to position itself as closely as possible. {@endtemplate}

### children

```dart
List<Widget> children
```

{@macro flutter.material.TextSelectionToolbar.children}

See also:

- [DesktopTextSelectionToolbarButton], which builds a default Material-style desktop text selection toolbar text button.

### build()

```dart
Widget build(BuildContext context)
```
