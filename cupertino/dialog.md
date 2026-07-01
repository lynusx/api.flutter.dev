@docImport 'package:flutter/material.dart';

@docImport 'button.dart'; @docImport 'route.dart';

# CupertinoAlertDialog

```dart
class CupertinoAlertDialog extends StatefulWidget {}
```

An iOS-style alert dialog.

{@youtube 560 315 https://www.youtube.com/watch?v=75CsnyRXf5I}

An alert dialog informs the user about situations that require acknowledgment. An alert dialog has an optional title, optional content, and an optional list of actions. The title is displayed above the content and the actions are displayed below the content.

This dialog styles its title and content (typically a message) to match the standard iOS title and message dialog text style. These default styles can be overridden by explicitly defining [TextStyle]s for [Text] widgets that are part of the title or content.

To display action buttons that look like standard iOS dialog buttons, provide [CupertinoDialogAction]s for the [actions] given to this dialog.

Typically passed as the child widget to [showDialog], which displays the dialog.

{@tool dartpad} This sample shows how to use a [CupertinoAlertDialog]. The [CupertinoAlertDialog] shows an alert with a set of two choices when [CupertinoButton] is pressed.

** See code in examples/api/lib/cupertino/dialog/cupertino_alert_dialog.0.dart ** {@end-tool}

See also:

- [CupertinoPopupSurface], which is a generic iOS-style popup surface that holds arbitrary content to create custom popups.
- [CupertinoDialogAction], which is an iOS-style dialog button.
- [AlertDialog], a Material Design alert dialog.
- <https://developer.apple.com/design/human-interface-guidelines/alerts/>

### CupertinoAlertDialog()

```dart
CupertinoAlertDialog({dynamic key, Widget? title, Widget? content, List<Widget> actions = const <Widget>[], ScrollController? scrollController, ScrollController? actionScrollController, Duration insetAnimationDuration = const Duration(milliseconds: 100), Curve insetAnimationCurve = Curves.decelerate})
```

Creates an iOS-style alert dialog.

### title

```dart
Widget? title
```

The (optional) title of the dialog is displayed in a large font at the top of the dialog.

Typically a [Text] widget.

### content

```dart
Widget? content
```

The (optional) content of the dialog is displayed in the center of the dialog in a lighter font.

Typically a [Text] widget.

### actions

```dart
List<Widget> actions
```

The (optional) set of actions that are displayed at the bottom of the dialog.

Typically this is a list of [CupertinoDialogAction] widgets.

### scrollController

```dart
ScrollController? scrollController
```

A scroll controller that can be used to control the scrolling of the [content] in the dialog.

Defaults to null, which means the [CupertinoDialogAction] will create a scroll controller internally.

See also:

- [actionScrollController], which can be used for controlling the actions section when there are many actions.

### actionScrollController

```dart
ScrollController? actionScrollController
```

A scroll controller that can be used to control the scrolling of the actions in the dialog.

Defaults to null, which means the [CupertinoDialogAction] will create an action scroll controller internally.

See also:

- [scrollController], which can be used for controlling the [content] section when it is long.

### insetAnimationDuration

```dart
Duration insetAnimationDuration
```

{@macro flutter.material.dialog.insetAnimationDuration}

### insetAnimationCurve

```dart
Curve insetAnimationCurve
```

{@macro flutter.material.dialog.insetAnimationCurve}

### createState()

```dart
State<CupertinoAlertDialog> createState()
```

# CupertinoPopupSurface

```dart
class CupertinoPopupSurface extends StatelessWidget {}
```

An iOS-style component for creating modal overlays like dialogs and action sheets.

By default, [CupertinoPopupSurface] generates a rounded rectangle surface that applies two effects to the background content:

1.  Background filter: Saturates and then blurs content behind the surface.
2.  Overlay color: Covers the filtered background with a transparent surface color. The color adapts to the CupertinoTheme's brightness: light gray when the ambient [CupertinoTheme] brightness is [Brightness.light], and dark gray when [Brightness.dark].

The blur strength can be changed by setting [blurSigma] to a positive value, or removed by setting the [blurSigma] to 0.

The saturation effect can be removed for debugging by setting [debugIsVibrancePainted] to false. The saturation effect is not supported on web with the skwasm renderer and will not be applied regardless of the value of [debugIsVibrancePainted].

The surface color can be disabled by setting [isSurfacePainted] to false, which is useful for more complicated layouts, such as rendering divider gaps in [CupertinoAlertDialog] or rendering custom surface colors.

{@tool dartpad} This sample shows how to use a [CupertinoPopupSurface]. The [CupertinoPopupSurface] shows a modal popup from the bottom of the screen. Toggle the switch to configure its surface color.

** See code in examples/api/lib/cupertino/dialog/cupertino_popup_surface.0.dart ** {@end-tool}

See also:

- [CupertinoAlertDialog], which is a dialog with a title, content, and actions.
- <https://developer.apple.com/design/human-interface-guidelines/alerts/>

### CupertinoPopupSurface()

```dart
CupertinoPopupSurface({dynamic key, double blurSigma = defaultBlurSigma, bool isSurfacePainted = true, required Widget child})
```

Creates an iOS-style rounded rectangle popup surface.

### blurSigma

```dart
double blurSigma
```

The strength of the gaussian blur applied to the area beneath this surface.

Defaults to [defaultBlurSigma]. Setting [blurSigma] to 0 will remove the blur filter.

### isSurfacePainted

```dart
bool isSurfacePainted
```

Whether or not to paint a translucent white on top of this surface's blurred background. [isSurfacePainted] should be true for a typical popup that contains content without any dividers. A popup that requires dividers should set [isSurfacePainted] to false and then paint its own surface area.

Some popups, like iOS's volume control popup, choose to render a blurred area without any white paint covering it. To achieve this effect, [isSurfacePainted] should be set to false.

Defaults to true.

### child

```dart
Widget child
```

The widget below this widget in the tree.

### defaultBlurSigma

```dart
double defaultBlurSigma
```

The default strength of the blur applied to widgets underlying a [CupertinoPopupSurface].

Eyeballed from the iOS 17 simulator.

### debugIsVibrancePainted

```dart
bool debugIsVibrancePainted
```

Whether or not the area beneath this surface should be saturated with a [ColorFilter].

The appearance of the [ColorFilter] is determined by the [Brightness] value obtained from the ambient [CupertinoTheme].

The vibrance is always painted if asserts are disabled.

Defaults to true.

### build()

```dart
Widget build(BuildContext context)
```

# CupertinoActionSheet

```dart
class CupertinoActionSheet extends StatefulWidget {}
```

An iOS-style action sheet.

{@youtube 560 315 https://www.youtube.com/watch?v=U-ao8p4A82k}

An action sheet is a specific style of alert that presents the user with a set of two or more choices related to the current context. An action sheet can have a title, an additional message, and a list of actions. The title is displayed above the message and the actions are displayed below this content.

This action sheet styles its title and message to match standard iOS action sheet title and message text style.

To display action buttons that look like standard iOS action sheet buttons, provide [CupertinoActionSheetAction]s for the [actions] given to this action sheet.

To include a iOS-style cancel button separate from the other buttons, provide an [CupertinoActionSheetAction] for the [cancelButton] given to this action sheet.

An action sheet is typically passed as the child widget to [showCupertinoModalPopup], which displays the action sheet by sliding it up from the bottom of the screen.

{@tool dartpad} This sample shows how to use a [CupertinoActionSheet]. The [CupertinoActionSheet] shows a modal popup that slides in from the bottom when [CupertinoButton] is pressed.

** See code in examples/api/lib/cupertino/dialog/cupertino_action_sheet.0.dart ** {@end-tool}

See also:

- [CupertinoActionSheetAction], which is an iOS-style action sheet button.
- <https://developer.apple.com/design/human-interface-guidelines/ios/views/action-sheets/>

### CupertinoActionSheet()

```dart
CupertinoActionSheet({dynamic key, Widget? title, Widget? message, List<Widget>? actions, ScrollController? messageScrollController, ScrollController? actionScrollController, Widget? cancelButton})
```

Creates an iOS-style action sheet.

An action sheet must have a non-null value for at least one of the following arguments: [actions], [title], [message], or [cancelButton].

Generally, action sheets are used to give the user a choice between two or more choices for the current context.

### title

```dart
Widget? title
```

An optional title of the action sheet. When the [message] is non-null, the font of the [title] is bold.

Typically a [Text] widget.

### message

```dart
Widget? message
```

An optional descriptive message that provides more details about the reason for the alert.

Typically a [Text] widget.

### actions

```dart
List<Widget>? actions
```

The set of actions that are displayed for the user to select.

This must be a list of [CupertinoActionSheetAction] widgets.

### messageScrollController

```dart
ScrollController? messageScrollController
```

A scroll controller that can be used to control the scrolling of the [message] in the action sheet.

Defaults to null, which means the [CupertinoActionSheet] will create a scroll controller internally.

### actionScrollController

```dart
ScrollController? actionScrollController
```

A scroll controller that can be used to control the scrolling of the [actions] in the action sheet.

Defaults to null, which means the [CupertinoActionSheet] will create an action scroll controller internally.

### cancelButton

```dart
Widget? cancelButton
```

The optional cancel button that is grouped separately from the other actions.

This must be a [CupertinoActionSheetAction] widget.

### createState()

```dart
State<CupertinoActionSheet> createState()
```

# CupertinoActionSheetAction

```dart
class CupertinoActionSheetAction extends StatefulWidget {}
```

The content of a typical action button in a [CupertinoActionSheet].

This widget draws the content of a button, i.e. the text, while the background of the button is drawn by [CupertinoActionSheet]. When [focusNode] has focus, this widget will draw the background of color [focusColor].

See also:

- [CupertinoActionSheet], an alert that presents the user with a set of two or more choices related to the current context.

### CupertinoActionSheetAction()

```dart
CupertinoActionSheetAction({dynamic key, required VoidCallback onPressed, bool isDefaultAction = false, bool isDestructiveAction = false, MouseCursor? mouseCursor, FocusNode? focusNode, Color? focusColor, required Widget child})
```

Creates an action for an iOS-style action sheet.

### onPressed

```dart
VoidCallback onPressed
```

The callback that is called when the button is selected.

The button can be selected by either by tapping on this button or by pressing elsewhere and sliding onto this button before releasing.

### isDefaultAction

```dart
bool isDefaultAction
```

Whether this action is the default choice in the action sheet.

Default buttons have bold text.

### isDestructiveAction

```dart
bool isDestructiveAction
```

Whether this action might change or delete data.

Destructive buttons have red text.

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor that will be shown when hovering over the button.

If null, defaults to [SystemMouseCursors.click] on web and [MouseCursor.defer] on other platforms.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### focusColor

```dart
Color? focusColor
```

The color of the background that highlights active focus.

A transparency of [kCupertinoButtonTintedOpacityLight] (light mode) or [kCupertinoButtonTintedOpacityDark] (dark mode) is automatically applied to this color.

When [focusColor] is null, defaults to [CupertinoColors.activeBlue].

### child

```dart
Widget child
```

The widget below this widget in the tree.

Typically a [Text] widget.

### createState()

```dart
State<CupertinoActionSheetAction> createState()
```

# CupertinoDialogAction

```dart
class CupertinoDialogAction extends StatefulWidget {}
```

A button typically used in a [CupertinoAlertDialog].

See also:

- [CupertinoAlertDialog], a dialog that informs the user about situations that require acknowledgment.

### CupertinoDialogAction()

```dart
CupertinoDialogAction({dynamic key, VoidCallback? onPressed, bool isDefaultAction = false, bool isDestructiveAction = false, TextStyle? textStyle, MouseCursor? mouseCursor, required Widget child})
```

Creates an action for an iOS-style dialog.

### onPressed

```dart
VoidCallback? onPressed
```

The callback that is called when the button is tapped or otherwise activated.

If this is set to null, the button will be disabled.

### isDefaultAction

```dart
bool isDefaultAction
```

Set to true if button is the default choice in the dialog.

Default buttons have bold text. Similar to [UIAlertController.preferredAction](https://developer.apple.com/documentation/uikit/uialertcontroller/1620102-preferredaction), but more than one action can have this attribute set to true in the same [CupertinoAlertDialog].

This parameters defaults to false.

### isDestructiveAction

```dart
bool isDestructiveAction
```

Whether this action destroys an object.

For example, an action that deletes an email is destructive.

Defaults to false.

### textStyle

```dart
TextStyle? textStyle
```

[TextStyle] to apply to any text that appears in this button.

Dialog actions have a built-in text resizing policy for long text. To ensure that this resizing policy always works as expected, [textStyle] must be used if a text size is desired other than that specified in [_kCupertinoDialogActionStyle].

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor that will be shown when hovering over the button.

If null, defaults to [SystemMouseCursors.click] on web and [MouseCursor.defer] on other platforms.

### child

```dart
Widget child
```

The widget below this widget in the tree.

Typically a [Text] widget.

### createState()

```dart
State<CupertinoDialogAction> createState()
```
