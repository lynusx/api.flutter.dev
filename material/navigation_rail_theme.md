@docImport 'navigation_bar.dart';

# NavigationRailThemeData

```dart
class NavigationRailThemeData with Diagnosticable {}
```

Defines default property values for descendant [NavigationRail] widgets.

Descendant widgets obtain the current [NavigationRailThemeData] object using [NavigationRailTheme.of]. Instances of [NavigationRailThemeData] can be customized with [NavigationRailThemeData.copyWith].

Typically a [NavigationRailThemeData] is specified as part of the overall [Theme] with [ThemeData.navigationRailTheme].

All [NavigationRailThemeData] properties are `null` by default. When null, the [NavigationRail] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults based on the overall [Theme]'s textTheme and colorScheme. See the individual [NavigationRail] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### NavigationRailThemeData()

```dart
NavigationRailThemeData({Color? backgroundColor, double? elevation, TextStyle? unselectedLabelTextStyle, TextStyle? selectedLabelTextStyle, IconThemeData? unselectedIconTheme, IconThemeData? selectedIconTheme, double? groupAlignment, NavigationRailLabelType? labelType, bool? useIndicator, Color? indicatorColor, ShapeBorder? indicatorShape, double? minWidth, double? minExtendedWidth})
```

Creates a theme that can be used for [ThemeData.navigationRailTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Color to be used for the [NavigationRail]'s background.

### elevation

```dart
double? elevation
```

The z-coordinate to be used for the [NavigationRail]'s elevation.

### unselectedLabelTextStyle

```dart
TextStyle? unselectedLabelTextStyle
```

The style to merge with the default text style for [NavigationRailDestination] labels, when the destination is not selected.

### selectedLabelTextStyle

```dart
TextStyle? selectedLabelTextStyle
```

The style to merge with the default text style for [NavigationRailDestination] labels, when the destination is selected.

### unselectedIconTheme

```dart
IconThemeData? unselectedIconTheme
```

The theme to merge with the default icon theme for [NavigationRailDestination] icons, when the destination is not selected.

### selectedIconTheme

```dart
IconThemeData? selectedIconTheme
```

The theme to merge with the default icon theme for [NavigationRailDestination] icons, when the destination is selected.

### groupAlignment

```dart
double? groupAlignment
```

The alignment for the [NavigationRailDestination]s as they are positioned within the [NavigationRail].

### labelType

```dart
NavigationRailLabelType? labelType
```

The type that defines the layout and behavior of the labels in the [NavigationRail].

### useIndicator

```dart
bool? useIndicator
```

Whether or not the selected [NavigationRailDestination] should include a [NavigationIndicator].

### indicatorColor

```dart
Color? indicatorColor
```

Overrides the default value of [NavigationRail]'s selection indicator color, when [useIndicator] is true.

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

Overrides the default shape of the [NavigationRail]'s selection indicator.

### minWidth

```dart
double? minWidth
```

Overrides the default value of [NavigationRail]'s minimum width when it is not extended.

### minExtendedWidth

```dart
double? minExtendedWidth
```

Overrides the default value of [NavigationRail]'s minimum width when it is extended.

### copyWith()

```dart
NavigationRailThemeData copyWith({Color? backgroundColor, double? elevation, TextStyle? unselectedLabelTextStyle, TextStyle? selectedLabelTextStyle, IconThemeData? unselectedIconTheme, IconThemeData? selectedIconTheme, double? groupAlignment, NavigationRailLabelType? labelType, bool? useIndicator, Color? indicatorColor, ShapeBorder? indicatorShape, double? minWidth, double? minExtendedWidth})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
NavigationRailThemeData? lerp(NavigationRailThemeData? a, NavigationRailThemeData? b, double t)
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

# NavigationRailTheme

```dart
class NavigationRailTheme extends InheritedTheme {}
```

An inherited widget that defines visual properties for [NavigationRail]s and [NavigationRailDestination]s in this widget's subtree.

Values specified here are used for [NavigationRail] properties that are not given an explicit non-null value.

### NavigationRailTheme()

```dart
NavigationRailTheme({dynamic key, required NavigationRailThemeData data, required dynamic child})
```

Creates a navigation rail theme that controls the [NavigationRailThemeData] properties for a [NavigationRail].

### data

```dart
NavigationRailThemeData data
```

Specifies the background color, elevation, label text style, icon theme, group alignment, and label type and border values for descendant [NavigationRail] widgets.

### of()

```dart
NavigationRailThemeData of(BuildContext context)
```

Retrieves the [NavigationRailThemeData] from the closest ancestor [NavigationRailTheme].

If there is no enclosing [NavigationRailTheme] widget, then [ThemeData.navigationRailTheme] is used.

Typical usage is as follows:

```dart
NavigationRailThemeData theme = NavigationRailTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(NavigationRailTheme oldWidget)
```
