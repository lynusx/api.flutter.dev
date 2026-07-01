@docImport 'package:flutter/material.dart';

# CupertinoSpellCheckSuggestionsToolbar

```dart
class CupertinoSpellCheckSuggestionsToolbar extends StatelessWidget {}
```

The default spell check suggestions toolbar for iOS.

Tries to position itself below the [anchors], but if it doesn't fit, then it readjusts to fit above bottom view insets.

See also:

- [SpellCheckSuggestionsToolbar], which is similar but for both the Material and Cupertino libraries.

### CupertinoSpellCheckSuggestionsToolbar()

```dart
CupertinoSpellCheckSuggestionsToolbar({dynamic key, required TextSelectionToolbarAnchors anchors, required List<ContextMenuButtonItem> buttonItems})
```

Constructs a [CupertinoSpellCheckSuggestionsToolbar].

[buttonItems] must not contain more than three items.

### CupertinoSpellCheckSuggestionsToolbar.editableText()

```dart
CupertinoSpellCheckSuggestionsToolbar.editableText({dynamic key, required EditableTextState editableTextState})
```

Constructs a [CupertinoSpellCheckSuggestionsToolbar] with the default children for an [EditableText].

See also:

- [SpellCheckSuggestionsToolbar.editableText], which is similar but builds an Android-style toolbar.

### anchors

```dart
TextSelectionToolbarAnchors anchors
```

The location on which to anchor the menu.

### buttonItems

```dart
List<ContextMenuButtonItem> buttonItems
```

The [ContextMenuButtonItem]s that will be turned into the correct button widgets and displayed in the spell check suggestions toolbar.

Must not contain more than three items.

See also:

- [AdaptiveTextSelectionToolbar.buttonItems], the list of [ContextMenuButtonItem]s that are used to build the buttons of the text selection toolbar.
- [SpellCheckSuggestionsToolbar.buttonItems], the list of [ContextMenuButtonItem]s used to build the Material style spell check suggestions toolbar.

### buildButtonItems()

```dart
List<ContextMenuButtonItem>? buildButtonItems(EditableTextState editableTextState)
```

Builds the button items for the toolbar based on the available spell check suggestions.

### build()

```dart
Widget build(BuildContext context)
```
