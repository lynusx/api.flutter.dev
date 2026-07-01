# TabBarTheme

```dart
class TabBarTheme extends InheritedTheme with Diagnosticable {}
```

Defines default property values for descendant [TabBar] widgets.

Descendant widgets obtain the current [TabBarThemeData] object using [TabBarTheme.of]. Instances of [TabBarThemeData] can be customized with [TabBarThemeData.copyWith].

Typically a [TabBarThemeData] is specified as part of the overall [Theme] with [ThemeData.tabBarTheme].

See also:

- [TabBarThemeData], which describes the actual configuration of a tab bar theme.

### TabBarTheme()

```dart
TabBarTheme({dynamic key, Decoration? indicator, Color? indicatorColor, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, EdgeInsetsGeometry? labelPadding, TextStyle? labelStyle, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, WidgetStateProperty<Color?>? overlayColor, InteractiveInkFeatureFactory? splashFactory, WidgetStateProperty<MouseCursor?>? mouseCursor, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation, TabBarThemeData? data, Widget? child})
```

Creates a tab bar theme that can be used with [ThemeData.tabBarTheme].

### indicator

```dart
Decoration? get indicator
```

Overrides the default value for [TabBar.indicator].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.indicator] property in [data] instead.

### indicatorColor

```dart
Color? get indicatorColor
```

Overrides the default value for [TabBar.indicatorColor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.indicatorColor] property in [data] instead.

### indicatorSize

```dart
TabBarIndicatorSize? get indicatorSize
```

Overrides the default value for [TabBar.indicatorSize].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.indicatorSize] property in [data] instead.

### dividerColor

```dart
Color? get dividerColor
```

Overrides the default value for [TabBar.dividerColor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.dividerColor] property in [data] instead.

### dividerHeight

```dart
double? get dividerHeight
```

Overrides the default value for [TabBar.dividerHeight].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.dividerHeight] property in [data] instead.

### labelColor

```dart
Color? get labelColor
```

Overrides the default value for [TabBar.labelColor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.labelColor] property in [data] instead.

### labelPadding

```dart
EdgeInsetsGeometry? get labelPadding
```

Overrides the default value for [TabBar.labelPadding].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.labelPadding] property in [data] instead.

### labelStyle

```dart
TextStyle? get labelStyle
```

Overrides the default value for [TabBar.labelStyle].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.labelStyle] property in [data] instead.

### unselectedLabelColor

```dart
Color? get unselectedLabelColor
```

Overrides the default value for [TabBar.unselectedLabelColor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.unselectedLabelColor] property in [data] instead.

### unselectedLabelStyle

```dart
TextStyle? get unselectedLabelStyle
```

Overrides the default value for [TabBar.unselectedLabelStyle].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.unselectedLabelStyle] property in [data] instead.

### overlayColor

```dart
WidgetStateProperty<Color?>? get overlayColor
```

Overrides the default value for [TabBar.overlayColor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.overlayColor] property in [data] instead.

### splashFactory

```dart
InteractiveInkFeatureFactory? get splashFactory
```

Overrides the default value for [TabBar.splashFactory].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.splashFactory] property in [data] instead.

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? get mouseCursor
```

Overrides the default value of [TabBar.mouseCursor].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.mouseCursor] property in [data] instead.

### tabAlignment

```dart
TabAlignment? get tabAlignment
```

Overrides the default value for [TabBar.tabAlignment].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.tabAlignment] property in [data] instead.

### textScaler

```dart
TextScaler? get textScaler
```

Overrides the default value for [TabBar.textScaler].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.textScaler] property in [data] instead.

### indicatorAnimation

```dart
TabIndicatorAnimation? get indicatorAnimation
```

Overrides the default value for [TabBar.indicatorAnimation].

This property is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.indicatorAnimation] property in [data] instead.

### data

```dart
TabBarThemeData get data
```

The properties used for all descendant [TabBar] widgets.

### copyWith()

```dart
TabBarTheme copyWith({Decoration? indicator, Color? indicatorColor, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, EdgeInsetsGeometry? labelPadding, TextStyle? labelStyle, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, WidgetStateProperty<Color?>? overlayColor, InteractiveInkFeatureFactory? splashFactory, WidgetStateProperty<MouseCursor?>? mouseCursor, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation})
```

Creates a copy of this object but with the given fields replaced with the new values.

This method is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.copyWith] instead.

### of()

```dart
TabBarThemeData of(BuildContext context)
```

Returns the configuration [data] from the closest [TabBarTheme] ancestor. If there is no ancestor, it returns [ThemeData.tabBarTheme].

Typical usage is as follows:

```dart
TabBarThemeData theme = TabBarTheme.of(context);
```

### lerp()

```dart
TabBarTheme lerp(TabBarTheme a, TabBarTheme b, double t)
```

Linearly interpolate between two tab bar themes.

{@macro dart.ui.shadow.lerp}

This method is obsolete and will be deprecated in a future release: please use the [TabBarThemeData.lerp] instead.

### updateShouldNotify()

```dart
bool updateShouldNotify(TabBarTheme oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

# TabBarThemeData

```dart
class TabBarThemeData with Diagnosticable {}
```

Defines default property values for descendant [TabBar] widgets.

Descendant widgets obtain the current [TabBarThemeData] object using [TabBarTheme.of]. Instances of [TabBarThemeData] can be customized with [TabBarThemeData.copyWith].

Typically a [TabBarThemeData] is specified as part of the overall [Theme] with [ThemeData.tabBarTheme].

All [TabBarThemeData] properties are `null` by default. When null, the [TabBar] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults. See the individual [TabBar] properties for details.

See also:

- [TabBar], which displays a row of tabs.
- [ThemeData], which describes the overall theme information for the application.

### TabBarThemeData()

```dart
TabBarThemeData({Decoration? indicator, Color? indicatorColor, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, EdgeInsetsGeometry? labelPadding, TextStyle? labelStyle, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, WidgetStateProperty<Color?>? overlayColor, InteractiveInkFeatureFactory? splashFactory, WidgetStateProperty<MouseCursor?>? mouseCursor, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation, BorderRadius? splashBorderRadius})
```

Creates a tab bar theme that can be used with [ThemeData.tabBarTheme].

### indicator

```dart
Decoration? indicator
```

Overrides the default value for [TabBar.indicator].

### indicatorColor

```dart
Color? indicatorColor
```

Overrides the default value for [TabBar.indicatorColor].

### indicatorSize

```dart
TabBarIndicatorSize? indicatorSize
```

Overrides the default value for [TabBar.indicatorSize].

### dividerColor

```dart
Color? dividerColor
```

Overrides the default value for [TabBar.dividerColor].

### dividerHeight

```dart
double? dividerHeight
```

Overrides the default value for [TabBar.dividerHeight].

### labelColor

```dart
Color? labelColor
```

Overrides the default value for [TabBar.labelColor].

If [labelColor] is a [WidgetStateColor], then the effective color will depend on the [WidgetState.selected] state, i.e. if the [Tab] is selected or not. In case of unselected state, this [WidgetStateColor]'s resolved color will be used even if [TabBar.unselectedLabelColor] or [unselectedLabelColor] is non-null.

### labelPadding

```dart
EdgeInsetsGeometry? labelPadding
```

Overrides the default value for [TabBar.labelPadding].

If there are few tabs with both icon and text and few tabs with only icon or text, this padding is vertically adjusted to provide uniform padding to all tabs.

### labelStyle

```dart
TextStyle? labelStyle
```

Overrides the default value for [TabBar.labelStyle].

### unselectedLabelColor

```dart
Color? unselectedLabelColor
```

Overrides the default value for [TabBar.unselectedLabelColor].

### unselectedLabelStyle

```dart
TextStyle? unselectedLabelStyle
```

Overrides the default value for [TabBar.unselectedLabelStyle].

### overlayColor

```dart
WidgetStateProperty<Color?>? overlayColor
```

Overrides the default value for [TabBar.overlayColor].

### splashFactory

```dart
InteractiveInkFeatureFactory? splashFactory
```

Overrides the default value for [TabBar.splashFactory].

### mouseCursor

```dart
WidgetStateProperty<MouseCursor?>? mouseCursor
```

{@macro flutter.material.tabs.mouseCursor}

If specified, overrides the default value of [TabBar.mouseCursor].

### tabAlignment

```dart
TabAlignment? tabAlignment
```

Overrides the default value for [TabBar.tabAlignment].

### textScaler

```dart
TextScaler? textScaler
```

Overrides the default value for [TabBar.textScaler].

### indicatorAnimation

```dart
TabIndicatorAnimation? indicatorAnimation
```

Overrides the default value for [TabBar.indicatorAnimation].

### splashBorderRadius

```dart
BorderRadius? splashBorderRadius
```

Defines the clipping radius of splashes that extend outside the bounds of the tab.

### copyWith()

```dart
TabBarThemeData copyWith({Decoration? indicator, Color? indicatorColor, TabBarIndicatorSize? indicatorSize, Color? dividerColor, double? dividerHeight, Color? labelColor, EdgeInsetsGeometry? labelPadding, TextStyle? labelStyle, Color? unselectedLabelColor, TextStyle? unselectedLabelStyle, WidgetStateProperty<Color?>? overlayColor, InteractiveInkFeatureFactory? splashFactory, WidgetStateProperty<MouseCursor?>? mouseCursor, TabAlignment? tabAlignment, TextScaler? textScaler, TabIndicatorAnimation? indicatorAnimation, BorderRadius? splashBorderRadius})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
TabBarThemeData lerp(TabBarThemeData a, TabBarThemeData b, double t)
```

Linearly interpolate between two tab bar themes.

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
