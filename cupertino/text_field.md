@docImport 'package:flutter/material.dart';

# OverlayVisibilityMode

```dart
enum OverlayVisibilityMode {}
```

Visibility of text field overlays based on the state of the current text entry.

Used to toggle the visibility behavior of the optional decorating widgets surrounding the [EditableText] such as the clear text button.

Overlay will never appear regardless of the text entry state.

Overlay will only appear when the current text entry is not empty.

This includes prefilled text that the user did not type in manually. But does not include text in placeholders.

Overlay will only appear when the current text entry is empty.

This also includes not having prefilled text that the user did not type in manually. Texts in placeholders are ignored.

Always show the overlay regardless of the text entry state.

# CupertinoTextField

```dart
class CupertinoTextField extends StatefulWidget {}
```

An iOS-style text field.

A text field lets the user enter text, either with a hardware keyboard or with an onscreen keyboard.

This widget corresponds to both a `UITextField` and an editable `UITextView` on iOS.

The text field calls the [onChanged] callback whenever the user changes the text in the field. If the user indicates that they are done typing in the field (e.g., by pressing a button on the soft keyboard), the text field calls the [onSubmitted] callback.

{@macro flutter.widgets.EditableText.onChanged}

{@tool dartpad} This example shows how to set the initial value of the [CupertinoTextField] using a [controller] that already contains some text.

** See code in examples/api/lib/cupertino/text_field/cupertino_text_field.0.dart ** {@end-tool}

The [controller] can also control the selection and composing region (and to observe changes to the text, selection, and composing region).

The text field has an overridable [decoration] that, by default, draws a rounded rectangle border around the text field. If you set the [decoration] property to null, the decoration will be removed entirely.

{@macro flutter.material.textfield.wantKeepAlive}

Remember to call [TextEditingController.dispose] when it is no longer needed. This will ensure we discard any resources used by the object.

{@macro flutter.widgets.editableText.showCaretOnScreen}

## Scrolling Considerations

If this [CupertinoTextField] is not a descendant of [Scaffold] and is being used within a [Scrollable] or nested [Scrollable]s, consider placing a [ScrollNotificationObserver] above the root [Scrollable] that contains this [CupertinoTextField] to ensure proper scroll coordination for [CupertinoTextField] and its components like [TextSelectionOverlay].

See also:

- <https://developer.apple.com/documentation/uikit/uitextfield>
- [TextField], an alternative text field widget that follows the Material Design UI conventions.
- [EditableText], which is the raw text editing control at the heart of a [TextField].
- Learn how to use a [TextEditingController] in one of our [cookbook recipes](https://docs.flutter.dev/cookbook/forms/text-field-changes#2-use-a-texteditingcontroller).
- <https://developer.apple.com/design/human-interface-guidelines/ios/controls/text-fields/>

### CupertinoTextField()

```dart
CupertinoTextField({dynamic key, Object groupId = EditableText, TextEditingController? controller, FocusNode? focusNode, UndoHistoryController? undoController, BoxDecoration? decoration = _kDefaultRoundedBorderDecoration, EdgeInsetsGeometry padding = const EdgeInsets.all(7.0), String? placeholder, TextStyle? placeholderStyle = const TextStyle(fontWeight: FontWeight.w400, color: CupertinoColors.placeholderText), Widget? prefix, OverlayVisibilityMode prefixMode = OverlayVisibilityMode.always, Widget? suffix, OverlayVisibilityMode suffixMode = OverlayVisibilityMode.always, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, OverlayVisibilityMode clearButtonMode = OverlayVisibilityMode.never, String? clearButtonSemanticLabel, TextInputType? keyboardType, TextInputAction? textInputAction, TextCapitalization textCapitalization = TextCapitalization.none, TextStyle? style, StrutStyle? strutStyle, TextAlign textAlign = TextAlign.start, TextAlignVertical? textAlignVertical, TextDirection? textDirection, bool readOnly = false, ToolbarOptions? toolbarOptions, bool? showCursor, bool autofocus = false, String obscuringCharacter = '•', bool obscureText = false, bool? autocorrect = true, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, int? maxLines = 1, int? minLines, bool expands = false, int? maxLength, MaxLengthEnforcement? maxLengthEnforcement, ValueChanged<String>? onChanged, VoidCallback? onEditingComplete, ValueChanged<String>? onSubmitted, TapRegionCallback? onTapOutside, TapRegionCallback? onTapUpOutside, List<TextInputFormatter>? inputFormatters, bool enabled = true, double cursorWidth = 2.0, double? cursorHeight, Radius cursorRadius = const Radius.circular(2.0), bool cursorOpacityAnimates = true, Color? cursorColor, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, Brightness? keyboardAppearance, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool? enableInteractiveSelection, bool? selectAllOnFocus, TextSelectionControls? selectionControls, GestureTapCallback? onTap, ScrollController? scrollController, ScrollPhysics? scrollPhysics, Iterable<String>? autofillHints = const <String>[], ContentInsertionConfiguration? contentInsertionConfiguration, Clip clipBehavior = Clip.hardEdge, String? restorationId, bool scribbleEnabled = true, bool stylusHandwritingEnabled = EditableText.defaultStylusHandwritingEnabled, bool enableIMEPersonalizedLearning = true, bool? enableInlinePrediction, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, SpellCheckConfiguration? spellCheckConfiguration, TextMagnifierConfiguration? magnifierConfiguration})
```

Creates an iOS-style text field.

To provide a prefilled text entry, pass in a [TextEditingController] with an initial value to the [controller] parameter.

To provide a hint placeholder text that appears when the text entry is empty, pass a [String] to the [placeholder] parameter.

The [maxLines] property can be set to null to remove the restriction on the number of lines. In this mode, the intrinsic height of the widget will grow as the number of lines of text grows. By default, it is `1`, meaning this is a single-line text field and will scroll horizontally when it overflows. [maxLines] must not be zero.

The text cursor is not shown if [showCursor] is false or if [showCursor] is null (the default) and [readOnly] is true.

If specified, the [maxLength] property must be greater than zero.

The [selectionHeightStyle] and [selectionWidthStyle] properties allow changing the shape of the selection highlighting. These properties default to [EditableText.defaultSelectionHeightStyle] and [EditableText.defaultSelectionWidthStyle], respectively.

The [autocorrect], [autofocus], [clearButtonMode], [dragStartBehavior], [expands], [obscureText], [prefixMode], [readOnly], [scrollPadding], [suffixMode], [textAlign], [selectionHeightStyle], [selectionWidthStyle], [enableSuggestions], and [enableIMEPersonalizedLearning] properties must not be null.

{@macro flutter.widgets.editableText.accessibility}

See also:

- [minLines], which is the minimum number of lines to occupy when the content spans fewer lines.
- [expands], to allow the widget to size itself to its parent's height.
- [maxLength], which discusses the precise meaning of "number of characters" and how it may differ from the intuitive meaning.

### CupertinoTextField.borderless()

```dart
CupertinoTextField.borderless({dynamic key, Object groupId = EditableText, TextEditingController? controller, FocusNode? focusNode, UndoHistoryController? undoController, BoxDecoration? decoration, EdgeInsetsGeometry padding = const EdgeInsets.all(7.0), String? placeholder, TextStyle? placeholderStyle = _kDefaultPlaceholderStyle, Widget? prefix, OverlayVisibilityMode prefixMode = OverlayVisibilityMode.always, Widget? suffix, OverlayVisibilityMode suffixMode = OverlayVisibilityMode.always, CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center, OverlayVisibilityMode clearButtonMode = OverlayVisibilityMode.never, String? clearButtonSemanticLabel, TextInputType? keyboardType, TextInputAction? textInputAction, TextCapitalization textCapitalization = TextCapitalization.none, TextStyle? style, StrutStyle? strutStyle, TextAlign textAlign = TextAlign.start, TextAlignVertical? textAlignVertical, TextDirection? textDirection, bool readOnly = false, ToolbarOptions? toolbarOptions, bool? showCursor, bool autofocus = false, String obscuringCharacter = '•', bool obscureText = false, bool? autocorrect, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, int? maxLines = 1, int? minLines, bool expands = false, int? maxLength, MaxLengthEnforcement? maxLengthEnforcement, ValueChanged<String>? onChanged, VoidCallback? onEditingComplete, ValueChanged<String>? onSubmitted, TapRegionCallback? onTapOutside, TapRegionCallback? onTapUpOutside, List<TextInputFormatter>? inputFormatters, bool enabled = true, double cursorWidth = 2.0, double? cursorHeight, Radius cursorRadius = const Radius.circular(2.0), bool cursorOpacityAnimates = true, Color? cursorColor, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, Brightness? keyboardAppearance, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool? enableInteractiveSelection, bool? selectAllOnFocus, TextSelectionControls? selectionControls, GestureTapCallback? onTap, ScrollController? scrollController, ScrollPhysics? scrollPhysics, Iterable<String>? autofillHints = const <String>[], ContentInsertionConfiguration? contentInsertionConfiguration, Clip clipBehavior = Clip.hardEdge, String? restorationId, bool scribbleEnabled = true, bool stylusHandwritingEnabled = true, bool enableIMEPersonalizedLearning = true, bool? enableInlinePrediction, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, SpellCheckConfiguration? spellCheckConfiguration, TextMagnifierConfiguration? magnifierConfiguration})
```

Creates a borderless iOS-style text field.

To provide a prefilled text entry, pass in a [TextEditingController] with an initial value to the [controller] parameter.

To provide a hint placeholder text that appears when the text entry is empty, pass a [String] to the [placeholder] parameter.

The [maxLines] property can be set to null to remove the restriction on the number of lines. In this mode, the intrinsic height of the widget will grow as the number of lines of text grows. By default, it is `1`, meaning this is a single-line text field and will scroll horizontally when it overflows. [maxLines] must not be zero.

The text cursor is not shown if [showCursor] is false or if [showCursor] is null (the default) and [readOnly] is true.

If specified, the [maxLength] property must be greater than zero.

The [selectionHeightStyle] and [selectionWidthStyle] properties allow changing the shape of the selection highlighting. These properties default to [ui.BoxHeightStyle.tight] and [ui.BoxWidthStyle.tight] respectively.

See also:

- [minLines], which is the minimum number of lines to occupy when the content spans fewer lines.
- [expands], to allow the widget to size itself to its parent's height.
- [maxLength], which discusses the precise meaning of "number of characters" and how it may differ from the intuitive meaning.

### groupId

```dart
Object groupId
```

{@macro flutter.widgets.editableText.groupId}

### controller

```dart
TextEditingController? controller
```

Controls the text being edited.

If null, this widget will create its own [TextEditingController].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### decoration

```dart
BoxDecoration? decoration
```

Controls the [BoxDecoration] of the box behind the text input.

Defaults to having a rounded rectangle grey border and can be null to have no box decoration.

### padding

```dart
EdgeInsetsGeometry padding
```

Padding around the text entry area between the [prefix] and [suffix] or the clear button when [clearButtonMode] is not never.

Defaults to a padding of 6 pixels on all sides and can be null.

### placeholder

```dart
String? placeholder
```

A lighter colored placeholder hint that appears on the first line of the text field when the text entry is empty.

Defaults to having no placeholder text.

The text style of the placeholder text matches that of the text field's main text entry except a lighter font weight and a grey font color.

### placeholderStyle

```dart
TextStyle? placeholderStyle
```

The style to use for the placeholder text.

The [placeholderStyle] is merged with the [style] [TextStyle] when applied to the [placeholder] text. To avoid merging with [style], specify [TextStyle.inherit] as false.

Defaults to the [style] property with w300 font weight and grey color.

If specifically set to null, placeholder's style will be the same as [style].

### prefix

```dart
Widget? prefix
```

An optional [Widget] to display before the text.

### prefixMode

```dart
OverlayVisibilityMode prefixMode
```

Controls the visibility of the [prefix] widget based on the state of text entry when the [prefix] argument is not null.

Defaults to [OverlayVisibilityMode.always].

Has no effect when [prefix] is null.

### suffix

```dart
Widget? suffix
```

An optional [Widget] to display after the text.

### suffixMode

```dart
OverlayVisibilityMode suffixMode
```

Controls the visibility of the [suffix] widget based on the state of text entry when the [suffix] argument is not null.

Defaults to [OverlayVisibilityMode.always].

Has no effect when [suffix] is null.

### crossAxisAlignment

```dart
CrossAxisAlignment crossAxisAlignment
```

Controls the vertical alignment of the [prefix] and the [suffix] widget in relation to content.

Defaults to [CrossAxisAlignment.center].

Has no effect when both the [prefix] and [suffix] are null.

### clearButtonMode

```dart
OverlayVisibilityMode clearButtonMode
```

Show an iOS-style clear button to clear the current text entry.

Can be made to appear depending on various text states of the [TextEditingController].

Will only appear if no [suffix] widget is appearing.

Defaults to [OverlayVisibilityMode.never].

### clearButtonSemanticLabel

```dart
String? clearButtonSemanticLabel
```

The semantic label for the clear button used by screen readers.

This will be used by screen reading software to identify the clear button widget. Defaults to "Clear".

### keyboardType

```dart
TextInputType keyboardType
```

{@macro flutter.widgets.editableText.keyboardType}

### textInputAction

```dart
TextInputAction? textInputAction
```

The type of action button to use for the keyboard.

Defaults to [TextInputAction.newline] if [keyboardType] is [TextInputType.multiline] and [TextInputAction.done] otherwise.

### textCapitalization

```dart
TextCapitalization textCapitalization
```

{@macro flutter.widgets.editableText.textCapitalization}

### style

```dart
TextStyle? style
```

The style to use for the text being edited.

Also serves as a base for the [placeholder] text's style.

Defaults to the standard iOS font style from [CupertinoTheme] if null.

### strutStyle

```dart
StrutStyle? strutStyle
```

{@macro flutter.widgets.editableText.strutStyle}

### textAlign

```dart
TextAlign textAlign
```

{@macro flutter.widgets.editableText.textAlign}

### toolbarOptions

```dart
ToolbarOptions? toolbarOptions
```

Configuration of toolbar options.

If not set, select all and paste will default to be enabled. Copy and cut will be disabled if [obscureText] is true. If [readOnly] is true, paste and cut will be disabled regardless.

### textAlignVertical

```dart
TextAlignVertical? textAlignVertical
```

{@macro flutter.material.InputDecorator.textAlignVertical}

### textDirection

```dart
TextDirection? textDirection
```

{@macro flutter.widgets.editableText.textDirection}

### readOnly

```dart
bool readOnly
```

{@macro flutter.widgets.editableText.readOnly}

### showCursor

```dart
bool? showCursor
```

{@macro flutter.widgets.editableText.showCursor}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.editableText.autofocus}

### obscuringCharacter

```dart
String obscuringCharacter
```

{@macro flutter.widgets.editableText.obscuringCharacter}

### obscureText

```dart
bool obscureText
```

{@macro flutter.widgets.editableText.obscureText}

### autocorrect

```dart
bool? autocorrect
```

{@macro flutter.widgets.editableText.autocorrect}

### smartDashesType

```dart
SmartDashesType smartDashesType
```

{@macro flutter.services.TextInputConfiguration.smartDashesType}

### smartQuotesType

```dart
SmartQuotesType smartQuotesType
```

{@macro flutter.services.TextInputConfiguration.smartQuotesType}

### enableSuggestions

```dart
bool enableSuggestions
```

{@macro flutter.services.TextInputConfiguration.enableSuggestions}

### maxLines

```dart
int? maxLines
```

{@macro flutter.widgets.editableText.maxLines}

- [expands], which determines whether the field should fill the height of its parent.

### minLines

```dart
int? minLines
```

{@macro flutter.widgets.editableText.minLines}

- [expands], which determines whether the field should fill the height of its parent.

### expands

```dart
bool expands
```

{@macro flutter.widgets.editableText.expands}

### maxLength

```dart
int? maxLength
```

The maximum number of characters (Unicode grapheme clusters) to allow in the text field.

After [maxLength] characters have been input, additional input is ignored, unless [maxLengthEnforcement] is set to [MaxLengthEnforcement.none].

The TextField enforces the length with a [LengthLimitingTextInputFormatter], which is evaluated after the supplied [inputFormatters], if any.

This value must be either null or greater than zero. If set to null (the default), there is no limit to the number of characters allowed.

Whitespace characters (e.g. newline, space, tab) are included in the character count.

{@macro flutter.services.lengthLimitingTextInputFormatter.maxLength}

### maxLengthEnforcement

```dart
MaxLengthEnforcement? maxLengthEnforcement
```

Determines how the [maxLength] limit should be enforced.

If [MaxLengthEnforcement.none] is set, additional input beyond [maxLength] will not be enforced by the limit.

{@macro flutter.services.textFormatter.effectiveMaxLengthEnforcement}

{@macro flutter.services.textFormatter.maxLengthEnforcement}

### onChanged

```dart
ValueChanged<String>? onChanged
```

{@macro flutter.widgets.editableText.onChanged}

### onEditingComplete

```dart
VoidCallback? onEditingComplete
```

{@macro flutter.widgets.editableText.onEditingComplete}

### onSubmitted

```dart
ValueChanged<String>? onSubmitted
```

{@macro flutter.widgets.editableText.onSubmitted}

See also:

- [TextInputAction.next] and [TextInputAction.previous], which automatically shift the focus to the next/previous focusable item when the user is done editing.

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

{@macro flutter.widgets.editableText.onTapOutside}

### onTapUpOutside

```dart
TapRegionCallback? onTapUpOutside
```

{@macro flutter.widgets.editableText.onTapUpOutside}

### inputFormatters

```dart
List<TextInputFormatter>? inputFormatters
```

{@macro flutter.widgets.editableText.inputFormatters}

### enabled

```dart
bool enabled
```

Disables the text field when false.

Text fields in disabled states have a light grey background and don't respond to touch events including the [prefix], [suffix] and the clear button.

Defaults to true.

### cursorWidth

```dart
double cursorWidth
```

{@macro flutter.widgets.editableText.cursorWidth}

### cursorHeight

```dart
double? cursorHeight
```

{@macro flutter.widgets.editableText.cursorHeight}

### cursorRadius

```dart
Radius cursorRadius
```

{@macro flutter.widgets.editableText.cursorRadius}

### cursorOpacityAnimates

```dart
bool cursorOpacityAnimates
```

{@macro flutter.widgets.editableText.cursorOpacityAnimates}

### cursorColor

```dart
Color? cursorColor
```

The color to use when painting the cursor.

Defaults to the [DefaultSelectionStyle.cursorColor]. If that color is null, it uses the [CupertinoThemeData.primaryColor] of the ambient theme, which itself defaults to [CupertinoColors.activeBlue] in the light theme and [CupertinoColors.activeOrange] in the dark theme.

### selectionHeightStyle

```dart
ui.BoxHeightStyle? selectionHeightStyle
```

Controls how tall the selection highlight boxes are computed to be.

See [ui.BoxHeightStyle] for details on available styles.

### selectionWidthStyle

```dart
ui.BoxWidthStyle? selectionWidthStyle
```

Controls how wide the selection highlight boxes are computed to be.

See [ui.BoxWidthStyle] for details on available styles.

### keyboardAppearance

```dart
Brightness? keyboardAppearance
```

The appearance of the keyboard.

This setting is only honored on iOS devices.

If null, defaults to [Brightness.light].

### scrollPadding

```dart
EdgeInsets scrollPadding
```

{@macro flutter.widgets.editableText.scrollPadding}

### enableInteractiveSelection

```dart
bool enableInteractiveSelection
```

{@macro flutter.widgets.editableText.enableInteractiveSelection}

### selectAllOnFocus

```dart
bool? selectAllOnFocus
```

{@macro flutter.widgets.editableText.selectAllOnFocus}

### selectionControls

```dart
TextSelectionControls? selectionControls
```

{@macro flutter.widgets.editableText.selectionControls}

### dragStartBehavior

```dart
DragStartBehavior dragStartBehavior
```

{@macro flutter.widgets.scrollable.dragStartBehavior}

### scrollController

```dart
ScrollController? scrollController
```

{@macro flutter.widgets.editableText.scrollController}

### scrollPhysics

```dart
ScrollPhysics? scrollPhysics
```

{@macro flutter.widgets.editableText.scrollPhysics}

### selectionEnabled

```dart
bool get selectionEnabled
```

{@macro flutter.widgets.editableText.selectionEnabled}

### onTap

```dart
GestureTapCallback? onTap
```

{@macro flutter.material.textfield.onTap}

### autofillHints

```dart
Iterable<String>? autofillHints
```

{@macro flutter.widgets.editableText.autofillHints} {@macro flutter.services.AutofillConfiguration.autofillHints}

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### restorationId

```dart
String? restorationId
```

{@macro flutter.material.textfield.restorationId}

### scribbleEnabled

```dart
bool scribbleEnabled
```

{@macro flutter.widgets.editableText.scribbleEnabled}

### stylusHandwritingEnabled

```dart
bool stylusHandwritingEnabled
```

{@macro flutter.widgets.editableText.stylusHandwritingEnabled}

### enableIMEPersonalizedLearning

```dart
bool enableIMEPersonalizedLearning
```

{@macro flutter.services.TextInputConfiguration.enableIMEPersonalizedLearning}

### enableInlinePrediction

```dart
bool? enableInlinePrediction
```

{@macro flutter.services.TextInputConfiguration.enableInlinePrediction}

### contentInsertionConfiguration

```dart
ContentInsertionConfiguration? contentInsertionConfiguration
```

{@macro flutter.widgets.editableText.contentInsertionConfiguration}

### contextMenuBuilder

```dart
EditableTextContextMenuBuilder? contextMenuBuilder
```

{@macro flutter.widgets.EditableText.contextMenuBuilder}

If not provided, will build a default menu based on the platform.

See also:

- [CupertinoAdaptiveTextSelectionToolbar], which is built by default.

### magnifierConfiguration

```dart
TextMagnifierConfiguration? magnifierConfiguration
```

Configuration for the text field magnifier.

By default (when this property is set to null), a [CupertinoTextMagnifier] is used on mobile platforms, and nothing on desktop platforms. To suppress the magnifier on all platforms, consider passing [TextMagnifierConfiguration.disabled] explicitly.

{@macro flutter.widgets.magnifier.intro}

{@tool dartpad} This sample demonstrates how to customize the magnifier that this text field uses.

** See code in examples/api/lib/widgets/text_magnifier/text_magnifier.0.dart ** {@end-tool}

### spellCheckConfiguration

```dart
SpellCheckConfiguration? spellCheckConfiguration
```

{@macro flutter.widgets.EditableText.spellCheckConfiguration}

If [SpellCheckConfiguration.misspelledTextStyle] is not specified in this configuration, then [cupertinoMisspelledTextStyle] is used by default.

### cupertinoMisspelledTextStyle

```dart
TextStyle cupertinoMisspelledTextStyle
```

The [TextStyle] used to indicate misspelled words in the Cupertino style.

See also:

- [SpellCheckConfiguration.misspelledTextStyle], the style configured to mark misspelled words with.
- [TextField.materialMisspelledTextStyle], the style configured to mark misspelled words with in the Material style.

### kMisspelledSelectionColor

```dart
Color kMisspelledSelectionColor
```

The color of the selection highlight when the spell check menu is visible.

Eyeballed from a screenshot taken on an iPhone 11 running iOS 16.2.

### defaultSpellCheckSuggestionsToolbarBuilder()

```dart
Widget defaultSpellCheckSuggestionsToolbarBuilder(BuildContext context, EditableTextState editableTextState)
```

Default builder for the spell check suggestions toolbar in the Cupertino style.

See also:

- [spellCheckConfiguration], where this is typically specified for [CupertinoTextField].
- [SpellCheckConfiguration.spellCheckSuggestionsToolbarBuilder], the parameter for which this is the default value for [CupertinoTextField].
- [TextField.defaultSpellCheckSuggestionsToolbarBuilder], which is like this but specifies the default for [CupertinoTextField].

### undoController

```dart
UndoHistoryController? undoController
```

{@macro flutter.widgets.undoHistory.controller}

### createState()

```dart
State<CupertinoTextField> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### inferIOSSpellCheckConfiguration()

```dart
SpellCheckConfiguration inferIOSSpellCheckConfiguration(SpellCheckConfiguration? configuration)
```

Returns a new [SpellCheckConfiguration] where the given configuration has had any missing values replaced with their defaults for the iOS platform.
