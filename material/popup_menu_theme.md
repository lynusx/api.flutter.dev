@docImport 'popup_menu.dart';

# PopupMenuPosition

```dart
enum PopupMenuPosition {}
```

Used to configure how the [PopupMenuButton] positions its popup menu.

Menu is positioned over the anchor.

Menu is positioned under the anchor.

# PopupMenuThemeData

```dart
class PopupMenuThemeData with Diagnosticable {}
```

Defines the visual properties of the routes used to display popup menus as well as [PopupMenuItem] and [PopupMenuDivider] widgets.

Descendant widgets obtain the current [PopupMenuThemeData] object using [PopupMenuTheme.of]. Instances of [PopupMenuThemeData] can be customized with [PopupMenuThemeData.copyWith].

Typically, a [PopupMenuThemeData] is specified as part of the overall [Theme] with [ThemeData.popupMenuTheme]. Otherwise, [PopupMenuTheme] can be used to configure its own widget subtree.

All [PopupMenuThemeData] properties are `null` by default. If any of these properties are null, the popup menu will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### PopupMenuThemeData()

```dart
PopupMenuThemeData({Color? color, ShapeBorder? shape, EdgeInsetsGeometry? menuPadding, double? elevation, Color? shadowColor, Color? surfaceTintColor, TextStyle? textStyle, WidgetStateProperty<TextStyle?>? labelTextStyle, bool? enableFeedback, WidgetStateProperty<MouseCursor?>? mouseCursor, PopupMenuPosition? position, Color? iconColor, double? iconSize})
```

Creates the set of properties used to configure [PopupMenuTheme].

### color

```dart
Color? color
```

The background color of the popup menu.

### shape

```dart
ShapeBorder? shape
```

The shape of the popup menu.

### menuPadding

```dart
EdgeInsetsGeometry? menuPadding
```

If specified, the padding of the popup menu.

If [PopupMenuButton.menuPadding] is provided, [menuPadding] is ignored.

### elevation

```dart
double? elevation
```

The elevation of the popup menu.

### shadowColor

```dart
Color? shadowColor
```

The color used to paint shadow below the popup menu.

### surfaceTintColor

```dart
Color? surfaceTintColor
```

The color used as an overlay on [color] of the popup menu.

### textStyle

```dart
TextStyle? textStyle
```

The text style of items in the popup menu.

### labelTextStyle

```dart
WidgetStateProperty<TextStyle?>? labelTextStyle
```

You can use this to specify a different style of the label when the popup menu item is enabled and disabled.

### enableFeedback

```dart
bool? enableFeedback
```

If specified, defines the feedback property for [PopupMenuButton].

If [PopupMenuButton.enableFeedback] is provided, [enableFeedback] is ignored.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.popupmenu.mouseCursor}

If specified, overrides the default value of [PopupMenuItem.mouseCursor].

### position

```dart
PopupMenuPosition? position
```

Whether the popup menu is positioned over or under the popup menu button.

When not set, the position defaults to [PopupMenuPosition.over] which makes the popup menu appear directly over the button that was used to create it.

### iconColor

```dart
Color? iconColor
```

The color of the icon in the popup menu button.

### iconSize

```dart
double? iconSize
```

The size of the icon in the popup menu button.

### copyWith()

```dart
PopupMenuThemeData copyWith({Color? color, ShapeBorder? shape, EdgeInsetsGeometry? menuPadding, double? elevation, Color? shadowColor, Color? surfaceTintColor, TextStyle? textStyle, WidgetStateProperty<TextStyle?>? labelTextStyle, bool? enableFeedback, WidgetStateProperty<MouseCursor?>? mouseCursor, PopupMenuPosition? position, Color? iconColor, double? iconSize})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
PopupMenuThemeData? lerp(PopupMenuThemeData? a, PopupMenuThemeData? b, double t)
```

Linearly interpolate between two popup menu themes.

If both arguments are null, then null is returned.

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

# PopupMenuTheme

```dart
class PopupMenuTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for popup menus in this widget's subtree.

Values specified here are used for popup menu properties that are not given an explicit non-null value.

### PopupMenuTheme()

```dart
PopupMenuTheme({dynamic key, required PopupMenuThemeData data, required dynamic child})
```

Creates a popup menu theme that controls the configurations for popup menus in its widget subtree.

### data

```dart
PopupMenuThemeData data
```

The properties for descendant popup menu widgets.

### of()

```dart
PopupMenuThemeData of(BuildContext context)
```

The closest instance of this class's [data] value that encloses the given context. If there is no ancestor, it returns [ThemeData.popupMenuTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
PopupMenuThemeData theme = PopupMenuTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(PopupMenuTheme oldWidget)
```
