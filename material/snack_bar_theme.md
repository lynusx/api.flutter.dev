@docImport 'bottom_navigation_bar.dart'; @docImport 'color_scheme.dart'; @docImport 'colors.dart'; @docImport 'floating_action_button.dart'; @docImport 'navigation_bar.dart'; @docImport 'scaffold.dart'; @docImport 'snack_bar.dart';

# SnackBarBehavior

```dart
enum SnackBarBehavior {}
```

Defines where a [SnackBar] should appear within a [Scaffold] and how its location should be adjusted when the scaffold also includes a [FloatingActionButton] or a [BottomNavigationBar].

Fixes the [SnackBar] at the bottom of the [Scaffold].

The exception is that the [SnackBar] will be shown above a [BottomNavigationBar] or a [NavigationBar]. Additionally, the [SnackBar] will cause other non-fixed widgets inside [Scaffold] to be pushed above (for example, the [FloatingActionButton]).

This behavior will cause [SnackBar] to be shown above other widgets in the [Scaffold]. This includes being displayed above a [BottomNavigationBar] or a [NavigationBar], and a [FloatingActionButton] when its location is on the bottom. When the floating action button location is on the top, this behavior will cause the [SnackBar] to be shown above other widgets in the [Scaffold] except the floating action button.

See <https://material.io/design/components/snackbars.html> for more details.

# SnackBarThemeData

```dart
class SnackBarThemeData with Diagnosticable {}
```

Customizes default property values for [SnackBar] widgets.

Descendant widgets obtain the current [SnackBarThemeData] object using [SnackBarTheme.of]. Instances of [SnackBarThemeData] can be customized with [SnackBarThemeData.copyWith].

Typically a [SnackBarThemeData] is specified as part of the overall [Theme] with [ThemeData.snackBarTheme]. The default for [ThemeData.snackBarTheme] provides all `null` properties.

All [SnackBarThemeData] properties are `null` by default. When null, the [SnackBar] will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### SnackBarThemeData()

```dart
SnackBarThemeData({Color? backgroundColor, Color? actionTextColor, Color? disabledActionTextColor, TextStyle? contentTextStyle, double? elevation, ShapeBorder? shape, SnackBarBehavior? behavior, double? width, EdgeInsets? insetPadding, bool? showCloseIcon, Color? closeIconColor, double? actionOverflowThreshold, Color? actionBackgroundColor, Color? disabledActionBackgroundColor, DismissDirection? dismissDirection})
```

Creates a theme that can be used for [ThemeData.snackBarTheme].

The [elevation] must be null or non-negative.

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value for [SnackBar.backgroundColor].

If null, [SnackBar] defaults to dark grey: `Color(0xFF323232)`.

### actionTextColor

```dart
Color? actionTextColor
```

Overrides the default value for [SnackBarAction.textColor].

If null, [SnackBarAction] defaults to [ColorScheme.secondary] of [ThemeData.colorScheme].

### disabledActionTextColor

```dart
Color? disabledActionTextColor
```

Overrides the default value for [SnackBarAction.disabledTextColor].

If null, [SnackBarAction] defaults to [ColorScheme.onSurface] with its opacity set to 0.30 if the [Theme]'s brightness is [Brightness.dark], 0.38 otherwise.

### contentTextStyle

```dart
TextStyle? contentTextStyle
```

Used to configure the [DefaultTextStyle] for the [SnackBar.content] widget.

If null, [SnackBar] defines its default.

### elevation

```dart
double? elevation
```

Overrides the default value for [SnackBar.elevation].

If null, [SnackBar] uses a default of 6.0.

### shape

```dart
ShapeBorder? shape
```

Overrides the default value for [SnackBar.shape].

If null, [SnackBar] provides different defaults depending on the [SnackBarBehavior]. For [SnackBarBehavior.fixed], no overriding shape is specified, so the [SnackBar] is rectangular. For [SnackBarBehavior.floating], it uses a [RoundedRectangleBorder] with a circular corner radius of 4.0.

### behavior

```dart
SnackBarBehavior? behavior
```

Overrides the default value for [SnackBar.behavior].

If null, [SnackBar] will default to [SnackBarBehavior.fixed].

### width

```dart
double? width
```

Overrides the default value for [SnackBar.width].

If this property is null, then the snack bar will take up the full device width less the margin. This value is only used when [behavior] is [SnackBarBehavior.floating].

### insetPadding

```dart
EdgeInsets? insetPadding
```

Overrides the default value for [SnackBar.margin].

This value is only used when [behavior] is [SnackBarBehavior.floating].

### showCloseIcon

```dart
bool? showCloseIcon
```

Overrides the default value for [SnackBar.showCloseIcon].

Whether to show an optional "Close" icon.

### closeIconColor

```dart
Color? closeIconColor
```

Overrides the default value for [SnackBar.closeIconColor].

This value is only used if [showCloseIcon] is true.

### actionOverflowThreshold

```dart
double? actionOverflowThreshold
```

Overrides the default value for [SnackBar.actionOverflowThreshold].

Must be a value between 0 and 1, if present.

### actionBackgroundColor

```dart
Color? actionBackgroundColor
```

Overrides default value for [SnackBarAction.backgroundColor].

If null, [SnackBarAction] falls back to [Colors.transparent].

### disabledActionBackgroundColor

```dart
Color? disabledActionBackgroundColor
```

Overrides default value for [SnackBarAction.disabledBackgroundColor].

If null, [SnackBarAction] falls back to [Colors.transparent].

### dismissDirection

```dart
DismissDirection? dismissDirection
```

Overrides the default value for [SnackBar.dismissDirection].

If null, [SnackBar] will default to [DismissDirection.down].

### copyWith()

```dart
SnackBarThemeData copyWith({Color? backgroundColor, Color? actionTextColor, Color? disabledActionTextColor, TextStyle? contentTextStyle, double? elevation, ShapeBorder? shape, SnackBarBehavior? behavior, double? width, EdgeInsets? insetPadding, bool? showCloseIcon, Color? closeIconColor, double? actionOverflowThreshold, Color? actionBackgroundColor, Color? disabledActionBackgroundColor, DismissDirection? dismissDirection})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
SnackBarThemeData lerp(SnackBarThemeData? a, SnackBarThemeData? b, double t)
```

Linearly interpolate between two SnackBar Themes.

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

# SnackBarTheme

```dart
class SnackBarTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for [SnackBar]s in this widget's subtree.

Values specified here are used for [SnackBar] properties that are not given an explicit non-null value.

### SnackBarTheme()

```dart
SnackBarTheme({dynamic key, required SnackBarThemeData data, required dynamic child})
```

Creates a snackbar theme that controls the configurations for [SnackBar]s in its widget subtree.

### data

```dart
SnackBarThemeData data
```

The properties for descendant [SnackBar] widgets.

### of()

```dart
SnackBarThemeData of(BuildContext context)
```

The closest instance of this class's [data] value that encloses the given context.

If there is no ancestor, it returns [ThemeData.snackBarTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
SnackBarThemeData theme = SnackBarTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(SnackBarTheme oldWidget)
```
