@docImport 'selectable_text.dart'; @docImport 'selection_area.dart'; @docImport 'text_field.dart';

# AdaptiveTextSelectionToolbar

```dart
class AdaptiveTextSelectionToolbar extends StatelessWidget {}
```

The default context menu for text selection for the current platform.

{@template flutter.material.AdaptiveTextSelectionToolbar.contextMenuBuilders} Typically, this widget would be passed to `contextMenuBuilder` in a supported parent widget, such as:

- [EditableText.contextMenuBuilder]
- [TextField.contextMenuBuilder]
- [CupertinoTextField.contextMenuBuilder]
- [SelectionArea.contextMenuBuilder]
- [SelectableText.contextMenuBuilder] {@endtemplate}

See also:

- [EditableText.getEditableButtonItems], which returns the default [ContextMenuButtonItem]s for [EditableText] on the platform.
- [AdaptiveTextSelectionToolbar.getAdaptiveButtons], which builds the button Widgets for the current platform given [ContextMenuButtonItem]s.
- [CupertinoAdaptiveTextSelectionToolbar], which does the same thing as this widget but only for Cupertino context menus.
- [TextSelectionToolbar], the default toolbar for Android.
- [DesktopTextSelectionToolbar], the default toolbar for desktop platforms other than MacOS.
- [CupertinoTextSelectionToolbar], the default toolbar for iOS.
- [CupertinoDesktopTextSelectionToolbar], the default toolbar for MacOS.

### AdaptiveTextSelectionToolbar()

```dart
AdaptiveTextSelectionToolbar({dynamic key, required List<Widget>? children, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [AdaptiveTextSelectionToolbar] with the given [children].

See also:

{@template flutter.material.AdaptiveTextSelectionToolbar.buttonItems}

- [AdaptiveTextSelectionToolbar.buttonItems], which takes a list of [ContextMenuButtonItem]s instead of [children] widgets. {@endtemplate} {@template flutter.material.AdaptiveTextSelectionToolbar.editable}
- [AdaptiveTextSelectionToolbar.editable], which builds the default children for an editable field. {@endtemplate} {@template flutter.material.AdaptiveTextSelectionToolbar.editableText}
- [AdaptiveTextSelectionToolbar.editableText], which builds the default children for an [EditableText]. {@endtemplate} {@template flutter.material.AdaptiveTextSelectionToolbar.selectable}
- [AdaptiveTextSelectionToolbar.selectable], which builds the default children for content that is selectable but not editable. {@endtemplate}

### AdaptiveTextSelectionToolbar.buttonItems()

```dart
AdaptiveTextSelectionToolbar.buttonItems({dynamic key, required List<ContextMenuButtonItem>? buttonItems, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [AdaptiveTextSelectionToolbar] whose children will be built from the given [buttonItems].

See also:

{@template flutter.material.AdaptiveTextSelectionToolbar.new}

- [AdaptiveTextSelectionToolbar.new], which takes the children directly as a list of widgets. {@endtemplate} {@macro flutter.material.AdaptiveTextSelectionToolbar.editable} {@macro flutter.material.AdaptiveTextSelectionToolbar.editableText} {@macro flutter.material.AdaptiveTextSelectionToolbar.selectable}

### AdaptiveTextSelectionToolbar.editable()

```dart
AdaptiveTextSelectionToolbar.editable({dynamic key, required ClipboardStatus clipboardStatus, required VoidCallback? onCopy, required VoidCallback? onCut, required VoidCallback? onPaste, required VoidCallback? onSelectAll, required VoidCallback? onLookUp, required VoidCallback? onSearchWeb, required VoidCallback? onShare, required VoidCallback? onLiveTextInput, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [AdaptiveTextSelectionToolbar] with the default children for an editable field.

If an on* callback parameter is null, then its corresponding button will not be built.

These callbacks are called when their corresponding button is activated and only then. For example, `onPaste` is called when the user taps the "Paste" button in the context menu and not when the user pastes with the keyboard.

See also:

{@macro flutter.material.AdaptiveTextSelectionToolbar.new} {@macro flutter.material.AdaptiveTextSelectionToolbar.editableText} {@macro flutter.material.AdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.material.AdaptiveTextSelectionToolbar.selectable}

### AdaptiveTextSelectionToolbar.editableText()

```dart
AdaptiveTextSelectionToolbar.editableText({dynamic key, required EditableTextState editableTextState})
```

Create an instance of [AdaptiveTextSelectionToolbar] with the default children for an [EditableText].

See also:

{@macro flutter.material.AdaptiveTextSelectionToolbar.new} {@macro flutter.material.AdaptiveTextSelectionToolbar.editable} {@macro flutter.material.AdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.material.AdaptiveTextSelectionToolbar.selectable}

### AdaptiveTextSelectionToolbar.selectable()

```dart
AdaptiveTextSelectionToolbar.selectable({dynamic key, required VoidCallback onCopy, required VoidCallback onSelectAll, required VoidCallback? onShare, required SelectionGeometry selectionGeometry, required TextSelectionToolbarAnchors anchors})
```

Create an instance of [AdaptiveTextSelectionToolbar] with the default children for selectable, but not editable, content.

See also:

{@macro flutter.material.AdaptiveTextSelectionToolbar.new} {@macro flutter.material.AdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.material.AdaptiveTextSelectionToolbar.editable} {@macro flutter.material.AdaptiveTextSelectionToolbar.editableText}

### AdaptiveTextSelectionToolbar.selectableRegion()

```dart
AdaptiveTextSelectionToolbar.selectableRegion({dynamic key, required SelectableRegionState selectableRegionState})
```

Create an instance of [AdaptiveTextSelectionToolbar] with the default children for a [SelectableRegion].

See also:

{@macro flutter.material.AdaptiveTextSelectionToolbar.new} {@macro flutter.material.AdaptiveTextSelectionToolbar.buttonItems} {@macro flutter.material.AdaptiveTextSelectionToolbar.editable} {@macro flutter.material.AdaptiveTextSelectionToolbar.editableText} {@macro flutter.material.AdaptiveTextSelectionToolbar.selectable}

### buttonItems

```dart
List<ContextMenuButtonItem>? buttonItems
```

{@template flutter.material.AdaptiveTextSelectionToolbar.buttonItems} The [ContextMenuButtonItem]s that will be turned into the correct button widgets for the current platform. {@endtemplate}

### children

```dart
List<Widget>? children
```

The children of the toolbar, typically buttons.

### anchors

```dart
TextSelectionToolbarAnchors anchors
```

{@template flutter.material.AdaptiveTextSelectionToolbar.anchors} The location on which to anchor the menu. {@endtemplate}

### getButtonLabel()

```dart
String getButtonLabel(BuildContext context, ContextMenuButtonItem buttonItem)
```

Returns the default button label String for the button of the given [ContextMenuButtonType] on any platform.

### getAdaptiveButtons()

```dart
Iterable<Widget> getAdaptiveButtons(BuildContext context, List<ContextMenuButtonItem> buttonItems)
```

Returns a List of Widgets generated by turning [buttonItems] into the default context menu buttons for the current platform.

This is useful when building a text selection toolbar with the default button appearance for the given platform, but where the toolbar and/or the button actions and labels may be custom.

{@tool dartpad} This sample demonstrates how to use `getAdaptiveButtons` to generate default button widgets in a custom toolbar.

** See code in examples/api/lib/material/context_menu/editable_text_toolbar_builder.2.dart ** {@end-tool}

See also:

- [CupertinoAdaptiveTextSelectionToolbar.getAdaptiveButtons], which is the Cupertino equivalent of this class and builds only the Cupertino buttons.

### build()

```dart
Widget build(BuildContext context)
```
