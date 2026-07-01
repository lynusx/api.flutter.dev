@docImport 'package:flutter/cupertino.dart';

# TextSelectionPoint

```dart
class TextSelectionPoint {}
```

Represents the coordinates of the point in a selection, and the text direction at that point, relative to top left of the [RenderEditable] that holds the selection.

### TextSelectionPoint()

```dart
TextSelectionPoint(Offset point, TextDirection? direction)
```

Creates a description of a point in a text selection.

### point

```dart
Offset point
```

Coordinates of the lower left or lower right corner of the selection, relative to the top left of the [RenderEditable] object.

### direction

```dart
TextDirection? direction
```

Direction of the text at this edge of the selection.

### operator ==()

```dart
bool operator ==(Object other)
```

### toString()

```dart
String toString()
```

### hashCode

```dart
int get hashCode
```

# VerticalCaretMovementRun

```dart
class VerticalCaretMovementRun implements Iterator<TextPosition> {}
```

The consecutive sequence of [TextPosition]s that the caret should move to when the user navigates the paragraph using the upward arrow key or the downward arrow key.

{@template flutter.rendering.RenderEditable.verticalArrowKeyMovement} When the user presses the upward arrow key or the downward arrow key, on many platforms (macOS for instance), the caret will move to the previous line or the next line, while maintaining its original horizontal location. When it encounters a shorter line, the caret moves to the closest horizontal location within that line, and restores the original horizontal location when a long enough line is encountered.

Additionally, the caret will move to the beginning of the document if the upward arrow key is pressed and the caret is already on the first line. If the downward arrow key is pressed next, the caret will restore its original horizontal location and move to the second line. Similarly the caret moves to the end of the document if the downward arrow key is pressed when it's already on the last line.

Consider a left-aligned paragraph: aa| a aaa where the caret was initially placed at the end of the first line. Pressing the downward arrow key once will move the caret to the end of the second line, and twice the arrow key moves to the third line after the second "a" on that line. Pressing the downward arrow key again, the caret will move to the end of the third line (the end of the document). Pressing the upward arrow key in this state will result in the caret moving to the end of the second line.

Vertical caret runs are typically interrupted when the layout of the text changes (including when the text itself changes), or when the selection is changed by other input events or programmatically (for example, when the user pressed the left arrow key). {@endtemplate}

The [movePrevious] method moves the caret location (which is [VerticalCaretMovementRun.current]) to the previous line, and in case the caret is already on the first line, the method does nothing and returns false. Similarly the [moveNext] method moves the caret to the next line, and returns false if the caret is already on the last line.

The [moveByOffset] method takes a pixel offset from the current position to move the caret up or down.

If the underlying paragraph's layout changes, [isValid] becomes false and the [VerticalCaretMovementRun] must not be used. The [isValid] property must be checked before calling [movePrevious], [moveNext] and [moveByOffset], or accessing [current].

### isValid

```dart
bool get isValid
```

Whether this [VerticalCaretMovementRun] can still continue.

A [VerticalCaretMovementRun] run is valid if the underlying text layout hasn't changed.

The [current] value and the [movePrevious], [moveNext] and [moveByOffset] methods must not be accessed when [isValid] is false.

### current

```dart
TextPosition get current
```

### moveNext()

```dart
bool moveNext()
```

### movePrevious()

```dart
bool movePrevious()
```

Move back to the previous element.

Returns true and updates [current] if successful.

### moveByOffset()

```dart
bool moveByOffset(double offset)
```

Move forward or backward by a number of elements determined by pixel [offset].

If [offset] is negative, move backward; otherwise move forward.

Returns true and updates [current] if successful.

# RenderEditable

```dart
class RenderEditable extends RenderBox with RelayoutWhenSystemFontsChangeMixin, ContainerRenderObjectMixin<RenderBox, TextParentData>, RenderInlineChildrenContainerDefaults implements TextLayoutMetrics {}
```

Displays some text in a scrollable container with a potentially blinking cursor and with gesture recognizers.

This is the renderer for an editable text field. It does not directly provide affordances for editing the text, but it does handle text selection and manipulation of the text cursor.

The [text] is displayed, scrolled by the given [offset], aligned according to [textAlign]. The [maxLines] property controls whether the text displays on one line or many. The [selection], if it is not collapsed, is painted in the [selectionColor]. If it _is_ collapsed, then it represents the cursor position. The cursor is shown while [showCursor] is true. It is painted in the [cursorColor].

Keyboard handling, IME handling, scrolling, toggling the [showCursor] value to actually blink the cursor, and other features not mentioned above are the responsibility of higher layers and not handled by this object.

### RenderEditable()

```dart
RenderEditable({InlineSpan? text, required TextDirection textDirection, TextAlign textAlign = TextAlign.start, Color? cursorColor, Color? backgroundCursorColor, ValueNotifier<bool>? showCursor, bool? hasFocus, required LayerLink startHandleLayerLink, required LayerLink endHandleLayerLink, int? maxLines = 1, int? minLines, bool expands = false, StrutStyle? strutStyle, Color? selectionColor, double textScaleFactor = 1.0, TextScaler textScaler = TextScaler.noScaling, TextSelection? selection, required ViewportOffset offset, bool ignorePointer = false, bool readOnly = false, bool forceLine = true, TextHeightBehavior? textHeightBehavior, TextWidthBasis textWidthBasis = TextWidthBasis.parent, String obscuringCharacter = '•', bool obscureText = false, Locale? locale, double cursorWidth = 1.0, double? cursorHeight, Radius? cursorRadius, bool paintCursorAboveText = false, Offset cursorOffset = Offset.zero, double devicePixelRatio = 1.0, ui.BoxHeightStyle selectionHeightStyle = ui.BoxHeightStyle.max, ui.BoxWidthStyle selectionWidthStyle = ui.BoxWidthStyle.max, bool? enableInteractiveSelection, EdgeInsets floatingCursorAddedMargin = const EdgeInsets.fromLTRB(4, 4, 4, 5), TextRange? promptRectRange, Color? promptRectColor, Clip clipBehavior = Clip.hardEdge, required TextSelectionDelegate textSelectionDelegate, RenderEditablePainter? painter, RenderEditablePainter? foregroundPainter, List<RenderBox>? children})
```

Creates a render object that implements the visual aspects of a text field.

The [textAlign] argument defaults to [TextAlign.start].

If [showCursor] is not specified, then it defaults to hiding the cursor.

The [maxLines] property can be set to null to remove the restriction on the number of lines. By default, it is 1, meaning this is a single-line text field. If it is not null, it must be greater than zero.

Use [ViewportOffset.zero] for the [offset] if there is no need for scrolling.

### dispose()

```dart
void dispose()
```

### foregroundPainter

```dart
RenderEditablePainter? get foregroundPainter
```

The [RenderEditablePainter] to use for painting above this [RenderEditable]'s text content.

The new [RenderEditablePainter] will replace the previously specified foreground painter, and schedule a repaint if the new painter's `shouldRepaint` method returns true.

### foregroundPainter

```dart
set foregroundPainter(RenderEditablePainter? newPainter)
```

### painter

```dart
RenderEditablePainter? get painter
```

Sets the [RenderEditablePainter] to use for painting beneath this [RenderEditable]'s text content.

The new [RenderEditablePainter] will replace the previously specified painter, and schedule a repaint if the new painter's `shouldRepaint` method returns true.

### painter

```dart
set painter(RenderEditablePainter? newPainter)
```

### ignorePointer

```dart
bool ignorePointer
```

Whether the [handleEvent] will propagate pointer events to selection handlers.

If this property is true, the [handleEvent] assumes that this renderer will be notified of input gestures via [handleTapDown], [handleTap], [handleDoubleTap], and [handleLongPress].

If there are any gesture recognizers in the text span, the [handleEvent] will still propagate pointer events to those recognizers.

The default value of this property is false.

### textHeightBehavior

```dart
TextHeightBehavior? get textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### textHeightBehavior

```dart
set textHeightBehavior(TextHeightBehavior? value)
```

### textWidthBasis

```dart
TextWidthBasis get textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### textWidthBasis

```dart
set textWidthBasis(TextWidthBasis value)
```

### devicePixelRatio

```dart
double get devicePixelRatio
```

The pixel ratio of the current device.

Should be obtained by querying MediaQuery for the devicePixelRatio.

### devicePixelRatio

```dart
set devicePixelRatio(double value)
```

### obscuringCharacter

```dart
String get obscuringCharacter
```

Character used for obscuring text if [obscureText] is true.

Must have a length of exactly one.

### obscuringCharacter

```dart
set obscuringCharacter(String value)
```

### obscureText

```dart
bool get obscureText
```

Whether to hide the text being edited (e.g., for passwords).

### obscureText

```dart
set obscureText(bool value)
```

### selectionHeightStyle

```dart
ui.BoxHeightStyle get selectionHeightStyle
```

Controls how tall the selection highlight boxes are computed to be.

See [ui.BoxHeightStyle] for details on available styles.

### selectionHeightStyle

```dart
set selectionHeightStyle(ui.BoxHeightStyle value)
```

### selectionWidthStyle

```dart
ui.BoxWidthStyle get selectionWidthStyle
```

Controls how wide the selection highlight boxes are computed to be.

See [ui.BoxWidthStyle] for details on available styles.

### selectionWidthStyle

```dart
set selectionWidthStyle(ui.BoxWidthStyle value)
```

### textSelectionDelegate

```dart
TextSelectionDelegate textSelectionDelegate
```

The object that controls the text selection, used by this render object for implementing cut, copy, and paste keyboard shortcuts.

It will make cut, copy and paste functionality work with the most recently set [TextSelectionDelegate].

### selectionStartInViewport

```dart
ValueListenable<bool> get selectionStartInViewport
```

Track whether position of the start of the selected text is within the viewport.

For example, if the text contains "Hello World", and the user selects "Hello", then scrolls so only "World" is visible, this will become false. If the user scrolls back so that the "H" is visible again, this will become true.

This bool indicates whether the text is scrolled so that the handle is inside the text field viewport, as opposed to whether it is actually visible on the screen.

### selectionEndInViewport

```dart
ValueListenable<bool> get selectionEndInViewport
```

Track whether position of the end of the selected text is within the viewport.

For example, if the text contains "Hello World", and the user selects "World", then scrolls so only "Hello" is visible, this will become 'false'. If the user scrolls back so that the "d" is visible again, this will become 'true'.

This bool indicates whether the text is scrolled so that the handle is inside the text field viewport, as opposed to whether it is actually visible on the screen.

### getLineAtOffset()

```dart
TextSelection getLineAtOffset(TextPosition position)
```

{@macro flutter.services.TextLayoutMetrics.getLineAtOffset}

### getWordBoundary()

```dart
TextRange getWordBoundary(TextPosition position)
```

{@macro flutter.painting.TextPainter.getWordBoundary}

### getTextPositionAbove()

```dart
TextPosition getTextPositionAbove(TextPosition position)
```

{@macro flutter.services.TextLayoutMetrics.getTextPositionAbove}

### getTextPositionBelow()

```dart
TextPosition getTextPositionBelow(TextPosition position)
```

{@macro flutter.services.TextLayoutMetrics.getTextPositionBelow}

### markNeedsPaint()

```dart
void markNeedsPaint()
```

### systemFontsDidChange()

```dart
void systemFontsDidChange()
```

### plainText

```dart
String get plainText
```

Returns a plain text version of the text in [TextPainter].

If [obscureText] is true, returns the obscured text. See [obscureText] and [obscuringCharacter]. In order to get the styled text as an [InlineSpan] tree, use [text].

### text

```dart
InlineSpan? get text
```

The text to paint in the form of a tree of [InlineSpan]s.

In order to get the plain text representation, use [plainText].

### text

```dart
set text(InlineSpan? value)
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

### locale

```dart
Locale? get locale
```

Used by this renderer's internal [TextPainter] to select a locale-specific font.

In some cases the same Unicode character may be rendered differently depending on the locale. For example the '骨' character is rendered differently in the Chinese and Japanese locales. In these cases the [locale] may be used to select a locale-specific font.

If this value is null, a system-dependent algorithm is used to select the font.

### locale

```dart
set locale(Locale? value)
```

### strutStyle

```dart
StrutStyle? get strutStyle
```

The [StrutStyle] used by the renderer's internal [TextPainter] to determine the strut to use.

### strutStyle

```dart
set strutStyle(StrutStyle? value)
```

### cursorColor

```dart
Color? get cursorColor
```

The color to use when painting the cursor.

### cursorColor

```dart
set cursorColor(Color? value)
```

### backgroundCursorColor

```dart
Color? get backgroundCursorColor
```

The color to use when painting the cursor aligned to the text while rendering the floating cursor.

Typically this would be set to [CupertinoColors.inactiveGray].

If this is null, the background cursor is not painted.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### backgroundCursorColor

```dart
set backgroundCursorColor(Color? value)
```

### showCursor

```dart
ValueNotifier<bool> get showCursor
```

Whether to paint the cursor.

### showCursor

```dart
set showCursor(ValueNotifier<bool> value)
```

### hasFocus

```dart
bool get hasFocus
```

Whether the editable is currently focused.

### hasFocus

```dart
set hasFocus(bool value)
```

### forceLine

```dart
bool get forceLine
```

Whether this rendering object will take a full line regardless the text width.

### forceLine

```dart
set forceLine(bool value)
```

### readOnly

```dart
bool get readOnly
```

Whether this rendering object is read only.

### readOnly

```dart
set readOnly(bool value)
```

### maxLines

```dart
int? get maxLines
```

The maximum number of lines for the text to span, wrapping if necessary.

If this is 1 (the default), the text will not wrap, but will extend indefinitely instead.

If this is null, there is no limit to the number of lines.

When this is not null, the intrinsic height of the render object is the height of one line of text multiplied by this value. In other words, this also controls the height of the actual editing widget.

### maxLines

```dart
set maxLines(int? value)
```

The value may be null. If it is not null, then it must be greater than zero.

### minLines

```dart
int? get minLines
```

{@macro flutter.widgets.editableText.minLines}

### minLines

```dart
set minLines(int? value)
```

The value may be null. If it is not null, then it must be greater than zero.

### expands

```dart
bool get expands
```

{@macro flutter.widgets.editableText.expands}

### expands

```dart
set expands(bool value)
```

### selectionColor

```dart
Color? get selectionColor
```

The color to use when painting the selection.

### selectionColor

```dart
set selectionColor(Color? value)
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

### selection

```dart
TextSelection? get selection
```

The region of text that is selected, if any.

The caret position is represented by a collapsed selection.

If [selection] is null, there is no selection and attempts to manipulate the selection will throw.

### selection

```dart
set selection(TextSelection? value)
```

### offset

```dart
ViewportOffset get offset
```

The offset at which the text should be painted.

If the text content is larger than the editable line itself, the editable line clips the text. This property controls which part of the text is visible by shifting the text by the given offset before clipping.

### offset

```dart
set offset(ViewportOffset value)
```

### cursorWidth

```dart
double get cursorWidth
```

How thick the cursor will be.

### cursorWidth

```dart
set cursorWidth(double value)
```

### cursorHeight

```dart
double get cursorHeight
```

How tall the cursor will be.

This can be null, in which case the getter will actually return [preferredLineHeight].

Setting this to itself fixes the value to the current [preferredLineHeight]. Setting this to null returns the behavior of deferring to [preferredLineHeight].

### cursorHeight

```dart
set cursorHeight(double? value)
```

### paintCursorAboveText

```dart
bool get paintCursorAboveText
```

{@template flutter.rendering.RenderEditable.paintCursorAboveText} If the cursor should be painted on top of the text or underneath it.

By default, the cursor should be painted on top for iOS platforms and underneath for Android platforms. {@endtemplate}

### paintCursorAboveText

```dart
set paintCursorAboveText(bool value)
```

### cursorOffset

```dart
Offset get cursorOffset
```

{@template flutter.rendering.RenderEditable.cursorOffset} The offset that is used, in pixels, when painting the cursor on screen.

By default, the cursor position should be set to an offset of (-[cursorWidth] \* 0.5, 0.0) on iOS platforms and (0, 0) on Android platforms. The origin from where the offset is applied to is the arbitrary location where the cursor ends up being rendered from by default. {@endtemplate}

### cursorOffset

```dart
set cursorOffset(Offset value)
```

### cursorRadius

```dart
Radius? get cursorRadius
```

How rounded the corners of the cursor should be.

A null value is the same as [Radius.zero].

### cursorRadius

```dart
set cursorRadius(Radius? value)
```

### startHandleLayerLink

```dart
LayerLink get startHandleLayerLink
```

The [LayerLink] of start selection handle.

[RenderEditable] is responsible for calculating the [Offset] of this [LayerLink], which will be used as [CompositedTransformTarget] of start handle.

### startHandleLayerLink

```dart
set startHandleLayerLink(LayerLink value)
```

### endHandleLayerLink

```dart
LayerLink get endHandleLayerLink
```

The [LayerLink] of end selection handle.

[RenderEditable] is responsible for calculating the [Offset] of this [LayerLink], which will be used as [CompositedTransformTarget] of end handle.

### endHandleLayerLink

```dart
set endHandleLayerLink(LayerLink value)
```

### floatingCursorAddedMargin

```dart
EdgeInsets floatingCursorAddedMargin
```

The padding applied to text field. Used to determine the bounds when moving the floating cursor.

Defaults to a padding with left, top and right set to 4, bottom to 5.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### floatingCursorOn

```dart
bool get floatingCursorOn
```

Returns true if the floating cursor is visible, false otherwise.

### enableInteractiveSelection

```dart
bool? get enableInteractiveSelection
```

Whether to allow the user to change the selection.

Since [RenderEditable] does not handle selection manipulation itself, this actually only affects whether the accessibility hints provided to the system (via [describeSemanticsConfiguration]) will enable selection manipulation. It's the responsibility of this object's owner to provide selection manipulation affordances.

This field is used by [selectionEnabled] (which then controls the accessibility hints mentioned above). When null, [obscureText] is used to determine the value of [selectionEnabled] instead.

### enableInteractiveSelection

```dart
set enableInteractiveSelection(bool? value)
```

### selectionEnabled

```dart
bool get selectionEnabled
```

Whether interactive selection are enabled based on the values of [enableInteractiveSelection] and [obscureText].

Since [RenderEditable] does not handle selection manipulation itself, this actually only affects whether the accessibility hints provided to the system (via [describeSemanticsConfiguration]) will enable selection manipulation. It's the responsibility of this object's owner to provide selection manipulation affordances.

By default, [enableInteractiveSelection] is null, [obscureText] is false, and this getter returns true.

If [enableInteractiveSelection] is null and [obscureText] is true, then this getter returns false. This is the common case for password fields.

If [enableInteractiveSelection] is non-null then its value is returned. An application might [enableInteractiveSelection] to true to enable interactive selection for a password field, or to false to unconditionally disable interactive selection.

### promptRectColor

```dart
Color? get promptRectColor
```

The color used to paint the prompt rectangle.

The prompt rectangle will only be requested on non-web iOS applications.

### promptRectColor

```dart
set promptRectColor(Color? newValue)
```

### setPromptRectRange()

```dart
void setPromptRectRange(TextRange? newRange)
```

Dismisses the currently displayed prompt rectangle and displays a new prompt rectangle over [newRange] in the given color [promptRectColor].

The prompt rectangle will only be requested on non-web iOS applications.

When set to null, the currently displayed prompt rectangle (if any) will be dismissed.

### maxScrollExtent

```dart
double get maxScrollExtent
```

The maximum amount the text is allowed to scroll.

This value is only valid after layout and can change as additional text is entered or removed in order to accommodate expanding when [expands] is set to true.

### clipBehavior

```dart
Clip get clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### clipBehavior

```dart
set clipBehavior(Clip value)
```

### getBoxesForSelection()

```dart
List<TextBox> getBoxesForSelection(TextSelection selection)
```

Returns a list of rects that bound the given selection, and the text direction. The text direction is used by the engine to calculate the closest position to a given point.

See [TextPainter.getBoxesForSelection] for more details.

### describeSemanticsConfiguration()

```dart
void describeSemanticsConfiguration(SemanticsConfiguration config)
```

### assembleSemanticsNode()

```dart
void assembleSemanticsNode(SemanticsNode node, SemanticsConfiguration config, Iterable<SemanticsNode> children)
```

### attach()

```dart
void attach(PipelineOwner owner)
```

### detach()

```dart
void detach()
```

### redepthChildren()

```dart
void redepthChildren()
```

### visitChildren()

```dart
void visitChildren(RenderObjectVisitor visitor)
```

### getEndpointsForSelection()

```dart
List<TextSelectionPoint> getEndpointsForSelection(TextSelection selection)
```

Returns the local coordinates of the endpoints of the given selection.

If the selection is collapsed (and therefore occupies a single point), the returned list is of length one. Otherwise, the selection is not collapsed and the returned list is of length two. In this case, however, the two points might actually be co-located (e.g., because of a bidirectional selection that contains some text but whose ends meet in the middle).

See also:

- [getLocalRectForCaret], which is the equivalent but for a [TextPosition] rather than a [TextSelection].

### getRectForComposingRange()

```dart
Rect? getRectForComposingRange(TextRange range)
```

Returns the smallest [Rect], in the local coordinate system, that covers the text within the [TextRange] specified.

This method is used to calculate the approximate position of the IME bar on iOS.

Returns null if [TextRange.isValid] is false for the given `range`, or the given `range` is collapsed.

### getPositionForPoint()

```dart
TextPosition getPositionForPoint(Offset globalPosition)
```

Returns the position in the text for the given global coordinate.

See also:

- [getLocalRectForCaret], which is the reverse operation, taking a [TextPosition] and returning a [Rect].
- [TextPainter.getPositionForOffset], which is the equivalent method for a [TextPainter] object.

### getLocalRectForCaret()

```dart
Rect getLocalRectForCaret(TextPosition caretPosition)
```

Returns the [Rect] in local coordinates for the caret at the given text position.

See also:

- [getPositionForPoint], which is the reverse operation, taking an [Offset] in global coordinates and returning a [TextPosition].
- [getEndpointsForSelection], which is the equivalent but for a selection rather than a particular text position.
- [TextPainter.getOffsetForCaret], the equivalent method for a [TextPainter] object.

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

An estimate of the height of a line in the text. See [TextPainter.preferredLineHeight]. This does not require the layout to be updated.

### computeMinIntrinsicHeight()

```dart
double computeMinIntrinsicHeight(double width)
```

### computeMaxIntrinsicHeight()

```dart
double computeMaxIntrinsicHeight(double width)
```

### computeDistanceToActualBaseline()

```dart
double computeDistanceToActualBaseline(TextBaseline baseline)
```

### hitTestSelf()

```dart
bool hitTestSelf(Offset position)
```

### hitTestChildren()

```dart
bool hitTestChildren(BoxHitTestResult result, {required Offset position})
```

### handleEvent()

```dart
void handleEvent(PointerEvent event, BoxHitTestEntry entry)
```

### lastSecondaryTapDownPosition

```dart
Offset? get lastSecondaryTapDownPosition
```

{@template flutter.rendering.RenderEditable.lastSecondaryTapDownPosition} The position of the most recent secondary tap down event on this text input. {@endtemplate}

### handleSecondaryTapDown()

```dart
void handleSecondaryTapDown(TapDownDetails details)
```

Tracks the position of a secondary tap event.

Should be called before attempting to change the selection based on the position of a secondary tap.

### handleTapDown()

```dart
void handleTapDown(TapDownDetails details)
```

If [ignorePointer] is false (the default) then this method is called by the internal gesture recognizer's [TapGestureRecognizer.onTapDown] callback.

When [ignorePointer] is true, an ancestor widget must respond to tap down events by calling this method.

### handleTap()

```dart
void handleTap()
```

If [ignorePointer] is false (the default) then this method is called by the internal gesture recognizer's [TapGestureRecognizer.onTap] callback.

When [ignorePointer] is true, an ancestor widget must respond to tap events by calling this method.

### handleDoubleTap()

```dart
void handleDoubleTap()
```

If [ignorePointer] is false (the default) then this method is called by the internal gesture recognizer's [DoubleTapGestureRecognizer.onDoubleTap] callback.

When [ignorePointer] is true, an ancestor widget must respond to double tap events by calling this method.

### handleLongPress()

```dart
void handleLongPress()
```

If [ignorePointer] is false (the default) then this method is called by the internal gesture recognizer's [LongPressGestureRecognizer.onLongPress] callback.

When [ignorePointer] is true, an ancestor widget must respond to long press events by calling this method.

### selectPosition()

```dart
void selectPosition({required SelectionChangedCause cause})
```

Move selection to the location of the last tap down.

{@template flutter.rendering.RenderEditable.selectPosition} This method is mainly used to translate user inputs in global positions into a [TextSelection]. When used in conjunction with a [EditableText], the selection change is fed back into [TextEditingController.selection].

If you have a [TextEditingController], it's generally easier to programmatically manipulate its `value` or `selection` directly. {@endtemplate}

### selectPositionAt()

```dart
void selectPositionAt({required Offset from, Offset? to, required SelectionChangedCause cause})
```

Select text between the global positions [from] and [to].

[from] corresponds to the [TextSelection.baseOffset], and [to] corresponds to the [TextSelection.extentOffset].

### wordBoundaries

```dart
WordBoundary get wordBoundaries
```

{@macro flutter.painting.TextPainter.wordBoundaries}

### selectWord()

```dart
void selectWord({required SelectionChangedCause cause})
```

Select a word around the location of the last tap down.

{@macro flutter.rendering.RenderEditable.selectPosition}

### selectWordsInRange()

```dart
void selectWordsInRange({required Offset from, Offset? to, required SelectionChangedCause cause})
```

Selects the set words of a paragraph that intersect a given range of global positions.

The set of words selected are not strictly bounded by the range of global positions.

The first and last endpoints of the selection will always be at the beginning and end of a word respectively.

{@macro flutter.rendering.RenderEditable.selectPosition}

### selectWordEdge()

```dart
void selectWordEdge({required SelectionChangedCause cause})
```

Move the selection to the beginning or end of a word.

{@macro flutter.rendering.RenderEditable.selectPosition}

### getWordAtOffset()

```dart
TextSelection getWordAtOffset(TextPosition position)
```

Returns a [TextSelection] that encompasses the word at the given [TextPosition].

### computeDryLayout()

```dart
Size computeDryLayout(BoxConstraints constraints)
```

### computeDryBaseline()

```dart
double computeDryBaseline(BoxConstraints constraints, TextBaseline baseline)
```

### performLayout()

```dart
void performLayout()
```

### calculateBoundedFloatingCursorOffset()

```dart
Offset calculateBoundedFloatingCursorOffset(Offset rawCursorOffset, {bool? shouldResetOrigin})
```

Returns the position within the text field closest to the raw cursor offset.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### setFloatingCursor()

```dart
void setFloatingCursor(FloatingCursorDragState state, Offset boundedOffset, TextPosition lastTextPosition, {double? resetLerpValue})
```

Sets the screen position of the floating cursor and the text position closest to the cursor.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### startVerticalCaretMovement()

```dart
VerticalCaretMovementRun startVerticalCaretMovement(TextPosition startPosition)
```

Starts a [VerticalCaretMovementRun] at the given location in the text, for handling consecutive vertical caret movements.

This can be used to handle consecutive upward/downward arrow key movements in an input field.

{@macro flutter.rendering.RenderEditable.verticalArrowKeyMovement}

The [VerticalCaretMovementRun.isValid] property indicates whether the text layout has changed and the vertical caret run is invalidated.

The caller should typically discard a [VerticalCaretMovementRun] when its [VerticalCaretMovementRun.isValid] becomes false, or on other occasions where the vertical caret run should be interrupted.

### applyPaintTransform()

```dart
void applyPaintTransform(RenderBox child, Matrix4 transform)
```

### paint()

```dart
void paint(PaintingContext context, Offset offset)
```

### describeApproximatePaintClip()

```dart
Rect? describeApproximatePaintClip(RenderObject child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugDescribeChildren()

```dart
List<DiagnosticsNode> debugDescribeChildren()
```

# RenderEditablePainter

```dart
abstract class RenderEditablePainter extends ChangeNotifier {}
```

An interface that paints within a [RenderEditable]'s bounds, above or beneath its text content.

This painter is typically used for painting auxiliary content that depends on text layout metrics (for instance, for painting carets and text highlight blocks). It can paint independently from its [RenderEditable], allowing it to repaint without triggering a repaint on the entire [RenderEditable] stack when only auxiliary content changes (e.g. a blinking cursor) are present. It will be scheduled to repaint when:

- It's assigned to a new [RenderEditable] (replacing a prior [RenderEditablePainter]) and the [shouldRepaint] method returns true.
- Any of the [RenderEditable]s it is attached to repaints.
- The [notifyListeners] method is called, which typically happens when the painter's attributes change.

See also:

- [RenderEditable.foregroundPainter], which takes a [RenderEditablePainter] and sets it as the foreground painter of the [RenderEditable].
- [RenderEditable.painter], which takes a [RenderEditablePainter] and sets it as the background painter of the [RenderEditable].
- [CustomPainter], a similar class which paints within a [RenderCustomPaint].

### shouldRepaint()

```dart
bool shouldRepaint(RenderEditablePainter? oldDelegate)
```

Determines whether repaint is needed when a new [RenderEditablePainter] is provided to a [RenderEditable].

If the new instance represents different information than the old instance, then the method should return true, otherwise it should return false. When [oldDelegate] is null, this method should always return true unless the new painter initially does not paint anything.

If the method returns false, then the [paint] call might be optimized away. However, the [paint] method will get called whenever the [RenderEditable]s it attaches to repaint, even if [shouldRepaint] returns false.

### paint()

```dart
void paint(Canvas canvas, Size size, RenderEditable renderEditable)
```

Paints within the bounds of a [RenderEditable].

The given [Canvas] has the same coordinate space as the [RenderEditable], which may be different from the coordinate space the [RenderEditable]'s [TextPainter] uses, when the text moves inside the [RenderEditable].

Paint operations performed outside of the region defined by the [canvas]'s origin and the [size] parameter may get clipped, when [RenderEditable]'s [RenderEditable.clipBehavior] is not [Clip.none].
