@docImport 'floating_action_button.dart'; @docImport 'ink_well.dart'; @docImport 'material.dart'; @docImport 'theme.dart'; @docImport 'theme_data.dart';

# FloatingActionButtonThemeData

```dart
class FloatingActionButtonThemeData with Diagnosticable {}
```

Defines default property values for descendant [FloatingActionButton] widgets.

Descendant widgets obtain the current [FloatingActionButtonThemeData] object using [FloatingActionButtonTheme.of]. Instances of [FloatingActionButtonThemeData] can be customized with [FloatingActionButtonThemeData.copyWith].

Typically a [FloatingActionButtonThemeData] is specified as part of the overall [Theme] with [ThemeData.floatingActionButtonTheme].

All [FloatingActionButtonThemeData] properties are `null` by default. When null, the [FloatingActionButton] provides its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### FloatingActionButtonThemeData()

```dart
FloatingActionButtonThemeData({Color? foregroundColor, Color? backgroundColor, Color? focusColor, Color? hoverColor, Color? splashColor, double? elevation, double? focusElevation, double? hoverElevation, double? disabledElevation, double? highlightElevation, ShapeBorder? shape, bool? enableFeedback, double? iconSize, BoxConstraints? sizeConstraints, BoxConstraints? smallSizeConstraints, BoxConstraints? largeSizeConstraints, BoxConstraints? extendedSizeConstraints, double? extendedIconLabelSpacing, EdgeInsetsGeometry? extendedPadding, TextStyle? extendedTextStyle, WidgetStateProperty<MouseCursor?>? mouseCursor})
```

Creates a theme that can be used for [ThemeData.floatingActionButtonTheme] and [FloatingActionButtonTheme].

### foregroundColor

```dart
Color? foregroundColor
```

Color to be used for the unselected, enabled [FloatingActionButton]'s foreground.

### backgroundColor

```dart
Color? backgroundColor
```

Color to be used for the unselected, enabled [FloatingActionButton]'s background.

### focusColor

```dart
Color? focusColor
```

The color to use for filling the button when the button has input focus.

### hoverColor

```dart
Color? hoverColor
```

The color to use for filling the button when the button has a pointer hovering over it.

### splashColor

```dart
Color? splashColor
```

The splash color for this [FloatingActionButton]'s [InkWell].

### elevation

```dart
double? elevation
```

The z-coordinate to be used for the unselected, enabled [FloatingActionButton]'s elevation foreground.

### focusElevation

```dart
double? focusElevation
```

The z-coordinate at which to place this button relative to its parent when the button has the input focus.

This controls the size of the shadow below the floating action button.

### hoverElevation

```dart
double? hoverElevation
```

The z-coordinate at which to place this button relative to its parent when the button is enabled and has a pointer hovering over it.

This controls the size of the shadow below the floating action button.

### disabledElevation

```dart
double? disabledElevation
```

The z-coordinate to be used for the disabled [FloatingActionButton]'s elevation foreground.

### highlightElevation

```dart
double? highlightElevation
```

The z-coordinate to be used for the selected, enabled [FloatingActionButton]'s elevation foreground.

### shape

```dart
ShapeBorder? shape
```

The shape to be used for the floating action button's [Material].

### enableFeedback

```dart
bool? enableFeedback
```

If specified, defines the feedback property for [FloatingActionButton].

If [FloatingActionButton.enableFeedback] is provided, [enableFeedback] is ignored.

### iconSize

```dart
double? iconSize
```

Overrides the default icon size for the [FloatingActionButton];

### sizeConstraints

```dart
BoxConstraints? sizeConstraints
```

Overrides the default size constraints for the [FloatingActionButton].

### smallSizeConstraints

```dart
BoxConstraints? smallSizeConstraints
```

Overrides the default size constraints for [FloatingActionButton.small].

### largeSizeConstraints

```dart
BoxConstraints? largeSizeConstraints
```

Overrides the default size constraints for [FloatingActionButton.large].

### extendedSizeConstraints

```dart
BoxConstraints? extendedSizeConstraints
```

Overrides the default size constraints for [FloatingActionButton.extended].

### extendedIconLabelSpacing

```dart
double? extendedIconLabelSpacing
```

The spacing between the icon and the label for an extended [FloatingActionButton].

### extendedPadding

```dart
EdgeInsetsGeometry? extendedPadding
```

The padding for an extended [FloatingActionButton]'s content.

### extendedTextStyle

```dart
TextStyle? extendedTextStyle
```

The text style for an extended [FloatingActionButton]'s label.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.RawMaterialButton.mouseCursor}

If specified, overrides the default value of [FloatingActionButton.mouseCursor].

### copyWith()

```dart
FloatingActionButtonThemeData copyWith({Color? foregroundColor, Color? backgroundColor, Color? focusColor, Color? hoverColor, Color? splashColor, double? elevation, double? focusElevation, double? hoverElevation, double? disabledElevation, double? highlightElevation, ShapeBorder? shape, bool? enableFeedback, double? iconSize, BoxConstraints? sizeConstraints, BoxConstraints? smallSizeConstraints, BoxConstraints? largeSizeConstraints, BoxConstraints? extendedSizeConstraints, double? extendedIconLabelSpacing, EdgeInsetsGeometry? extendedPadding, TextStyle? extendedTextStyle, WidgetStateProperty<MouseCursor?>? mouseCursor})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
FloatingActionButtonThemeData? lerp(FloatingActionButtonThemeData? a, FloatingActionButtonThemeData? b, double t)
```

Linearly interpolate between two floating action button themes.

If both arguments are null then null is returned.

{@macro dart.ui.shadow.lerp}

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

# FloatingActionButtonTheme

```dart
class FloatingActionButtonTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for [FloatingActionButton]s in this widget's subtree.

Values specified here are used for [FloatingActionButton] properties that are not given an explicit non-null value.

### FloatingActionButtonTheme()

```dart
FloatingActionButtonTheme({dynamic key, required FloatingActionButtonThemeData data, required dynamic child})
```

Creates a floating action button theme that controls the configurations for [FloatingActionButton]s in its widget subtree.

### data

```dart
FloatingActionButtonThemeData data
```

The properties for descendant [FloatingActionButton] widgets.

### of()

```dart
FloatingActionButtonThemeData of(BuildContext context)
```

The closest instance of this class's [data] value that encloses the given context.

If there is no ancestor, it returns [ThemeData.floatingActionButtonTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
FloatingActionButtonThemeData theme = FloatingActionButtonTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(FloatingActionButtonTheme oldWidget)
```
