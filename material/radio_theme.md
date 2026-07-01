@docImport 'constants.dart'; @docImport 'radio.dart';

# RadioThemeData

```dart
class RadioThemeData with Diagnosticable {}
```

Defines default property values for descendant [Radio] widgets.

Descendant widgets obtain the current [RadioThemeData] object using [RadioTheme.of]. Instances of [RadioThemeData] can be customized with [RadioThemeData.copyWith].

Typically a [RadioThemeData] is specified as part of the overall [Theme] with [ThemeData.radioTheme].

All [RadioThemeData] properties are `null` by default. When null, the [Radio] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s colorScheme. See the individual [Radio] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.
- [RadioTheme], which is used by descendants to obtain the [RadioThemeData].

### RadioThemeData()

```dart
RadioThemeData({WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? fillColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, WidgetStateProperty<Color?>? backgroundColor, BorderSide? side, WidgetStateProperty<double?>? innerRadius})
```

Creates a theme that can be used for [ThemeData.radioTheme].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.widget.RawRadio.mouseCursor}

If specified, overrides the default value of [Radio.mouseCursor]. The default value is [WidgetStateMouseCursor.clickable].

### fillColor

```dart
WidgetStateProperty<Color?>? fillColor
```

{@macro flutter.material.radio.fillColor}

If specified, overrides the default value of [Radio.fillColor].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

{@macro flutter.material.radio.overlayColor}

If specified, overrides the default value of [Radio.overlayColor].

### splashRadius

```dart
double? splashRadius
```

{@macro flutter.material.radio.splashRadius}

If specified, overrides the default value of [Radio.splashRadius]. The default value is [kRadialReactionRadius].

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@macro flutter.material.radio.materialTapTargetSize}

If specified, overrides the default value of [Radio.materialTapTargetSize]. The default value is the value of [ThemeData.materialTapTargetSize].

### visualDensity

```dart
VisualDensity? visualDensity
```

{@macro flutter.material.radio.visualDensity}

If specified, overrides the default value of [Radio.visualDensity]. The default value is the value of [ThemeData.visualDensity].

### backgroundColor

```dart
WidgetStateProperty<Color?>? backgroundColor
```

{@macro flutter.material.Radio.backgroundColor}

If specified, overrides the default value of [Radio.backgroundColor]. The default value is transparent in all states.

### side

```dart
BorderSide? side
```

{@macro flutter.material.Radio.side}

If specified, overrides the default value of [Radio.side]. The default value is a border using the fill color.

### innerRadius

```dart
WidgetStateProperty<double?>? innerRadius
```

{@macro flutter.material.Radio.innerRadius}

If specified, overrides the default value of [Radio.innerRadius]. The default value is `4.5` in all states.

### copyWith()

```dart
RadioThemeData copyWith({WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? fillColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, WidgetStateProperty<Color?>? backgroundColor, BorderSide? side, WidgetStateProperty<double?>? innerRadius})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
RadioThemeData lerp(RadioThemeData? a, RadioThemeData? b, double t)
```

Linearly interpolate between two [RadioThemeData]s.

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

# RadioTheme

```dart
class RadioTheme extends InheritedWidget {}
```

Applies a radio theme to descendant [Radio] widgets.

Descendant widgets obtain the current theme's [RadioTheme] object using [RadioTheme.of]. When a widget uses [RadioTheme.of], it is automatically rebuilt if the theme later changes.

A radio theme can be specified as part of the overall Material theme using [ThemeData.radioTheme].

See also:

- [RadioThemeData], which describes the actual configuration of a radio theme.

### RadioTheme()

```dart
RadioTheme({dynamic key, required RadioThemeData data, required dynamic child})
```

Constructs a radio theme that configures all descendant [Radio] widgets.

### data

```dart
RadioThemeData data
```

The properties used for all descendant [Radio] widgets.

### of()

```dart
RadioThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [RadioTheme] ancestor. If there is no ancestor, it returns [ThemeData.radioTheme].

Typical usage is as follows:

```dart
RadioThemeData theme = RadioTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(RadioTheme oldWidget)
```
