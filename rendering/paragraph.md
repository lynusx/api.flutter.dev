@docImport 'package:flutter/widgets.dart';

@docImport 'editable.dart';

# PlaceholderSpanIndexSemanticsTag

```dart
class PlaceholderSpanIndexSemanticsTag extends SemanticsTag {}
```

Used by the [RenderParagraph] to map its rendering children to their corresponding semantics nodes.

The [RichText] uses this to tag the relation between its placeholder spans and their semantics nodes.

### PlaceholderSpanIndexSemanticsTag()

```dart
PlaceholderSpanIndexSemanticsTag(int index)
```

Creates a semantics tag with the input `index`.

Different [PlaceholderSpanIndexSemanticsTag]s with the same `index` are consider the same.

### index

```dart
int index
```

The index of this tag.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# TextParentData

```dart
class TextParentData extends ParentData with ContainerParentDataMixin<RenderBox> {}
```

Parent data used by [RenderParagraph] and [RenderEditable] to annotate inline contents (such as [WidgetSpan]s) with.

### offset

```dart
Offset? get offset
```

The offset at which to paint the child in the parent's coordinate system.

A `null` value indicates this inline widget is not laid out. For instance, when the inline widget has never been laid out, or the inline widget is ellipsized away.

### span

```dart
PlaceholderSpan? span
```

The [PlaceholderSpan] associated with this render child.

This field is usually set by a [ParentDataWidget], and is typically not null when `performLayout` is called.

### detach()

```dart
void detach()
```

### toString()

```dart
String toString()
```

# RenderInlineChildrenContainerDefaults

```dart
mixin RenderInlineChildrenContainerDefaults on RenderBox, ContainerRenderObjectMixin<RenderBox, TextParentData> {}
```

A mixin that provides useful default behaviors for text [RenderBox]es ([RenderParagraph] and [RenderEditable] for example) with inline content children managed by the [ContainerRenderObjectMixin] mixin.

This mixin assumes every child managed by the [ContainerRenderObjectMixin] mixin corresponds to a [PlaceholderSpan], and they are organized in logical order of the text (the order each [PlaceholderSpan] is encountered when the user reads the text).

To use this mixin in a [RenderBox] class:

- Call [layoutInlineChildren] in the `performLayout` and `computeDryLayout` implementation, and during intrinsic size calculations, to get the size information of the inline widgets as a `List` of `PlaceholderDimensions`. Determine the positioning of the inline widgets (which is usually done by a [TextPainter] using its line break algorithm).

- Call [positionInlineChildren] with the positioning information of the inline widgets.

- Implement [RenderBox.applyPaintTransform], optionally with [defaultApplyPaintTransform].

- Call [paintInlineChildren] in [RenderBox.paint] to paint the inline widgets.

- Call [hitTestInlineChildren] in [RenderBox.hitTestChildren] to hit test the inline widgets.

See also:

- [WidgetSpan.extractFromInlineSpan], a helper function for extracting [WidgetSpan]s from an [InlineSpan] tree.

### setupParentData()

```dart
void setupParentData(RenderBox child)
```

### layoutInlineChildren()

```dart
List<PlaceholderDimensions> layoutInlineChildren(double maxWidth, ChildLayouter layoutChild, ChildBaselineGetter getChildBaseline)
```

Computes the layout for every inline child using the `maxWidth` constraint.

Returns a list of [PlaceholderDimensions], representing the layout results for each child managed by the [ContainerRenderObjectMixin] mixin.

The `getChildBaseline` parameter and the `layoutChild` parameter must be consistent: if `layoutChild` computes the size of the child without modifying the actual layout of that child, then `getChildBaseline` must also be "dry", and vice versa.

Since this method does not impose a maximum height constraint on the inline children, some children may become taller than this [RenderBox].

See also:

- [TextPainter.setPlaceholderDimensions], the method that usually takes the layout results from this method as the input.

### positionInlineChildren()

```dart
void positionInlineChildren(List<ui.TextBox> boxes)
```

Positions each inline child according to the coordinates provided in the `boxes` list.

The `boxes` list must be in logical order, which is the order each child is encountered when the user reads the text. Usually the length of the list equals [childCount], but it can be less than that, when some children are omitted due to ellipsing. It never exceeds [childCount].

See also:

- [TextPainter.inlinePlaceholderBoxes], the method that can be used to get the input `boxes`.

### defaultApplyPaintTransform()

```dart
void defaultApplyPaintTransform(RenderBox child, Matrix4 transform)
```

Applies the transform that would be applied when painting the given child to the given matrix.

Render children whose [TextParentData.offset] is null zeros out the `transform` to indicate they're invisible thus should not be painted.

### paintInlineChildren()

```dart
void paintInlineChildren(PaintingContext context, Offset offset)
```

Paints each inline child.

Render children whose [TextParentData.offset] is null will be skipped by this method.

### hitTestInlineChildren()

```dart
bool hitTestInlineChildren(BoxHitTestResult result, Offset position)
```

Performs a hit test on each inline child.

Render children whose [TextParentData.offset] is null will be skipped by this method.

# RenderParagraph

```dart
class RenderParagraph extends RenderBox with ContainerRenderObjectMixin<RenderBox, TextParentData>, RenderInlineChildrenContainerDefaults, RelayoutWhenSystemFontsChangeMixin {}
```

A render object that displays a paragraph of text.

### RenderParagraph()

```dart
RenderParagraph(InlineSpan text, {TextAlign textAlign = TextAlign.start, required TextDirection textDirection, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, double textScaleFactor = 1.0, TextScaler textScaler = const _UnspecifiedTextScaler(), int? maxLines, Locale? locale, StrutStyle? strutStyle, TextWidthBasis textWidthBasis = TextWidthBasis.parent, ui.TextHeightBehavior? textHeightBehavior, List<RenderBox>? children, Color? selectionColor, SelectionRegistrar? registrar, double devicePixelRatio = 1.0})
```

Creates a paragraph render object.

The [maxLines] property may be null (and indeed defaults to null), but if it is not null, it must be greater than zero.

### text

```dart
InlineSpan get text
```

The text to display.

### text

```dart
set text(InlineSpan value)
```

### selections

```dart
List<TextSelection> get selections
```

The ongoing selections in this paragraph.

The selection does not include selections in [PlaceholderSpan] if there are any.

### registrar

```dart
SelectionRegistrar? get registrar
```

The [SelectionRegistrar] this paragraph will be, or is, registered to.

### registrar

```dart
set registrar(SelectionRegistrar? value)
```

### selectableBelongsToParagraph()

```dart
bool selectableBelongsToParagraph(Selectable selectable)
```

Determines whether the given [Selectable] was created by this [RenderParagraph].

The [RenderParagraph] splits its text into multiple [Selectable]s, delimited by [PlaceholderSpan]s or [WidgetSpan]s.

### alwaysNeedsCompositing

```dart
bool get alwaysNeedsCompositing
```

### markNeedsLayout()

```dart
void markNeedsLayout()
```

### dispose()

```dart
void dispose()
```

### textAlign

```dart
TextAlign get textAlign
```

How the text should be aligned horizontally.

### textAlign

```dart
set textAlign(TextAlign value)
```

### textDirection

```dart
TextDirection get textDirection
```

The directionality of the text.

This decides how the [TextAlign.start], [TextAlign.end], and [TextAlign.justify] values of [textAlign] are interpreted.

This is also used to disambiguate how to render bidirectional text. For example, if the [text] is an English phrase followed by a Hebrew phrase, in a [TextDirection.ltr] context the English phrase will be on the left and the Hebrew phrase to its right, while in a [TextDirection.rtl] context, the English phrase will be on the right and the Hebrew phrase on its left.

### textDirection

```dart
set textDirection(TextDirection value)
```

### softWrap

```dart
bool get softWrap
```

Whether the text should break at soft line breaks.

If false, the glyphs in the text will be positioned as if there was unlimited horizontal space.

If [softWrap] is false, [overflow] and [textAlign] may have unexpected effects.

### softWrap

```dart
set softWrap(bool value)
```

### overflow

```dart
TextOverflow get overflow
```

How visual overflow should be handled.

### overflow

```dart
set overflow(TextOverflow value)
```

### textScaleFactor

```dart
double get textScaleFactor
```

Deprecated. Will be removed in a future version of Flutter. Use [textScaler] instead.

The number of font pixels for each logical pixel.

For example, if the text scale factor is 1.5, text will be 50% larger than the specified font size.

### textScaleFactor

```dart
set textScaleFactor(double value)
```

### textScaler

```dart
TextScaler get textScaler
```

{@macro flutter.painting.textPainter.textScaler}

### textScaler

```dart
set textScaler(TextScaler value)
```

### devicePixelRatio

```dart
double get devicePixelRatio
```

The number of device pixels for each logical pixel.

This is used by some renderers (like WebParagraph on the web) to regenerate the text bitmap when the scale changes.

### devicePixelRatio

```dart
set devicePixelRatio(double value)
```

### maxLines

```dart
int? get maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary. If the text exceeds the given number of lines, it will be truncated according to [overflow] and [softWrap].

### maxLines

```dart
set maxLines(int? value)
```

The value may be null. If it is not null, then it must be greater than zero.

### locale

```dart
Locale? get locale
```

Used by this paragraph's internal [TextPainter] to select a locale-specific font.

In some cases, the same Unicode character may be rendered differently depending on the locale. For example, the '骨' character is rendered differently in the Chinese and Japanese locales. In these cases, the [locale] may be used to select a locale-specific font.

### locale

```dart
set locale(Locale? value)
```

The value may be null.

### strutStyle

```dart
StrutStyle? get strutStyle
```

{@macro flutter.painting.textPainter.strutStyle}

### strutStyle

```dart
set strutStyle(StrutStyle? value)
```

The value may be null.

### textWidthBasis

```dart
TextWidthBasis get textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### textWidthBasis

```dart
set textWidthBasis(TextWidthBasis value)
```

### textHeightBehavior

```dart
ui.TextHeightBehavior? get textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### textHeightBehavior

```dart
set textHeightBehavior(ui.TextHeightBehavior? value)
```

### selectionColor

```dart
Color? get selectionColor
```

The color to use when painting the selection.

Ignored if the text is not selectable (e.g. if [registrar] is null).

### selectionColor

```dart
set selectionColor(Color? value)
```

### computeMinIntrinsicWidth()

```dart
double computeMinIntrinsicWidth(double height)
```

### computeMaxIntrinsicWidth()

```dart
double computeMaxIntrinsicWidth(double height)
```

### preferredLineHeight

```dart
double get preferredLineHeight
```

An estimate of the height of a line in the text. See [TextPainter.preferredLineHeight].

This does not require the layout to be updated.

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### debugHasOverflowShader

```dart
bool get debugHasOverflowShader
```

Whether this paragraph currently has a [dart:ui.Shader] for its overflow effect.

Used to test this object. Not for use in production.

### systemFontsDidChange()

```dart
void systemFontsDidChange()
```

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDistanceToActualBaseline()

```dart
double computeDistanceToActualBaseline(TextBaseline baseline)
```

### computeDryBaseline()

```dart
double computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### getOffsetForCaret()

```dart
Offset getOffsetForCaret(TextPosition position, Rect caretPrototype)
```

Returns the offset at which to paint the caret.

Valid only after [layout].

### getFullHeightForCaret()

```dart
double getFullHeightForCaret(TextPosition position)
```

{@macro flutter.painting.textPainter.getFullHeightForCaret}

Valid only after [layout].

### getBoxesForSelection()

```dart
List<ui.TextBox> getBoxesForSelection(TextSelection selection, {ui.BoxHeightStyle boxHeightStyle = ui.BoxHeightStyle.tight, ui.BoxWidthStyle boxWidthStyle = ui.BoxWidthStyle.tight})
```

Returns a list of rects that bound the given selection.

The [boxHeightStyle] and [boxWidthStyle] arguments may be used to select the shape of the [TextBox]es. These properties default to [ui.BoxHeightStyle.tight] and [ui.BoxWidthStyle.tight] respectively.

A given selection might have more than one rect if the [RenderParagraph] contains multiple [InlineSpan]s or bidirectional text, because logically contiguous text might not be visually contiguous.

Valid only after [layout].

See also:

- [TextPainter.getBoxesForSelection], the method in TextPainter to get the equivalent boxes.

### getPositionForOffset()

```dart
TextPosition getPositionForOffset(Offset offset)
```

Returns the position within the text for the given pixel offset.

Valid only after [layout].

### getWordBoundary()

```dart
TextRange getWordBoundary(TextPosition position)
```

Returns the text range of the word at the given offset. Characters not part of a word, such as spaces, symbols, and punctuation, have word breaks on both sides. In such cases, this method will return a text range that contains the given text position.

Word boundaries are defined more precisely in Unicode Standard Annex #29 <http://www.unicode.org/reports/tr29/#Word_Boundaries>.

Valid only after [layout].

### textSize

```dart
Size get textSize
```

Returns the size of the text as laid out.

This can differ from [size] if the text overflowed or if the [constraints] provided by the parent [RenderObject] forced the layout to be bigger than necessary for the given [text].

This returns the [TextPainter.size] of the underlying [TextPainter].

Valid only after [layout].

### didExceedMaxLines

```dart
bool get didExceedMaxLines
```

Whether the text was truncated or ellipsized as laid out.

This returns the [TextPainter.didExceedMaxLines] of the underlying [TextPainter].

Valid only after [layout].

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### assembleSemanticsNode()

```dart
void assembleSemanticsNode(SemanticsNode node, SemanticsConfiguration config, Iterable<SemanticsNode> children)
```

### clearSemantics()

```dart
void clearSemantics()
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
