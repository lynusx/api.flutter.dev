@docImport 'elevated_button.dart'; @docImport 'elevated_button_theme.dart'; @docImport 'icon_button.dart'; @docImport 'outlined_button.dart'; @docImport 'outlined_button_theme.dart'; @docImport 'text_button.dart'; @docImport 'text_button_theme.dart'; @docImport 'text_theme.dart';

# MaterialButton

```dart
class MaterialButton extends StatelessWidget {}
```

A utility class for building Material buttons that depend on the ambient [ButtonTheme] and [Theme].

This class is planned to be deprecated in a future release. Please use one or more of these buttons and associated themes instead:

- [TextButton], [TextButtonTheme], [TextButtonThemeData],
- [ElevatedButton], [ElevatedButtonTheme], [ElevatedButtonThemeData],
- [OutlinedButton], [OutlinedButtonTheme], [OutlinedButtonThemeData],
- [FilledButton], [FilledButtonTheme], [FilledButtonThemeData]

The button's size will expand to fit the child widget, if necessary.

MaterialButtons whose [onPressed] and [onLongPress] callbacks are null will be disabled. To have an enabled button, make sure to pass a non-null value for [onPressed] or [onLongPress].

To create a button directly, without inheriting theme defaults, use [RawMaterialButton].

If you want an ink-splash effect for taps, but don't want to use a button, consider using [InkWell] directly.

See also:

- [IconButton], to create buttons that contain icons rather than text.

### MaterialButton()

```dart
MaterialButton({dynamic key, required VoidCallback? onPressed, VoidCallback? onLongPress, ValueChanged<bool>? onHighlightChanged, MouseCursor? mouseCursor, ButtonTextTheme? textTheme, Color? textColor, Color? disabledTextColor, Color? color, Color? disabledColor, Color? focusColor, Color? hoverColor, Color? highlightColor, Color? splashColor, Brightness? colorBrightness, double? elevation, double? focusElevation, double? hoverElevation, double? highlightElevation, double? disabledElevation, EdgeInsetsGeometry? padding, VisualDensity? visualDensity, ShapeBorder? shape, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, MaterialTapTargetSize? materialTapTargetSize, Duration? animationDuration, double? minWidth, double? height, bool enableFeedback = true, Widget? child})
```

Creates a Material Design button.

To create a custom Material button consider using [TextButton], [ElevatedButton], or [OutlinedButton].

The [elevation], [hoverElevation], [focusElevation], [highlightElevation], and [disabledElevation] arguments must be non-negative, if specified.

### onPressed

```dart
VoidCallback? onPressed
```

The callback that is called when the button is tapped or otherwise activated.

If this callback and [onLongPress] are null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onLongPress

```dart
VoidCallback? onLongPress
```

The callback that is called when the button is long-pressed.

If this callback and [onPressed] are null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onHighlightChanged

```dart
ValueChanged<bool>? onHighlightChanged
```

Called by the underlying [InkWell] widget's [InkWell.onHighlightChanged] callback.

If [onPressed] changes from null to non-null while a gesture is ongoing, this can fire during the build phase (in which case calling [State.setState] is not allowed).

### mouseCursor

```dart
MouseCursor? mouseCursor
```

{@macro flutter.material.RawMaterialButton.mouseCursor}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### textTheme

```dart
ButtonTextTheme? textTheme
```

Defines the button's base colors, and the defaults for the button's minimum size, internal padding, and shape.

Defaults to `ButtonTheme.of(context).textTheme`.

### textColor

```dart
Color? textColor
```

The color to use for this button's text.

The button's [Material.textStyle] will be the current theme's button text style, [TextTheme.labelLarge] of [ThemeData.textTheme], configured with this color.

The default text color depends on the button theme's text theme, [ButtonThemeData.textTheme].

If [textColor] is a [WidgetStateProperty<Color>], [disabledTextColor] will be ignored.

See also:

- [disabledTextColor], the text color to use when the button has been disabled.

### disabledTextColor

```dart
Color? disabledTextColor
```

The color to use for this button's text when the button is disabled.

The button's [Material.textStyle] will be the current theme's button text style, [TextTheme.labelLarge] of [ThemeData.textTheme], configured with this color.

The default value is the theme's disabled color, [ThemeData.disabledColor].

If [textColor] is a [WidgetStateProperty<Color>], [disabledTextColor] will be ignored.

See also:

- [textColor] - The color to use for this button's text when the button is [enabled].

### color

```dart
Color? color
```

The button's fill color, displayed by its [Material], while it is in its default (unpressed, [enabled]) state.

See also:

- [disabledColor] - the fill color of the button when the button is disabled.

### disabledColor

```dart
Color? disabledColor
```

The fill color of the button when the button is disabled.

The default value of this color is the theme's disabled color, [ThemeData.disabledColor].

See also:

- [color] - the fill color of the button when the button is [enabled].

### splashColor

```dart
Color? splashColor
```

The splash color of the button's [InkWell].

The ink splash indicates that the button has been touched. It appears on top of the button's child and spreads in an expanding circle beginning where the touch occurred.

The default splash color is the current theme's splash color, [ThemeData.splashColor].

The appearance of the splash can be configured with the theme's splash factory, [ThemeData.splashFactory].

### focusColor

```dart
Color? focusColor
```

The fill color of the button's [Material] when it has the input focus.

The button changed focus color when the button has the input focus. It appears behind the button's child.

### hoverColor

```dart
Color? hoverColor
```

The fill color of the button's [Material] when a pointer is hovering over it.

The button changes fill color when a pointer is hovering over the button. It appears behind the button's child.

### highlightColor

```dart
Color? highlightColor
```

The highlight color of the button's [InkWell].

The highlight indicates that the button is actively being pressed. It appears on top of the button's child and quickly spreads to fill the button, and then fades out.

If [textTheme] is [ButtonTextTheme.primary], the default highlight color is transparent (in other words the highlight doesn't appear). Otherwise it's the current theme's highlight color, [ThemeData.highlightColor].

### elevation

```dart
double? elevation
```

The z-coordinate at which to place this button relative to its parent.

This controls the size of the shadow below the raised button.

Defaults to 2, the appropriate elevation for raised buttons. The value is always non-negative.

See also:

- [TextButton], a button with no elevation or fill color.
- [focusElevation], the elevation when the button is focused.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [disabledElevation], the elevation when the button is disabled.
- [highlightElevation], the elevation when the button is pressed.

### hoverElevation

```dart
double? hoverElevation
```

The elevation for the button's [Material] when the button is [enabled] and a pointer is hovering over it.

Defaults to 4.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [focusElevation], the elevation when the button is focused.
- [disabledElevation], the elevation when the button is disabled.
- [highlightElevation], the elevation when the button is pressed.

### focusElevation

```dart
double? focusElevation
```

The elevation for the button's [Material] when the button is [enabled] and has the input focus.

Defaults to 4.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [disabledElevation], the elevation when the button is disabled.
- [highlightElevation], the elevation when the button is pressed.

### highlightElevation

```dart
double? highlightElevation
```

The elevation for the button's [Material] relative to its parent when the button is [enabled] and pressed.

This controls the size of the shadow below the button. When a tap down gesture occurs within the button, its [InkWell] displays a [highlightColor] "highlight".

Defaults to 8.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [focusElevation], the elevation when the button is focused.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [disabledElevation], the elevation when the button is disabled.

### disabledElevation

```dart
double? disabledElevation
```

The elevation for the button's [Material] relative to its parent when the button is not [enabled].

Defaults to 0.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [highlightElevation], the elevation when the button is pressed.

### colorBrightness

```dart
Brightness? colorBrightness
```

The theme brightness to use for this button.

Defaults to the theme's brightness in [ThemeData.brightness]. Setting this value determines the button text's colors based on [ButtonThemeData.getTextColor].

See also:

- [ButtonTextTheme], uses [Brightness] to determine text color.

### child

```dart
Widget? child
```

The button's label.

Often a [Text] widget in all caps.

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

Buttons are disabled by default. To enable a button, set its [onPressed] or [onLongPress] properties to a non-null value.

### padding

```dart
EdgeInsetsGeometry? padding
```

The internal padding for the button's [child].

Defaults to the value from the current [ButtonTheme], [ButtonThemeData.padding].

### visualDensity

```dart
VisualDensity? visualDensity
```

Defines how compact the button's layout will be.

{@macro flutter.material.themedata.visualDensity}

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### shape

```dart
ShapeBorder? shape
```

The shape of the button's [Material].

The button's highlight and splash are clipped to this shape. If the button has an elevation, then its drop shadow is defined by this shape as well.

Defaults to the value from the current [ButtonTheme], [ButtonThemeData.shape].

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### focusNode

```dart
FocusNode? focusNode
```

{@macro flutter.widgets.Focus.focusNode}

### autofocus

```dart
bool autofocus
```

{@macro flutter.widgets.Focus.autofocus}

### animationDuration

```dart
Duration? animationDuration
```

Defines the duration of animated changes for [shape] and [elevation].

The default value is [kThemeChangeDuration].

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

Configures the minimum size of the tap target.

Defaults to [ThemeData.materialTapTargetSize].

See also:

- [MaterialTapTargetSize], for a description of how this affects tap targets.

### minWidth

```dart
double? minWidth
```

The smallest horizontal extent that the button will occupy.

Defaults to the value from the current [ButtonTheme].

### height

```dart
double? height
```

The vertical extent of the button.

Defaults to the value from the current [ButtonTheme].

### enableFeedback

```dart
bool enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
