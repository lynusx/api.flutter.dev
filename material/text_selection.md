# MaterialTextSelectionHandleControls

```dart
class MaterialTextSelectionHandleControls extends MaterialTextSelectionControls with TextSelectionHandleControls {}
```

Android Material styled text selection handle controls.

Specifically does not manage the toolbar, which is left to [EditableText.contextMenuBuilder].

# MaterialTextSelectionControls

```dart
class MaterialTextSelectionControls extends TextSelectionControls {}
```

Android Material styled text selection controls.

The [materialTextSelectionControls] global variable has a suitable instance of this class.

### getHandleSize()

```dart
Size getHandleSize(double textLineHeight)
```

Returns the size of the Material handle.

### buildToolbar()

```dart
Widget buildToolbar(BuildContext context, Rect globalEditableRegion, double textLineHeight, Offset selectionMidpoint, List<TextSelectionPoint> endpoints, TextSelectionDelegate delegate, ValueListenable<ClipboardStatus>? clipboardStatus, Offset? lastSecondaryTapDownPosition)
```

Builder for material-style copy/paste text selection toolbar.

### buildHandle()

```dart
Widget buildHandle(BuildContext context, TextSelectionHandleType type, double textHeight, [VoidCallback? onTap])
```

Builder for material-style text selection handles.

### getHandleAnchor()

```dart
Offset getHandleAnchor(TextSelectionHandleType type, double textLineHeight)
```

Gets anchor for material-style text selection handles.

See [TextSelectionControls.getHandleAnchor].

### canSelectAll()

```dart
bool canSelectAll(TextSelectionDelegate delegate)
```

# materialTextSelectionHandleControls

```dart
TextSelectionControls materialTextSelectionHandleControls
```

Text selection handle controls that follow the Material Design specification.

# materialTextSelectionControls

```dart
TextSelectionControls materialTextSelectionControls
```

Text selection controls that follow the Material Design specification.
