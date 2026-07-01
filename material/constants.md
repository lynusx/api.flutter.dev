@docImport 'package:flutter/cupertino.dart';

@docImport 'app_bar.dart'; @docImport 'icon_button.dart'; @docImport 'tabs.dart'; @docImport 'theme_data.dart';

# kMinInteractiveDimension

```dart
double kMinInteractiveDimension
```

The minimum dimension of any interactive region according to Material guidelines.

This is used to avoid small regions that are hard for the user to interact with. It applies to both dimensions of a region, so a square of size kMinInteractiveDimension x kMinInteractiveDimension is the smallest acceptable region that should respond to gestures.

See also:

- [kMinInteractiveDimensionCupertino]
- The Material spec on touch targets at <https://material.io/design/usability/accessibility.html#layout-typography>.

# kToolbarHeight

```dart
double kToolbarHeight
```

The height of the toolbar component of the [AppBar].

# kBottomNavigationBarHeight

```dart
double kBottomNavigationBarHeight
```

The height of the bottom navigation bar.

# kTextTabBarHeight

```dart
double kTextTabBarHeight
```

The height of a tab bar containing text.

# kThemeChangeDuration

```dart
Duration kThemeChangeDuration
```

The amount of time theme change animations should last.

# kRadialReactionRadius

```dart
double kRadialReactionRadius
```

The default radius of a circular material ink response in logical pixels.

# kRadialReactionDuration

```dart
Duration kRadialReactionDuration
```

The amount of time a circular material ink response should take to expand to its full size.

# kRadialReactionAlpha

```dart
int kRadialReactionAlpha
```

The value of the alpha channel to use when drawing a circular material ink response.

# kTabScrollDuration

```dart
Duration kTabScrollDuration
```

The duration of the horizontal scroll animation that occurs when a tab is tapped.

# kTabLabelPadding

```dart
EdgeInsets kTabLabelPadding
```

The horizontal padding included by [Tab]s.

# kMaterialListPadding

```dart
EdgeInsets kMaterialListPadding
```

The padding added around material list items.

# kDefaultIconLightColor

```dart
Color kDefaultIconLightColor
```

The default color for [ThemeData.iconTheme] when [ThemeData.brightness] is [Brightness.dark]. This color is used in [IconButton] to detect whether [IconTheme.of(context).color] is the same as the default color of [ThemeData.iconTheme].

# kDefaultIconDarkColor

```dart
Color kDefaultIconDarkColor
```

The default color for [ThemeData.iconTheme] when [ThemeData.brightness] is [Brightness.light]. This color is used in [IconButton] to detect whether [IconTheme.of(context).color] is the same as the default color of [ThemeData.iconTheme].
