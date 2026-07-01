@docImport 'app_bar.dart';

# AppBarTheme

```dart
class AppBarTheme extends InheritedTheme with Diagnosticable {}
```

Defines default property values for descendant [AppBar] widgets.

Descendant widgets obtain the current [AppBarThemeData] object with [AppBarTheme.of]. Instances of [AppBarThemeData] can be customized with [AppBarThemeData.copyWith].

Typically an [AppBarThemeData] is specified as part of the overall [Theme] with [ThemeData.appBarTheme].

All [AppBarTheme] properties are `null` by default. When null, the

See also:

- [ThemeData], which describes the overall theme information for the application.

### AppBarTheme()

```dart
AppBarTheme({dynamic key, Color? color, Color? backgroundColor, Color? foregroundColor, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool? centerTitle, double? titleSpacing, double? leadingWidth, double? toolbarHeight, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, EdgeInsetsGeometry? actionsPadding, AppBarThemeData? data, Widget? child})
```

Creates a theme that can be used for [ThemeData.appBarTheme].

### backgroundColor

```dart
Color? get backgroundColor
```

Overrides the default value of [AppBar.backgroundColor] in all descendant [AppBar] widgets.

See also:

- [foregroundColor], which overrides the default value of [AppBar.foregroundColor] in all descendant [AppBar] widgets.

### foregroundColor

```dart
Color? get foregroundColor
```

Overrides the default value of [AppBar.foregroundColor] in all descendant [AppBar] widgets.

See also:

- [backgroundColor], which overrides the default value of [AppBar.backgroundColor] in all descendant [AppBar] widgets.

### elevation

```dart
double? get elevation
```

Overrides the default value of [AppBar.elevation] in all descendant [AppBar] widgets.

### scrolledUnderElevation

```dart
double? get scrolledUnderElevation
```

Overrides the default value of [AppBar.scrolledUnderElevation] in all descendant [AppBar] widgets.

### shadowColor

```dart
Color? get shadowColor
```

Overrides the default value of [AppBar.shadowColor] in all descendant [AppBar] widgets.

### surfaceTintColor

```dart
Color? get surfaceTintColor
```

Overrides the default value of [AppBar.surfaceTintColor] in all descendant [AppBar] widgets.

### shape

```dart
ShapeBorder? get shape
```

Overrides the default value of [AppBar.shape] in all descendant [AppBar] widgets.

### iconTheme

```dart
IconThemeData? get iconTheme
```

Overrides the default value of [AppBar.iconTheme] in all descendant [AppBar] widgets.

See also:

- [actionsIconTheme], which overrides the default value of [AppBar.actionsIconTheme] in all descendant [AppBar] widgets.
- [foregroundColor], which overrides the default value [AppBar.foregroundColor] in all descendant [AppBar] widgets.

### actionsIconTheme

```dart
IconThemeData? get actionsIconTheme
```

Overrides the default value of [AppBar.actionsIconTheme] in all descendant [AppBar] widgets.

See also:

- [iconTheme], which overrides the default value of [AppBar.iconTheme] in all descendant [AppBar] widgets.
- [foregroundColor], which overrides the default value [AppBar.foregroundColor] in all descendant [AppBar] widgets.

### centerTitle

```dart
bool? get centerTitle
```

Overrides the default value of [AppBar.centerTitle] property in all descendant [AppBar] widgets.

### titleSpacing

```dart
double? get titleSpacing
```

Overrides the default value of the obsolete [AppBar.titleSpacing] property in all descendant [AppBar] widgets.

If null, [AppBar] uses default value of [NavigationToolbar.kMiddleSpacing].

### leadingWidth

```dart
double? get leadingWidth
```

Overrides the default value of the [AppBar.leadingWidth] property in all descendant [AppBar] widgets.

### toolbarHeight

```dart
double? get toolbarHeight
```

Overrides the default value of the [AppBar.toolbarHeight] property in all descendant [AppBar] widgets.

See also:

- [AppBar.preferredHeightFor], which computes the overall height of an AppBar widget, taking this value into account.

### toolbarTextStyle

```dart
TextStyle? get toolbarTextStyle
```

Overrides the default value of the obsolete [AppBar.toolbarTextStyle] property in all descendant [AppBar] widgets.

See also:

- [titleTextStyle], which overrides the default of [AppBar.titleTextStyle] in all descendant [AppBar] widgets.

### titleTextStyle

```dart
TextStyle? get titleTextStyle
```

Overrides the default value of [AppBar.titleTextStyle] property in all descendant [AppBar] widgets.

See also:

- [toolbarTextStyle], which overrides the default of [AppBar.toolbarTextStyle] in all descendant [AppBar] widgets.

### systemOverlayStyle

```dart
SystemUiOverlayStyle? get systemOverlayStyle
```

Overrides the default value of [AppBar.systemOverlayStyle] property in all descendant [AppBar] widgets.

### actionsPadding

```dart
EdgeInsetsGeometry? get actionsPadding
```

Overrides the default value of [AppBar.actionsPadding] property in all descendant [AppBar] widgets.

### data

```dart
AppBarThemeData get data
```

The properties used for all descendant [AppBar] widgets.

### copyWith()

```dart
AppBarTheme copyWith({IconThemeData? actionsIconTheme, Color? color, Color? backgroundColor, Color? foregroundColor, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, IconThemeData? iconTheme, bool? centerTitle, double? titleSpacing, double? leadingWidth, double? toolbarHeight, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, EdgeInsetsGeometry? actionsPadding})
```

Creates a copy of this object with the given fields replaced with the new values.

This method is obsolete and will be deprecated in a future release: please use the [AppBarThemeData.copyWith] method instead.

### of()

```dart
AppBarThemeData of(BuildContext context)
```

Retrieves the [AppBarThemeData] from the closest ancestor [AppBarTheme].

If there is no enclosing [AppBarTheme] widget, then [ThemeData.appBarTheme] is used.

Typical usage is as follows:

```dart
AppBarThemeData theme = AppBarTheme.of(context);
```

### lerp()

```dart
AppBarTheme lerp(AppBarTheme? a, AppBarTheme? b, double t)
```

Linearly interpolate between two AppBar themes.

{@macro dart.ui.shadow.lerp}

### updateShouldNotify()

```dart
bool updateShouldNotify(AppBarTheme oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

# AppBarThemeData

```dart
class AppBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [AppBar] widgets.

Descendant widgets obtain the current [AppBarThemeData] object using [AppBarTheme.of]. Instances of [AppBarThemeData] can be customized with [AppBarThemeData.copyWith].

Typically an [AppBarThemeData] is specified as part of the overall [Theme] with [ThemeData.appBarTheme].

All [AppBarThemeData] properties are `null` by default. When null, the [AppBar] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults. See the individual [AppBar] properties for details.

See also:

- [AppBar], which is the widget that this theme configures.
- [ThemeData], which describes the overall theme information for the application.

### AppBarThemeData()

```dart
AppBarThemeData({Color? backgroundColor, Color? foregroundColor, Color? color, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool? centerTitle, double? titleSpacing, double? leadingWidth, double? toolbarHeight, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, EdgeInsetsGeometry? actionsPadding})
```

Creates an app bar theme that can be used with [ThemeData.appBarTheme].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value of [AppBar.backgroundColor].

### foregroundColor

```dart
Color? foregroundColor
```

Overrides the default value of [AppBar.foregroundColor].

### elevation

```dart
double? elevation
```

Overrides the default value of [AppBar.elevation].

### scrolledUnderElevation

```dart
double? scrolledUnderElevation
```

Overrides the default value of [AppBar.scrolledUnderElevation].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value of [AppBar.shadowColor].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of [AppBar.surfaceTintColor].

### shape

```dart
ShapeBorder? shape
```

Overrides the default value of [AppBar.shape].

### iconTheme

```dart
IconThemeData? iconTheme
```

Overrides the default value of [AppBar.iconTheme].

### actionsIconTheme

```dart
IconThemeData? actionsIconTheme
```

Overrides the default value of [AppBar.actionsIconTheme].

### centerTitle

```dart
bool? centerTitle
```

Overrides the default value of [AppBar.centerTitle].

### titleSpacing

```dart
double? titleSpacing
```

Overrides the default value of [AppBar.titleSpacing].

### leadingWidth

```dart
double? leadingWidth
```

Overrides the default value of [AppBar.leadingWidth].

### toolbarHeight

```dart
double? toolbarHeight
```

Overrides the default value of [AppBar.toolbarHeight].

### toolbarTextStyle

```dart
TextStyle? toolbarTextStyle
```

Overrides the default value of [AppBar.toolbarTextStyle].

### titleTextStyle

```dart
TextStyle? titleTextStyle
```

Overrides the default value of [AppBar.titleTextStyle].

### systemOverlayStyle

```dart
SystemUiOverlayStyle? systemOverlayStyle
```

Overrides the default value of [AppBar.systemOverlayStyle].

### actionsPadding

```dart
EdgeInsetsGeometry? actionsPadding
```

Overrides the default value of [AppBar.actionsPadding].

### copyWith()

```dart
AppBarThemeData copyWith({Color? backgroundColor, Color? foregroundColor, Color? color, double? elevation, double? scrolledUnderElevation, Color? shadowColor, Color? surfaceTintColor, ShapeBorder? shape, IconThemeData? iconTheme, IconThemeData? actionsIconTheme, bool? centerTitle, double? titleSpacing, double? leadingWidth, double? toolbarHeight, TextStyle? toolbarTextStyle, TextStyle? titleTextStyle, SystemUiOverlayStyle? systemOverlayStyle, EdgeInsetsGeometry? actionsPadding})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
AppBarThemeData lerp(AppBarThemeData a, AppBarThemeData b, double t)
```

Linearly interpolate between two app bar themes.

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
