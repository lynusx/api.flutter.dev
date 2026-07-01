@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart'; @docImport 'package:flutter/rendering.dart';

@docImport 'live_text.dart'; @docImport 'scribe.dart'; @docImport 'text_formatter.dart';

# SmartDashesType

```dart
enum SmartDashesType {}
```

Indicates how to handle the intelligent replacement of dashes in text input.

See also:

- [TextField.smartDashesType]
- [CupertinoTextField.smartDashesType]
- [EditableText.smartDashesType]
- [SmartQuotesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits>

Smart dashes is disabled.

This corresponds to the ["no" value of UITextSmartDashesType](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/no).

Smart dashes is enabled.

This corresponds to the ["yes" value of UITextSmartDashesType](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/yes).

# SmartQuotesType

```dart
enum SmartQuotesType {}
```

Indicates how to handle the intelligent replacement of quotes in text input.

See also:

- [TextField.smartQuotesType]
- [CupertinoTextField.smartQuotesType]
- [EditableText.smartQuotesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits>

Smart quotes is disabled.

This corresponds to the ["no" value of UITextSmartQuotesType](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/no).

Smart quotes is enabled.

This corresponds to the ["yes" value of UITextSmartQuotesType](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/yes).

# TextInputType

```dart
class TextInputType {}
```

The type of information for which to optimize the text input control.

On Android, behavior may vary across device and keyboard provider.

This class stays as close to `Enum` interface as possible, and allows for additional flags for some input types. For example, numeric input can specify whether it supports decimal numbers and/or signed numbers.

### TextInputType.numberWithOptions()

```dart
TextInputType.numberWithOptions({bool? signed = false, bool? decimal = false})
```

Optimize for numerical information.

Requests a numeric keyboard with additional settings. The [signed] and [decimal] parameters are optional.

### index

```dart
int index
```

Enum value index, corresponds to one of the [values].

### signed

```dart
bool? signed
```

The number is signed, allowing a positive or negative sign at the start.

This flag is only used for the [number] input type, otherwise `null`. Use `const TextInputType.numberWithOptions(signed: true)` to set this.

### decimal

```dart
bool? decimal
```

The number is decimal, allowing a decimal point to provide fractional.

This flag is only used for the [number] input type, otherwise `null`. Use `const TextInputType.numberWithOptions(decimal: true)` to set this.

### text

```dart
TextInputType text
```

Optimize for textual information.

Requests the default platform keyboard.

### multiline

```dart
TextInputType multiline
```

Optimize for multiline textual information.

Requests the default platform keyboard, but accepts newlines when the enter key is pressed. This is the input type used for all multiline text fields.

### number

```dart
TextInputType number
```

Optimize for unsigned numerical information without a decimal point.

Requests a default keyboard with ready access to the number keys. Additional options, such as decimal point and/or positive/negative signs, can be requested using [TextInputType.numberWithOptions].

### phone

```dart
TextInputType phone
```

Optimize for telephone numbers.

Requests a keyboard with ready access to the number keys, "*", and "#".

### datetime

```dart
TextInputType datetime
```

Optimize for date and time information.

On iOS, requests the default keyboard.

On Android, requests a keyboard with ready access to the number keys, ":", and "-".

### emailAddress

```dart
TextInputType emailAddress
```

Optimize for email addresses.

Requests a keyboard with ready access to the "@" and "." keys.

### url

```dart
TextInputType url
```

Optimize for URLs.

Requests a keyboard with ready access to the "/" and "." keys.

### visiblePassword

```dart
TextInputType visiblePassword
```

Optimize for passwords that are visible to the user.

Requests a keyboard with ready access to both letters and numbers.

### name

```dart
TextInputType name
```

Optimized for a person's name.

On iOS, requests the [UIKeyboardType.namePhonePad](https://developer.apple.com/documentation/uikit/uikeyboardtype/namephonepad) keyboard, a keyboard optimized for entering a person’s name or phone number. Does not support auto-capitalization.

On Android, requests a keyboard optimized for [TYPE_TEXT_VARIATION_PERSON_NAME](https://developer.android.com/reference/android/text/InputType#TYPE_TEXT_VARIATION_PERSON_NAME).

### streetAddress

```dart
TextInputType streetAddress
```

Optimized for postal mailing addresses.

On iOS, requests the default keyboard.

On Android, requests a keyboard optimized for [TYPE_TEXT_VARIATION_POSTAL_ADDRESS](https://developer.android.com/reference/android/text/InputType#TYPE_TEXT_VARIATION_POSTAL_ADDRESS).

### none

```dart
TextInputType none
```

Prevent the OS from showing the on-screen virtual keyboard.

### webSearch

```dart
TextInputType webSearch
```

Optimized for web searches.

Requests a keyboard that includes keys useful for web searches as well as URLs.

On iOS, requests a default keyboard with ready access to the "." key. In contrast to [url], a space bar is available.

On Android this is remapped to the [url] keyboard type as it always shows a space bar.

### twitter

```dart
TextInputType twitter
```

Optimized for social media.

Requests a keyboard that includes keys useful for handles and tags.

On iOS, requests a default keyboard with ready access to the "@" and "#" keys.

On Android this is remapped to the [emailAddress] keyboard type as it always shows the "@" key.

### values

```dart
List<TextInputType> values
```

All possible enum values.

### toJson()

```dart
Map<String, dynamic> toJson()
```

Returns a representation of this object as a JSON object.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# TextInputAction

```dart
enum TextInputAction {}
```

An action the user has requested the text input control to perform.

Each action represents a logical meaning, and also configures the soft keyboard to display a certain kind of action button. The visual appearance of the action button might differ between versions of the same OS.

Despite the logical meaning of each action, choosing a particular [TextInputAction] does not necessarily cause any specific behavior to happen, other than changing the focus when appropriate. It is up to the developer to ensure that the behavior that occurs when an action button is pressed is appropriate for the action button chosen.

For example: If the user presses the keyboard action button on iOS when it reads "Emergency Call", the result should not be a focus change to the next TextField. This behavior is not logically appropriate for a button that says "Emergency Call".

See [EditableText] for more information about customizing action button behavior.

Most [TextInputAction]s are supported equally by both Android and iOS. However, there is not a complete, direct mapping between Android's IME input types and iOS's keyboard return types. Therefore, some [TextInputAction]s are inappropriate for one of the platforms. If a developer chooses an inappropriate [TextInputAction] when running in debug mode, an error will be thrown. If the same thing is done in release mode, then instead of sending the inappropriate value, Android will use "unspecified" on the platform side and iOS will use "default" on the platform side.

See also:

- [TextInput], which configures the platform's keyboard setup.
- [EditableText], which invokes callbacks when the action button is pressed.

Logical meaning: There is no relevant input action for the current input source, e.g., [TextField].

Android: Corresponds to Android's "IME_ACTION_NONE". The keyboard setup is decided by the OS. The keyboard will likely show a return key.

iOS: iOS does not have a keyboard return type of "none." It is inappropriate to choose this [TextInputAction] when running on iOS.

Logical meaning: Let the OS decide which action is most appropriate.

Android: Corresponds to Android's "IME_ACTION_UNSPECIFIED". The OS chooses which keyboard action to display. The decision will likely be a done button or a return key.

iOS: Corresponds to iOS's "UIReturnKeyDefault". The title displayed in the action button is "return".

Logical meaning: The user is done providing input to a group of inputs (like a form). Some kind of finalization behavior should now take place.

Android: Corresponds to Android's "IME_ACTION_DONE". The OS displays a button that represents completion, e.g., a checkmark button.

iOS: Corresponds to iOS's "UIReturnKeyDone". The title displayed in the action button is "Done".

Logical meaning: The user has entered some text that represents a destination, e.g., a restaurant name. The "go" button is intended to take the user to a part of the app that corresponds to this destination.

Android: Corresponds to Android's "IME_ACTION_GO". The OS displays a button that represents taking "the user to the target of the text they typed", e.g., a right-facing arrow button.

iOS: Corresponds to iOS's "UIReturnKeyGo". The title displayed in the action button is "Go".

Logical meaning: Execute a search query.

Android: Corresponds to Android's "IME_ACTION_SEARCH". The OS displays a button that represents a search, e.g., a magnifying glass button.

iOS: Corresponds to iOS's "UIReturnKeySearch". The title displayed in the action button is "Search".

Logical meaning: Sends something that the user has composed, e.g., an email or a text message.

Android: Corresponds to Android's "IME_ACTION_SEND". The OS displays a button that represents sending something, e.g., a paper plane button.

iOS: Corresponds to iOS's "UIReturnKeySend". The title displayed in the action button is "Send".

Logical meaning: The user is done with the current input source and wants to move to the next one.

Moves the focus to the next focusable item in the same [FocusScope].

Android: Corresponds to Android's "IME_ACTION_NEXT". The OS displays a button that represents moving forward, e.g., a right-facing arrow button.

iOS: Corresponds to iOS's "UIReturnKeyNext". The title displayed in the action button is "Next".

Logical meaning: The user wishes to return to the previous input source in the group, e.g., a form with multiple [TextField]s.

Moves the focus to the previous focusable item in the same [FocusScope].

Android: Corresponds to Android's "IME_ACTION_PREVIOUS". The OS displays a button that represents moving backward, e.g., a left-facing arrow button.

iOS: iOS does not have a keyboard return type of "previous." It is inappropriate to choose this [TextInputAction] when running on iOS.

Logical meaning: In iOS apps, it is common for a "Back" button and "Continue" button to appear at the top of the screen. However, when the keyboard is open, these buttons are often hidden off-screen. Therefore, the purpose of the "Continue" return key on iOS is to make the "Continue" button available when the user is entering text.

Historical context aside, [TextInputAction.continueAction] can be used any time that the term "Continue" seems most appropriate for the given action.

Android: Android does not have an IME input type of "continue." It is inappropriate to choose this [TextInputAction] when running on Android.

iOS: Corresponds to iOS's "UIReturnKeyContinue". The title displayed in the action button is "Continue". This action is only available on iOS 9.0+.

The reason that this value has "Action" post-fixed to it is because "continue" is a reserved word in Dart, as well as many other languages.

Logical meaning: The user wants to join something, e.g., a wireless network.

Android: Android does not have an IME input type of "join." It is inappropriate to choose this [TextInputAction] when running on Android.

iOS: Corresponds to iOS's "UIReturnKeyJoin". The title displayed in the action button is "Join".

Logical meaning: The user wants routing options, e.g., driving directions.

Android: Android does not have an IME input type of "route." It is inappropriate to choose this [TextInputAction] when running on Android.

iOS: Corresponds to iOS's "UIReturnKeyRoute". The title displayed in the action button is "Route".

Logical meaning: Initiate a call to emergency services.

Android: Android does not have an IME input type of "emergencyCall." It is inappropriate to choose this [TextInputAction] when running on Android.

iOS: Corresponds to iOS's "UIReturnKeyEmergencyCall". The title displayed in the action button is "Emergency Call".

Logical meaning: Insert a newline character in the focused text input, e.g., [TextField].

Android: Corresponds to Android's "IME_ACTION_NONE". The OS displays a button that represents a new line, e.g., a carriage return button.

iOS: Corresponds to iOS's "UIReturnKeyDefault". The title displayed in the action button is "return".

The term [TextInputAction.newline] exists in Flutter but not in Android or iOS. The reason for introducing this term is so that developers can achieve the common result of inserting new lines without needing to understand the various IME actions on Android and return keys on iOS. Thus, [TextInputAction.newline] is a convenience term that alleviates the need to understand the underlying platforms to achieve this common behavior.

# TextCapitalization

```dart
enum TextCapitalization {}
```

Configures how the platform keyboard will select an uppercase or lowercase keyboard.

Only supports text keyboards, other keyboard types will ignore this configuration. Capitalization is locale-aware.

Defaults to an uppercase keyboard for the first letter of each word.

Corresponds to `InputType.TYPE_TEXT_FLAG_CAP_WORDS` on Android, and `UITextAutocapitalizationTypeWords` on iOS.

Defaults to an uppercase keyboard for the first letter of each sentence.

Corresponds to `InputType.TYPE_TEXT_FLAG_CAP_SENTENCES` on Android, and `UITextAutocapitalizationTypeSentences` on iOS.

Defaults to an uppercase keyboard for each character.

Corresponds to `InputType.TYPE_TEXT_FLAG_CAP_CHARACTERS` on Android, and `UITextAutocapitalizationTypeAllCharacters` on iOS.

Defaults to a lowercase keyboard.

# TextInputConfiguration

```dart
class TextInputConfiguration {}
```

Controls the visual appearance of the text input control.

Many [TextInputAction]s are common between Android and iOS. However, if an [inputAction] is provided that is not supported by the current platform in debug mode, an error will be thrown when the corresponding text input is attached. For example, providing iOS's "emergencyCall" action when running on an Android device will result in an error when in debug mode. In release mode, incompatible [TextInputAction]s are replaced either with "unspecified" on Android, or "default" on iOS. Appropriate [inputAction]s can be chosen by checking the current platform and then selecting the appropriate action.

See also:

- [TextInput.attach]
- [TextInputAction]

### TextInputConfiguration()

```dart
TextInputConfiguration({int? viewId, TextInputType inputType = TextInputType.text, bool readOnly = false, bool obscureText = false, bool autocorrect = true, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool enableSuggestions = true, bool enableInteractiveSelection = true, String? actionLabel, TextInputAction inputAction = TextInputAction.done, Brightness keyboardAppearance = Brightness.light, TextCapitalization textCapitalization = TextCapitalization.none, AutofillConfiguration autofillConfiguration = AutofillConfiguration.disabled, bool enableIMEPersonalizedLearning = true, List<String> allowedMimeTypes = const <String>[], bool enableDeltaModel = false, List<Locale>? hintLocales = const <Locale>[], bool? enableInlinePrediction})
```

Creates configuration information for a text input control.

All arguments have default values, except [actionLabel]. Only [actionLabel] may be null.

### viewId

```dart
int? viewId
```

The ID of the view that the text input belongs to.

See also:

- [FlutterView], which is the view that the ID points to.
- [View], which is a widget that wraps a [FlutterView].

### inputType

```dart
TextInputType inputType
```

The type of information for which to optimize the text input control.

### readOnly

```dart
bool readOnly
```

Whether the text field can be edited or not.

Defaults to false.

### obscureText

```dart
bool obscureText
```

Whether to hide the text being edited (e.g., for passwords).

Defaults to false.

### autocorrect

```dart
bool autocorrect
```

Whether to enable autocorrection.

Defaults to true.

### autofillConfiguration

```dart
AutofillConfiguration autofillConfiguration
```

The configuration to use for autofill.

Defaults to null, in which case no autofill information will be provided to the platform. This will prevent the corresponding input field from participating in autofills triggered by other fields. Additionally, on Android and web, setting [autofillConfiguration] to null disables autofill.

### smartDashesType

```dart
SmartDashesType smartDashesType
```

{@template flutter.services.TextInputConfiguration.smartDashesType} Whether to allow the platform to automatically format dashes.

This flag only affects iOS versions 11 and above. It sets [`UITextSmartDashesType`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype?language=objc) in the engine. When true, it passes [`UITextSmartDashesTypeYes`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/uitextsmartdashestypeyes?language=objc), and when false, it passes [`UITextSmartDashesTypeNo`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/uitextsmartdashestypeno?language=objc).

As an example of what this does, two consecutive hyphen characters will be automatically replaced with one en dash, and three consecutive hyphens will become one em dash.

Defaults to true, unless [obscureText] is true, when it defaults to false. This is to avoid the problem where password fields receive autoformatted characters.

See also:

- [smartQuotesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits> {@endtemplate}

### smartQuotesType

```dart
SmartQuotesType smartQuotesType
```

{@template flutter.services.TextInputConfiguration.smartQuotesType} Whether to allow the platform to automatically format quotes.

This flag only affects iOS. It sets [`UITextSmartQuotesType`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype?language=objc) in the engine. When true, it passes [`UITextSmartQuotesTypeYes`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/uitextsmartquotestypeyes?language=objc), and when false, it passes [`UITextSmartQuotesTypeNo`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/uitextsmartquotestypeno?language=objc).

As an example of what this does, a standard vertical double quote character will be automatically replaced by a left or right double quote depending on its position in a word.

Defaults to true, unless [obscureText] is true, when it defaults to false. This is to avoid the problem where password fields receive autoformatted characters.

See also:

- [smartDashesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits> {@endtemplate}

### enableSuggestions

```dart
bool enableSuggestions
```

{@template flutter.services.TextInputConfiguration.enableSuggestions} Whether to show input suggestions as the user types.

This flag only affects Android. On iOS, suggestions are tied directly to [autocorrect], so that suggestions are only shown when [autocorrect] is true. On Android autocorrection and suggestion are controlled separately.

Defaults to true.

See also:

- <https://developer.android.com/reference/android/text/InputType.html#TYPE_TEXT_FLAG_NO_SUGGESTIONS> {@endtemplate}

### enableInteractiveSelection

```dart
bool enableInteractiveSelection
```

Whether a user can change its selection.

This flag only affects iOS VoiceOver. On Android Talkback, the selection change is sent through semantics actions and is directly disabled from the widget side.

Defaults to true.

### actionLabel

```dart
String? actionLabel
```

What text to display in the text input control's action button.

### inputAction

```dart
TextInputAction inputAction
```

What kind of action to request for the action button on the IME.

### textCapitalization

```dart
TextCapitalization textCapitalization
```

Specifies how platforms may automatically capitalize text entered by the user.

Defaults to [TextCapitalization.none].

See also:

- [TextCapitalization], for a description of each capitalization behavior.

### keyboardAppearance

```dart
Brightness keyboardAppearance
```

The appearance of the keyboard.

This setting is only honored on iOS devices.

Defaults to [Brightness.light].

### enableIMEPersonalizedLearning

```dart
bool enableIMEPersonalizedLearning
```

{@template flutter.services.TextInputConfiguration.enableIMEPersonalizedLearning} Whether to enable that the IME update personalized data such as typing history and user dictionary data.

This flag only affects Android. On iOS, there is no equivalent flag.

Defaults to true.

See also:

- <https://developer.android.com/reference/android/view/inputmethod/EditorInfo#IME_FLAG_NO_PERSONALIZED_LEARNING> {@endtemplate}

### allowedMimeTypes

```dart
List<String> allowedMimeTypes
```

{@macro flutter.widgets.contentInsertionConfiguration.allowedMimeTypes}

### hintLocales

```dart
List<Locale>? hintLocales
```

{@template flutter.services.TextInputConfiguration.hintLocales} List of the languages that the user is expected to use.

This special "hint" can be used mainly for, but not limited to, multilingual users who want IMEs to switch language based on editor's context.

Pass an empty list to express the intention that a specific hint should not be set.

Defaults to null, which indicates no preference in keyboard language.

This setting is only honored on Android devices running API 24 and above.

See also:

- <https://developer.android.com/reference/android/view/inputmethod/EditorInfo#hintLocales> {@endtemplate}

### enableInlinePrediction

```dart
bool? enableInlinePrediction
```

{@template flutter.services.TextInputConfiguration.enableInlinePrediction} Whether to enable inline predictive text.

This feature is specific to iOS 17 and later. It has no effect on other platforms.

By default, this property is null, which means inline prediction is disabled on iOS. Setting this flag overrides the platform behavior: when true, inline prediction is enabled; when false, it is disabled. {@endtemplate}

### copyWith()

```dart
TextInputConfiguration copyWith({int? viewId, TextInputType? inputType, bool? readOnly, bool? obscureText, bool? autocorrect, SmartDashesType? smartDashesType, SmartQuotesType? smartQuotesType, bool? enableSuggestions, bool? enableInteractiveSelection, String? actionLabel, TextInputAction? inputAction, Brightness? keyboardAppearance, TextCapitalization? textCapitalization, bool? enableIMEPersonalizedLearning, List<String>? allowedMimeTypes, AutofillConfiguration? autofillConfiguration, bool? enableDeltaModel, List<Locale>? hintLocales, bool? enableInlinePrediction})
```

Creates a copy of this [TextInputConfiguration] with the given fields replaced with new values.

### enableDeltaModel

```dart
bool enableDeltaModel
```

Whether to enable that the engine sends text input updates to the framework as [TextEditingDelta]'s or as one [TextEditingValue].

Enabling this flag results in granular text updates being received from the platform's text input control.

When this is enabled:

- You must implement [DeltaTextInputClient] and not [TextInputClient] to receive granular updates from the platform's text input.
- Platform text input updates will come through [DeltaTextInputClient.updateEditingValueWithDeltas].
- If [TextInputClient] is implemented with this property enabled then you will experience unexpected behavior as [TextInputClient] does not implement a delta channel.

When this is disabled:

- If [DeltaTextInputClient] is implemented then updates for the editing state will continue to come through the [DeltaTextInputClient.updateEditingValue] channel.
- If [TextInputClient] is implemented then updates for the editing state will come through [TextInputClient.updateEditingValue].

Defaults to false.

### toJson()

```dart
Map<String, dynamic> toJson()
```

Returns a representation of this object as a JSON object.

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

# FloatingCursorDragState

```dart
enum FloatingCursorDragState {}
```

The state of a "floating cursor" drag on an iOS soft keyboard.

The "floating cursor" cursor-positioning mode is an iOS feature used to precisely position the caret in some editable text using certain touch gestures. As an example, when the user long-presses the spacebar on the iOS virtual keyboard, iOS enters floating cursor mode where the whole keyboard becomes a trackpad. In this mode, there are two visible cursors. One, the floating cursor, hovers over the text, following the user's horizontal movements exactly and snapping to lines vertically. The other, the placeholder cursor, is a "shadow" that also snaps to the actual location where the cursor will go horizontally when the user releases the trackpad.

The floating cursor renders over the text field, while the placeholder cursor is a faint shadow of the cursor rendered in the text field in the location between characters where the cursor will drop into when released. The placeholder cursor is a faint vertical bar, while the floating cursor has the same appearance as a normal cursor (a blue vertical bar).

This feature works out-of-the-box with Flutter. Support is built into [EditableText].

See also:

- [EditableText.backgroundCursorColor], which configures the color of the placeholder cursor while the floating cursor is being dragged.

A user has just activated a floating cursor by long pressing on the spacebar.

A user is dragging a floating cursor.

A user has lifted their finger off the screen after using a floating cursor.

# RawFloatingCursorPoint

```dart
class RawFloatingCursorPoint {}
```

The current state and position of the floating cursor.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### RawFloatingCursorPoint()

```dart
RawFloatingCursorPoint({Offset? offset, (Offset, TextPosition)? startLocation, required FloatingCursorDragState state})
```

Creates information for setting the position and state of a floating cursor.

[state] must not be null and [offset] must not be null if the state is [FloatingCursorDragState.Update].

### offset

```dart
Offset? offset
```

The raw position of the floating cursor as determined by the iOS sdk.

### startLocation

```dart
(Offset, TextPosition)? startLocation
```

Represents the starting location when initiating a floating cursor via long press. This is a tuple where the first item is the local offset and the second item is the new caret position. This is only non-null when a floating cursor is started.

### state

```dart
FloatingCursorDragState state
```

The state of the floating cursor.

# TextEditingValue

```dart
class TextEditingValue {}
```

The current text, selection, and composing state for editing a run of text.

### TextEditingValue()

```dart
TextEditingValue({String text = '', TextSelection selection = const TextSelection.collapsed(offset: -1), TextRange composing = TextRange.empty})
```

Creates information for editing a run of text.

The selection and composing range must be within the text. This is not checked during construction, and must be guaranteed by the caller.

The default value of [selection] is `TextSelection.collapsed(offset: -1)`. This indicates that there is no selection at all.

### TextEditingValue.fromJSON()

```dart
TextEditingValue.fromJSON(Map<String, dynamic> encoded)
```

Creates an instance of this class from a JSON object.

### text

```dart
String text
```

The current text being edited.

### selection

```dart
TextSelection selection
```

The range of text that is currently selected.

When [selection] is a [TextSelection] that has the same non-negative `baseOffset` and `extentOffset`, the [selection] property represents the caret position.

If the current [selection] has a negative `baseOffset` or `extentOffset`, then the text currently does not have a selection or a caret location, and most text editing operations that rely on the current selection (for instance, insert a character at the caret location) will do nothing.

### composing

```dart
TextRange composing
```

The range of text that is still being composed.

Composing regions are created by input methods (IMEs) to indicate the text within a certain range is provisional. For instance, the Android Gboard app's English keyboard puts the current word under the caret into a composing region to indicate the word is subject to autocorrect or prediction changes.

Composing regions can also be used for performing multistage input, which is typically used by IMEs designed for phonetic keyboard to enter ideographic symbols. As an example, many CJK keyboards require the user to enter a Latin alphabet sequence and then convert it to CJK characters. On iOS, the default software keyboards do not have a dedicated view to show the unfinished Latin sequence, so it's displayed directly in the text field, inside of a composing region.

On iOS 17 and later, the composing region can also be used to display inline text predictions. The user can accept the predicted text by tapping the Space bar.

The composing region should typically only be changed by the IME, or the user via interacting with the IME.

If the range represented by this property is [TextRange.empty], then the text is not currently being composed.

### empty

```dart
TextEditingValue empty
```

A value that corresponds to the empty string with no selection and no composing range.

### copyWith()

```dart
TextEditingValue copyWith({String? text, TextSelection? selection, TextRange? composing})
```

Creates a copy of this value but with the given fields replaced with the new values.

### isComposingRangeValid

```dart
bool get isComposingRangeValid
```

Whether the [composing] range is a valid range within [text].

Returns true if and only if the [composing] range is normalized, its start is greater than or equal to 0, and its end is less than or equal to [text]'s length.

If this property is false while the [composing] range's `isValid` is true, it usually indicates the current [composing] range is invalid because of a programming error.

### replaced()

```dart
TextEditingValue replaced(TextRange replacementRange, String replacementString)
```

Returns a new [TextEditingValue], which is this [TextEditingValue] with its [text] partially replaced by the `replacementString`.

The `replacementRange` parameter specifies the range of the [TextEditingValue.text] that needs to be replaced.

The `replacementString` parameter specifies the string to replace the given range of text with.

This method also adjusts the selection range and the composing range of the resulting [TextEditingValue], such that they point to the same substrings as the corresponding ranges in the original [TextEditingValue]. For example, if the original [TextEditingValue] is "Hello world" with the word "world" selected, replacing "Hello" with a different string using this method will not change the selected word.

This method does nothing if the given `replacementRange` is not [TextRange.isValid].

### toJSON()

```dart
Map<String, dynamic> toJSON()
```

Returns a representation of this object as a JSON object.

### toString()

```dart
String toString()
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

# SelectionChangedCause

```dart
enum SelectionChangedCause {}
```

Indicates what triggered the change in selected text (including changes to the cursor location).

The user tapped on the text and that caused the selection (or the location of the cursor) to change.

The user tapped twice in quick succession on the text and that caused the selection (or the location of the cursor) to change.

The user long-pressed the text and that caused the selection (or the location of the cursor) to change.

The user force-pressed the text and that caused the selection (or the location of the cursor) to change.

The user used the keyboard to change the selection or the location of the cursor.

Keyboard-triggered selection changes may be caused by the IME as well as by accessibility tools (e.g. TalkBack on Android).

The user used the selection toolbar to change the selection or the location of the cursor.

An example is when the user taps on select all in the tool bar.

The user used the mouse to change the selection by dragging over a piece of text.

The user used stylus handwriting to change the selection.

Currently, this is only supported on iPadOS 14+ via the Scribble feature, or on Android API 34+ via the Scribe feature.

### scribble

```dart
SelectionChangedCause scribble
```

The user used stylus handwriting to change the selection.

Currently, this is only supported on iPadOS 14+ via the Scribble feature, or on Android API 34+ via the Scribe feature.

# TextSelectionDelegate

```dart
mixin TextSelectionDelegate {}
```

A mixin for manipulating the selection, provided for toolbar or shortcut keys.

### textEditingValue

```dart
TextEditingValue get textEditingValue
```

Gets the current text input.

### userUpdateTextEditingValue()

```dart
void userUpdateTextEditingValue(TextEditingValue value, SelectionChangedCause cause)
```

Indicates that the user has requested the delegate to replace its current text editing state with [value].

The new [value] is treated as user input and thus may subject to input formatting.

See also:

- [EditableTextState.userUpdateTextEditingValue]: an implementation that applies additional pre-processing to the specified [value], before updating the text editing state.

### hideToolbar()

```dart
void hideToolbar([bool hideHandles = true])
```

Hides the text selection toolbar.

By default, hideHandles is true, and the toolbar is hidden along with its handles. If hideHandles is set to false, then the toolbar will be hidden but the handles will remain.

### bringIntoView()

```dart
void bringIntoView(TextPosition position)
```

Brings the provided [TextPosition] into the visible area of the text input.

### cutEnabled

```dart
bool get cutEnabled
```

Whether cut is enabled.

### copyEnabled

```dart
bool get copyEnabled
```

Whether copy is enabled.

### pasteEnabled

```dart
bool get pasteEnabled
```

Whether paste is enabled.

### selectAllEnabled

```dart
bool get selectAllEnabled
```

Whether select all is enabled.

### lookUpEnabled

```dart
bool get lookUpEnabled
```

Whether look up is enabled.

### searchWebEnabled

```dart
bool get searchWebEnabled
```

Whether search web is enabled.

### shareEnabled

```dart
bool get shareEnabled
```

Whether share is enabled.

### liveTextInputEnabled

```dart
bool get liveTextInputEnabled
```

Whether Live Text input is enabled.

See also:

- [LiveText], where the availability of Live Text input can be obtained.
- [LiveTextInputStatusNotifier], where the status of Live Text can be listened to.

### cutSelection()

```dart
void cutSelection(SelectionChangedCause cause)
```

Cut current selection to [Clipboard].

If and only if [cause] is [SelectionChangedCause.toolbar], the toolbar will be hidden and the current selection will be scrolled into view.

### pasteText()

```dart
Future<void> pasteText(SelectionChangedCause cause)
```

Paste text from [Clipboard].

If there is currently a selection, it will be replaced.

If and only if [cause] is [SelectionChangedCause.toolbar], the toolbar will be hidden and the current selection will be scrolled into view.

### selectAll()

```dart
void selectAll(SelectionChangedCause cause)
```

Set the current selection to contain the entire text value.

If and only if [cause] is [SelectionChangedCause.toolbar], the selection will be scrolled into view.

### copySelection()

```dart
void copySelection(SelectionChangedCause cause)
```

Copy current selection to [Clipboard].

If [cause] is [SelectionChangedCause.toolbar], the position of [bringIntoView] to selection will be called and hide toolbar.

# TextInputClient

```dart
mixin TextInputClient {}
```

An interface to receive information from [TextInput].

If [TextInputConfiguration.enableDeltaModel] is set to true, [DeltaTextInputClient] must be implemented instead of this class.

See also:

- [TextInput.attach]
- [EditableText], a [TextInputClient] implementation.
- [DeltaTextInputClient], a [TextInputClient] extension that receives granular information from the platform's text input.

### currentTextEditingValue

```dart
TextEditingValue? get currentTextEditingValue
```

The current state of the [TextEditingValue] held by this client.

### currentAutofillScope

```dart
AutofillScope? get currentAutofillScope
```

The [AutofillScope] this [TextInputClient] belongs to, if any.

It should return null if this [TextInputClient] does not need autofill support. For a [TextInputClient] that supports autofill, returning null causes it to participate in autofill alone.

See also:

- [AutofillGroup], a widget that creates an [AutofillScope] for its descendent autofillable [TextInputClient]s.

### updateEditingValue()

```dart
void updateEditingValue(TextEditingValue value)
```

Requests that this client update its editing state to the given value.

The new [value] is treated as user input and thus may subject to input formatting.

### performAction()

```dart
void performAction(TextInputAction action)
```

Requests that this client perform the given action.

### insertContent()

```dart
void insertContent(KeyboardInsertedContent content)
```

Notify client about new content insertion from Android keyboard.

### performPrivateCommand()

```dart
void performPrivateCommand(String action, Map<String, dynamic> data)
```

Request from the input method that this client perform the given private command.

This can be used to provide domain-specific features that are only known between certain input methods and their clients.

See also:

- [performPrivateCommand](<https://developer.android.com/reference/android/view/inputmethod/InputConnection#performPrivateCommand(java.lang.String,%20android.os.Bundle)>), which is the Android documentation for performPrivateCommand, used to send a command from the input method.
- [sendAppPrivateCommand](https://developer.android.com/reference/android/view/inputmethod/InputMethodManager#sendAppPrivateCommand), which is the Android documentation for sendAppPrivateCommand, used to send a command to the input method.

### updateFloatingCursor()

```dart
void updateFloatingCursor(RawFloatingCursorPoint point)
```

Updates the floating cursor position and state.

See also:

- [FloatingCursorDragState], which explains the floating cursor feature in detail.

### showAutocorrectionPromptRect()

```dart
void showAutocorrectionPromptRect(int start, int end)
```

Requests that this client display a prompt rectangle for the given text range, to indicate the range of text that will be changed by a pending autocorrection.

This method will only be called on iOS.

### onFocusReceived()

```dart
bool onFocusReceived()
```

Notifies the client that the platform moved focus back to this input.

This is necessary to support autofill on some browsers (e.g. iOS Safari) that blur the text field and refocus it before autofilling.

Returns true if the client acquired focus, false otherwise.

### connectionClosed()

```dart
void connectionClosed()
```

Platform notified framework of closed connection.

[TextInputClient] should cleanup its connection and finalize editing.

### didChangeInputControl()

```dart
void didChangeInputControl(TextInputControl? oldControl, TextInputControl? newControl)
```

The framework calls this method to notify that the text input control has been changed.

The [TextInputClient] may switch to the new text input control by hiding the old and showing the new input control.

See also:

- [TextInputControl.hide], a method to hide the old input control.
- [TextInputControl.show], a method to show the new input control.

### showToolbar()

```dart
void showToolbar()
```

Requests that the client show the editing toolbar, for example when the platform changes the selection through a non-flutter method such as scribble.

### insertTextPlaceholder()

```dart
void insertTextPlaceholder(Size size)
```

Requests that the client add a text placeholder to reserve visual space in the text.

For example, this is called when responding to UIKit requesting a text placeholder be added at the current selection, such as when requesting additional writing space with iPadOS14 Scribble.

### removeTextPlaceholder()

```dart
void removeTextPlaceholder()
```

Requests that the client remove the text placeholder.

### performSelector()

```dart
void performSelector(String selectorName)
```

Performs the specified MacOS-specific selector from the `NSStandardKeyBindingResponding` protocol or user-specified selector from `DefaultKeyBinding.Dict`.

# ScribbleClient

```dart
abstract class ScribbleClient {}
```

An interface into iOS's stylus handwriting text input.

See also:

- [Scribe], which provides similar functionality for Android.
- [UIIndirectScribbleInteraction](https://developer.apple.com/documentation/uikit/uiindirectscribbleinteraction), which is iOS's API for Scribble.

### elementIdentifier

```dart
String get elementIdentifier
```

A unique identifier for this element.

### onScribbleFocus()

```dart
void onScribbleFocus(Offset offset)
```

Called by the engine when the [ScribbleClient] should receive focus.

For example, this method is called during a UIIndirectScribbleInteraction.

### isInScribbleRect()

```dart
bool isInScribbleRect(Rect rect)
```

Tests whether the [ScribbleClient] overlaps the given rectangle bounds.

### bounds

```dart
Rect get bounds
```

The current bounds of the [ScribbleClient].

# SelectionRect

```dart
class SelectionRect {}
```

Represents a selection rect for a character and it's position in the text.

This is used to report the current text selection rect and position data to the engine for Scribble support on iPadOS 14.

### SelectionRect()

```dart
SelectionRect({required int position, required Rect bounds, TextDirection direction = TextDirection.ltr})
```

Constructor for creating a [SelectionRect] from a text [position] and [bounds].

### position

```dart
int position
```

The position of this selection rect within the text String.

### bounds

```dart
Rect bounds
```

The rectangle representing the bounds of this selection rect within the currently focused [RenderEditable]'s coordinate space.

### direction

```dart
TextDirection direction
```

The direction text flows within this selection rect.

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

# DeltaTextInputClient

```dart
mixin DeltaTextInputClient implements TextInputClient {}
```

An interface to receive granular information from [TextInput].

See also:

- [TextInput.attach]
- [TextInputConfiguration], to opt-in to receive [TextEditingDelta]'s from the platforms [TextInput] you must set [TextInputConfiguration.enableDeltaModel] to true.

### updateEditingValueWithDeltas()

```dart
void updateEditingValueWithDeltas(List<TextEditingDelta> textEditingDeltas)
```

Requests that this client update its editing state by applying the deltas received from the engine.

The list of [TextEditingDelta]'s are treated as changes that will be applied to the client's editing state. A change is any mutation to the raw text value, or any updates to the selection and/or composing region.

{@tool snippet} This example shows what an implementation of this method could look like.

```dart
class MyClient with DeltaTextInputClient {
  TextEditingValue? _localValue;

  @override
  void updateEditingValueWithDeltas(List<TextEditingDelta> textEditingDeltas) {
    if (_localValue == null) {
      return;
    }
    TextEditingValue newValue = _localValue!;
    for (final TextEditingDelta delta in textEditingDeltas) {
      newValue = delta.apply(newValue);
    }
    _localValue = newValue;
  }

  // ...
}
```

{@end-tool}

# TextInputStyle

```dart
final class TextInputStyle with Diagnosticable {}
```

Text styling information for the current input client.

See also:

- [TextInputConnection.updateStyle], which uses this class to send style information to the platform.
- [TextInputControl.updateStyle], which receives this style information in custom text input controls.

### TextInputStyle()

```dart
TextInputStyle({String? fontFamily, double? fontSize, FontWeight? fontWeight, required TextDirection textDirection, required TextAlign textAlign, double? letterSpacing, double? wordSpacing, double? lineHeight})
```

Creates text styling information for the current input client.

### fontFamily

```dart
String? fontFamily
```

The name of the font to use when painting the text (e.g., Roboto).

### fontSize

```dart
double? fontSize
```

The size of fonts (in logical pixels) to use when painting the text.

### fontWeight

```dart
FontWeight? fontWeight
```

The typeface thickness to use when painting the text (e.g., bold).

### textDirection

```dart
TextDirection textDirection
```

The directionality of the text.

### textAlign

```dart
TextAlign textAlign
```

How the text should be aligned horizontally.

### letterSpacing

```dart
double? letterSpacing
```

The amount of space (in logical pixels) to add between each letter.

### wordSpacing

```dart
double? wordSpacing
```

The amount of space (in logical pixels) to add at each sequence of white-space (i.e. between each word).

### lineHeight

```dart
double? lineHeight
```

The line height in logical pixels.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toJson()

```dart
Map<String, dynamic> toJson()
```

Returns a representation of this object as a JSON object.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# TextInputConnection

```dart
class TextInputConnection {}
```

An interface for interacting with a text input control.

See also:

- [TextInput.attach], a method used to establish a [TextInputConnection] between the system's text input and a [TextInputClient].
- [EditableText], a [TextInputClient] that connects to and interacts with the system's text input using a [TextInputConnection].

### debugResetId()

```dart
void debugResetId({int to = 1})
```

Resets the internal ID counter for testing purposes.

This call has no effect when asserts are disabled. Calling it from application code will likely break text input for the application.

### attached

```dart
bool get attached
```

Whether this connection is currently interacting with the text input control.

### scribbleInProgress

```dart
bool get scribbleInProgress
```

Whether there is currently a Scribble interaction in progress.

This is used to make sure selection handles are shown when UIKit changes the selection during a Scribble interaction.

### show()

```dart
void show()
```

Requests that the text input control become visible.

### requestAutofill()

```dart
void requestAutofill()
```

Requests the system autofill UI to appear.

Currently only works on Android. Other platforms do not respond to this message.

See also:

- [EditableText], a [TextInputClient] that calls this method when focused.

### updateConfig()

```dart
void updateConfig(TextInputConfiguration configuration)
```

Requests that the text input control update itself according to the new [TextInputConfiguration].

### setEditingState()

```dart
void setEditingState(TextEditingValue value)
```

Requests that the text input control change its internal state to match the given state.

### setEditableSizeAndTransform()

```dart
void setEditableSizeAndTransform(Size editableBoxSize, Matrix4 transform)
```

Send the size and transform of the editable text to engine.

The values are sent as platform messages so they can be used on web for example to correctly position and size the html input field.

1.  [editableBoxSize]: size of the render editable box.

2.  [transform]: a matrix that maps the local paint coordinate system to the [PipelineOwner.rootNode].

### setComposingRect()

```dart
void setComposingRect(Rect rect)
```

Send the smallest rect that covers the text in the client that's currently being composed.

If any of the 4 coordinates of the given [Rect] is not finite, a [Rect] of size (-1, -1) will be sent instead.

This information is used for positioning the IME candidates menu on each platform.

### setCaretRect()

```dart
void setCaretRect(Rect rect)
```

Sends the coordinates of caret rect. This is used on macOS for positioning the accent selection menu.

### setSelectionRects()

```dart
void setSelectionRects(List<SelectionRect> selectionRects)
```

Send the bounding boxes of the current selected glyphs in the client to the platform's text input plugin.

These are used by the engine during a UIDirectScribbleInteraction.

### setStyle()

```dart
void setStyle({required String? fontFamily, required double? fontSize, required FontWeight? fontWeight, required TextDirection textDirection, required TextAlign textAlign})
```

Send text styling information.

This information is used by the Flutter Web Engine to change the style of the hidden native input's content. Hence, the content size will match to the size of the editable widget's content.

### updateStyle()

```dart
void updateStyle(TextInputStyle style)
```

Send text styling information.

This information is used by the Flutter Web Engine to change the style of the hidden native input's content. Hence, the content size will match to the size of the editable widget's content.

### close()

```dart
void close()
```

Stop interacting with the text input control.

After calling this method, the text input control might disappear if no other client attaches to it within this animation frame.

### connectionClosedReceived()

```dart
void connectionClosedReceived()
```

Platform sent a notification informing the connection is closed.

[TextInputConnection] should clean current client connection.

# TextInput

```dart
class TextInput {}
```

An low-level interface to the system's text input control.

To start interacting with the system's text input control, call [attach] to establish a [TextInputConnection] between the system's text input control and a [TextInputClient]. The majority of commands available for interacting with the text input control reside in the returned [TextInputConnection]. The communication between the system text input and the [TextInputClient] is asynchronous.

The platform text input plugin (which represents the system's text input) and the [TextInputClient] usually maintain their own text editing states ([TextEditingValue]) separately. They must be kept in sync as long as the [TextInputClient] is connected. The following methods can be used to send [TextEditingValue] to update the other party, when either party's text editing states change:

- The [TextInput.attach] method allows a [TextInputClient] to establish a connection to the text input. An optional field in its `configuration` parameter can be used to specify an initial value for the platform text input plugin's [TextEditingValue].

- The [TextInputClient] sends its [TextEditingValue] to the platform text input plugin using [TextInputConnection.setEditingState].

- The platform text input plugin sends its [TextEditingValue] to the connected [TextInputClient] via a "TextInput.setEditingState" message.

- When autofill happens on a disconnected [TextInputClient], the platform text input plugin sends the [TextEditingValue] to the connected [TextInputClient]'s [AutofillScope], and the [AutofillScope] will further relay the value to the correct [TextInputClient].

When synchronizing the [TextEditingValue]s, the communication may get stuck in an infinite when both parties are trying to send their own update. To mitigate the problem, only [TextInputClient]s are allowed to alter the received [TextEditingValue]s while platform text input plugins are to accept the received [TextEditingValue]s unmodified. More specifically:

- When a [TextInputClient] receives a new [TextEditingValue] from the platform text input plugin, it's allowed to modify the value (for example, apply [TextInputFormatter]s). If it decides to do so, it must send the updated [TextEditingValue] back to the platform text input plugin to keep the [TextEditingValue]s in sync.

- When the platform text input plugin receives a new value from the connected [TextInputClient], it must accept the new value as-is, to avoid sending back an updated value.

See also:

- [TextField], a widget in which the user may enter text.
- [EditableText], a [TextInputClient] that connects to [TextInput] when it wants to take user input from the keyboard.

### setChannel()

```dart
void setChannel(MethodChannel newChannel)
```

Set the [MethodChannel] used to communicate with the system's text input control.

This is only meant for testing within the Flutter SDK. Changing this will break the ability to input text. This has no effect if asserts are disabled.

### setInputControl()

```dart
void setInputControl(TextInputControl? newControl)
```

Sets the current text input control.

The current text input control receives text input state changes and visual text input control requests, such as showing and hiding the input control, from the framework.

Setting the current text input control as `null` removes the visual text input control.

See also:

- [TextInputControl], an interface for implementing text input controls.
- [TextInput.restorePlatformInputControl], a method to restore the default platform text input control.

### restorePlatformInputControl()

```dart
void restorePlatformInputControl()
```

Restores the default platform text input control.

See also:

- [TextInput.setInputControl], a method to set a custom input control, or to remove the visual input control.

### ensureInitialized()

```dart
void ensureInitialized()
```

Ensure that a [TextInput] instance has been set up so that the platform can handle messages on the text input method channel.

### attach()

```dart
TextInputConnection attach(TextInputClient client, TextInputConfiguration configuration)
```

Begin interacting with the text input control.

Calling this function helps multiple clients coordinate about which one is currently interacting with the text input control. The returned [TextInputConnection] provides an interface for actually interacting with the text input control.

A client that no longer wishes to interact with the text input control should call [TextInputConnection.close] on the returned [TextInputConnection].

### scribbleClients

```dart
Map<String, ScribbleClient> get scribbleClients
```

Used for testing within the Flutter SDK to get the currently registered [ScribbleClient] list.

### scribbleInProgress

```dart
bool get scribbleInProgress
```

Returns true if a scribble interaction is currently happening.

### updateEditingValue()

```dart
void updateEditingValue(TextEditingValue value)
```

Updates the editing value of the attached input client.

This method should be called by the text input control implementation to send editing value updates to the attached input client.

### finishAutofillContext()

```dart
void finishAutofillContext({bool shouldSave = true})
```

Finishes the current autofill context, and potentially saves the user input for future use if `shouldSave` is true.

Typically, this method should be called when the user has finalized their input. For example, in a [Form], it's typically done immediately before or after its content is submitted.

The topmost [AutofillGroup]s also call [finishAutofillContext] automatically when they are disposed. The default behavior can be overridden in [AutofillGroup.onDisposeAction].

{@template flutter.services.TextInput.finishAutofillContext} An autofill context is a collection of input fields that live in the platform's text input plugin. The platform is encouraged to save the user input stored in the current autofill context before the context is destroyed, when [TextInput.finishAutofillContext] is called with `shouldSave` set to true.

Currently, there can only be at most one autofill context at any given time. When any input field in an [AutofillGroup] requests for autofill (which is done automatically when an autofillable [EditableText] gains focus), the current autofill context will merge the content of that [AutofillGroup] into itself. When there isn't an existing autofill context, one will be created to hold the newly added input fields from the group.

Once added to an autofill context, an input field will stay in the context until the context is destroyed. To prevent leaks, call [TextInput.finishAutofillContext] to signal the text input plugin that the user has finalized their input in the current autofill context. The platform text input plugin either encourages or discourages the platform from saving the user input based on the value of the `shouldSave` parameter. The platform usually shows a "Save for autofill?" prompt for user confirmation. {@endtemplate}

On many platforms, calling [finishAutofillContext] shows the save user input dialog and disrupts the user's flow. Ideally the dialog should only be shown no more than once for every screen. Consider removing premature [finishAutofillContext] calls to prevent showing the save user input UI too frequently. However, calling [finishAutofillContext] when there's no existing autofill context usually does not bring up the save user input UI.

See also:

- [EditableText.autofillHints] for autofill save troubleshooting tips.
- [AutofillGroup.onDisposeAction], a configurable action that runs when a topmost [AutofillGroup] is getting disposed.

### registerScribbleElement()

```dart
void registerScribbleElement(String elementIdentifier, ScribbleClient scribbleClient)
```

Registers a [ScribbleClient] with [elementIdentifier] that can be focused by the engine.

For example, the registered [ScribbleClient] list is used to respond to UIIndirectScribbleInteraction on an iPad.

### unregisterScribbleElement()

```dart
void unregisterScribbleElement(String elementIdentifier)
```

Unregisters a [ScribbleClient] with [elementIdentifier].

# TextInputControl

```dart
mixin TextInputControl {}
```

An interface for implementing text input controls that receive text editing state changes and visual input control requests.

Editing state changes and input control requests are sent by the framework when the editing state of the attached text input client changes, or it requests the input control to be shown or hidden, for example.

The input control can be installed with [TextInput.setInputControl], and the default platform text input control can be restored with [TextInput.restorePlatformInputControl].

The [TextInputControl] class must be extended. [TextInputControl] implementations should call [TextInput.updateEditingValue] to send user input to the attached input client.

{@tool dartpad} This example illustrates a basic [TextInputControl] implementation.

** See code in examples/api/lib/services/text_input/text_input_control.0.dart ** {@end-tool}

See also:

- [TextInput.setInputControl], a method to install a custom text input control.
- [TextInput.restorePlatformInputControl], a method to restore the default platform text input control.
- [TextInput.updateEditingValue], a method to send user input to the framework.

### attach()

```dart
void attach(TextInputClient client, TextInputConfiguration configuration)
```

Requests the text input control to attach to the given input client.

This method is called when a text input client is attached. The input control should update its configuration to match the client's configuration.

### detach()

```dart
void detach(TextInputClient client)
```

Requests the text input control to detach from the given input client.

This method is called when a text input client is detached. The input control should release any resources allocated for the client.

### show()

```dart
void show()
```

Requests that the text input control is shown.

This method is called when the input control should become visible.

### hide()

```dart
void hide()
```

Requests that the text input control is hidden.

This method is called when the input control should hide.

### updateConfig()

```dart
void updateConfig(TextInputConfiguration configuration)
```

Informs the text input control about input configuration changes.

This method is called when the configuration of the attached input client has changed.

### setEditingState()

```dart
void setEditingState(TextEditingValue value)
```

Informs the text input control about editing state changes.

This method is called when the editing state of the attached input client has changed.

### setEditableSizeAndTransform()

```dart
void setEditableSizeAndTransform(Size editableBoxSize, Matrix4 transform)
```

Informs the text input control about client position changes.

This method is called on when the input control should position itself in relation to the attached input client.

### setComposingRect()

```dart
void setComposingRect(Rect rect)
```

Informs the text input control about composing area changes.

This method is called when the attached input client's composing area changes.

### setCaretRect()

```dart
void setCaretRect(Rect rect)
```

Informs the text input control about caret area changes.

This method is called when the attached input client's caret area changes.

### setSelectionRects()

```dart
void setSelectionRects(List<SelectionRect> selectionRects)
```

Informs the text input control about selection area changes.

This method is called when the attached input client's selection area changes.

### setStyle()

```dart
void setStyle({required String? fontFamily, required double? fontSize, required FontWeight? fontWeight, required TextDirection textDirection, required TextAlign textAlign})
```

Informs the text input control about text style changes.

This method is called on the when the attached input client's text style changes.

### updateStyle()

```dart
void updateStyle(TextInputStyle style)
```

Informs the text input control about text style changes.

This method is called on the when the attached input client's text style changes.

### requestAutofill()

```dart
void requestAutofill()
```

Requests autofill from the text input control.

This method is called when the autofill UI should appear.

### finishAutofillContext()

```dart
void finishAutofillContext({bool shouldSave = true})
```

Requests that the autofill context is finalized.

See also:

- [TextInput.finishAutofillContext]

# SystemContextMenuController

```dart
class SystemContextMenuController with SystemContextMenuClient, Diagnosticable {}
```

Allows access to the system context menu.

The context menu is the menu that appears, for example, when doing text selection. Flutter typically draws this menu itself, but this class deals with the platform-rendered context menu.

Only one instance can be visible at a time. Calling [show] while the system context menu is already visible will hide it and show it again at the new [Rect]. An instance that is hidden is informed via [onSystemHide].

Currently this system context menu is bound to text input. The buttons that are shown and the actions they perform are dependent on the currently active [TextInputConnection]. Using this without an active [TextInputConnection] is a noop.

Call [dispose] when no longer needed.

See also:

- [ContextMenuController], which controls Flutter-drawn context menus.
- [SystemContextMenu], which wraps this functionality in a widget.
- [MediaQuery.maybeSupportsShowingSystemContextMenu], which indicates whether the system context menu is supported.

### SystemContextMenuController()

```dart
SystemContextMenuController({VoidCallback? onSystemHide})
```

Creates an instance of [SystemContextMenuController].

Not shown until [show] is called.

### onSystemHide

```dart
VoidCallback? onSystemHide
```

Called when the system has hidden the context menu.

For example, tapping outside of the context menu typically causes the system to hide it directly. Flutter is made aware that the context menu is no longer visible through this callback.

This is not called when [show]ing a new system context menu causes another to be hidden.

### isVisible

```dart
bool get isVisible
```

Indicates whether the system context menu managed by this controller is currently being displayed to the user.

### handleSystemHide()

```dart
void handleSystemHide()
```

### handleCustomContextMenuAction()

```dart
void handleCustomContextMenuAction(String callbackId)
```

### show()

```dart
Future<void> show(Rect targetRect)
```

Shows the system context menu anchored on the given [Rect].

Currently only supported on iOS 16.0 and later. Check [MediaQuery.maybeSupportsShowingSystemContextMenu] before calling this.

The [Rect] represents what the context menu is pointing to. For example, for some text selection, this would be the selection [Rect].

Currently this system context menu is bound to text input. Using this without an active [TextInputConnection] will be a noop.

There can only be one system context menu visible at a time. Calling this while another system context menu is already visible will remove the old menu before showing the new menu.

See also:

- [hide], which hides the menu shown by this method.
- [MediaQuery.supportsShowingSystemContextMenu], which indicates whether this method is supported on the current platform.

### showWithItems()

```dart
Future<void> showWithItems(Rect targetRect, List<IOSSystemContextMenuItemData> items)
```

Shows the system context menu anchored on the given [Rect] with the given buttons.

Currently only supported on iOS 16.0 and later. Check [MediaQuery.maybeSupportsShowingSystemContextMenu] before calling this.

The [Rect] represents what the context menu is pointing to. For example, for some text selection, this would be the selection [Rect].

`items` specifies the buttons that appear in the menu. The buttons that appear in the menu will be exactly as given and will not automatically update based on the state of the input field. See [SystemContextMenu.getDefaultItems] for the default items for a given [EditableTextState].

Currently this system context menu is bound to text input. Using this without an active [TextInputConnection] will be a noop.

There can only be one system context menu visible at a time. Calling this while another system context menu is already visible will remove the old menu before showing the new menu.

See also:

- [hide], which hides the menu shown by this method.
- [MediaQuery.supportsShowingSystemContextMenu], which indicates whether this method is supported on the current platform.

### hide()

```dart
Future<void> hide()
```

Hides this system context menu.

If this hasn't been shown, or if another instance has hidden this menu, does nothing.

Currently this is only supported on iOS 16.0 and later.

See also:

- [show], which shows the menu hidden by this method.
- [MediaQuery.supportsShowingSystemContextMenu], which indicates whether the system context menu is supported on the current platform.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### dispose()

```dart
void dispose()
```

Used to release resources when this instance will never be used again.

# IOSSystemContextMenuItemData

```dart
sealed class IOSSystemContextMenuItemData {}
```

Describes a context menu button that will be rendered in the system context menu.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItem], which performs a similar role but at the widget level, where the titles can be replaced with default localized values.
- [ContextMenuButtonItem], which performs a similar role for Flutter-drawn context menus.

### IOSSystemContextMenuItemData()

```dart
IOSSystemContextMenuItemData()
```

### title

```dart
String? get title
```

The text to display to the user.

Not exposed for some built-in menu items whose title is always set by the platform.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

# IOSSystemContextMenuItemDataCopy

```dart
final class IOSSystemContextMenuItemDataCopy extends IOSSystemContextMenuItemData {}
```

An [IOSSystemContextMenuItemData] for the system's built-in copy button.

The title and action are both handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemCopy], which performs a similar role but at the widget level.

### IOSSystemContextMenuItemDataCopy()

```dart
IOSSystemContextMenuItemDataCopy()
```

Creates an instance of [IOSSystemContextMenuItemDataCopy].

# IOSSystemContextMenuItemDataCut

```dart
final class IOSSystemContextMenuItemDataCut extends IOSSystemContextMenuItemData {}
```

An [IOSSystemContextMenuItemData] for the system's built-in cut button.

The title and action are both handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemCut], which performs a similar role but at the widget level.

### IOSSystemContextMenuItemDataCut()

```dart
IOSSystemContextMenuItemDataCut()
```

Creates an instance of [IOSSystemContextMenuItemDataCut].

# IOSSystemContextMenuItemDataPaste

```dart
final class IOSSystemContextMenuItemDataPaste extends IOSSystemContextMenuItemData {}
```

An [IOSSystemContextMenuItemData] for the system's built-in paste button.

The title and action are both handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemPaste], which performs a similar role but at the widget level.

### IOSSystemContextMenuItemDataPaste()

```dart
IOSSystemContextMenuItemDataPaste()
```

Creates an instance of [IOSSystemContextMenuItemDataPaste].

# IOSSystemContextMenuItemDataSelectAll

```dart
final class IOSSystemContextMenuItemDataSelectAll extends IOSSystemContextMenuItemData {}
```

An [IOSSystemContextMenuItemData] for the system's built-in select all button.

The title and action are both handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemSelectAll], which performs a similar role but at the widget level.

### IOSSystemContextMenuItemDataSelectAll()

```dart
IOSSystemContextMenuItemDataSelectAll()
```

Creates an instance of [IOSSystemContextMenuItemDataSelectAll].

# IOSSystemContextMenuItemDataLookUp

```dart
final class IOSSystemContextMenuItemDataLookUp extends IOSSystemContextMenuItemData with Diagnosticable {}
```

An [IOSSystemContextMenuItemData] for the system's built-in look up button.

Must specify a [title], typically [WidgetsLocalizations.lookUpButtonLabel].

The action is handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemLookUp], which performs a similar role but at the widget level, where the title can be replaced with a default localized value.

### IOSSystemContextMenuItemDataLookUp()

```dart
IOSSystemContextMenuItemDataLookUp({required String title})
```

Creates an instance of [IOSSystemContextMenuItemDataLookUp].

### title

```dart
String title
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemDataSearchWeb

```dart
final class IOSSystemContextMenuItemDataSearchWeb extends IOSSystemContextMenuItemData with Diagnosticable {}
```

An [IOSSystemContextMenuItemData] for the system's built-in search web button.

Must specify a [title], typically [WidgetsLocalizations.searchWebButtonLabel].

The action is handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemSearchWeb], which performs a similar role but at the widget level, where the title can be replaced with a default localized value.

### IOSSystemContextMenuItemDataSearchWeb()

```dart
IOSSystemContextMenuItemDataSearchWeb({required String title})
```

Creates an instance of [IOSSystemContextMenuItemDataSearchWeb].

### title

```dart
String title
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemDataShare

```dart
final class IOSSystemContextMenuItemDataShare extends IOSSystemContextMenuItemData with Diagnosticable {}
```

An [IOSSystemContextMenuItemData] for the system's built-in share button.

Must specify a [title], typically [WidgetsLocalizations.shareButtonLabel].

The action is handled by the platform.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemShare], which performs a similar role but at the widget level, where the title can be replaced with a default localized value.

### IOSSystemContextMenuItemDataShare()

```dart
IOSSystemContextMenuItemDataShare({required String title})
```

Creates an instance of [IOSSystemContextMenuItemDataShare].

### title

```dart
String title
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# IOSSystemContextMenuItemDataLiveText

```dart
final class IOSSystemContextMenuItemDataLiveText extends IOSSystemContextMenuItemData {}
```

An [IOSSystemContextMenuItemData] for the system's built-in Live Text (OCR) button.

This button is only available on iOS 15.0+ devices with camera support. It allows the user to scan text from the camera and insert it at the current cursor position.

The title and action are both handled by the platform, and the platform will use its default localized title.

See also:

- [IOSSystemContextMenuItemLiveText], which performs a similar role but at the widget level.
- https://github.com/flutter/flutter/issues/169781

### IOSSystemContextMenuItemDataLiveText()

```dart
IOSSystemContextMenuItemDataLiveText()
```

Creates an instance of [IOSSystemContextMenuItemDataLiveText].

# IOSSystemContextMenuItemDataCustom

```dart
final class IOSSystemContextMenuItemDataCustom extends IOSSystemContextMenuItemData with Diagnosticable {}
```

An [IOSSystemContextMenuItemData] for custom action buttons defined by the developer.

Must specify a [title] and [onPressed].

Only supported on iOS 16.0 and above.

See also:

- [SystemContextMenuController], which is used to show the system context menu.
- [IOSSystemContextMenuItemCustom], which performs a similar role but at the widget level.

### IOSSystemContextMenuItemDataCustom()

```dart
IOSSystemContextMenuItemDataCustom({required String title, required VoidCallback onPressed})
```

Creates an instance of [IOSSystemContextMenuItemDataCustom].

### title

```dart
String title
```

### onPressed

```dart
VoidCallback onPressed
```

The callback to be executed when the item is selected.

### callbackId

```dart
String get callbackId
```

The unique identifier for this custom action.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```
