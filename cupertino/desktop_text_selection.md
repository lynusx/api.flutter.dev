# CupertinoDesktopTextSelectionControls

```dart
class CupertinoDesktopTextSelectionControls extends TextSelectionControls {}
```

Desktop Cupertino styled text selection controls.

The [cupertinoDesktopTextSelectionControls] global variable has a suitable instance of this class.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

Desktop has no text selection handles.

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

Builder for the MacOS-style copy/paste text selection toolbar.

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

### handleSelectAll()

```dart
void handleSelectAll(TextSelectionDelegate delegate)
```

# cupertinoDesktopTextSelectionHandleControls

```dart
TextSelectionControls cupertinoDesktopTextSelectionHandleControls
```

Text selection handle controls that follow MacOS design conventions.

# cupertinoDesktopTextSelectionControls

```dart
TextSelectionControls cupertinoDesktopTextSelectionControls
```

Text selection controls that follows MacOS design conventions.
