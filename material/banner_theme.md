@docImport 'banner.dart';

# MaterialBannerThemeData

```dart
class MaterialBannerThemeData with Diagnosticable {}
```

Defines the visual properties of [MaterialBanner] widgets.

Descendant widgets obtain the current [MaterialBannerThemeData] object using [MaterialBannerTheme.of]. Instances of [MaterialBannerThemeData] can be customized with [MaterialBannerThemeData.copyWith].

Typically a [MaterialBannerThemeData] is specified as part of the overall [Theme] with [ThemeData.bannerTheme].

All [MaterialBannerThemeData] properties are `null` by default. When null, the [MaterialBanner] will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### MaterialBannerThemeData()

```dart
MaterialBannerThemeData({Color? backgroundColor, Color? surfaceTintColor, Color? shadowColor, Color? dividerColor, TextStyle? contentTextStyle, double? elevation, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? leadingPadding})
```

Creates a theme that can be used for [MaterialBannerTheme] or [ThemeData.bannerTheme].

### backgroundColor

```dart
Color? backgroundColor
```

The background color of a [MaterialBanner].

### surfaceTintColor

```dart
Color? surfaceTintColor
```

Overrides the default value of [MaterialBanner.surfaceTintColor].

### shadowColor

```dart
Color? shadowColor
```

Overrides the default value of [MaterialBanner.shadowColor].

### dividerColor

```dart
Color? dividerColor
```

Overrides the default value of [MaterialBanner.dividerColor].

### contentTextStyle

```dart
TextStyle? contentTextStyle
```

Used to configure the [DefaultTextStyle] for the [MaterialBanner.content] widget.

### elevation

```dart
double? elevation
```

Default value for [MaterialBanner.elevation].

### padding

```dart
EdgeInsetsGeometry? padding
```

The amount of space by which to inset [MaterialBanner.content].

### leadingPadding

```dart
EdgeInsetsGeometry? leadingPadding
```

The amount of space by which to inset [MaterialBanner.leading].

### copyWith()

```dart
MaterialBannerThemeData copyWith({Color? backgroundColor, Color? surfaceTintColor, Color? shadowColor, Color? dividerColor, TextStyle? contentTextStyle, double? elevation, EdgeInsetsGeometry? padding, EdgeInsetsGeometry? leadingPadding})
```

Creates a copy of this object with the given fields replaced with the new values.

### lerp()

```dart
MaterialBannerThemeData lerp(MaterialBannerThemeData? a, MaterialBannerThemeData? b, double t)
```

Linearly interpolate between two Banner themes.

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

# MaterialBannerTheme

```dart
class MaterialBannerTheme extends InheritedTheme {}
```

An inherited widget that defines the configuration for [MaterialBanner]s in this widget's subtree.

Values specified here are used for [MaterialBanner] properties that are not given an explicit non-null value.

### MaterialBannerTheme()

```dart
MaterialBannerTheme({dynamic key, MaterialBannerThemeData? data, required dynamic child})
```

Creates a banner theme that controls the configurations for [MaterialBanner]s in its widget subtree.

### data

```dart
MaterialBannerThemeData? data
```

The properties for descendant [MaterialBanner] widgets.

### of()

```dart
MaterialBannerThemeData of(BuildContext context)
```

The closest instance of this class's [data] value that encloses the given context.

If there is no ancestor, it returns [ThemeData.bannerTheme]. Applications can assume that the returned value will not be null.

Typical usage is as follows:

```dart
MaterialBannerThemeData theme = MaterialBannerTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(MaterialBannerTheme oldWidget)
```
