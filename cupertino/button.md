@docImport 'nav_bar.dart';

# CupertinoButtonSize

```dart
enum CupertinoButtonSize {}
```

The size of a [CupertinoButton]. Based on the iOS (17) [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/buttons#iOS-iPadOS).

Displays a smaller button with round sides and smaller text (uses [CupertinoTextThemeData.actionSmallTextStyle]).

Displays a medium sized button with round sides and regular-sized text.

Displays a (classic) large button with rounded edges and regular-sized text.

# CupertinoButton

```dart
class CupertinoButton extends StatefulWidget {}
```

An iOS-style button.

Takes in a text or an icon that fades out and in on touch. May optionally have a background.

The [padding] defaults to 16.0 pixels. When using a [CupertinoButton] within a fixed height parent, like a [CupertinoNavigationBar], a smaller, or even [EdgeInsets.zero], should be used to prevent clipping larger [child] widgets.

Preserves any parent [IconThemeData] but overwrites its [IconThemeData.color] with the [CupertinoThemeData.primaryColor] (or [CupertinoThemeData.primaryContrastingColor] if the button is disabled).

{@tool dartpad} This sample shows produces an enabled and disabled [CupertinoButton] and [CupertinoButton.filled].

** See code in examples/api/lib/cupertino/button/cupertino_button.0.dart ** {@end-tool}

See also:

- <https://developer.apple.com/design/human-interface-guidelines/buttons/>

### CupertinoButton()

```dart
CupertinoButton({dynamic key, required Widget child, CupertinoButtonSize sizeStyle = CupertinoButtonSize.large, EdgeInsetsGeometry? padding, Color? color, Color? foregroundColor, Color disabledColor = CupertinoColors.quaternarySystemFill, double? minSize, Size? minimumSize, double? pressedOpacity = 0.4, BorderRadius? borderRadius, AlignmentGeometry alignment = Alignment.center, Color? focusColor, FocusNode? focusNode, ValueChanged<bool>? onFocusChange, bool autofocus = false, MouseCursor? mouseCursor, VoidCallback? onLongPress, required VoidCallback? onPressed})
```

Creates an iOS-style button.

### CupertinoButton.tinted()

```dart
CupertinoButton.tinted({dynamic key, required Widget child, CupertinoButtonSize sizeStyle = CupertinoButtonSize.large, EdgeInsetsGeometry? padding, Color? color, Color? foregroundColor, Color disabledColor = CupertinoColors.tertiarySystemFill, double? minSize, Size? minimumSize, double? pressedOpacity = 0.4, BorderRadius? borderRadius, AlignmentGeometry alignment = Alignment.center, Color? focusColor, FocusNode? focusNode, ValueChanged<bool>? onFocusChange, bool autofocus = false, MouseCursor? mouseCursor, VoidCallback? onLongPress, required VoidCallback? onPressed})
```

Creates an iOS-style button with a tinted background.

The background color is derived from the [CupertinoTheme]'s `primaryColor` + transparency. The foreground color is the [CupertinoTheme]'s `primaryColor`.

To specify a custom background color, use the [color] argument of the default constructor.

To match the iOS "grey" button style, set [color] to [CupertinoColors.systemGrey].

### CupertinoButton.filled()

```dart
CupertinoButton.filled({dynamic key, required Widget child, CupertinoButtonSize sizeStyle = CupertinoButtonSize.large, EdgeInsetsGeometry? padding, Color? color, Color disabledColor = CupertinoColors.tertiarySystemFill, Color? foregroundColor, double? minSize, Size? minimumSize, double? pressedOpacity = 0.4, BorderRadius? borderRadius, AlignmentGeometry alignment = Alignment.center, Color? focusColor, FocusNode? focusNode, ValueChanged<bool>? onFocusChange, bool autofocus = false, MouseCursor? mouseCursor, VoidCallback? onLongPress, required VoidCallback? onPressed})
```

Creates an iOS-style button with a filled background.

The background color is derived from the [color] argument. The foreground color is the [CupertinoTheme]'s `primaryContrastingColor`.

### child

```dart
Widget child
```

The widget below this widget in the tree.

Typically a [Text] widget.

### padding

```dart
EdgeInsetsGeometry? padding
```

The amount of space to surround the child inside the bounds of the button.

Defaults to 16.0 pixels.

### color

```dart
Color? color
```

The color of the button's background.

Defaults to null which produces a button with no background or border.

Defaults to the [CupertinoTheme]'s `primaryColor` when the [CupertinoButton.filled] constructor is used.

### disabledColor

```dart
Color disabledColor
```

The color of the button's background when the button is disabled.

Ignored if the [CupertinoButton] doesn't also have a [color].

Defaults to [CupertinoColors.quaternarySystemFill] when [color] is specified.

### foregroundColor

```dart
Color? foregroundColor
```

The color of the button's text and icons.

Defaults to the [CupertinoTheme]'s `primaryColor` when the [CupertinoButton.filled] constructor is used.

### onPressed

```dart
VoidCallback? onPressed
```

The callback that is called when the button is tapped or otherwise activated.

If [onPressed] and [onLongPress] callbacks are null, then the button will be disabled.

### onLongPress

```dart
VoidCallback? onLongPress
```

If [onPressed] and [onLongPress] callbacks are null, then the button will be disabled.

### minSize

```dart
double? minSize
```

Minimum size of the button.

Defaults to kMinInteractiveDimensionCupertino which the iOS Human Interface Guidelines recommends as the minimum tappable area.

### minimumSize

```dart
Size? minimumSize
```

The minimum size of the button.

Defaults to a button with a height and a width of [kMinInteractiveDimensionCupertino], which the iOS Human Interface Guidelines recommends as the minimum tappable area.

### pressedOpacity

```dart
double? pressedOpacity
```

The opacity that the button will fade to when it is pressed. The button will have an opacity of 1.0 when it is not pressed.

This defaults to 0.4. If null, opacity will not change on pressed if using your own custom effects is desired.

### borderRadius

```dart
BorderRadius? borderRadius
```

The radius of the button's corners when it has a background color.

Defaults to [kCupertinoButtonSizeBorderRadius], based on [sizeStyle].

### sizeStyle

```dart
CupertinoButtonSize sizeStyle
```

The size of the button.

Defaults to [CupertinoButtonSize.large].

### alignment

```dart
AlignmentGeometry alignment
```

The alignment of the button's [child].

Typically buttons are sized to be just big enough to contain the child and its [padding]. If the button's size is constrained to a fixed size, for example by enclosing it with a [SizedBox], this property defines how the child is aligned within the available space.

Always defaults to [Alignment.center].

### focusColor

```dart
Color? focusColor
```

The color to use for the focus highlight for keyboard interactions.

Defaults to a slightly transparent [color]. If [color] is null, defaults to a slightly transparent [CupertinoColors.activeBlue]. Slightly transparent in this context means the color is used with an opacity of 0.80, a brightness of 0.69 and a saturation of 0.835.

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### onFocusChange

```dart
ValueChanged<bool>? onFocusChange
```

Handler called when the focus changes.

Called with true if this widget's node gains focus, and false if it loses focus.

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### mouseCursor

```dart
MouseCursor? mouseCursor
```

The cursor for a mouse pointer when it enters or is hovering over the widget.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]:

- [WidgetState.disabled].
- [WidgetState.pressed].
- [WidgetState.focused].

If null, then [MouseCursor.defer] is used when the button is disabled. When the button is enabled, [SystemMouseCursors.click] is used on Web and [MouseCursor.defer] is used on other platforms.

See also:

- [WidgetStateMouseCursor], a [MouseCursor] that implements [WidgetStateProperty] which is used in APIs that need to accept either a [MouseCursor] or a [WidgetStateProperty].

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled. Buttons are disabled by default. To enable a button, set [onPressed] or [onLongPress] to a non-null value.

### tapMoveSlop()

```dart
double tapMoveSlop()
```

The distance a button needs to be moved after being pressed for its opacity to change.

The opacity changes when the position moved is this distance away from the button.

### createState()

```dart
State<CupertinoButton> createState()
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
