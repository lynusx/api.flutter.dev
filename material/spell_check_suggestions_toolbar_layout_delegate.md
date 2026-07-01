@docImport 'spell_check_suggestions_toolbar.dart';

# SpellCheckSuggestionsToolbarLayoutDelegate

```dart
class SpellCheckSuggestionsToolbarLayoutDelegate extends SingleChildLayoutDelegate {}
```

Positions the toolbar below [anchor] or adjusts it higher to fit above the bottom view insets, if applicable.

See also:

- [SpellCheckSuggestionsToolbar], which uses this to position itself.

### SpellCheckSuggestionsToolbarLayoutDelegate()

```dart
SpellCheckSuggestionsToolbarLayoutDelegate({required Offset anchor})
```

Creates an instance of [SpellCheckSuggestionsToolbarLayoutDelegate].

### anchor

```dart
Offset anchor
```

{@macro flutter.material.SpellCheckSuggestionsToolbar.anchor}

Should be provided in local coordinates.

### getConstraintsForChild()

```dart
BoxConstraints getConstraintsForChild(BoxConstraints constraints)
```

### getPositionForChild()

```dart
Offset getPositionForChild(Size size, Size childSize)
```

### shouldRelayout()

```dart
bool shouldRelayout(SpellCheckSuggestionsToolbarLayoutDelegate oldDelegate)
```
