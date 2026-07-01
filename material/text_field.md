@docImport 'input_border.dart'; @docImport 'material.dart'; @docImport 'scaffold.dart'; @docImport 'text_form_field.dart'; @docImport 'text_theme.dart';

# InputCounterWidgetBuilder

```dart
typedef InputCounterWidgetBuilder = Widget? Function(BuildContext context, {required int currentLength, required int? maxLength, required bool isFocused})
```

Signature for the [TextField.buildCounter] callback.

The build context for the TextField.

The length of the string currently in the input.

The maximum string length that can be entered into the TextField.

Whether or not the TextField is currently focused. Mainly provided for the [liveRegion] parameter in the [Semantics] widget for accessibility.

# TextField

```dart
class TextField extends StatefulWidget {}
```

A Material Design text field.

A text field lets the user enter text, either with hardware keyboard or with an onscreen keyboard.

The text field calls the [onChanged] callback whenever the user changes the text in the field. If the user indicates that they are done typing in the field (e.g., by pressing a button on the soft keyboard), the text field calls the [onSubmitted] callback.

To control the text that is displayed in the text field, use the [controller]. For example, to set the initial value of the text field, use a [controller] that already contains some text. The [controller] can also control the selection and composing region (and to observe changes to the text, selection, and composing region).

By default, a text field has a [decoration] that draws a divider below the text field. You can use the [decoration] property to control the decoration, for example by adding a label or an icon. If you set the [decoration] property to null, the decoration will be removed entirely, including the extra padding introduced by the decoration to save space for the labels.

If [decoration] is non-null (which is the default), the text field requires one of its ancestors to be a [Material] widget.

To integrate the [TextField] into a [Form] with other [FormField] widgets, consider using [TextFormField].

{@template flutter.material.textfield.wantKeepAlive} When the widget has focus, it will prevent itself from disposing via its underlying [EditableText]'s [AutomaticKeepAliveClientMixin.wantKeepAlive] in order to avoid losing the selection. Removing the focus will allow it to be disposed. {@endtemplate}

Remember to call [TextEditingController.dispose] on the [TextEditingController] when it is no longer needed. This will ensure we discard any resources used by the object.

If this field is part of a scrolling container that lazily constructs its children, like a [ListView] or a [CustomScrollView], then a [controller] should be specified. The controller's lifetime should be managed by a stateful widget ancestor of the scrolling container.

## Obscured Input

{@tool dartpad} This example shows how to create a [TextField] that will obscure input. The [InputDecoration] surrounds the field in a border using [OutlineInputBorder] and adds a label.

** See code in examples/api/lib/material/text_field/text_field.0.dart ** {@end-tool}

## Reading values

A common way to read a value from a TextField is to use the [onSubmitted] callback. This callback is applied to the text field's current value when the user finishes editing.

{@tool dartpad} This sample shows how to get a value from a TextField via the [onSubmitted] callback.

** See code in examples/api/lib/material/text_field/text_field.1.dart ** {@end-tool}

{@macro flutter.widgets.EditableText.lifeCycle}

For most applications the [onSubmitted] callback will be sufficient for reacting to user input.

The [onEditingComplete] callback also runs when the user finishes editing. It's different from [onSubmitted] because it has a default value which updates the text controller and yields the keyboard focus. Applications that require different behavior can override the default [onEditingComplete] callback.

Keep in mind you can also always read the current string from a TextField's [TextEditingController] using [TextEditingController.text].

## Handling emojis and other complex characters

{@macro flutter.widgets.EditableText.onChanged}

In the live Dartpad example above, try typing the emoji 👨‍👩‍👦 into the field and submitting. Because the example code measures the length with `value.characters.length`, the emoji is correctly counted as a single character.

{@macro flutter.widgets.editableText.showCaretOnScreen}

{@macro flutter.widgets.editableText.accessibility}

{@tool dartpad} This sample shows how to style a text field to match a filled or outlined Material Design 3 text field.

** See code in examples/api/lib/material/text_field/text_field.2.dart ** {@end-tool}

## Scrolling Considerations

If this [TextField] is not a descendant of [Scaffold] and is being used within a [Scrollable] or nested [Scrollable]s, consider placing a [ScrollNotificationObserver] above the root [Scrollable] that contains this [TextField] to ensure proper scroll coordination for [TextField] and its components like [TextSelectionOverlay].

{@tool dartpad} This sample demonstrates how to use the [Shortcuts] and [Actions] widgets to create a custom `Shift+Enter` keyboard shortcut for inserting a new line in a [TextField].

** See code in examples/api/lib/material/text_field/text_field.3.dart ** {@end-tool}

See also:

- [TextFormField], which integrates with the [Form] widget.
- [InputDecorator], which shows the labels and other visual elements that surround the actual text editing widget.
- [EditableText], which is the raw text editing control at the heart of a [TextField]. The [EditableText] widget is rarely used directly unless you are implementing an entirely different design language, such as Cupertino.
- <https://material.io/design/components/text-fields.html>
- Cookbook: [Create and style a text field](https://docs.flutter.dev/cookbook/forms/text-input)
- Cookbook: [Handle changes to a text field](https://docs.flutter.dev/cookbook/forms/text-field-changes)
- Cookbook: [Retrieve the value of a text field](https://docs.flutter.dev/cookbook/forms/retrieve-input)
- Cookbook: [Focus and text fields](https://docs.flutter.dev/cookbook/forms/focus)

### TextField()

```dart
TextField({dynamic key, Object groupId = EditableText, TextEditingController? controller, FocusNode? focusNode, UndoHistoryController? undoController, InputDecoration? decoration = const InputDecoration(), TextInputType? keyboardType, TextInputAction? textInputAction, TextCapitalization textCapitalization = TextCapitalization.none, TextStyle? style, StrutStyle? strutStyle, TextAlign textAlign = TextAlign.start, TextAlignVertical? textAlignVertical, TextDirection? textDirection, bool readOnly = false, ToolbarOptions? toolbarOptions, bool? showCursor, bool autofocus = false, MaterialStatesController? statesController, String obscuringCharacter = '•', bool obscureText = false, bool? autocorrect, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, int? maxLines = 1, int? minLines, bool expands = false, int? maxLength, MaxLengthEnforcement? maxLengthEnforcement, ValueChanged<String>? onChanged, VoidCallback? onEditingComplete, ValueChanged<String>? onSubmitted, AppPrivateCommandCallback? onAppPrivateCommand, List<TextInputFormatter>? inputFormatters, bool? enabled, bool? ignorePointers, double cursorWidth = 2.0, double? cursorHeight, Radius? cursorRadius, bool? cursorOpacityAnimates, Color? cursorColor, Color? cursorErrorColor, ui.BoxHeightStyle? selectionHeightStyle, ui.BoxWidthStyle? selectionWidthStyle, Brightness? keyboardAppearance, EdgeInsets scrollPadding = const EdgeInsets.all(20.0), DragStartBehavior dragStartBehavior = DragStartBehavior.start, bool? enableInteractiveSelection, bool? selectAllOnFocus, TextSelectionControls? selectionControls, GestureTapCallback? onTap, bool onTapAlwaysCalled = false, TapRegionCallback? onTapOutside, TapRegionUpCallback? onTapUpOutside, MouseCursor? mouseCursor, InputCounterWidgetBuilder? buildCounter, ScrollController? scrollController, ScrollPhysics? scrollPhysics, Iterable<String>? autofillHints = const <String>[], ContentInsertionConfiguration? contentInsertionConfiguration, Clip clipBehavior = Clip.hardEdge, String? restorationId, bool scribbleEnabled = true, bool stylusHandwritingEnabled = EditableText.defaultStylusHandwritingEnabled, bool enableIMEPersonalizedLearning = true, bool? enableInlinePrediction, EditableTextContextMenuBuilder? contextMenuBuilder = _defaultContextMenuBuilder, bool canRequestFocus = true, SpellCheckConfiguration? spellCheckConfiguration, TextMagnifierConfiguration? magnifierConfiguration, List<Locale>? hintLocales})
```

Creates a Material Design text field.

If [decoration] is non-null (which is the default), the text field requires one of its ancestors to be a [Material] widget.

To remove the decoration entirely (including the extra padding introduced by the decoration to save space for the labels), set the [decoration] to null.

The [maxLines] property can be set to null to remove the restriction on the number of lines. By default, it is one, meaning this is a single-line text field. [maxLines] must not be zero.

The [maxLength] property is set to null by default, which means the number of characters allowed in the text field is not restricted. If [maxLength] is set a character counter will be displayed below the field showing how many characters have been entered. If the value is set to a positive integer it will also display the maximum allowed number of characters to be entered. If the value is set to [TextField.noMaxLength] then only the current length is displayed.

After [maxLength] characters have been input, additional input is ignored, unless [maxLengthEnforcement] is set to [MaxLengthEnforcement.none]. The text field enforces the length with a [LengthLimitingTextInputFormatter], which is evaluated after the supplied [inputFormatters], if any. The [maxLength] value must be either null or greater than zero.

If [maxLengthEnforcement] is set to [MaxLengthEnforcement.none], then more than [maxLength] characters may be entered, and the error counter and divider will switch to the [decoration].errorStyle when the limit is exceeded.

The text cursor is not shown if [showCursor] is false or if [showCursor] is null (the default) and [readOnly] is true.

The [selectionHeightStyle] and [selectionWidthStyle] properties allow changing the shape of the selection highlighting. These properties default to [EditableText.defaultSelectionHeightStyle] and [EditableText.defaultSelectionHeightStyle], respectively.

See also:

- [maxLength], which discusses the precise meaning of "number of characters" and how it may differ from the intuitive meaning.

### magnifierConfiguration

```dart
TextMagnifierConfiguration? magnifierConfiguration
```

The configuration for the magnifier of this text field.

By default, builds a [CupertinoTextMagnifier] on iOS and [TextMagnifier] on Android, and builds nothing on all other platforms. To suppress the magnifier, consider passing [TextMagnifierConfiguration.disabled].

{@macro flutter.widgets.magnifier.intro}

{@tool dartpad} This sample demonstrates how to customize the magnifier that this text field uses.

** See code in examples/api/lib/widgets/text_magnifier/text_magnifier.0.dart ** {@end-tool}

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

Defines the keyboard focus for this widget.

The [focusNode] is a long-lived object that's typically managed by a [StatefulWidget] parent. See [FocusNode] for more information.

To give the keyboard focus to this widget, provide a [focusNode] and then use the current [FocusScope] to request the focus:

```dart
FocusScope.of(context).requestFocus(myFocusNode);
```

This happens automatically when the widget is tapped.

To be notified when the widget gains or loses the focus, add a listener to the [focusNode]:

```dart
myFocusNode.addListener(() { print(myFocusNode.hasFocus); });
```

If null, this widget will create its own [FocusNode].

## Keyboard

Requesting the focus will typically cause the keyboard to be shown if it's not showing already.

On Android, the user can hide the keyboard - without changing the focus - with the system back button. They can restore the keyboard's visibility by tapping on a text field. The user might hide the keyboard and switch to a physical keyboard, or they might just need to get it out of the way for a moment, to expose something it's obscuring. In this case requesting the focus again will not cause the focus to change, and will not make the keyboard visible.

This widget builds an [EditableText] and will ensure that the keyboard is showing when it is tapped by calling [EditableTextState.requestKeyboard()].

### decoration

```dart
InputDecoration? decoration
```

The decoration to show around the text field.

By default, draws a horizontal line under the text field but can be configured to show an icon, label, hint text, and error text.

Specify null to remove the decoration entirely (including the extra padding introduced by the decoration to save space for the labels).

### keyboardType

```dart
TextInputType keyboardType
```

{@macro flutter.widgets.editableText.keyboardType}

### textInputAction

```dart
TextInputAction? textInputAction
```

{@template flutter.widgets.TextField.textInputAction} The type of action button to use for the keyboard.

Defaults to [TextInputAction.newline] if [keyboardType] is [TextInputType.multiline] and [TextInputAction.done] otherwise. {@endtemplate}

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

This text style is also used as the base style for the [decoration].

If null, [TextTheme.bodyLarge] will be used. When the text field is disabled, [TextTheme.bodyLarge] with an opacity of 0.38 will be used instead.

If null and [ThemeData.useMaterial3] is false, [TextTheme.titleMedium] will be used. When the text field is disabled, [TextTheme.titleMedium] with [ThemeData.disabledColor] will be used instead.

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

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.editableText.autofocus}

### statesController

```dart
MaterialStatesController? statesController
```

Represents the interactive "state" of this widget in terms of a set of [WidgetState]s, including [WidgetState.disabled], [WidgetState.hovered], [WidgetState.error], and [WidgetState.focused].

Classes based on this one can provide their own [WidgetStatesController] to which they've added listeners. They can also update the controller's [WidgetStatesController.value] however, this may only be done when it's safe to call [State.setState], like in an event handler.

The controller's [WidgetStatesController.value] represents the set of states that a widget's visual properties, typically [WidgetStateProperty] values, are resolved against. It is _not_ the intrinsic state of the widget. The widget is responsible for ensuring that the controller's [WidgetStatesController.value] tracks its intrinsic state. For example one cannot request the keyboard focus for a widget by adding [WidgetState.focused] to its controller. When the widget gains the or loses the focus it will [WidgetStatesController.update] its controller's [WidgetStatesController.value] and notify listeners of the change.

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

### readOnly

```dart
bool readOnly
```

{@macro flutter.widgets.editableText.readOnly}

### toolbarOptions

```dart
ToolbarOptions? toolbarOptions
```

Configuration of toolbar options.

If not set, select all and paste will default to be enabled. Copy and cut will be disabled if [obscureText] is true. If [readOnly] is true, paste and cut will be disabled regardless.

### showCursor

```dart
bool? showCursor
```

{@macro flutter.widgets.editableText.showCursor}

### noMaxLength

```dart
int noMaxLength
```

If [maxLength] is set to this value, only the "current input length" part of the character counter is shown.

### maxLength

```dart
int? maxLength
```

The maximum number of characters (Unicode grapheme clusters) to allow in the text field.

If set, a character counter will be displayed below the field showing how many characters have been entered. If set to a number greater than 0, it will also display the maximum number allowed. If set to [TextField.noMaxLength] then only the current character count is displayed. To remove the counter, set [InputDecoration.counterText] to an empty string or return null from [TextField.buildCounter] callback.

After [maxLength] characters have been input, additional input is ignored, unless [maxLengthEnforcement] is set to [MaxLengthEnforcement.none].

The text field enforces the length with a [LengthLimitingTextInputFormatter], which is evaluated after the supplied [inputFormatters], if any.

This value must be either null, [TextField.noMaxLength], or greater than 0. If null (the default) then there is no limit to the number of characters that can be entered. If set to [TextField.noMaxLength], then no limit will be enforced, but the number of characters entered will still be displayed.

Whitespace characters (e.g. newline, space, tab) are included in the character count.

If [maxLengthEnforcement] is [MaxLengthEnforcement.none], then more than [maxLength] characters may be entered, but the error counter and divider will switch to the [decoration]'s [InputDecoration.errorStyle] when the limit is exceeded.

{@macro flutter.services.lengthLimitingTextInputFormatter.maxLength}

### maxLengthEnforcement

```dart
MaxLengthEnforcement? maxLengthEnforcement
```

Determines how the [maxLength] limit should be enforced.

{@macro flutter.services.textFormatter.effectiveMaxLengthEnforcement}

{@macro flutter.services.textFormatter.maxLengthEnforcement}

### onChanged

```dart
ValueChanged<String>? onChanged
```

{@macro flutter.widgets.editableText.onChanged}

See also:

- [inputFormatters], which are called before [onChanged] runs and can validate and change ("format") the input value.
- [onEditingComplete], [onSubmitted]: which are more specialized input change notifications.

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

### onAppPrivateCommand

```dart
AppPrivateCommandCallback? onAppPrivateCommand
```

{@macro flutter.widgets.editableText.onAppPrivateCommand}

### inputFormatters

```dart
List<TextInputFormatter>? inputFormatters
```

{@macro flutter.widgets.editableText.inputFormatters}

### enabled

```dart
bool? enabled
```

If false the text field is "disabled": it ignores taps and its [decoration] is rendered in grey.

If non-null this property overrides the [decoration]'s [InputDecoration.enabled] property.

When a text field is disabled, all of its children widgets are also disabled, including the [InputDecoration.suffixIcon]. If you need to keep the suffix icon interactive while disabling the text field, consider using [readOnly] and [enableInteractiveSelection] instead:

```dart
TextField(
  enabled: true,
  readOnly: true,
  enableInteractiveSelection: false,
  decoration: InputDecoration(
    suffixIcon: IconButton(
      onPressed: () {
        // This will work because the TextField is enabled
      },
      icon: const Icon(Icons.edit_outlined),
    ),
  ),
)
```

### ignorePointers

```dart
bool? ignorePointers
```

Determines whether this widget ignores pointer events.

Defaults to null, and when null, does nothing.

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
Radius? cursorRadius
```

{@macro flutter.widgets.editableText.cursorRadius}

### cursorOpacityAnimates

```dart
bool? cursorOpacityAnimates
```

{@macro flutter.widgets.editableText.cursorOpacityAnimates}

### cursorColor

```dart
Color? cursorColor
```

The color of the cursor.

The cursor indicates the current location of text insertion point in the field.

If this is null it will default to the ambient [DefaultSelectionStyle.cursorColor]. If that is null, and the [ThemeData.platform] is [TargetPlatform.iOS] or [TargetPlatform.macOS] it will use [CupertinoThemeData.primaryColor]. Otherwise it will use the value of [ColorScheme.primary] of [ThemeData.colorScheme].

### cursorErrorColor

```dart
Color? cursorErrorColor
```

The color of the cursor when the [InputDecorator] is showing an error.

If this is null it will default to [TextStyle.color] of [InputDecoration.errorStyle]. If that is null, it will use [ColorScheme.error] of [ThemeData.colorScheme].

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

If unset, defaults to [ThemeData.brightness].

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

### selectionEnabled

```dart
bool get selectionEnabled
```

{@macro flutter.widgets.editableText.selectionEnabled}

### onTap

```dart
GestureTapCallback? onTap
```

{@template flutter.material.textfield.onTap} Called for the first tap in a series of taps.

The text field builds a [GestureDetector] to handle input events like tap, to trigger focus requests, to move the caret, adjust the selection, etc. Handling some of those events by wrapping the text field with a competing GestureDetector is problematic.

To unconditionally handle taps, without interfering with the text field's internal gesture detector, provide this callback.

If the text field is created with [enabled] false, taps will not be recognized.

To be notified when the text field gains or loses the focus, provide a [focusNode] and add a listener to that.

To listen to arbitrary pointer events without competing with the text field's internal gesture detector, use a [Listener]. {@endtemplate}

If [onTapAlwaysCalled] is enabled, this will also be called for consecutive taps.

### onTapAlwaysCalled

```dart
bool onTapAlwaysCalled
```

Whether [onTap] should be called for every tap.

Defaults to false, so [onTap] is only called for each distinct tap. When enabled, [onTap] is called for every tap including consecutive taps.

### onTapOutside

```dart
TapRegionCallback? onTapOutside
```

{@macro flutter.widgets.editableText.onTapOutside}

{@tool dartpad} This example shows how to use a `TextFieldTapRegion` to wrap a set of "spinner" buttons that increment and decrement a value in the [TextField] without causing the text field to lose keyboard focus.

This example includes a generic `SpinnerField<T>` class that you can copy into your own project and customize.

** See code in examples/api/lib/widgets/tap_region/text_field_tap_region.0.dart ** {@end-tool}

See also:

- [TapRegion] for how the region group is determined.

### onTapUpOutside

```dart
TapRegionUpCallback? onTapUpOutside
```

{@macro flutter.widgets.editableText.onTapUpOutside}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.error].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

If this property is null, [WidgetStateMouseCursor.textable] will be used.

The [mouseCursor] is the only property of [TextField] that controls the appearance of the mouse pointer. All other properties related to "cursor" stand for the text cursor, which is usually a blinking vertical line at the editing position.

### buildCounter

```dart
InputCounterWidgetBuilder? buildCounter
```

Callback that generates a custom [InputDecoration.counter] widget.

See [InputCounterWidgetBuilder] for an explanation of the passed in arguments. The returned widget will be placed below the line in place of the default widget built when [InputDecoration.counterText] is specified.

The returned widget will be wrapped in a [Semantics] widget for accessibility, but it also needs to be accessible itself. For example, if returning a Text widget, set the [Text.semanticsLabel] property.

{@tool snippet}

```dart
Widget counter(
  BuildContext context,
  {
    required int currentLength,
    required int? maxLength,
    required bool isFocused,
  }
) {
  return Text(
    '$currentLength of $maxLength characters',
    semanticsLabel: 'character count',
  );
}
```

{@end-tool}

If buildCounter returns null, then no counter and no Semantics widget will be created at all.

### scrollPhysics

```dart
ScrollPhysics? scrollPhysics
```

{@macro flutter.widgets.editableText.scrollPhysics}

### scrollController

```dart
ScrollController? scrollController
```

{@macro flutter.widgets.editableText.scrollController}

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

{@template flutter.material.textfield.restorationId} Restoration ID to save and restore the state of the text field.

If non-null, the text field will persist and restore its current scroll offset and - if no [controller] has been provided - the content of the text field. If a [controller] has been provided, it is the responsibility of the owner of that controller to persist and restore it, e.g. by using a [RestorableTextEditingController].

The state of this widget is persisted in a [RestorationBucket] claimed from the surrounding [RestorationScope] using the provided restoration ID.

See also:

- [RestorationManager], which explains how state restoration works in Flutter. {@endtemplate}

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

- [AdaptiveTextSelectionToolbar], which is built by default.
- [BrowserContextMenu], which allows the browser's context menu on web to be disabled and Flutter-rendered context menus to appear.

### canRequestFocus

```dart
bool canRequestFocus
```

Determine whether this text field can request the primary focus.

Defaults to true. If false, the text field will not request focus when tapped, or when its context menu is displayed. If false it will not be possible to move the focus to the text field with tab key.

### undoController

```dart
UndoHistoryController? undoController
```

{@macro flutter.widgets.undoHistory.controller}

### hintLocales

```dart
List<Locale>? hintLocales
```

{@macro flutter.services.TextInputConfiguration.hintLocales}

### spellCheckConfiguration

```dart
SpellCheckConfiguration? spellCheckConfiguration
```

{@macro flutter.widgets.EditableText.spellCheckConfiguration}

If [SpellCheckConfiguration.misspelledTextStyle] is not specified in this configuration, then [materialMisspelledTextStyle] is used by default.

### materialMisspelledTextStyle

```dart
TextStyle materialMisspelledTextStyle
```

The [TextStyle] used to indicate misspelled words in the Material style.

See also:

- [SpellCheckConfiguration.misspelledTextStyle], the style configured to mark misspelled words with.
- [CupertinoTextField.cupertinoMisspelledTextStyle], the style configured to mark misspelled words with in the Cupertino style.

### defaultSpellCheckSuggestionsToolbarBuilder()

```dart
Widget defaultSpellCheckSuggestionsToolbarBuilder(BuildContext context, EditableTextState editableTextState)
```

Default builder for [TextField]'s spell check suggestions toolbar.

On Apple platforms, builds an iOS-style toolbar. Everywhere else, builds an Android-style toolbar.

See also:

- [spellCheckConfiguration], where this is typically specified for [TextField].
- [SpellCheckConfiguration.spellCheckSuggestionsToolbarBuilder], the parameter for which this is the default value for [TextField].
- [CupertinoTextField.defaultSpellCheckSuggestionsToolbarBuilder], which is like this but specifies the default for [CupertinoTextField].

### inferAndroidSpellCheckConfiguration()

```dart
SpellCheckConfiguration inferAndroidSpellCheckConfiguration(SpellCheckConfiguration? configuration)
```

Returns a new [SpellCheckConfiguration] where the given configuration has had any missing values replaced with their defaults for the Android platform.

### createState()

```dart
State<TextField> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
