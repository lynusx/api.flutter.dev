@docImport 'text_input.dart';

# TextEditingDelta

```dart
abstract class TextEditingDelta with Diagnosticable {}
```

A structure representing a granular change that has occurred to the editing state as a result of text editing.

See also:

- [TextEditingDeltaInsertion], a delta representing an insertion.
- [TextEditingDeltaDeletion], a delta representing a deletion.
- [TextEditingDeltaReplacement], a delta representing a replacement.
- [TextEditingDeltaNonTextUpdate], a delta representing an update to the selection and/or composing region.
- [TextInputConfiguration], to opt-in your [DeltaTextInputClient] to receive [TextEditingDelta]'s you must set [TextInputConfiguration.enableDeltaModel] to true.

### TextEditingDelta()

```dart
TextEditingDelta({required String oldText, required TextSelection selection, required TextRange composing})
```

Creates a delta for a given change to the editing state.

### TextEditingDelta.fromJSON()

```dart
TextEditingDelta.fromJSON(Map<String, dynamic> encoded)
```

Creates an instance of this class from a JSON object by inferring the type of delta based on values sent from the engine.

### oldText

```dart
String oldText
```

The old text state before the delta has occurred.

### selection

```dart
TextSelection selection
```

The range of text that is currently selected after the delta has been applied.

### composing

```dart
TextRange composing
```

The range of text that is still being composed after the delta has been applied.

### apply()

```dart
TextEditingValue apply(TextEditingValue value)
```

This method will take the given [TextEditingValue] and return a new [TextEditingValue] with that instance of [TextEditingDelta] applied to it.

# TextEditingDeltaInsertion

```dart
class TextEditingDeltaInsertion extends TextEditingDelta {}
```

A structure representing an insertion of a single/or contiguous sequence of characters at some offset of an editing state.

### TextEditingDeltaInsertion()

```dart
TextEditingDeltaInsertion({required String oldText, required String textInserted, required int insertionOffset, required TextSelection selection, required dynamic composing})
```

Creates an insertion delta for a given change to the editing state.

{@template flutter.services.TextEditingDelta.optIn} See also:

- [TextInputConfiguration], to opt-in your [DeltaTextInputClient] to receive [TextEditingDelta]'s you must set [TextInputConfiguration.enableDeltaModel] to true. {@endtemplate}

### textInserted

```dart
String textInserted
```

The text that is being inserted into [oldText].

### insertionOffset

```dart
int insertionOffset
```

The offset in the [oldText] where the insertion begins.

### apply()

```dart
TextEditingValue apply(TextEditingValue value)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TextEditingDeltaDeletion

```dart
class TextEditingDeltaDeletion extends TextEditingDelta {}
```

A structure representing the deletion of a single/or contiguous sequence of characters in an editing state.

### TextEditingDeltaDeletion()

```dart
TextEditingDeltaDeletion({required String oldText, required TextRange deletedRange, required TextSelection selection, required dynamic composing})
```

Creates a deletion delta for a given change to the editing state.

{@macro flutter.services.TextEditingDelta.optIn}

### deletedRange

```dart
TextRange deletedRange
```

The range in [oldText] that is being deleted.

### textDeleted

```dart
String get textDeleted
```

The text from [oldText] that is being deleted.

### apply()

```dart
TextEditingValue apply(TextEditingValue value)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TextEditingDeltaReplacement

```dart
class TextEditingDeltaReplacement extends TextEditingDelta {}
```

A structure representing a replacement of a range of characters with a new sequence of text.

### TextEditingDeltaReplacement()

```dart
TextEditingDeltaReplacement({required String oldText, required String replacementText, required TextRange replacedRange, required TextSelection selection, required dynamic composing})
```

Creates a replacement delta for a given change to the editing state.

The range that is being replaced can either grow or shrink based on the given replacement text.

A replacement can occur in cases such as auto-correct, suggestions, and when a selection is replaced by a single character.

{@macro flutter.services.TextEditingDelta.optIn}

### replacementText

```dart
String replacementText
```

The new text that is replacing [replacedRange] in [oldText].

### replacedRange

```dart
TextRange replacedRange
```

The range in [oldText] that is being replaced.

### textReplaced

```dart
String get textReplaced
```

The original text that is being replaced in [oldText].

### apply()

```dart
TextEditingValue apply(TextEditingValue value)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TextEditingDeltaNonTextUpdate

```dart
class TextEditingDeltaNonTextUpdate extends TextEditingDelta {}
```

A structure representing changes to the selection and/or composing regions of an editing state and no changes to the text value.

### TextEditingDeltaNonTextUpdate()

```dart
TextEditingDeltaNonTextUpdate({required String oldText, required TextSelection selection, required dynamic composing})
```

Creates a delta representing no updates to the text value of the current editing state. This delta includes updates to the selection and/or composing regions.

A situation where this delta would be created is when dragging the selection handles. There are no changes to the text, but there are updates to the selection and potentially the composing region as well.

{@macro flutter.services.TextEditingDelta.optIn}

### apply()

```dart
TextEditingValue apply(TextEditingValue value)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
