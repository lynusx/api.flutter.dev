@docImport 'dart:ui';

@docImport 'package:flutter/material.dart';

@docImport 'placeholder_span.dart';

# Accumulator

```dart
class Accumulator {}
```

Mutable wrapper of an integer that can be passed by reference to track a value across a recursive stack.

### Accumulator()

```dart
Accumulator([int _value = 0])
```

[Accumulator] may be initialized with a specified value, otherwise, it will initialize to zero.

### value

```dart
int get value
```

The integer stored in this [Accumulator].

### increment()

```dart
void increment(int addend)
```

Increases the [value] by the `addend`.

# InlineSpanVisitor

```dart
typedef InlineSpanVisitor = bool Function(InlineSpan span)
```

Called on each span as [InlineSpan.visitChildren] walks the [InlineSpan] tree.

Returns true when the walk should continue, and false to stop visiting further [InlineSpan]s.

# InlineSpanSemanticsInformation

```dart
class InlineSpanSemanticsInformation {}
```

The textual and semantic label information for an [InlineSpan].

For [PlaceholderSpan]s, [InlineSpanSemanticsInformation.placeholder] is used by default.

See also:

- [InlineSpan.getSemanticsInformation]

### InlineSpanSemanticsInformation()

```dart
InlineSpanSemanticsInformation(String text, {bool isPlaceholder = false, String? semanticsLabel, String? semanticsIdentifier, List<ui.StringAttribute> stringAttributes = const <ui.StringAttribute>[], GestureRecognizer? recognizer})
```

Constructs an object that holds the text and semantics label values of an [InlineSpan].

Use [InlineSpanSemanticsInformation.placeholder] instead of directly setting [isPlaceholder].

### placeholder

```dart
InlineSpanSemanticsInformation placeholder
```

The text info for a [PlaceholderSpan].

### text

```dart
String text
```

The text value, if any. For [PlaceholderSpan]s, this will be the unicode placeholder value.

### semanticsLabel

```dart
String? semanticsLabel
```

The semanticsLabel, if any.

### semanticsIdentifier

```dart
String? semanticsIdentifier
```

The semanticsIdentifier, if any.

### recognizer

```dart
GestureRecognizer? recognizer
```

The gesture recognizer, if any, for this span.

### isPlaceholder

```dart
bool isPlaceholder
```

Whether this is for a placeholder span.

### requiresOwnNode

```dart
bool requiresOwnNode
```

True if this configuration should get its own semantics node.

This will be the case if the [recognizer] is not null, or if [isPlaceholder] is true, or if [semanticsIdentifier] has a value.

### stringAttributes

```dart
List<ui.StringAttribute> stringAttributes
```

The string attributes attached to this semantics information

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

# combineSemanticsInfo()

```dart
List<InlineSpanSemanticsInformation> combineSemanticsInfo(List<InlineSpanSemanticsInformation> infoList)
```

Combines _semanticsInfo entries where permissible.

Consecutive inline spans can be combined if their [InlineSpanSemanticsInformation.requiresOwnNode] return false.

# InlineSpan

```dart
abstract class InlineSpan extends DiagnosticableTree {}
```

An immutable span of inline content which forms part of a paragraph.

- The subclass [TextSpan] specifies text and may contain child [InlineSpan]s.
- The subclass [PlaceholderSpan] represents a placeholder that may be filled with non-text content. [PlaceholderSpan] itself defines a [PlaceholderAlignment] and a [TextBaseline]. To be useful, [PlaceholderSpan] must be extended to define content. An instance of this is the [WidgetSpan] class in the widgets library.
- The subclass [WidgetSpan] specifies embedded inline widgets.

{@tool snippet}

This example shows a tree of [InlineSpan]s that make a query asking for a name with a [TextField] embedded inline.

```dart
Text.rich(
  TextSpan(
    text: 'My name is ',
    style: const TextStyle(color: Colors.black),
    children: <InlineSpan>[
      WidgetSpan(
        alignment: PlaceholderAlignment.baseline,
        baseline: TextBaseline.alphabetic,
        child: ConstrainedBox(
          constraints: const BoxConstraints(maxWidth: 100),
          child: const TextField(),
        )
      ),
      const TextSpan(
        text: '.',
      ),
    ],
  ),
)
```

{@end-tool}

See also:

- [Text], a widget for showing uniformly-styled text.
- [RichText], a widget for finer control of text rendering.
- [TextPainter], a class for painting [InlineSpan] objects on a [Canvas].

### InlineSpan()

```dart
InlineSpan({TextStyle? style})
```

Creates an [InlineSpan] with the given values.

### style

```dart
TextStyle? style
```

The [TextStyle] to apply to this span.

The [style] is also applied to any child spans when this is an instance of [TextSpan].

### build()

```dart
void build(ui.ParagraphBuilder builder, {TextScaler textScaler = TextScaler.noScaling, List<PlaceholderDimensions>? dimensions})
```

Apply the properties of this object to the given [ParagraphBuilder], from which a [Paragraph] can be obtained.

The `textScaler` parameter specifies a [TextScaler] that the text and placeholders will be scaled by. The scaling is performed before layout, so the text will be laid out with the scaled glyphs and placeholders.

The `dimensions` parameter specifies the sizes of the placeholders. Each [PlaceholderSpan] must be paired with a [PlaceholderDimensions] in the same order as defined in the [InlineSpan] tree.

[Paragraph] objects can be drawn on [Canvas] objects.

### visitChildren()

```dart
bool visitChildren(InlineSpanVisitor visitor)
```

Walks this [InlineSpan] and any descendants in pre-order and calls `visitor` for each span that has content.

When `visitor` returns true, the walk will continue. When `visitor` returns false, then the walk will end.

See also:

- [visitDirectChildren], which preforms `build`-order traversal on the immediate children of this [InlineSpan], regardless of whether they have content.

### visitDirectChildren()

```dart
bool visitDirectChildren(InlineSpanVisitor visitor)
```

Calls `visitor` for each immediate child of this [InlineSpan].

The immediate children are visited in the same order they are added to a [ui.ParagraphBuilder] in the [build] method, which is also the logical order of the child [InlineSpan]s in the text.

The traversal stops when all immediate children are visited, or when the `visitor` callback returns `false` on an immediate child. This method itself returns a `bool` indicating whether the visitor callback returned `true` on all immediate children.

See also:

- [visitChildren], which performs preorder traversal on this [InlineSpan] if it has content, and all its descendants with content.

### getSpanForPosition()

```dart
InlineSpan? getSpanForPosition(TextPosition position)
```

Returns the [InlineSpan] that contains the given position in the text.

### getSpanForPositionVisitor()

```dart
InlineSpan? getSpanForPositionVisitor(TextPosition position, Accumulator offset)
```

Performs the check at each [InlineSpan] for if the `position` falls within the range of the span and returns the span if it does.

The `offset` parameter tracks the current index offset in the text buffer formed if the contents of the [InlineSpan] tree were concatenated together starting from the root [InlineSpan].

This method should not be directly called. Use [getSpanForPosition] instead.

### toPlainText()

```dart
String toPlainText({bool includeSemanticsLabels = true, bool includePlaceholders = true})
```

Flattens the [InlineSpan] tree into a single string.

Styles are not honored in this process. If `includeSemanticsLabels` is true, then the text returned will include the [TextSpan.semanticsLabel]s instead of the text contents for [TextSpan]s.

When `includePlaceholders` is true, [PlaceholderSpan]s in the tree will be represented as a 0xFFFC 'object replacement character'.

### getSemanticsInformation()

```dart
List<InlineSpanSemanticsInformation> getSemanticsInformation()
```

Flattens the [InlineSpan] tree to a list of [InlineSpanSemanticsInformation] objects.

[PlaceholderSpan]s in the tree will be represented with a [InlineSpanSemanticsInformation.placeholder] value.

### computeSemanticsInformation()

```dart
void computeSemanticsInformation(List<InlineSpanSemanticsInformation> collector)
```

Walks the [InlineSpan] tree and accumulates a list of [InlineSpanSemanticsInformation] objects.

This method should not be directly called. Use [getSemanticsInformation] instead.

[PlaceholderSpan]s in the tree will be represented with a [InlineSpanSemanticsInformation.placeholder] value.

### computeToPlainText()

```dart
void computeToPlainText(StringBuffer buffer, {bool includeSemanticsLabels = true, bool includePlaceholders = true})
```

Walks the [InlineSpan] tree and writes the plain text representation to `buffer`.

This method should not be directly called. Use [toPlainText] instead.

Styles are not honored in this process. If `includeSemanticsLabels` is true, then the text returned will include the [TextSpan.semanticsLabel]s instead of the text contents for [TextSpan]s.

When `includePlaceholders` is true, [PlaceholderSpan]s in the tree will be represented as a 0xFFFC 'object replacement character'.

The plain-text representation of this [InlineSpan] is written into the `buffer`. This method will then recursively call [computeToPlainText] on its children [InlineSpan]s if available.

### codeUnitAt()

```dart
int? codeUnitAt(int index)
```

Returns the UTF-16 code unit at the given `index` in the flattened string.

This only accounts for the [TextSpan.text] values and ignores [PlaceholderSpan]s.

Returns null if the `index` is out of bounds.

### codeUnitAtVisitor()

```dart
int? codeUnitAtVisitor(int index, Accumulator offset)
```

Performs the check at each [InlineSpan] for if the `index` falls within the range of the span and returns the corresponding code unit. Returns null otherwise.

The `offset` parameter tracks the current index offset in the text buffer formed if the contents of the [InlineSpan] tree were concatenated together starting from the root [InlineSpan].

This method should not be directly called. Use [codeUnitAt] instead.

### debugAssertIsValid()

```dart
bool debugAssertIsValid()
```

In debug mode, throws an exception if the object is not in a valid configuration. Otherwise, returns true.

This is intended to be used as follows:

```dart
assert(myInlineSpan.debugAssertIsValid());
```

### compareTo()

```dart
RenderComparison compareTo(InlineSpan other)
```

Describe the difference between this span and another, in terms of how much damage it will make to the rendering. The comparison is deep.

Comparing [InlineSpan] objects of different types, for example, comparing a [TextSpan] to a [WidgetSpan], always results in [RenderComparison.layout].

See also:

- [TextStyle.compareTo], which does the same thing for [TextStyle]s.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
