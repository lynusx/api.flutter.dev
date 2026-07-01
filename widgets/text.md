@docImport 'package:flutter/gestures.dart'; @docImport 'package:flutter/material.dart';

@docImport 'editable_text.dart'; @docImport 'gesture_detector.dart'; @docImport 'implicit_animations.dart'; @docImport 'transitions.dart'; @docImport 'widget_span.dart';

# DefaultTextStyle

```dart
class DefaultTextStyle extends InheritedTheme {}
```

The text style to apply to descendant [Text] widgets which don't have an explicit style.

A [MediaQuery] ancestor of a [Text] widget may still override the [TextStyle.height], [TextStyle.letterSpacing], and [TextStyle.wordSpacing] of the [TextStyle] set by this [DefaultTextStyle] widget through its [MediaQueryData.lineHeightScaleFactorOverride], [MediaQueryData.letterSpacingOverride], and [MediaQueryData.wordSpacingOverride] members.

{@tool dartpad} This example shows how to use [DefaultTextStyle.merge] to create a default text style that inherits styling information from the current default text style and overrides some properties.

** See code in examples/api/lib/widgets/text/text.0.dart ** {@end-tool}

See also:

- [AnimatedDefaultTextStyle], which animates changes in the text style smoothly over a given duration.
- [DefaultTextStyleTransition], which takes a provided [Animation] to animate changes in text style smoothly over time.

### DefaultTextStyle()

```dart
DefaultTextStyle({dynamic key, required TextStyle style, TextAlign? textAlign, bool softWrap = true, TextOverflow overflow = TextOverflow.clip, int? maxLines, TextWidthBasis textWidthBasis = TextWidthBasis.parent, ui.TextHeightBehavior? textHeightBehavior, required Widget child})
```

Creates a default text style for the given subtree.

Consider using [DefaultTextStyle.merge] to inherit styling information from the current default text style for a given [BuildContext].

The [maxLines] property may be null (and indeed defaults to null), but if it is not null, it must be greater than zero.

### DefaultTextStyle.fallback()

```dart
DefaultTextStyle.fallback({dynamic key})
```

A const-constructable default text style that provides fallback values.

Returned from [of] when the given [BuildContext] doesn't have an enclosing default text style.

This constructor creates a [DefaultTextStyle] with an invalid [child], which means the constructed value cannot be incorporated into the tree.

### merge()

```dart
Widget merge({Key? key, TextStyle? style, TextAlign? textAlign, bool? softWrap, TextOverflow? overflow, int? maxLines, TextWidthBasis? textWidthBasis, TextHeightBehavior? textHeightBehavior, required Widget child})
```

Creates a default text style that overrides the text styles in scope at this point in the widget tree.

The given [style] is merged with the [style] from the default text style for the [BuildContext] where the widget is inserted, and any of the other arguments that are not null replace the corresponding properties on that same default text style.

This constructor cannot be used to override the [maxLines] property of the ancestor with the value null, since null here is used to mean "defer to ancestor". To replace a non-null [maxLines] from an ancestor with the null value (to remove the restriction on number of lines), manually obtain the ambient [DefaultTextStyle] using [DefaultTextStyle.of], then create a new [DefaultTextStyle] using the [DefaultTextStyle.new] constructor directly. See the source below for an example of how to do this (since that's essentially what this constructor does).

If a [textHeightBehavior] is provided, the existing configuration will be replaced completely. To retain part of the original [textHeightBehavior], manually obtain the ambient [DefaultTextStyle] using [DefaultTextStyle.of].

### style

```dart
TextStyle style
```

The text style to apply.

### textAlign

```dart
TextAlign? textAlign
```

How each line of text in the Text widget should be aligned horizontally.

### softWrap

```dart
bool softWrap
```

Whether the text should break at soft line breaks.

If false, the glyphs in the text will be positioned as if there was unlimited horizontal space.

This also decides the [overflow] property's behavior. If this is true or null, the glyph causing overflow, and those that follow, will not be rendered.

### overflow

```dart
TextOverflow overflow
```

How visual overflow should be handled.

If [softWrap] is true or null, the glyph causing overflow, and those that follow, will not be rendered. Otherwise, it will be shown with the given overflow option.

### maxLines

```dart
int? maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary. If the text exceeds the given number of lines, it will be truncated according to [overflow].

If this is 1, text will not wrap. Otherwise, text will be wrapped at the edge of the box.

If this is non-null, it will override even explicit null values of [Text.maxLines].

### textWidthBasis

```dart
TextWidthBasis textWidthBasis
```

The strategy to use when calculating the width of the Text.

See [TextWidthBasis] for possible values and their implications.

### textHeightBehavior

```dart
ui.TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### of()

```dart
DefaultTextStyle of(BuildContext context)
```

The closest instance of this class that encloses the given context.

If no such instance exists, returns an instance created by [DefaultTextStyle.fallback], which contains fallback values.

Typical usage is as follows:

```dart
DefaultTextStyle style = DefaultTextStyle.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DefaultTextStyle oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# DefaultTextHeightBehavior

```dart
class DefaultTextHeightBehavior extends InheritedTheme {}
```

The [TextHeightBehavior] that will apply to descendant [Text] and [EditableText] widgets which have not explicitly set [Text.textHeightBehavior].

If there is a [DefaultTextStyle] with a non-null [DefaultTextStyle.textHeightBehavior] below this widget, the [DefaultTextStyle.textHeightBehavior] will be used over this widget's [TextHeightBehavior].

See also:

- [DefaultTextStyle], which defines a [TextStyle] to apply to descendant [Text] widgets.

### DefaultTextHeightBehavior()

```dart
DefaultTextHeightBehavior({dynamic key, required TextHeightBehavior textHeightBehavior, required Widget child})
```

Creates a default text height behavior for the given subtree.

### textHeightBehavior

```dart
TextHeightBehavior textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### maybeOf()

```dart
TextHeightBehavior? maybeOf(BuildContext context)
```

The closest instance of [DefaultTextHeightBehavior] that encloses the given context, or null if none is found.

If no such instance exists, this method will return `null`.

Calling this method will create a dependency on the closest [DefaultTextHeightBehavior] in the [context], if there is one.

Typical usage is as follows:

```dart
TextHeightBehavior? defaultTextHeightBehavior = DefaultTextHeightBehavior.of(context);
```

See also:

- [DefaultTextHeightBehavior.maybeOf], which is similar to this method, but asserts if no [DefaultTextHeightBehavior] ancestor is found.

### of()

```dart
TextHeightBehavior of(BuildContext context)
```

The closest instance of [DefaultTextHeightBehavior] that encloses the given context.

If no such instance exists, this method will assert in debug mode, and throw an exception in release mode.

Typical usage is as follows:

```dart
TextHeightBehavior defaultTextHeightBehavior = DefaultTextHeightBehavior.of(context);
```

Calling this method will create a dependency on the closest [DefaultTextHeightBehavior] in the [context].

See also:

- [DefaultTextHeightBehavior.maybeOf], which is similar to this method, but returns null if no [DefaultTextHeightBehavior] ancestor is found.

### updateShouldNotify()

```dart
bool updateShouldNotify(DefaultTextHeightBehavior oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# Text

```dart
class Text extends StatelessWidget {}
```

A run of text with a single style.

The [Text] widget displays a string of text with single style. The string might break across multiple lines or might all be displayed on the same line depending on the layout constraints.

The [style] argument is optional. When omitted, the text will use the style from the closest enclosing [DefaultTextStyle]. If the given style's [TextStyle.inherit] property is true (the default), the given style will be merged with the closest enclosing [DefaultTextStyle]. This merging behavior is useful, for example, to make the text bold while using the default font family and size.

{@tool snippet}

This example shows how to display text using the [Text] widget with the [overflow] set to [TextOverflow.ellipsis].

![If the text overflows, the Text widget displays an ellipsis to trim the overflowing text](https://flutter.github.io/assets-for-api-docs/assets/widgets/text_ellipsis.png)

```dart
Container(
  width: 100,
  decoration: BoxDecoration(border: Border.all()),
  child: const Text(
    'Hello, how are you?',
    overflow: TextOverflow.ellipsis,
  ),
)
```

{@end-tool}

{@tool snippet}

Setting [maxLines] to `1` is not equivalent to disabling soft wrapping with [softWrap]. This is apparent when using [TextOverflow.fade] as the following examples show.

![If a second line overflows the Text widget displays a horizontal fade](https://flutter.github.io/assets-for-api-docs/assets/widgets/text_fade_max_lines.png)

```dart
const Text(
  'Hello, how are you?',
  overflow: TextOverflow.fade,
  maxLines: 1,
)
```

Here soft wrapping is enabled and the [Text] widget tries to wrap the words "how are you?" to a second line. This is prevented by the [maxLines] value of `1`. The result is that a second line overflows and the fade appears in a horizontal direction at the bottom.

![If a single line overflows the Text widget displays a horizontal fade](https://flutter.github.io/assets-for-api-docs/assets/widgets/text_fade_soft_wrap.png)

```dart
const Text(
  'Hello, how are you?',
  overflow: TextOverflow.fade,
  softWrap: false,
)
```

Here soft wrapping is disabled with `softWrap: false` and the [Text] widget attempts to display its text in a single unbroken line. The result is that the single line overflows and the fade appears in a vertical direction at the right.

{@end-tool}

Using the [Text.rich] constructor, the [Text] widget can display a paragraph with differently styled [TextSpan]s. The sample that follows displays "Hello beautiful world" with different styles for each word.

{@tool snippet}

![The word "Hello" is shown with the default text styles. The word "beautiful" is italicized. The word "world" is bold.](https://flutter.github.io/assets-for-api-docs/assets/widgets/text_rich.png)

```dart
const Text.rich(
  TextSpan(
    text: 'Hello', // default text style
    children: <TextSpan>[
      TextSpan(text: ' beautiful ', style: TextStyle(fontStyle: FontStyle.italic)),
      TextSpan(text: 'world', style: TextStyle(fontWeight: FontWeight.bold)),
    ],
  ),
)
```

{@end-tool}

## Interactivity

To make [Text] react to touch events, wrap it in a [GestureDetector] widget with a [GestureDetector.onTap] handler.

In a Material Design application, consider using a [TextButton] instead, or if that isn't appropriate, at least using an [InkWell] instead of [GestureDetector].

To make sections of the text interactive, use [RichText] and specify a [TapGestureRecognizer] as the [TextSpan.recognizer] of the relevant part of the text.

## Selection

[Text] is not selectable by default. To make a [Text] selectable, one can wrap a subtree with a [SelectionArea] widget. To exclude a part of a subtree under [SelectionArea] from selection, once can also wrap that part of the subtree with [SelectionContainer.disabled].

{@tool dartpad} This sample demonstrates how to disable selection for a Text under a SelectionArea.

** See code in examples/api/lib/material/selection_container/selection_container_disabled.0.dart ** {@end-tool}

See also:

- [RichText], which gives you more control over the text styles.
- [DefaultTextStyle], which sets default styles for [Text] widgets.
- [SelectableRegion], which provides an overview of the selection system.

### Text()

```dart
Text(String? data, {dynamic key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, TextScaler? textScaler, int? maxLines, String? semanticsLabel, String? semanticsIdentifier, TextWidthBasis? textWidthBasis, ui.TextHeightBehavior? textHeightBehavior, Color? selectionColor})
```

Creates a text widget.

If the [style] argument is null, the text will use the style from the closest enclosing [DefaultTextStyle].

The [overflow] property's behavior is affected by the [softWrap] argument. If the [softWrap] is true or null, the glyph causing overflow, and those that follow, will not be rendered. Otherwise, it will be shown with the given overflow option.

### Text.rich()

```dart
Text.rich(InlineSpan? textSpan, {dynamic key, TextStyle? style, StrutStyle? strutStyle, TextAlign? textAlign, TextDirection? textDirection, Locale? locale, bool? softWrap, TextOverflow? overflow, double? textScaleFactor, TextScaler? textScaler, int? maxLines, String? semanticsLabel, String? semanticsIdentifier, TextWidthBasis? textWidthBasis, ui.TextHeightBehavior? textHeightBehavior, Color? selectionColor})
```

Creates a text widget with a [InlineSpan].

The following subclasses of [InlineSpan] may be used to build rich text:

- [TextSpan]s define text and children [InlineSpan]s.
- [WidgetSpan]s define embedded inline widgets.

See [RichText] which provides a lower-level way to draw text.

### data

```dart
String? data
```

The text to display.

This will be null if a [textSpan] is provided instead.

### textSpan

```dart
InlineSpan? textSpan
```

The text to display as a [InlineSpan].

This will be null if [data] is provided instead.

### style

```dart
TextStyle? style
```

If non-null, the style to use for this text.

If the style's "inherit" property is true, the style will be merged with the closest enclosing [DefaultTextStyle]. Otherwise, the style will replace the closest enclosing [DefaultTextStyle].

The user or platform may override this [style]'s [TextStyle.fontWeight], [TextStyle.height], [TextStyle.letterSpacing], and [TextStyle.wordSpacing] via a [MediaQuery] ancestor's [MediaQueryData.boldText], [MediaQueryData.lineHeightScaleFactorOverride], [MediaQueryData.letterSpacingOverride], and [MediaQueryData.wordSpacingOverride] regardless of its [TextStyle.inherit] value.

### strutStyle

```dart
StrutStyle? strutStyle
```

{@macro flutter.painting.textPainter.strutStyle}

The user or platform may override this [strutStyle]'s [StrutStyle.height] via a [MediaQuery] ancestor's [MediaQueryData.lineHeightScaleFactorOverride].

### textAlign

```dart
TextAlign? textAlign
```

How the text should be aligned horizontally.

### textDirection

```dart
TextDirection? textDirection
```

The directionality of the text.

This decides how [textAlign] values like [TextAlign.start] and [TextAlign.end] are interpreted.

This is also used to disambiguate how to render bidirectional text. For example, if the [data] is an English phrase followed by a Hebrew phrase, in a [TextDirection.ltr] context the English phrase will be on the left and the Hebrew phrase to its right, while in a [TextDirection.rtl] context, the English phrase will be on the right and the Hebrew phrase on its left.

Defaults to the ambient [Directionality], if any.

### locale

```dart
Locale? locale
```

Used to select a font when the same Unicode character can be rendered differently, depending on the locale.

It's rarely necessary to set this property. By default its value is inherited from the enclosing app with `Localizations.localeOf(context)`.

See [RenderParagraph.locale] for more information.

### softWrap

```dart
bool? softWrap
```

Whether the text should break at soft line breaks.

If false, the glyphs in the text will be positioned as if there was unlimited horizontal space.

### overflow

```dart
TextOverflow? overflow
```

How visual overflow should be handled.

If this is null [TextStyle.overflow] will be used, otherwise the value from the nearest [DefaultTextStyle] ancestor will be used.

### textScaleFactor

```dart
double? textScaleFactor
```

Deprecated. Will be removed in a future version of Flutter. Use [textScaler] instead.

The number of font pixels for each logical pixel.

For example, if the text scale factor is 1.5, text will be 50% larger than the specified font size.

The value given to the constructor as textScaleFactor. If null, will use the [MediaQueryData.textScaleFactor] obtained from the ambient [MediaQuery], or 1.0 if there is no [MediaQuery] in scope.

### textScaler

```dart
TextScaler? textScaler
```

{@macro flutter.painting.textPainter.textScaler}

### maxLines

```dart
int? maxLines
```

An optional maximum number of lines for the text to span, wrapping if necessary. If the text exceeds the given number of lines, it will be truncated according to [overflow].

If this is 1, text will not wrap. Otherwise, text will be wrapped at the edge of the box.

If this is null, but there is an ambient [DefaultTextStyle] that specifies an explicit number for its [DefaultTextStyle.maxLines], then the [DefaultTextStyle] value will take precedence. You can use a [RichText] widget directly to entirely override the [DefaultTextStyle].

### semanticsLabel

```dart
String? semanticsLabel
```

{@template flutter.widgets.Text.semanticsLabel} An alternative semantics label for this text.

If present, the semantics of this widget will contain this value instead of the actual text. This will overwrite any of the semantics labels applied directly to the [TextSpan]s.

This is useful for replacing abbreviations or shorthands with the full text value:

```dart
const Text(r'$$', semanticsLabel: 'Double dollars')
```

{@endtemplate}

### semanticsIdentifier

```dart
String? semanticsIdentifier
```

A unique identifier for the semantics node for this widget.

This is useful for cases where the text widget needs to have a uniquely identifiable ID that is recognized through the automation tools without having a dependency on the actual content of the text that can possibly be dynamic in nature.

### textWidthBasis

```dart
TextWidthBasis? textWidthBasis
```

{@macro flutter.painting.textPainter.textWidthBasis}

### textHeightBehavior

```dart
ui.TextHeightBehavior? textHeightBehavior
```

{@macro dart.ui.textHeightBehavior}

### selectionColor

```dart
Color? selectionColor
```

The color to use when painting the selection.

This is ignored if [SelectionContainer.maybeOf] returns null in the [BuildContext] of the [Text] widget.

If null, the ambient [DefaultSelectionStyle] is used (if any); failing that, the selection color defaults to [DefaultSelectionStyle.defaultColor] (semi-transparent grey).

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
