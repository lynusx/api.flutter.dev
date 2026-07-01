@docImport 'badge.dart';

# BadgeThemeData

```dart
class BadgeThemeData with Diagnosticable {}
```

Overrides the default properties values for descendant [Badge] widgets.

Descendant widgets obtain the current [BadgeThemeData] object using [BadgeTheme.of]. Instances of [BadgeThemeData] can be customized with [BadgeThemeData.copyWith].

Typically a [BadgeThemeData] is specified as part of the overall [Theme] with [ThemeData.badgeTheme].

All [BadgeThemeData] properties are `null` by default. When null, the [Badge] will use the values from [ThemeData] if they exist, otherwise it will provide its own defaults.

See also:

- [ThemeData], which describes the overall theme information for the application.

### BadgeThemeData()

```dart
BadgeThemeData({Color? backgroundColor, Color? textColor, double? smallSize, double? largeSize, TextStyle? textStyle, EdgeInsetsGeometry? padding, AlignmentGeometry? alignment, Offset? offset})
```

Creates the set of color, style, and size properties used to configure [Badge].

### backgroundColor

```dart
Color? backgroundColor
```

Overrides the default value for [Badge.backgroundColor].

### textColor

```dart
Color? textColor
```

Overrides the default value for [Badge.textColor].

### smallSize

```dart
double? smallSize
```

Overrides the default value for [Badge.smallSize].

### largeSize

```dart
double? largeSize
```

Overrides the default value for [Badge.largeSize].

### textStyle

```dart
TextStyle? textStyle
```

Overrides the default value for [Badge.textStyle].

### padding

```dart
EdgeInsetsGeometry? padding
```

Overrides the default value for [Badge.padding].

### alignment

```dart
AlignmentGeometry? alignment
```

Overrides the default value for [Badge.alignment].

### offset

```dart
Offset? offset
```

Overrides the default value for [Badge.offset].

### copyWith()

```dart
BadgeThemeData copyWith({Color? backgroundColor, Color? textColor, double? smallSize, double? largeSize, TextStyle? textStyle, EdgeInsetsGeometry? padding, AlignmentGeometry? alignment, Offset? offset})
```

Creates a copy of this object but with the given fields replaced with the new values.

### lerp()

```dart
BadgeThemeData lerp(BadgeThemeData? a, BadgeThemeData? b, double t)
```

Linearly interpolate between two [Badge] themes.

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

# BadgeTheme

```dart
class BadgeTheme extends InheritedTheme {}
```

An inherited widget that overrides the default color style, and size parameters for [Badge]s in this widget's subtree.

Values specified here override the defaults for [Badge] properties which are not given an explicit non-null value.

### BadgeTheme()

```dart
BadgeTheme({dynamic key, required BadgeThemeData data, required dynamic child})
```

Creates a theme that overrides the default color parameters for [Badge]s in this widget's subtree.

### data

```dart
BadgeThemeData data
```

Specifies the default color and size overrides for descendant [Badge] widgets.

### of()

```dart
BadgeThemeData of(BuildContext context)
```

Retrieves the [BadgeThemeData] from the closest ancestor [BadgeTheme].

If there is no enclosing [BadgeTheme] widget, then [ThemeData.badgeTheme] is used.

Typical usage is as follows:

```dart
BadgeThemeData theme = BadgeTheme.of(context);
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### updateShouldNotify()

```dart
bool updateShouldNotify(BadgeTheme oldWidget)
```
