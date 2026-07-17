@docImport 'package:flutter/material.dart';

@docImport 'icon.dart'; @docImport 'image_icon.dart';

# IconTheme

```dart
class IconTheme extends InheritedTheme {}
```

控制 Widget 子树中图标的默认属性。

[Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 和 [ImageIcon](https://www.yuque.com/thyname/flutter.widgets/imageicon) 组件均遵循该图标主题。

### IconTheme()

```dart
IconTheme({dynamic key, required IconThemeData data, required Widget child})
```

创建一个用于控制后代组件属性的图标主题。

### merge()

```dart
Widget merge({Key? key, required IconThemeData data, required Widget child})
```

创建一个用于控制后代组件属性的图标主题，并与当前的图标主题（如果存在）进行合并。

### data

```dart
IconThemeData data
```

该子树中图标所使用的属性集合。

### of()

```dart
IconThemeData of(BuildContext context)
```

获取最近的此类实例（如果存在）中包含给定上下文的数据。

如果不存在环境图标主题，则默认使用 [IconThemeData.fallback]。返回的 [IconThemeData](https://www.yuque.com/thyname/flutter.widgets/iconthemedata) 是具体的（所有值均非空；参见 [IconThemeData.isConcrete]）。环境图标主题中任何为空的属性都会使用 [IconThemeData.fallback] 中指定的值作为默认值。

`material` 库中的 [Theme](https://www.yuque.com/thyname/flutter.material/theme) 组件会引入一个设置为 [ThemeData.iconTheme] 的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 组件，因此在 Material Design 应用中，图标主题通常默认取自环境 [Theme](https://www.yuque.com/thyname/flutter.material/theme)。

典型用法如下：

```dart
IconThemeData theme = IconTheme.of(context);
```

### updateShouldNotify()

```dart
bool updateShouldNotify(IconTheme oldWidget)
```

### wrap()

```dart
Widget wrap(BuildContext context, Widget child)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
