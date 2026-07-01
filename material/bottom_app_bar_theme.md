@docImport 'bottom_app_bar.dart'; @docImport 'material.dart';

# BottomAppBarTheme

```dart
class BottomAppBarTheme extends InheritedTheme with Diagnosticable {}
```

Defines default property values for descendant [BottomAppBar] widgets.

Descendant widgets obtain the current [BottomAppBarThemeData] object using [BottomAppBarTheme.of]. Instances of [BottomAppBarThemeData] can be customized with [BottomAppBarThemeData.copyWith].

Typically a [BottomAppBarThemeData] is specified as part of the overall [Theme] with [ThemeData.bottomAppBarTheme].

All [BottomAppBarTheme] properties are `null` by default. When null, the [BottomAppBar] constructor provides defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### BottomAppBarTheme()

```dart
BottomAppBarTheme({dynamic key, Color? color, double? elevation, NotchedShape? shape, double? height, Color? surfaceTintColor, Color? shadowColor, EdgeInsetsGeometry? padding, BottomAppBarThemeData? data, Widget? child})
```

Creates a theme that can be used for [ThemeData.bottomAppBarTheme].

### color

```dart
Color? get color
```

Overrides the default value for [BottomAppBar.color].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.color] property in [data] instead.

### elevation

```dart
double? get elevation
```

Overrides the default value for [BottomAppBar.elevation].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.elevation] property in [data] instead.

### shape

```dart
NotchedShape? get shape
```

Overrides the default value for [BottomAppBar.shape].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.shape] property in [data] instead.

### height

```dart
double? get height
```

Overrides the default value for [BottomAppBar.height].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.height] property in [data] instead.

### surfaceTintColor

```dart
Color? get surfaceTintColor
```

Overrides the default value for [BottomAppBar.surfaceTintColor].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.surfaceTintColor] property in [data] instead.

If null, [BottomAppBar] will not display an overlay color.

See [Material.surfaceTintColor] for more details.

### shadowColor

```dart
Color? get shadowColor
```

Overrides the default value for [BottomAppBar.shadowColor].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.shadowColor] property in [data] instead.

### padding

```dart
EdgeInsetsGeometry? get padding
```

Overrides the default value for [BottomAppBar.padding].

This property is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.padding] property in [data] instead.

### data

```dart
BottomAppBarThemeData get data
```

The properties used for all descendant [BottomAppBar] widgets.

### copyWith()

```dart
BottomAppBarTheme copyWith({Color? color, double? elevation, NotchedShape? shape, double? height, Color? surfaceTintColor, Color? shadowColor, EdgeInsetsGeometry? padding})
```

Creates a copy of this object but with the given fields replaced with the new values.

This method is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.copyWith] method instead.

### of()

```dart
BottomAppBarThemeData of(BuildContext context)
```

Returns the closest [BottomAppBarThemeData] instance given the build context.

### lerp()

```dart
BottomAppBarTheme lerp(BottomAppBarTheme? a, BottomAppBarTheme? b, double t)
```

Linearly interpolate between two bottom app bar themes.

{@macro dart.ui.shadow.lerp}

This method is obsolete and will be deprecated in a future release: please use the [BottomAppBarThemeData.lerp] instead.

### updateShouldNotify()

```dart
bool updateShouldNotify(BottomAppBarTheme oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

# BottomAppBarThemeData

```dart
class BottomAppBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [BottomAppBar] widgets.

Descendant widgets obtain the current [BottomAppBarThemeData] object using [BottomAppBarTheme.of]. Instances of [BottomAppBarThemeData] can be customized with [BottomAppBarThemeData.copyWith].

Typically a [BottomAppBarThemeData] is specified as part of the overall [Theme] with [ThemeData.bottomAppBarTheme].

All [BottomAppBarThemeData] properties are `null` by default. When null, the [BottomAppBar] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults. See the individual [BottomAppBar] properties for details.

See also:

- [BottomAppBar], which is the widget that this theme configures.
- [ThemeData], which describes the overall theme information for the application.

### BottomAppBarThemeData()

```dart
BottomAppBarThemeData({Color? color, double? elevation, NotchedShape? shape, double? height, Color? surfaceTintColor, Color? shadowColor, EdgeInsetsGeometry? padding})
```

Creates a bottom app bar theme that can be used with [ThemeData.bottomAppBarTheme].

### color

```dart
Color? color
```

Overrides the default value for [BottomAppBar.color].

### elevation

```dart
double? elevation
```

Overrides the default value for [BottomAppBar.elevation].

### shape

```dart
NotchedShape? shape
```

Overrides the default value for [BottomAppBar.shape].

### height

```dart
double? height
```

Overrides the default value for [BottomAppBar.height].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value for [BottomAppBar.surfaceTintColor].

If null, [BottomAppBar] will not display an overlay color.

See [Material.surfaceTintColor] for more details.

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value for [BottomAppBar.shadowColor].

### padding

```dart
EdgeInsetsGeometry? padding
```

Overrides the default value for [BottomAppBar.padding].

### copyWith()

```dart
BottomAppBarThemeData copyWith({Color? color, double? elevation, NotchedShape? shape, double? height, Color? surfaceTintColor, Color? shadowColor, EdgeInsetsGeometry? padding})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
BottomAppBarThemeData lerp(BottomAppBarThemeData? a, BottomAppBarThemeData? b, double t)
```

Linearly interpolate between two bottom app bar themes.

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
