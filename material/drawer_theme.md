@docImport 'drawer.dart';

# DrawerThemeData

```dart
class DrawerThemeData with Diagnosticable {}
```

Defines default property values for descendant [Drawer] widgets.

Descendant widgets obtain the current [DrawerThemeData] object using [DrawerTheme.of]. Instances of [DrawerThemeData] can be customized with [DrawerThemeData.copyWith].

Typically a [DrawerThemeData] is specified as part of the overall [Theme] with [ThemeData.drawerTheme].

All [DrawerThemeData] properties are `null` by default.

See also:

- [DrawerTheme], an [InheritedWidget] that propagates the theme down its subtree.
- [ThemeData], which describes the overall theme information for the application and can customize a drawer using [ThemeData.drawerTheme].

### DrawerThemeData()

```dart
DrawerThemeData({Color? backgroundColor, Color? scrimColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, ShapeBorder? endShape, double? width, Clip? clipBehavior})
```

Creates a theme that can be used for [ThemeData.drawerTheme] and [DrawerTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [Drawer.backgroundColor].

### scrimColor

```dart
Color? scrimColor
```

Overrides the default value of [DrawerController.scrimColor].

### elevation

```dart
double? elevation
```

Overrides the default value of [Drawer.elevation].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value for [Drawer.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value for [Drawer.surfaceTintColor].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value of [Drawer.shape].

### endShape

```dart
ShapeBorder? endShape
```

Overrides the default value of [Drawer.shape] for an end drawer.

### width

```dart
double? width
```

Overrides the default value of [Drawer.width].

### clipBehavior

```dart
Clip? clipBehavior
```

Overrides the default value of [Drawer.clipBehavior].

### copyWith()

```dart
DrawerThemeData copyWith({Color? backgroundColor, Color? scrimColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, ShapeBorder? endShape, double? width, Clip? clipBehavior})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
DrawerThemeData? lerp(DrawerThemeData? a, DrawerThemeData? b, double t)
```

Linearly interpolate between two drawer themes.

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

# DrawerTheme

```dart
class DrawerTheme extends InheritedTheme {}
```

An inherited widget that defines visual properties for [Drawer]s in this widget's subtree.

Values specified here are used for [Drawer] properties that are not given an explicit non-null value.

Using this would allow you to override the [ThemeData.drawerTheme].

### DrawerTheme()

```dart
DrawerTheme({dynamic key, required DrawerThemeData data, required dynamic child})
```

Creates a theme that defines the [DrawerThemeData] properties for a [Drawer].

### data

```dart
DrawerThemeData data
```

Specifies the background color, scrim color, elevation, and shape for descendant [Drawer] widgets.

### of()

```dart
DrawerThemeData of(BuildContext context)
```

Retrieves the [DrawerThemeData] from the closest ancestor [DrawerTheme].

If there is no enclosing [DrawerTheme] widget, then [ThemeData.drawerTheme] is used.

Typical usage is as follows:

```dart
DrawerThemeData theme = DrawerTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(DrawerTheme oldWidget)
```
