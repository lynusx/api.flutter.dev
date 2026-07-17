@docImport 'package:flutter/material.dart';

@docImport 'app.dart'; @docImport 'image_icon.dart';

# Icon

```dart
class Icon extends StatelessWidget {}
```

一个使用 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata) 中描述的字体字形绘制的图形图标组件，例如 material 中预定义的 [IconData](https://www.yuque.com/thyname/flutter.widgets/icondata)（见 [Icons](https://www.yuque.com/thyname/flutter.material/icons)）。

图标不可交互。如需交互式图标，请考虑使用 material 的 [IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton)。

使用 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 时必须存在环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality) 组件。通常这由 [WidgetsApp](https://www.yuque.com/thyname/flutter.widgets/widgetsapp) 或 [MaterialApp](https://www.yuque.com/thyname/flutter.material/materialapp) 自动引入。

此组件假定所渲染的图标为正方形。非正方形图标可能渲染不正确。

{@tool snippet}

此示例展示了如何创建一个包含不同颜色和大小的 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 的 [Row](https://www.yuque.com/thyname/flutter.widgets/row)。第一个 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 使用了 [semanticLabel]，以便在 TalkBack 和 VoiceOver 等无障碍模式下播报。

![以下代码片段将生成一行图标，包括一个粉色的心形、一个绿色的音符和一个蓝色的沙滩伞，每个图标依次变大。](https://flutter.github.io/assets-for-api-docs/assets/widgets/icon.png)

```dart
const Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: <Widget>[
    Icon(
      Icons.favorite,
      color: Colors.pink,
      size: 24.0,
      semanticLabel: 'Text to announce in accessibility modes',
    ),
    Icon(
      Icons.audiotrack,
      color: Colors.green,
      size: 30.0,
    ),
    Icon(
      Icons.beach_access,
      color: Colors.blue,
      size: 36.0,
    ),
  ],
)
```

{@end-tool}

另请参阅：

- [IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton)，用于交互式图标。
- [Icons](https://www.yuque.com/thyname/flutter.material/icons)，用于此类可用的 Material 图标列表。
- [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，用于为图标提供环境配置。
- [ImageIcon](https://www.yuque.com/thyname/flutter.widgets/imageicon)，用于展示来自 [AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage) 或其他 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 的图标。

### Icon()

```dart
Icon(IconData? icon, {dynamic key, double? size, double? fill, double? weight, double? grade, double? opticalSize, Color? color, List<Shadow>? shadows, String? semanticLabel, TextDirection? textDirection, bool? applyTextScaling, BlendMode? blendMode, FontWeight? fontWeight})
```

创建一个图标。

### icon

```dart
IconData? icon
```

要显示的图标。可用图标详见 [Icons](https://www.yuque.com/thyname/flutter.material/icons)。

该图标可为空，此时组件将渲染为指定 [size] 大小的空白区域。

### size

```dart
double? size
```

图标的逻辑像素大小。

图标会占据一个宽高均等于 size 的正方形区域。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.size]。

如果此 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 被放置在 [IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton) 内，则应改用 [IconButton.iconSize]，以便 [IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton) 也能相应地设置合适的水波纹区域大小。[IconButton](https://www.yuque.com/thyname/flutter.material/iconbutton) 使用 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 将大小传递给 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon)。

### fill

```dart
double? fill
```

绘制图标时使用的填充度。

需要底层图标字体支持 `FILL` [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 轴，否则不生效。可变字体的文件名通常会指明其支持的轴。取值必须在 0.0（未填充）到 1.0（完全填充）之间（含端点）。

可用于表达动画或交互中的状态转换。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.fill]。

另请参阅：

- [weight]，用于控制笔画粗细。
- [grade]，用于以更精细的方式控制笔画粗细。
- [opticalSize]，用于控制视觉大小。

### weight

```dart
double? weight
```

绘制图标时使用的笔画粗细。

需要底层图标字体支持 `wght` [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 轴，否则不生效。可变字体的文件名通常会指明其支持的轴。取值必须大于 0。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.weight]。

另请参阅：

- [fill]，用于控制填充度。
- [grade]，用于以更精细的方式控制笔画粗细。
- [opticalSize]，用于控制视觉大小。
- https://fonts.google.com/knowledge/glossary/weight_axis

### grade

```dart
double? grade
```

绘制图标时使用的分级（更精细的笔画粗细）。

需要底层图标字体支持 `GRAD` [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 轴，否则不生效。可变字体的文件名通常会指明其支持的轴。取值可为负数。

分级（grade）和 [weight] 都会影响符号的笔画粗细，但分级对符号大小的影响更小。

某些文本字体也支持分级。可以在文本字体和符号字体之间匹配分级级别，以获得和谐的视觉效果。例如，如果文本字体的分级值为 -25，符号字体也可以使用合适的值（如 -25）来匹配。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.grade]。

另请参阅：

- [fill]，用于控制填充度。
- [weight]，用于以不太精细的方式控制笔画粗细。
- [opticalSize]，用于控制视觉大小。
- https://fonts.google.com/knowledge/glossary/grade_axis

### opticalSize

```dart
double? opticalSize
```

绘制图标时使用的视觉大小。

需要底层图标字体支持 `opsz` [FontVariation](https://www.yuque.com/thyname/dart.ui/fontvariation) 轴，否则不生效。可变字体的文件名通常会指明其支持的轴。取值必须大于 0。

为使图标在不同大小下看起来一致，笔画粗细必须随图标大小的缩放而变化。视觉大小提供了一种在图标大小变化时自动调整笔画粗细的方式。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.opticalSize]。

另请参阅：

- [fill]，用于控制填充度。
- [weight]，用于控制笔画粗细。
- [grade]，用于以更精细的方式控制笔画粗细。
- https://fonts.google.com/knowledge/glossary/optical_size_axis

### color

```dart
Color? color
```

绘制图标时使用的颜色。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.color]。

该颜色（无论是在此处显式指定还是从 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 获取）还会受到最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.opacity] 的进一步调整。

{@tool snippet} 通常会使用 Material Design 颜色，如下所示：

```dart
Icon(
  Icons.widgets,
  color: Colors.blue.shade400,
)
```

{@end-tool}

### shadows

```dart
List<Shadow>? shadows
```

将绘制在图标下方的一组 [Shadow](https://www.yuque.com/thyname/dart.ui/shadow)。

支持多个阴影，以模拟来自多个光源的光照效果。

多个阴影必须按相同的顺序排列，才能使 [Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 被视为等效，因为顺序会产生不同的透明度效果。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.shadows]。

### semanticLabel

```dart
String? semanticLabel
```

图标的语义标签。

由辅助技术（如 TalkBack/VoiceOver）播报。此标签不会在界面中显示。

- [SemanticsProperties.label]，在底层 [Semantics](https://www.yuque.com/thyname/flutter.widgets/semantics) 组件中设置为 [semanticLabel]。

### textDirection

```dart
TextDirection? textDirection
```

渲染图标时使用的文本方向。

如果此值为空，则改用环境 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

某些图标会跟随阅读方向变化。例如，"返回"按钮在从左到右的环境中指向左侧，在从右到左的环境中指向右侧。此类图标的 [IconData.matchTextDirection] 字段被设置为 true，[Icon](https://www.yuque.com/thyname/flutter.widgets/icon) 组件会使用 [textDirection] 来确定绘制图标的方向。

如果 [icon] 的 [IconData.matchTextDirection] 字段为 false，则此属性不起作用，但出于一致性考虑，必须始终指定文本方向值，可直接使用此属性，也可使用 [Directionality](https://www.yuque.com/thyname/flutter.widgets/directionality)。

### applyTextScaling

```dart
bool? applyTextScaling
```

是否使用环境 [MediaQuery](https://www.yuque.com/thyname/flutter.widgets/mediaquery) 的 [TextScaler](https://www.yuque.com/thyname/flutter.painting/textscaler) 缩放此组件的大小。

当图标与文本关联时，这一点尤其有用，因为仅缩放文本而不缩放图标会导致界面显得混乱。

默认为最近的 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的 [IconThemeData.applyTextScaling]。

### blendMode

```dart
BlendMode? blendMode
```

应用于图标前景的 [BlendMode](https://www.yuque.com/thyname/dart.ui/blendmode)。

默认为 [BlendMode.srcOver]

### fontWeight

```dart
FontWeight? fontWeight
```

绘制文本时使用的字体粗细（例如加粗）。

### build()

```dart
Widget build(BuildContext context)
```

### debugFillProperties()

```dart
void debugFillProperties(DiagnosticPropertiesBuilder properties)
```
