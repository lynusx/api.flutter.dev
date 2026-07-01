@docImport 'package:flutter/material.dart';

# PlaceholderSpan

```dart
abstract class PlaceholderSpan extends InlineSpan {}
```

An immutable placeholder that is embedded inline within text.

[PlaceholderSpan] represents a placeholder that acts as a stand-in for other content. A [PlaceholderSpan] by itself does not contain useful information to change a [TextSpan]. [WidgetSpan] from the widgets library extends [PlaceholderSpan] and may be used instead to specify a widget as the contents of the placeholder.

Flutter widgets such as [TextField], [Text] and [RichText] do not recognize [PlaceholderSpan] subclasses other than [WidgetSpan]. **Consider implementing the [WidgetSpan] interface instead of the [Placeholder] interface.**

See also:

- [WidgetSpan], a leaf node that represents an embedded inline widget.
- [TextSpan], a node that represents text in a [TextSpan] tree.
- [Text], a widget for showing uniformly-styled text.
- [RichText], a widget for finer control of text rendering.
- [TextPainter], a class for painting [TextSpan] objects on a [Canvas].

### PlaceholderSpan()

```dart
PlaceholderSpan({ui.PlaceholderAlignment alignment = ui.PlaceholderAlignment.bottom, TextBaseline? baseline, TextStyle? style})
```

Creates a [PlaceholderSpan] with the given values.

A [TextStyle] may be provided with the [style] property, but only the decoration, foreground, background, and spacing options will be used.

### placeholderCodeUnit

```dart
int placeholderCodeUnit
```

The unicode character to represent a placeholder.

### alignment

```dart
ui.PlaceholderAlignment alignment
```

How the placeholder aligns vertically with the text.

See [ui.PlaceholderAlignment] for details on each mode.

### baseline

```dart
TextBaseline? baseline
```

The [TextBaseline] to align against when using [ui.PlaceholderAlignment.baseline], [ui.PlaceholderAlignment.aboveBaseline], and [ui.PlaceholderAlignment.belowBaseline].

This is ignored when using other alignment modes.

### computeToPlainText()

```dart
void computeToPlainText(StringBuffer buffer, {bool includeSemanticsLabels = true, bool includePlaceholders = true})
```

[PlaceholderSpan]s are flattened to a `0xFFFC` object replacement character in the plain text representation when `includePlaceholders` is true.

### computeSemanticsInformation()

```dart
void computeSemanticsInformation(List<InlineSpanSemanticsInformation> collector)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### debugAssertIsValid()

```dart
bool debugAssertIsValid()
```
