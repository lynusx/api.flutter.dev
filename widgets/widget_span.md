@docImport 'editable_text.dart'; @docImport 'text.dart';

# WidgetSpan

```dart
class WidgetSpan extends PlaceholderSpan {}
```

An immutable widget that is embedded inline within text.

The [child] property is the widget that will be embedded. Children are constrained by the width of the paragraph.

The [child] property may contain its own [Widget] children (if applicable), including [Text] and [RichText] widgets which may include additional [WidgetSpan]s. Child [Text] and [RichText] widgets will be laid out independently and occupy a rectangular space in the parent text layout.

[WidgetSpan]s will be ignored when passed into a [TextPainter] directly. To properly layout and paint the [child] widget, [WidgetSpan] should be passed into a [Text.rich] widget.

{@tool snippet}

A card with `Hello World!` embedded inline within a TextSpan tree.

```dart
const Text.rich(
  TextSpan(
    children: <InlineSpan>[
      TextSpan(text: 'Flutter is'),
      WidgetSpan(
        child: SizedBox(
          width: 120,
          height: 50,
          child: Card(
            child: Center(
              child: Text('Hello World!')
            )
          ),
        )
      ),
      TextSpan(text: 'the best!'),
    ],
  )
)
```

{@end-tool}

[WidgetSpan] contributes the semantics of the [WidgetSpan.child] to the semantics tree.

See also:

- [TextSpan], a node that represents text in an [InlineSpan] tree.
- [Text], a widget for showing uniformly-styled text.
- [RichText], a widget for finer control of text rendering.
- [TextPainter], a class for painting [InlineSpan] objects on a [Canvas].

### WidgetSpan()

```dart
WidgetSpan({required Widget child, dynamic alignment, dynamic baseline, dynamic style})
```

Creates a [WidgetSpan] with the given values.

[WidgetSpan] is a leaf node in the [InlineSpan] tree. Child widgets are constrained by the width of the paragraph they occupy. Child widget heights are unconstrained, and may cause the text to overflow and be ellipsized/truncated.

A [TextStyle] may be provided with the [style] property, but only the decoration, foreground, background, and spacing options will be used.

### extractFromInlineSpan()

```dart
List<Widget> extractFromInlineSpan(InlineSpan span, TextScaler textScaler)
```

Helper function for extracting [WidgetSpan]s in preorder, from the given [InlineSpan] as a list of widgets.

The `textScaler` is the scaling strategy for scaling the content.

This function is used by [EditableText] and [RichText] so calling it directly is rarely necessary.

### child

```dart
Widget child
```

The widget to embed inline within text.

### build()

```dart
void build(ui.ParagraphBuilder builder, {TextScaler textScaler = TextScaler.noScaling, List<PlaceholderDimensions>? dimensions})
```

Adds a placeholder box to the paragraph builder if a size has been calculated for the widget.

Sizes are provided through `dimensions`, which should contain a 1:1 in-order mapping of widget to laid-out dimensions. If no such dimension is provided, the widget will be skipped.

The `textScaler` will be applied to the laid-out size of the widget.

### visitChildren()

```dart
bool visitChildren(InlineSpanVisitor visitor)
```

Calls `visitor` on this [WidgetSpan]. There are no children spans to walk.

### visitDirectChildren()

```dart
bool visitDirectChildren(InlineSpanVisitor visitor)
```

### getSpanForPositionVisitor()

```dart
InlineSpan? getSpanForPositionVisitor(TextPosition position, Accumulator offset)
```

### codeUnitAtVisitor()

```dart
int? codeUnitAtVisitor(int index, Accumulator offset)
```

### compareTo()

```dart
RenderComparison compareTo(InlineSpan other)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### getSpanForPosition()

```dart
InlineSpan? getSpanForPosition(TextPosition position)
```

Returns the text span that contains the given position in the text.

### debugAssertIsValid()

```dart
bool debugAssertIsValid()
```

In debug mode, throws an exception if the object is not in a valid configuration. Otherwise, returns true.

This is intended to be used as follows:

```dart
assert(myWidgetSpan.debugAssertIsValid());
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
