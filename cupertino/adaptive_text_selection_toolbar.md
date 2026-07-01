@docImport 'package:flutter/material.dart';

# CupertinoAdaptiveTextSelectionToolbar

```dart
class CupertinoAdaptiveTextSelectionToolbar extends StatelessWidget {}
```

The default Cupertino context menu for text selection for the current platform with the given children.

{@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.platforms} Builds the mobile Cupertino context menu on all mobile platforms, not just iOS, and builds the desktop Cupertino context menu on all desktop platforms, not just MacOS. For a widget that builds the native-looking context menu for all platforms, see [AdaptiveTextSelectionToolbar]. {@endtemplate}

See also:

- [AdaptiveTextSelectionToolbar], which does the same thing as this widget but for all platforms, not just the Cupertino-styled platforms.
- [CupertinoAdaptiveTextSelectionToolbar.getAdaptiveButtons], which builds the Cupertino button Widgets for the current platform given [ContextMenuButtonItem]s.

### CupertinoAdaptiveTextSelectionToolbar()

```dart
CupertinoAdaptiveTextSelectionToolbar({dynamic key, required List<Widget>? children, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [CupertinoAdaptiveTextSelectionToolbar] with the given [children].

See also:

{@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.buttonItems}

- [CupertinoAdaptiveTextSelectionToolbar.buttonItems], which takes a list of [ContextMenuButtonItem]s instead of [children] widgets. {@endtemplate} {@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editable}
- [CupertinoAdaptiveTextSelectionToolbar.editable], which builds the default Cupertino children for an editable field. {@endtemplate} {@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editableText}
- [CupertinoAdaptiveTextSelectionToolbar.editableText], which builds the default Cupertino children for an [EditableText]. {@endtemplate} {@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.selectable}
- [CupertinoAdaptiveTextSelectionToolbar.selectable], which builds the Cupertino children for content that is selectable but not editable. {@endtemplate}

### CupertinoAdaptiveTextSelectionToolbar.buttonItems()

```dart
CupertinoAdaptiveTextSelectionToolbar.buttonItems({dynamic key, required List<ContextMenuButtonItem>? buttonItems, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [CupertinoAdaptiveTextSelectionToolbar] whose children will be built from the given [buttonItems].

See also:

{@template flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.new}

- [CupertinoAdaptiveTextSelectionToolbar.new], which takes the children directly as a list of widgets. {@endtemplate} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editable} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editableText} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.selectable}

### CupertinoAdaptiveTextSelectionToolbar.editable()

```dart
CupertinoAdaptiveTextSelectionToolbar.editable({dynamic key, required ClipboardStatus clipboardStatus, required VoidCallback? onCopy, required VoidCallback? onCut, required VoidCallback? onPaste, required VoidCallback? onSelectAll, required VoidCallback? onLookUp, required VoidCallback? onSearchWeb, required VoidCallback? onShare, required VoidCallback? onLiveTextInput, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [CupertinoAdaptiveTextSelectionToolbar] with the default children for an editable field.

If a callback is null, then its corresponding button will not be built.

See also:

- [AdaptiveTextSelectionToolbar.editable], which is similar to this but includes Material and Cupertino toolbars. {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.new} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editableText} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.selectable}

### CupertinoAdaptiveTextSelectionToolbar.editableText()

```dart
CupertinoAdaptiveTextSelectionToolbar.editableText({dynamic key, required EditableTextState editableTextState})
```

Create an instance of [CupertinoAdaptiveTextSelectionToolbar] with the default children for an [EditableText].

See also:

- [AdaptiveTextSelectionToolbar.editableText], which is similar to this but includes Material and Cupertino toolbars. {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.new} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editable} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.selectable}

### CupertinoAdaptiveTextSelectionToolbar.selectable()

```dart
CupertinoAdaptiveTextSelectionToolbar.selectable({dynamic key, required VoidCallback onCopy, required VoidCallback onSelectAll, required SelectionGeometry selectionGeometry, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [CupertinoAdaptiveTextSelectionToolbar] with the default children for selectable, but not editable, content.

See also:

- [AdaptiveTextSelectionToolbar.selectable], which is similar to this but includes Material and Cupertino toolbars. {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.new} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editable} {@macro flutter.cupertino.CupertinoAdaptiveTextSelectionToolbar.editableText}

### anchors

```dart
TextSelectionToolbarAnchors anchors
```

{@macro flutter.material.AdaptiveTextSelectionToolbar.anchors}

### children

```dart
List<Widget>? children
```

The children of the toolbar, typically buttons.

### buttonItems

```dart
List<ContextMenuButtonItem>? buttonItems
```

The [ContextMenuButtonItem]s that will be turned into the correct button widgets for the current platform.

### getAdaptiveButtons()

```dart
Iterable<Widget> getAdaptiveButtons(BuildContext context, List<ContextMenuButtonItem> buttonItems)
```

Returns a List of Widgets generated by turning [buttonItems] into the default context menu buttons for Cupertino on the current platform.

This is useful when building a text selection toolbar with the default button appearance for the given platform, but where the toolbar and/or the button actions and labels may be custom.

Does not build Material buttons. On non-Apple platforms, Cupertino buttons will still be used, because the Cupertino library does not access the Material library. To get the native-looking buttons on every platform, use [AdaptiveTextSelectionToolbar.getAdaptiveButtons] in the Material library.

See also:

- [AdaptiveTextSelectionToolbar.getAdaptiveButtons], which is the Material equivalent of this class and builds only the Material buttons. It includes a live example of using `getAdaptiveButtons`.

### build()

```dart
Widget build(BuildContext context)
```
