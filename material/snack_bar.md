@docImport 'bottom_navigation_bar.dart'; @docImport 'floating_action_button.dart';

# SnackBarClosedReason

```dart
enum SnackBarClosedReason {}
```

Specify how a [SnackBar] was closed.

The [ScaffoldMessengerState.showSnackBar] function returns a [ScaffoldFeatureController]. The value of the controller's closed property is a Future that resolves to a SnackBarClosedReason. Applications that need to know how a snackbar was closed can use this value.

Example:

```dart
ScaffoldMessenger.of(context).showSnackBar(
  const SnackBar(
    content: Text('He likes me. I think he likes me.'),
  )
).closed.then((SnackBarClosedReason reason) {
   // ...
});
```

The snack bar was closed after the user tapped a [SnackBarAction].

The snack bar was closed through a [SemanticsAction.dismiss].

The snack bar was closed by a user's swipe.

The snack bar was closed by the [ScaffoldFeatureController] close callback or by calling [ScaffoldMessengerState.hideCurrentSnackBar] directly.

The snack bar was closed by an call to [ScaffoldMessengerState.removeCurrentSnackBar].

The snack bar was closed because its timer expired.

# SnackBarAction

```dart
class SnackBarAction extends StatefulWidget {}
```

A button for a [SnackBar], known as an "action".

Snack bar actions are always enabled. Instead of disabling a snack bar action, avoid including it in the snack bar in the first place.

Snack bar actions can only be pressed once. Subsequent presses are ignored.

See also:

- [SnackBar]
- <https://material.io/design/components/snackbars.html>

### SnackBarAction()

```dart
SnackBarAction({dynamic key, Color? textColor, Color? disabledTextColor, Color? backgroundColor, Color? disabledBackgroundColor, required String label, required VoidCallback onPressed})
```

Creates an action for a [SnackBar].

### textColor

```dart
Color? textColor
```

The button label color. If not provided, defaults to [SnackBarThemeData.actionTextColor].

If [textColor] is a [WidgetStateColor], then the text color will be resolved against the set of [WidgetState]s that the action text is in, thus allowing for different colors for states such as pressed, hovered and others.

### backgroundColor

```dart
Color? backgroundColor
```

The button background fill color. If not provided, defaults to [SnackBarThemeData.actionBackgroundColor].

If [backgroundColor] is a [WidgetStateColor], then the text color will be resolved against the set of [WidgetState]s that the action text is in, thus allowing for different colors for the states.

### disabledTextColor

```dart
Color? disabledTextColor
```

The button disabled label color. This color is shown after the [SnackBarAction] is dismissed.

### disabledBackgroundColor

```dart
Color? disabledBackgroundColor
```

The button disabled background color. This color is shown after the [SnackBarAction] is dismissed.

If not provided, defaults to [SnackBarThemeData.disabledActionBackgroundColor].

### label

```dart
String label
```

The button label.

### onPressed

```dart
VoidCallback onPressed
```

The callback to be called when the button is pressed.

This callback will be called at most once each time this action is displayed in a [SnackBar].

### createState()

```dart
State<SnackBarAction> createState()
```

# SnackBar

```dart
class SnackBar extends StatefulWidget {}
```

A lightweight message with an optional action which briefly displays at the bottom of the screen.

{@youtube 560 315 https://www.youtube.com/watch?v=zpO6n_oZWw0}

To display a snack bar, call `ScaffoldMessenger.of(context).showSnackBar()`, passing an instance of [SnackBar] that describes the message.

To control how long the [SnackBar] remains visible, specify a [duration].

A SnackBar with an action will not time out when TalkBack or VoiceOver are enabled. This is controlled by [AccessibilityFeatures.accessibleNavigation].

During page transitions, the [SnackBar] will smoothly animate to its location on the other page. For example if the [SnackBar.behavior] is set to [SnackBarBehavior.floating] and the next page has a floating action button, while the current one does not, the [SnackBar] will smoothly animate above the floating action button. It also works in the case of a back gesture transition.

{@tool dartpad} Here is an example of a [SnackBar] with an [action] button implemented using [SnackBarAction].

** See code in examples/api/lib/material/snack_bar/snack_bar.0.dart ** {@end-tool}

{@tool dartpad} Here is an example of a customized [SnackBar]. It utilizes [behavior], [shape], [padding], [width], and [duration] to customize the location, appearance, and the duration for which the [SnackBar] is visible.

** See code in examples/api/lib/material/snack_bar/snack_bar.1.dart ** {@end-tool}

{@tool dartpad} This example demonstrates the various [SnackBar] widget components, including an optional icon, in either floating or fixed format.

** See code in examples/api/lib/material/snack_bar/snack_bar.2.dart ** {@end-tool}

See also:

- [ScaffoldMessenger.of], to obtain the current [ScaffoldMessengerState], which manages the display and animation of snack bars.
- [ScaffoldMessengerState.showSnackBar], which displays a [SnackBar].
- [ScaffoldMessengerState.removeCurrentSnackBar], which abruptly hides the currently displayed snack bar, if any, and allows the next to be displayed.
- [SnackBarAction], which is used to specify an [action] button to show on the snack bar.
- [SnackBarThemeData], to configure the default property values for [SnackBar] widgets.
- <https://material.io/design/components/snackbars.html>

### SnackBar()

```dart
SnackBar({dynamic key, required Widget content, Color? backgroundColor, double? elevation, EdgeInsetsGeometry? margin, EdgeInsetsGeometry? padding, double? width, ShapeBorder? shape, HitTestBehavior? hitTestBehavior, SnackBarBehavior? behavior, SnackBarAction? action, double? actionOverflowThreshold, bool? showCloseIcon, Color? closeIconColor, Duration duration = _snackBarDisplayDuration, bool? persist, Animation<double>? animation, VoidCallback? onVisible, DismissDirection? dismissDirection, Clip clipBehavior = Clip.hardEdge})
```

Creates a snack bar.

The [elevation] must be null or non-negative.

### content

```dart
Widget content
```

The primary content of the snack bar.

Typically a [Text] widget.

### backgroundColor

```dart
Color? backgroundColor
```

The snack bar's background color.

If not specified, the ambient [SnackBarThemeData.backgroundColor] is used. If that is not specified it will default to a dark variation of [ColorScheme.surface] for light themes, or [ColorScheme.onSurface] for dark themes.

### elevation

```dart
double? elevation
```

The z-coordinate at which to place the snack bar. This controls the size of the shadow below the snack bar.

Defines the card's [Material.elevation].

If this property is null, then the ambient [SnackBarThemeData.elevation] is used, if that is also null, the default value is 6.0.

### margin

```dart
EdgeInsetsGeometry? margin
```

Empty space to surround the snack bar.

This property is only used when [behavior] is [SnackBarBehavior.floating]. It can not be used if [width] is specified.

If this property is null, then the ambient [SnackBarThemeData.insetPadding] is used. If that is also null, then the default is `EdgeInsets.fromLTRB(15.0, 5.0, 15.0, 10.0)`.

If this property is not null and [hitTestBehavior] is null, then [hitTestBehavior] default is [HitTestBehavior.deferToChild].

### padding

```dart
EdgeInsetsGeometry? padding
```

The amount of padding to apply to the snack bar's content and optional action.

If this property is null, the default padding values are as follows:

- [content] * Top and bottom paddings are 14. * Left padding is 24 if [behavior] is [SnackBarBehavior.fixed], 16 if [behavior] is [SnackBarBehavior.floating]. * Right padding is same as start padding if there is no [action], otherwise 0.
- [action] * Top and bottom paddings are 14. * Left and right paddings are half of [content]'s left padding.

If this property is not null, the padding is as follows:

- [content] * Left, top and bottom paddings are assigned normally. * Right padding is assigned normally if there is no [action], otherwise 0.
- [action] * Left padding is replaced with half the right padding. * Top and bottom paddings are assigned normally. * Right padding is replaced with one and a half times the right padding.

### width

```dart
double? width
```

The width of the snack bar.

If width is specified, the snack bar will be centered horizontally in the available space. This property is only used when [behavior] is [SnackBarBehavior.floating]. It can not be used if [margin] is specified.

If this property is null, then the ambient [SnackBarThemeData.width] is used. If that is null, the snack bar will take up the full device width less the margin.

### shape

```dart
ShapeBorder? shape
```

The shape of the snack bar's [Material].

Defines the snack bar's [Material.shape].

If this property is null, then the ambient [SnackBarThemeData.shape] is used. If that's null then the shape will depend on the [SnackBarBehavior]. For [SnackBarBehavior.fixed], no overriding shape is specified, so the [SnackBar] is rectangular. For [SnackBarBehavior.floating], it uses a [RoundedRectangleBorder] with a circular corner radius of 4.0.

### hitTestBehavior

```dart
HitTestBehavior? hitTestBehavior
```

Defines how the snack bar area, including margin, will behave during hit testing.

If this property is null, and [margin] is not null or the ambient [SnackBarThemeData.insetPadding] is not null, then [HitTestBehavior.deferToChild] is used by default.

Please refer to [HitTestBehavior] for a detailed explanation of every behavior.

### behavior

```dart
SnackBarBehavior? behavior
```

This defines the behavior and location of the snack bar.

Defines where a [SnackBar] should appear within a [Scaffold] and how its location should be adjusted when the scaffold also includes a [FloatingActionButton] or a [BottomNavigationBar]

If this property is null, then the ambient [SnackBarThemeData.behavior] is used. If that is null, then the default is [SnackBarBehavior.fixed].

If this value is [SnackBarBehavior.floating], the length of the bar is defined by either [width] or [margin].

### action

```dart
SnackBarAction? action
```

(optional) An action that the user can take based on the snack bar.

For example, the snack bar might let the user undo the operation that prompted the snackbar. Snack bars can have at most one action.

The action should not be "dismiss" or "cancel".

### actionOverflowThreshold

```dart
double? actionOverflowThreshold
```

(optional) The percentage threshold for action widget's width before it overflows to a new line.

Must be between 0 and 1. If the width of the [action] divided by the total snackbar width is greater than this percentage, the [action] will appear below the [content].

At a value of 0, the action will always overflow to a new line.

Defaults to 0.25.

### showCloseIcon

```dart
bool? showCloseIcon
```

(optional) Whether to include a "close" icon widget.

Tapping the icon will close the snack bar.

### closeIconColor

```dart
Color? closeIconColor
```

An optional color for the close icon, if [showCloseIcon] is true.

If this property is null, then the ambient [SnackBarThemeData.closeIconColor] is used. If that is null, then the default is inverse surface.

If [closeIconColor] is a [WidgetStateColor], then the icon color will be resolved against the set of [WidgetState]s that the action text is in, thus allowing for different colors for states such as pressed, hovered and others.

### duration

```dart
Duration duration
```

The amount of time the snack bar should be displayed.

Defaults to 4.0s.

See also:

- [ScaffoldMessengerState.removeCurrentSnackBar], which abruptly hides the currently displayed snack bar, if any, and allows the next to be displayed.
- <https://material.io/design/components/snackbars.html>

### persist

```dart
bool persist
```

Whether the snack bar will stay or auto-dismiss after timeout.

If true, the snack bar remains visible even after the timeout, until the user taps the action button or the close icon.

If false, the snack bar will be dismissed after the timeout.

If not provided, but the snackbar action is not null, the snackbar will persist as well.

### animation

```dart
Animation<double>? animation
```

The animation driving the entrance and exit of the snack bar.

### onVisible

```dart
VoidCallback? onVisible
```

Called the first time that the snackbar is visible within a [Scaffold].

When multiple [Scaffold]s are registered to the same [ScaffoldMessengerState], [onVisible] is called once for each scaffold.

See also:

- [ScaffoldMessenger], which manages [SnackBar]s for [Scaffold] descendants.

### dismissDirection

```dart
DismissDirection? dismissDirection
```

The direction in which the SnackBar can be dismissed.

If this property is null, then the ambient [SnackBarThemeData.dismissDirection] is used. If that is null, then the default is [DismissDirection.down].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.hardEdge].

### createAnimationController()

```dart
AnimationController createAnimationController({required TickerProvider vsync, Duration? duration, Duration? reverseDuration})
```

Creates an animation controller useful for driving a snack bar's entrance and exit animation.

### withAnimation()

```dart
SnackBar withAnimation(Animation<double> newAnimation, {Key? fallbackKey})
```

Creates a copy of this snack bar but with the animation replaced with the given animation.

If the original snack bar lacks a key, the newly created snack bar will use the given fallback key.

### createState()

```dart
State<SnackBar> createState()
```
