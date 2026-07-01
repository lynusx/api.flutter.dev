# CupertinoTextSelectionHandleControls

```dart
class CupertinoTextSelectionHandleControls extends CupertinoTextSelectionControls with TextSelectionHandleControls {}
```

iOS Cupertino styled text selection handle controls.

Specifically does not manage the toolbar, which is left to [EditableText.contextMenuBuilder].

# CupertinoTextSelectionControls

```dart
class CupertinoTextSelectionControls extends TextSelectionControls {}
```

iOS Cupertino styled text selection controls.

The [cupertinoTextSelectionControls] global variable has a suitable instance of this class.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

Returns the size of the Cupertino handle.

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

Builder for iOS-style copy/paste text selection toolbar.

### buildHandle()

```dart
Widget buildHandle(BuildContext context, TextSelectionHandleType type, double textLineHeight, [VoidCallback? onTap])
```

Builder for iOS text selection edges.

### getHandleAnchor()

```dart
Offset getHandleAnchor(TextSelectionHandleType type, double textLineHeight)
```

Gets anchor for cupertino-style text selection handles.

See [TextSelectionControls.getHandleAnchor].

# cupertinoTextSelectionHandleControls

```dart
TextSelectionControls cupertinoTextSelectionHandleControls
```

Text selection handle controls that follow iOS design conventions.

# cupertinoTextSelectionControls

```dart
TextSelectionControls cupertinoTextSelectionControls
```

Text selection controls that follow iOS design conventions.
