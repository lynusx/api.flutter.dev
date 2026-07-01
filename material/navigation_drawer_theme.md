@docImport 'navigation_bar.dart';

# NavigationDrawerThemeData

```dart
class NavigationDrawerThemeData with Diagnosticable {}
```

Defines default property values for descendant [NavigationDrawer] widgets.

Descendant widgets obtain the current [NavigationDrawerThemeData] object using [NavigationDrawerTheme.of]. Instances of [NavigationDrawerThemeData] can be customized with [NavigationDrawerThemeData.copyWith].

Typically a [NavigationDrawerThemeData] is specified as part of the overall [Theme] with [ThemeData.navigationDrawerTheme]. Alternatively, a [NavigationDrawerTheme] inherited widget can be used to theme [NavigationDrawer]s in a subtree of widgets.

All [NavigationDrawerThemeData] properties are `null` by default. When null, the [NavigationDrawer] will provide its own defaults based on the overall [Theme]'s textTheme and colorScheme. See the individual [NavigationDrawer] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### NavigationDrawerThemeData()

```dart
NavigationDrawerThemeData({double? tileHeight, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Color? indicatorColor, ShapeBorder? indicatorShape, Size? indicatorSize, WidgetStateProperty<TextStyle?>? labelTextStyle, WidgetStateProperty<IconThemeData?>? iconTheme})
```

Creates a theme that can be used for [ThemeData.navigationDrawerTheme] and [NavigationDrawerTheme].

### tileHeight

```dart
double? tileHeight
```

Overrides the default height of [NavigationDrawerDestination].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [NavigationDrawer.backgroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value of [NavigationDrawer.elevation].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value of [NavigationDrawer.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of [NavigationDrawer.surfaceTintColor].

### indicatorColor

```dart
Color? indicatorColor
```

Overrides the default value of [NavigationDrawer]'s selection indicator.

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

Overrides the default shape of the [NavigationDrawer]'s selection indicator.

### indicatorSize

```dart
Size? indicatorSize
```

Overrides the default size of the [NavigationDrawer]'s selection indicator.

### labelTextStyle

```dart
WidgetStateProperty<TextStyle?>? labelTextStyle
```

The style to merge with the default text style for [NavigationDestination] labels.

You can use this to specify a different style when the label is selected.

### iconTheme

```dart
WidgetStateProperty<IconThemeData?>? iconTheme
```

The theme to merge with the default icon theme for [NavigationDestination] icons.

You can use this to specify a different icon theme when the icon is selected.

### copyWith()

```dart
NavigationDrawerThemeData copyWith({double? tileHeight, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Color? indicatorColor, ShapeBorder? indicatorShape, Size? indicatorSize, WidgetStateProperty<TextStyle?>? labelTextStyle, WidgetStateProperty<IconThemeData?>? iconTheme})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
NavigationDrawerThemeData? lerp(NavigationDrawerThemeData? a, NavigationDrawerThemeData? b, double t)
```

Linearly interpolate between two navigation rail themes.

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

# NavigationDrawerTheme

```dart
class NavigationDrawerTheme extends InheritedTheme {}
```

An inherited widget that defines visual properties for [NavigationDrawer]s and [NavigationDestination]s in this widget's subtree.

Values specified here are used for [NavigationDrawer] properties that are not given an explicit non-null value.

See also:

- [ThemeData.navigationDrawerTheme], which describes the [NavigationDrawerThemeData] in the overall theme for the application.

### NavigationDrawerTheme()

```dart
NavigationDrawerTheme({dynamic key, required NavigationDrawerThemeData data, required dynamic child})
```

Creates a navigation rail theme that controls the [NavigationDrawerThemeData] properties for a [NavigationDrawer].

### data

```dart
NavigationDrawerThemeData data
```

Specifies the background color, label text style, icon theme, and label type values for descendant [NavigationDrawer] widgets.

### of()

```dart
NavigationDrawerThemeData of(BuildContext context)
```

Retrieves the [NavigationDrawerThemeData] from the closest ancestor [NavigationDrawerTheme].

If there is no enclosing [NavigationDrawerTheme] widget, then [ThemeData.navigationDrawerTheme] is used.

Typical usage is as follows:

```dart
NavigationDrawerThemeData theme = NavigationDrawerTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(NavigationDrawerTheme oldWidget)
```
