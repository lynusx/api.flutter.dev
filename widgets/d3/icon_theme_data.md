@docImport 'package:flutter/cupertino.dart'; @docImport 'package:flutter/material.dart';

@docImport 'icon.dart'; @docImport 'icon_theme.dart';

# IconThemeData

```dart
class IconThemeData with Diagnosticable {}
```

定义图标的大小、字体变化轴、颜色、不透明度和阴影。

由 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 使用，以控制 Widget 子树中的这些属性。

要获取当前的图标主题，请使用 [IconTheme.of]。要将图标主题转换为所有字段均已填充的版本，请使用 [IconThemeData.fallback]。

### IconThemeData()

```dart
IconThemeData({double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, double? opacity, List<Shadow>? shadows, bool? applyTextScaling})
```

创建图标主题数据。

不透明度同时应用于显式指定的图标颜色和默认图标颜色。该值会被限制在 0.0 到 1.0 之间。

### IconThemeData.fallback()

```dart
IconThemeData.fallback()
```

创建一个具有合理默认值的图标主题。

[size] 为 24.0，[fill] 为 0.0，[weight] 为 400.0，[grade] 为 0.0，opticalSize 为 48.0，[color] 为黑色，[opacity] 为 1.0。

### copyWith()

```dart
IconThemeData copyWith({double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, double? opacity, List<Shadow>? shadows, bool? applyTextScaling})
```

创建此图标主题的副本，并将给定字段替换为新值。

### merge()

```dart
IconThemeData merge(IconThemeData? other)
```

返回一个新的图标主题，该主题与此图标主题相匹配，但会用给定图标主题中的非空参数替换部分值。如果给定的图标主题为空，则返回此图标主题本身。

### resolve()

```dart
IconThemeData resolve(BuildContext context)
```

由 [IconTheme.of] 调用，用于将此实例转换为适配给定 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 的 [IconThemeData](https://www.yuque.com/thyname/flutter.widgets/iconthemedata)。

此方法使环境 [IconThemeData](https://www.yuque.com/thyname/flutter.widgets/iconthemedata) 有机会在被 [IconTheme.of] 获取之后、作为最终结果返回之前进行自我更新。例如，[CupertinoIconThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinoiconthemedata) 重写了此方法，用于在 [color] 是 [CupertinoDynamicColor](https://www.yuque.com/thyname/flutter.cupertino/cupertinodynamiccolor) 的情况下，在其作为常规 [Color](https://www.yuque.com/thyname/dart.ui/color) 使用之前根据给定的 [BuildContext](https://www.yuque.com/thyname/flutter.widgets/buildcontext) 对其进行解析。

默认实现按原样返回此 [IconThemeData](https://www.yuque.com/thyname/flutter.widgets/iconthemedata)。

另请参阅：

- [CupertinoIconThemeData.resolve]，一种在返回之前解析 [CupertinoIconThemeData](https://www.yuque.com/thyname/flutter.cupertino/cupertinoiconthemedata) 颜色的实现。

### isConcrete

```dart
bool get isConcrete
```

此对象的所有属性（[shadows] 除外）是否均为非空。

### size

```dart
double? size
```

[Icon.size] 的默认值。

回退为 24.0。

### fill

```dart
double? fill
```

[Icon.fill] 的默认值。

回退为 0.0。

### weight

```dart
double? weight
```

[Icon.weight] 的默认值。

回退为 400.0。

### grade

```dart
double? grade
```

[Icon.grade] 的默认值。

回退为 0.0。

### opticalSize

```dart
double? opticalSize
```

[Icon.opticalSize] 的默认值。

回退为 48.0。

### color

```dart
Color? color
```

[Icon.color] 的默认值。

在 Material 应用中，如果存在 [Theme](https://www.yuque.com/thyname/flutter.material/theme) 但未指定任何 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，则当 [ThemeData.brightness] 为深色（dark）时，图标颜色默认为白色；为浅色（light）时，默认为黑色。

否则，回退为黑色。

### opacity

```dart
double? get opacity
```

同时应用于显式指定的图标颜色和默认图标颜色的不透明度。

回退为 1.0。

### shadows

```dart
List<Shadow>? shadows
```

[Icon.shadows] 的默认值。

### applyTextScaling

```dart
bool? applyTextScaling
```

[Icon.applyTextScaling] 的默认值。

### lerp()

```dart
IconThemeData lerp(IconThemeData? a, IconThemeData? b, double t)
```

在两个图标主题数据对象之间进行线性插值。

{@macro dart.ui.shadow.lerp}

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
