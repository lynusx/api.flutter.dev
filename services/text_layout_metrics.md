# TextLayoutMetrics

```dart
abstract class TextLayoutMetrics {}
```

A read-only interface for accessing visual information about the implementing text.

### isWhitespace()

```dart
bool isWhitespace(int codeUnit)
```

Check if the given code unit is a white space or separator character.

Includes newline characters from ASCII and separators from the [unicode separator category](https://www.compart.com/en/unicode/category/Zs)

### isLineTerminator()

```dart
bool isLineTerminator(int codeUnit)
```

Check if the given code unit is a line terminator character.

Includes newline characters from ASCII (https://www.unicode.org/standard/reports/tr13/tr13-5.html).

### getLineAtOffset()

```dart
TextSelection getLineAtOffset(TextPosition position)
```

{@template flutter.services.TextLayoutMetrics.getLineAtOffset} Return a [TextSelection] containing the line of the given [TextPosition]. {@endtemplate}

### getWordBoundary()

```dart
TextRange getWordBoundary(TextPosition position)
```

{@macro flutter.painting.TextPainter.getWordBoundary}

### getTextPositionAbove()

```dart
TextPosition getTextPositionAbove(TextPosition position)
```

{@template flutter.services.TextLayoutMetrics.getTextPositionAbove} Returns the TextPosition above the given offset into the text.

If the offset is already on the first line, the given offset will be returned. {@endtemplate}

### getTextPositionBelow()

```dart
TextPosition getTextPositionBelow(TextPosition position)
```

{@template flutter.services.TextLayoutMetrics.getTextPositionBelow} Returns the TextPosition below the given offset into the text.

If the offset is already on the last line, the given offset will be returned. {@endtemplate}
