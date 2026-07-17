@docImport 'package:flutter/material.dart';

# ImageIcon

```dart
class ImageIcon extends StatelessWidget {}
```

一种来自 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 的图标，例如来自 [AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage)。

另请参阅：

- [IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton)，用于交互式图标。
- [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，提供图标的环境配置。
- [Icon](https://www.yuque.com/thyname/flutter.widgets/icon)，基于字体字形（而非图片）的图标。
- [Icons](https://www.yuque.com/thyname/flutter.material/icons)，Material 图标库。

### ImageIcon()

```dart
ImageIcon(ImageProvider? image, {dynamic key, double? size, Color? color, String? semanticLabel, bool useOriginalColors = false})
```

创建一个图片图标。

[size] 和 [color] 默认使用当前 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 提供的值。

### image

```dart
ImageProvider? image
```

要作为图标显示的图片。

该图标可以为 null，此时组件将渲染为指定 [size] 大小的空白区域。

### size

```dart
double? size
```

图标的大小，以逻辑像素为单位。

图标占据一个宽度和高度均等于 size 的正方形区域。

默认为当前 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 指定的大小（如果存在）。如果不存在 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，或其未指定明确的大小，则默认值为 24.0。

### color

```dart
Color? color
```

绘制图标时使用的颜色。

默认为当前 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 指定的颜色（如果存在）。如果不存在 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，则默认不对图片重新着色。

此外，图片还会根据当前 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的不透明度（如果存在）进行相应调整。

### semanticLabel

```dart
String? semanticLabel
```

图标的语义标签。

由辅助技术（如 TalkBack/VoiceOver）朗读。该标签不会在界面中显示。

- [SemanticsProperties.label]，该属性会在底层 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 组件中被设置为 [semanticLabel] 的值。

### useOriginalColors

```dart
bool useOriginalColors
```

是否使用图片的原始颜色进行渲染。

如果为 false（默认值），则会使用 [BlendMode.srcIn] 将 [color]（如果为 null，则使用 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的颜色）与图片进行混合着色。这是图标的标准行为。

如果为 true，则会禁用颜色混合滤镜，图片将以其原始颜色渲染。这使得诸如品牌徽标之类的多彩图片能够被准确显示。

如果此项为 true，则 [color] 必须为 null。

默认值为 false。

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
