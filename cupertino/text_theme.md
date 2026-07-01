@docImport 'interface_level.dart'; @docImport 'theme.dart';

# CupertinoTextThemeData

```dart
class CupertinoTextThemeData with Diagnosticable {}
```

Cupertino typography theme in a [CupertinoThemeData].

### CupertinoTextThemeData()

```dart
CupertinoTextThemeData({Color primaryColor = CupertinoColors.systemBlue, TextStyle? textStyle, TextStyle? actionTextStyle, TextStyle? actionSmallTextStyle, TextStyle? tabLabelTextStyle, TextStyle? navTitleTextStyle, TextStyle? navLargeTitleTextStyle, TextStyle? navActionTextStyle, TextStyle? pickerTextStyle, TextStyle? dateTimePickerTextStyle})
```

Create a [CupertinoTextThemeData].

The [primaryColor] is used to derive TextStyle defaults of other attributes such as [navActionTextStyle] and [actionTextStyle]. It must not be null when either [navActionTextStyle] or [actionTextStyle] is null. Defaults to [CupertinoColors.systemBlue].

Other [TextStyle] parameters default to default iOS text styles when unspecified.

### textStyle

```dart
TextStyle get textStyle
```

The [TextStyle] of general text content for Cupertino widgets.

### actionTextStyle

```dart
TextStyle get actionTextStyle
```

The [TextStyle] of interactive text content such as text in a button without background.

### actionSmallTextStyle

```dart
TextStyle get actionSmallTextStyle
```

The [TextStyle] of interactive text content such as text in a small button.

### tabLabelTextStyle

```dart
TextStyle get tabLabelTextStyle
```

The [TextStyle] of unselected tabs.

### navTitleTextStyle

```dart
TextStyle get navTitleTextStyle
```

The [TextStyle] of titles in standard navigation bars.

### navLargeTitleTextStyle

```dart
TextStyle get navLargeTitleTextStyle
```

The [TextStyle] of large titles in sliver navigation bars.

### navActionTextStyle

```dart
TextStyle get navActionTextStyle
```

The [TextStyle] of interactive text content in navigation bars.

### pickerTextStyle

```dart
TextStyle get pickerTextStyle
```

The [TextStyle] of pickers.

### dateTimePickerTextStyle

```dart
TextStyle get dateTimePickerTextStyle
```

The [TextStyle] of date time pickers.

### resolveFrom()

```dart
CupertinoTextThemeData resolveFrom(BuildContext context)
```

Returns a copy of the current [CupertinoTextThemeData] with all the colors resolved against the given [BuildContext].

If any of the [InheritedWidget]s required to resolve this [CupertinoTextThemeData] is not found in [context], any unresolved [CupertinoDynamicColor]s will use the default trait value ([Brightness.light] platform brightness, normal contrast, [CupertinoUserInterfaceLevelData.base] elevation level).

### copyWith()

```dart
CupertinoTextThemeData copyWith({Color? primaryColor, TextStyle? textStyle, TextStyle? actionTextStyle, TextStyle? actionSmallTextStyle, TextStyle? tabLabelTextStyle, TextStyle? navTitleTextStyle, TextStyle? navLargeTitleTextStyle, TextStyle? navActionTextStyle, TextStyle? pickerTextStyle, TextStyle? dateTimePickerTextStyle})
```

Returns a copy of the current [CupertinoTextThemeData] instance with specified overrides.

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```
