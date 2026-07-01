@docImport 'adaptive_text_selection_toolbar.dart'; @docImport 'spell_check_suggestions_toolbar.dart'; @docImport 'text_selection_toolbar_text_button.dart';

# TextSelectionToolbar

```dart
class TextSelectionToolbar extends StatelessWidget {}
```

A fully-functional Material-style text selection toolbar.

Tries to position itself above [anchorAbove], but if it doesn't fit, then it positions itself below [anchorBelow].

If any children don't fit in the menu, an overflow menu will automatically be created.

See also:

- [AdaptiveTextSelectionToolbar], which builds the toolbar for the current platform.
- [CupertinoTextSelectionToolbar], which is similar, but builds an iOS- style toolbar.

### TextSelectionToolbar()

```dart
TextSelectionToolbar({dynamic key, required Offset anchorAbove, required Offset anchorBelow, ToolbarBuilder toolbarBuilder = _defaultToolbarBuilder, required List<Widget> children})
```

Creates an instance of TextSelectionToolbar.

### anchorAbove

```dart
Offset anchorAbove
```

{@template flutter.material.TextSelectionToolbar.anchorAbove} The focal point above which the toolbar attempts to position itself.

If there is not enough room above before reaching the top of the screen, then the toolbar will position itself below [anchorBelow]. {@endtemplate}

### anchorBelow

```dart
Offset anchorBelow
```

{@template flutter.material.TextSelectionToolbar.anchorBelow} The focal point below which the toolbar attempts to position itself, if it doesn't fit above [anchorAbove]. {@endtemplate}

### children

```dart
List<Widget> children
```

{@template flutter.material.TextSelectionToolbar.children} The children that will be displayed in the text selection toolbar.

Typically these are buttons.

Must not be empty. {@endtemplate}

See also:

- [TextSelectionToolbarTextButton], which builds a default Material- style text selection toolbar text button.

### toolbarBuilder

```dart
ToolbarBuilder toolbarBuilder
```

{@template flutter.material.TextSelectionToolbar.toolbarBuilder} Builds the toolbar container.

Useful for customizing the high-level background of the toolbar. The given child Widget will contain all of the [children]. {@endtemplate}

### kHandleSize

```dart
double kHandleSize
```

The size of the text selection handles.

See also:

- [SpellCheckSuggestionsToolbar], which references this value to calculate the padding between the toolbar and anchor.

### kToolbarContentDistanceBelow

```dart
double kToolbarContentDistanceBelow
```

Padding between the toolbar and the anchor.

### build()

```dart
Widget build(BuildContext context)
```
