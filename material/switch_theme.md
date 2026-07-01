@docImport 'switch.dart';

# SwitchThemeData

```dart
class SwitchThemeData with Diagnosticable {}
```

Defines default property values for descendant [Switch] widgets.

Descendant widgets obtain the current [SwitchThemeData] object using [SwitchTheme.of]. Instances of [SwitchThemeData] can be customized with [SwitchThemeData.copyWith].

Typically a [SwitchThemeData] is specified as part of the overall [Theme] with [ThemeData.switchTheme].

All [SwitchThemeData] properties are `null` by default. When null, the [Switch] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s colorScheme. See the individual [Switch] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### SwitchThemeData()

```dart
SwitchThemeData({WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackOutlineColor, WidgetStateProperty<double?>? trackOutlineWidth, MaterialTapTargetSize? materialTapTargetSize, WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, WidgetStateProperty<Icon?>? thumbIcon, EdgeInsetsGeometry? padding})
```

Creates a theme that can be used for [ThemeData.switchTheme].

### thumbColor

```dart
WidgetStateProperty<Color?>? thumbColor
```

{@macro flutter.material.switch.thumbColor}

If specified, overrides the default value of [Switch.thumbColor].

### trackColor

```dart
WidgetStateProperty<Color?>? trackColor
```

{@macro flutter.material.switch.trackColor}

If specified, overrides the default value of [Switch.trackColor].

### trackOutlineColor

```dart
WidgetStateProperty<Color?>? trackOutlineColor
```

{@macro flutter.material.switch.trackOutlineColor}

If specified, overrides the default value of [Switch.trackOutlineColor].

### trackOutlineWidth

```dart
WidgetStateProperty<double?>? trackOutlineWidth
```

{@macro flutter.material.switch.trackOutlineWidth}

If specified, overrides the default value of [Switch.trackOutlineWidth].

### materialTapTargetSize

```dart
MaterialTapTargetSize? materialTapTargetSize
```

{@macro flutter.material.switch.materialTapTargetSize}

If specified, overrides the default value of [Switch.materialTapTargetSize].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.switch.mouseCursor}

If specified, overrides the default value of [Switch.mouseCursor].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

{@macro flutter.material.switch.overlayColor}

If specified, overrides the default value of [Switch.overlayColor].

### splashRadius

```dart
double? splashRadius
```

{@macro flutter.material.switch.splashRadius}

If specified, overrides the default value of [Switch.splashRadius].

### thumbIcon

```dart
WidgetStateProperty<Icon?>? thumbIcon
```

{@macro flutter.material.switch.thumbIcon}

It is overridden by [Switch.thumbIcon].

### padding

```dart
EdgeInsetsGeometry? padding
```

If specified, overrides the default value of [Switch.padding].

### copyWith()

```dart
SwitchThemeData copyWith({WidgetStateProperty<Color?>? thumbColor, WidgetStateProperty<Color?>? trackColor, WidgetStateProperty<Color?>? trackOutlineColor, WidgetStateProperty<double?>? trackOutlineWidth, MaterialTapTargetSize? materialTapTargetSize, WidgetStateProperty<MouseCursor?>? mouseCursor, WidgetStateProperty<Color?>? overlayColor, double? splashRadius, WidgetStateProperty<Icon?>? thumbIcon, EdgeInsetsGeometry? padding})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
SwitchThemeData lerp(SwitchThemeData? a, SwitchThemeData? b, double t)
```

Linearly interpolate between two [SwitchThemeData]s.

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

# SwitchTheme

```dart
class SwitchTheme extends InheritedWidget {}
```

Applies a switch theme to descendant [Switch] widgets.

Descendant widgets obtain the current theme's [SwitchTheme] object using [SwitchTheme.of]. When a widget uses [SwitchTheme.of], it is automatically rebuilt if the theme later changes.

A switch theme can be specified as part of the overall Material theme using [ThemeData.switchTheme].

See also:

- [SwitchThemeData], which describes the actual configuration of a switch theme.

### SwitchTheme()

```dart
SwitchTheme({dynamic key, required SwitchThemeData data, required dynamic child})
```

Constructs a switch theme that configures all descendant [Switch] widgets.

### data

```dart
SwitchThemeData data
```

The properties used for all descendant [Switch] widgets.

### of()

```dart
SwitchThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [SwitchTheme] ancestor. If there is no ancestor, it returns [ThemeData.switchTheme].

Typical usage is as follows:

```dart
SwitchThemeData theme = SwitchTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SwitchTheme oldWidget)
```
