@docImport 'ink_well.dart'; @docImport 'toggle_buttons.dart';

# ToggleButtonsThemeData

```dart
class ToggleButtonsThemeData with Diagnosticable {}
```

Defines default property values for descendant [ToggleButtons] widgets.

Descendant widgets obtain the current [ToggleButtonsThemeData] object using [ToggleButtonsTheme.of]. Instances of [ToggleButtonsThemeData] can be customized with [ToggleButtonsThemeData.copyWith].

Typically a [ToggleButtonsThemeData] is specified as part of the overall [Theme] with [ThemeData.toggleButtonsTheme].

See also:

- [ToggleButtonsTheme], which describes the actual configuration of a toggle buttons theme.

### ToggleButtonsThemeData()

```dart
ToggleButtonsThemeData({TextStyle? textStyle, BoxConstraints? constraints, Color? color, Color? selectedColor, Color? disabledColor, Color? fillColor, Color? focusColor, Color? highlightColor, Color? hoverColor, Color? splashColor, Color? borderColor, Color? selectedBorderColor, Color? disabledBorderColor, BorderRadius? borderRadius, double? borderWidth})
```

Creates the set of color and border properties used to configure [ToggleButtons].

### textStyle

```dart
TextStyle? textStyle
```

The default text style for [ToggleButtons.children].

[TextStyle.color] will be ignored and substituted by [color], [selectedColor] or [disabledColor] depending on whether the buttons are active, selected, or disabled.

### constraints

```dart
BoxConstraints? constraints
```

Defines the button's size.

Typically used to constrain the button's minimum size.

### color

```dart
Color? color
```

The color for descendant [Text] and [Icon] widgets if the toggle button is enabled.

### selectedColor

```dart
Color? selectedColor
```

The color for descendant [Text] and [Icon] widgets if the toggle button is selected.

### disabledColor

```dart
Color? disabledColor
```

The color for descendant [Text] and [Icon] widgets if the toggle button is disabled.

### fillColor

```dart
Color? fillColor
```

The fill color for selected toggle buttons.

### focusColor

```dart
Color? focusColor
```

The color to use for filling the button when the button has input focus.

### highlightColor

```dart
Color? highlightColor
```

The highlight color for the toggle button's [InkWell].

### splashColor

```dart
Color? splashColor
```

The splash color for the toggle button's [InkWell].

### hoverColor

```dart
Color? hoverColor
```

The color to use for filling the toggle button when the button has a pointer hovering over it.

### borderColor

```dart
Color? borderColor
```

The border color to display when the toggle button is enabled.

### selectedBorderColor

```dart
Color? selectedBorderColor
```

The border color to display when the toggle button is selected.

### disabledBorderColor

```dart
Color? disabledBorderColor
```

The border color to display when the toggle button is disabled.

### borderWidth

```dart
double? borderWidth
```

The width of the border surrounding each toggle button.

This applies to both the greater surrounding border, as well as the borders dividing each toggle button.

To render a hairline border (one physical pixel), set borderWidth to 0.0. See [BorderSide.width] for more details on hairline borders.

### borderRadius

```dart
BorderRadius? borderRadius
```

The radii of the border's corners.

### copyWith()

```dart
ToggleButtonsThemeData copyWith({TextStyle? textStyle, BoxConstraints? constraints, Color? color, Color? selectedColor, Color? disabledColor, Color? fillColor, Color? focusColor, Color? highlightColor, Color? hoverColor, Color? splashColor, Color? borderColor, Color? selectedBorderColor, Color? disabledBorderColor, BorderRadius? borderRadius, double? borderWidth})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
ToggleButtonsThemeData? lerp(ToggleButtonsThemeData? a, ToggleButtonsThemeData? b, double t)
```

Linearly interpolate between two toggle buttons themes.

### hashCode

```dart
int get hashCode
```

### operator ==()

```dart
bool operator ==(Object other)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

# ToggleButtonsTheme

```dart
class ToggleButtonsTheme extends InheritedTheme {}
```

An inherited widget that defines color and border parameters for [ToggleButtons] in this widget's subtree.

Values specified here are used for [ToggleButtons] properties that are not given an explicit non-null value.

### ToggleButtonsTheme()

```dart
ToggleButtonsTheme({dynamic key, required ToggleButtonsThemeData data, required dynamic child})
```

Creates a toggle buttons theme that controls the color and border parameters for [ToggleButtons].

### data

```dart
ToggleButtonsThemeData data
```

Specifies the color and border values for descendant [ToggleButtons] widgets.

### of()

```dart
ToggleButtonsThemeData of(BuildContext context)
```

Retrieves the [ToggleButtonsThemeData] from the closest ancestor [ToggleButtonsTheme].

If there is no enclosing [ToggleButtonsTheme] widget, then [ThemeData.toggleButtonsTheme] is used.

Typical usage is as follows:

```dart
ToggleButtonsThemeData theme = ToggleButtonsTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(ToggleButtonsTheme oldWidget)
```
