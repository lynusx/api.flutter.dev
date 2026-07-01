# BottomNavigationBarThemeData

```dart
class BottomNavigationBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [BottomNavigationBar] widgets.

Descendant widgets obtain the current [BottomNavigationBarThemeData] object using [BottomNavigationBarTheme.of]. Instances of [BottomNavigationBarThemeData] can be customized with [BottomNavigationBarThemeData.copyWith].

Typically a [BottomNavigationBarThemeData] is specified as part of the overall [Theme] with [ThemeData.bottomNavigationBarTheme].

All [BottomNavigationBarThemeData] properties are `null` by default. When null, the [BottomNavigationBar]'s build method provides defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### BottomNavigationBarThemeData()

```dart
BottomNavigationBarThemeData({Color? backgroundColor, double? elevation, IconThemeData? selectedIconTheme, IconThemeData? unselectedIconTheme, Color? selectedItemColor, Color? unselectedItemColor, TextStyle? selectedLabelStyle, TextStyle? unselectedLabelStyle, bool? showSelectedLabels, bool? showUnselectedLabels, BottomNavigationBarType? type, bool? enableFeedback, BottomNavigationBarLandscapeLayout? landscapeLayout, WidgetStateProperty<MouseCursor?>? mouseCursor})
```

Creates a theme that can be used for [ThemeData.bottomNavigationBarTheme].

### backgroundColor

```dart
Color? backgroundColor
```

The color of the [BottomNavigationBar] itself.

See [BottomNavigationBar.backgroundColor].

### elevation

```dart
double? elevation
```

The z-coordinate of the [BottomNavigationBar].

See [BottomNavigationBar.elevation].

### selectedIconTheme

```dart
IconThemeData? selectedIconTheme
```

The size, opacity, and color of the icon in the currently selected [BottomNavigationBarItem.icon].

If [BottomNavigationBar.selectedIconTheme] is non-null on the widget, the whole [IconThemeData] from the widget will be used over this [selectedIconTheme].

See [BottomNavigationBar.selectedIconTheme].

### unselectedIconTheme

```dart
IconThemeData? unselectedIconTheme
```

The size, opacity, and color of the icon in the currently unselected [BottomNavigationBarItem.icon]s.

If [BottomNavigationBar.unselectedIconTheme] is non-null on the widget, the whole [IconThemeData] from the widget will be used over this [unselectedIconTheme].

See [BottomNavigationBar.unselectedIconTheme].

### selectedItemColor

```dart
Color? selectedItemColor
```

The color of the selected [BottomNavigationBarItem.icon] and [BottomNavigationBarItem.label].

See [BottomNavigationBar.selectedItemColor].

### unselectedItemColor

```dart
Color? unselectedItemColor
```

The color of the unselected [BottomNavigationBarItem.icon] and [BottomNavigationBarItem.label]s.

See [BottomNavigationBar.unselectedItemColor].

### selectedLabelStyle

```dart
TextStyle? selectedLabelStyle
```

The [TextStyle] of the [BottomNavigationBarItem] labels when they are selected.

See [BottomNavigationBar.selectedLabelStyle].

### unselectedLabelStyle

```dart
TextStyle? unselectedLabelStyle
```

The [TextStyle] of the [BottomNavigationBarItem] labels when they are not selected.

See [BottomNavigationBar.unselectedLabelStyle].

### showSelectedLabels

```dart
bool? showSelectedLabels
```

Whether the labels are shown for the selected [BottomNavigationBarItem].

See [BottomNavigationBar.showSelectedLabels].

### showUnselectedLabels

```dart
bool? showUnselectedLabels
```

Whether the labels are shown for the unselected [BottomNavigationBarItem]s.

See [BottomNavigationBar.showUnselectedLabels].

### type

```dart
BottomNavigationBarType? type
```

Defines the layout and behavior of a [BottomNavigationBar].

See [BottomNavigationBar.type].

### enableFeedback

```dart
bool? enableFeedback
```

If specified, defines the feedback property for [BottomNavigationBar].

If [BottomNavigationBar.enableFeedback] is provided, [enableFeedback] is ignored.

### landscapeLayout

```dart
BottomNavigationBarLandscapeLayout? landscapeLayout
```

If non-null, overrides the [BottomNavigationBar.landscapeLayout] property.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

If specified, overrides the default value of [BottomNavigationBar.mouseCursor].

### copyWith()

```dart
BottomNavigationBarThemeData copyWith({Color? backgroundColor, double? elevation, IconThemeData? selectedIconTheme, IconThemeData? unselectedIconTheme, Color? selectedItemColor, Color? unselectedItemColor, TextStyle? selectedLabelStyle, TextStyle? unselectedLabelStyle, bool? showSelectedLabels, bool? showUnselectedLabels, BottomNavigationBarType? type, bool? enableFeedback, BottomNavigationBarLandscapeLayout? landscapeLayout, WidgetStateProperty<MouseCursor?>? mouseCursor})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
BottomNavigationBarThemeData lerp(BottomNavigationBarThemeData? a, BottomNavigationBarThemeData? b, double t)
```

Linearly interpolate between two [BottomNavigationBarThemeData].

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

# BottomNavigationBarTheme

```dart
class BottomNavigationBarTheme extends InheritedWidget {}
```

Applies a bottom navigation bar theme to descendant [BottomNavigationBar] widgets.

Descendant widgets obtain the current theme's [BottomNavigationBarTheme] object using [BottomNavigationBarTheme.of]. When a widget uses [BottomNavigationBarTheme.of], it is automatically rebuilt if the theme later changes.

A bottom navigation theme can be specified as part of the overall Material theme using [ThemeData.bottomNavigationBarTheme].

See also:

- [BottomNavigationBarThemeData], which describes the actual configuration of a bottom navigation bar theme.

### BottomNavigationBarTheme()

```dart
BottomNavigationBarTheme({dynamic key, required BottomNavigationBarThemeData data, required dynamic child})
```

Constructs a bottom navigation bar theme that configures all descendant [BottomNavigationBar] widgets.

### data

```dart
BottomNavigationBarThemeData data
```

The properties used for all descendant [BottomNavigationBar] widgets.

### of()

```dart
BottomNavigationBarThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [BottomNavigationBarTheme] ancestor. If there is no ancestor, it returns [ThemeData.bottomNavigationBarTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
BottomNavigationBarThemeData theme = BottomNavigationBarTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(BottomNavigationBarTheme oldWidget)
```
