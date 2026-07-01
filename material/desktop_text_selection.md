# DesktopTextSelectionControls

```dart
class DesktopTextSelectionControls extends TextSelectionControls {}
```

Desktop Material styled text selection controls.

The [desktopTextSelectionControls] global variable has a suitable instance of this class.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

Desktop has no text selection handles.

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

Builder for the Material-style desktop copy/paste text selection toolbar.

### buildHandle()

```dart
Widget buildHandle(BuildContext context, TextSelectionHandleType type, double textLineHeight, [VoidCallback? onTap])
```

Builds the text selection handles, but desktop has none.

### getHandleAnchor()

```dart
Offset getHandleAnchor(TextSelectionHandleType type, double textLineHeight)
```

Gets the position for the text selection handles, but desktop has none.

### canSelectAll()

```dart
bool canSelectAll(TextSelectionDelegate delegate)
```

### handleSelectAll()

```dart
void handleSelectAll(TextSelectionDelegate delegate)
```

# desktopTextSelectionHandleControls

```dart
TextSelectionControls desktopTextSelectionHandleControls
```

Desktop text selection handle controls that loosely follow Material design conventions.

# desktopTextSelectionControls

```dart
TextSelectionControls desktopTextSelectionControls
```

Desktop text selection controls that loosely follow Material design conventions.
