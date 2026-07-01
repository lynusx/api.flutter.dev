@docImport 'button.dart'; @docImport 'button_bar.dart'; @docImport 'dropdown.dart'; @docImport 'elevated_button.dart'; @docImport 'elevated_button_theme.dart'; @docImport 'filled_button.dart'; @docImport 'filled_button_theme.dart'; @docImport 'material.dart'; @docImport 'outlined_button.dart'; @docImport 'outlined_button_theme.dart'; @docImport 'text_button.dart'; @docImport 'text_button_theme.dart'; @docImport 'text_theme.dart';

# ButtonTextTheme

```dart
enum ButtonTextTheme {}
```

Used with [ButtonTheme] and [ButtonThemeData] to define a button's base colors, and the defaults for the button's minimum size, internal padding, and shape.

Button text is black or white depending on [ThemeData.brightness].

Button text is [ColorScheme.secondary].

Button text is based on [ThemeData.primaryColor].

# ButtonBarLayoutBehavior

```dart
enum ButtonBarLayoutBehavior {}
```

Used with [ButtonTheme] and [ButtonThemeData] to define how the button bar should size itself with either constraints or internal padding.

Button bars will be constrained to a minimum height of 52.

This setting is require to create button bars which conform to the Material Design specification.

Button bars will calculate their padding from the button theme padding.

# ButtonTheme

```dart
class ButtonTheme extends InheritedTheme {}
```

Used with [ButtonThemeData] to configure the color and geometry of buttons.

This class is planned to be deprecated in a future release. Please use one or more of these buttons and associated themes instead:

- [ElevatedButton], [ElevatedButtonTheme], [ElevatedButtonThemeData],
- [FilledButton], [FilledButtonTheme], [FilledButtonThemeData],
- [OutlinedButton], [OutlinedButtonTheme], [OutlinedButtonThemeData]
- [TextButton], [TextButtonTheme], [TextButtonThemeData],

A button theme can be specified as part of the overall Material theme using [ThemeData.buttonTheme]. The Material theme's button theme data can be overridden with [ButtonTheme].

The actual appearance of buttons depends on the button theme, the button's enabled state, its elevation (if any), and the overall [Theme].

See also:

- [RawMaterialButton], which can be used to configure a button that doesn't depend on any inherited themes.

### ButtonTheme()

```dart
ButtonTheme({dynamic key, ButtonTextTheme textTheme = ButtonTextTheme.normal, ButtonBarLayoutBehavior layoutBehavior = ButtonBarLayoutBehavior.padded, double minWidth = 88.0, double height = 36.0, EdgeInsetsGeometry? padding, ShapeBorder? shape, bool alignedDropdown = false, Color? buttonColor, Color? disabledColor, Color? focusColor, Color? hoverColor, Color? highlightColor, Color? splashColor, ColorScheme? colorScheme, MaterialTapTargetSize? materialTapTargetSize, required dynamic child})
```

Creates a button theme.

### ButtonTheme.fromButtonThemeData()

```dart
ButtonTheme.fromButtonThemeData({dynamic key, required ButtonThemeData data, required dynamic child})
```

Creates a button theme from [data].

### data

```dart
ButtonThemeData data
```

Specifies the color and geometry of buttons.

### of()

```dart
ButtonThemeData of(BuildContext context)
```

Retrieves the [ButtonThemeData] from the closest ancestor [ButtonTheme] widget.

Typical usage is as follows:

```dart
ButtonThemeData theme = ButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ButtonTheme oldWidget)
```

# ButtonThemeData

```dart
class ButtonThemeData with Diagnosticable {}
```

Used with [ButtonTheme] to configure the color and geometry of buttons.

This class is planned to be deprecated in a future release. Please use one or more of these buttons and associated themes instead:

- [TextButton], [TextButtonTheme], [TextButtonThemeData],
- [ElevatedButton], [ElevatedButtonTheme], [ElevatedButtonThemeData],
- [OutlinedButton], [OutlinedButtonTheme], [OutlinedButtonThemeData]

A button theme can be specified as part of the overall Material theme using [ThemeData.buttonTheme]. The Material theme's button theme data can be overridden with [ButtonTheme].

### ButtonThemeData()

```dart
ButtonThemeData({ButtonTextTheme textTheme = ButtonTextTheme.normal, double minWidth = 88.0, double height = 36.0, EdgeInsetsGeometry? padding, ShapeBorder? shape, ButtonBarLayoutBehavior layoutBehavior = ButtonBarLayoutBehavior.padded, bool alignedDropdown = false, Color? buttonColor, Color? disabledColor, Color? focusColor, Color? hoverColor, Color? highlightColor, Color? splashColor, ColorScheme? colorScheme, MaterialTapTargetSize? materialTapTargetSize})
```

Create a button theme object that can be used with [ButtonTheme] or [ThemeData].

The [minWidth] and [height] parameters must greater than or equal to zero.

The ButtonTheme's methods that have a [MaterialButton] parameter and have a name with a `get` prefix are used to configure a [RawMaterialButton].

### minWidth

```dart
double minWidth
```

The minimum width for buttons.

The actual horizontal space allocated for a button's child is at least this value less the theme's horizontal [padding].

Defaults to 88.0 logical pixels.

### height

```dart
double height
```

The minimum height for buttons.

Defaults to 36.0 logical pixels.

### textTheme

```dart
ButtonTextTheme textTheme
```

Defines a button's base colors, and the defaults for the button's minimum size, internal padding, and shape.

Despite the name, this property is not a [TextTheme], its value is not a collection of [TextStyle]s.

### layoutBehavior

```dart
ButtonBarLayoutBehavior layoutBehavior
```

Defines whether a [ButtonBar] should size itself with a minimum size constraint or with padding.

Defaults to [ButtonBarLayoutBehavior.padded].

### constraints

```dart
BoxConstraints get constraints
```

Convenience that returns [minWidth] and [height] as a [BoxConstraints] object.

### padding

```dart
EdgeInsetsGeometry get padding
```

Padding for a button's child (typically the button's label).

Defaults to 24.0 on the left and right if [textTheme] is [ButtonTextTheme.primary], 16.0 on the left and right otherwise.

See also:

- [getPadding], which is used to calculate padding for the button's child (typically the button's label).

### shape

```dart
ShapeBorder get shape
```

The shape of a button's material.

The button's highlight and splash are clipped to this shape. If the button has an elevation, then its drop shadow is defined by this shape as well.

Defaults to a rounded rectangle with circular corner radii of 4.0 if [textTheme] is [ButtonTextTheme.primary], a rounded rectangle with circular corner radii of 2.0 otherwise.

See also:

- [getShape], which is used to calculate the shape of the button's [Material].

### alignedDropdown

```dart
bool alignedDropdown
```

If true, then a [DropdownButton] menu's width will match the button's width.

If false (the default), then the dropdown's menu will be wider than its button. In either case the dropdown button will line up the leading edge of the menu's value with the leading edge of the values displayed by the menu items.

This property only affects [DropdownButton] and its menu.

### colorScheme

```dart
ColorScheme? colorScheme
```

A set of thirteen colors that can be used to derive the button theme's colors.

This property was added much later than the theme's set of highly specific colors, like [ThemeData.highlightColor] and [ThemeData.splashColor] etc.

The colors for new button classes can be defined exclusively in terms of [colorScheme]. When it's possible, the existing buttons will (continue to) gradually migrate to it.

### getBrightness()

```dart
Brightness getBrightness(MaterialButton button)
```

The [button]'s overall brightness.

Returns the button's [MaterialButton.colorBrightness] if it is non-null, otherwise the color scheme's [ColorScheme.brightness] is returned.

### getTextTheme()

```dart
ButtonTextTheme getTextTheme(MaterialButton button)
```

Defines the [button]'s base colors, and the defaults for the button's minimum size, internal padding, and shape.

Despite the name, this property is not the [TextTheme] whose [TextTheme.labelLarge] is used as the button text's [TextStyle].

### getDisabledTextColor()

```dart
Color getDisabledTextColor(MaterialButton button)
```

The foreground color of the [button]'s text and icon when [MaterialButton.onPressed] is null (when MaterialButton.enabled is false).

Returns the button's [MaterialButton.disabledColor] if it is non-null. Otherwise the color scheme's [ColorScheme.onSurface] color is returned with its opacity set to 0.38.

If [MaterialButton.textColor] is a [WidgetStateProperty<Color>], it will be used as the `disabledTextColor`. It will be resolved in the [WidgetState.disabled] state.

### getDisabledFillColor()

```dart
Color getDisabledFillColor(MaterialButton button)
```

The [button]'s background color when [MaterialButton.onPressed] is null (when [MaterialButton.enabled] is false).

Returns the button's [MaterialButton.disabledColor] if it is non-null.

Otherwise the value of the `disabledColor` constructor parameter is returned, if it is non-null.

Otherwise the color scheme's [ColorScheme.onSurface] color is returned with its opacity set to 0.38.

### getFillColor()

```dart
Color? getFillColor(MaterialButton button)
```

The button's background fill color or null for buttons that don't have a background color.

Returns [MaterialButton.color] if it is non-null and the button is enabled.

Otherwise, returns [MaterialButton.disabledColor] if it is non-null and the button is disabled.

Otherwise the fill color depends on the value of [getTextTheme].

- [ButtonTextTheme.normal] or [ButtonTextTheme.accent], the color scheme's [ColorScheme.primary] color if the [button] is enabled the value of [getDisabledFillColor] otherwise.
- [ButtonTextTheme.primary], if the [button] is enabled then the value of the `buttonColor` constructor parameter if it is non-null, otherwise the color scheme's ColorScheme.primary color. If the button is not enabled then the colorScheme's [ColorScheme.onSurface] color with opacity 0.12.

### getTextColor()

```dart
Color getTextColor(MaterialButton button)
```

The foreground color of the [button]'s text and icon.

If [button] is not [MaterialButton.enabled], the value of [getDisabledTextColor] is returned. If the button is enabled and [MaterialButton.textColor] is non-null, then [MaterialButton.textColor] is returned.

Otherwise the text color depends on the value of [getTextTheme] and [getBrightness].

- [ButtonTextTheme.normal]: [Colors.white] is used if [getBrightness] resolves to [Brightness.dark]. [Colors.black87] is used if [getBrightness] resolves to [Brightness.light].
- [ButtonTextTheme.accent]: [ColorScheme.secondary] of [colorScheme].
- [ButtonTextTheme.primary]: If [getFillColor] is dark then [Colors.white], otherwise [Colors.black].

### getSplashColor()

```dart
Color getSplashColor(MaterialButton button)
```

The color of the ink "splash" overlay that appears when the (enabled) [button] is tapped.

Returns the button's [MaterialButton.splashColor] if it is non-null.

Otherwise, returns the value of the `splashColor` constructor parameter it is non-null.

Otherwise, returns the value of the `splashColor` constructor parameter if it is non-null and [getTextTheme] is not [ButtonTextTheme.primary].

Otherwise, returns [getTextColor] with an opacity of 0.12.

### getFocusColor()

```dart
Color getFocusColor(MaterialButton button)
```

The fill color of the button when it has input focus.

Returns the button's [MaterialButton.focusColor] if it is non-null. Otherwise the focus color depends on [getTextTheme]:

- [ButtonTextTheme.normal], [ButtonTextTheme.accent]: returns the value of the `focusColor` constructor parameter if it is non-null, otherwise the value of [getTextColor] with opacity 0.12.
- [ButtonTextTheme.primary], returns [Colors.transparent].

### getHoverColor()

```dart
Color getHoverColor(MaterialButton button)
```

The fill color of the button when it has input focus.

Returns the button's [MaterialButton.focusColor] if it is non-null. Otherwise the focus color depends on [getTextTheme]:

- [ButtonTextTheme.normal], [ButtonTextTheme.accent], [ButtonTextTheme.primary]: returns the value of the `focusColor` constructor parameter if it is non-null, otherwise the value of [getTextColor] with opacity 0.04.

### getHighlightColor()

```dart
Color getHighlightColor(MaterialButton button)
```

The color of the overlay that appears when the [button] is pressed.

Returns the button's [MaterialButton.highlightColor] if it is non-null. Otherwise the highlight color depends on [getTextTheme]:

- [ButtonTextTheme.normal], [ButtonTextTheme.accent]: returns the value of the `highlightColor` constructor parameter if it is non-null, otherwise the value of [getTextColor] with opacity 0.16.
- [ButtonTextTheme.primary], returns [Colors.transparent].

### getElevation()

```dart
double getElevation(MaterialButton button)
```

The [button]'s elevation when it is enabled and has not been pressed.

Returns the button's [MaterialButton.elevation] if it is non-null, otherwise it is 2.0.

### getFocusElevation()

```dart
double getFocusElevation(MaterialButton button)
```

The [button]'s elevation when it is enabled and has focus.

Returns the button's [MaterialButton.focusElevation] if it is non-null, otherwise the highlight elevation is 4.0.

### getHoverElevation()

```dart
double getHoverElevation(MaterialButton button)
```

The [button]'s elevation when it is enabled and has focus.

Returns the button's [MaterialButton.hoverElevation] if it is non-null, otherwise the highlight elevation is 4.0.

### getHighlightElevation()

```dart
double getHighlightElevation(MaterialButton button)
```

The [button]'s elevation when it is enabled and has been pressed.

Returns the button's [MaterialButton.highlightElevation] if it is non-null, otherwise the highlight elevation is 8.0.

### getDisabledElevation()

```dart
double getDisabledElevation(MaterialButton button)
```

The [button]'s elevation when [MaterialButton.onPressed] is null (when MaterialButton.enabled is false).

Returns the button's [MaterialButton.elevation] if it is non-null.

Otherwise the disabled elevation is 0.0.

### getPadding()

```dart
EdgeInsetsGeometry getPadding(MaterialButton button)
```

Padding for the [button]'s child (typically the button's label).

Returns the button's [MaterialButton.padding] if it is non-null, otherwise, returns the `padding` of the constructor parameter if it is non-null.

Otherwise, returns horizontal padding of 24.0 on the left and right if [getTextTheme] is [ButtonTextTheme.primary], 16.0 on the left and right otherwise.

### getShape()

```dart
ShapeBorder getShape(MaterialButton button)
```

The shape of the [button]'s [Material].

Returns the button's [MaterialButton.shape] if it is non-null, otherwise [shape] is returned.

### getAnimationDuration()

```dart
Duration getAnimationDuration(MaterialButton button)
```

The duration of the [button]'s highlight animation.

Returns the button's [MaterialButton.animationDuration] it if is non-null, otherwise 200ms.

### getConstraints()

```dart
BoxConstraints getConstraints(MaterialButton button)
```

The [BoxConstraints] that the define the [button]'s size.

By default this method just returns [constraints]. Subclasses could override this method to return a value that was, for example, based on the button's type.

### getMaterialTapTargetSize()

```dart
MaterialTapTargetSize getMaterialTapTargetSize(MaterialButton button)
```

The minimum size of the [button]'s tap target.

Returns the button's [MaterialButton.materialTapTargetSize] if it is non-null.

Otherwise the value of the `materialTapTargetSize` constructor parameter is returned if that's non-null.

Otherwise [MaterialTapTargetSize.padded] is returned.

### copyWith()

```dart
ButtonThemeData copyWith({ButtonTextTheme? textTheme, ButtonBarLayoutBehavior? layoutBehavior, double? minWidth, double? height, EdgeInsetsGeometry? padding, ShapeBorder? shape, bool? alignedDropdown, Color? buttonColor, Color? disabledColor, Color? focusColor, Color? hoverColor, Color? highlightColor, Color? splashColor, ColorScheme? colorScheme, MaterialTapTargetSize? materialTapTargetSize})
```

Creates a copy of this button theme data object with the matching fields replaced with the non-null parameter values.

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
