# CupertinoSearchTextField

```dart
class CupertinoSearchTextField extends StatefulWidget {}
```

A [CupertinoTextField] that mimics the look and behavior of UIKit's `UISearchTextField`.

This control defaults to showing the basic parts of a `UISearchTextField`, like the 'Search' placeholder, prefix-ed Search icon, and suffix-ed X-Mark icon.

To control the text that is displayed in the text field, use the [controller]. For example, to set the initial value of the text field, use a [controller] that already contains some text such as:

{@tool dartpad} This examples shows how to provide initial text to a [CupertinoSearchTextField] using the [controller] property.

** See code in examples/api/lib/cupertino/search_field/cupertino_search_field.0.dart ** {@end-tool}

It is recommended to pass a [ValueChanged<String>] to both [onChanged] and [onSubmitted] parameters in order to be notified once the value of the field changes or is submitted by the keyboard:

{@tool dartpad} This examples shows how to be notified of field changes or submitted text from a [CupertinoSearchTextField].

** See code in examples/api/lib/cupertino/search_field/cupertino_search_field.1.dart ** {@end-tool}

See also:

- <https://developer.apple.com/design/human-interface-guidelines/ios/bars/search-bars/>

### CupertinoSearchTextField()

```dart
CupertinoSearchTextField({dynamic key, TextEditingController? controller, ValueChanged<String>? onChanged, ValueChanged<String>? onSubmitted, TextStyle? style, String? placeholder, TextStyle? placeholderStyle, BoxDecoration? decoration, Color? backgroundColor, BorderRadius? borderRadius, TextInputType? keyboardType = TextInputType.text, EdgeInsetsGeometry padding = const EdgeInsetsDirectional.fromSTEB(5.5, 8, 5.5, 8), Color itemColor = CupertinoColors.secondaryLabel, double itemSize = 20.0, EdgeInsetsGeometry prefixInsets = const EdgeInsetsDirectional.fromSTEB(6, 8, 0, 8), Widget prefixIcon = const Icon(CupertinoIcons.search), EdgeInsetsGeometry suffixInsets = const EdgeInsetsDirectional.fromSTEB(0, 8, 5, 8), Icon suffixIcon = const Icon(CupertinoIcons.xmark_circle_fill), OverlayVisibilityMode suffixMode = OverlayVisibilityMode.editing, VoidCallback? onSuffixTap, String? restorationId, FocusNode? focusNode, SmartQuotesType? smartQuotesType, SmartDashesType? smartDashesType, bool enableIMEPersonalizedLearning = true, bool autofocus = false, VoidCallback? onTap, bool autocorrect = true, bool? enabled, double cursorWidth = 2.0, double? cursorHeight, Radius cursorRadius = const Radius.circular(2.0), bool cursorOpacityAnimates = true, Color? cursorColor})
```

Creates a [CupertinoTextField] that mimics the look and behavior of UIKit's `UISearchTextField`.

Similar to [CupertinoTextField], to provide a prefilled text entry, pass in a [TextEditingController] with an initial value to the [controller] parameter.

The [onChanged] parameter takes a [ValueChanged<String>] which is invoked upon a change in the text field's value.

The [onSubmitted] parameter takes a [ValueChanged<String>] which is invoked when the keyboard submits.

To provide a hint placeholder text that appears when the text entry is empty, pass a [String] to the [placeholder] parameter. This defaults to 'Search'.

The [style] and [placeholderStyle] properties allow changing the style of the text and placeholder of the text field. [placeholderStyle] defaults to the gray [CupertinoColors.secondaryLabel] iOS color.

To set the text field's background color and border radius, pass a [BoxDecoration] to the [decoration] parameter. This defaults to the default translucent tertiarySystemFill iOS color and 9 px corner radius.

The [itemColor] and [itemSize] properties allow changing the icon color and icon size of the search icon (prefix) and X-Mark (suffix). They default to [CupertinoColors.secondaryLabel] and `20.0`.

The [padding], [prefixInsets], and [suffixInsets] let you set the padding insets for text, the search icon (prefix), and the X-Mark icon (suffix). They default to values that replicate the `UISearchTextField` look. These default fields were determined using the comparison tool in https://github.com/flutter/platform_tests/.

To customize the prefix icon, pass a [Widget] to [prefixIcon]. This defaults to the search icon.

To customize the suffix icon, pass an [Icon] to [suffixIcon]. This defaults to the X-Mark.

To dictate when the X-Mark (suffix) should be visible, a.k.a. only on when editing, not editing, on always, or on never, pass a [OverlayVisibilityMode] to [suffixMode]. This defaults to only on when editing.

To customize the X-Mark (suffix) action, pass a [VoidCallback] to [onSuffixTap]. This defaults to clearing the text.

### controller

```dart
TextEditingController? controller
```

Controls the text being edited.

Similar to [CupertinoTextField], to provide a prefilled text entry, pass in a [TextEditingController] with an initial value to the [controller] parameter. Defaults to creating its own [TextEditingController].

### onChanged

```dart
ValueChanged<String>? onChanged
```

Invoked upon user input.

### onSubmitted

```dart
ValueChanged<String>? onSubmitted
```

Invoked upon keyboard submission.

### style

```dart
TextStyle? style
```

Allows changing the style of the text.

Defaults to the gray [CupertinoColors.secondaryLabel] iOS color.

### placeholder

```dart
String? placeholder
```

A hint placeholder text that appears when the text entry is empty.

Defaults to 'Search' localized in each supported language.

### placeholderStyle

```dart
TextStyle? placeholderStyle
```

Sets the style of the placeholder of the text field.

Defaults to the gray [CupertinoColors.secondaryLabel] iOS color.

### decoration

```dart
BoxDecoration? decoration
```

Sets the decoration for the text field.

This property is automatically set using the [backgroundColor] and [borderRadius] properties, which both have default values. Therefore, [decoration] has a default value upon building the widget. It is designed to mimic the look of a `UISearchTextField`.

### backgroundColor

```dart
Color? backgroundColor
```

Set the [decoration] property's background color.

Can't be set along with the [decoration]. Defaults to the translucent [CupertinoColors.tertiarySystemFill] iOS color.

### borderRadius

```dart
BorderRadius? borderRadius
```

Sets the [decoration] property's border radius.

Can't be set along with the [decoration]. Defaults to 9 px circular corner radius.

### keyboardType

```dart
TextInputType? keyboardType
```

The keyboard type for this search field.

Defaults to [TextInputType.text].

### padding

```dart
EdgeInsetsGeometry padding
```

Sets the padding insets for the text and placeholder.

Defaults to padding that replicates the `UISearchTextField` look. The inset values were determined using the comparison tool in https://github.com/flutter/platform_tests/.

### itemColor

```dart
Color itemColor
```

Sets the color for the suffix and prefix icons.

Defaults to [CupertinoColors.secondaryLabel].

### itemSize

```dart
double itemSize
```

Sets the base icon size for the suffix and prefix icons.

The size of the icon is scaled using the accessibility font scale settings. Defaults to `20.0`.

### prefixInsets

```dart
EdgeInsetsGeometry prefixInsets
```

Sets the padding insets for the suffix.

Defaults to padding that replicates the `UISearchTextField` suffix look. The inset values were determined using the comparison tool in https://github.com/flutter/platform_tests/.

### prefixIcon

```dart
Widget prefixIcon
```

Sets a prefix widget.

Defaults to an [Icon] widget with the [CupertinoIcons.search] icon.

### suffixInsets

```dart
EdgeInsetsGeometry suffixInsets
```

Sets the padding insets for the prefix.

Defaults to padding that replicates the `UISearchTextField` prefix look. The inset values were determined using the comparison tool in https://github.com/flutter/platform_tests/.

### suffixIcon

```dart
Icon suffixIcon
```

Sets the suffix widget's icon.

Defaults to the X-Mark [CupertinoIcons.xmark_circle_fill]. "To change the functionality of the suffix icon, provide a custom onSuffixTap callback and specify an intuitive suffixIcon.

### suffixMode

```dart
OverlayVisibilityMode suffixMode
```

Dictates when the X-Mark (suffix) should be visible.

Defaults to only on when editing.

### onSuffixTap

```dart
VoidCallback? onSuffixTap
```

Sets the X-Mark (suffix) action.

Defaults to clearing the text. The suffix action is customizable so that users can override it with other functionality, that isn't necessarily clearing text.

### restorationId

```dart
String? restorationId
```

{@macro flutter.material.textfield.restorationId}

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.editableText.autofocus}

### onTap

```dart
VoidCallback? onTap
```

{@macro flutter.material.textfield.onTap}

### autocorrect

```dart
bool autocorrect
```

Whether to enable autocorrection.

Defaults to true.

### smartQuotesType

```dart
SmartQuotesType? smartQuotesType
```

Whether to allow the platform to automatically format quotes.

This flag only affects iOS, where it is equivalent to [`UITextSmartQuotesType`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype?language=objc).

When set to [SmartQuotesType.enabled], it passes [`UITextSmartQuotesTypeYes`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/uitextsmartquotestypeyes?language=objc), and when set to [SmartQuotesType.disabled], it passes [`UITextSmartQuotesTypeNo`](https://developer.apple.com/documentation/uikit/uitextsmartquotestype/uitextsmartquotestypeno?language=objc).

If set to null, [SmartQuotesType.enabled] will be used.

As an example of what this does, a standard vertical double quote character will be automatically replaced by a left or right double quote depending on its position in a word.

Defaults to null.

See also:

- [smartDashesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits>

### smartDashesType

```dart
SmartDashesType? smartDashesType
```

Whether to allow the platform to automatically format dashes.

This flag only affects iOS versions 11 and above, where it is equivalent to [`UITextSmartDashesType`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype?language=objc).

When set to [SmartDashesType.enabled], it passes [`UITextSmartDashesTypeYes`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/uitextsmartdashestypeyes?language=objc), and when set to [SmartDashesType.disabled], it passes [`UITextSmartDashesTypeNo`](https://developer.apple.com/documentation/uikit/uitextsmartdashestype/uitextsmartdashestypeno?language=objc).

If set to null, [SmartDashesType.enabled] will be used.

As an example of what this does, two consecutive hyphen characters will be automatically replaced with one en dash, and three consecutive hyphens will become one em dash.

Defaults to null.

See also:

- [smartQuotesType]
- <https://developer.apple.com/documentation/uikit/uitextinputtraits>

### enableIMEPersonalizedLearning

```dart
bool enableIMEPersonalizedLearning
```

{@macro flutter.services.TextInputConfiguration.enableIMEPersonalizedLearning}

### enabled

```dart
bool? enabled
```

Disables the text field when false.

Text fields in disabled states have a light grey background and don't respond to touch events including the [prefixIcon] and [suffixIcon] button.

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

### createState()

```dart
State<StatefulWidget> createState()
```
