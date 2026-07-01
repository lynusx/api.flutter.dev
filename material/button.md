@docImport 'button_style_button.dart'; @docImport 'elevated_button.dart'; @docImport 'filled_button.dart'; @docImport 'material_button.dart'; @docImport 'outlined_button.dart'; @docImport 'text_button.dart';

# RawMaterialButton

```dart
class RawMaterialButton extends StatefulWidget {}
```

Creates a button based on [Semantics], [Material], and [InkWell] widgets.

This class does not use the current [Theme] or [ButtonTheme] to compute default values for unspecified parameters. It's intended to be used for custom Material buttons that optionally incorporate defaults from the themes or from app-specific sources.

This class is planned to be deprecated in a future release, see [ButtonStyleButton], the base class of [ElevatedButton], [FilledButton], [OutlinedButton] and [TextButton].

See also:

- [ElevatedButton], a filled button whose material elevates when pressed.
- [FilledButton], a filled button that doesn't elevate when pressed.
- [FilledButton.tonal], a filled button variant that uses a secondary fill color.
- [OutlinedButton], a button with an outlined border and no fill color.
- [TextButton], a button with no outline or fill color.

### RawMaterialButton()

```dart
RawMaterialButton({dynamic key, required VoidCallback? onPressed, VoidCallback? onLongPress, ValueChanged<bool>? onHighlightChanged, MouseCursor? mouseCursor, TextStyle? textStyle, Color? fillColor, Color? focusColor, Color? hoverColor, Color? highlightColor, Color? splashColor, double elevation = 2.0, double focusElevation = 4.0, double hoverElevation = 4.0, double highlightElevation = 8.0, double disabledElevation = 0.0, EdgeInsetsGeometry padding = EdgeInsets.zero, VisualDensity visualDensity = VisualDensity.standard, BoxConstraints constraints = const BoxConstraints(minWidth: 88.0, minHeight: 36.0), ShapeBorder shape = const RoundedRectangleBorder(), Duration animationDuration = kThemeChangeDuration, Clip clipBehavior = Clip.none, FocusNode? focusNode, bool autofocus = false, MaterialTapTargetSize? materialTapTargetSize, Widget? child, bool enableFeedback = true})
```

Create a button based on [Semantics], [Material], and [InkWell] widgets.

The [elevation], [focusElevation], [hoverElevation], [highlightElevation], and [disabledElevation] parameters must be non-negative.

### onPressed

```dart
VoidCallback? onPressed
```

Called when the button is tapped or otherwise activated.

If this callback and [onLongPress] are null, then the button will be disabled.

See also:

- [enabled], which is true if the button is enabled.

### onLongPress

```dart
VoidCallback? onLongPress
```

Called when the button is long-pressed.

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

{@template flutter.material.RawMaterialButton.mouseCursor} The cursor for a mouse pointer when it enters or is hovering over the button.

If [mouseCursor] is a [WidgetStateMouseCursor], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.pressed].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled]. {@endtemplate}

If this property is null, [WidgetStateMouseCursor.adaptiveClickable] will be used.

### textStyle

```dart
TextStyle? textStyle
```

Defines the default text style, with [Material.textStyle], for the button's [child].

If [TextStyle.color] is a [WidgetStateProperty<Color>], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.pressed].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

### fillColor

```dart
Color? fillColor
```

The color of the button's [Material].

### focusColor

```dart
Color? focusColor
```

The color for the button's [Material] when it has the input focus.

### hoverColor

```dart
Color? hoverColor
```

The color for the button's [Material] when a pointer is hovering over it.

### highlightColor

```dart
Color? highlightColor
```

The highlight color for the button's [InkWell].

### splashColor

```dart
Color? splashColor
```

The splash color for the button's [InkWell].

### elevation

```dart
double elevation
```

The elevation for the button's [Material] when the button is [enabled] but not pressed.

Defaults to 2.0. The value is always non-negative.

See also:

- [highlightElevation], the default elevation.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [focusElevation], the elevation when the button is focused.
- [disabledElevation], the elevation when the button is disabled.

### hoverElevation

```dart
double hoverElevation
```

The elevation for the button's [Material] when the button is [enabled] and a pointer is hovering over it.

Defaults to 4.0. The value is always non-negative.

If the button is [enabled], and being pressed (in the highlighted state), then the [highlightElevation] take precedence over the [hoverElevation].

See also:

- [elevation], the default elevation.
- [focusElevation], the elevation when the button is focused.
- [disabledElevation], the elevation when the button is disabled.
- [highlightElevation], the elevation when the button is pressed.

### focusElevation

```dart
double focusElevation
```

The elevation for the button's [Material] when the button is [enabled] and has the input focus.

Defaults to 4.0. The value is always non-negative.

If the button is [enabled], and being pressed (in the highlighted state), or a mouse cursor is hovering over the button, then the [hoverElevation] and [highlightElevation] take precedence over the [focusElevation].

See also:

- [elevation], the default elevation.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [disabledElevation], the elevation when the button is disabled.
- [highlightElevation], the elevation when the button is pressed.

### highlightElevation

```dart
double highlightElevation
```

The elevation for the button's [Material] when the button is [enabled] and pressed.

Defaults to 8.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [focusElevation], the elevation when the button is focused.
- [disabledElevation], the elevation when the button is disabled.

### disabledElevation

```dart
double disabledElevation
```

The elevation for the button's [Material] when the button is not [enabled].

Defaults to 0.0. The value is always non-negative.

See also:

- [elevation], the default elevation.
- [hoverElevation], the elevation when a pointer is hovering over the button.
- [focusElevation], the elevation when the button is focused.
- [highlightElevation], the elevation when the button is pressed.

### padding

```dart
EdgeInsetsGeometry padding
```

The internal padding for the button's [child].

### visualDensity

```dart
VisualDensity visualDensity
```

Defines how compact the button's layout will be.

{@macro flutter.material.themedata.visualDensity}

See also:

- [ThemeData.visualDensity], which specifies the [visualDensity] for all widgets within a [Theme].

### constraints

```dart
BoxConstraints constraints
```

Defines the button's size.

Typically used to constrain the button's minimum size.

### shape

```dart
ShapeBorder shape
```

The shape of the button's [Material].

The button's highlight and splash are clipped to this shape. If the button has an elevation, then its drop shadow is defined by this shape.

If [shape] is a [WidgetStateProperty<ShapeBorder>], [WidgetStateProperty.resolve] is used for the following [WidgetState]s:

- [WidgetState.pressed].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

### animationDuration

```dart
Duration animationDuration
```

Defines the duration of animated changes for [shape] and [elevation].

The default value is [kThemeChangeDuration].

### child

```dart
Widget? child
```

Typically the button's label.

### enabled

```dart
bool get enabled
```

Whether the button is enabled or disabled.

Buttons are disabled by default. To enable a button, set its [onPressed] or [onLongPress] properties to a non-null value.

### materialTapTargetSize

```dart
MaterialTapTargetSize materialTapTargetSize
```

Configures the minimum size of the tap target.

Defaults to [MaterialTapTargetSize.padded].

See also:

- [MaterialTapTargetSize], for a description of how this affects tap targets.

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

### clipBehavior

```dart
Clip clipBehavior
```

{@macro flutter.material.Material.clipBehavior}

Defaults to [Clip.none].

### enableFeedback

```dart
bool enableFeedback
```

Whether detected gestures should provide acoustic and/or haptic feedback.

For example, on Android a tap will produce a clicking sound and a long-press will produce a short vibration, when feedback is enabled.

See also:

- [Feedback] for providing platform-specific feedback to certain actions.

### createState()

```dart
State<RawMaterialButton> createState()
```
