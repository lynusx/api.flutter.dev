# SpellCheckSuggestionsToolbar

```dart
class SpellCheckSuggestionsToolbar extends StatelessWidget {}
```

The default spell check suggestions toolbar for Android.

Tries to position itself below the [anchor], but if it doesn't fit, then it readjusts to fit above bottom view insets.

See also:

- [CupertinoSpellCheckSuggestionsToolbar], which is similar but builds an iOS-style spell check toolbar.

### SpellCheckSuggestionsToolbar()

```dart
SpellCheckSuggestionsToolbar({dynamic key, required Offset anchor, required List<ContextMenuButtonItem> buttonItems})
```

Constructs a [SpellCheckSuggestionsToolbar].

[buttonItems] must not contain more than four items, generally three suggestions and one delete button.

### SpellCheckSuggestionsToolbar.editableText()

```dart
SpellCheckSuggestionsToolbar.editableText({dynamic key, required EditableTextState editableTextState})
```

Constructs a [SpellCheckSuggestionsToolbar] with the default children for an [EditableText].

See also:

- [CupertinoSpellCheckSuggestionsToolbar.editableText], which is similar but builds an iOS-style toolbar.

### anchor

```dart
Offset anchor
```

{@template flutter.material.SpellCheckSuggestionsToolbar.anchor} The focal point below which the toolbar attempts to position itself. {@endtemplate}

### buttonItems

```dart
List<ContextMenuButtonItem> buttonItems
```

The [ContextMenuButtonItem]s that will be turned into the correct button widgets and displayed in the spell check suggestions toolbar.

Must not contain more than four items, typically three suggestions and a delete button.

See also:

- [AdaptiveTextSelectionToolbar.buttonItems], the list of [ContextMenuButtonItem]s that are used to build the buttons of the text selection toolbar.
- [CupertinoSpellCheckSuggestionsToolbar.buttonItems], the list of [ContextMenuButtonItem]s used to build the Cupertino style spell check suggestions toolbar.

### buildButtonItems()

```dart
List<ContextMenuButtonItem>? buildButtonItems(EditableTextState editableTextState)
```

Builds the button items for the toolbar based on the available spell check suggestions.

### getToolbarAnchor()

```dart
Offset getToolbarAnchor(TextSelectionToolbarAnchors anchors)
```

Determines the Offset that the toolbar will be anchored to.

### build()

```dart
Widget build(BuildContext context)
```
