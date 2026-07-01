@docImport 'package:flutter/widgets.dart';

# kDefaultFontSize

```dart
double kDefaultFontSize
```

The default font size if none is specified.

This should be kept in sync with the defaults set in the engine (e.g., LibTxt's text_style.h, paragraph_style.h).

# TextOverflow

```dart
enum TextOverflow {}
```

How overflowing text should be handled.

A [TextOverflow] can be passed to [Text] and [RichText] via their [Text.overflow] and [RichText.overflow] properties respectively.

Clip the overflowing text to fix its container.

Fade the overflowing text to transparent.

Use an ellipsis to indicate that the text has overflowed.

Render overflowing text outside of its container.

# PlaceholderDimensions

```dart
class PlaceholderDimensions {}
```

Holds the [Size] and baseline required to represent the dimensions of a placeholder in text.

Placeholders specify an empty space in the text layout, which is used to later render arbitrary inline widgets into defined by a [WidgetSpan].

See also:

- [WidgetSpan], a subclass of [InlineSpan] and [PlaceholderSpan] that represents an inline widget embedded within text. The space this widget takes is indicated by a placeholder.
- [RichText], a text widget that supports text inline widgets.

### PlaceholderDimensions()

```dart
PlaceholderDimensions({required Size size, required ui.PlaceholderAlignment alignment, TextBaseline? baseline, double? baselineOffset})
```

Constructs a [PlaceholderDimensions] with the specified parameters.

The `size` and `alignment` are required as a placeholder's dimensions require at least `size` and `alignment` to be fully defined.

### empty

```dart
PlaceholderDimensions empty
```

A constant representing an empty placeholder.

### size

```dart
Size size
```

Width and height dimensions of the placeholder.

### alignment

```dart
ui.PlaceholderAlignment alignment
```

How to align the placeholder with the text.

See also:

- [baseline], the baseline to align to when using [dart:ui.PlaceholderAlignment.baseline], [dart:ui.PlaceholderAlignment.aboveBaseline], or [dart:ui.PlaceholderAlignment.belowBaseline].
- [baselineOffset], the distance of the alphabetic baseline from the upper edge of the placeholder.

### baselineOffset

```dart
double? baselineOffset
```

Distance of the [baseline] from the upper edge of the placeholder.

Only used when [alignment] is [ui.PlaceholderAlignment.baseline].

### baseline

```dart
TextBaseline? baseline
```

The [TextBaseline] to align to. Used with:

- [ui.PlaceholderAlignment.baseline]
- [ui.PlaceholderAlignment.aboveBaseline]
- [ui.PlaceholderAlignment.belowBaseline]
- [ui.PlaceholderAlignment.middle]

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# TextWidthBasis

```dart
enum TextWidthBasis {}
```

The different ways of measuring the width of one or more lines of text.

See [Text.textWidthBasis], for example.

multiline text will take up the full width given by the parent. For single line text, only the minimum amount of width needed to contain the text will be used. A common use case for this is a standard series of paragraphs.

The width will be exactly enough to contain the longest line and no longer. A common use case for this is chat bubbles.

# WordBoundary

```dart
class WordBoundary extends TextBoundary {}
```

A [TextBoundary] subclass for locating word breaks.

The underlying implementation uses [UAX #29](https://unicode.org/reports/tr29/) defined default word boundaries.

The default word break rules can be tailored to meet the requirements of different use cases. For instance, the default rule set keeps horizontal whitespaces together as a single word, which may not make sense in a word-counting context -- "hello world" counts as 3 words instead of 2. An example is the [moveByWordBoundary] variant, which is a tailored word-break locator that more closely matches the default behavior of most platforms and editors when it comes to handling text editing keyboard shortcuts that move or delete word by word.

### getTextBoundaryAt()

```dart
TextRange getTextBoundaryAt(int position)
```

### moveByWordBoundary

```dart
TextBoundary moveByWordBoundary
```

Returns a [TextBoundary] suitable for handling keyboard navigation commands that change the current selection word by word.

This [TextBoundary] is used by text widgets in the flutter framework to provide default implementation for text editing shortcuts, for example, "delete to the previous word".

The implementation applies the same set of rules [WordBoundary] uses, except that word breaks end on a space separator or a punctuation will be skipped, to match the behavior of most platforms. Additional rules may be added in the future to better match platform behaviors.

# TextPainter

```dart
class TextPainter {}
```

An object that paints a [TextSpan] tree into a [Canvas].

To use a [TextPainter], follow these steps:

1.  Create a [TextSpan] tree and pass it to the [TextPainter] constructor.

2.  Call [layout] to prepare the paragraph.

3.  Call [paint] as often as desired to paint the paragraph.

4.  Call [dispose] when the object will no longer be accessed to release native resources. For [TextPainter] objects that are used repeatedly and stored on a [State] or [RenderObject], call [dispose] from [State.dispose] or [RenderObject.dispose] or similar. For [TextPainter] objects that are only used ephemerally, it is safe to immediately dispose them after the last call to methods or properties on the object.

If the width of the area into which the text is being painted changes, return to step 2. If the text to be painted changes, return to step 1.

The default text style color is white on non-web platforms and black on the web. If developing across both platforms, always set the text color explicitly.

### TextPainter()

```dart
TextPainter({InlineSpan? text, TextAlign textAlign = TextAlign.start, TextDirection? textDirection, double textScaleFactor = 1.0, TextScaler textScaler = const _UnspecifiedTextScaler(), int? maxLines, String? ellipsis, Locale? locale, StrutStyle? strutStyle, TextWidthBasis textWidthBasis = TextWidthBasis.parent, TextHeightBehavior? textHeightBehavior})
```

Creates a text painter that paints the given text.

The `text` and `textDirection` arguments are optional but [text] and [textDirection] must be non-null before calling [layout].

The [maxLines] property, if non-null, must be greater than zero.

### computeWidth()

```dart
double computeWidth({required InlineSpan text, required TextDirection textDirection, TextAlign textAlign = TextAlign.start, double textScaleFactor = 1.0, TextScaler textScaler = TextScaler.noScaling, int? maxLines, String? ellipsis, Locale? locale, StrutStyle? strutStyle, TextWidthBasis textWidthBasis = TextWidthBasis.parent, TextHeightBehavior? textHeightBehavior, double minWidth = 0.0, double maxWidth = double.infinity})
```

Computes the width of a configured [TextPainter].

This is a convenience method that creates a text painter with the supplied parameters, lays it out with the supplied [minWidth] and [maxWidth], and returns its [TextPainter.width] making sure to dispose the underlying resources. Doing this operation is expensive and should be avoided whenever it is possible to preserve the [TextPainter] to paint the text or get other information about it.

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth({required InlineSpan text, required TextDirection textDirection, TextAlign textAlign = TextAlign.start, double textScaleFactor = 1.0, TextScaler textScaler = TextScaler.noScaling, int? maxLines, String? ellipsis, Locale? locale, StrutStyle? strutStyle, TextWidthBasis textWidthBasis = TextWidthBasis.parent, TextHeightBehavior? textHeightBehavior, double minWidth = 0.0, double maxWidth = double.infinity})
```

Computes the max intrinsic width of a configured [TextPainter].

This is a convenience method that creates a text painter with the supplied parameters, lays it out with the supplied [minWidth] and [maxWidth], and returns its [TextPainter.maxIntrinsicWidth] making sure to dispose the underlying resources. Doing this operation is expensive and should be avoided whenever it is possible to preserve the [TextPainter] to paint the text or get other information about it.

### markNeedsLayout()

```dart
void markNeedsLayout()
```

Marks this text painter's layout information as dirty and removes cached information.

Uses this method to notify text painter to relayout in the case of layout changes in engine. In most cases, updating text painter properties in framework will automatically invoke this method.

### text

```dart
InlineSpan? get text
```

The (potentially styled) text to paint.

After this is set, you must call [layout] before the next call to [paint]. This and [textDirection] must be non-null before you call [layout].

The [InlineSpan] this provides is in the form of a tree that may contain multiple instances of [TextSpan]s and [WidgetSpan]s. To obtain a plain text representation of the contents of this [TextPainter], use [plainText].

### text

```dart
set text(InlineSpan? value)
```

### plainText

```dart
String get plainText
```

Returns a plain text version of the text to paint.

This uses [InlineSpan.toPlainText] to get the full contents of all nodes in the tree.

### textAlign

```dart
TextAlign get textAlign
```

How the text should be aligned horizontally.

After this is set, you must call [layout] before the next call to [paint].

The [textAlign] property defaults to [TextAlign.start].

### textAlign

```dart
set textAlign(TextAlign value)
```

### textDirection

```dart
TextDirection? get textDirection
```

The default directionality of the text.

This controls how the [TextAlign.start], [TextAlign.end], and [TextAlign.justify] values of [textAlign] are resolved.

This is also used to disambiguate how to render bidirectional text. For example, if the [text] is an English phrase followed by a Hebrew phrase, in a [TextDirection.ltr] context the English phrase will be on the left and the Hebrew phrase to its right, while in a [TextDirection.rtl] context, the English phrase will be on the right and the Hebrew phrase on its left.

After this is set, you must call [layout] before the next call to [paint].

This and [text] must be non-null before you call [layout].

### textDirection

```dart
set textDirection(TextDirection? value)
```

### textScaleFactor

```dart
double get textScaleFactor
```

Deprecated. Will be removed in a future version of Flutter. Use [textScaler] instead.

The number of font pixels for each logical pixel.

For example, if the text scale factor is 1.5, text will be 50% larger than the specified font size.

After this is set, you must call [layout] before the next call to [paint].

### textScaleFactor

```dart
set textScaleFactor(double value)
```

### textScaler

```dart
TextScaler get textScaler
```

{@template flutter.painting.textPainter.textScaler} The font scaling strategy to use when laying out and rendering the text.

The value usually comes from [MediaQuery.textScalerOf], which typically reflects the user-specified text scaling value in the platform's accessibility settings. The [TextStyle.fontSize] of the text will be adjusted by the [TextScaler] before the text is laid out and rendered. {@endtemplate}

The [layout] method must be called after [textScaler] changes as it affects the text layout.

### textScaler

```dart
set textScaler(TextScaler value)
```

### ellipsis

```dart
String? get ellipsis
```

The string used to ellipsize overflowing text. Setting this to a non-empty string will cause this string to be substituted for the remaining text if the text can not fit within the specified maximum width.

Specifically, the ellipsis is applied to the last line before the line truncated by [maxLines], if [maxLines] is non-null and that line overflows the width constraint, or to the first line that is wider than the width constraint, if [maxLines] is null. The width constraint is the `maxWidth` passed to [layout].

After this is set, you must call [layout] before the next call to [paint].

The higher layers of the system, such as the [Text] widget, represent overflow effects using the [TextOverflow] enum. The [TextOverflow.ellipsis] value corresponds to setting this property to U+2026 HORIZONTAL ELLIPSIS (…).

### ellipsis

```dart
set ellipsis(String? value)
```

### locale

```dart
Locale? get locale
```

The locale used to select region-specific glyphs.

### locale

```dart
set locale(Locale? value)
```

### maxLines

```dart
int? get maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary.

If the text exceeds the given number of lines, it is truncated such that subsequent lines are dropped.

After this is set, you must call [layout] before the next call to [paint].

### maxLines

```dart
set maxLines(int? value)
```

The value may be null. If it is not null, then it must be greater than zero.

### strutStyle

```dart
StrutStyle? get strutStyle
```

{@template flutter.painting.textPainter.strutStyle} The strut style to use. Strut style defines the strut, which sets minimum vertical layout metrics.

Omitting or providing null will disable strut.

Omitting or providing null for any properties of [StrutStyle] will result in default values being used. It is highly recommended to at least specify a [StrutStyle.fontSize].

See [StrutStyle] for details. {@endtemplate}

### strutStyle

```dart
set strutStyle(StrutStyle? value)
```

### textWidthBasis

```dart
TextWidthBasis get textWidthBasis
```

{@template flutter.painting.textPainter.textWidthBasis} Defines how to measure the width of the rendered text. {@endtemplate}

### textWidthBasis

```dart
set textWidthBasis(TextWidthBasis value)
```

### textHeightBehavior

```dart
TextHeightBehavior? get textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### textHeightBehavior

```dart
set textHeightBehavior(TextHeightBehavior? value)
```

### inlinePlaceholderBoxes

```dart
List<TextBox>? get inlinePlaceholderBoxes
```

An ordered list of [TextBox]es that bound the positions of the placeholders in the paragraph.

Each box corresponds to a [PlaceholderSpan] in the order they were defined in the [InlineSpan] tree.

### setPlaceholderDimensions()

```dart
void setPlaceholderDimensions(List<PlaceholderDimensions>? value)
```

Sets the dimensions of each placeholder in [text].

The number of [PlaceholderDimensions] provided should be the same as the number of [PlaceholderSpan]s in text. Passing in an empty or null `value` will do nothing.

If [layout] is attempted without setting the placeholder dimensions, the placeholders will be ignored in the text layout and no valid [inlinePlaceholderBoxes] will be returned.

### preferredLineHeight

```dart
double get preferredLineHeight
```

The height of a space in [text] in logical pixels.

Not every line of text in [text] will have this height, but this height is "typical" for text in [text] and useful for sizing other objects relative a typical line of text.

Obtaining this value does not require calling [layout].

The style of the [text] property is used to determine the font settings that contribute to the [preferredLineHeight]. If [text] is null or if it specifies no styles, the default [TextStyle] values are used (a 10 pixel sans-serif font).

### minIntrinsicWidth

```dart
double get minIntrinsicWidth
```

The width at which decreasing the width of the text would prevent it from painting itself completely within its bounds.

Valid only after [layout] has been called.

### maxIntrinsicWidth

```dart
double get maxIntrinsicWidth
```

The width at which increasing the width of the text no longer decreases the height.

Valid only after [layout] has been called.

### width

```dart
double get width
```

The horizontal space required to paint this text.

Valid only after [layout] has been called.

### height

```dart
double get height
```

The vertical space required to paint this text.

Valid only after [layout] has been called.

### size

```dart
Size get size
```

The amount of space required to paint this text.

Valid only after [layout] has been called.

### computeDistanceToActualBaseline()

```dart
double computeDistanceToActualBaseline(TextBaseline baseline)
```

Returns the distance from the top of the text to the first baseline of the given type.

Valid only after [layout] has been called.

### didExceedMaxLines

```dart
bool get didExceedMaxLines
```

Whether any text was truncated or ellipsized.

If [maxLines] is not null, this is true if there were more lines to be drawn than the given [maxLines], and thus at least one line was omitted in the output; otherwise it is false.

If [maxLines] is null, this is true if [ellipsis] is not the empty string and there was a line that overflowed the `maxWidth` argument passed to [layout]; otherwise it is false.

Valid only after [layout] has been called.

### layout()

```dart
void layout({double minWidth = 0.0, double maxWidth = double.infinity})
```

Computes the visual position of the glyphs for painting the text.

The text will layout with a width that's as close to its max intrinsic width (or its longest line, if [textWidthBasis] is set to [TextWidthBasis.parent]) as possible while still being greater than or equal to `minWidth` and less than or equal to `maxWidth`.

The [text] and [textDirection] properties must be non-null before this is called.

### debugPaintTextLayoutBoxes

```dart
bool debugPaintTextLayoutBoxes
```

Causes the paragraph to paint the layout boxes of the text.

{@template flutter.painting.textPainter.debugPaintTextLayoutBoxes} Each painted box illustrates how the encompassed text contributes to the overall text layout. For instance, for paragraphs whose [StrutStyle] is disabled, the line height of a line is the smallest vertical extent that covers all text boxes on that line.

Typically, only characters with a non-zero horizontal advance produce these boxes. No boxes will be painted for lines that only consist of a new line character. {@endtemplate}

The [paint] method reads this flag only in debug mode.

### paint()

```dart
void paint(Canvas canvas, Offset offset)
```

Paints the text onto the given canvas at the given offset.

Valid only after [layout] has been called.

If you cannot see the text being painted, check that your text color does not conflict with the background on which you are drawing. The default text color is white (to contrast with the default black background color), so if you are writing an application with a white background, the text will not be visible by default.

To set the text style, specify a [TextStyle] when creating the [TextSpan] that you pass to the [TextPainter] constructor or to the [text] property.

### isHighSurrogate()

```dart
bool isHighSurrogate(int value)
```

Returns true iff the given value is a valid UTF-16 high (first) surrogate. The value must be a UTF-16 code unit, meaning it must be in the range 0x0000-0xFFFF.

See also:

- https://en.wikipedia.org/wiki/UTF-16#Code_points_from_U+010000_to_U+10FFFF
- [isLowSurrogate], which checks the same thing for low (second) surrogates.

### isLowSurrogate()

```dart
bool isLowSurrogate(int value)
```

Returns true iff the given value is a valid UTF-16 low (second) surrogate. The value must be a UTF-16 code unit, meaning it must be in the range 0x0000-0xFFFF.

See also:

- https://en.wikipedia.org/wiki/UTF-16#Code_points_from_U+010000_to_U+10FFFF
- [isHighSurrogate], which checks the same thing for high (first) surrogates.

### getOffsetAfter()

```dart
int? getOffsetAfter(int offset)
```

Returns the closest offset after `offset` at which the input cursor can be positioned.

### getOffsetBefore()

```dart
int? getOffsetBefore(int offset)
```

Returns the closest offset before `offset` at which the input cursor can be positioned.

### getOffsetForCaret()

```dart
Offset getOffsetForCaret(TextPosition position, Rect caretPrototype)
```

Returns the offset at which to paint the caret.

Valid only after [layout] has been called.

### getFullHeightForCaret()

```dart
double getFullHeightForCaret(TextPosition position, Rect caretPrototype)
```

{@template flutter.painting.textPainter.getFullHeightForCaret} Returns the strut bounded height of the glyph at the given `position`. {@endtemplate}

Valid only after [layout] has been called.

### getBoxesForSelection()

```dart
List<TextBox> getBoxesForSelection(TextSelection selection, {ui.BoxHeightStyle boxHeightStyle = ui.BoxHeightStyle.tight, ui.BoxWidthStyle boxWidthStyle = ui.BoxWidthStyle.tight})
```

Returns a list of rects that bound the given selection.

The [selection] must be a valid range (with [TextSelection.isValid] true).

The [boxHeightStyle] and [boxWidthStyle] arguments may be used to select the shape of the [TextBox]s. These properties default to [ui.BoxHeightStyle.tight] and [ui.BoxWidthStyle.tight] respectively.

A given selection might have more than one rect if this text painter contains bidirectional text because logically contiguous text might not be visually contiguous.

Leading or trailing newline characters will be represented by zero-width `TextBox`es.

The method only returns `TextBox`es of glyphs that are entirely enclosed by the given `selection`: a multi-code-unit glyph will be excluded if only part of its code units are in `selection`.

### getClosestGlyphForOffset()

```dart
ui.GlyphInfo? getClosestGlyphForOffset(Offset offset)
```

Returns the [GlyphInfo] of the glyph closest to the given `offset` in the paragraph coordinate system, or null if the text is empty, or is entirely clipped or ellipsized away.

This method first finds the line closest to `offset.dy`, and then returns the [GlyphInfo] of the closest glyph(s) within that line.

### getPositionForOffset()

```dart
TextPosition getPositionForOffset(Offset offset)
```

Returns the closest position within the text for the given pixel offset.

### getWordBoundary()

```dart
TextRange getWordBoundary(TextPosition position)
```

{@template flutter.painting.TextPainter.getWordBoundary} Returns the text range of the word at the given offset. Characters not part of a word, such as spaces, symbols, and punctuation, have word breaks on both sides. In such cases, this method will return a text range that contains the given text position.

Word boundaries are defined more precisely in Unicode Standard Annex #29 <http://www.unicode.org/reports/tr29/#Word_Boundaries>. {@endtemplate}

### wordBoundaries

```dart
WordBoundary get wordBoundaries
```

{@template flutter.painting.TextPainter.wordBoundaries} Returns a [TextBoundary] that can be used to perform word boundary analysis on the current [text].

This [TextBoundary] uses word boundary rules defined in [Unicode Standard Annex #29](http://www.unicode.org/reports/tr29/#Word_Boundaries). {@endtemplate}

Currently word boundary analysis can only be performed after [layout] has been called.

### getLineBoundary()

```dart
TextRange getLineBoundary(TextPosition position)
```

Returns the text range of the line at the given offset.

The newline (if any) is not returned as part of the range.

### computeLineMetrics()

```dart
List<ui.LineMetrics> computeLineMetrics()
```

Returns the full list of [LineMetrics] that describe in detail the various metrics of each laid out line.

The [LineMetrics] list is presented in the order of the lines they represent. For example, the first line is in the zeroth index.

[LineMetrics] contains measurements such as ascent, descent, baseline, and width for the line as a whole, and may be useful for aligning additional widgets to a particular line.

Valid only after [layout] has been called.

### debugDisposed

```dart
bool get debugDisposed
```

Whether this object has been disposed or not.

Only for use when asserts are enabled.

### dispose()

```dart
void dispose()
```

Releases the resources associated with this painter.

After disposal this painter is unusable.
