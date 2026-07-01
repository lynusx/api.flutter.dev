@docImport 'default_text_editing_shortcuts.dart'; @docImport 'editable_text.dart';

# DoNothingAndStopPropagationTextIntent

```dart
class DoNothingAndStopPropagationTextIntent extends Intent {}
```

An [Intent] to send the event straight to the engine.

See also:

- [DefaultTextEditingShortcuts], which triggers this [Intent].

### DoNothingAndStopPropagationTextIntent()

```dart
DoNothingAndStopPropagationTextIntent()
```

Creates an instance of [DoNothingAndStopPropagationTextIntent].

# DirectionalTextEditingIntent

```dart
abstract class DirectionalTextEditingIntent extends Intent {}
```

A text editing related [Intent] that performs an operation towards a given direction of the current caret location.

### DirectionalTextEditingIntent()

```dart
DirectionalTextEditingIntent(bool forward)
```

Creates a [DirectionalTextEditingIntent].

### forward

```dart
bool forward
```

Whether the input field, if applicable, should perform the text editing operation from the current caret location towards the end of the document.

Unless otherwise specified by the recipient of this intent, this parameter uses the logical order of characters in the string to determine the direction, and is not affected by the writing direction of the text.

# DeleteCharacterIntent

```dart
class DeleteCharacterIntent extends DirectionalTextEditingIntent {}
```

Deletes the character before or after the caret location, based on whether `forward` is true.

{@template flutter.widgets.TextEditingIntents.logicalOrder} {@endtemplate}

Typically a text field will not respond to this intent if it has no active caret ([TextSelection.isValid] is false for the current selection).

### DeleteCharacterIntent()

```dart
DeleteCharacterIntent({required bool forward})
```

Creates a [DeleteCharacterIntent].

# DeleteToNextWordBoundaryIntent

```dart
class DeleteToNextWordBoundaryIntent extends DirectionalTextEditingIntent {}
```

Deletes from the current caret location to the previous or next word boundary, based on whether `forward` is true.

### DeleteToNextWordBoundaryIntent()

```dart
DeleteToNextWordBoundaryIntent({required bool forward})
```

Creates a [DeleteToNextWordBoundaryIntent].

# DeleteToLineBreakIntent

```dart
class DeleteToLineBreakIntent extends DirectionalTextEditingIntent {}
```

Deletes from the current caret location to the previous or next soft or hard line break, based on whether `forward` is true.

### DeleteToLineBreakIntent()

```dart
DeleteToLineBreakIntent({required bool forward})
```

Creates a [DeleteToLineBreakIntent].

# DirectionalCaretMovementIntent

```dart
abstract class DirectionalCaretMovementIntent extends DirectionalTextEditingIntent {}
```

A [DirectionalTextEditingIntent] that moves the caret or the selection to a new location.

### DirectionalCaretMovementIntent()

```dart
DirectionalCaretMovementIntent(bool forward, bool collapseSelection, [bool collapseAtReversal = false, bool continuesAtWrap = false])
```

Creates a [DirectionalCaretMovementIntent].

### collapseSelection

```dart
bool collapseSelection
```

Whether this [Intent] should make the selection collapsed (so it becomes a caret), after the movement.

When [collapseSelection] is false, the input field typically only moves the current [TextSelection.extent] to the new location, while maintains the current [TextSelection.base] location.

When [collapseSelection] is true, the input field typically should move both the [TextSelection.base] and the [TextSelection.extent] to the new location.

### collapseAtReversal

```dart
bool collapseAtReversal
```

Whether to collapse the selection when it would otherwise reverse order.

For example, consider when forward is true and the extent is before the base. If collapseAtReversal is true, then this will cause the selection to collapse at the base. If it's false, then the extent will be placed at the linebreak, reversing the order of base and offset.

Cannot be true when collapseSelection is true.

### continuesAtWrap

```dart
bool continuesAtWrap
```

Whether or not to continue to the next line at a wordwrap.

If true, when an [Intent] to go to the beginning/end of a wordwrapped line is received and the selection is already at the beginning/end of the line, then the selection will be moved to the next/previous line. If false, the selection will remain at the wordwrap.

# ExtendSelectionByCharacterIntent

```dart
class ExtendSelectionByCharacterIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the previous or the next character boundary.

### ExtendSelectionByCharacterIntent()

```dart
ExtendSelectionByCharacterIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionByCharacterIntent].

# ExtendSelectionToNextWordBoundaryIntent

```dart
class ExtendSelectionToNextWordBoundaryIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the previous or the next word boundary.

### ExtendSelectionToNextWordBoundaryIntent()

```dart
ExtendSelectionToNextWordBoundaryIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionToNextWordBoundaryIntent].

# ExtendSelectionToNextWordBoundaryOrCaretLocationIntent

```dart
class ExtendSelectionToNextWordBoundaryOrCaretLocationIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the previous or the next word boundary, or the [TextSelection.base] position if it's closer in the move direction.

This [Intent] typically has the same effect as an [ExtendSelectionToNextWordBoundaryIntent], except it collapses the selection when the order of [TextSelection.base] and [TextSelection.extent] would reverse.

This is typically only used on MacOS.

### ExtendSelectionToNextWordBoundaryOrCaretLocationIntent()

```dart
ExtendSelectionToNextWordBoundaryOrCaretLocationIntent({required bool forward})
```

Creates an [ExtendSelectionToNextWordBoundaryOrCaretLocationIntent].

# ExpandSelectionToDocumentBoundaryIntent

```dart
class ExpandSelectionToDocumentBoundaryIntent extends DirectionalCaretMovementIntent {}
```

Expands the current selection to the document boundary in the direction given by [forward].

Unlike [ExpandSelectionToLineBreakIntent], the extent will be moved, which matches the behavior on MacOS.

See also:

[ExtendSelectionToDocumentBoundaryIntent], which is similar but always moves the extent.

### ExpandSelectionToDocumentBoundaryIntent()

```dart
ExpandSelectionToDocumentBoundaryIntent({required bool forward})
```

Creates an [ExpandSelectionToDocumentBoundaryIntent].

# ExpandSelectionToLineBreakIntent

```dart
class ExpandSelectionToLineBreakIntent extends DirectionalCaretMovementIntent {}
```

Expands the current selection to the closest line break in the direction given by [forward].

Either the base or extent can move, whichever is closer to the line break. The selection will never shrink.

This behavior is common on MacOS.

See also:

[ExtendSelectionToLineBreakIntent], which is similar but always moves the extent.

### ExpandSelectionToLineBreakIntent()

```dart
ExpandSelectionToLineBreakIntent({required bool forward})
```

Creates an [ExpandSelectionToLineBreakIntent].

# ExtendSelectionToLineBreakIntent

```dart
class ExtendSelectionToLineBreakIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the closest line break in the direction given by [forward].

See also:

[ExpandSelectionToLineBreakIntent], which is similar but always increases the size of the selection.

### ExtendSelectionToLineBreakIntent()

```dart
ExtendSelectionToLineBreakIntent({required bool forward, required bool collapseSelection, bool collapseAtReversal = false, bool continuesAtWrap = false})
```

Creates an [ExtendSelectionToLineBreakIntent].

# ExtendSelectionVerticallyToAdjacentLineIntent

```dart
class ExtendSelectionVerticallyToAdjacentLineIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the closest position on the adjacent line.

### ExtendSelectionVerticallyToAdjacentLineIntent()

```dart
ExtendSelectionVerticallyToAdjacentLineIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionVerticallyToAdjacentLineIntent].

# ExtendSelectionVerticallyToAdjacentPageIntent

```dart
class ExtendSelectionVerticallyToAdjacentPageIntent extends DirectionalCaretMovementIntent {}
```

Expands, or moves the current selection from the current [TextSelection.extent] position to the closest position on the adjacent page.

### ExtendSelectionVerticallyToAdjacentPageIntent()

```dart
ExtendSelectionVerticallyToAdjacentPageIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionVerticallyToAdjacentPageIntent].

# ExtendSelectionToNextParagraphBoundaryIntent

```dart
class ExtendSelectionToNextParagraphBoundaryIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the previous or the next paragraph boundary.

### ExtendSelectionToNextParagraphBoundaryIntent()

```dart
ExtendSelectionToNextParagraphBoundaryIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionToNextParagraphBoundaryIntent].

# ExtendSelectionToNextParagraphBoundaryOrCaretLocationIntent

```dart
class ExtendSelectionToNextParagraphBoundaryOrCaretLocationIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the previous or the next paragraph boundary depending on the [forward] parameter.

This [Intent] typically has the same effect as an [ExtendSelectionToNextParagraphBoundaryIntent], except it collapses the selection when the order of [TextSelection.base] and [TextSelection.extent] would reverse.

This is typically only used on MacOS.

### ExtendSelectionToNextParagraphBoundaryOrCaretLocationIntent()

```dart
ExtendSelectionToNextParagraphBoundaryOrCaretLocationIntent({required bool forward})
```

Creates an [ExtendSelectionToNextParagraphBoundaryOrCaretLocationIntent].

# ExtendSelectionToDocumentBoundaryIntent

```dart
class ExtendSelectionToDocumentBoundaryIntent extends DirectionalCaretMovementIntent {}
```

Extends, or moves the current selection from the current [TextSelection.extent] position to the start or the end of the document.

See also:

[ExtendSelectionToDocumentBoundaryIntent], which is similar but always increases the size of the selection.

### ExtendSelectionToDocumentBoundaryIntent()

```dart
ExtendSelectionToDocumentBoundaryIntent({required bool forward, required bool collapseSelection})
```

Creates an [ExtendSelectionToDocumentBoundaryIntent].

# ScrollToDocumentBoundaryIntent

```dart
class ScrollToDocumentBoundaryIntent extends DirectionalTextEditingIntent {}
```

Scrolls to the beginning or end of the document depending on the [forward] parameter.

### ScrollToDocumentBoundaryIntent()

```dart
ScrollToDocumentBoundaryIntent({required bool forward})
```

Creates a [ScrollToDocumentBoundaryIntent].

# SelectAllTextIntent

```dart
class SelectAllTextIntent extends Intent {}
```

An [Intent] to select everything in the field.

### SelectAllTextIntent()

```dart
SelectAllTextIntent(SelectionChangedCause cause)
```

Creates an instance of [SelectAllTextIntent].

### cause

```dart
SelectionChangedCause cause
```

{@template flutter.widgets.TextEditingIntents.cause} The [SelectionChangedCause] that triggered the intent. {@endtemplate}

# CopySelectionTextIntent

```dart
class CopySelectionTextIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to copy or cut the current selection in the field.

### CopySelectionTextIntent.cut()

```dart
CopySelectionTextIntent.cut(SelectionChangedCause cause)
```

Creates an [Intent] that represents a user interaction that attempts to cut the current selection in the field.

### copy

```dart
CopySelectionTextIntent copy
```

An [Intent] that represents a user interaction that attempts to copy the current selection in the field.

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

### collapseSelection

```dart
bool collapseSelection
```

Whether the original text needs to be removed from the input field if the copy action was successful.

# PasteTextIntent

```dart
class PasteTextIntent extends Intent {}
```

An [Intent] to paste text from [Clipboard] to the field.

### PasteTextIntent()

```dart
PasteTextIntent(SelectionChangedCause cause)
```

Creates an instance of [PasteTextIntent].

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

# RedoTextIntent

```dart
class RedoTextIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to go back to the previous editing state.

### RedoTextIntent()

```dart
RedoTextIntent(SelectionChangedCause cause)
```

Creates a [RedoTextIntent].

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

# ReplaceTextIntent

```dart
class ReplaceTextIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to modify the current [TextEditingValue] in an input field.

### ReplaceTextIntent()

```dart
ReplaceTextIntent(TextEditingValue currentTextEditingValue, String replacementText, TextRange replacementRange, SelectionChangedCause cause)
```

Creates a [ReplaceTextIntent].

### currentTextEditingValue

```dart
TextEditingValue currentTextEditingValue
```

The [TextEditingValue] that this [Intent]'s action should perform on.

### replacementText

```dart
String replacementText
```

The text to replace the original text within the [replacementRange] with.

### replacementRange

```dart
TextRange replacementRange
```

The range of text in [currentTextEditingValue] that needs to be replaced.

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

# UndoTextIntent

```dart
class UndoTextIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to go back to the previous editing state.

### UndoTextIntent()

```dart
UndoTextIntent(SelectionChangedCause cause)
```

Creates an [UndoTextIntent].

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

# UpdateSelectionIntent

```dart
class UpdateSelectionIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to change the selection in an input field.

### UpdateSelectionIntent()

```dart
UpdateSelectionIntent(TextEditingValue currentTextEditingValue, TextSelection newSelection, SelectionChangedCause cause)
```

Creates an [UpdateSelectionIntent].

### currentTextEditingValue

```dart
TextEditingValue currentTextEditingValue
```

The [TextEditingValue] that this [Intent]'s action should perform on.

### newSelection

```dart
TextSelection newSelection
```

The new [TextSelection] the input field should adopt.

### cause

```dart
SelectionChangedCause cause
```

{@macro flutter.widgets.TextEditingIntents.cause}

# TransposeCharactersIntent

```dart
class TransposeCharactersIntent extends Intent {}
```

An [Intent] that represents a user interaction that attempts to swap the characters immediately around the cursor.

### TransposeCharactersIntent()

```dart
TransposeCharactersIntent()
```

Creates a [TransposeCharactersIntent].

# EditableTextTapOutsideIntent

```dart
class EditableTextTapOutsideIntent extends Intent {}
```

An [Intent] that represents a tap outside the field.

Invoked when the user taps outside the focused [EditableText] if [EditableText.onTapOutside] is null.

Override this [Intent] to modify the default behavior, which is to unfocus on a touch event on web and do nothing on other platforms.

See also:

- [Action.overridable] for an example on how to make an [Action] overridable.

### EditableTextTapOutsideIntent()

```dart
EditableTextTapOutsideIntent({required FocusNode focusNode, required PointerDownEvent pointerDownEvent})
```

Creates an [EditableTextTapOutsideIntent].

### focusNode

```dart
FocusNode focusNode
```

The [FocusNode] that this [Intent]'s action should be performed on.

### pointerDownEvent

```dart
PointerDownEvent pointerDownEvent
```

The [PointerDownEvent] that initiated this [Intent].

# EditableTextTapUpOutsideIntent

```dart
class EditableTextTapUpOutsideIntent extends Intent {}
```

An [Intent] that represents a tap outside the field.

Invoked when the user taps up outside the focused [EditableText] if [EditableText.onTapUpOutside] is null.

Override this [Intent] to modify the default behavior, which is to unfocus on a touch event on web and do nothing on other platforms.

{@tool dartpad} A common requirement is to unfocus text fields when the user taps outside of it. For UX reasons, it's often desirable to only unfocus when the user taps outside of the text field, but not when they scroll.

To achieve this, you can override the default behavior of [EditableTextTapOutsideIntent] and [EditableTextTapUpOutsideIntent] to check the difference in distance between the pointer down and pointer up events before potentially unfocusing.

** See code in examples/api/lib/widgets/text_editing_intents/editable_text_tap_up_outside_intent.0.dart ** {@end-tool}

See also:

- [Action.overridable] for an example on how to make an [Action] overridable.

### EditableTextTapUpOutsideIntent()

```dart
EditableTextTapUpOutsideIntent({required FocusNode focusNode, required PointerUpEvent pointerUpEvent})
```

Creates an [EditableTextTapUpOutsideIntent].

### focusNode

```dart
FocusNode focusNode
```

The [FocusNode] that this [Intent]'s action should be performed on.

### pointerUpEvent

```dart
PointerUpEvent pointerUpEvent
```

The [PointerUpEvent] that initiated this [Intent].
