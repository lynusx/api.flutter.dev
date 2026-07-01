# NavigationBarThemeData

```dart
class NavigationBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [NavigationBar] widgets.

Descendant widgets obtain the current [NavigationBarThemeData] object using [NavigationBarTheme.of]. Instances of [NavigationBarThemeData] can be customized with [NavigationBarThemeData.copyWith].

Typically a [NavigationBarThemeData] is specified as part of the overall [Theme] with [ThemeData.navigationBarTheme]. Alternatively, a [NavigationBarTheme] inherited widget can be used to theme [NavigationBar]s in a subtree of widgets.

All [NavigationBarThemeData] properties are `null` by default. When null, the [NavigationBar] will provide its own defaults based on the overall [Theme]'s textTheme and colorScheme. See the individual [NavigationBar] properties for details.

See also:

- [ThemeData], which describes the overall theme information for the application.

### NavigationBarThemeData()

```dart
NavigationBarThemeData({double? height, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Color? indicatorColor, ShapeBorder? indicatorShape, WidgetStateProperty<TextStyle?>? labelTextStyle, WidgetStateProperty<IconThemeData?>? iconTheme, NavigationDestinationLabelBehavior? labelBehavior, WidgetStateProperty<Color?>? overlayColor, EdgeInsetsGeometry? labelPadding})
```

Creates a theme that can be used for [ThemeData.navigationBarTheme] and [NavigationBarTheme].

### height

```dart
double? height
```

Overrides the default value of [NavigationBar.height].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [NavigationBar.backgroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value of [NavigationBar.elevation].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value of [NavigationBar.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of [NavigationBar.surfaceTintColor].

### indicatorColor

```dart
Color? indicatorColor
```

Overrides the default value of [NavigationBar]'s selection indicator.

### indicatorShape

```dart
ShapeBorder? indicatorShape
```

Overrides the default shape of the [NavigationBar]'s selection indicator.

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

### labelBehavior

```dart
NavigationDestinationLabelBehavior? labelBehavior
```

Overrides the default value of [NavigationBar.labelBehavior].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

Overrides the default value of [NavigationBar.overlayColor].

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

Overrides the default value of [NavigationBar.labelPadding].

### copyWith()

```dart
NavigationBarThemeData copyWith({double? height, Color? backgroundColor, double? elevation, Color? shadowColor, Color? surfaceTintColor, Color? indicatorColor, ShapeBorder? indicatorShape, WidgetStateProperty<TextStyle?>? labelTextStyle, WidgetStateProperty<IconThemeData?>? iconTheme, NavigationDestinationLabelBehavior? labelBehavior, WidgetStateProperty<Color?>? overlayColor, EdgeInsetsGeometry? labelPadding})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
NavigationBarThemeData? lerp(NavigationBarThemeData? a, NavigationBarThemeData? b, double t)
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

# NavigationBarTheme

```dart
class NavigationBarTheme extends InheritedTheme {}
```

An inherited widget that defines visual properties for [NavigationBar]s and [NavigationDestination]s in this widget's subtree.

Values specified here are used for [NavigationBar] properties that are not given an explicit non-null value.

See also:

- [ThemeData.navigationBarTheme], which describes the [NavigationBarThemeData] in the overall theme for the application.

### NavigationBarTheme()

```dart
NavigationBarTheme({dynamic key, required NavigationBarThemeData data, required dynamic child})
```

Creates a navigation rail theme that controls the [NavigationBarThemeData] properties for a [NavigationBar].

### data

```dart
NavigationBarThemeData data
```

Specifies the background color, label text style, icon theme, and label type values for descendant [NavigationBar] widgets.

### of()

```dart
NavigationBarThemeData of(BuildContext context)
```

Retrieves the [NavigationBarThemeData] from the closest ancestor [NavigationBarTheme].

If there is no enclosing [NavigationBarTheme] widget, then [ThemeData.navigationBarTheme] is used.

Typical usage is as follows:

```dart
NavigationBarThemeData theme = NavigationBarTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(NavigationBarTheme oldWidget)
```
