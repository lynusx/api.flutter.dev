# UntilPredicate

```dart
typedef UntilPredicate = bool Function(int offset, bool forward)
```

Signature for a predicate that takes an offset into a UTF-16 string, and a boolean that indicates the search direction.

# TextBoundary

```dart
abstract class TextBoundary {}
```

An interface for retrieving the logical text boundary (as opposed to the visual boundary) at a given code unit offset in a document.

Either the [getTextBoundaryAt] method, or both the [getLeadingTextBoundaryAt] method and the [getTrailingTextBoundaryAt] method must be implemented.

### TextBoundary()

```dart
TextBoundary()
```

A constant constructor to enable subclass override.

### getLeadingTextBoundaryAt()

```dart
int? getLeadingTextBoundaryAt(int position)
```

Returns the offset of the closest text boundary before or at the given `position`, or null if no boundaries can be found.

The return value, if not null, is usually less than or equal to `position`.

The range of the return value is given by the closed interval `[0, string.length]`.

### getTrailingTextBoundaryAt()

```dart
int? getTrailingTextBoundaryAt(int position)
```

Returns the offset of the closest text boundary after the given `position`, or null if there is no boundary can be found after `position`.

The return value, if not null, is usually greater than `position`.

The range of the return value is given by the closed interval `[0, string.length]`.

### getTextBoundaryAt()

```dart
TextRange getTextBoundaryAt(int position)
```

Returns the text boundary range that encloses the input position.

The returned [TextRange] may contain `-1`, which indicates no boundaries can be found in that direction.

# CharacterBoundary

```dart
class CharacterBoundary extends TextBoundary {}
```

A [TextBoundary] subclass for retrieving the range of the grapheme the given `position` is in.

The class is implemented using the [characters](https://pub.dev/packages/characters) package.

### CharacterBoundary()

```dart
CharacterBoundary(String _text)
```

Creates a [CharacterBoundary] with the text.

### getLeadingTextBoundaryAt()

```dart
int? getLeadingTextBoundaryAt(int position)
```

### getTrailingTextBoundaryAt()

```dart
int? getTrailingTextBoundaryAt(int position)
```

### getTextBoundaryAt()

```dart
TextRange getTextBoundaryAt(int position)
```

# LineBoundary

```dart
class LineBoundary extends TextBoundary {}
```

A [TextBoundary] subclass for locating closest line breaks to a given `position`.

When the given `position` points to a hard line break, the returned range is the line's content range before the hard line break, and does not contain the given `position`. For instance, the line breaks at `position = 1` for "a\nb" is `[0, 1)`, which does not contain the position `1`.

### LineBoundary()

```dart
LineBoundary(TextLayoutMetrics _textLayout)
```

Creates a [LineBoundary] with the text and layout information.

### getTextBoundaryAt()

```dart
TextRange getTextBoundaryAt(int position)
```

# ParagraphBoundary

```dart
class ParagraphBoundary extends TextBoundary {}
```

A text boundary that uses paragraphs as logical boundaries.

A paragraph is defined as the range between line terminators. If no line terminators exist then the paragraph boundary is the entire document.

### ParagraphBoundary()

```dart
ParagraphBoundary(String _text)
```

Creates a [ParagraphBoundary] with the text.

### getLeadingTextBoundaryAt()

```dart
int? getLeadingTextBoundaryAt(int position)
```

Returns the [int] representing the start position of the paragraph that bounds the given `position`. The returned [int] is the position of the code unit that follows the line terminator that encloses the desired paragraph.

### getTrailingTextBoundaryAt()

```dart
int? getTrailingTextBoundaryAt(int position)
```

Returns the [int] representing the end position of the paragraph that bounds the given `position`. The returned [int] is the position of the code unit representing the trailing line terminator that encloses the desired paragraph.

# DocumentBoundary

```dart
class DocumentBoundary extends TextBoundary {}
```

A text boundary that uses the entire document as logical boundary.

### DocumentBoundary()

```dart
DocumentBoundary(String _text)
```

Creates a [DocumentBoundary] with the text.

### getLeadingTextBoundaryAt()

```dart
int? getLeadingTextBoundaryAt(int position)
```

### getTrailingTextBoundaryAt()

```dart
int? getTrailingTextBoundaryAt(int position)
```
