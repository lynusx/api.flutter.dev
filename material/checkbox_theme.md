@docImport 'checkbox.dart';

# CheckboxThemeData

```dart
class CheckboxThemeData with Diagnosticable {}
```

Defines default property values for descendant [Checkbox] widgets.

Descendant widgets obtain the current [CheckboxThemeData] object using [CheckboxTheme.of]. Instances of [CheckboxThemeData] can be customized with [CheckboxThemeData.copyWith].

Typically a [CheckboxThemeData] is specified as part of the overall [Theme] with [ThemeData.checkboxTheme].

All [CheckboxThemeData] properties are `null` by default. When null, the [Checkbox] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s colorScheme. See the individual [Checkbox] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### CheckboxThemeData()

```dart
CheckboxThemeData({WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? fillColor, WidgetStateProperty<Color?>? checkColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, OutlinedBorder? shape, BorderSide? side})
```

Creates a theme that can be used for [ThemeData.checkboxTheme].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.checkbox.mouseCursor}

If specified, overrides the default value of [Checkbox.mouseCursor].

### fillColor

```dart
WidgetStateProperty<Color?>? fillColor
```

{@macro flutter.material.checkbox.fillColor}

If specified, overrides the default value of [Checkbox.fillColor].

### checkColor

```dart
WidgetStateProperty<Color?>? checkColor
```

{@macro flutter.material.checkbox.checkColor}

Resolves in the following states:

- [WidgetState.selected].
- [WidgetState.hovered].
- [WidgetState.focused].
- [WidgetState.disabled].

If specified, overrides the default value of [Checkbox.checkColor].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

{@macro flutter.material.checkbox.overlayColor}

If specified, overrides the default value of [Checkbox.overlayColor].

### splashRadius

```dart
double? splashRadius
```

{@macro flutter.material.checkbox.splashRadius}

If specified, overrides the default value of [Checkbox.splashRadius].

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@macro flutter.material.checkbox.materialTapTargetSize}

If specified, overrides the default value of [Checkbox.materialTapTargetSize].

### visualDensity

```dart
VisualDensity? visualDensity
```

{@macro flutter.material.checkbox.visualDensity}

If specified, overrides the default value of [Checkbox.visualDensity].

### shape

```dart
OutlinedBorder? shape
```

{@macro flutter.material.checkbox.shape}

If specified, overrides the default value of [Checkbox.shape].

### side

```dart
BorderSide? side
```

{@macro flutter.material.checkbox.side}

If specified, overrides the default value of [Checkbox.side].

### copyWith()

```dart
CheckboxThemeData copyWith({WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? fillColor, WidgetStateProperty<Color?>? checkColor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, MaterialTapTargetSize? materialTapTargetSize, VisualDensity? visualDensity, OutlinedBorder? shape, BorderSide? side})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
CheckboxThemeData lerp(CheckboxThemeData? a, CheckboxThemeData? b, double t)
```

Linearly interpolate between two [CheckboxThemeData]s.

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

# CheckboxTheme

```dart
class CheckboxTheme extends InheritedWidget {}
```

Applies a checkbox theme to descendant [Checkbox] widgets.

Descendant widgets obtain the current theme's [CheckboxTheme] object using [CheckboxTheme.of]. When a widget uses [CheckboxTheme.of], it is automatically rebuilt if the theme later changes.

A checkbox theme can be specified as part of the overall Material theme using [ThemeData.checkboxTheme].

See also:

- [CheckboxThemeData], which describes the actual configuration of a checkbox theme.

### CheckboxTheme()

```dart
CheckboxTheme({dynamic key, required CheckboxThemeData data, required dynamic child})
```

Constructs a checkbox theme that configures all descendant [Checkbox] widgets.

### data

```dart
CheckboxThemeData data
```

The properties used for all descendant [Checkbox] widgets.

### of()

```dart
CheckboxThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [CheckboxTheme] ancestor. If there is no ancestor, it returns [ThemeData.checkboxTheme].

Typical usage is as follows:

```dart
CheckboxThemeData theme = CheckboxTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(CheckboxTheme oldWidget)
```
