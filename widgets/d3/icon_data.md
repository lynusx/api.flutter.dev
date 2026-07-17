@docImport 'dart:ui'; @docImport 'package:flutter/material.dart';

@docImport 'basic.dart'; @docImport 'icon.dart';

# IconData

```dart
final class IconData {}
```

通过字体字形实现的图标描述。

关于 Material Design 应用可用的预定义图标，参见 [Icons](https://www.yuque.com/thyname/flutter.material/icons)。

在发布构建中，Flutter 工具会将 Dart 应用代码中未被引用的字符编码（或 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 实例）从内置字体中树摇（tree shake）掉。更多细节参见 [staticIconProvider](https://www.yuque.com/thyname/flutter.widgets/staticiconprovider) 注解。

### IconData()

```dart
IconData(int codePoint, {String? fontFamily, String? fontPackage, bool matchTextDirection = false, List<String>? fontFamilyFallback})
```

创建图标数据。

很少直接使用。建议改用 [Icons](https://www.yuque.com/thyname/flutter.material/icons) 集合中的预定义图标之一。

使用自定义图标时通常需要提供 [fontFamily] 参数。

例如，当使用来自 `CustomIcons` 字体的 [codePoint] 时：

```yaml
fonts:
  - family: CustomIcons
    fonts:
      - asset: assets/fonts/CustomIcons.ttf
```

`IconData` 的使用需要指定 `fontFamily: 'CustomIcons'`。

当使用的字体族包含在某个包中时，必须提供非空的 [fontPackage] 参数。此参数用于选择字体。

在应用中实例化此类的非 const 实例意味着应用无法在发布模式下进行图标树摇构建（除非在构建时显式选择退出）。更多背景信息参见 [staticIconProvider](https://www.yuque.com/thyname/flutter.widgets/staticiconprovider)。

### codePoint

```dart
int codePoint
```

该图标在图标字体中存储位置对应的 Unicode 码点。

### fontFamily

```dart
String? fontFamily
```

用于选取 [codePoint] 对应字形的字体族。

### fontPackage

```dart
String? fontPackage
```

包含该字体族的包名称。

[Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 组件在配置 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 时会使用此名称，以便从相应资源中获取给定的 [fontFamily]。

另请参阅：

- [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle)，描述如何使用来自其他包的字体。

### matchTextDirection

```dart
bool matchTextDirection
```

在从右到左的环境中，此图标是否应自动镜像。

[Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 组件通过在 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 为 [TextDirection.rtl] 时镜像图标来遵循此值。

### fontFamilyFallback

```dart
List<String>? fontFamilyFallback
```

当某个字形无法在优先级更高的字体族中找到时，依次回退使用的字体族有序列表。

更多细节参见 [TextStyle](https://www.yuque.com/thyname/dart.ui/textstyle) 的文档。

### operator ==()

```dart
bool operator ==(Object other)
```

### hashCode

```dart
int get hashCode
```

### toString()

```dart
String toString()
```

# IconDataProperty

```dart
class IconDataProperty extends DiagnosticsProperty<IconData> {}
```

以 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 作为值的 [DiagnosticsProperty](https://www.yuque.com/thyname/flutter.foundation/diagnosticsproperty)。

### IconDataProperty()

```dart
IconDataProperty(String name, dynamic value, {dynamic ifNull, dynamic showName, dynamic style, dynamic level})
```

为 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 创建一个诊断属性。

### toJsonMap()

```dart
Map<String, Object?> toJsonMap(DiagnosticsSerializationDelegate delegate)
```

# staticIconProvider

```dart
Object staticIconProvider
```

用于标注仅提供静态 const [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 实例的类的注解。

这是给字体树摇器的一个提示，使其在为该应用打包字体时，忽略此声明中出现的常量 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 实例，不将其视为未使用的字符编码进行树摇。

带有此注解的类必须仅包含 "static const" 成员。如果存在任何非 const 的 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 实例，将导致引入该声明的应用在发布构建期间无法使用图标树摇功能。

```dart
@staticIconProvider
abstract final class MyCustomIcons {
  static const String fontFamily = 'MyCustomIcons';
  static const IconData happyFace = IconData(1, fontFamily: fontFamily);
  static const IconData sadFace = IconData(2, fontFamily: fontFamily);
}
```
