@docImport 'icon.dart'; @docImport 'image_icon.dart';

# FlutterLogo

```dart
class FlutterLogo extends StatelessWidget {}
```

Widget 形式的 Flutter 徽标。此组件遵循 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)。有关使用 Flutter 徽标的准则，请访问 https://flutter.dev/brand。

{@youtube 560 315 https://www.youtube.com/watch?v=aAmP-WcI6dg}

另请参阅：

- [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，用于为图标提供环境配置。
- [Icon](https://www.yuque.com/thyname/flutter.widgets/icon)，用于展示 Material 设计图标库中的图标。
- [ImageIcon](https://www.yuque.com/thyname/flutter.widgets/imageicon)，用于展示来自 [AssetImage](https://www.yuque.com/thyname/flutter.painting/assetimage) 或其他 [ImageProvider](https://www.yuque.com/thyname/flutter.painting/imageprovider) 的图标。

### FlutterLogo()

```dart
FlutterLogo({dynamic key, double? size, Color textColor = const Color(0xFF757575), FlutterLogoStyle style = FlutterLogoStyle.markOnly, Duration duration = const Duration(milliseconds: 750), Curve curve = Curves.fastOutSlowIn})
```

创建一个用于绘制 Flutter 徽标的组件。

### size

```dart
double? size
```

徽标的逻辑像素大小。

徽标将被适配到这个大小的正方形区域内。

默认为当前 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme) 的大小。如果不存在 [IconTheme](https://www.yuque.com/thyname/flutter.widgets/icontheme)，或其未指定明确的大小，则默认为 24.0。

### textColor

```dart
Color textColor
```

用于绘制徽标上 "Flutter" 文字的颜色，当 [style] 为 [FlutterLogoStyle.horizontal] 或 [FlutterLogoStyle.stacked] 时生效。

如果可能，应在白色背景下使用默认值（中灰色）。

### style

```dart
FlutterLogoStyle style
```

是否绘制以及在何处绘制 "Flutter" 文字。默认仅绘制徽标本身。

### duration

```dart
Duration duration
```

当 [style] 或 [textColor] 属性发生变化时，动画持续的时长。

### curve

```dart
Curve curve
```

当 [style] 或 [textColor] 发生变化时，徽标动画所使用的曲线。
