# TextSelection

```dart
class TextSelection extends TextRange {}
```

A range of text that represents a selection.

### TextSelection()

```dart
TextSelection({required int baseOffset, required int extentOffset, TextAffinity affinity = TextAffinity.downstream, bool isDirectional = false})
```

Creates a text selection.

### TextSelection.collapsed()

```dart
TextSelection.collapsed({required int offset, TextAffinity affinity = TextAffinity.downstream})
```

Creates a collapsed selection at the given offset.

A collapsed selection starts and ends at the same offset, which means it contains zero characters but instead serves as an insertion point in the text.

### TextSelection.fromPosition()

```dart
TextSelection.fromPosition(TextPosition position)
```

Creates a collapsed selection at the given text position.

A collapsed selection starts and ends at the same offset, which means it contains zero characters but instead serves as an insertion point in the text.

### baseOffset

```dart
int baseOffset
```

The offset at which the selection originates.

Might be larger than, smaller than, or equal to extent.

### extentOffset

```dart
int extentOffset
```

The offset at which the selection terminates.

When the user uses the arrow keys to adjust the selection, this is the value that changes. Similarly, if the current theme paints a caret on one side of the selection, this is the location at which to paint the caret.

Might be larger than, smaller than, or equal to base.

### affinity

```dart
TextAffinity affinity
```

If the text range is collapsed and has more than one visual location (e.g., occurs at a line break), which of the two locations to use when painting the caret.

### isDirectional

```dart
bool isDirectional
```

Whether this selection has disambiguated its base and extent.

On some platforms, the base and extent are not disambiguated until the first time the user adjusts the selection. At that point, either the start or the end of the selection becomes the base and the other one becomes the extent and is adjusted.

### base

```dart
TextPosition get base
```

The position at which the selection originates.

{@template flutter.services.TextSelection.TextAffinity} The [TextAffinity] of the resulting [TextPosition] is based on the relative logical position in the text to the other selection endpoint:

- if [baseOffset] < [extentOffset], [base] will have [TextAffinity.downstream] and [extent] will have [TextAffinity.upstream].
- if [baseOffset] > [extentOffset], [base] will have [TextAffinity.upstream] and [extent] will have [TextAffinity.downstream].
- if [baseOffset] == [extentOffset], [base] and [extent] will both have the collapsed selection's [affinity]. {@endtemplate}

Might be larger than, smaller than, or equal to extent.

### extent

```dart
TextPosition get extent
```

The position at which the selection terminates.

When the user uses the arrow keys to adjust the selection, this is the value that changes. Similarly, if the current theme paints a caret on one side of the selection, this is the location at which to paint the caret.

{@macro flutter.services.TextSelection.TextAffinity}

Might be larger than, smaller than, or equal to base.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### copyWith()

```dart
TextSelection copyWith({int? baseOffset, int? extentOffset, TextAffinity? affinity, bool? isDirectional})
```

Creates a new [TextSelection] based on the current selection, with the provided parameters overridden.

### expandTo()

```dart
TextSelection expandTo(TextPosition position, [bool extentAtIndex = false])
```

Returns the smallest [TextSelection] that this could expand to in order to include the given [TextPosition].

If the given [TextPosition] is already inside of the selection, then returns `this` without change.

The returned selection will always be a strict superset of the current selection. In other words, the selection grows to include the given [TextPosition].

If extentAtIndex is true, then the [TextSelection.extentOffset] will be placed at the given index regardless of the original order of it and [TextSelection.baseOffset]. Otherwise, their order will be preserved.

## Difference with [extendTo]

In contrast with this method, [extendTo] is a pivot; it holds [TextSelection.baseOffset] fixed while moving [TextSelection.extentOffset] to the given [TextPosition]. It doesn't strictly grow the selection and may collapse it or flip its order.

### extendTo()

```dart
TextSelection extendTo(TextPosition position)
```

Keeping the selection's [TextSelection.baseOffset] fixed, pivot the [TextSelection.extentOffset] to the given [TextPosition].

In some cases, the [TextSelection.baseOffset] and [TextSelection.extentOffset] may flip during this operation, and/or the size of the selection may shrink.

## Difference with [expandTo]

In contrast with this method, [expandTo] is strictly growth; the selection is grown to include the given [TextPosition] and will never shrink.
